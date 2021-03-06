---
title: Utiliser PowerShell pour créer une application Azure AD pour accéder à l’API Azure Media Services | Microsoft Docs
description: Découvrez comment utiliser PowerShell pour créer une application Azure Active Directory (Azure AD) et la configurer pour accéder à l’API Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/19/2019
ms.author: juliako
ms.openlocfilehash: ff7f8bc27d358c667b10c0bd3383e78b20494303
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/13/2019
ms.locfileid: "64680134"
---
# <a name="use-powershell-to-create-an-azure-ad-app-to-use-with-the-azure-media-services-api"></a>Utiliser PowerShell pour créer une application Azure AD à utiliser avec l’API Azure Media Services

> [!NOTE]
> Aucune nouvelle fonctionnalité ni fonction n’est ajoutée à Media Services v2. <br/>Découvrez la dernière version, [Media Services v3](https://docs.microsoft.com/azure/media-services/latest/). Consultez aussi [Conseils de migration de v2 vers v3](../latest/migrate-from-v2-to-v3.md).

Découvrez comment utiliser un script PowerShell pour créer une application Azure Active Directory (Azure AD) et un principal du service pour accéder aux ressources Azure Media Services.  

## <a name="prerequisites"></a>Prérequis

- Un compte Azure. Si vous n’avez pas de compte, commencez avec un [essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Un compte Media Services. Pour plus d’informations, voir [Création d’un compte Azure Media Services dans le portail Azure](media-services-portal-create-account.md).

- Azure PowerShell. Pour plus d’informations, découvrez l’[utilisation d’Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Créer une application Azure AD à l’aide de PowerShell  

```powershell
Connect-AzAccount
Import-Module Az.Resources
Set-AzContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds to allow the service principal application to become active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

Pour plus d’informations, consultez les articles suivants :

- [Créer un principal du service pour accéder aux ressources à l’aide d’Azure PowerShell](../../active-directory/develop/howto-authenticate-service-principal-powershell.md)
- [Gérer le contrôle d’accès en fonction du rôle à l’aide d’Azure PowerShell](../../role-based-access-control/role-assignments-powershell.md)
- [Comment configurer manuellement des applications démons à l’aide de certificats](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Étapes suivantes

Commencez le [chargement de fichiers sur votre compte](media-services-portal-upload-files.md).
