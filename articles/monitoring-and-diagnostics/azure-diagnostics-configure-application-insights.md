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
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="9f787-103">Отправить облачной службы, виртуальную машину или Service Fabric tooApplication диагностических данных аналитики</span><span class="sxs-lookup"><span data-stu-id="9f787-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="9f787-104">Облачные службы, виртуальных машин, наборы масштабирования виртуальных машин и Service Fabric использовать данные toocollect расширения системы диагностики Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9f787-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="9f787-105">Диагностика Azure отправляет tooAzure данных таблиц хранилища.</span><span class="sxs-lookup"><span data-stu-id="9f787-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="9f787-106">Тем не менее вы также можете канала все или часть hello данных tooother расположения с помощью модуля диагностики Azure 1.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="9f787-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="9f787-107">В этой статье описывается, как данные toosend из hello tooApplication расширения системы диагностики Azure Insights.</span><span class="sxs-lookup"><span data-stu-id="9f787-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="9f787-108">Описание конфигурации системы диагностики</span><span class="sxs-lookup"><span data-stu-id="9f787-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="9f787-109">Здравствуйте, приемники расширения 1.5 появились диагностики Azure, являющиеся дополнительные папки, куда можно отправлять диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="9f787-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="9f787-110">Ниже приведен пример конфигурации приемника для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9f787-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="9f787-111">Hello **приемник** *имя* атрибут является строковое значение, однозначно определяющее hello приемника.</span><span class="sxs-lookup"><span data-stu-id="9f787-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="9f787-112">Hello **ApplicationInsights** элемент указывает ключ инструментирования hello ресурс Application insights, куда отправлять данные диагностики Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9f787-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="9f787-113">Если у вас нет существующего ресурса Application Insights, см. раздел [создать новый ресурс Application Insights](../application-insights/app-insights-create-new-resource.md) Дополнительные сведения о создании ресурса и получении ключа инструментирования hello.</span><span class="sxs-lookup"><span data-stu-id="9f787-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="9f787-114">При разработке облачной службы с использованием пакета SDK для Azure 2.8 и более поздних версий этот ключ инструментирования заполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="9f787-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="9f787-115">Hello значение основано на hello **APPINSIGHTS_INSTRUMENTATIONKEY** параметр конфигурации службы при упаковке проекта облачной службы hello.</span><span class="sxs-lookup"><span data-stu-id="9f787-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="9f787-116">В разделе [проблемы используйте Application Insights с tootroubleshoot диагностики Azure облачной службы](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="9f787-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="9f787-117">Hello **каналы** элемент содержит один или несколько **канала** элементов.</span><span class="sxs-lookup"><span data-stu-id="9f787-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="9f787-118">Hello *имя* атрибут однозначно ссылается toothat канала.</span><span class="sxs-lookup"><span data-stu-id="9f787-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="9f787-119">Hello *loglevel* атрибут позволяет указать уровень ведения журнала hello, hello канал позволяет.</span><span class="sxs-lookup"><span data-stu-id="9f787-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="9f787-120">уровни доступное среди резервных Hello в порядке наиболее tooleast сведения являются:</span><span class="sxs-lookup"><span data-stu-id="9f787-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="9f787-121">Подробная информация</span><span class="sxs-lookup"><span data-stu-id="9f787-121">Verbose</span></span>
        - <span data-ttu-id="9f787-122">Информация</span><span class="sxs-lookup"><span data-stu-id="9f787-122">Information</span></span>
        - <span data-ttu-id="9f787-123">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="9f787-123">Warning</span></span>
        - <span data-ttu-id="9f787-124">Ошибка</span><span class="sxs-lookup"><span data-stu-id="9f787-124">Error</span></span>
        - <span data-ttu-id="9f787-125">критические ошибки.</span><span class="sxs-lookup"><span data-stu-id="9f787-125">Critical</span></span>

<span data-ttu-id="9f787-126">Канал действует как фильтр и предоставляет tooselect определенном журнале уровни toosend toohello целевой приемника.</span><span class="sxs-lookup"><span data-stu-id="9f787-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="9f787-127">Например может собирать подробные журналы и отправлять их toostorage, но отправлять только ошибки toohello приемника.</span><span class="sxs-lookup"><span data-stu-id="9f787-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="9f787-128">Hello следующий рисунок демонстрирует эти отношения.</span><span class="sxs-lookup"><span data-stu-id="9f787-128">hello following graphic shows this relationship.</span></span>

![Открытая конфигурация диагностики](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="9f787-130">Следующий график Hello перечислены значения конфигурации hello и принципы их работы.</span><span class="sxs-lookup"><span data-stu-id="9f787-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="9f787-131">Можно включить несколько приемников в hello конфигурации на разных уровнях иерархии hello.</span><span class="sxs-lookup"><span data-stu-id="9f787-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="9f787-132">приемник Hello на верхнем уровне hello действует как глобальный параметр и hello один указало на отдельных hello элемент ведет себя как глобальные настройки toothat переопределение.</span><span class="sxs-lookup"><span data-stu-id="9f787-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Конфигурация приемников системы диагностики с Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="9f787-134">Полный пример конфигурации приемника</span><span class="sxs-lookup"><span data-stu-id="9f787-134">Complete sink configuration example</span></span>
<span data-ttu-id="9f787-135">Ниже приведен полный пример hello открытой конфигурации файла, который</span><span class="sxs-lookup"><span data-stu-id="9f787-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="9f787-136">отправляет все ошибки tooApplication аналитики (определено на hello **DiagnosticMonitorConfiguration** узла)</span><span class="sxs-lookup"><span data-stu-id="9f787-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="9f787-137">также отправляет подробных журналов уровня для hello журналы приложений (определено на hello **журналы** узла).</span><span class="sxs-lookup"><span data-stu-id="9f787-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

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
<span data-ttu-id="9f787-138">В предыдущей конфигурации hello hello следующие строки имеют hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="9f787-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="9f787-139">Отправлять все данные hello, которые собираются системой диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="9f787-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="9f787-140">Отправлять только журналы toohello Application Insights приемником ошибок</span><span class="sxs-lookup"><span data-stu-id="9f787-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="9f787-141">Отправлять журналы аналитики tooApplication Verbose приложений</span><span class="sxs-lookup"><span data-stu-id="9f787-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="9f787-142">Ограничения</span><span class="sxs-lookup"><span data-stu-id="9f787-142">Limitations</span></span>

- <span data-ttu-id="9f787-143">**Каналы могут вести журнал типов, но не счетчиков производительности.**</span><span class="sxs-lookup"><span data-stu-id="9f787-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="9f787-144">Если указать канал с элементом счетчика производительности, он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="9f787-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="9f787-145">**Hello уровень ведения журнала для канала не может превышать hello уровень ведения журнала для что собираются с помощью диагностики Azure.**</span><span class="sxs-lookup"><span data-stu-id="9f787-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="9f787-146">Например нельзя собирать данные об ошибках в журнале приложений в элементе журналы hello и повторите toosend подробных журналов toohello Application Insight приемника.</span><span class="sxs-lookup"><span data-stu-id="9f787-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="9f787-147">Hello *scheduledTransferLogLevelFilter* атрибута необходимо собрать всегда равно или больше журналов, чем hello журналы вы пытаетесь toosend tooa приемника.</span><span class="sxs-lookup"><span data-stu-id="9f787-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="9f787-148">**Не удается отправить собранные tooApplication расширения системы диагностики Azure Insights данные большого двоичного объекта.**</span><span class="sxs-lookup"><span data-stu-id="9f787-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="9f787-149">Например, все, что указывается в разделе hello *каталоги* узла.</span><span class="sxs-lookup"><span data-stu-id="9f787-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="9f787-150">Аварийные дампы фактическое аварийной копии памяти hello отправляется tooblob хранилища и был создан только уведомление, которое hello аварийный дамп отправляется tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="9f787-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f787-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f787-151">Next Steps</span></span>
* <span data-ttu-id="9f787-152">Узнайте, каким образом слишком[Просмотр данных диагностики Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9f787-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="9f787-153">Используйте [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello расширения службы диагностики Azure для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9f787-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="9f787-154">Используйте [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello расширения службы диагностики Azure для приложения</span><span class="sxs-lookup"><span data-stu-id="9f787-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
