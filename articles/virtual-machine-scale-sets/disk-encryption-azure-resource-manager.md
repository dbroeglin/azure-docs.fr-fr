---
title: Créer et chiffrer un groupe de machines virtuelles identiques avec des modèles Azure Resource Manager
description: Dans ce guide de démarrage rapide, vous allez apprendre à utiliser les modèles Azure Resource Manager pour créer et chiffrer un groupe de machines virtuelles identiques
author: msmbaldwin
ms.author: mbaldwin
ms.service: virtual-machine-scale-sets
ms.topic: quickstart
ms.date: 10/10/2019
ms.openlocfilehash: aeba9aee8dd10b1245fb0a1e1cc98a1951382c72
ms.sourcegitcommit: f29fec8ec945921cc3a89a6e7086127cc1bc1759
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72530937"
---
# <a name="encrypt-virtual-machine-scale-sets-with-azure-resource-manager"></a>Chiffrer des groupes de machines virtuelles identiques avec Azure Resource Manager

Vous pouvez chiffrer ou déchiffrer des groupes de machines virtuelles identiques Linux à l’aide de modèles Azure Resource Manager.

## <a name="deploying-templates"></a>Déploiement de modèles

Tout d’abord, sélectionnez le modèle qui convient à votre scénario.

- [Activer le chiffrement de disque sur un groupe de machines virtuelles identiques Linux en cours d’exécution](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-vmss-linux)

- [Activer le chiffrement de disque sur un groupe de machines virtuelles identiques Windows en cours d’exécution](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-vmss-windows)

  - [Déployer un groupe de machines virtuelles identiques Linux avec une machine jumpbox et activer le chiffrement sur les groupes de machines virtuelles identiques Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-vmss-linux-jumpbox)

  - [Déployer un groupe de machines virtuelles identiques Windows avec une machine jumpbox et activer le chiffrement sur les groupes de machines virtuelles identiques Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-vmss-windows-jumpbox)

- [Désactiver le chiffrement de disque sur un groupe de machines virtuelles identiques Linux en cours d’exécution](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-vmss-linux)

- [Désactiver le chiffrement de disque sur un groupe de machines virtuelles identiques Windows en cours d’exécution](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-vmss-windows)

Exécutez ensuite les opérations qui suivent :

     1. Click **Deploy to Azure**.
     2. Fill in the required fields then agree to the terms and conditions.
     3. Click **Purchase** to deploy the template.

## <a name="next-steps"></a>Étapes suivantes

- [Azure Disk Encryption pour les groupes de machines virtuelles identiques](disk-encryption-overview.md)
- [Chiffrer un groupe de machines virtuelles identiques à l’aide d’Azure CLI](disk-encryption-cli.md)
- [Chiffrer un groupe de machines virtuelles identiques à l’aide d’Azure PowerShell](disk-encryption-powershell.md)
- [Créer et configurer un coffre de clés pour Azure Disk Encryption](disk-encryption-key-vault.md)
- [Utiliser Azure Disk Encryption avec le séquencement d’extensions de groupes de machines virtuelles identiques](disk-encryption-extension-sequencing.md)