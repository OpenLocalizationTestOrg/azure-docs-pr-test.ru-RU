---
title: "оповещения tooset aaaUse Powershell в Application Insights | Документы Microsoft"
description: "Автоматизируйте настройку tooget Application Insights по электронной почте о изменениях метрики."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Используйте PowerShell tooset предупреждения в Application Insights
Можно автоматизировать настройку hello [оповещения](app-insights-alerts.md) в [Application Insights](app-insights-overview.md).

Кроме того, вы можете [задать оповещения tooan ответа веб-перехватчиков tooautomate](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

> [!NOTE]
> Если требуется toocreate ресурсы и оповещения на hello таким же времени, рассмотрите возможность [с помощью шаблона Azure Resource Manager](app-insights-powershell.md).
>
>

## <a name="one-time-setup"></a>Однократная настройка
Если вы ранее не использовали PowerShell для подписки Azure:

Установка модуля Azure Powershell hello на hello компьютер, где toorun hello скриптов.

* Установите [установщик веб-платформы Майкрософт (версии 5 или более поздней)](http://www.microsoft.com/web/downloads/platform.aspx).
* Используйте его tooinstall Microsoft Azure Powershell

## <a name="connect-tooazure"></a>Подключение tooAzure
Запустите Azure PowerShell и [подключения подписки tooyour](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>Получение оповещений
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Добавление оповещения
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>Пример 1
Отправить мне электронное сообщение, если выполняется медленнее, чем 1 секунду запросов tooHTTP ответа сервера hello, Усредненное за 5 минут. Мой ресурс Application Insights называется IceCreamWebApp, и он находится в группе ресурсов Fabrikam. Я hello владельца hello подписки Azure.

Hello GUID — идентификатор подписки hello (не hello ключ инструментирования приложения hello).

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>Пример 2
У меня есть приложение, в котором используется [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport метрику с именем «salesPerHour.» Отправьте сообщение электронной почты toomy коллег, если «salesPerHour» становится меньше 100, Усредненное более 24 часов.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

такие же правила можно использовать для метрики hello Hello отчет с помощью hello [измерения параметра](app-insights-api-custom-events-metrics.md#properties) отслеживания другого вызова, например TrackEvent или trackPageView.

## <a name="metric-names"></a>Имена метрик
| Имя метрики | Имя экрана | Описание |
| --- | --- | --- |
| `basicExceptionBrowser.count` |Исключения браузера |Число неперехваченных исключений в браузере hello. |
| `basicExceptionServer.count` |Исключения сервера |Число необработанных исключений выданных приложение hello |
| `clientPerformance.clientProcess.value` |Время обработки клиента |Время между получением hello получения последнего байта документа до загрузки модели DOM hello. Обработка асинхронных запросов может продолжаться. |
| `clientPerformance.networkConnection.value` |Время подключения к сети при загрузке страницы |Браузер hello времени занимает tooconnect toohello сети. Может быть 0, если страница в кэше. |
| `clientPerformance.receiveRequest.value` |Время получения ответа |Время между браузера при отправке ответа tooreceive toostarting запрос. |
| `clientPerformance.sendRequest.value` |Время отправки запроса |Время выполнения запроса toosend обозревателя. |
| `clientPerformance.total.value` |Время загрузки страницы в браузере |Время с момента отправки запроса пользователя до загрузки DOM, таблиц стилей, сценариев и изображений. |
| `performanceCounter.available_bytes.value` |Объем доступной памяти |Физическая память, доступная для использования процессами или системой. |
| `performanceCounter.io_data_bytes_per_sec.value` |Скорость обработки операций ввода-вывода |Всего байт на второй чтения и записи toofiles, сети и устройства. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |Частота порождения исключений |Количество исключений, порождаемых в секунду. |
| `performanceCounter.percentage_processor_time.value` |Обработка ЦП |Процент времени, затраченного всеми потоками процесса, используемые инструкции tooexecution hello процессора для процесса приложения hello Hello. |
| `performanceCounter.percentage_processor_total.value` |Процессорное время |Hello процент времени, hello процессора, затраченного в активные потоки. |
| `performanceCounter.process_private_bytes.value` |Количество байтов исключительного использования процессов |Память, исключительно назначенная toohello мониторинг процессов приложения. |
| `performanceCounter.request_execution_time.value` |Время выполнения запроса ASP.NET |Время выполнения последнего запроса hello. |
| `performanceCounter.requests_in_application_queue.value` |Число запросов ASP.NET в очереди выполнения |Длина очереди запросов приложения hello. |
| `performanceCounter.requests_per_sec.value` |Частота запросов ASP.NET |Скорость всех запросов toohello приложение в секунду из ASP.NET. |
| `remoteDependencyFailed.durationMetric.count` |Ошибки зависимости |Количество неудачных вызовов, сделанных ресурсы tooexternal hello сервера приложений. |
| `request.duration` |Время ответа от сервера |Время между получения HTTP-запроса и завершением отправки ответа hello. |
| `request.rate` |Частота запросов |Частота всех запросов, toohello приложение в секунду. |
| `requestFailed.count` |Failed requests (Неудачные запросы) |Число HTTP-запросов, приведших к отображению кода ответа >= 400. |
| `view.count` |Просмотры страниц |Количество клиентских запросов пользователя для веб-страницы. Искусственный трафик отфильтровывается. |
| {имя пользовательской метрики} |{имя метрики} |Сообщаемые вашей значение метрики [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) или в hello [параметр измерения отслеживания вызова](app-insights-api-custom-events-metrics.md#properties). |

метрики Hello не будут отправлены в разных телеметрии модули:

| Группа метрик | Модуль сборщика |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>view |[Browser JavaScript](app-insights-javascript.md) |
| performanceCounter |[Производительность](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[Dependency](app-insights-configuration-with-applicationinsights-config.md) |
| request,<br/>requestFailed |[Server request](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Объекты Webhook
Вы можете [автоматизировать оповещения tooan ответ](../monitoring-and-diagnostics/insights-webhooks-alerts.md). При возникновении оповещения Azure будет вызывать выбранный вами веб-адрес.

## <a name="see-also"></a>См. также
* [Сценарий tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [Создание ресурсов Application Insights и веб-тестов на основе шаблонов](app-insights-powershell.md)
* [Автоматизация взаимозависимость аналитики tooApplication системы диагностики Microsoft Azure](app-insights-powershell-azure-diagnostics.md)
* [Автоматизация оповещения tooan ответа](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
