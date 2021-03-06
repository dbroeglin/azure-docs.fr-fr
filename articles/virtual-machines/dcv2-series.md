---
title: Série DC – Machines virtuelles Microsoft Azure
description: Spécifications pour les machines virtuelles de la série DC.
services: virtual-machines
author: jonbeck7
ms.service: virtual-machines
ms.topic: article
ms.date: 02/20/2020
ms.author: lahugh
ms.openlocfilehash: c4e141b7854925f5d12afce19481a6e9c2f8dd1d
ms.sourcegitcommit: 99ac4a0150898ce9d3c6905cbd8b3a5537dd097e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/25/2020
ms.locfileid: "77599610"
---
# <a name="preview-dcv2-series"></a>Aperçu : Série DCv2


La série DCv2 permet de protéger la confidentialité et l’intégrité de vos données et de votre code lors de leur traitement dans le cloud public. Ces machines bénéficient du processeur Intel XEON E-2288G de dernière génération avec la technologie SGX. Avec Intel Turbo Boost Technology, ces machines peuvent atteindre 5,0 GHz. Les instances de la série DCv2 permettent aux clients de créer des applications sécurisées basées sur enclave pour protéger leur code et leurs données en cours d’utilisation.

Les exemples de cas d’utilisation incluent le partage de données pluripartites confidentielles, la détection des fraudes, le blanchiment d’argent, la blockchain, l’analyse de l’utilisation confidentielle, l’analyse décisionnelle et le machine learning confidentiel.

Premium Storage : Pris en charge*

Mise en cache du Stockage Premium : Pris en charge*

*Sauf pour Standard_DC8_v2



| Size             | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et mis en cache max. : IOPS / MBps (taille du cache en Gio) | Débit du disque non mis en cache max. : IOPS / MBps | Nombre max. de cartes réseau / Bande passante réseau attendue (Mbits/s) |
|------------------|------|-------------|------------------------|----------------|-------------------------------------------------------------------------|-------------------------------------------|----------------------------------------------|
| Standard_DC1s_v2 | 1    | 4           | 50                     | 1              | 2000/16 (21)                                                            | 1600/24                                   | 2                                            |
| Standard_DC2s_v2 | 2    | 8           | 100                    | 2              | 4 000/32 (43)                                                            | 3 200/48                                   | 2                                            |
| Standard_DC4s_v2 | 4    | 16          | 200                    | 4              | 8 000/64 (86)                                                            | 6 400/96                                   | 2                                            |
| Standard_DC8_v2  | 8   | 32          | 400                    | 8              | 16 000/128 (172)                                                         | 12 800/192                                 | 2                                            |

- Les machines virtuelles de la série DCv2 sont des [machines virtuelles de 2e génération](./linux/generation-2.md#creating-a-generation-2-vm) et ne prennent en charge que les images `Gen2`.




## <a name="other-sizes"></a>Autres tailles

- [Usage général](sizes-general.md)
- [Mémoire optimisée](sizes-memory.md)
- [Optimisé pour le stockage](sizes-storage.md)
- [Optimisé pour le GPU](sizes-gpu.md)
- [Calcul haute performance](sizes-hpc.md)
- [Générations précédentes](sizes-previous-gen.md)

## <a name="next-steps"></a>Étapes suivantes

Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.