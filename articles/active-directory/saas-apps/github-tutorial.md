---
title: 'Tutoriel : Intégration d’Azure Active Directory à GitHub | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.reviewer: barbkess
ms.assetid: 8761f5ca-c57c-4a7e-bf14-ac0421bd3b5e
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 01/31/2020
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ddc2622a67979f989c030d615c402387e7762d5
ms.sourcegitcommit: 4f6a7a2572723b0405a21fea0894d34f9d5b8e12
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/04/2020
ms.locfileid: "76983467"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-github"></a>Tutoriel : Intégration de l’authentification unique Azure Active Directory à GitHub

Dans ce tutoriel, vous allez apprendre à intégrer GitHub à Azure Active Directory (Azure AD). Quand vous intégrez GitHub à Azure AD, vous pouvez :

* Contrôler dans Azure AD qui a accès à GitHub.
* Permettre à vos utilisateurs de se connecter automatiquement à GitHub avec leur compte Azure AD.
* Gérer vos comptes à un emplacement central : le Portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS à Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).

## <a name="prerequisites"></a>Conditions préalables requises

Pour configurer l’intégration d’Azure AD à GitHub, vous avez besoin des éléments suivants :

* Un abonnement Azure AD Si vous n’avez pas d’environnement Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).
* Une organisation GitHub créée dans [GitHub Enterprise Cloud](https://help.github.com/articles/github-s-products/#github-enterprise), ce qui nécessite le [plan de facturation GitHub Enterprise](https://help.github.com/articles/github-s-billing-plans/#billing-plans-for-organizations)

## <a name="scenario-description"></a>Description du scénario

Dans ce didacticiel, vous configurez et testez l’authentification unique Azure AD dans un environnement de test.

* GitHub prend en charge l’authentification unique initiée par le **fournisseur de services**

* GitHub prend en charge l’[attribution d’utilisateurs **automatique**](github-provisioning-tutorial.md).
* Après avoir configuré GitHub, vous pouvez appliquer le contrôle de session, qui protège l’exfiltration et l’infiltration des données sensibles de votre organisation en temps réel. Le contrôle de session est étendu à partir de l’accès conditionnel. [Découvrir comment appliquer un contrôle de session avec Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/proxy-deployment-aad)

## <a name="adding-github-from-the-gallery"></a>Ajout de GitHub à partir de la galerie

Pour configurer l’intégration de GitHub à Azure AD, vous devez ajouter GitHub à partir de la galerie à votre liste d’applications SaaS gérées.

1. Connectez-vous au [portail Azure](https://portal.azure.com) avec un compte professionnel ou scolaire ou avec un compte personnel Microsoft.
1. Dans le panneau de navigation gauche, sélectionnez le service **Azure Active Directory**.
1. Accédez à **Applications d’entreprise**, puis sélectionnez **Toutes les applications**.
1. Pour ajouter une nouvelle application, sélectionnez **Nouvelle application**.
1. Dans la section **Ajouter à partir de la galerie**, tapez **GitHub** dans la zone de recherche.
1. Sélectionnez **GitHub** dans le volet de résultats, puis ajoutez l’application. Patientez quelques secondes pendant que l’application est ajoutée à votre locataire.


## <a name="configure-and-test-azure-ad-single-sign-on-for-github"></a>Configurer et tester l’authentification unique Azure AD pour GitHub

Configurez et testez l’authentification unique Azure AD avec GitHub à l’aide d’un utilisateur de test appelé **B.Simon**. Pour que l’authentification unique fonctionne, vous devez établir un lien entre un utilisateur Azure AD et l’utilisateur GitHub associé.

Pour configurer et tester l’authentification unique Azure AD avec GitHub, suivez les indications des sections ci-après :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-sso)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
    * **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec B. Simon.
    * **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à B. Simon d’utiliser l’authentification unique Azure AD.
1. **[Configurer l’authentification unique GitHub](#configure-github-sso)** pour configurer les paramètres de l’authentification unique côté application.
    * **[Créer un utilisateur de test GitHub](#create-github-test-user)** pour avoir un équivalent de B.Simon dans GitHub lié à la représentation Azure AD de l’utilisateur.
1. **[Tester l’authentification unique](#test-sso)** pour vérifier si la configuration fonctionne.

## <a name="configure-azure-ad-sso"></a>Configurer l’authentification unique Azure AD

Effectuez les étapes suivantes pour activer l’authentification unique Azure AD dans le Portail Azure.

1. Dans le [portail Azure](https://portal.azure.com/), accédez à la page d’intégration de l’application **GitHub**, recherchez la section **Gérer** et sélectionnez **Authentification unique**.
1. Dans la page **Sélectionner une méthode d’authentification unique**, sélectionnez **SAML**.
1. Dans la page **Configurer l’authentification unique avec SAML**, cliquez sur l’icône de modification/stylet de **Configuration SAML de base** pour modifier les paramètres.

   ![Modifier la configuration SAML de base](common/edit-urls.png)

1. Dans la section **Configuration SAML de base**, entrez les valeurs pour les champs suivants :

   a. Dans la zone de texte **URL de connexion**, saisissez une URL au format suivant : `https://github.com/orgs/<entity-id>/sso`

    b. Dans la zone de texte **Identificateur (ID d’entité)** , saisissez une URL au format suivant : `https://github.com/orgs/<entity-id>`

    > [!NOTE]
    > Notez qu’il ne s’agit pas des valeurs réelles. Vous devez mettre à jour ces valeurs avec l’URL de connexion et l’identificateur réels. Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur. Accédez à la section d’administration de GitHub pour extraire ces valeurs.

5. L’application GitHub s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre configuration Attributs du jeton SAML. La capture d’écran suivante montre la liste des attributs par défaut, où **nameidentifier** est mappé avec **user.userprincipalname**. L’application GitHub s’attend à ce que **nameidentifier** soit mappé avec **user.mail**. Vous devez donc modifier le mappage d’attribut en cliquant sur l’icône **Modifier**.

    ![image](common/edit-attribute.png)

6. Dans la page **Configurer l’authentification unique avec SAML**, dans la section **Certificat de signature SAML**, cliquez sur **Télécharger** pour télécharger le **Certificat (Base64)** en fonction des options définies par rapport à vos besoins, puis enregistrez-le sur votre ordinateur.

    ![Lien Téléchargement de certificat](common/certificatebase64.png)

7. Dans la section **Configurer GitHub**, copiez la ou les URL appropriées en fonction de vos besoins.

    ![Copier les URL de configuration](common/copy-configuration-urls.png)

    a. URL de connexion

    b. Identificateur Azure AD

    c. URL de déconnexion

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

Dans cette section, vous allez autoriser B.Simon à utiliser l’authentification unique Azure en lui accordant l’accès à GitHub.

1. Dans le portail Azure, sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.
1. Dans la liste des applications, sélectionnez **GitHub**.
1. Dans la page de vue d’ensemble de l’application, recherchez la section **Gérer** et sélectionnez **Utilisateurs et groupes**.

   ![Lien « Utilisateurs et groupes »](common/users-groups-blade.png)

1. Sélectionnez **Ajouter un utilisateur**, puis **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une attribution**.

    ![Lien Ajouter un utilisateur](common/add-assign-user.png)

1. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **B. Simon** dans la liste Utilisateurs, puis cliquez sur le bouton **Sélectionner** au bas de l’écran.
1. Si vous attendez une valeur de rôle dans l’assertion SAML, dans la boîte de dialogue **Sélectionner un rôle**, sélectionnez le rôle approprié pour l’utilisateur dans la liste, puis cliquez sur le bouton **Sélectionner** en bas de l’écran.
1. Dans la boîte de dialogue **Ajouter une attribution**, cliquez sur le bouton **Attribuer**.

## <a name="configure-github-sso"></a>Configurer l’authentification unique GitHub

1. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise GitHub en tant qu’administrateur.

2. Accédez aux **Paramètres** et cliquez sur **Sécurité**

    ![Paramètres](./media/github-tutorial/tutorial_github_config_github_03.png)

3. Cochez la case **Activer l’authentification SAML**, révélant ainsi les champs de configuration de l’authentification unique. Utilisez en suite la valeur d’URL d’authentification unique pour mettre à jour l’URL d’authentification unique dans la configuration d’Azure AD.

    ![Paramètres](./media/github-tutorial/tutorial_github_config_github_13.png)

4. Configurez les champs suivants :

    ![Paramètres](./media/github-tutorial/tutorial_github_config_github_051.png)

    a. Dans la zone de texte **Sign on URL** (URL de connexion), collez l’**URL de connexion** que vous avez copiée sur le portail Azure.

    b. Dans la zone de texte **Issuer** (Émetteur), collez l’**Identificateur Azure AD** que vous avez copié sur le Portail Azure.

    c. Ouvrez le certificat téléchargé à partir du portail Azure dans le bloc-notes et collez le contenu dans la zone de texte **Certificat public**.

    d. Cliquez sur l’icône **Modifier** pour changer la **méthode de signature** et la **méthode Digest** de **RSA-SHA1** et **SHA1** en **RSA-SHA256** et **SHA256** comme indiqué ci-dessous.

    ![image](./media/github-tutorial/tutorial_github_sha.png)

5. Cliquez sur **Tester la configuration SAML** pour vérifier l’absence d’échecs ou d’erreurs de validation pendant l’authentification unique (SSO).

    ![Paramètres](./media/github-tutorial/tutorial_github_config_github_06.png)

6. Cliquez sur **Enregistrer**.

> [!NOTE]
> L’authentification unique dans GitHub authentifie auprès d’une organisation dans GitHub, et ne remplace pas l’authentification GitHub. Par conséquent, si la session github.com de l’utilisateur a expiré, vous pouvez être invité à vous authentifier avec un ID ou un mot de passe GitHub pendant le processus d’authentification unique.

### <a name="create-github-test-user"></a>Créer un utilisateur de test GitHub

L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans GitHub. GitHub prend en charge l’attribution automatique d’utilisateurs, qui est activée par défaut. Vous trouverez plus d’informations [ici](github-provisioning-tutorial.md) sur la façon de configurer l’attribution automatique d’utilisateurs.

**Si vous avez besoin de créer un utilisateur manuellement, procédez comme suit :**

1. Connectez-vous à votre site d’entreprise GitHub en tant qu’administrateur.

2. Cliquez sur **People**.

    ![Personnes](./media/github-tutorial/tutorial_github_config_github_08.png "Personnes")

3. Cliquez sur **Invite member**.

    ![Inviter des utilisateurs](./media/github-tutorial/tutorial_github_config_github_09.png "Inviter des utilisateurs")

4. Dans la boîte de dialogue **Invite member**, procédez comme suit :

    a. Dans la zone de texte **E-mail** , tapez l’adresse de messagerie du compte de Britta Simon.

    ![Inviter des personnes](./media/github-tutorial/tutorial_github_config_github_10.png "Inviter des personnes")

    b. Cliquez sur **Send Invitation**.

    ![Inviter des personnes](./media/github-tutorial/tutorial_github_config_github_11.png "Inviter des personnes")

    > [!NOTE]
    > Le titulaire du compte Azure Active Directory reçoit un message électronique contenant un lien à suivre pour confirmer son compte et l’activer.

## <a name="test-sso"></a>Tester l’authentification unique (SSO) 

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Quand vous cliquez sur la vignette GitHub dans le volet d’accès, vous devez être connecté automatiquement à l’application GitHub pour laquelle vous avez configuré l’authentification unique. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Ressources supplémentaires

- [Liste de tutoriels sur l’intégration d’applications SaaS avec Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Qu’est-ce que l’accès conditionnel dans Azure Active Directory ?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Essayer GitHub avec Azure AD](https://aad.portal.azure.com/)

- [Qu’est-ce que le contrôle de session dans Microsoft Cloud App Security ?](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)