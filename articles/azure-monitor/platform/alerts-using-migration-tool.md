---
title: Migrer vos alertes classiques dans Azure Monitor à l’aide de l’outil de migration volontaire
description: Découvrez comment utiliser l’outil de migration volontaire pour migrer vos règles d’alerte classiques.
author: yanivlavi
ms.author: yalavi
ms.topic: conceptual
ms.date: 03/19/2018
ms.subservice: alerts
ms.openlocfilehash: 537d84639523a74cbd9403d4ad25c34a798b7061
ms.sourcegitcommit: 747a20b40b12755faa0a69f0c373bd79349f39e3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2020
ms.locfileid: "77665100"
---
# <a name="use-the-voluntary-migration-tool-to-migrate-your-classic-alert-rules"></a>Utiliser l’outil de migration volontaire pour migrer vos règles d’alerte classiques

Comme [précédemment annoncé](monitoring-classic-retirement.md), les alertes classiques dans Azure Monitor seront mises hors service en septembre 2019 (c’était initialement prévu pour juillet 2019). Un outil de migration est disponible dans le Portail Azure pour les clients qui utilisent des règles d’alerte classiques et qui souhaitent déclencher la migration eux-mêmes. Cet article vous explique comment utiliser l’outil de migration pour migrer volontairement vos règles d’alerte classiques avant que la migration automatique démarre en septembre 2019.

> [!NOTE]
> En raison de retards dans le déploiement de l’outil de migration, la date de mise hors service des alertes classiques a été [repoussée au 31 août 2019](https://azure.microsoft.com/updates/azure-monitor-classic-alerts-retirement-date-extended-to-august-31st-2019/) (la date annoncée à l’origine était le 30 juin 2019).

## <a name="benefits-of-new-alerts"></a>Avantages des nouvelles alertes

Les alertes classiques sont remplacées par de nouvelles alertes unifiées dans Azure Monitor. La nouvelle plateforme d’alertes présente les avantages suivants :

- Vous pouvez créer des alertes sur diverses métriques multidimensionnelles pour [de nombreux services Azure supplémentaires](alerts-metric-near-real-time.md#metrics-and-dimensions-supported).
- Les nouvelles alertes sur les métriques prennent en charge des [règles d’alerte multiressources](alerts-metric-overview.md#monitoring-at-scale-using-metric-alerts-in-azure-monitor) qui réduisent considérablement la surcharge de la gestion de nombreuses règles.
- Le mécanisme de notification unifié, qui prend en charge :
  - Les [groupes d’actions](action-groups.md), un mécanisme de notification modulaire qui fonctionne avec tous les nouveaux types d’alertes (métriques, journaux et journaux d’activité).
  - De nouveaux mécanismes de notification tels que les SMS, la voix et le connecteur ITSM.
- [L’expérience d’alerte unifiée](alerts-overview.md) rassemble toutes les alertes sur des signaux différents (métriques, journaux et journaux d’activité) dans un seul endroit.

## <a name="before-you-migrate"></a>Avant de migrer

Le processus de migration convertit les règles d’alerte classiques en de nouvelles règles équivalentes et crée des groupes d’actions. Lors de la préparation, tenez compte des points suivants :

- Le format de charge utile de notification et les API pour créer et gérer les nouvelles règles d’alerte sont différents de ceux des règles d’alerte classiques, car ils prennent en charge davantage de fonctionnalités. [Découvrez comment préparer la migration](alerts-prepare-migration.md).

- Certaines règles d’alerte classiques ne peuvent pas être migrées à l’aide de l’outil. [Découvrez les règles qui ne peuvent pas être migrées et que faire avec](alerts-understand-migration.md#classic-alert-rules-that-will-not-be-migrated).

    > [!NOTE]
    > Le processus de migration n’affecte pas l’évaluation de vos règles d’alerte classiques. Elles continuent à s’exécuter et envoyer des alertes jusqu'à ce qu’elles soient migrées et que les nouvelles règles d’alerte prennent effet.

## <a name="how-to-use-the-migration-tool"></a>Guide pratique pour utiliser l’outil de migration

Pour déclencher la migration de vos règles d’alerte classiques dans le portail Azure, procédez comme suit :

1. Dans le [Portail Azure](https://portal.azure.com), sélectionnez **Surveiller**.

1. Sélectionnez **Alertes**, puis **Gérer les règles d’alerte** ou **Afficher les alertes classiques**.

1. Sélectionnez **Migrer vers les nouvelles règles** pour accéder à la page d’accueil de migration. Cette page affiche une liste de tous vos abonnements et leur état de migration :

    ![migration-landing](media/alerts-migration/migration-landing.png "Migrer les règles")

    Tous les abonnements qui peuvent être migrés à l’aide de l’outil sont marqués comme **Prêts pour la migration**.

    > [!NOTE]
    > L’outil de migration est déployé en plusieurs phases à tous les abonnements qui utilisent des règles d’alerte classiques. Dans les premières phases du déploiement, vous pouvez voir certains abonnements marqués comme n’étant pas prêts pour la migration.

1. Sélectionnez un ou plusieurs abonnements, puis **Aperçu de la migration**.

    La page résultante affiche les détails des règles d’alerte classiques qui seront migrées pour un abonnement à la fois. Vous pouvez également sélectionner **Télécharger les détails de la migration pour cet abonnement** pour obtenir les détails au format CSV.

    ![migration-preview](media/alerts-migration/migration-preview.png "Prévisualiser la migration")

1. Spécifiez une ou plusieurs adresses e-mail pour être informé de l’état de la migration. Vous recevrez un e-mail lorsque de la migration sera terminée ou si une action est nécessaire de votre part.

1. Sélectionnez **Démarrer la migration**. Lisez les informations affichées dans la boîte de dialogue de confirmation et confirmez que vous êtes prêt à commencer le processus de migration.

    > [!IMPORTANT]
    > Une fois que vous initiez la migration pour un abonnement, vous ne pourrez pas modifier ou créer des règles d’alerte classiques pour cet abonnement. Cette restriction garantit qu’aucune modification de vos règles d’alerte classiques n’est perdue pendant la migration vers les nouvelles règles. Bien que vous ne pourrez pas modifier vos règles d’alerte classiques, elles continueront à exécuter et à fournir des alertes jusqu'à leur migration. Une fois la migration terminée pour votre abonnement, vous ne pourrez plus utiliser les règles d’alerte classiques.

    ![migration-confirm](media/alerts-migration/migration-confirm.png "Confirmer le démarrage de la migration")

1. Lorsque la migration est terminée, ou si une action est nécessaire de votre part, vous recevrez un e-mail aux adresses que vous avez fournies précédemment. Vous pouvez également régulièrement vérifier l’état sur la page d’accueil de migration dans le portail.

## <a name="frequently-asked-questions"></a>Forum aux questions

### <a name="why-is-my-subscription-listed-as-not-ready-for-migration"></a>Pourquoi mon abonnement est-il marqué comme « Not Ready for migration » (Pas prêt pour la migration) ?

L’outil de migration est livré aux clients en plusieurs phases. Dans les premières phases, la plupart ou la totalité de vos abonnements pourraient être marqués comme **non prêts pour la migration**. 

Quand un abonnement est prêt pour la migration, le propriétaire de l’abonnement reçoit un e-mail indiquant que l’outil est disponible. Surveillez l’arrivée de ce message.

### <a name="who-can-trigger-the-migration"></a>Qui peut déclencher la migration ?

Les utilisateurs qui ont le rôle Contributeur de surveillance au niveau de l’abonnement peuvent déclencher la migration. [En savoir plus sur le contrôle d’accès en fonction du rôle pour le processus de migration](alerts-understand-migration.md#who-can-trigger-the-migration).

### <a name="how-long-will-the-migration-take"></a>Combien de temps prendra la migration ?

La migration est effectuée pour la plupart des abonnements en moins d’une heure. Vous pouvez suivre la progression de la migration sur la page d’accueil de migration. Pendant la migration, vous avez la garantie que vos alertes continuent à s’exécuter dans le système d’alertes classique ou le nouveau.

### <a name="what-can-i-do-if-i-run-into-a-problem-during-migration"></a>Que puis-je faire si je rencontre un problème pendant la migration ?

Consultez le [guide de dépannage](alerts-understand-migration.md#common-problems-and-remedies) pour vous aider à résoudre les problèmes que vous pourriez rencontrer pendant la migration. Si une action est nécessaire de votre part pour terminer la migration, vous en serez averti sur les adresses e-mail que vous avez fournies lorsque vous avez configuré l’outil.

## <a name="next-steps"></a>Étapes suivantes

- [Préparer la migration](alerts-prepare-migration.md)
- [Comprendre le fonctionnement de l’outil de migration](alerts-understand-migration.md)
