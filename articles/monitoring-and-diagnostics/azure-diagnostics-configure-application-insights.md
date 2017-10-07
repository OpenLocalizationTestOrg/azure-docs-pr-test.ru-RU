---
title: "aaaConfigure диагностики Azure toosend данных tooApplication аналитики | Документы Microsoft"
description: "Обновление данных toosend tooApplication аналитики hello Azure Diagnostics общедоступной конфигурации."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>Отправить облачной службы, виртуальную машину или Service Fabric tooApplication диагностических данных аналитики
Облачные службы, виртуальных машин, наборы масштабирования виртуальных машин и Service Fabric использовать данные toocollect расширения системы диагностики Azure hello.  Диагностика Azure отправляет tooAzure данных таблиц хранилища.  Тем не менее вы также можете канала все или часть hello данных tooother расположения с помощью модуля диагностики Azure 1.5 или более поздней версии.

В этой статье описывается, как данные toosend из hello tooApplication расширения системы диагностики Azure Insights.

## <a name="diagnostics-configuration-explained"></a>Описание конфигурации системы диагностики
Здравствуйте, приемники расширения 1.5 появились диагностики Azure, являющиеся дополнительные папки, куда можно отправлять диагностические данные.

Ниже приведен пример конфигурации приемника для Application Insights.

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- Hello **приемник** *имя* атрибут является строковое значение, однозначно определяющее hello приемника.

- Hello **ApplicationInsights** элемент указывает ключ инструментирования hello ресурс Application insights, куда отправлять данные диагностики Azure hello.
    - Если у вас нет существующего ресурса Application Insights, см. раздел [создать новый ресурс Application Insights](../application-insights/app-insights-create-new-resource.md) Дополнительные сведения о создании ресурса и получении ключа инструментирования hello.
    - При разработке облачной службы с использованием пакета SDK для Azure 2.8 и более поздних версий этот ключ инструментирования заполняется автоматически. Hello значение основано на hello **APPINSIGHTS_INSTRUMENTATIONKEY** параметр конфигурации службы при упаковке проекта облачной службы hello. В разделе [проблемы используйте Application Insights с tootroubleshoot диагностики Azure облачной службы](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).

- Hello **каналы** элемент содержит один или несколько **канала** элементов.
    - Hello *имя* атрибут однозначно ссылается toothat канала.
    - Hello *loglevel* атрибут позволяет указать уровень ведения журнала hello, hello канал позволяет. уровни доступное среди резервных Hello в порядке наиболее tooleast сведения являются:
        - Подробная информация
        - Информация
        - Предупреждение
        - Ошибка
        - критические ошибки.

Канал действует как фильтр и предоставляет tooselect определенном журнале уровни toosend toohello целевой приемника. Например может собирать подробные журналы и отправлять их toostorage, но отправлять только ошибки toohello приемника.

Hello следующий рисунок демонстрирует эти отношения.

![Открытая конфигурация диагностики](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

Следующий график Hello перечислены значения конфигурации hello и принципы их работы. Можно включить несколько приемников в hello конфигурации на разных уровнях иерархии hello. приемник Hello на верхнем уровне hello действует как глобальный параметр и hello один указало на отдельных hello элемент ведет себя как глобальные настройки toothat переопределение.

![Конфигурация приемников системы диагностики с Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>Полный пример конфигурации приемника
Ниже приведен полный пример hello открытой конфигурации файла, который
1. отправляет все ошибки tooApplication аналитики (определено на hello **DiagnosticMonitorConfiguration** узла)
2. также отправляет подробных журналов уровня для hello журналы приложений (определено на hello **журналы** узла).

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
В предыдущей конфигурации hello hello следующие строки имеют hello следующие значения:

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Отправлять все данные hello, которые собираются системой диагностики Azure

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>Отправлять только журналы toohello Application Insights приемником ошибок

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>Отправлять журналы аналитики tooApplication Verbose приложений

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>Ограничения

- **Каналы могут вести журнал типов, но не счетчиков производительности.** Если указать канал с элементом счетчика производительности, он игнорируется.
- **Hello уровень ведения журнала для канала не может превышать hello уровень ведения журнала для что собираются с помощью диагностики Azure.** Например нельзя собирать данные об ошибках в журнале приложений в элементе журналы hello и повторите toosend подробных журналов toohello Application Insight приемника. Hello *scheduledTransferLogLevelFilter* атрибута необходимо собрать всегда равно или больше журналов, чем hello журналы вы пытаетесь toosend tooa приемника.
- **Не удается отправить собранные tooApplication расширения системы диагностики Azure Insights данные большого двоичного объекта.** Например, все, что указывается в разделе hello *каталоги* узла. Аварийные дампы фактическое аварийной копии памяти hello отправляется tooblob хранилища и был создан только уведомление, которое hello аварийный дамп отправляется tooApplication аналитики.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[Просмотр данных диагностики Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) в Application Insights.
* Используйте [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello расширения службы диагностики Azure для вашего приложения.
* Используйте [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello расширения службы диагностики Azure для приложения
