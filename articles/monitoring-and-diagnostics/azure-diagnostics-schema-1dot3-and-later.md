---
title: "схема конфигурации 1.3 и более поздних версий расширения диагностики aaaAzure | Документы Microsoft"
description: "Схема версии 1.3 и более поздней версии Диагностика Azure поставляется как часть hello Microsoft Azure SDK 2.4 и более поздней версии."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: robb
ms.openlocfilehash: bd15d3a79ea818fcb3235854717e58d5da36518e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="d6704-103">Схема конфигурации системы диагностики Azure версии 1.3 и более поздней</span><span class="sxs-lookup"><span data-stu-id="d6704-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="d6704-104">Hello расширения системы диагностики Azure — компонент hello используется toocollect счетчики производительности и другие статистические данные из:</span><span class="sxs-lookup"><span data-stu-id="d6704-104">hello Azure Diagnostics extension is hello component used toocollect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="d6704-105">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="d6704-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="d6704-106">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d6704-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="d6704-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d6704-107">Service Fabric</span></span> 
> - <span data-ttu-id="d6704-108">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="d6704-108">Cloud Services</span></span> 
> - <span data-ttu-id="d6704-109">группы сетевой безопасности;</span><span class="sxs-lookup"><span data-stu-id="d6704-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="d6704-110">Данная страница применяется только в том случае, если вы используете одну из этих служб.</span><span class="sxs-lookup"><span data-stu-id="d6704-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="d6704-111">Эта страница предназначена для версий 1.3 и более поздних (пакет Azure SDK 2.4 и более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="d6704-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="d6704-112">Новые разделы конфигурации являются комментариями tooshow в какой версии, они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="d6704-112">Newer configuration sections are commented tooshow in what version they were added.</span></span>  

<span data-ttu-id="d6704-113">файл конфигурации Hello, описанные здесь — используется tooset диагностические параметры конфигурации, при запуске монитора диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-113">hello configuration file described here is used tooset diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

<span data-ttu-id="d6704-114">расширение Hello используется в сочетании с другими продуктами Майкрософт диагностики, как монитор Azure, Application Insights и анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="d6704-114">hello extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="d6704-115">Загрузите определение схемы файл открытой конфигурации hello, выполнив следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="d6704-115">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="d6704-116">Дополнительные сведения об использовании системы диагностики Azure см. в [этой статье](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d6704-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="d6704-117">Пример файла конфигурации диагностики hello</span><span class="sxs-lookup"><span data-stu-id="d6704-117">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="d6704-118">Следующий пример Hello показан типичный файл конфигурации диагностики:</span><span class="sxs-lookup"><span data-stu-id="d6704-118">hello following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

        <DockerSources> <!-- Added in 1.9 --> 
          <Stats enabled="true" sampleRate="PT1M" scheduledTransferPeriod="PT1M" />
        </DockerSources>

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

  </WadCfg>  

  <StorageAccount>diagstorageaccount</StorageAccount>
  <StorageType>TableAndBlob</StorageType> <!-- Added in 1.8 -->  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" sasToken="{sas token}"  />  <!-- sasToken in Private config added in 1.8.1 -->  
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
   
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
   
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

<span data-ttu-id="d6704-119">Эквивалент в формате JSON hello предыдущего XML-файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d6704-119">JSON equivalent of hello previous XML configuration file.</span></span> 

<span data-ttu-id="d6704-120">Поскольку в большинстве случаев использования json, они передаются как переменные разных разделяются Hello PublicConfig и PrivateConfig.</span><span class="sxs-lookup"><span data-stu-id="d6704-120">hello PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="d6704-121">К таким примерам относятся шаблоны Resource Manager, масштабируемый набор виртуальных машин PowerShell и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6704-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

```json
"PublicConfig" {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
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
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```json
"PrivateConfig" {
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a><span data-ttu-id="d6704-122">Чтение этой страницы</span><span class="sxs-lookup"><span data-stu-id="d6704-122">Reading this page</span></span>  
 <span data-ttu-id="d6704-123">Hello следующие теги располагаются примерно в порядке, показанном в предыдущих пример hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-123">hello tags following are roughly in order shown in hello preceding example.</span></span>  <span data-ttu-id="d6704-124">Если вы не видите полное описание, где ожидается, страница «поиск» hello hello элемента или атрибута.</span><span class="sxs-lookup"><span data-stu-id="d6704-124">If you don't see a full description where you expect it, search hello page for hello element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="d6704-125">Общие типы атрибутов</span><span class="sxs-lookup"><span data-stu-id="d6704-125">Common Attribute Types</span></span>  
 <span data-ttu-id="d6704-126">Атрибут **scheduledTransferPeriod** присутствует в нескольких элементах.</span><span class="sxs-lookup"><span data-stu-id="d6704-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="d6704-127">Это hello интервал между запланированными передачами toostorage округлено в большую сторону toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="d6704-127">It is hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="d6704-128">значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="d6704-128">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="d6704-129">Элемент DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="d6704-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="d6704-130">*Дерево: корневой элемент — DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="d6704-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="d6704-131">Добавлен в версии 1.3.</span><span class="sxs-lookup"><span data-stu-id="d6704-131">Added in version 1.3.</span></span>  

<span data-ttu-id="d6704-132">элемент верхнего уровня Hello hello файла конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="d6704-132">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="d6704-133">**Атрибут** xmlns - hello пространство имен XML для файла конфигурации диагностики hello:</span><span class="sxs-lookup"><span data-stu-id="d6704-133">**Attribute**  xmlns - hello XML namespace for hello diagnostics configuration file is:</span></span>  
<span data-ttu-id="d6704-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration.</span><span class="sxs-lookup"><span data-stu-id="d6704-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="d6704-135">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-135">Child Elements</span></span>|<span data-ttu-id="d6704-136">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="d6704-137">**PublicConfig**</span></span>|<span data-ttu-id="d6704-138">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-138">Required.</span></span> <span data-ttu-id="d6704-139">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="d6704-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="d6704-140">**PrivateConfig**</span></span>|<span data-ttu-id="d6704-141">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-141">Optional.</span></span> <span data-ttu-id="d6704-142">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="d6704-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="d6704-143">**IsEnabled**</span></span>|<span data-ttu-id="d6704-144">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="d6704-144">Boolean.</span></span> <span data-ttu-id="d6704-145">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="d6704-146">Элемент PublicConfig</span><span class="sxs-lookup"><span data-stu-id="d6704-146">PublicConfig Element</span></span>  
 <span data-ttu-id="d6704-147">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="d6704-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="d6704-148">Описание конфигурации диагностики открытый hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-148">Describes hello public diagnostics configuration.</span></span>  

|<span data-ttu-id="d6704-149">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-149">Child Elements</span></span>|<span data-ttu-id="d6704-150">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="d6704-151">**WadCfg**</span></span>|<span data-ttu-id="d6704-152">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-152">Required.</span></span> <span data-ttu-id="d6704-153">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="d6704-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="d6704-154">**StorageAccount**</span></span>|<span data-ttu-id="d6704-155">Имя данных hello toostore учетной записи хранилища Azure hello в Hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-155">hello name of hello Azure Storage account toostore hello data in.</span></span> <span data-ttu-id="d6704-156">Может также быть указан как параметр при выполнении командлета hello AzureServiceDiagnosticsExtension набор.</span><span class="sxs-lookup"><span data-stu-id="d6704-156">May also be specified as a parameter when executing hello Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="d6704-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="d6704-157">**StorageType**</span></span>|<span data-ttu-id="d6704-158">Может быть *таблицей*, *большим двоичным объектом* или *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="d6704-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="d6704-159">Таблица — это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d6704-159">Table is default.</span></span> <span data-ttu-id="d6704-160">При выборе TableAndBlob записываются диагностические данные дважды — один раз tooeach типа.</span><span class="sxs-lookup"><span data-stu-id="d6704-160">When TableAndBlob is chosen, diagnostic data is written twice -- once tooeach type.</span></span>|  
|<span data-ttu-id="d6704-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="d6704-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="d6704-162">Hello каталог на виртуальной машине hello, где hello Monitoring Agent хранятся данные о событиях.</span><span class="sxs-lookup"><span data-stu-id="d6704-162">hello directory on hello virtual machine where hello Monitoring Agent stores event data.</span></span> <span data-ttu-id="d6704-163">Если не задано, используется каталог по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="d6704-163">If not, set, hello default directory is used:</span></span><br /><br /> <span data-ttu-id="d6704-164">для рабочей роли или веб-роли: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="d6704-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="d6704-165">для виртуальной машины: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="d6704-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="d6704-166">Ниже перечислены обязательные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="d6704-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="d6704-167">- **путь** - hello на toobe системы hello, применяемые в диагностике Azure.</span><span class="sxs-lookup"><span data-stu-id="d6704-167">- **path** - hello directory on hello system toobe used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="d6704-168">- **expandEnvironment** -управляет ли переменные среды раскрываются в имени пути hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-168">- **expandEnvironment** - Controls whether environment variables are expanded in hello path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="d6704-169">Элемент WadCFG</span><span class="sxs-lookup"><span data-stu-id="d6704-169">WadCFG Element</span></span>  
 <span data-ttu-id="d6704-170">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig, WadCFG*</span><span class="sxs-lookup"><span data-stu-id="d6704-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="d6704-171">Определяет и настраивает hello телеметрии данных toobe собраны.</span><span class="sxs-lookup"><span data-stu-id="d6704-171">Identifies and configures hello telemetry data toobe collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="d6704-172">Элемент DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="d6704-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="d6704-173">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig, WadCFG, DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="d6704-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="d6704-174">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d6704-174">Required</span></span> 

|<span data-ttu-id="d6704-175">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d6704-175">Attributes</span></span>|<span data-ttu-id="d6704-176">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="d6704-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d6704-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="d6704-178">Максимальный объем дискового пространства, который может использоваться hello Hello различные типы диагностических данных, собранные системой диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="d6704-178">hello maximum amount of local disk space that may be consumed by hello various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="d6704-179">Hello по умолчанию составляет 5120 МБ.</span><span class="sxs-lookup"><span data-stu-id="d6704-179">hello default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="d6704-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="d6704-180">**useProxyServer**</span></span> | <span data-ttu-id="d6704-181">Параметры диагностики Azure toouse hello прокси-сервера как указано в параметрах IE.</span><span class="sxs-lookup"><span data-stu-id="d6704-181">Configure Azure Diagnostics toouse hello proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="d6704-182">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-182">Child Elements</span></span>|<span data-ttu-id="d6704-183">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="d6704-184">**CrashDumps**</span></span>|<span data-ttu-id="d6704-185">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="d6704-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="d6704-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="d6704-187">Включает сбор журналов, создаваемых системой диагностикой Azure.</span><span class="sxs-lookup"><span data-stu-id="d6704-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="d6704-188">журналы инфраструктуры диагностики Hello полезны для устранения неполадок hello самой системе диагностики.</span><span class="sxs-lookup"><span data-stu-id="d6704-188">hello diagnostic infrastructure logs are useful for troubleshooting hello diagnostics system itself.</span></span> <span data-ttu-id="d6704-189">Необязательные атрибуты:</span><span class="sxs-lookup"><span data-stu-id="d6704-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="d6704-190">- **scheduledTransferLogLevelFilter** -настраивает hello минимальную степень серьезности выполняется сбор журналов hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-190">- **scheduledTransferLogLevelFilter** - Configures hello minimum severity level of hello logs collected.</span></span><br /><br /> <span data-ttu-id="d6704-191">- **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="d6704-191">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="d6704-192">значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="d6704-192">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="d6704-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="d6704-193">**Directories**</span></span>|<span data-ttu-id="d6704-194">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="d6704-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="d6704-195">**EtwProviders**</span></span>|<span data-ttu-id="d6704-196">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="d6704-197">**Метрики**</span><span class="sxs-lookup"><span data-stu-id="d6704-197">**Metrics**</span></span>|<span data-ttu-id="d6704-198">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="d6704-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="d6704-199">**PerformanceCounters**</span></span>|<span data-ttu-id="d6704-200">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="d6704-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="d6704-201">**WindowsEventLog**</span></span>|<span data-ttu-id="d6704-202">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="d6704-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="d6704-203">**DockerSources**</span></span>|<span data-ttu-id="d6704-204">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="d6704-205">Элемент CrashDumps</span><span class="sxs-lookup"><span data-stu-id="d6704-205">CrashDumps Element</span></span>  
 <span data-ttu-id="d6704-206">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="d6704-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="d6704-207">Включите сбор аварийных дампов hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-207">Enable hello collection of crash dumps.</span></span>  

|<span data-ttu-id="d6704-208">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d6704-208">Attributes</span></span>|<span data-ttu-id="d6704-209">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="d6704-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="d6704-210">**containerName**</span></span>|<span data-ttu-id="d6704-211">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-211">Optional.</span></span> <span data-ttu-id="d6704-212">Имя Hello hello контейнера BLOB-объектов в вашей toobe учетной записи хранилища Azure используется toostore аварийных дампов.</span><span class="sxs-lookup"><span data-stu-id="d6704-212">hello name of hello blob container in your Azure Storage account toobe used toostore crash dumps.</span></span>|  
|<span data-ttu-id="d6704-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="d6704-213">**crashDumpType**</span></span>|<span data-ttu-id="d6704-214">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-214">Optional.</span></span>  <span data-ttu-id="d6704-215">Настройка системы диагностики Azure toocollect мини- или полный аварийных дампов.</span><span class="sxs-lookup"><span data-stu-id="d6704-215">Configures Azure Diagnostics toocollect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="d6704-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="d6704-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="d6704-217">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-217">Optional.</span></span>  <span data-ttu-id="d6704-218">Настраивает процент hello **overallQuotaInMB** toobe, зарезервированный для аварийные дампы на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d6704-218">Configures hello percentage of **overallQuotaInMB** toobe reserved for crash dumps on hello VM.</span></span>|  

|<span data-ttu-id="d6704-219">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-219">Child Elements</span></span>|<span data-ttu-id="d6704-220">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="d6704-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="d6704-222">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-222">Required.</span></span> <span data-ttu-id="d6704-223">Определяет значения конфигурации для каждого процесса.</span><span class="sxs-lookup"><span data-stu-id="d6704-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="d6704-224">требуется также Hello следующий атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-224">hello following attribute is also required:</span></span><br /><br /> <span data-ttu-id="d6704-225">**processName** - hello имя требуется toocollect диагностики Azure аварийного дампа для процесса hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-225">**processName** - hello name of hello process you want Azure Diagnostics toocollect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="d6704-226">Элемент Directories</span><span class="sxs-lookup"><span data-stu-id="d6704-226">Directories Element</span></span> 
 <span data-ttu-id="d6704-227">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories*</span><span class="sxs-lookup"><span data-stu-id="d6704-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="d6704-228">Включает Здравствуйте коллекцию hello содержимого каталога, IIS не удалось выполнить запрос журналы событий и журналы IIS.</span><span class="sxs-lookup"><span data-stu-id="d6704-228">Enables hello collection of hello contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="d6704-229">Необязательный атрибут **scheduledTransferPeriod**.</span><span class="sxs-lookup"><span data-stu-id="d6704-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="d6704-230">Ознакомьтесь с описанием выше.</span><span class="sxs-lookup"><span data-stu-id="d6704-230">See explanation earlier.</span></span>  

|<span data-ttu-id="d6704-231">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-231">Child Elements</span></span>|<span data-ttu-id="d6704-232">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="d6704-233">**IISLogs**</span></span>|<span data-ttu-id="d6704-234">Включая этот элемент в конфигурации hello включает hello сбор журналов IIS:</span><span class="sxs-lookup"><span data-stu-id="d6704-234">Including this element in hello configuration enables hello collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="d6704-235">**Имя контейнера** -журналы IIS hello toostore используется имя hello hello контейнер больших двоичных объектов в вашей toobe учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d6704-235">**containerName** - hello name of hello blob container in your Azure Storage account toobe used toostore hello IIS logs.</span></span>|   
|<span data-ttu-id="d6704-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="d6704-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="d6704-237">Включая этот элемент в конфигурации hello включает сбор журналов обо всех невыполненных запросов tooan сайту или приложению IIS.</span><span class="sxs-lookup"><span data-stu-id="d6704-237">Including this element in hello configuration enables collection of logs about failed requests tooan IIS site or application.</span></span> <span data-ttu-id="d6704-238">Вам также необходимо включить параметры трассировки в разделе **system.WebServer** файла **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="d6704-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="d6704-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="d6704-239">**DataSources**</span></span>|<span data-ttu-id="d6704-240">Список каталогов toomonitor.</span><span class="sxs-lookup"><span data-stu-id="d6704-240">A list of directories toomonitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="d6704-241">Элемент DataSources</span><span class="sxs-lookup"><span data-stu-id="d6704-241">DataSources Element</span></span>  
 <span data-ttu-id="d6704-242">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories — DataSources*</span><span class="sxs-lookup"><span data-stu-id="d6704-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="d6704-243">Список каталогов toomonitor.</span><span class="sxs-lookup"><span data-stu-id="d6704-243">A list of directories toomonitor.</span></span>  

|<span data-ttu-id="d6704-244">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-244">Child Elements</span></span>|<span data-ttu-id="d6704-245">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="d6704-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="d6704-247">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-247">Required.</span></span> <span data-ttu-id="d6704-248">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="d6704-249">**Имя контейнера** - hello имя контейнера BLOB-объектов hello в вашей учетной записи хранилища Azure, что toobe использовать файлы журнала toostore hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-249">**containerName** - hello name of hello blob container in your Azure Storage account that toobe used toostore hello log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="d6704-250">Элемент DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="d6704-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="d6704-251">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories — DataSources — DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="d6704-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="d6704-252">Может содержать либо hello **абсолютный** или **LocalResource** элемент, но не оба.</span><span class="sxs-lookup"><span data-stu-id="d6704-252">May include either hello **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="d6704-253">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-253">Child Elements</span></span>|<span data-ttu-id="d6704-254">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="d6704-255">**Absolute**</span></span>|<span data-ttu-id="d6704-256">toomonitor directory toohello Hello абсолютный путь.</span><span class="sxs-lookup"><span data-stu-id="d6704-256">hello absolute path toohello directory toomonitor.</span></span> <span data-ttu-id="d6704-257">Привет, следующие атрибуты не требуются:</span><span class="sxs-lookup"><span data-stu-id="d6704-257">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="d6704-258">- **Путь** -hello toomonitor directory toohello абсолютный путь.</span><span class="sxs-lookup"><span data-stu-id="d6704-258">- **Path** - hello absolute path toohello directory toomonitor.</span></span><br /><br /> <span data-ttu-id="d6704-259">- **expandEnvironment**: позволяет раскрыть переменные среды, указанные в пути.</span><span class="sxs-lookup"><span data-stu-id="d6704-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="d6704-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="d6704-260">**LocalResource**</span></span>|<span data-ttu-id="d6704-261">Здравствуйте, toomonitor локального ресурса tooa относительный путь.</span><span class="sxs-lookup"><span data-stu-id="d6704-261">hello path relative tooa local resource toomonitor.</span></span> <span data-ttu-id="d6704-262">Ниже перечислены обязательные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="d6704-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="d6704-263">- **Имя** -hello локального ресурса, содержащего hello directory toomonitor</span><span class="sxs-lookup"><span data-stu-id="d6704-263">- **Name** - hello local resource that contains hello directory toomonitor</span></span><br /><br /> <span data-ttu-id="d6704-264">- **relativePath** -hello tooName относительный путь, содержащий hello directory toomonitor</span><span class="sxs-lookup"><span data-stu-id="d6704-264">- **relativePath** - hello path relative tooName that contains hello directory toomonitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="d6704-265">Элемент EtwProviders</span><span class="sxs-lookup"><span data-stu-id="d6704-265">EtwProviders Element</span></span>  
 <span data-ttu-id="d6704-266">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="d6704-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="d6704-267">Настраивает сбор событий ETW (трассировка событий Windows) из поставщиков на основе EventSource и (или) манифеста ETW.</span><span class="sxs-lookup"><span data-stu-id="d6704-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="d6704-268">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-268">Child Elements</span></span>|<span data-ttu-id="d6704-269">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="d6704-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="d6704-271">Позволяет настроить сбор событий, создаваемых из [класса EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="d6704-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="d6704-272">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="d6704-273">**Поставщик** -hello имя класса событий EventSource hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-273">**provider** - hello class name of hello EventSource event.</span></span><br /><br /> <span data-ttu-id="d6704-274">Необязательные атрибуты:</span><span class="sxs-lookup"><span data-stu-id="d6704-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="d6704-275">- **scheduledTransferLogLevelFilter** -hello учетной записи хранилища tooyour уровня tootransfer Минимальная важность.</span><span class="sxs-lookup"><span data-stu-id="d6704-275">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="d6704-276">- **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="d6704-276">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="d6704-277">значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="d6704-277">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="d6704-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="d6704-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="d6704-279">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="d6704-280">**Поставщик** -hello GUID поставщика событий hello</span><span class="sxs-lookup"><span data-stu-id="d6704-280">**provider** - hello GUID of hello event provider</span></span><br /><br /> <span data-ttu-id="d6704-281">Необязательные атрибуты:</span><span class="sxs-lookup"><span data-stu-id="d6704-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="d6704-282">- **scheduledTransferLogLevelFilter** -hello учетной записи хранилища tooyour уровня tootransfer Минимальная важность.</span><span class="sxs-lookup"><span data-stu-id="d6704-282">- **scheduledTransferLogLevelFilter** - hello minimum severity level tootransfer tooyour storage account.</span></span><br /><br /> <span data-ttu-id="d6704-283">- **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="d6704-283">- **scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="d6704-284">значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="d6704-284">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="d6704-285">Элемент EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="d6704-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="d6704-286">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders — EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="d6704-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="d6704-287">Позволяет настроить сбор событий, создаваемых из [класса EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="d6704-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="d6704-288">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-288">Child Elements</span></span>|<span data-ttu-id="d6704-289">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="d6704-290">**DefaultEvents**</span></span>|<span data-ttu-id="d6704-291">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="d6704-292">**eventDestination** — hello имя события hello toostore hello таблицы в</span><span class="sxs-lookup"><span data-stu-id="d6704-292">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="d6704-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="d6704-293">**Event**</span></span>|<span data-ttu-id="d6704-294">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="d6704-295">**Идентификатор** -идентификатор hello hello события.</span><span class="sxs-lookup"><span data-stu-id="d6704-295">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="d6704-296">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="d6704-297">**eventDestination** — hello имя события hello toostore hello таблицы в</span><span class="sxs-lookup"><span data-stu-id="d6704-297">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="d6704-298">Элемент EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="d6704-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="d6704-299">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders — EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="d6704-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="d6704-300">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-300">Child Elements</span></span>|<span data-ttu-id="d6704-301">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="d6704-302">**DefaultEvents**</span></span>|<span data-ttu-id="d6704-303">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="d6704-304">**eventDestination** — hello имя события hello toostore hello таблицы в</span><span class="sxs-lookup"><span data-stu-id="d6704-304">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  
|<span data-ttu-id="d6704-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="d6704-305">**Event**</span></span>|<span data-ttu-id="d6704-306">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="d6704-307">**Идентификатор** -идентификатор hello hello события.</span><span class="sxs-lookup"><span data-stu-id="d6704-307">**id** - hello id of hello event.</span></span><br /><br /> <span data-ttu-id="d6704-308">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="d6704-309">**eventDestination** — hello имя события hello toostore hello таблицы в</span><span class="sxs-lookup"><span data-stu-id="d6704-309">**eventDestination** - hello name of hello table toostore hello events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="d6704-310">Элемент Metrics</span><span class="sxs-lookup"><span data-stu-id="d6704-310">Metrics Element</span></span>  
 <span data-ttu-id="d6704-311">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Metrics*</span><span class="sxs-lookup"><span data-stu-id="d6704-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="d6704-312">Позволяет toogenerate таблицу счетчика производительности, которая оптимизирована для быстрого запросов.</span><span class="sxs-lookup"><span data-stu-id="d6704-312">Enables you toogenerate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="d6704-313">Каждый счетчик производительности, который определен в hello **PerformanceCounters** элемент хранится в таблице показателей hello в таблице счетчиков производительности toohello сложения.</span><span class="sxs-lookup"><span data-stu-id="d6704-313">Each performance counter that is defined in hello **PerformanceCounters** element is stored in hello Metrics table in addition toohello Performance Counter table.</span></span>  

 <span data-ttu-id="d6704-314">Hello **resourceId** атрибут является обязательным.</span><span class="sxs-lookup"><span data-stu-id="d6704-314">hello **resourceId** attribute is required.</span></span>  <span data-ttu-id="d6704-315">Идентификатор ресурса Hello hello развертывании диагностики Azure для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d6704-315">hello resource ID of hello Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="d6704-316">Получить hello **resourceID** из hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6704-316">Get hello **resourceID** from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d6704-317">Выберите **Обзор** -> **Группы ресурсов** -> **<Имя\>**.</span><span class="sxs-lookup"><span data-stu-id="d6704-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="d6704-318">Нажмите кнопку hello **свойства** плитку и скопируйте значение hello из hello **идентификатор** поля.</span><span class="sxs-lookup"><span data-stu-id="d6704-318">Click hello **Properties** tile and copy hello value from hello **ID** field.</span></span>  

|<span data-ttu-id="d6704-319">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-319">Child Elements</span></span>|<span data-ttu-id="d6704-320">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="d6704-321">**MetricAggregation**</span></span>|<span data-ttu-id="d6704-322">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="d6704-323">**scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="d6704-323">**scheduledTransferPeriod** - hello interval between scheduled transfers toostorage rounded up toohello nearest minute.</span></span> <span data-ttu-id="d6704-324">значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="d6704-324">hello value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="d6704-325">Элемент PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="d6704-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="d6704-326">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="d6704-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="d6704-327">Включает сбор hello счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="d6704-327">Enables hello collection of performance counters.</span></span>  

 <span data-ttu-id="d6704-328">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-328">Optional attribute:</span></span>  

 <span data-ttu-id="d6704-329">Необязательный атрибут **scheduledTransferPeriod**.</span><span class="sxs-lookup"><span data-stu-id="d6704-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="d6704-330">Ознакомьтесь с описанием выше.</span><span class="sxs-lookup"><span data-stu-id="d6704-330">See explanation earlier.</span></span>

|<span data-ttu-id="d6704-331">Дочерний элемент</span><span class="sxs-lookup"><span data-stu-id="d6704-331">Child Element</span></span>|<span data-ttu-id="d6704-332">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="d6704-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="d6704-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="d6704-334">Привет, следующие атрибуты не требуются:</span><span class="sxs-lookup"><span data-stu-id="d6704-334">hello following attributes are required:</span></span><br /><br /> <span data-ttu-id="d6704-335">- **counterSpecifier** — hello имя счетчика производительности "hello".</span><span class="sxs-lookup"><span data-stu-id="d6704-335">- **counterSpecifier** - hello name of hello performance counter.</span></span> <span data-ttu-id="d6704-336">Например, `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="d6704-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="d6704-337">tooget список производительности счетчиков на узле, выполните команду hello `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="d6704-337">tooget a list of performance counters on your host, run hello command `typeperf`.</span></span><br /><br /> <span data-ttu-id="d6704-338">- **SampleRate содержит** -как часто hello счетчиков должны быть считаны.</span><span class="sxs-lookup"><span data-stu-id="d6704-338">- **sampleRate** - How often hello counter should be sampled.</span></span><br /><br /> <span data-ttu-id="d6704-339">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="d6704-340">**Единица** -единица измерения счетчиков hello hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-340">**unit** - hello unit of measure of hello counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="d6704-341">Элемент WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="d6704-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="d6704-342">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="d6704-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="d6704-343">Включает сбор hello журналов событий Windows.</span><span class="sxs-lookup"><span data-stu-id="d6704-343">Enables hello collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="d6704-344">Необязательный атрибут **scheduledTransferPeriod**.</span><span class="sxs-lookup"><span data-stu-id="d6704-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="d6704-345">Ознакомьтесь с описанием выше.</span><span class="sxs-lookup"><span data-stu-id="d6704-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="d6704-346">Дочерний элемент</span><span class="sxs-lookup"><span data-stu-id="d6704-346">Child Element</span></span>|<span data-ttu-id="d6704-347">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="d6704-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="d6704-348">**DataSource**</span></span>|<span data-ttu-id="d6704-349">toocollect журналы событий Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-349">hello Windows Event logs toocollect.</span></span> <span data-ttu-id="d6704-350">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="d6704-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="d6704-351">**имя** -собранные hello запрос XPath, описывающий toobe событий windows hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-351">**name** - hello XPath query describing hello windows events toobe collected.</span></span> <span data-ttu-id="d6704-352">Например:</span><span class="sxs-lookup"><span data-stu-id="d6704-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="d6704-353">Укажите все события toocollect «*»</span><span class="sxs-lookup"><span data-stu-id="d6704-353">toocollect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="d6704-354">Элемент Logs</span><span class="sxs-lookup"><span data-stu-id="d6704-354">Logs Element</span></span>  
 <span data-ttu-id="d6704-355">*Дерево:корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Logs*</span><span class="sxs-lookup"><span data-stu-id="d6704-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="d6704-356">Используется в версиях 1.0 и 1.1.</span><span class="sxs-lookup"><span data-stu-id="d6704-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="d6704-357">Отсутствует в версии 1.2.</span><span class="sxs-lookup"><span data-stu-id="d6704-357">Missing in 1.2.</span></span> <span data-ttu-id="d6704-358">Снова добавлен в версии 1.3.</span><span class="sxs-lookup"><span data-stu-id="d6704-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="d6704-359">Определяет конфигурацию буфера hello для базовых журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="d6704-359">Defines hello buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="d6704-360">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d6704-360">Attribute</span></span>|<span data-ttu-id="d6704-361">Тип</span><span class="sxs-lookup"><span data-stu-id="d6704-361">Type</span></span>|<span data-ttu-id="d6704-362">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d6704-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d6704-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="d6704-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="d6704-364">**unsignedInt**</span></span>|<span data-ttu-id="d6704-365">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-365">Optional.</span></span> <span data-ttu-id="d6704-366">Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.</span><span class="sxs-lookup"><span data-stu-id="d6704-366">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="d6704-367">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="d6704-367">hello default is 0.</span></span>|  
|<span data-ttu-id="d6704-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="d6704-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="d6704-369">**string**</span><span class="sxs-lookup"><span data-stu-id="d6704-369">**string**</span></span>|<span data-ttu-id="d6704-370">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-370">Optional.</span></span> <span data-ttu-id="d6704-371">Указывает hello минимальную степень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="d6704-371">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="d6704-372">значение по умолчанию Hello — **Undefined**, который передает все журналы.</span><span class="sxs-lookup"><span data-stu-id="d6704-372">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="d6704-373">Другие возможные значения (в порядке наиболее сведения tooleast) **Verbose**, **сведения**, **предупреждение**, **ошибка**и **Критические**.</span><span class="sxs-lookup"><span data-stu-id="d6704-373">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="d6704-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="d6704-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="d6704-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="d6704-375">**duration**</span></span>|<span data-ttu-id="d6704-376">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-376">Optional.</span></span> <span data-ttu-id="d6704-377">Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="d6704-377">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="d6704-378">по умолчанию Hello — PT0S.</span><span class="sxs-lookup"><span data-stu-id="d6704-378">hello default is PT0S.</span></span>|  
|<span data-ttu-id="d6704-379">**sinks** (добавлен в версии 1.5)</span><span class="sxs-lookup"><span data-stu-id="d6704-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="d6704-380">**string**</span><span class="sxs-lookup"><span data-stu-id="d6704-380">**string**</span></span>|<span data-ttu-id="d6704-381">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="d6704-381">Optional.</span></span> <span data-ttu-id="d6704-382">Приемник расположение точки tooa tooalso отправлять диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="d6704-382">Points tooa sink location tooalso send diagnostic data.</span></span> <span data-ttu-id="d6704-383">Например, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d6704-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="d6704-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="d6704-384">DockerSources</span></span>
 <span data-ttu-id="d6704-385">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — DockerSources*</span><span class="sxs-lookup"><span data-stu-id="d6704-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="d6704-386">Добавлен в версии 1.9.</span><span class="sxs-lookup"><span data-stu-id="d6704-386">Added in 1.9.</span></span>

|<span data-ttu-id="d6704-387">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d6704-387">Element Name</span></span>|<span data-ttu-id="d6704-388">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="d6704-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="d6704-389">**Stats**</span></span>|<span data-ttu-id="d6704-390">Сообщает системе hello toocollect статистики для контейнеров Docker</span><span class="sxs-lookup"><span data-stu-id="d6704-390">Tells hello system toocollect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="d6704-391">Элемент SinksConfig</span><span class="sxs-lookup"><span data-stu-id="d6704-391">SinksConfig Element</span></span>  
 <span data-ttu-id="d6704-392">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="d6704-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="d6704-393">Список расположений toosend данных tooand hello конфигурация диагностики связанных с этим местам.</span><span class="sxs-lookup"><span data-stu-id="d6704-393">A list of locations toosend diagnostics data tooand hello configuration associated with those locations.</span></span>  

|<span data-ttu-id="d6704-394">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="d6704-394">Element Name</span></span>|<span data-ttu-id="d6704-395">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="d6704-396">**Приемник**</span><span class="sxs-lookup"><span data-stu-id="d6704-396">**Sink**</span></span>|<span data-ttu-id="d6704-397">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="d6704-398">Элемент Sink</span><span class="sxs-lookup"><span data-stu-id="d6704-398">Sink Element</span></span>
 <span data-ttu-id="d6704-399">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink*</span><span class="sxs-lookup"><span data-stu-id="d6704-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="d6704-400">Добавлен в версии 1.5.</span><span class="sxs-lookup"><span data-stu-id="d6704-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="d6704-401">Определяет расположение toosend диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="d6704-401">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="d6704-402">Например hello служба Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d6704-402">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="d6704-403">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d6704-403">Attribute</span></span>|<span data-ttu-id="d6704-404">Тип</span><span class="sxs-lookup"><span data-stu-id="d6704-404">Type</span></span>|<span data-ttu-id="d6704-405">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d6704-406">**name**</span><span class="sxs-lookup"><span data-stu-id="d6704-406">**name**</span></span>|<span data-ttu-id="d6704-407">string</span><span class="sxs-lookup"><span data-stu-id="d6704-407">string</span></span>|<span data-ttu-id="d6704-408">Строка идентификации hello sinkname.</span><span class="sxs-lookup"><span data-stu-id="d6704-408">A string identifying hello sinkname.</span></span>|  

|<span data-ttu-id="d6704-409">Элемент</span><span class="sxs-lookup"><span data-stu-id="d6704-409">Element</span></span>|<span data-ttu-id="d6704-410">Тип</span><span class="sxs-lookup"><span data-stu-id="d6704-410">Type</span></span>|<span data-ttu-id="d6704-411">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="d6704-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="d6704-412">**Application Insights**</span></span>|<span data-ttu-id="d6704-413">string</span><span class="sxs-lookup"><span data-stu-id="d6704-413">string</span></span>|<span data-ttu-id="d6704-414">Используется только при отправке данных tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="d6704-414">Used only when sending data tooApplication Insights.</span></span> <span data-ttu-id="d6704-415">Содержать hello ключ инструментирования для активной, у вас есть доступ к учетной записи Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d6704-415">Contain hello Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="d6704-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="d6704-416">**Channels**</span></span>|<span data-ttu-id="d6704-417">строка</span><span class="sxs-lookup"><span data-stu-id="d6704-417">string</span></span>|<span data-ttu-id="d6704-418">Указывается для каждой дополнительной фильтрации, используемой при потоковой передаче.</span><span class="sxs-lookup"><span data-stu-id="d6704-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="d6704-419">Элемент Channels</span><span class="sxs-lookup"><span data-stu-id="d6704-419">Channels Element</span></span>  
 <span data-ttu-id="d6704-420">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink — Channels*</span><span class="sxs-lookup"><span data-stu-id="d6704-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="d6704-421">Добавлен в версии 1.5.</span><span class="sxs-lookup"><span data-stu-id="d6704-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="d6704-422">Определяет фильтры для потоков данных журнала, проходящих через приемник.</span><span class="sxs-lookup"><span data-stu-id="d6704-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="d6704-423">Элемент</span><span class="sxs-lookup"><span data-stu-id="d6704-423">Element</span></span>|<span data-ttu-id="d6704-424">Тип</span><span class="sxs-lookup"><span data-stu-id="d6704-424">Type</span></span>|<span data-ttu-id="d6704-425">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="d6704-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="d6704-426">**Channel**</span></span>|<span data-ttu-id="d6704-427">строка</span><span class="sxs-lookup"><span data-stu-id="d6704-427">string</span></span>|<span data-ttu-id="d6704-428">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6704-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="d6704-429">Элемент Channel</span><span class="sxs-lookup"><span data-stu-id="d6704-429">Channel Element</span></span>
 <span data-ttu-id="d6704-430">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink — Channels — Channel*</span><span class="sxs-lookup"><span data-stu-id="d6704-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="d6704-431">Добавлен в версии 1.5.</span><span class="sxs-lookup"><span data-stu-id="d6704-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="d6704-432">Определяет расположение toosend диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="d6704-432">Defines locations toosend diagnostic data to.</span></span> <span data-ttu-id="d6704-433">Например hello служба Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d6704-433">For example, hello Application Insights service.</span></span>  

|<span data-ttu-id="d6704-434">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d6704-434">Attributes</span></span>|<span data-ttu-id="d6704-435">Тип</span><span class="sxs-lookup"><span data-stu-id="d6704-435">Type</span></span>|<span data-ttu-id="d6704-436">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="d6704-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="d6704-437">**logLevel**</span></span>|<span data-ttu-id="d6704-438">**string**</span><span class="sxs-lookup"><span data-stu-id="d6704-438">**string**</span></span>|<span data-ttu-id="d6704-439">Указывает hello минимальную степень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="d6704-439">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="d6704-440">значение по умолчанию Hello — **Undefined**, который передает все журналы.</span><span class="sxs-lookup"><span data-stu-id="d6704-440">hello default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="d6704-441">Другие возможные значения (в порядке наиболее сведения tooleast) **Verbose**, **сведения**, **предупреждение**, **ошибка**и **Критические**.</span><span class="sxs-lookup"><span data-stu-id="d6704-441">Other possible values (in order of most tooleast information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="d6704-442">**name**</span><span class="sxs-lookup"><span data-stu-id="d6704-442">**name**</span></span>|<span data-ttu-id="d6704-443">**string**</span><span class="sxs-lookup"><span data-stu-id="d6704-443">**string**</span></span>|<span data-ttu-id="d6704-444">Уникальное имя toorefer hello канала для</span><span class="sxs-lookup"><span data-stu-id="d6704-444">A unique name of hello channel toorefer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="d6704-445">Элемент PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="d6704-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="d6704-446">*Дерево: корневой элемент — DiagnosticsConfiguration — PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="d6704-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="d6704-447">Добавлен в версии 1.3.</span><span class="sxs-lookup"><span data-stu-id="d6704-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="d6704-448">Необязательно</span><span class="sxs-lookup"><span data-stu-id="d6704-448">Optional</span></span>  

 <span data-ttu-id="d6704-449">Хранит hello закрытые сведения учетной записи хранения hello (имя, ключ и конечной точки).</span><span class="sxs-lookup"><span data-stu-id="d6704-449">Stores hello private details of hello storage account (name, key, and endpoint).</span></span> <span data-ttu-id="d6704-450">Эта информация отправляется toohello виртуальной машины, но не удается получить из него.</span><span class="sxs-lookup"><span data-stu-id="d6704-450">This information is sent toohello virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="d6704-451">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="d6704-451">Child Elements</span></span>|<span data-ttu-id="d6704-452">Описание</span><span class="sxs-lookup"><span data-stu-id="d6704-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="d6704-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="d6704-453">**StorageAccount**</span></span>|<span data-ttu-id="d6704-454">toouse учетной записи хранилища Hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-454">hello storage account toouse.</span></span> <span data-ttu-id="d6704-455">требуются следующие атрибуты Hello</span><span class="sxs-lookup"><span data-stu-id="d6704-455">hello following attributes are required</span></span><br /><br /> <span data-ttu-id="d6704-456">- **имя** - hello имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="d6704-456">- **name** - hello name of hello storage account.</span></span><br /><br /> <span data-ttu-id="d6704-457">- **ключ** - hello ключа toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d6704-457">- **key** - hello key toohello storage account.</span></span><br /><br /> <span data-ttu-id="d6704-458">- **Конечная точка** -конечная точка tooaccess hello hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="d6704-458">- **endpoint** - hello endpoint tooaccess hello storage account.</span></span> <br /><br /> <span data-ttu-id="d6704-459">-**sasToken** (добавлена 1.8.1)-, можно указать маркер SAS, а не ключа учетной записи хранения в частной конфигурации hello. Если указано, ключ учетной записи хранения hello учитывается.</span><span class="sxs-lookup"><span data-stu-id="d6704-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in hello private config. If provided, hello storage account key is ignored.</span></span> <br /><span data-ttu-id="d6704-460">Требования для маркера SAS hello:</span><span class="sxs-lookup"><span data-stu-id="d6704-460">Requirements for hello SAS Token:</span></span> <br /><span data-ttu-id="d6704-461">Поддерживает только маркер SAS учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d6704-461">- Supports account SAS token only</span></span> <br /><span data-ttu-id="d6704-462">Требуемые типы служб: - *b*, *t*.</span><span class="sxs-lookup"><span data-stu-id="d6704-462">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="d6704-463">Требуемые разрешения: - *a*, *c*, *u*, *w*.</span><span class="sxs-lookup"><span data-stu-id="d6704-463">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="d6704-464">Требуемые типы ресурсов: - *c*, *o*.</span><span class="sxs-lookup"><span data-stu-id="d6704-464">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="d6704-465">-Поддерживает только протокол HTTPS hello</span><span class="sxs-lookup"><span data-stu-id="d6704-465">- Supports hello HTTPS protocol only</span></span> <br /> <span data-ttu-id="d6704-466">Время начала и окончания срока действия должно быть допустимым.</span><span class="sxs-lookup"><span data-stu-id="d6704-466">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="d6704-467">Элемент IsEnabled</span><span class="sxs-lookup"><span data-stu-id="d6704-467">IsEnabled Element</span></span>  
 <span data-ttu-id="d6704-468">*Дерево: корневой элемент — DiagnosticsConfiguration — IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="d6704-468">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="d6704-469">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="d6704-469">Boolean.</span></span> <span data-ttu-id="d6704-470">Используйте `true` tooenable hello диагностики или `false` toodisable hello диагностики.</span><span class="sxs-lookup"><span data-stu-id="d6704-470">Use `true` tooenable hello diagnostics or `false` toodisable hello diagnostics.</span></span>
