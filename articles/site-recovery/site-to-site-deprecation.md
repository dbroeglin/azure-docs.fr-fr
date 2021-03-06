---
title: Dépréciation de la récupération d'urgence entre des sites gérés par un client (avec VMM) à l'aide d'Azure Site Recovery | Microsoft Docs
description: Détails sur la dépréciation à venir de la récupération d’urgence entre sites appartenant à un client avec Hyper-V et entre sites gérés par SCVMM vers Azure et alternatives
services: site-recovery
author: rajani-janaki-ram
manager: rochakm
ms.service: site-recovery
ms.topic: article
ms.date: 02/25/2020
ms.author: rajanaki
ms.openlocfilehash: 68d975a1b8bb8d47011bb292d3cf897956b31712
ms.sourcegitcommit: 5a71ec1a28da2d6ede03b3128126e0531ce4387d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2020
ms.locfileid: "77623617"
---
# <a name="deprecation-of-disaster-recovery-between-customer-managed-sites-with-vmm-using-azure-site-recovery"></a>Dépréciation de la récupération d'urgence entre des sites gérés par un client (avec VMM) à l'aide d'Azure Site Recovery

Cet article décrit le plan de dépréciation à venir, les implications correspondantes et les options alternatives disponibles pour les clients pour le scénario suivant :

Récupération d’urgence entre des sites appartenant à un client et gérés par System Center Virtual Machine Manager (SCVMM) à l’aide de Site Recovery

> [!IMPORTANT]
> Les clients sont invités à prendre les mesures correctives au plus tôt pour éviter toute interruption dans leur environnement. 

## <a name="what-changes-should-you-expect"></a>À quelles modifications devez-vous vous attendre ?

- À partir de mars 2020, vous recevrez des notifications du portail Azure ainsi que des e-mails de communication sur la prochaine dépréciation de la réplication de site à site des machines virtuelles Hyper-V. La dépréciation est prévue pour mars 2023.

- Si vous disposez d'une configuration existante, il n'y aura aucun impact sur celle-ci.

- Une fois les scénarios dépréciés, les réplications existantes peuvent être interrompues à moins que le client ne suive les autres approches. Les clients ne seront pas en mesure d’afficher, de gérer ou d’effectuer des opérations de récupération d’urgence par le biais de l’expérience Azure Site Recovery dans le Portail Azure.
 
## <a name="alternatives"></a>Autres solutions 

Vous trouverez ci-dessous les alternatives parmi lesquelles le client peut choisir pour s’assurer que sa stratégie de récupération d’urgence ne sera pas compromise lorsque le scénario sera déprécié. 

- Option 1 (recommandée) : Choisissez de [commencer à utiliser Azure comme cible de récupération d’urgence pour les machines virtuelles sur les hôtes Hyper-V](hyper-v-azure-tutorial.md).

    > [!IMPORTANT]
    > Notez que votre environnement local peut toujours disposer de SCVMMM, mais que vous configurerez ASR avec des références aux hôtes Hyper-V uniquement.

- Option n°2 : Choisissez de continuer la réplication de site à site en utilisant la [solution de réplication Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica) sous-jacente ; mais vous ne serez alors pas en mesure de gérer les configurations de récupération d’urgence à l’aide d’Azure Site Recovery dans le Portail Azure. 


## <a name="remediation-steps"></a>Étapes de correction

Si vous choisissez d’utiliser l’option 1, veuillez exécuter les étapes suivantes :

1. [Désactiver la protection de toutes les machines virtuelles associées aux VMM](site-recovery-manage-registration-and-protection.md#disable-protection-for-a-hyper-v-virtual-machine-replicating-to-secondary-vmm-server-using-the-system-center-vmm-to-vmm-scenario). Utilisez l’option **Désactiver la réplication et supprimer** ou exécutez les scripts mentionnés pour vous assurer que les paramètres de réplication locaux sont nettoyés. 

2. [Désinscrire tous les serveurs VMM](site-recovery-manage-registration-and-protection.md#unregister-a-vmm-server)

3. [Préparer les ressources Azure](tutorial-prepare-azure-for-hyperv.md) pour activer la réplication de vos machines virtuelles.
4. [Préparer des serveurs Hyper-V locaux](hyper-v-prepare-on-premises-tutorial.md)

> [!IMPORTANT]
> Notez qu'il n'est pas nécessaire de suivre les étapes de la section Préparer un VMM.

5. [Configurer la réplication des machines virtuelles](hyper-v-azure-tutorial.md)
6. Cette étape est facultative, mais recommandée : [Exécuter un test de récupération d’urgence](tutorial-dr-drill-azure.md)

Si vous choisissez d'utiliser l'option 2 du réplica Hyper-V, suivez les étapes ci-dessous :

1. Dans **Éléments protégés** > **Éléments répliqués**, cliquez avec le bouton droit sur la machine et sélectionnez **Désactiver la réplication**.
2. Dans **Désactiver la réplication**, sélectionnez **Supprimer**.

    Elle supprime l’élément répliqué d’Azure Site Recovery (la facturation est arrêtée). La configuration de la réplication sur la machine virtuelle locale **n’est pas** nettoyée. 

## <a name="next-steps"></a>Étapes suivantes
Planifiez la dépréciation et choisissez l’alternative qui convient le mieux à votre infrastructure et votre entreprise. Si vous avez des questions, contactez le Support Microsoft.

