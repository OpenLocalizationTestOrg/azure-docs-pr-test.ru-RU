---
title: "Настройка диагностики Azure для отправки данных в Application Insights | Документация Майкрософт"
description: "Обновление открытой конфигурации диагностики Azure для отправки данных в Application Insights."
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
ms.openlocfilehash: 67dc2d5bbfa2012e4e098616edda593d023c4c1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="1af47-103">Отправка в Application Insights диагностических данных облачной службы, виртуальной машины или Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1af47-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="1af47-104">Облачные службы, виртуальные машины, масштабируемые наборы виртуальных машин и Service Fabric используют расширение системы диагностики Azure для сбора данных.</span><span class="sxs-lookup"><span data-stu-id="1af47-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="1af47-105">Система диагностики Azure отправляет данные в таблицы службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1af47-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="1af47-106">Тем не менее эти данные можно также полностью или частично передавать в другие расположения, используя расширение системы диагностики Azure 1.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1af47-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="1af47-107">В этой статье описывается, как отправлять данные из расширения системы диагностики Azure в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1af47-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="1af47-108">Описание конфигурации системы диагностики</span><span class="sxs-lookup"><span data-stu-id="1af47-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="1af47-109">Расширение системы диагностики Azure 1.5 вводит понятие приемников — дополнительных расположений, в которые можно отправлять диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="1af47-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="1af47-110">Ниже приведен пример конфигурации приемника для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1af47-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="1af47-111">Атрибут **Sink** *name* — это строковое значение, однозначно определяющее приемник.</span><span class="sxs-lookup"><span data-stu-id="1af47-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="1af47-112">Элемент **ApplicationInsights** указывает ключ инструментирования ресурса Application Insights, в который отправляются диагностические данные Azure.</span><span class="sxs-lookup"><span data-stu-id="1af47-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="1af47-113">Если ресурс Application Insights еще не существует, см. статью [Создание нового ресурса Application Insights](../application-insights/app-insights-create-new-resource.md), где содержатся дополнительные сведения о создании ресурса и получении ключа инструментирования.</span><span class="sxs-lookup"><span data-stu-id="1af47-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="1af47-114">При разработке облачной службы с использованием пакета SDK для Azure 2.8 и более поздних версий этот ключ инструментирования заполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="1af47-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="1af47-115">При упаковке проекта облачной службы это значение задается на основе параметра конфигурации службы **APPINSIGHTS_INSTRUMENTATIONKEY**.</span><span class="sxs-lookup"><span data-stu-id="1af47-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="1af47-116">См. статью [Устранение неполадок облачных служб с помощью Application Insights](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="1af47-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="1af47-117">Элемент **Channels** содержит один или несколько элементов **Channel**.</span><span class="sxs-lookup"><span data-stu-id="1af47-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="1af47-118">Атрибут *name* однозначно ссылается на этот канал.</span><span class="sxs-lookup"><span data-stu-id="1af47-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="1af47-119">Атрибут *Loglevel* позволяет указать уровень ведения журнала для канала.</span><span class="sxs-lookup"><span data-stu-id="1af47-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="1af47-120">Доступны следующие уровни ведения журнала (от наиболее к наименее информативным):</span><span class="sxs-lookup"><span data-stu-id="1af47-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="1af47-121">Подробная информация</span><span class="sxs-lookup"><span data-stu-id="1af47-121">Verbose</span></span>
        - <span data-ttu-id="1af47-122">Информация</span><span class="sxs-lookup"><span data-stu-id="1af47-122">Information</span></span>
        - <span data-ttu-id="1af47-123">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="1af47-123">Warning</span></span>
        - <span data-ttu-id="1af47-124">Ошибка</span><span class="sxs-lookup"><span data-stu-id="1af47-124">Error</span></span>
        - <span data-ttu-id="1af47-125">критические ошибки.</span><span class="sxs-lookup"><span data-stu-id="1af47-125">Critical</span></span>

<span data-ttu-id="1af47-126">Канал действует как фильтр и позволяет выбрать конкретные уровни ведения журнала для отправки в приемник.</span><span class="sxs-lookup"><span data-stu-id="1af47-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="1af47-127">Например, можно собирать подробные журналы и отправлять их в хранилище, а в приемник отправлять только журнал ошибок.</span><span class="sxs-lookup"><span data-stu-id="1af47-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="1af47-128">Эта взаимосвязь показана на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="1af47-128">The following graphic shows this relationship.</span></span>

![Открытая конфигурация диагностики](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="1af47-130">На следующем рисунке показаны значения конфигурации и как они работают.</span><span class="sxs-lookup"><span data-stu-id="1af47-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="1af47-131">В конфигурацию можно включить несколько приемников на разных уровнях иерархии.</span><span class="sxs-lookup"><span data-stu-id="1af47-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="1af47-132">Приемник, указанный на верхнем уровне, действует как глобальный параметр, а приемник, указанный на уровне отдельного элемента, действует как переопределение для этого глобального параметра.</span><span class="sxs-lookup"><span data-stu-id="1af47-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Конфигурация приемников системы диагностики с Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="1af47-134">Полный пример конфигурации приемника</span><span class="sxs-lookup"><span data-stu-id="1af47-134">Complete sink configuration example</span></span>
<span data-ttu-id="1af47-135">Ниже приведен полный пример файла общедоступной конфигурации, которая:</span><span class="sxs-lookup"><span data-stu-id="1af47-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="1af47-136">Отправляет все ошибки в службу Application Insights (указанную в узле **DiagnosticMonitorConfiguration**).</span><span class="sxs-lookup"><span data-stu-id="1af47-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="1af47-137">Отправляет подробные журналы приложений (указанные в узле **Logs**).</span><span class="sxs-lookup"><span data-stu-id="1af47-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
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
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
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
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
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
<span data-ttu-id="1af47-138">В предыдущей конфигурации приведенные ниже строки имеют следующий смысл.</span><span class="sxs-lookup"><span data-stu-id="1af47-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="1af47-139">Отправка всех данных, собираемых системой диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="1af47-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="1af47-140">Отправка в приемник Application Insights только журналов ошибок</span><span class="sxs-lookup"><span data-stu-id="1af47-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="1af47-141">Отправка подробных журналов приложений в Application Insights</span><span class="sxs-lookup"><span data-stu-id="1af47-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="1af47-142">Ограничения</span><span class="sxs-lookup"><span data-stu-id="1af47-142">Limitations</span></span>

- <span data-ttu-id="1af47-143">**Каналы могут вести журнал типов, но не счетчиков производительности.**</span><span class="sxs-lookup"><span data-stu-id="1af47-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="1af47-144">Если указать канал с элементом счетчика производительности, он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="1af47-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="1af47-145">**Уровень ведения журнала для канала не может превышать уровень ведения журнала, данные которого собираются системой диагностики Azure.**</span><span class="sxs-lookup"><span data-stu-id="1af47-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="1af47-146">Например, нельзя собирать данные об ошибках в журнале приложений в элементе Logs и пытаться отправлять подробные журналы в приемник Application Insight.</span><span class="sxs-lookup"><span data-stu-id="1af47-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="1af47-147">Атрибут *ScheduledTransferLogLevelFilter* должен всегда собирать равное или большее число журналов, чем число журналов, которые вы пытаетесь отправить в приемник.</span><span class="sxs-lookup"><span data-stu-id="1af47-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="1af47-148">**В Application Insights нельзя отправлять собранные расширением системы диагностики Azure данные больших двоичных объектов.**</span><span class="sxs-lookup"><span data-stu-id="1af47-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="1af47-149">Например, данные, указанные в узле *Directories*.</span><span class="sxs-lookup"><span data-stu-id="1af47-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="1af47-150">Что касается аварийных дампов, фактический аварийный дамп отправляется в хранилище BLOB-объектов, а в Application Insights отправляется только уведомление о том, что аварийный дамп был создан.</span><span class="sxs-lookup"><span data-stu-id="1af47-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1af47-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1af47-151">Next Steps</span></span>
* <span data-ttu-id="1af47-152">Узнайте, как [просматривать данные диагностики Azure](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="1af47-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="1af47-153">Используйте [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md), чтобы включить расширение диагностики Azure для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="1af47-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="1af47-154">Используйте [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) , чтобы включить расширение диагностики Azure для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="1af47-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
