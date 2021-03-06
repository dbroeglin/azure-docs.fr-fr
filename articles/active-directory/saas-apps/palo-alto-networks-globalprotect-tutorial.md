---
title: 'Didacticiel : Intégration de l’authentification unique Azure Active Directory à Palo Alto Networks - GlobalProtect | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et Palo Alto Networks - GlobalProtect.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 03bef6f2-3ea2-4eaa-a828-79c5f1346ce5
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 08/23/2019
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8faa1d0ecfec629487c9cddee6a01fb9f809393f
ms.sourcegitcommit: 19a821fc95da830437873d9d8e6626ffc5e0e9d6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70165982"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-palo-alto-networks---globalprotect"></a>Didacticiel : Intégration de l’authentification unique Azure Active Directory à Palo Alto Networks - GlobalProtect

Dans ce tutoriel, vous allez découvrir comment intégrer Palo Alto Networks - GlobalProtect à Azure Active Directory (Azure AD). Quand vous intégrez Palo Alto Networks - GlobalProtect à Azure AD, vous pouvez :

* Contrôler dans Azure AD qui a accès à Palo Alto Networks - GlobalProtect.
* Permettre à vos utilisateurs de se connecter automatiquement à Palo Alto Networks - GlobalProtect avec leur compte Azure AD.
* Gérer vos comptes à un emplacement central : le Portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS à Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).

## <a name="prerequisites"></a>Prérequis

Pour commencer, vous devez disposer de ce qui suit :

* Un abonnement Azure AD Si vous ne disposez d’aucun abonnement, vous pouvez obtenir [un compte gratuit](https://azure.microsoft.com/free/).
* Un abonnement Palo Alto Networks - GlobalProtect pour lequel l’authentification unique est activée

## <a name="scenario-description"></a>Description du scénario

Dans ce tutoriel, vous allez configurer et tester l’authentification unique Azure AD dans un environnement de test.

* Palo Alto Networks - GlobalProtect prend en charge l’authentification unique initiée par le **fournisseur de services**.
* Palo Alto Networks - GlobalProtect prend en charge l’approvisionnement utilisateur **juste-à-temps**.

## <a name="adding-palo-alto-networks---globalprotect-from-the-gallery"></a>Ajout de Palo Alto Networks - GlobalProtect depuis la galerie

Pour configurer l’intégration de Palo Alto Networks - GlobalProtect à Azure AD, vous devez ajouter Palo Alto Networks - GlobalProtect à partir de la galerie à votre liste d’applications SaaS gérées.

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec un compte professionnel ou scolaire ou avec un compte personnel Microsoft.
1. Dans le panneau de navigation gauche, sélectionnez le service **Azure Active Directory**.
1. Accédez à **Applications d’entreprise**, puis sélectionnez **Toutes les applications**.
1. Pour ajouter une nouvelle application, sélectionnez **Nouvelle application**.
1. Dans la section **Ajouter à partir de la galerie**, tapez **Palo Alto Networks - GlobalProtect** dans la zone de recherche.
1. Sélectionnez **Palo Alto Networks - GlobalProtect** dans le volet de résultats, puis ajoutez l’application. Patientez quelques secondes pendant que l’application est ajoutée à votre locataire.

## <a name="configure-and-test-azure-ad-single-sign-on-for-palo-alto-networks---globalprotect"></a>Configurer et tester l’authentification unique Azure AD pour Palo Alto Networks - GlobalProtect

Configurez et testez l’authentification unique Azure AD avec Palo Alto Networks - GlobalProtect pour un utilisateur de test nommé **B.Simon**. Pour que l’authentification unique fonctionne, vous devez établir un lien entre un utilisateur Azure AD et l’utilisateur Palo Alto Networks - GlobalProtect associé.

Pour configurer et tester l’authentification unique Azure AD avec Palo Alto Networks - GlobalProtect, suivez les indications des sections suivantes :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-sso)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
    1. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec B. Simon.
    1. **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à B. Simon d’utiliser l’authentification unique Azure AD.
1. **[Configurer l’authentification unique Palo Alto Networks - GlobalProtect](#configure-palo-alto-networks---globalprotect-sso)** pour configurer les paramètres de l’authentification unique côté application.
    1. **[Créer un utilisateur de test Palo Alto Networks - GlobalProtect](#create-palo-alto-networks---globalprotect-test-user)** pour obtenir un équivalent de B.Simon dans Palo Alto Networks - GlobalProtect lié à la représentation Azure AD associée.
1. **[Tester l’authentification unique](#test-sso)** pour vérifier si la configuration fonctionne.

## <a name="configure-azure-ad-sso"></a>Configurer l’authentification unique Azure AD

Effectuez les étapes suivantes pour activer l’authentification unique Azure AD dans le Portail Azure.

1. Dans le [portail Azure](https://portal.azure.com/), dans la page d’intégration de l’application **Palo Alto Networks - GlobalProtect**, recherchez la section **Gérer** et sélectionnez **Authentification unique**.
1. Dans la page **Sélectionner une méthode d’authentification unique**, sélectionnez **SAML**.
1. Dans la page **Configurer l’authentification unique avec SAML**, cliquez sur l’icône de modification/stylet de **Configuration SAML de base** pour modifier les paramètres.

   ![Modifier la configuration SAML de base](common/edit-urls.png)

1. Dans la section **Configuration SAML de base**, entrez les valeurs pour les champs suivants :

    a. Dans la zone de texte **URL de connexion**, saisissez une URL au format suivant : `https://<Customer Firewall URL>`

    b. Dans la zone de texte **Identificateur (ID d’entité)** , saisissez une URL au format suivant : `https://<Customer Firewall URL>/SAML20/SP`

    > [!NOTE]
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels. Contactez [l’équipe de support client de Palo Alto Networks - GlobalProtect](https://support.paloaltonetworks.com/support) pour obtenir ces valeurs. Vous pouvez également consulter les modèles figurant à la section **Configuration SAML de base** dans le portail Azure.

1. Dans la page **Configurer l’authentification unique avec SAML**, dans la section **Certificat de signature SAML**, recherchez **XML de métadonnées de fédération**, puis sélectionnez **Télécharger** pour télécharger le certificat et l’enregistrer sur votre ordinateur.

    ![Lien Téléchargement de certificat](common/metadataxml.png)

1. Dans la section **Configurer Palo Alto Networks - GlobalProtect**, copiez les URL appropriées en fonction de vos besoins.

    ![Copier les URL de configuration](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

Dans cette section, vous allez créer un utilisateur de test appelé B. Simon dans le portail Azure.

1. Dans le volet gauche du Portail Azure, sélectionnez **Azure Active Directory**, **Utilisateurs**, puis **Tous les utilisateurs**.
1. Sélectionnez **Nouvel utilisateur** dans la partie supérieure de l’écran.
1. Dans les propriétés **Utilisateur**, effectuez les étapes suivantes :
   1. Dans le champ **Nom**, entrez `B.Simon`.  
   1. Dans le champ **Nom de l’utilisateur**, entrez username@companydomain.extension. Par exemple : `B.Simon@contoso.com`.
   1. Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.
   1. Cliquez sur **Créer**.

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous autorisez B.Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Palo Alto Networks - GlobalProtect.

1. Dans le portail Azure, sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.
1. Dans la liste des applications, sélectionnez **Palo Alto Networks - GlobalProtect**.
1. Dans la page de vue d’ensemble de l’application, recherchez la section **Gérer** et sélectionnez **Utilisateurs et groupes**.

   ![Lien « Utilisateurs et groupes »](common/users-groups-blade.png)

1. Sélectionnez **Ajouter un utilisateur**, puis **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une attribution**.

    ![Lien Ajouter un utilisateur](common/add-assign-user.png)

1. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **B. Simon** dans la liste Utilisateurs, puis cliquez sur le bouton **Sélectionner** au bas de l’écran.
1. Si vous attendez une valeur de rôle dans l’assertion SAML, dans la boîte de dialogue **Sélectionner un rôle**, sélectionnez le rôle approprié pour l’utilisateur dans la liste, puis cliquez sur le bouton **Sélectionner** en bas de l’écran.
1. Dans la boîte de dialogue **Ajouter une attribution**, cliquez sur le bouton **Attribuer**.

## <a name="configure-palo-alto-networks---globalprotect-sso"></a>Configurer l’authentification unique pour Palo Alto Networks - GlobalProtect

1. Ouvrez l’interface utilisateur de l’administration du pare-feu Palo Alto Networks en tant qu’administrateur dans une autre fenêtre de navigateur.

2. Cliquez sur **Appareil**.

    ![Configurer l’authentification unique Palo Alto](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoadmin_admin1.png)

3. Sélectionnez **Fournisseur d’identité SAML** dans la barre de navigation gauche et cliquez sur « Importer » pour importer le fichier de métadonnées.

    ![Configurer l’authentification unique Palo Alto](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoadmin_admin2.png)

4. Effectuez les actions suivantes sur la fenêtre Importer

    ![Configurer l’authentification unique Palo Alto](./media/paloaltoglobalprotect-tutorial/tutorial_paloaltoadmin_admin3.png)

    a. Dans la zone de texte **Nom du profil**, spécifiez un nom, par exemple Azure AD GlobalProtect.

    b. Dans **Métadonnées du fournisseur d’identité**, cliquez sur **Parcourir** et sélectionnez le fichier metadata.xml que vous avez téléchargé à partir du portail Azure.

    c. Cliquez sur **OK**

### <a name="create-palo-alto-networks---globalprotect-test-user"></a>Créer un utilisateur de test Palo Alto Networks - GlobalProtect

Dans cette section, vous allez créer un utilisateur nommé B.Simon dans Palo Alto Networks - GlobalProtect. Palo Alto Networks - GlobalProtect prend en charge l’approvisionnement utilisateur juste-à-temps, qui est activé par défaut. Vous n’avez aucune opération à effectuer dans cette section. S’il n’existe pas encore d’utilisateur dans Palo Alto Networks - GlobalProtect, il en est créé un après l’authentification.

## <a name="test-sso"></a>Tester l’authentification unique (SSO) 

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Quand vous cliquez sur la vignette Palo Alto Networks - GlobalProtect dans le panneau d’accès, vous devez être connecté automatiquement à l’application Palo Alto Networks - GlobalProtect pour laquelle vous avez configuré l’authentification unique. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Ressources supplémentaires

- [Liste de tutoriels sur l’intégration d’applications SaaS avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Qu’est-ce que l’accès conditionnel dans Azure Active Directory ?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Essayer Palo Alto Networks - GlobalProtect avec Azure AD](https://aad.portal.azure.com/)