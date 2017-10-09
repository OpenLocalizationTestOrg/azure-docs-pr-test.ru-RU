---
title: "tooalerts aaaResponses в аналитику журнала OMS | Документы Microsoft"
description: "Предупреждения в службе анализа журналов определить важную информацию в репозитории OMS и можно заранее уведомлять вас о проблемах или вызова действия tooattempt toocorrect их.  В этой статье описывается, как toocreate правила оповещения и сведения о hello различные действия они могут получить."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>Добавьте правила tooalert действия в службе анализа журналов
Когда [предупреждение создается в службе анализа журналов](log-analytics-alerts.md), предусмотрена возможность hello [Настройка правила оповещения hello](log-analytics-alerts.md) tooperform одно или несколько действий.  Эта статья описывает hello различные действия, которые доступны и сведения о настройке каждого типа.

| Действие | Описание |
|:--|:--|
| [Электронная почта](#email-actions) | Отправьте электронное письмо с подробными сведениями hello предупреждения tooone hello или нескольких получателей. |
| [webhook](#webhook-actions) | Вызов внешнего процесса с помощью одного запроса HTTP POST. |
| [Runbook](#runbook-actions) | Запуск модуля Runbook в службе автоматизации Azure. |


## <a name="email-actions"></a>Действия электронной почты
Действия по электронной почте Отправить электронное письмо с подробными сведениями hello предупреждения tooone hello или нескольких получателей.  Можно указать hello тему hello mail, но его содержимое — это стандартный формат, созданный службой аналитики журналов.  Он включает сводные сведения, такие как имя hello предупреждение hello в toodetails сложения из записей tooten возвращенных hello поиска журналов.  Она также включает поиска журнала tooa ссылку для анализа журналов, которая вернет hello полного набора записей из этого запроса.   Отправитель Hello почты hello *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* . 

Действия электронной почты требуют свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| Субъект |Темы в сообщении электронной почты hello.  Не удается изменить текст hello почты hello. |
| Recipients |Адреса всех получателей электронной почты.  Если указать более одного адреса, а затем отдельной hello адреса точкой с запятой (;). |


## <a name="webhook-actions"></a>Действия webhook

Веб-перехватчика действия позволяют проводить tooinvoke внешний процесс с помощью одного запроса HTTP POST.  вызываемой службы Hello следует поддерживать веб-перехватчиков и определить, как использовать все полезные данные получит.  Можно также вызвать API REST, который не поддерживает специально веб-перехватчики при условии, что запрос hello находится в формате, который понимает API hello.  Примеры использования веб-перехватчик в предупреждении tooan ответ отправляется сообщение [Slack](http://slack.com) или создании инцидента в [PagerDuty](http://pagerduty.com/).  Полное Пошаговое руководство по Создание правила оповещения с помощью веб-перехватчика toocall Slack доступен на [веб-привязок к службе анализа журналов оповещений](log-analytics-alerts-webhooks.md).

Веб-перехватчика действия требуют свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| URL-адрес Webhook |Hello URL-адрес веб-перехватчика hello. |
| Настраиваемые полезные данные JSON |Toosend настраиваемые полезные данные с веб-перехватчика hello.  Дополнительные сведения см. ниже. |


Веб-перехватчиков включают URL-адрес и полезные данные форматирования в формате JSON, hello данные отправляются toohello внешней службы.  По умолчанию hello полезных данных будет содержать значения hello в hello в следующей таблице.  Вы можете tooreplace эти полезные данные с новый самостоятельно.  В этом случае можно использовать переменные hello hello таблицы для каждого из параметров tooinclude hello их значения в настраиваемые полезные данные.

| Параметр | Переменная | Описание |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Имя правила оповещения hello. |
| AlertThresholdOperator |#thresholdoperator |Оператор пороговое значение для правила оповещения hello.  *Больше* или *Меньше*. |
| AlertThresholdValue |#thresholdvalue |Пороговое значение для правила оповещения hello. |
| LinkToSearchResults |#linktosearchresults |Свяжите tooLog поиска журналов для аналитики, возвращающий hello записи из hello запрос, созданный hello предупреждение. |
| ResultCount |#searchresultcount |Число записей в результатах поиска hello. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Время окончания для hello запроса в формате UTC. |
| SearchIntervalInSeconds |#searchinterval |Окно времени для правила оповещения hello. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Время начала для hello запроса в формате UTC. |
| SearchQuery |#searchquery |Запрос поиска журнала используются правилом оповещения hello. |
| SearchResults |См. ниже |Записей, возвращаемых запросом hello в формате JSON.  Ограниченная toohello первых 5 000 записей. |
| WorkspaceID |#workspaceid |Идентификатор рабочей области OMS |

Например, можно указать следующие настраиваемые полезные данные, который включает один параметр с именем hello *текст*.  Этот параметр будет ожидать Hello служба, которая вызывает этот веб-перехватчик.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Этот пример полезных данных разрешится toosomething как hello при после отправки toohello веб-перехватчика.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

Результаты поиска tooinclude в настраиваемые полезные данные, добавьте hello, следующей строкой как свойство верхнего уровня в полезных данных json hello.  

    "IncludeSearchResults":true

Например toocreate настраиваемые полезные данные, включает только имя предупреждения hello и результаты поиска hello, можно использовать следующие hello. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


Вы можете выполнить полный пример создания правила оповещения с toostart веб-перехватчика внешней службы в [создания оповещений веб-перехватчика действий в tooSlack сообщения toosend аналитики журнала OMS](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Действия Runbook
Действия Runbook запускают модуль Runbook в службе автоматизации Azure.  Чтобы toouse этот тип действий, необходимо иметь hello [решение автоматизации](log-analytics-add-solutions.md) устанавливается и настраивается в рабочей области OMS.  Можно выбрать из модулей Runbook hello в учетной записи автоматизации hello, настроенного в hello решение автоматизации.

Действия Runbook требуют свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:---|
| Модуль Runbook | Модуль Runbook будет toostart при создании оповещения. |
| Запуск на | Укажите **Azure** toorun hello runbook в облаке hello.  Укажите **гибридной рабочей роли** toorun runbook hello на агенте с [гибридной рабочей ролью Runbook](../automation/automation-hybrid-runbook-worker.md ) установлен.  |

Запуск действия Runbook hello runbook с помощью [веб-перехватчика](../automation/automation-webhooks.md).  При создании правила оповещения hello, он автоматически создаст новый веб-перехватчика для hello runbook с именем hello **исправления оповещения OMS** идентификатор GUID.  

Невозможно напрямую заполнить все параметры модуля runbook hello, но, hello [$WebhookData параметр](../automation/automation-webhooks.md) будет включать сведения hello hello предупреждении, включая hello результатов поиска журналов hello, в которой он был создан.  Hello runbook потребуется toodefine **$WebhookData** как параметр для него tooaccess hello свойства предупреждения hello.  Hello данных предупреждений в формате json в одиночное свойство **SearchResults** в hello **RequestBody** свойство **$WebhookData**.  Это окажет со свойствами hello в hello в следующей таблице.

| Узел | Описание |
|:--- |:--- |
| id |Путь и идентификатор GUID для поиска hello. |
| __metadata |Сведения о hello предупреждения включая hello количество записей и состоянии hello результатов поиска. |
| value |Отдельную запись для каждой записи в результатах поиска hello.  Hello сведения о записи hello будет соответствовать hello свойства и значения записи hello. |

Например hello следующие runbook следует извлечь hello записей, возвращаемых поиска журналов hello и назначить различные свойства, в зависимости от типа hello каждой записи.  Обратите внимание, runbook hello запускается путем преобразования **RequestBody** из json, так что он может работать как объект в PowerShell.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>Дальнейшие действия
- Вы можете выполнить пошаговое руководство по [настройке webook](log-analytics-alerts-webhooks.md) с использованием правила генерации оповещений.  
- Узнайте, как toowrite [Runbook в автоматизации Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate проблемы определяется предупреждения.
