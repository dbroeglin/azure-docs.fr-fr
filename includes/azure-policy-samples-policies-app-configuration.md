---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/02/2020
ms.author: dacoulte
ms.openlocfilehash: 9e5b5d8b7b99134deba2df9b996b96e2bf904937
ms.sourcegitcommit: e4c33439642cf05682af7f28db1dbdb5cf273cc6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/03/2020
ms.locfileid: "78262689"
---
|Nom |Description |Effet(s) |Version |GitHub |
|---|---|---|---|---|
|[App Configuration doit utiliser une clé gérée par le client](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F967a4b4b-2da9-43c1-b7d0-f98d0d74d0b1) |Cette stratégie audite toutes les instances App Configuration qui n’utilisent pas de clé gérée par le client. |Audit, Désactivé |1.0.0 |[Lien](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Configuration/CustomerManagedKey_Audit.json)
|[App Configuration doit utiliser une liaison privée](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fca610c1d-041c-4332-9d88-7ed3094967c7) |Cette stratégie audite toutes les instances App Configuration qui n’utilisent pas de liaison privée. |AuditIfNotExists, Désactivé |1.0.0 |[Lien](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Configuration/PrivateLink_Audit.json)
