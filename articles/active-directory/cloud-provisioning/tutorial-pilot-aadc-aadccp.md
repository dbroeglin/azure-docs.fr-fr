---
title: Tutoriel – Piloter le provisionnement cloud Azure AD Connect pour une forêt AD synchronisée
description: tutoriel.
services: active-directory
author: billmath
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.topic: overview
ms.date: 12/05/2019
ms.subservice: hybrid
ms.author: billmath
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0bd53b72c334b35daea0864acf61cc432c272ae
ms.sourcegitcommit: 6e87ddc3cc961945c2269b4c0c6edd39ea6a5414
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2020
ms.locfileid: "77442120"
---
# <a name="pilot-cloud-provisioning-for-an-existing-synced-ad-forest"></a>Provisionnement cloud pilote pour une forêt AD synchronisée existante 

Ce tutoriel vous guide tout au long du pilotage du provisionnement cloud pour une forêt Active Directory test déjà synchronisée à l’aide de la synchronisation Azure Active Directory (Azure AD) Connect.

![Créer](media/tutorial-migrate-aadc-aadccp/diagram.png)

## <a name="considerations"></a>Considérations
Avant de suivre ce tutoriel, tenez compte des éléments suivants :
1. Vous devez bien connaître les principes de base du provisionnement cloud. 
2. Veillez à exécuter la synchronisation Azure AD Connect version 1.4.32.0 ou ultérieure et à configurer les règles de synchronisation stipulées. Pendant la procédure, vous allez supprimer un groupe ou une unité d’organisation de test de l’étendue de la synchronisation Azure AD Connect. Le déplacement d’objets en dehors de l’étendue provoque la suppression de ces objets dans Azure AD. Dans le cas d’objets utilisateur, les objets figurant dans Azure AD sont supprimés de façon réversible et peuvent être restaurés. Dans le cas d’objets de groupe, les objets figurant dans Azure AD sont supprimés définitivement et ne peuvent pas être restaurés. Un nouveau type de lien a été introduit dans la synchronisation Azure AD Connect, qui empêchera la suppression dans le cas d’un scénario de pilotage. 
3. Vérifiez que ms-ds-consistencyGUID a été renseigné pour les objets figurant dans l’étendue pilote afin d’avoir une correspondance exacte entre le provisionnement cloud et les objets. 

   > [!NOTE]
   > La synchronisation Azure AD Connect ne renseigne pas *ms-ds-consistencyGUID* par défaut pour les objets de groupe. Suivez les étapes décrites dans [ce billet de blog](https://blogs.technet.microsoft.com/markrenoden/2017/10/13/choosing-a-sourceanchor-for-groups-in-multi-forest-sync-with-aad-connect/) pour renseigner *ms-ds-consistencyGUID* pour les objets de groupe.

4. Il s’agit d’un scénario avancé. Veillez à suivre avec précision les étapes décrites dans ce tutoriel.

## <a name="prerequisites"></a>Prérequis
Voici les conditions préalables requises pour suivre ce didacticiel.
- Un environnement de test avec la synchronisation Azure AD Connect version 1.4.32.0 ou ultérieure
- Une unité d’organisation ou un groupe figurant dans l’étendue de la synchronisation et pouvant servir de pilote. Nous vous recommandons de commencer avec un ensemble réduit d’objets.
- Un serveur exécutant Windows Server 2012 R2 ou ultérieur, qui hébergera l’agent de provisionnement.  Ce serveur ne peut pas être identique au serveur Azure AD Connect.
- L’ancre source pour la synchronisation AAD Connect doit être *objectGuid* ou *ms-ds-consistencyGUID*

## <a name="update-azure-ad-connect"></a>Mettre à jour Azure AD Connect

Au minimum, vous devez disposer d’[Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594)1.4.32.0. Pour mettre à jour la synchronisation Azure AD Connect, suivez les étapes décrites dans [Azure AD Connect : Mettre à niveau vers la version la plus récente](../hybrid/how-to-upgrade-previous-version.md).  

## <a name="stop-the-scheduler"></a>Arrêter le planificateur
La synchronisation Azure AD Connect synchronise les modifications intervenant dans votre annuaire local à l’aide d’un planificateur. Pour pouvoir modifier et ajouter des règles personnalisées, vous pouvez désactiver le planificateur pour que les synchronisations ne s’exécutent pas pendant que vous travaillez à cette tâche.  Utiliser les étapes suivantes :

1.  Sur le serveur qui exécute la synchronisation Azure AD Connect, ouvrez PowerShell avec des privilèges d’administrateur.
2.  Exécutez `Stop-ADSyncSyncCycle`.  Appuyez sur Entrée.
3.  Exécutez `Set-ADSyncScheduler -SyncCycleEnabled $false`.

>[!NOTE] 
>Si vous exécutez votre propre planificateur personnalisé pour la synchronisation AAD Connect, désactivez le planificateur. 

## <a name="create-custom-user-inbound-rule"></a>Créer une règle personnalisée de trafic entrant utilisateur

 1. Exécutez l’éditeur de synchronisation à partir d’un menu d’application dans le poste de travail comme indiqué ci-après :</br>
 ![Menu de l’Éditeur de règles de synchronisation](media/how-to-cloud-custom-user-rule/user8.png)</br>
 
 2. Sélectionnez **Inbound** (Entrant) dans la liste déroulante Direction, puis cliquez sur **Add new rule** (Ajouter une nouvelle règle).
 ![Règle personnalisée](media/how-to-cloud-custom-user-rule/user1.png)</br>
 
 3. Dans la page **Description**, entrez les informations ci-dessous et cliquez sur **Suivant** :

    **Nom :** attribuez un nom explicite à la règle.<br>
    **Description :** ajoutez une description explicite.<br>
    **Connected System** (Système connecté) : choisissez le connecteur AD pour lequel vous écrivez la règle de synchronisation personnalisée.<br>
    **Connected System Object Type** (Type d’objet système connecté) : Utilisateur<br>
    **Metaverse Object Type** (Type d’objet métaverse) : Personne<br>
    **Link Type** (Type de lien) : Join<br>
    **Precedence** (Précédence) : indiquez une valeur unique dans le système.<br>
    **Tag** (Balise) : laissez ce champ vide.<br>
    ![Règle personnalisée](media/how-to-cloud-custom-user-rule/user2.png)</br>
 
 4. Dans la page **Scoping filter** (Filtre d’étendue), entrez l’unité d’organisation ou le groupe de sécurité sur lesquels vous souhaitez que le pilote s’appuie.  Pour filtrer sur l’unité d’organisation, ajoutez la partie UO du nom unique. Cette règle s’appliquera à tous les utilisateurs qui se trouvent dans cette unité d’organisation.  Par conséquent, si DN se termine par « OU=CPUsers,DC=contoso,DC=com », vous devez ajouter ce filtre.  Cliquez ensuite sur **Suivant**. 

    |Règle|Attribut|Opérateur|Valeur|
    |-----|----|----|-----|
    |Étendue d’unité d’organisation|DN|ENDSWITH|Nom unique de l’unité d’organisation.|
    |Étendue de groupe||ISMEMBEROF|Nom unique du groupe de sécurité.|

    ![Règle personnalisée](media/how-to-cloud-custom-user-rule/user3.png)</br>
 
 5. Dans la page **Join rules** (Règles de jointure), cliquez sur **Suivant**.
 6. Dans la page **Transformations**, ajoutez une transformation constante : spécifiez True pour l’attribut cloudNoFlow. Cliquez sur **Add**.
 ![Règle personnalisée](media/how-to-cloud-custom-user-rule/user4.png)</br>

Les mêmes étapes doivent être suivies pour tous les types d’objets (utilisateur, groupe et contact). Répétez les étapes par connecteur AD configuré/par forêt AD. 

## <a name="create-custom-user-outbound-rule"></a>Créer une règle personnalisée de trafic sortant utilisateur

 1. Sélectionnez **Outbound** (Sortant) dans la liste déroulante Direction, puis cliquez sur **Add new rule** (Ajouter une nouvelle règle).
 ![Règle personnalisée](media/how-to-cloud-custom-user-rule/user5.png)</br>
 
 2. Dans la page **Description**, entrez les informations ci-dessous et cliquez sur **Suivant** :

    **Nom :** attribuez un nom explicite à la règle.<br>
    **Description :** ajoutez une description explicite.<br>
    **Connected System** (Système connecté) : Choisissez le connecteur AAD pour lequel vous écrivez la règle de synchronisation personnalisée.<br>
    **Connected System Object Type** (Type d’objet système connecté) : Utilisateur<br>
    **Metaverse Object Type** (Type d’objet métaverse) : Personne<br>
    **Link Type** (Type de lien) : JoinNoFlow<br>
    **Precedence** (Précédence) : indiquez une valeur unique dans le système.<br>
    **Tag** (Balise) : laissez ce champ vide.<br>
    
    ![Règle personnalisée](media/how-to-cloud-custom-user-rule/user6.png)</br>
 
 3. Dans la page **Scoping filter** (Filtre d’étendue), choisissez **cloudNoFlow** EQUAL **True**. Cliquez ensuite sur **Suivant**.
 ![Règle personnalisée](media/how-to-cloud-custom-user-rule/user7.png)</br>
 
 4. Dans la page **Join rules** (Règles de jointure), cliquez sur **Suivant**.
 5. Dans la page **Transformations**, cliquez sur **Add** (Ajouter).

Les mêmes étapes doivent être suivies pour tous les types d’objets (utilisateur, groupe et contact).

## <a name="install-the-azure-ad-connect-provisioning-agent"></a>Installer l’agent de provisionnement Azure AD Connect
1. Connectez-vous au serveur que vous allez utiliser à l’aide des autorisations d’administrateur d’entreprise.  Si vous utilisez le tutoriel [Environnement de base Active Directory et Azure](tutorial-basic-ad-azure.md), il s’agit de CP1.
2. Téléchargez l’agent de provisionnement cloud Azure AD Connect [ici](https://go.microsoft.com/fwlink/?linkid=2109037).
3. Exécuter le provisionnement cloud Azure AD Connect (AADConnectProvisioningAgent.Installer)
3. Dans l’écran de démarrage, **acceptez** les termes du contrat de licence et cliquez sur **Installer**.</br>
![Écran d’accueil](media/how-to-install/install1.png)</br>

4. Une fois cette opération terminée, l’Assistant de configuration démarre.  Connectez-vous avec votre compte d’administrateur général Azure AD.
5. Dans l’écran **Connexion à Active Directory**, cliquez sur **Ajout d’un annuaire**, puis connectez-vous avec votre compte d’administrateur Active Directory.  Cette opération ajoute votre annuaire local.  Cliquez sur **Suivant**.</br>
![Écran d’accueil](media/how-to-install/install3.png)</br>

6. Dans l’écran **Configuration terminée**, cliquez sur **Confirmer**.  Cette opération inscrit et redémarre l’agent.</br>
![Écran d’accueil](media/how-to-install/install4.png)</br>

7. Une fois cette opération terminée, vous devriez voir une notification : **La configuration de votre agent a été vérifiée avec succès.**  Vous pouvez cliquer sur **Quitter**.</br>
![Écran d’accueil](media/how-to-install/install5.png)</br>
8. Si vous voyez encore l’écran de démarrage initial, cliquez sur **Fermer**.

## <a name="verify-agent-installation"></a>Vérifier l’installation de l’agent
La vérification de l’agent se produit dans le portail Azure et sur le serveur local qui exécute l’agent.

### <a name="azure-portal-agent-verification"></a>Vérification de l’agent dans le portail Azure
Pour vérifier que l’agent est visible par Azure, procédez comme suit :

1. Connectez-vous au portail Azure.
2. Sur la gauche, sélectionnez **Azure Active Directory**, cliquez sur **Azure AD Connect** et, au centre, sélectionnez **Gérer le provisionnement (préversion)** .</br>
![Azure portal](media/how-to-install/install6.png)</br>

3.  Dans l’écran **Provisionnement Azure AD (préversion)** , cliquez sur **Passer en revue tous les agents**.
![Provisionnement Azure AD](media/how-to-install/install7.png)</br>
 
4. Dans l’écran **Agents de provisionnement locaux**, vous voyez les agents que vous avez installés.  Vérifiez que l’agent en question est présent et qu’il est marqué comme étant **désactivé**.  L’agent est désactivé par défaut par défaut parmi les ![agents de provisionnement](media/how-to-install/verify1.png)</br>

### <a name="on-the-local-server"></a>Sur le serveur local
Pour vérifier que l’agent est en cours d’exécution, effectuez les étapes suivantes :

1.  Connectez-vous au serveur avec un compte administrateur.
2.  Ouvrez **Services** en y accédant ou en accédant à Démarrer/Exécuter/Services.msc.
3.  Sous **Services**, assurez-vous que le **Programme de mise à jour de l’agent Microsoft Azure AD Connect** et l’**Agent de provisionnement Microsoft Azure AD Connect** sont présents, et que leur état est **En cours d’exécution**.
![Services](media/how-to-troubleshoot/troubleshoot1.png)

## <a name="configure-azure-ad-connect-cloud-provisioning"></a>Configurer le provisionnement cloud Azure AD Connect
Pour configurer le provisionnement, procédez comme suit :

 1. Connectez-vous au portail Azure AD.
 2. Cliquez sur **Azure Active Directory**.
 3. Cliquez sur **Azure AD Connect**.
 4. Sélectionnez **Gérer le provisionnement (préversion)** 
 ![](media/how-to-configure/manage1.png).</br>
 5.  Cliquez sur **Nouvelle configuration**
 ![](media/tutorial-single-forest/configure1.png).</br>
 6.  Dans l’écran de configuration, entrez une adresse **e-mail de notification**, déplacez le sélecteur sur **Activer** et cliquez sur **Enregistrer**.
 ![](media/tutorial-single-forest/configure2.png)</br>
 7. Sous **Configurer**, sélectionnez **Tous les utilisateurs** pour modifier l’étendue de la règle de configuration.
 ![](media/how-to-configure/scope2.png)</br>
 8. Sur la droite, modifiez l’étendue pour inclure l’unité d’organisation spécifique que vous venez de créer : « OU=CPUsers,DC=contoso,DC=com ».
 ![](media/tutorial-existing-forest/scope2.png)</br>
 9.  Cliquez sur **Terminé**, puis sur **Enregistrer**.
 10. L’étendue doit maintenant être définie sur une unité d’organisation. 
 ![](media/tutorial-existing-forest/scope3.png)</br>
 

## <a name="verify-users-are-provisioned-by-cloud-provisioning"></a>Vérifier que les utilisateurs sont provisionnés par provisionnement cloud
Vous allez maintenant vérifier que les utilisateurs de l’annuaire local ont été synchronisés et figurent maintenant dans le locataire Azure AD.  Cette opération peut prendre quelques heures.  Pour vérifier que les utilisateurs sont provisionnés par provisionnement cloud, procédez comme suit :

1. Accédez au [portail Azure](https://portal.azure.com) et connectez-vous avec un compte qui dispose d’un abonnement Azure.
2. À gauche, sélectionnez **Azure Active Directory**
3. Cliquez sur **Azure AD Connect**.
4. Cliquez sur **Gérer le provisionnement (préversion)** .
5. Cliquez sur le bouton **Journaux**.
6. Recherchez un nom d’utilisateur pour confirmer que l’utilisateur est provisionné par provisionnement cloud.

De plus, vous pouvez vérifier que l’utilisateur et le groupe existent dans Azure AD.

## <a name="start-the-scheduler"></a>Démarrer le planificateur
La synchronisation Azure AD Connect synchronise les modifications intervenant dans votre annuaire local à l’aide d’un planificateur. Maintenant que vous avez modifié les règles, vous pouvez redémarrer le planificateur.  Utiliser les étapes suivantes :

1.  Sur le serveur qui exécute la synchronisation Azure AD Connect, ouvrez PowerShell avec des privilèges d’administrateur.
2.  Exécutez `Set-ADSyncScheduler -SyncCycleEnabled $true`.
3.  Exécutez `Start-ADSyncSyncCycle`.  Appuyez sur Entrée.  

>[!NOTE] 
>Si vous exécutez votre propre planificateur personnalisé pour la synchronisation AAD Connect, activez le planificateur. 

## <a name="something-went-wrong"></a>Survenue d’un problème
Si le pilote ne fonctionne pas comme prévu, vous pouvez revenir à la configuration de la synchronisation Azure AD Connect en suivant les étapes ci-dessous :
1.  Désactivez la configuration du provisionnement dans le portail Azure. 
2.  Désactivez toutes les règles de synchronisation personnalisées créées pour le provisionnement cloud à l’aide de l’Éditeur de règles de synchronisation. La désactivation doit entraîner une synchronisation complète sur tous les connecteurs.

## <a name="configure-azure-ad-connect-sync-to-exclude-the-pilot-ou"></a>Configurer la synchronisation Azure AD Connect pour exclure l’unité d’organisation pilote
Une fois que vous avez vérifié que les utilisateurs de l’unité d’organisation pilote sont correctement managés par le provisionnement cloud, vous pouvez reconfigurer Azure AD Connect pour exclure l’unité d’organisation pilote créée ci-dessus.  L’agent de provisionnement cloud va gérer la synchronisation pour ces utilisateurs à partir de maintenant.  Suivez les étapes ci-dessous pour définir l’étendue d’Azure AD Connect.

 1. Sur le serveur qui exécute Azure AD Connect, double-cliquez sur l’icône Azure AD Connect.
 2. Cliquez sur **Configurer**
 3. Sélectionnez **Personnalisation des options de synchronisation**, puis cliquez sur Suivant.
 4. Connectez-vous à Azure AD, puis cliquez sur **Suivant**.
 5. Dans l’écran **Connexion de vos annuaires**, cliquez sur **Suivant**.
 6. Dans l’écran **Filtrage par domaine ou unité d’organisation**, sélectionnez **Synchroniser les domaines et les unités d’organisation sélectionnés**.
 7. Développez votre domaine et **désélectionnez** l’unité d’organisation **CPUsers**.  Cliquez sur **Suivant**.
![scope](media/tutorial-existing-forest/scope1.png)</br>
 9. Dans l’écran **Fonctionnalités facultatives**, cliquez sur **Suivant**.
 10. Dans l’écran **Prêt à configurer**, cliquez sur **Configurer**.
 11. Une fois cette opération terminée, cliquez sur **Quitter**. 

## <a name="next-steps"></a>Étapes suivantes 

- [Présentation du provisionnement](what-is-provisioning.md)
- [Présentation du provisionnement cloud Azure AD Connect](what-is-cloud-provisioning.md)

