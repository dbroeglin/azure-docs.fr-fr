---
title: Changement de notification de détection intelligente - Azure Application Insights
description: Passez aux destinataires des notifications par défaut depuis la détection intelligente. La détection intelligente vous permet de superviser les suivis d’application avec Azure Application Insights afin de déterminer si les données de télémétrie du suivi présentent des anomalies.
ms.topic: conceptual
author: harelbr
ms.author: harelbr
ms.date: 03/13/2019
ms.reviewer: mbullwin
ms.openlocfilehash: f73e5bbdd8585b3367e529a8fa00630042e56cac
ms.sourcegitcommit: 747a20b40b12755faa0a69f0c373bd79349f39e3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2020
ms.locfileid: "77671781"
---
# <a name="smart-detection-e-mail-notification-change"></a>Modification des notifications par e-mail de la détection intelligente

Sur la base des commentaires des clients, nous modifions, le 1er avril 2019, les rôles par défaut qui reçoivent les notifications par e-mail de la détection intelligente.

## <a name="what-is-changing"></a>Qu’est-ce qui change ?

Actuellement, les notifications par e-mail de la détection intelligente sont envoyées par défaut aux rôles _Propriétaire de l’abonnement_, _Contributeur de l’abonnement_ et _Lecteur de l’abonnement_. Ces rôles englobent souvent des utilisateurs qui ne participent pas activement au monitoring, et qui reçoivent donc inutilement des notifications. Pour améliorer cette expérience, nous sommes en train d’apporter une modification : les notifications par e-mail ne seront par défaut envoyées qu’aux rôles [Lecteur de monitoring](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#monitoring-reader) et [Contributeur de monitoring](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#monitoring-contributor).

## <a name="scope-of-this-change"></a>Portée de ce changement

Cette modification touchera toutes les règles de détection intelligente, à l’exception des suivantes :

* les règles de détection intelligente marquées comme étant en préversion, qui à l’heure actuelle ne prennent pas en charge les notifications par e-mail ;

* la règle Anomalies de défaillance, qui commencera à cibler les nouveaux rôles par défaut une fois migrée d’une alerte classique à la plateforme d’alertes unifiée (pour plus d’informations, cliquez [ici](https://docs.microsoft.com/azure/azure-monitor/platform/monitoring-classic-retirement)).

## <a name="how-to-prepare-for-this-change"></a>Préparation à cette modification

Pour que les notifications par e-mail de la détection intelligente soient envoyées aux utilisateurs concernés, ces derniers doivent être assignés aux rôles [Lecteur de supervision](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#monitoring-reader) ou [Contributeur de supervision](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#monitoring-contributor) de l’abonnement.

Pour attribuer le rôle Lecteur de monitoring ou Contributeur de monitoring à des utilisateurs sur le Portail Azure, suivez les étapes de l’article [Ajouter une attribution de rôle](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal#add-a-role-assignment). Veillez à sélectionner le rôle _Lecteur de monitoring_ ou _Contributeur de monitoring_ pour l’attribuer aux utilisateurs.

> [!NOTE]
> Les destinataires spécifiques des notifications de la détection intelligente, configurés avec l’option _Autres destinataires des e-mails_ dans les paramètres des règles, ne seront pas concernés par cette modification. Ils continueront de recevoir les notifications par e-mail.

Si vous avez des questions ou des commentaires au sujet de cette modification, n’hésitez pas à [nous contacter](mailto:smart-alert-feedback@microsoft.com).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la détection intelligente :

- [Défaillances](../../azure-monitor/app/proactive-failure-diagnostics.md)
- [Fuites de mémoire](../../azure-monitor/app/proactive-potential-memory-leak.md)
- [Anomalies de performance](../../azure-monitor/app/proactive-performance-diagnostics.md)
