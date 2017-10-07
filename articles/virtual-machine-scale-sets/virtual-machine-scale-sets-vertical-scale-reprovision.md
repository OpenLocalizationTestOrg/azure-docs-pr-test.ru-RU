---
title: "наборы масштабирования виртуальной машины Azure шкалы aaaVertically | Документы Microsoft"
description: "Как toovertically масштабирования виртуальной машины в ответ toomonitoring предупреждения в службе автоматизации Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a>Вертикальное автомасштабирование масштабируемых наборов виртуальных машин
В этой статье описывается, как toovertically масштабирования Azure [наборы масштабирования виртуальных машин](https://azure.microsoft.com/services/virtual-machine-scale-sets/) с или без инициализацию. Вертикального масштабирования виртуальных машин, которые отсутствуют в наборы масштабирования, см. в разделе слишком[вертикальное масштабирование виртуальной машины Azure в службе автоматизации Azure](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Вертикальное масштабирование, также известный как *масштабировать* и *масштабировать*, означает увеличение или уменьшение размеров виртуальных машин (ВМ) в рабочей нагрузки tooa ответа. Сравните это с [горизонтальное масштабирование](virtual-machine-scale-sets-autoscale-overview.md), также называется tooas *горизонтальное масштабирование* и *масштабирования в*, где hello число виртуальных машин, изменяется в зависимости от нагрузки hello.

Повторная подготовка означает удаление существующей виртуальной машины и ее замену новой. При увеличении или уменьшении размера hello виртуальных машин в наборе масштабирования виртуальных Машин, в некоторых случаях вы хотите tooresize существующие виртуальные машины и сохранить данные, а в других случаях необходимо toodeploy новых виртуальных машин, новый размер hello. В этом документе описываются оба сценария.

Когда полезно выполнять вертикальное масштабирование:

* Если служба, работающая на базе виртуальных машин, мало используется (например, в выходные). Уменьшение размера виртуальной Машины hello можно сократить ежемесячные расходы.
* Увеличение toocope размер виртуальной Машины с требованиями большего размера без создания дополнительных виртуальных машин.

Можно настроить по вертикали масштабирование toobe активации на основе метрики на основе предупреждений из набора масштабирования виртуальных Машин. Активируется hello оповещение срабатывает, веб-перехватчика, которая инициирует runbook, который можно масштабировать шкалу значение вверх или вниз. Вертикальное масштабирование можно настроить так:

1. Создайте учетную запись службы автоматизации Azure с возможностью запуска от имени.
2. Импортируйте в подписку модули Runbook службы автоматизации Azure для вертикального масштабирования.
3. Добавьте веб-перехватчика tooyour runbook.
4. Добавление оповещений tooyour, набора масштабирования виртуальных Машин с помощью веб-перехватчика уведомление.

> [!NOTE]
> Вертикальное автомасштабирование поддерживается только для виртуальных машин определенных размеров. Сравните спецификации hello каждого размера перед принятием решения об tooscale из одного tooanother (большее число не всегда обеспечивает больший размер виртуальной Машины). Вы можете tooscale между hello следующие пары размеров:
> 
> | Пары размеров виртуальных машин, для которых можно применять вертикальное масштабирование |  |
> | --- | --- |
> | Standard_A0 |Standard_A11 |
> | Standard_D1 |Standard_D14 |
> | Standard_DS1 |Standard_DS14 |
> | Standard_D1v2 |Standard_D15v2 |
> | Standard_G1 |Standard_G5 |
> | Standard_GS1 |Standard_GS5 |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a>Создание учетной записи службы автоматизации Azure с возможностью запуска от имени
Hello первое, что необходимо toodo — создать учетную запись службы автоматизации Azure, где будет размещаться hello модулей Runbook используется tooscale hello набора масштабирования виртуальных Машин экземпляры. Недавно [автоматизации Azure](https://azure.microsoft.com/services/automation/) появилась возможность «Запуск от имени учетной записи» hello, что делает настройку hello участника-службы для автоматического запуска модулей Runbook hello от имени пользователя очень просто. Можно прочитать подробнее об этом в статье hello ниже:

* [Проверка подлинности модулей Runbook в Azure с помощью учетной записи запуска от имени](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a>Импорт в подписку модулей Runbook службы автоматизации Azure для вертикального масштабирования
модули Runbook Hello требуется toovertically масштабирования вашего набора масштабирования виртуальных Машин уже публикуются в коллекции модулей Runbook службы автоматизации Azure hello. tooimport их в подписке hello, выполните шаги в этой статье:

* [Runbook и коллекции модулей для службы автоматизации Azure](../automation/automation-runbook-gallery.md)

Выберите вариант обзора коллекции hello меню hello модулей Runbook.

![Toobe модули Runbook импортированы][runbooks]

Hello Runbook, которые требуется импортировать toobe отображаются. Выберите runbook hello, в зависимости от того, нужно ли вертикальное масштабирование с или без инициализацию:

![Коллекция модулей Runbook][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a>Добавить модуль runbook tooyour веб-перехватчика
После импорта модулей Runbook hello необходимо tooadd runbook toohello веб-перехватчика, может быть вызвано предупреждение от набора масштабирования виртуальных Машин. в этой статье описаны Hello подробные сведения о создании веб-перехватчика для модуля Runbook.

* [Объекты Webhook в службе автоматизации Azure](../automation/automation-webhooks.md)

> [!NOTE]
> Убедитесь, что копирование веб-перехватчика hello URI перед закрытием диалогового окна веб-перехватчика hello, как он потребуется в следующем разделе hello.
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a>Добавление оповещений tooyour, набора масштабирования виртуальных Машин
Ниже приведен сценарий PowerShell, котором показывается, как tooadd предупреждения tooa, набора масштабирования виртуальных Машин. Ссылаться после имени hello tooget статье hello метрики toofire hello предупреждения toohello: [общих метрик автоматическое масштабирование Azure монитор](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> Это рекомендуется tooconfigure окна слишком много времени для предупреждения hello в tooavoid порядок запуска вертикального масштабирования, вместе со всеми связанными перерыва в обслуживании, слишком часто. Начните с интервала минимум в 20–30 минут. Рассмотрите возможность горизонтальное масштабирование, при необходимости tooavoid нарушения работы.
> 
> 

Дополнительные сведения о как toocreate предупреждений см. следующие статьи toohello:

* [Примеры для быстрого запуска Azure Insights с помощью PowerShell](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [Примеры команд для межплатформенного интерфейса командной строки Azure Insights](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a>Сводка
В этой статье описан простой способ вертикального масштабирования. Указанные блоки (работа с учетной записью службы автоматизации, модулями Runbook, веб-перехватчиками и оповещениями) позволяют включить в настраиваемый набор действий самые разные события.

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
