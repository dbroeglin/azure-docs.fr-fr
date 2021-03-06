---
title: Résoudre les problèmes liés à Azure Stream Analytics à l’aide des journaux de diagnostic
description: Cet article décrit comment analyser les journaux de diagnostic dans Azure Stream Analytics.
author: jseb225
ms.author: jeanb
ms.reviewer: mamccrea
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 12/19/2019
ms.openlocfilehash: f318b373f6a6f46ee3a85703c6099c76568580ba
ms.sourcegitcommit: f4f626d6e92174086c530ed9bf3ccbe058639081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75426144"
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>Résoudre les problèmes liés à Azure Stream Analytics à l’aide des journaux de diagnostic

Il arrive parfois qu’un travail Azure Stream Analytics s’arrête de manière inattendue. Il est important d’être en mesure de résoudre ce type de problème. Les échecs peuvent être liés à un résultat de requête inattendu, à une mauvaise connectivité aux périphériques ou à un arrêt inattendu du service. Les journaux de diagnostic dans Stream Analytics peuvent vous aider à identifier la cause des problèmes lorsqu’ils surviennent et à réduire le délai de récupération.

Il est vivement recommandé d’activer les journaux de diagnostic pour tous les travaux, ce qui facilite grandement le débogage et la surveillance.

## <a name="log-types"></a>Types de journaux

Stream Analytics fournit deux types de journaux d’activité :

* Les [journaux d’activité](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (activés en permanence) fournissent des détails sur les opérations effectuées sur les travaux.

* Les [journaux de diagnostic](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (configurables) offrent des informations plus détaillées sur tous les événements liés à un travail. Les journaux de diagnostic enregistrent les événements entre le moment où le travail est créé et celui où le travail est supprimé. Ils consignent les événements qui se produisent lorsque le travail est mis à jour et lors de son exécution.

> [!NOTE]
> Vous pouvez utiliser des services, tels que Stockage Azure, Azure Event Hubs et les journaux Azure Monitor pour analyser les données non conformes. Les frais qui vous seront facturés varient selon le modèle de tarification de chaque service.

[!INCLUDE [azure-monitor-log-analytics-rebrand](../../includes/azure-monitor-log-analytics-rebrand.md)]

## <a name="debugging-using-activity-logs"></a>Débogage à l’aide des journaux d’activité

Les journaux d’activité sont activés par défaut et proposent des informations détaillées sur les opérations effectuées par votre travail Stream Analytics. Les informations présentes dans les journaux d’activité vous aident à déterminer la cause racine des problèmes ayant un impact sur votre travail. Pour utiliser les journaux d’activité dans Stream Analytics, procédez comme suit :

1. Connectez-vous au portail Azure et sélectionnez **Journal d’activité** sous **Vue d’ensemble**.

   ![Journal d’activité Stream Analytics](./media/stream-analytics-job-diagnostic-logs/stream-analytics-menu.png)

2. Vous pouvez consulter la liste des opérations effectuées. Toute opération ayant entraîné l’échec de votre travail est accompagnée d'une info-bulle rouge.

3. Cliquez sur une opération pour afficher un résumé la concernant. Les informations qui s'y trouvent sont souvent limitées. Pour plus d’informations sur l’opération, cliquez sur **JSON**.

   ![Résumé des opérations du journal d'activité Stream Analytics](./media/stream-analytics-job-diagnostic-logs/operation-summary.png)

4. Faites défiler jusqu'à la section **Propriétés** du JSON, qui fournit des détails sur l’erreur à l'origine de l'échec de l'opération. Dans cet exemple, cet échec était dû à une erreur d'exécution liée à des valeurs de latitude hors limites. Des incohérences dans les données qui sont traitées par un travail Stream Analytics provoque une erreur de données. Vous pouvez en savoir plus sur les différentes [erreurs de données d’entrée et de sortie, et la raison de leur survenue](https://docs.microsoft.com/azure/stream-analytics/data-errors).

   ![Détails d'erreur JSON](./media/stream-analytics-job-diagnostic-logs/error-details.png)

5. Vous pouvez effectuer des actions correctives en fonction du message d’erreur dans JSON. Dans cet exemple, il convient d'ajouter des vérifications à la requête pour s'assurer que la valeur de latitude est comprise entre -90 degrés et 90 degrés.

6. Si le message d’erreur présent dans les journaux d’activité ne permet pas d’identifier la cause racine, activez les journaux de diagnostic et utilisez les journaux Azure Monitor.

## <a name="send-diagnostics-to-azure-monitor-logs"></a>Envoyer des diagnostics aux journaux Azure Monitor

Il est vivement conseillé d’activer les journaux de diagnostic et de les envoyer aux journaux Azure Monitor. Les journaux de diagnostic sont **désactivés** par défaut. Pour activer les journaux de diagnostic, procédez comme suit :

1.  Connectez-vous au portail Azure et accédez à votre travail Stream Analytics. Sous **Supervision**, sélectionnez **Journaux de diagnostic**. Ensuite, sélectionnez **Activer les diagnostics**.

    ![Navigation dans le panneau jusqu’aux journaux de diagnostic](./media/stream-analytics-job-diagnostic-logs/diagnostic-logs-monitoring.png)  

2.  Créez un **nom** dans **Paramètres de diagnostic** et cochez la case située en regard de **Envoyer à Log Analytics**. Ajoutez ou créez ensuite un **espace de travail Log Analytics**. Cochez les cases **Exécution** et **Création** sous **JOURNAL**, ainsi que **AllMetrics** sous **MÉTRIQUE** . Cliquez sur **Enregistrer**. Il est recommandé d’utiliser un espace de travail Log Analytics dans la même région Azure que votre travail Stream Analytics, afin d’éviter des frais supplémentaires.

    ![Paramètres des journaux de diagnostic](./media/stream-analytics-job-diagnostic-logs/diagnostic-settings.png)

3. Lorsque votre tâche Stream Analytics démarre, les journaux de diagnostic sont routés vers votre espace de travail Log Analytics. Pour afficher les journaux de diagnostic de votre travail, sélectionnez **Journaux** sous la section **Surveillance**.

   ![Journaux de diagnostic sous Surveillance](./media/stream-analytics-job-diagnostic-logs/diagnostic-logs.png)

4. Stream Analytics fournit des requêtes prédéfinies qui vous permettent de rechercher facilement les journaux qui vous intéressent. Les trois catégories sont **Général**, **Erreurs des données d’entrée** et **Erreurs des données de sortie**. Par exemple, pour afficher un résumé de toutes les erreurs de votre travail au cours des sept derniers jours, vous pouvez sélectionner **Exécuter** pour la requête prédéfinie appropriée. 

   ![Journaux de diagnostic sous Surveillance](./media/stream-analytics-job-diagnostic-logs/logs-categories.png)

   ![Résultats des journaux](./media/stream-analytics-job-diagnostic-logs/logs-result.png)

## <a name="diagnostics-log-categories"></a>Catégories de journaux de diagnostic

Azure Stream Analytics capture deux catégories de journaux de diagnostics :

* **Création** : capture les événements de journal liés aux opérations de création de travaux (création du travail, ajout et suppression d’entrées et de sorties, ajout et mise à jour de la requête, démarrage et arrêt du travail).

* **Exécution** : capture les événements qui se produisent pendant l’exécution du travail.
    * Erreurs de connectivité
    * Erreurs de traitement des données, notamment :
        * Événements non conformes à la définition de la requête (types et valeurs de champs ne correspondant pas, champs manquants, etc.)
        * Erreurs d’évaluation d’expression
    * Autres erreurs et événements

## <a name="diagnostics-logs-schema"></a>Schéma des journaux de diagnostic

Tous les journaux d’activité sont stockés au format JSON. Chaque entrée comprend les champs de chaîne courants suivants :

Name | Description
------- | -------
time | L’horodatage (heure UTC) du journal.
resourceId | L’ID de la ressource sur laquelle l’opération a eu lieu, en majuscules. Comprend l’ID d’abonnement, le groupe de ressources et le nom du travail. Par exemple, **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.
catégorie | La catégorie de journal, **Exécution** ou **Création**.
operationName | Le nom de l’opération qui est journalisée. Par exemple, **Événements d’envoi : Échec d’écriture de la sortie SQL sur mysqloutput**.
status | État de l’opération. Par exemple, **Échec** ou **Réussite**.
level | Le niveau du journal. Par exemple, **Erreur**, **Avertissement** ou **Informations**.
properties | Détail spécifique de l’entrée du journal, sérialisé comme chaîne JSON. Pour plus d’informations, consultez les sections suivantes de cet article.

### <a name="execution-log-properties-schema"></a>Schéma de propriétés des journaux d’exécution

Les journaux d’activité d’exécution contiennent des informations sur les événements qui se sont produits pendant l’exécution du travail Stream Analytics. Le schéma de propriétés varie selon que l’événement est une erreur de données ou un événement générique.

### <a name="data-errors"></a>Erreurs de données

Toute erreur qui se produit lorsque le travail traite des données est consignée dans cette catégorie de journaux d’activité. La plupart du temps, ces journaux d’activité sont créés au cours des opérations de lecture, de sérialisation et d’écriture des données. Ces journaux d’activité n’incluent pas les erreurs de connectivité. Les erreurs de connectivité sont traitées comme des événements génériques. Vous pouvez en apprendre davantage sur la cause des différentes [erreurs de données d’entrée et de sortie](https://docs.microsoft.com/azure/stream-analytics/data-errors).

Name | Description
------- | -------
Source | Nom de l’entrée ou de la sortie du travail où l’erreur s’est produite.
Message | Message associé à l’erreur.
Type | Type d'erreur Par exemple, **DataConversionError**, **CsvParserError** ou **ServiceBusPropertyColumnMissingError**.
Données | Contient des données utiles pour localiser avec précision la source de l’erreur. Troncation possible en fonction de la taille.

En fonction de la valeur **operationName**, les erreurs de données ont le schéma suivant :

* Les **événements de sérialisation** se produisent pendant les opérations de lecture d’événements, lorsque les données en entrée ne répondent pas aux conditions du schéma de requête pour l’une des raisons suivantes :

   * *Incompatibilité de type pendant la (dé)sérialisation de l’événement :* identifie le champ à l’origine de l’erreur.

   * *Impossible de lire un événement, sérialisation non valide* : fournit des informations sur l’emplacement où l’erreur s’est produite dans les données d’entrée. (nom d’objet blob pour une entrée d’objet blob, décalage et exemple de données).

* Les **événements d’envoi** surviennent pendant les opérations d’écriture. Ils identifient l’événement de streaming à l’origine de l’erreur.

### <a name="generic-events"></a>Événements génériques

Les événements génériques couvrent tout le reste.

Name | Description
-------- | --------
Error | (facultatif) Informations sur l’erreur, en général des informations sur l’exception si celles-ci sont disponibles.
Message| Message de journal.
Type | Type de message, correspond à la catégorisation interne des erreurs. Par exemple, **JobValidationError** ou **BlobOutputAdapterInitializationFailure**.
ID de corrélation : | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) qui identifie de façon unique l’exécution du travail. Toutes les entrées du journal d’exécution générées depuis le démarrage du travail jusqu’à son arrêt ont le même **ID de corrélation**.

## <a name="next-steps"></a>Étapes suivantes

* [Présentation de Stream Analytics](stream-analytics-introduction.md)
* [Prise en main de Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l’échelle des travaux Stream Analytics](stream-analytics-scale-jobs.md)
* [Informations de référence sur le langage de requête Stream Analytics](https://docs.microsoft.com/stream-analytics-query/stream-analytics-query-language-reference)
* [Erreurs de données Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/data-errors)
