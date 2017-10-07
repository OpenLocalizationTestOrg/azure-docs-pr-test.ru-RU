---
title: "оповещения aaaCreate для служб Azure - PowerShell | Документы Microsoft"
description: "Триггер сообщения электронной почты, уведомления, вызовите URL-адреса веб-сайтов (веб-перехватчиков) или автоматизации при соблюдении заданных условий hello."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a>Создание оповещений метрик в Azure Monitor для служб Azure с помощью PowerShell
> [!div class="op_single_selector"]
> * [Портал](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Обзор
В этой статье показано, как tooset копирование Azure метрики оповещений с помощью PowerShell.  

Вы можете получать оповещения на основе отслеживания метрик или событий в службах Azure.

* **Значения метрик** - hello предупредить триггеры hello значение указанной метрики пересекает пороговое значение, присваиваемое в любом направлении. То есть, и триггеров при hello сначала условия, и затем позже при, условия больше не выполнены.    
* **События журнала действий**. Оповещение может активироваться при *каждом* событии или только тогда, когда выполняются определенные события. Дополнительные сведения об активности журнала предупреждений toolearn [щелкните здесь](monitoring-activity-log-alerts.md)

Вы можете настроить метрики оповещений toodo hello следующие при инициировании:

* Отправить администратору службы toohello уведомлений электронной почты и соадминистраторы
* Отправьте по электронной почте tooadditional сообщений электронной почты, указанных вами.
* вызов webhook;
* Запустите выполнение runbook для Azure (только из hello портал Azure)

Для настройки правил генерации оповещений и получении сведений о них можно использовать:

* [Портал Azure](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [интерфейс командной строки (CLI)](insights-alerts-command-line-interface.md)
* [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)

Дополнительные сведения, всегда можно ввести ```Get-Help``` и затем hello команду PowerShell, требуется получить справку.

## <a name="create-alert-rules-in-powershell"></a>Создание правил генерации оповещений в PowerShell
1. Войдите в tooAzure.   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. Получить список подписок hello достаточно. Убедитесь, что вы работаете с hello правильные подписка. Если нет, присвойте ему значение toohello вправо на один с выходными данными hello `Get-AzureRmSubscription`.

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. toolist существующие правила в группе ресурсов, hello используйте следующую команду:

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. toocreate правило, требуется toohave несколько важных аспекта сведений сначала.

  * Hello **идентификатор ресурса** для hello ресурса требуется tooset оповещение для
  * Hello **определения показателей** доступны для этого ресурса

     Одним из способов tooget hello идентификатор ресурса — toouse hello портал Azure. Предположим, что ресурс hello уже создан, выберите его в портал hello. Выберите в колонке Далее hello *свойства* под hello *параметры* раздела. **Идентификатор РЕСУРСА** — это поле в колонке Далее hello. Другим способом является toouse hello [обозревателя ресурсов Azure](https://resources.azure.com/).

     Ниже приведен пример идентификатора ресурса для веб-приложения.

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     Можно использовать `Get-AzureRmMetricDefinition` список hello tooview все определения показателей для конкретного ресурса.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     Hello следующий пример создает таблицу с метрикой hello имя и hello единицы для этой метрики.

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     Полный список доступных параметров Get-AzureRmMetricDefinition можно получить, выполнив Get-MetricDefinitions.
5. Здравствуйте, следующий пример настраивает оповещение на ресурс веб-сайта. Hello предупреждения триггеры всякий раз, когда постоянно получает любой трафик, 5 минут, и снова при получении трафика на 5 минут.

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. toocreate веб-перехватчик или отправить электронную почту, если оповещение триггерами, сначала создайте hello электронной почты и/или веб-привязок. Немедленно создайте правило hello позже с hello - тег действия и, как показано в следующий пример hello. С помощью PowerShell невозможно связать webhook или электронные адреса с уже созданными правилами.

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. tooverify, что оповещения были созданы правильно, просмотрев hello отдельных правил.

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. Удалите свои оповещения. Эти команды удаляют hello правил, созданных ранее в этой статье.

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор мониторинг Azure](monitoring-overview.md) включая hello типы данных, можно собирать и контролировать.
* Узнайте больше о [настройке веб-перехватчиков webhook в оповещениях](insights-webhooks-alerts.md).
* Узнайте больше о [настройке оповещений о событиях журнала действий](monitoring-activity-log-alerts.md).
* Узнайте больше о [модулях Runbook службы автоматизации Azure](../automation/automation-starting-a-runbook.md).
* Получить [Обзор сбора журналов диагностики](monitoring-overview-of-diagnostic-logs.md) toocollect подробные показатели высокой частотой в службе.
* Получить [Обзор сбора метрик](insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.
