---
title: Windows Virtual Desktop PowerShell – Azure
description: Comment résoudre des problèmes avec PowerShell quand vous configurez un environnement de locataire Windows Virtual Desktop.
services: virtual-desktop
author: Heidilohr
ms.service: virtual-desktop
ms.topic: troubleshooting
ms.date: 04/08/2019
ms.author: helohr
ms.openlocfilehash: e20d5a6b21c11930f0e547134479113539a2bc76
ms.sourcegitcommit: f97f086936f2c53f439e12ccace066fca53e8dc3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2020
ms.locfileid: "77367188"
---
# <a name="windows-virtual-desktop-powershell"></a>Windows Virtual Desktop PowerShell

Cet article vous aide à résoudre des problèmes et erreurs rencontrés lors de l’utilisation de PowerShell avec Windows Virtual Desktop. Pour plus d’informations sur les Services Bureau à distance PowerShell, voir [Windows Virtual Desktop Powershell](/powershell/module/windowsvirtualdesktop/).

## <a name="provide-feedback"></a>Fournir des commentaires

Rendez-vous sur le site [Windows Virtual Desktop Tech Community](https://techcommunity.microsoft.com/t5/Windows-Virtual-Desktop/bd-p/WindowsVirtualDesktop) pour discuter du service Windows Virtual Desktop avec l’équipe de produit et les membres actifs de la communauté.

## <a name="powershell-commands-used-during-windows-virtual-desktop-setup"></a>Commandes PowerShell utilisées pendant la configuration de Windows Virtual Desktop

Cette section répertorie les commandes PowerShell qui sont généralement utilisées lors de la configuration de Windows Virtual Desktop, et explique comment résoudre des problèmes qui peuvent se produire lors de leur utilisation.

### <a name="error-add-rdsappgroupuser-command----the-specified-userprincipalname-is-already-assigned-to-a-remoteapp-app-group-in-the-specified-host-pool"></a>Erreur : Commande Add-RdsAppGroupUser : le UserPrincipalName spécifié est déjà affecté à un groupe d’applications RemoteApp dans le pool d’hôte spécifié

```Powershell
Add-RdsAppGroupUser -TenantName <TenantName> -HostPoolName <HostPoolName> -AppGroupName 'Desktop Application Group' -UserPrincipalName <UserName>
```

**Cause :** Le nom d’utilisateur utilisé a déjà été attribué à un groupe d’applications d’un type différent. Des utilisateurs ne peuvent pas être affectés en même temps à un Bureau à distance et à un groupe d’applications à distance sous le même pool d’hôte de session.

**Correctif :** Si un utilisateur a besoin tant d’applications à distance que d’un Bureau à distance, créez des pools d’hôte différents ou accordez un accès utilisateur au Bureau à distance, ce qui permet d’utiliser tout e application sur la machine virtuelle de l’hôte de la session.

### <a name="error-add-rdsappgroupuser-command----the-specified-userprincipalname-doesnt-exist-in-the-azure-active-directory-associated-with-the-remote-desktop-tenant"></a>Erreur : Commande Add-RdsAppGroupUser : le UserPrincipalName spécifié n’existe pas dans l’Azure Active Directory associé au locataire du Bureau à distance

```PowerShell
Add-RdsAppGroupUser -TenantName <TenantName> -HostPoolName <HostPoolName> -AppGroupName "Desktop Application Group" -UserPrincipalName <UserPrincipalName>
```

**Cause :** L’utilisateur spécifié par le UserPrincipalName est introuvable dans l’Azure Active Directory lié au locataire Windows Virtual Desktop.

**Correctif :** Vérifiez les éléments dans la liste suivante.

- L’utilisateur est synchronisé sur Azure Active Directory.
- L’utilisateur n’est pas lié à commerce B2C ou B2B.
- Le locataire Windows Virtual Desktop est lié à l’Azure Active Directory correct.

### <a name="error-get-rdsdiagnosticactivities----user-isnt-authorized-to-query-the-management-service"></a>Erreur : Get-RdsDiagnosticActivities : l’utilisateur n’est pas autorisé à interroger le service de gestion

```PowerShell
Get-RdsDiagnosticActivities -ActivityId <ActivityId>
```

**Cause :** paramètre -TenantName

**Correctif :** Émettez Get-RdsDiagnosticActivities avec -TenantName \<TenantName>.

### <a name="error-get-rdsdiagnosticactivities----the-user-isnt-authorized-to-query-the-management-service"></a>Erreur : Get-RdsDiagnosticActivities : l’utilisateur n’est pas autorisé à interroger le service de gestion

```PowerShell
Get-RdsDiagnosticActivities -Deployment -username <username>
```

**Cause :** utilisation du commutateur -Deployment.

**Correctif :** le commutateur -Deployment ne peut être utilisé que par des administrateurs de déploiement. Ces administrateurs sont généralement des membres de l’équipe Services Bureau à distance/Windows Virtual Desktop. Remplacez le commutateur -Deployment par -TenantName \<TenantName>.

### <a name="error-new-rdsroleassignment----the-user-isnt-authorized-to-query-the-management-service"></a>Erreur : New-RdsRoleAssignment : l’utilisateur n’est pas autorisé à interroger le service de gestion

**Cause 1 :** Le compte utilisé ne dispose pas des autorisations de propriétaire de Services Bureau à distance sur le client.

**Correctif 1 :** Un utilisateur disposant d’autorisations de propriétaire de Services Bureau à distance doit exécuter l’attribution de rôle.

**Cause 2 :** Le compte utilisé dispose d’autorisations de propriétaire de Services Bureau à distance, mais ne fait pas partie de l’Azure Active Directory du locataire ou n’est pas autorisé à interroger l’Azure Active Directory où se trouve l’utilisateur.

**Correctif 2 :** Un utilisateur disposant d’autorisations Active Directory doit exécuter l’attribution de rôle.

>[!Note]
>New-RdsRoleAssignment ne peut pas accorder d’autorisations à un utilisateur qui n’existe pas dans l’Azure Active Directory (AD).

## <a name="next-steps"></a>Étapes suivantes

- Pour découvrir une vue d’ensemble de la résolution des problèmes Windows Virtual Desktop et des procédures d’escalade, consultez l’article [Vue d’ensemble du dépannage, commentaires et support](troubleshoot-set-up-overview.md).
- Pour résoudre les problèmes de création d’un pool de locataires et d’hôtes dans un environnement Windows Virtual Desktop, consultez [Création d’un pool de locataires et d’hôtes](troubleshoot-set-up-issues.md).
- Pour résoudre les problèmes de configuration d’une machine virtuelle dans Windows Virtual Desktop, consultez [Configuration d’une machine virtuelle hôte de session](troubleshoot-vm-configuration.md).
- Pour résoudre les problèmes de connexion au client Windows Virtual Desktop, consultez [Connexions au service Windows Virtual Desktop](troubleshoot-service-connection.md).
- Pour résoudre les problèmes liés aux clients Bureau à distance, consultez [Résoudre des problèmes du client Bureau à distance](troubleshoot-client.md).
- Pour plus d’informations sur le service, consultez [Environnement Windows Virtual Desktop](environment-setup.md).
- Suivez le [Didacticiel : Résoudre les problèmes liés aux déploiements de modèles Resource Manager](../azure-resource-manager/templates/template-tutorial-troubleshoot.md).
- Pour en savoir plus sur les actions d’audit, consultez [Opérations d’audit avec Resource Manager](../azure-resource-manager/management/view-activity-logs.md).
- Pour en savoir plus sur les actions visant à déterminer les erreurs au cours du déploiement, consultez [Voir les opérations de déploiement](../azure-resource-manager/templates/deployment-history.md).
