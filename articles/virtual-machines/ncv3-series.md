---
title: Série NCv3 – Machines virtuelles Microsoft Azure
description: Spécifications pour les machines virtuelles de la série NCv3.
services: virtual-machines
author: jonbeck7
ms.service: virtual-machines
ms.topic: article
ms.date: 02/03/2020
ms.author: lahugh
ms.openlocfilehash: 18a2198063c1dfc5149c5ca017da3807da821dd1
ms.sourcegitcommit: 98a5a6765da081e7f294d3cb19c1357d10ca333f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77492386"
---
# <a name="ncv3-series"></a>Série NCv3

Les machines virtuelles de série NCv3 sont optimisées par les GPU [NVIDIA Tesla V100](https://www.nvidia.com/data-center/tesla-v100/). Ces GPU peuvent fournir des performances de calcul une fois et demie supérieures à celles de la série NCv2. Les clients peuvent tirer parti de ces GPU mis à jour pour les charges de travail HPC traditionnelles telles que la modélisation de gisements, le séquençage de l’ADN, l’analyse des protéines, les simulations de Monte-Carlo, etc. La configuration NC24rs v3 fournit une interface réseau à haut débit et à faible latence optimisée pour les charges de travail d’informatique parallèle fortement couplées. Outre les GPU, les machines virtuelles de la série NCv3 sont également pilotées par des processeurs Intel Xeon E5-2690 v4 (Broadwell).

Premium Storage :  Prise en charge

Mise en cache du Stockage Premium :  Prise en charge

> [!IMPORTANT]
> Pour cette série de machines virtuelles, le quota de processeurs virtuels (cœurs) dans votre abonnement est initialement défini sur 0 dans chaque région. [Demandez une augmentation du quota de processeurs virtuels](../azure-supportability/resource-manager-core-quotas-request.md) pour cette série dans une [région disponible](https://azure.microsoft.com/regions/services/).
>
| Size | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | GPU | Mémoire GPU : Gio | Disques de données max. | Débit du disque non mis en cache max. : IOPS/Mbits/s | Nombre max de cartes réseau |
|---|---|---|---|---|---|---|---|---|
| Standard_NC6s_v3    | 6  | 112 | 736  | 1 | 16 | 12 | 20 000/200 | 4 |
| Standard_NC12s_v3   | 12 | 224 | 1474 | 2 | 32 | 24 | 40 000/400 | 8 |
| Standard_NC24s_v3   | 24 | 448 | 2948 | 4 | 64 | 32 | 80 000/800 | 8 |
| Standard_NC24rs_v3* | 24 | 448 | 2948 | 4 | 64 | 32 | 80 000/800 | 8 |

1 GPU = une carte V100.

*Compatible RDMA [!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="supported-operating-systems-and-drivers"></a>Systèmes d’exploitation et pilotes pris en charge

Pour tirer parti des fonctionnalités GPU de machines virtuelles de la série N Azure, installez des pilotes GPU NVIDIA.

[L’extension du pilote GPU NVIDIA](/extensions/hpccompute-gpu-windows.md) installe les pilotes CUDA ou GRID NVIDIA appropriés sur une machine virtuelle de série N. Installez ou gérez l’extension à l’aide du portail Azure ou d’outils tels qu’Azure PowerShell ou les modèles Azure Resource Manager. Consultez la [documentation sur l’extension du pilote GPU NVIDIA](/extensions/hpccompute-gpu-windows.md) pour connaître les systèmes d’exploitation pris en charge et les étapes de déploiement. Pour des informations générales sur les extensions de machine virtuelle, consultez [Extensions et fonctionnalités des machines virtuelles Azure](/extensions/overview.md).

Si vous choisissez d’installer manuellement les pilotes GPU NVIDIA, voir [Configuration des pilotes GPU de série N pour Windows](/windows/n-series-driver-setup.md) ou [Configuration des pilotes GPU de série N pour Linux](/linux/n-series-driver-setup) pour connaître les systèmes d’exploitation et pilotes pris en charge, ainsi que les étapes d’installation et de vérification.

## <a name="other-sizes"></a>Autres tailles

- [Usage général](sizes-general.md)
- [Mémoire optimisée](sizes-memory.md)
- [Optimisé pour le stockage](sizes-storage.md)
- [Optimisé pour le GPU](sizes-gpu.md)
- [Calcul haute performance](sizes-hpc.md)
- [Générations précédentes](sizes-previous-gen.md)

## <a name="next-steps"></a>Étapes suivantes

Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.