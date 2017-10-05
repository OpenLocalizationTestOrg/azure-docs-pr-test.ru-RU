---
title: "Схема конфигурации расширения системы диагностики Azure версии 1.3 и более поздней версии | Документация Майкрософт"
description: "Схема версии 1.3 и более поздние версии для системы диагностики Azure поставляются в составе пакета SDK 2.4 и более поздней версии для Microsoft Azure."
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
ms.openlocfilehash: 0d814825fb08452238a254ccd30bde230380c74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a><span data-ttu-id="e48fd-103">Схема конфигурации системы диагностики Azure версии 1.3 и более поздней</span><span class="sxs-lookup"><span data-stu-id="e48fd-103">Azure Diagnostics 1.3 and later configuration schema</span></span>
> [!NOTE]
> <span data-ttu-id="e48fd-104">Расширение системы диагностики Azure — это компонент, который используется для сбора данных счетчиков производительности и других статистических данных из:</span><span class="sxs-lookup"><span data-stu-id="e48fd-104">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="e48fd-105">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="e48fd-105">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="e48fd-106">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e48fd-106">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="e48fd-107">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e48fd-107">Service Fabric</span></span> 
> - <span data-ttu-id="e48fd-108">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="e48fd-108">Cloud Services</span></span> 
> - <span data-ttu-id="e48fd-109">группы сетевой безопасности;</span><span class="sxs-lookup"><span data-stu-id="e48fd-109">Network Security Groups</span></span>
> 
> <span data-ttu-id="e48fd-110">Данная страница применяется только в том случае, если вы используете одну из этих служб.</span><span class="sxs-lookup"><span data-stu-id="e48fd-110">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="e48fd-111">Эта страница предназначена для версий 1.3 и более поздних (пакет Azure SDK 2.4 и более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="e48fd-111">This page is valid for versions 1.3 and newer (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="e48fd-112">Новые разделы конфигурации снабжены комментариями, указывающими, в какой версии они были добавлены.</span><span class="sxs-lookup"><span data-stu-id="e48fd-112">Newer configuration sections are commented to show in what version they were added.</span></span>  

<span data-ttu-id="e48fd-113">Файл конфигурации, описанный здесь, используется для задания параметров конфигурации диагностики при запуске монитора диагностики.</span><span class="sxs-lookup"><span data-stu-id="e48fd-113">The configuration file described here is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="e48fd-114">Расширение используется в сочетании с другими продуктами диагностики корпорации Майкрософт, такими как Azure Monitor, Application Insights и Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e48fd-114">The extension is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>



<span data-ttu-id="e48fd-115">Скачайте общедоступное определение схемы файла конфигурации, выполнив следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e48fd-115">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

<span data-ttu-id="e48fd-116">Дополнительные сведения об использовании системы диагностики Azure см. в [этой статье](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="e48fd-116">For more information about using Azure Diagnostics, see [Azure Diagnostics Extension](azure-diagnostics.md).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="e48fd-117">Пример файла конфигурации диагностики</span><span class="sxs-lookup"><span data-stu-id="e48fd-117">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="e48fd-118">В следующем примере показан типичный файл конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="e48fd-118">The following example shows a typical diagnostics configuration file:</span></span>  

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

<span data-ttu-id="e48fd-119">Ниже приведен эквивалент предыдущего XML-файла конфигурации в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e48fd-119">JSON equivalent of the previous XML configuration file.</span></span> 

<span data-ttu-id="e48fd-120">Элементы PublicConfig и PrivateConfig разделяются, так как в большинстве примеров использования JSON они передаются как различные переменные.</span><span class="sxs-lookup"><span data-stu-id="e48fd-120">The PublicConfig and PrivateConfig are separated because in most json usage cases, they are passed as different variables.</span></span> <span data-ttu-id="e48fd-121">К таким примерам относятся шаблоны Resource Manager, масштабируемый набор виртуальных машин PowerShell и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e48fd-121">These cases include Resource Manager templates, Virtual Machine Scale set PowerShell, and Visual Studio.</span></span> 

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

## <a name="reading-this-page"></a><span data-ttu-id="e48fd-122">Чтение этой страницы</span><span class="sxs-lookup"><span data-stu-id="e48fd-122">Reading this page</span></span>  
 <span data-ttu-id="e48fd-123">Приведенные ниже теги указаны примерно в том же порядке, что и в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="e48fd-123">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="e48fd-124">Если вы не видите полное описание там, где оно предполагается, найдите соответствующий элемент или атрибут на странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-124">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="e48fd-125">Общие типы атрибутов</span><span class="sxs-lookup"><span data-stu-id="e48fd-125">Common Attribute Types</span></span>  
 <span data-ttu-id="e48fd-126">Атрибут **scheduledTransferPeriod** присутствует в нескольких элементах.</span><span class="sxs-lookup"><span data-stu-id="e48fd-126">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="e48fd-127">Это интервал между запланированными передачами в службу хранилища, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-127">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="e48fd-128">Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="e48fd-128">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>


## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="e48fd-129">Элемент DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="e48fd-129">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="e48fd-130">*Дерево: корневой элемент — DiagnosticsConfiguration*</span><span class="sxs-lookup"><span data-stu-id="e48fd-130">*Tree: Root - DiagnosticsConfiguration*</span></span>

<span data-ttu-id="e48fd-131">Добавлен в версии 1.3.</span><span class="sxs-lookup"><span data-stu-id="e48fd-131">Added in version 1.3.</span></span>  

<span data-ttu-id="e48fd-132">Элемент верхнего уровня в файле конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="e48fd-132">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="e48fd-133">**Атрибут**: xmlns. Пространство имен XML для файла конфигурации диагностики:</span><span class="sxs-lookup"><span data-stu-id="e48fd-133">**Attribute**  xmlns - The XML namespace for the diagnostics configuration file is:</span></span>  
<span data-ttu-id="e48fd-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration.</span><span class="sxs-lookup"><span data-stu-id="e48fd-134">http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration</span></span>  


|<span data-ttu-id="e48fd-135">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-135">Child Elements</span></span>|<span data-ttu-id="e48fd-136">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-136">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-137">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="e48fd-137">**PublicConfig**</span></span>|<span data-ttu-id="e48fd-138">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-138">Required.</span></span> <span data-ttu-id="e48fd-139">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-139">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="e48fd-140">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="e48fd-140">**PrivateConfig**</span></span>|<span data-ttu-id="e48fd-141">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-141">Optional.</span></span> <span data-ttu-id="e48fd-142">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-142">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="e48fd-143">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="e48fd-143">**IsEnabled**</span></span>|<span data-ttu-id="e48fd-144">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="e48fd-144">Boolean.</span></span> <span data-ttu-id="e48fd-145">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-145">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="e48fd-146">Элемент PublicConfig</span><span class="sxs-lookup"><span data-stu-id="e48fd-146">PublicConfig Element</span></span>  
 <span data-ttu-id="e48fd-147">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig*</span><span class="sxs-lookup"><span data-stu-id="e48fd-147">*Tree: Root - DiagnosticsConfiguration - PublicConfig*</span></span>

 <span data-ttu-id="e48fd-148">Описывает общедоступную конфигурацию диагностики.</span><span class="sxs-lookup"><span data-stu-id="e48fd-148">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="e48fd-149">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-149">Child Elements</span></span>|<span data-ttu-id="e48fd-150">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-150">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-151">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="e48fd-151">**WadCfg**</span></span>|<span data-ttu-id="e48fd-152">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-152">Required.</span></span> <span data-ttu-id="e48fd-153">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-153">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="e48fd-154">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="e48fd-154">**StorageAccount**</span></span>|<span data-ttu-id="e48fd-155">Имя учетной записи хранения Azure для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="e48fd-155">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="e48fd-156">Может также быть указан как параметр при выполнении командлета Set-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="e48fd-156">May also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="e48fd-157">**StorageType**</span><span class="sxs-lookup"><span data-stu-id="e48fd-157">**StorageType**</span></span>|<span data-ttu-id="e48fd-158">Может быть *таблицей*, *большим двоичным объектом* или *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="e48fd-158">Can be *Table*, *Blob*, or *TableAndBlob*.</span></span> <span data-ttu-id="e48fd-159">Таблица — это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e48fd-159">Table is default.</span></span> <span data-ttu-id="e48fd-160">При выборе TableAndBlob диагностические данные записываются дважды (по одному разу на каждый тип).</span><span class="sxs-lookup"><span data-stu-id="e48fd-160">When TableAndBlob is chosen, diagnostic data is written twice -- once to each type.</span></span>|  
|<span data-ttu-id="e48fd-161">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="e48fd-161">**LocalResourceDirectory**</span></span>|<span data-ttu-id="e48fd-162">Каталог на виртуальной машине, в котором Monitoring Agent хранит данные событий.</span><span class="sxs-lookup"><span data-stu-id="e48fd-162">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="e48fd-163">Если этот параметр не задан, используется каталог по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="e48fd-163">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="e48fd-164">для рабочей роли или веб-роли: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="e48fd-164">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="e48fd-165">для виртуальной машины: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="e48fd-165">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="e48fd-166">Ниже перечислены обязательные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-166">Required attributes are:</span></span><br /><br /> <span data-ttu-id="e48fd-167">- **path**: каталог в системе для использования системой диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="e48fd-167">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="e48fd-168">- **expandEnvironment**: позволяет раскрыть переменные среды в пути.</span><span class="sxs-lookup"><span data-stu-id="e48fd-168">- **expandEnvironment** - Controls whether environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="e48fd-169">Элемент WadCFG</span><span class="sxs-lookup"><span data-stu-id="e48fd-169">WadCFG Element</span></span>  
 <span data-ttu-id="e48fd-170">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig, WadCFG*</span><span class="sxs-lookup"><span data-stu-id="e48fd-170">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG*</span></span>
 
 <span data-ttu-id="e48fd-171">Позволяет определить и настроить сбор данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e48fd-171">Identifies and configures the telemetry data to be collected.</span></span>  


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="e48fd-172">Элемент DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="e48fd-172">DiagnosticMonitorConfiguration Element</span></span> 
 <span data-ttu-id="e48fd-173">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig, WadCFG, DiagnosticMonitorConfiguration*</span><span class="sxs-lookup"><span data-stu-id="e48fd-173">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration*</span></span>

 <span data-ttu-id="e48fd-174">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e48fd-174">Required</span></span> 

|<span data-ttu-id="e48fd-175">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e48fd-175">Attributes</span></span>|<span data-ttu-id="e48fd-176">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-176">Description</span></span>|  
|----------------|-----------------|  
| <span data-ttu-id="e48fd-177">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="e48fd-177">**overallQuotaInMB**</span></span> | <span data-ttu-id="e48fd-178">Максимальный объем пространства на локальном жестком диске, доступный для диагностических данных различного типа, собранных системой диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="e48fd-178">The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="e48fd-179">Значение по умолчанию составляет 5120 МБ.</span><span class="sxs-lookup"><span data-stu-id="e48fd-179">The default setting is 5120 MB.</span></span><br />
|<span data-ttu-id="e48fd-180">**useProxyServer**</span><span class="sxs-lookup"><span data-stu-id="e48fd-180">**useProxyServer**</span></span> | <span data-ttu-id="e48fd-181">Позволяет настроить систему диагностики Azure для использования параметров прокси-сервера, указанных в настройках IE.</span><span class="sxs-lookup"><span data-stu-id="e48fd-181">Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  

<br /> <br />

|<span data-ttu-id="e48fd-182">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-182">Child Elements</span></span>|<span data-ttu-id="e48fd-183">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-183">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-184">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="e48fd-184">**CrashDumps**</span></span>|<span data-ttu-id="e48fd-185">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-185">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="e48fd-186">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="e48fd-186">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="e48fd-187">Включает сбор журналов, создаваемых системой диагностикой Azure.</span><span class="sxs-lookup"><span data-stu-id="e48fd-187">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="e48fd-188">Журналы инфраструктуры диагностики удобны для устранения неполадок в самой системе диагностики.</span><span class="sxs-lookup"><span data-stu-id="e48fd-188">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="e48fd-189">Необязательные атрибуты:</span><span class="sxs-lookup"><span data-stu-id="e48fd-189">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="e48fd-190">- **scheduledTransferLogLevelFilter**: задает минимальный уровень серьезности собираемых журналов.</span><span class="sxs-lookup"><span data-stu-id="e48fd-190">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="e48fd-191">- **scheduledTransferPeriod**: интервал между запланированными передачами в службу хранилища, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-191">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="e48fd-192">Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="e48fd-192">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="e48fd-193">**Directories**</span><span class="sxs-lookup"><span data-stu-id="e48fd-193">**Directories**</span></span>|<span data-ttu-id="e48fd-194">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-194">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="e48fd-195">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="e48fd-195">**EtwProviders**</span></span>|<span data-ttu-id="e48fd-196">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-196">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="e48fd-197">**Метрики**</span><span class="sxs-lookup"><span data-stu-id="e48fd-197">**Metrics**</span></span>|<span data-ttu-id="e48fd-198">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-198">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="e48fd-199">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="e48fd-199">**PerformanceCounters**</span></span>|<span data-ttu-id="e48fd-200">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-200">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="e48fd-201">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="e48fd-201">**WindowsEventLog**</span></span>|<span data-ttu-id="e48fd-202">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-202">See description elsewhere on this page.</span></span>| 
|<span data-ttu-id="e48fd-203">**DockerSources**</span><span class="sxs-lookup"><span data-stu-id="e48fd-203">**DockerSources**</span></span>|<span data-ttu-id="e48fd-204">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-204">See description elsewhere on this page.</span></span> | 



## <a name="crashdumps-element"></a><span data-ttu-id="e48fd-205">Элемент CrashDumps</span><span class="sxs-lookup"><span data-stu-id="e48fd-205">CrashDumps Element</span></span>  
 <span data-ttu-id="e48fd-206">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — CrashDumps*</span><span class="sxs-lookup"><span data-stu-id="e48fd-206">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - CrashDumps*</span></span>
 
 <span data-ttu-id="e48fd-207">Включает сбор аварийных дампов.</span><span class="sxs-lookup"><span data-stu-id="e48fd-207">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="e48fd-208">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e48fd-208">Attributes</span></span>|<span data-ttu-id="e48fd-209">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-209">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="e48fd-210">**containerName**</span><span class="sxs-lookup"><span data-stu-id="e48fd-210">**containerName**</span></span>|<span data-ttu-id="e48fd-211">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-211">Optional.</span></span> <span data-ttu-id="e48fd-212">Имя контейнера больших двоичных объектов в вашей учетной записи хранения Azure, используемого для хранения аварийных дампов.</span><span class="sxs-lookup"><span data-stu-id="e48fd-212">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="e48fd-213">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="e48fd-213">**crashDumpType**</span></span>|<span data-ttu-id="e48fd-214">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-214">Optional.</span></span>  <span data-ttu-id="e48fd-215">Позволяет настроить систему диагностики Azure для сбора мини-дампов или полных дампов.</span><span class="sxs-lookup"><span data-stu-id="e48fd-215">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="e48fd-216">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="e48fd-216">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="e48fd-217">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-217">Optional.</span></span>  <span data-ttu-id="e48fd-218">Позволяет настроить процент от значения **overallQuotaInMB**, резервируемый для аварийных дампов на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e48fd-218">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="e48fd-219">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-219">Child Elements</span></span>|<span data-ttu-id="e48fd-220">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-220">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-221">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="e48fd-221">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="e48fd-222">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-222">Required.</span></span> <span data-ttu-id="e48fd-223">Определяет значения конфигурации для каждого процесса.</span><span class="sxs-lookup"><span data-stu-id="e48fd-223">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="e48fd-224">Следующий атрибут также является обязательным:</span><span class="sxs-lookup"><span data-stu-id="e48fd-224">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="e48fd-225">**processName**: имя процесса, для которого системе диагностики Azure нужно собирать аварийные дампы.</span><span class="sxs-lookup"><span data-stu-id="e48fd-225">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="e48fd-226">Элемент Directories</span><span class="sxs-lookup"><span data-stu-id="e48fd-226">Directories Element</span></span> 
 <span data-ttu-id="e48fd-227">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories*</span><span class="sxs-lookup"><span data-stu-id="e48fd-227">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration -  Directories*</span></span>

 <span data-ttu-id="e48fd-228">Включает сбор содержимого каталога, журналов невыполненных запросов на вход IIS и (или) журналов IIS.</span><span class="sxs-lookup"><span data-stu-id="e48fd-228">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="e48fd-229">Необязательный атрибут **scheduledTransferPeriod**.</span><span class="sxs-lookup"><span data-stu-id="e48fd-229">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="e48fd-230">Ознакомьтесь с описанием выше.</span><span class="sxs-lookup"><span data-stu-id="e48fd-230">See explanation earlier.</span></span>  

|<span data-ttu-id="e48fd-231">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-231">Child Elements</span></span>|<span data-ttu-id="e48fd-232">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-232">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-233">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="e48fd-233">**IISLogs**</span></span>|<span data-ttu-id="e48fd-234">Если добавить этот элемент в конфигурацию, то будет включен сбор журналов IIS.</span><span class="sxs-lookup"><span data-stu-id="e48fd-234">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="e48fd-235">**containerName**: имя контейнера больших двоичных объектов в вашей учетной записи хранения Azure, используемого для хранения журналов IIS.</span><span class="sxs-lookup"><span data-stu-id="e48fd-235">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|   
|<span data-ttu-id="e48fd-236">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="e48fd-236">**FailedRequestLogs**</span></span>|<span data-ttu-id="e48fd-237">Если добавить этот элемент в конфигурацию, то будет включен сбор журналов о невыполненных запросах к сайту или приложению IIS.</span><span class="sxs-lookup"><span data-stu-id="e48fd-237">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="e48fd-238">Вам также необходимо включить параметры трассировки в разделе **system.WebServer** файла **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="e48fd-238">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="e48fd-239">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="e48fd-239">**DataSources**</span></span>|<span data-ttu-id="e48fd-240">Задает список отслеживаемых каталогов.</span><span class="sxs-lookup"><span data-stu-id="e48fd-240">A list of directories to monitor.</span></span>| 




## <a name="datasources-element"></a><span data-ttu-id="e48fd-241">Элемент DataSources</span><span class="sxs-lookup"><span data-stu-id="e48fd-241">DataSources Element</span></span>  
 <span data-ttu-id="e48fd-242">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories — DataSources*</span><span class="sxs-lookup"><span data-stu-id="e48fd-242">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources*</span></span>

 <span data-ttu-id="e48fd-243">Задает список отслеживаемых каталогов.</span><span class="sxs-lookup"><span data-stu-id="e48fd-243">A list of directories to monitor.</span></span>  

|<span data-ttu-id="e48fd-244">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-244">Child Elements</span></span>|<span data-ttu-id="e48fd-245">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-245">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-246">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="e48fd-246">**DirectoryConfiguration**</span></span>|<span data-ttu-id="e48fd-247">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-247">Required.</span></span> <span data-ttu-id="e48fd-248">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-248">Required attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-249">**containerName**: имя контейнера больших двоичных объектов в вашей учетной записи хранения Azure, используемого для хранения файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="e48fd-249">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  





## <a name="directoryconfiguration-element"></a><span data-ttu-id="e48fd-250">Элемент DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="e48fd-250">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="e48fd-251">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories — DataSources — DirectoryConfiguration*</span><span class="sxs-lookup"><span data-stu-id="e48fd-251">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Directories - DataSources - DirectoryConfiguration*</span></span>

 <span data-ttu-id="e48fd-252">Может содержать только один из элементов **Absolute** и **LocalResource**, но не оба.</span><span class="sxs-lookup"><span data-stu-id="e48fd-252">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="e48fd-253">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-253">Child Elements</span></span>|<span data-ttu-id="e48fd-254">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-254">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-255">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="e48fd-255">**Absolute**</span></span>|<span data-ttu-id="e48fd-256">Абсолютный путь к отслеживаемому каталогу.</span><span class="sxs-lookup"><span data-stu-id="e48fd-256">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="e48fd-257">Ниже приведены обязательные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-257">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="e48fd-258">- **Path**: абсолютный путь к отслеживаемому каталогу.</span><span class="sxs-lookup"><span data-stu-id="e48fd-258">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="e48fd-259">- **expandEnvironment**: позволяет раскрыть переменные среды, указанные в пути.</span><span class="sxs-lookup"><span data-stu-id="e48fd-259">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="e48fd-260">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="e48fd-260">**LocalResource**</span></span>|<span data-ttu-id="e48fd-261">Путь относительно отслеживаемого локального ресурса.</span><span class="sxs-lookup"><span data-stu-id="e48fd-261">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="e48fd-262">Ниже перечислены обязательные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-262">Required attributes are:</span></span><br /><br /> <span data-ttu-id="e48fd-263">- **Name**: локальный ресурс, который содержит каталог для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="e48fd-263">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="e48fd-264">- **relativePath**: путь относительно значения Name, содержащего отслеживаемый каталог.</span><span class="sxs-lookup"><span data-stu-id="e48fd-264">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  



## <a name="etwproviders-element"></a><span data-ttu-id="e48fd-265">Элемент EtwProviders</span><span class="sxs-lookup"><span data-stu-id="e48fd-265">EtwProviders Element</span></span>  
 <span data-ttu-id="e48fd-266">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders*</span><span class="sxs-lookup"><span data-stu-id="e48fd-266">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders*</span></span>

 <span data-ttu-id="e48fd-267">Настраивает сбор событий ETW (трассировка событий Windows) из поставщиков на основе EventSource и (или) манифеста ETW.</span><span class="sxs-lookup"><span data-stu-id="e48fd-267">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="e48fd-268">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-268">Child Elements</span></span>|<span data-ttu-id="e48fd-269">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-269">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-270">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="e48fd-270">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="e48fd-271">Позволяет настроить сбор событий, создаваемых из [класса EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e48fd-271">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="e48fd-272">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-272">Required attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-273">**provider**: имя класса события EventSource.</span><span class="sxs-lookup"><span data-stu-id="e48fd-273">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="e48fd-274">Необязательные атрибуты:</span><span class="sxs-lookup"><span data-stu-id="e48fd-274">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="e48fd-275">- **scheduledTransferLogLevelFilter**: минимальный уровень серьезности события для переноса в вашу учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e48fd-275">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="e48fd-276">- **scheduledTransferPeriod**: интервал между запланированными передачами в службу хранилища, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-276">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="e48fd-277">Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="e48fd-277">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="e48fd-278">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="e48fd-278">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="e48fd-279">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-280">**provider**: GUID поставщика событий.</span><span class="sxs-lookup"><span data-stu-id="e48fd-280">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="e48fd-281">Необязательные атрибуты:</span><span class="sxs-lookup"><span data-stu-id="e48fd-281">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="e48fd-282">- **scheduledTransferLogLevelFilter**: минимальный уровень серьезности события для переноса в вашу учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e48fd-282">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="e48fd-283">- **scheduledTransferPeriod**: интервал между запланированными передачами в службу хранилища, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-283">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="e48fd-284">Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="e48fd-284">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="e48fd-285">Элемент EtwEventSourceProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="e48fd-285">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="e48fd-286">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders — EtwEventSourceProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="e48fd-286">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders- EtwEventSourceProviderConfiguration*</span></span>

 <span data-ttu-id="e48fd-287">Позволяет настроить сбор событий, создаваемых из [класса EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e48fd-287">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="e48fd-288">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-288">Child Elements</span></span>|<span data-ttu-id="e48fd-289">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-289">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-290">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="e48fd-290">**DefaultEvents**</span></span>|<span data-ttu-id="e48fd-291">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-291">Optional attribute:</span></span><br/><br/> <span data-ttu-id="e48fd-292">**eventDestination**: имя таблицы для хранения событий.</span><span class="sxs-lookup"><span data-stu-id="e48fd-292">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="e48fd-293">**Event**</span><span class="sxs-lookup"><span data-stu-id="e48fd-293">**Event**</span></span>|<span data-ttu-id="e48fd-294">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-295">**id**: идентификатор события.</span><span class="sxs-lookup"><span data-stu-id="e48fd-295">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="e48fd-296">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-296">Optional attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-297">**eventDestination**: имя таблицы для хранения событий.</span><span class="sxs-lookup"><span data-stu-id="e48fd-297">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="e48fd-298">Элемент EtwManifestProviderConfiguration</span><span class="sxs-lookup"><span data-stu-id="e48fd-298">EtwManifestProviderConfiguration Element</span></span>  
 <span data-ttu-id="e48fd-299">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders — EtwManifestProviderConfiguration*</span><span class="sxs-lookup"><span data-stu-id="e48fd-299">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - EtwProviders - EtwManifestProviderConfiguration*</span></span>

|<span data-ttu-id="e48fd-300">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-300">Child Elements</span></span>|<span data-ttu-id="e48fd-301">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-301">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-302">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="e48fd-302">**DefaultEvents**</span></span>|<span data-ttu-id="e48fd-303">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-303">Optional attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-304">**eventDestination**: имя таблицы для хранения событий.</span><span class="sxs-lookup"><span data-stu-id="e48fd-304">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="e48fd-305">**Event**</span><span class="sxs-lookup"><span data-stu-id="e48fd-305">**Event**</span></span>|<span data-ttu-id="e48fd-306">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-306">Required attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-307">**id**: идентификатор события.</span><span class="sxs-lookup"><span data-stu-id="e48fd-307">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="e48fd-308">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-308">Optional attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-309">**eventDestination**: имя таблицы для хранения событий.</span><span class="sxs-lookup"><span data-stu-id="e48fd-309">**eventDestination** - The name of the table to store the events in</span></span>|  



## <a name="metrics-element"></a><span data-ttu-id="e48fd-310">Элемент Metrics</span><span class="sxs-lookup"><span data-stu-id="e48fd-310">Metrics Element</span></span>  
 <span data-ttu-id="e48fd-311">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Metrics*</span><span class="sxs-lookup"><span data-stu-id="e48fd-311">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Metrics*</span></span>

 <span data-ttu-id="e48fd-312">Позволяет создать таблицу счетчиков производительности, которая оптимизирована для быстрых запросов.</span><span class="sxs-lookup"><span data-stu-id="e48fd-312">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="e48fd-313">Каждый счетчик производительности, который определен в элементе **PerformanceCounters**, помимо таблицы счетчиков производительности хранится в таблице метрик.</span><span class="sxs-lookup"><span data-stu-id="e48fd-313">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="e48fd-314">Атрибут **ResourceId** является обязательным.</span><span class="sxs-lookup"><span data-stu-id="e48fd-314">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="e48fd-315">Это идентификатор ресурса виртуальной машины, на которую развертывается система диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="e48fd-315">The resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="e48fd-316">Значение **resourceID** можно получить на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e48fd-316">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e48fd-317">Выберите **Обзор** -> **Группы ресурсов** -> **<Имя\>**.</span><span class="sxs-lookup"><span data-stu-id="e48fd-317">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="e48fd-318">Щелкните элемент **Свойства** и скопируйте значение поля **Идентификатор**.</span><span class="sxs-lookup"><span data-stu-id="e48fd-318">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="e48fd-319">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-319">Child Elements</span></span>|<span data-ttu-id="e48fd-320">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-320">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-321">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="e48fd-321">**MetricAggregation**</span></span>|<span data-ttu-id="e48fd-322">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-322">Required attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-323">**scheduledTransferPeriod**: интервал между запланированными передачами в службу хранилища, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-323">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="e48fd-324">Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).</span><span class="sxs-lookup"><span data-stu-id="e48fd-324">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  



## <a name="performancecounters-element"></a><span data-ttu-id="e48fd-325">Элемент PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="e48fd-325">PerformanceCounters Element</span></span>  
 <span data-ttu-id="e48fd-326">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — PerformanceCounters*</span><span class="sxs-lookup"><span data-stu-id="e48fd-326">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - PerformanceCounters*</span></span>

 <span data-ttu-id="e48fd-327">Включает сбор данных счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="e48fd-327">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="e48fd-328">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-328">Optional attribute:</span></span>  

 <span data-ttu-id="e48fd-329">Необязательный атрибут **scheduledTransferPeriod**.</span><span class="sxs-lookup"><span data-stu-id="e48fd-329">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="e48fd-330">Ознакомьтесь с описанием выше.</span><span class="sxs-lookup"><span data-stu-id="e48fd-330">See explanation earlier.</span></span>

|<span data-ttu-id="e48fd-331">Дочерний элемент</span><span class="sxs-lookup"><span data-stu-id="e48fd-331">Child Element</span></span>|<span data-ttu-id="e48fd-332">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-332">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="e48fd-333">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="e48fd-333">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="e48fd-334">Ниже приведены обязательные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-334">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="e48fd-335">- **counterSpecifier** — имя счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="e48fd-335">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="e48fd-336">Например, `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="e48fd-336">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="e48fd-337">Чтобы получить список счетчиков производительности на узле, выполните команду `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="e48fd-337">To get a list of performance counters on your host, run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="e48fd-338">- **sampleRate**: частота выборки для счетчика.</span><span class="sxs-lookup"><span data-stu-id="e48fd-338">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="e48fd-339">Необязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-339">Optional attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-340">**unit**: единица измерения счетчика.</span><span class="sxs-lookup"><span data-stu-id="e48fd-340">**unit** - The unit of measure of the counter.</span></span>|  




## <a name="windowseventlog-element"></a><span data-ttu-id="e48fd-341">Элемент WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="e48fd-341">WindowsEventLog Element</span></span>
 <span data-ttu-id="e48fd-342">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — WindowsEventLog*</span><span class="sxs-lookup"><span data-stu-id="e48fd-342">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - WindowsEventLog*</span></span>
 
 <span data-ttu-id="e48fd-343">Включает сбор журналов событий Windows.</span><span class="sxs-lookup"><span data-stu-id="e48fd-343">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="e48fd-344">Необязательный атрибут **scheduledTransferPeriod**.</span><span class="sxs-lookup"><span data-stu-id="e48fd-344">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="e48fd-345">Ознакомьтесь с описанием выше.</span><span class="sxs-lookup"><span data-stu-id="e48fd-345">See explanation  earlier.</span></span>  

|<span data-ttu-id="e48fd-346">Дочерний элемент</span><span class="sxs-lookup"><span data-stu-id="e48fd-346">Child Element</span></span>|<span data-ttu-id="e48fd-347">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-347">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="e48fd-348">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="e48fd-348">**DataSource**</span></span>|<span data-ttu-id="e48fd-349">Собираемые журналы событий Windows.</span><span class="sxs-lookup"><span data-stu-id="e48fd-349">The Windows Event logs to collect.</span></span> <span data-ttu-id="e48fd-350">Обязательный атрибут:</span><span class="sxs-lookup"><span data-stu-id="e48fd-350">Required attribute:</span></span><br /><br /> <span data-ttu-id="e48fd-351">**name** — запрос XPath, описывающий собираемые события Windows.</span><span class="sxs-lookup"><span data-stu-id="e48fd-351">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="e48fd-352">Например:</span><span class="sxs-lookup"><span data-stu-id="e48fd-352">For example:</span></span><br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> <span data-ttu-id="e48fd-353">Для сбора всех событий укажите "*".</span><span class="sxs-lookup"><span data-stu-id="e48fd-353">To collect all events, specify "*"</span></span>|  




## <a name="logs-element"></a><span data-ttu-id="e48fd-354">Элемент Logs</span><span class="sxs-lookup"><span data-stu-id="e48fd-354">Logs Element</span></span>  
 <span data-ttu-id="e48fd-355">*Дерево:корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Logs*</span><span class="sxs-lookup"><span data-stu-id="e48fd-355">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - Logs*</span></span>

 <span data-ttu-id="e48fd-356">Используется в версиях 1.0 и 1.1.</span><span class="sxs-lookup"><span data-stu-id="e48fd-356">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="e48fd-357">Отсутствует в версии 1.2.</span><span class="sxs-lookup"><span data-stu-id="e48fd-357">Missing in 1.2.</span></span> <span data-ttu-id="e48fd-358">Снова добавлен в версии 1.3.</span><span class="sxs-lookup"><span data-stu-id="e48fd-358">Added back in 1.3.</span></span>  

 <span data-ttu-id="e48fd-359">Определяет конфигурацию буфера для базовых журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="e48fd-359">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="e48fd-360">Атрибут</span><span class="sxs-lookup"><span data-stu-id="e48fd-360">Attribute</span></span>|<span data-ttu-id="e48fd-361">Тип</span><span class="sxs-lookup"><span data-stu-id="e48fd-361">Type</span></span>|<span data-ttu-id="e48fd-362">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-362">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="e48fd-363">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="e48fd-363">**bufferQuotaInMB**</span></span>|<span data-ttu-id="e48fd-364">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="e48fd-364">**unsignedInt**</span></span>|<span data-ttu-id="e48fd-365">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-365">Optional.</span></span> <span data-ttu-id="e48fd-366">Указывает максимальный объем хранилища файловой системы, который доступен для указанных данных.</span><span class="sxs-lookup"><span data-stu-id="e48fd-366">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="e48fd-367">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="e48fd-367">The default is 0.</span></span>|  
|<span data-ttu-id="e48fd-368">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="e48fd-368">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="e48fd-369">**string**</span><span class="sxs-lookup"><span data-stu-id="e48fd-369">**string**</span></span>|<span data-ttu-id="e48fd-370">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-370">Optional.</span></span> <span data-ttu-id="e48fd-371">Указывает минимальный уровень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="e48fd-371">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="e48fd-372">Значение по умолчанию — **Undefined**, при котором передаются все журналы.</span><span class="sxs-lookup"><span data-stu-id="e48fd-372">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="e48fd-373">Другие возможные значения (в порядке убывания информативности): **Verbose**, **Information**, **Warning**, **Error** и **Critical**.</span><span class="sxs-lookup"><span data-stu-id="e48fd-373">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="e48fd-374">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="e48fd-374">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="e48fd-375">**duration**</span><span class="sxs-lookup"><span data-stu-id="e48fd-375">**duration**</span></span>|<span data-ttu-id="e48fd-376">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-376">Optional.</span></span> <span data-ttu-id="e48fd-377">Указывает интервал между запланированными передачами данных, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-377">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="e48fd-378">По умолчанию используется значение PT0S.</span><span class="sxs-lookup"><span data-stu-id="e48fd-378">The default is PT0S.</span></span>|  
|<span data-ttu-id="e48fd-379">**sinks** (добавлен в версии 1.5)</span><span class="sxs-lookup"><span data-stu-id="e48fd-379">**sinks** Added in 1.5</span></span>|<span data-ttu-id="e48fd-380">**string**</span><span class="sxs-lookup"><span data-stu-id="e48fd-380">**string**</span></span>|<span data-ttu-id="e48fd-381">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e48fd-381">Optional.</span></span> <span data-ttu-id="e48fd-382">Указывает расположение приемника для отправки диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="e48fd-382">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="e48fd-383">Например, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e48fd-383">For example, Application Insights.</span></span>|  

## <a name="dockersources"></a><span data-ttu-id="e48fd-384">DockerSources</span><span class="sxs-lookup"><span data-stu-id="e48fd-384">DockerSources</span></span>
 <span data-ttu-id="e48fd-385">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — DockerSources*</span><span class="sxs-lookup"><span data-stu-id="e48fd-385">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - DiagnosticMonitorConfiguration - DockerSources*</span></span>

 <span data-ttu-id="e48fd-386">Добавлен в версии 1.9.</span><span class="sxs-lookup"><span data-stu-id="e48fd-386">Added in 1.9.</span></span>

|<span data-ttu-id="e48fd-387">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="e48fd-387">Element Name</span></span>|<span data-ttu-id="e48fd-388">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-388">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="e48fd-389">**Stats**</span><span class="sxs-lookup"><span data-stu-id="e48fd-389">**Stats**</span></span>|<span data-ttu-id="e48fd-390">Указывает системе, что нужно собрать статистику для контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="e48fd-390">Tells the system to collect stats for Docker containers</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="e48fd-391">Элемент SinksConfig</span><span class="sxs-lookup"><span data-stu-id="e48fd-391">SinksConfig Element</span></span>  
 <span data-ttu-id="e48fd-392">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig*</span><span class="sxs-lookup"><span data-stu-id="e48fd-392">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig*</span></span>

 <span data-ttu-id="e48fd-393">Содержит список расположений для отправки диагностических данных и конфигурацию, связанную с этими расположениями.</span><span class="sxs-lookup"><span data-stu-id="e48fd-393">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="e48fd-394">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="e48fd-394">Element Name</span></span>|<span data-ttu-id="e48fd-395">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-395">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="e48fd-396">**Приемник**</span><span class="sxs-lookup"><span data-stu-id="e48fd-396">**Sink**</span></span>|<span data-ttu-id="e48fd-397">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-397">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="e48fd-398">Элемент Sink</span><span class="sxs-lookup"><span data-stu-id="e48fd-398">Sink Element</span></span>
 <span data-ttu-id="e48fd-399">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink*</span><span class="sxs-lookup"><span data-stu-id="e48fd-399">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink*</span></span>

 <span data-ttu-id="e48fd-400">Добавлен в версии 1.5.</span><span class="sxs-lookup"><span data-stu-id="e48fd-400">Added in version 1.5.</span></span>  

 <span data-ttu-id="e48fd-401">Определяет расположение для отправки диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="e48fd-401">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="e48fd-402">Например, это может быть служба Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e48fd-402">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="e48fd-403">Атрибут</span><span class="sxs-lookup"><span data-stu-id="e48fd-403">Attribute</span></span>|<span data-ttu-id="e48fd-404">Тип</span><span class="sxs-lookup"><span data-stu-id="e48fd-404">Type</span></span>|<span data-ttu-id="e48fd-405">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-405">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="e48fd-406">**name**</span><span class="sxs-lookup"><span data-stu-id="e48fd-406">**name**</span></span>|<span data-ttu-id="e48fd-407">строка</span><span class="sxs-lookup"><span data-stu-id="e48fd-407">string</span></span>|<span data-ttu-id="e48fd-408">Строка, определяющая имя приемника.</span><span class="sxs-lookup"><span data-stu-id="e48fd-408">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="e48fd-409">Элемент</span><span class="sxs-lookup"><span data-stu-id="e48fd-409">Element</span></span>|<span data-ttu-id="e48fd-410">Тип</span><span class="sxs-lookup"><span data-stu-id="e48fd-410">Type</span></span>|<span data-ttu-id="e48fd-411">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-411">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="e48fd-412">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="e48fd-412">**Application Insights**</span></span>|<span data-ttu-id="e48fd-413">строка</span><span class="sxs-lookup"><span data-stu-id="e48fd-413">string</span></span>|<span data-ttu-id="e48fd-414">Используется только при отправке данных в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e48fd-414">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="e48fd-415">Содержит ключ инструментирования для активной учетной записи Application Insights, к которой у вас есть доступ.</span><span class="sxs-lookup"><span data-stu-id="e48fd-415">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="e48fd-416">**Channels**</span><span class="sxs-lookup"><span data-stu-id="e48fd-416">**Channels**</span></span>|<span data-ttu-id="e48fd-417">строка</span><span class="sxs-lookup"><span data-stu-id="e48fd-417">string</span></span>|<span data-ttu-id="e48fd-418">Указывается для каждой дополнительной фильтрации, используемой при потоковой передаче.</span><span class="sxs-lookup"><span data-stu-id="e48fd-418">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="e48fd-419">Элемент Channels</span><span class="sxs-lookup"><span data-stu-id="e48fd-419">Channels Element</span></span>  
 <span data-ttu-id="e48fd-420">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink — Channels*</span><span class="sxs-lookup"><span data-stu-id="e48fd-420">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels*</span></span>

 <span data-ttu-id="e48fd-421">Добавлен в версии 1.5.</span><span class="sxs-lookup"><span data-stu-id="e48fd-421">Added in version 1.5.</span></span>  

 <span data-ttu-id="e48fd-422">Определяет фильтры для потоков данных журнала, проходящих через приемник.</span><span class="sxs-lookup"><span data-stu-id="e48fd-422">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="e48fd-423">Элемент</span><span class="sxs-lookup"><span data-stu-id="e48fd-423">Element</span></span>|<span data-ttu-id="e48fd-424">Тип</span><span class="sxs-lookup"><span data-stu-id="e48fd-424">Type</span></span>|<span data-ttu-id="e48fd-425">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-425">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="e48fd-426">**Channel**</span><span class="sxs-lookup"><span data-stu-id="e48fd-426">**Channel**</span></span>|<span data-ttu-id="e48fd-427">строка</span><span class="sxs-lookup"><span data-stu-id="e48fd-427">string</span></span>|<span data-ttu-id="e48fd-428">Ознакомьтесь с описанием в другом разделе на этой странице.</span><span class="sxs-lookup"><span data-stu-id="e48fd-428">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="e48fd-429">Элемент Channel</span><span class="sxs-lookup"><span data-stu-id="e48fd-429">Channel Element</span></span>
 <span data-ttu-id="e48fd-430">*Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink — Channels — Channel*</span><span class="sxs-lookup"><span data-stu-id="e48fd-430">*Tree: Root - DiagnosticsConfiguration - PublicConfig - WadCFG - SinksConfig - Sink - Channels - Channel*</span></span>

 <span data-ttu-id="e48fd-431">Добавлен в версии 1.5.</span><span class="sxs-lookup"><span data-stu-id="e48fd-431">Added in version 1.5.</span></span>  

 <span data-ttu-id="e48fd-432">Определяет расположение для отправки диагностических данных.</span><span class="sxs-lookup"><span data-stu-id="e48fd-432">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="e48fd-433">Например, это может быть служба Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e48fd-433">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="e48fd-434">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e48fd-434">Attributes</span></span>|<span data-ttu-id="e48fd-435">Тип</span><span class="sxs-lookup"><span data-stu-id="e48fd-435">Type</span></span>|<span data-ttu-id="e48fd-436">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-436">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="e48fd-437">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="e48fd-437">**logLevel**</span></span>|<span data-ttu-id="e48fd-438">**string**</span><span class="sxs-lookup"><span data-stu-id="e48fd-438">**string**</span></span>|<span data-ttu-id="e48fd-439">Указывает минимальный уровень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="e48fd-439">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="e48fd-440">Значение по умолчанию — **Undefined**, при котором передаются все журналы.</span><span class="sxs-lookup"><span data-stu-id="e48fd-440">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="e48fd-441">Другие возможные значения (в порядке убывания информативности): **Verbose**, **Information**, **Warning**, **Error** и **Critical**.</span><span class="sxs-lookup"><span data-stu-id="e48fd-441">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="e48fd-442">**name**</span><span class="sxs-lookup"><span data-stu-id="e48fd-442">**name**</span></span>|<span data-ttu-id="e48fd-443">**string**</span><span class="sxs-lookup"><span data-stu-id="e48fd-443">**string**</span></span>|<span data-ttu-id="e48fd-444">Уникальное имя для использования ссылки на канал.</span><span class="sxs-lookup"><span data-stu-id="e48fd-444">A unique name of the channel to refer to</span></span>|  


## <a name="privateconfig-element"></a><span data-ttu-id="e48fd-445">Элемент PrivateConfig</span><span class="sxs-lookup"><span data-stu-id="e48fd-445">PrivateConfig Element</span></span> 
 <span data-ttu-id="e48fd-446">*Дерево: корневой элемент — DiagnosticsConfiguration — PrivateConfig*</span><span class="sxs-lookup"><span data-stu-id="e48fd-446">*Tree: Root - DiagnosticsConfiguration - PrivateConfig*</span></span>

 <span data-ttu-id="e48fd-447">Добавлен в версии 1.3.</span><span class="sxs-lookup"><span data-stu-id="e48fd-447">Added in version 1.3.</span></span>  

 <span data-ttu-id="e48fd-448">Необязательно</span><span class="sxs-lookup"><span data-stu-id="e48fd-448">Optional</span></span>  

 <span data-ttu-id="e48fd-449">Хранит частные сведения об учетной записи хранения (имя, ключ и конечную точку).</span><span class="sxs-lookup"><span data-stu-id="e48fd-449">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="e48fd-450">Эта информация отправляется на виртуальную машину, но извлечь ее из виртуальной машины невозможно.</span><span class="sxs-lookup"><span data-stu-id="e48fd-450">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="e48fd-451">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="e48fd-451">Child Elements</span></span>|<span data-ttu-id="e48fd-452">Описание</span><span class="sxs-lookup"><span data-stu-id="e48fd-452">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="e48fd-453">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="e48fd-453">**StorageAccount**</span></span>|<span data-ttu-id="e48fd-454">Используемая учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e48fd-454">The storage account to use.</span></span> <span data-ttu-id="e48fd-455">Ниже приведены обязательные атрибуты.</span><span class="sxs-lookup"><span data-stu-id="e48fd-455">The following attributes are required</span></span><br /><br /> <span data-ttu-id="e48fd-456">- **name**: имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e48fd-456">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="e48fd-457">- **key**: ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e48fd-457">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="e48fd-458">- **endpoint**: конечная точка для доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e48fd-458">- **endpoint** - The endpoint to access the storage account.</span></span> <br /><br /> <span data-ttu-id="e48fd-459">-**sasToken** (добавлен в версии 1.8.1): вы можете указать маркер SAS вместо ключа учетной записи хранения в закрытой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e48fd-459">-**sasToken** (added 1.8.1)- You can specify an SAS token instead of a storage account key in the private config.</span></span> <span data-ttu-id="e48fd-460">Если он указан, ключ учетной записи хранения не учитывается.</span><span class="sxs-lookup"><span data-stu-id="e48fd-460">If provided, the storage account key is ignored.</span></span> <br /><span data-ttu-id="e48fd-461">Требования к маркеру SAS:</span><span class="sxs-lookup"><span data-stu-id="e48fd-461">Requirements for the SAS Token:</span></span> <br /><span data-ttu-id="e48fd-462">Поддерживает только маркер SAS учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e48fd-462">- Supports account SAS token only</span></span> <br /><span data-ttu-id="e48fd-463">Требуемые типы служб: - *b*, *t*.</span><span class="sxs-lookup"><span data-stu-id="e48fd-463">- *b*, *t* service types are required.</span></span> <br /> <span data-ttu-id="e48fd-464">Требуемые разрешения: - *a*, *c*, *u*, *w*.</span><span class="sxs-lookup"><span data-stu-id="e48fd-464">- *a*, *c*, *u*, *w* permissions are required.</span></span> <br /> <span data-ttu-id="e48fd-465">Требуемые типы ресурсов: - *c*, *o*.</span><span class="sxs-lookup"><span data-stu-id="e48fd-465">- *c*, *o* resource types are required.</span></span> <br /> <span data-ttu-id="e48fd-466">Поддерживает только протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e48fd-466">- Supports the HTTPS protocol only</span></span> <br /> <span data-ttu-id="e48fd-467">Время начала и окончания срока действия должно быть допустимым.</span><span class="sxs-lookup"><span data-stu-id="e48fd-467">- Start and expiry time must be valid.</span></span>|  


## <a name="isenabled-element"></a><span data-ttu-id="e48fd-468">Элемент IsEnabled</span><span class="sxs-lookup"><span data-stu-id="e48fd-468">IsEnabled Element</span></span>  
 <span data-ttu-id="e48fd-469">*Дерево: корневой элемент — DiagnosticsConfiguration — IsEnabled*</span><span class="sxs-lookup"><span data-stu-id="e48fd-469">*Tree: Root - DiagnosticsConfiguration - IsEnabled*</span></span>

 <span data-ttu-id="e48fd-470">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="e48fd-470">Boolean.</span></span> <span data-ttu-id="e48fd-471">Используйте `true`, чтобы включить диагностику, или `false`, чтобы отключить ее.</span><span class="sxs-lookup"><span data-stu-id="e48fd-471">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
