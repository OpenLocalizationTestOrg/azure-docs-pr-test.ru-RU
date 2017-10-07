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
# <a name="azure-diagnostics-13-and-later-configuration-schema"></a>Схема конфигурации системы диагностики Azure версии 1.3 и более поздней
> [!NOTE]
> Hello расширения системы диагностики Azure — компонент hello используется toocollect счетчики производительности и другие статистические данные из:
> - Виртуальные машины Azure 
> - Наборы для масштабирования виртуальных машин
> - Service Fabric 
> - Облачные службы 
> - группы сетевой безопасности;
> 
> Данная страница применяется только в том случае, если вы используете одну из этих служб.

Эта страница предназначена для версий 1.3 и более поздних (пакет Azure SDK 2.4 и более поздней версии). Новые разделы конфигурации являются комментариями tooshow в какой версии, они были добавлены.  

файл конфигурации Hello, описанные здесь — используется tooset диагностические параметры конфигурации, при запуске монитора диагностики hello.  

расширение Hello используется в сочетании с другими продуктами Майкрософт диагностики, как монитор Azure, Application Insights и анализа журналов.



Загрузите определение схемы файл открытой конфигурации hello, выполнив следующую команду PowerShell hello:  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

Дополнительные сведения об использовании системы диагностики Azure см. в [этой статье](azure-diagnostics.md).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Пример файла конфигурации диагностики hello  
 Следующий пример Hello показан типичный файл конфигурации диагностики:  

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

Эквивалент в формате JSON hello предыдущего XML-файла конфигурации. 

Поскольку в большинстве случаев использования json, они передаются как переменные разных разделяются Hello PublicConfig и PrivateConfig. К таким примерам относятся шаблоны Resource Manager, масштабируемый набор виртуальных машин PowerShell и Visual Studio. 

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

## <a name="reading-this-page"></a>Чтение этой страницы  
 Hello следующие теги располагаются примерно в порядке, показанном в предыдущих пример hello.  Если вы не видите полное описание, где ожидается, страница «поиск» hello hello элемента или атрибута.  

## <a name="common-attribute-types"></a>Общие типы атрибутов  
 Атрибут **scheduledTransferPeriod** присутствует в нескольких элементах. Это hello интервал между запланированными передачами toostorage округлено в большую сторону toohello ближайшего минуты. значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp)


## <a name="diagnosticsconfiguration-element"></a>Элемент DiagnosticsConfiguration  
 *Дерево: корневой элемент — DiagnosticsConfiguration*

Добавлен в версии 1.3.  

элемент верхнего уровня Hello hello файла конфигурации диагностики.  

**Атрибут** xmlns - hello пространство имен XML для файла конфигурации диагностики hello:  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration.  


|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**PublicConfig**|обязательный параметр. Ознакомьтесь с описанием в другом разделе на этой странице.|  
|**PrivateConfig**|необязательный параметр. Ознакомьтесь с описанием в другом разделе на этой странице.|  
|**IsEnabled**|Логическое значение. Ознакомьтесь с описанием в другом разделе на этой странице.|  

## <a name="publicconfig-element"></a>Элемент PublicConfig  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig*

 Описание конфигурации диагностики открытый hello.  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**WadCfg**|обязательный параметр. Ознакомьтесь с описанием в другом разделе на этой странице.|  
|**StorageAccount**|Имя данных hello toostore учетной записи хранилища Azure hello в Hello. Может также быть указан как параметр при выполнении командлета hello AzureServiceDiagnosticsExtension набор.|  
|**StorageType**|Может быть *таблицей*, *большим двоичным объектом* или *TableAndBlob*. Таблица — это значение по умолчанию. При выборе TableAndBlob записываются диагностические данные дважды — один раз tooeach типа.|  
|**LocalResourceDirectory**|Hello каталог на виртуальной машине hello, где hello Monitoring Agent хранятся данные о событиях. Если не задано, используется каталог по умолчанию hello:<br /><br /> для рабочей роли или веб-роли: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> для виртуальной машины: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Ниже перечислены обязательные атрибуты.<br /><br /> - **путь** - hello на toobe системы hello, применяемые в диагностике Azure.<br /><br /> - **expandEnvironment** -управляет ли переменные среды раскрываются в имени пути hello.|  

## <a name="wadcfg-element"></a>Элемент WadCFG  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig, WadCFG*
 
 Определяет и настраивает hello телеметрии данных toobe собраны.  


## <a name="diagnosticmonitorconfiguration-element"></a>Элемент DiagnosticMonitorConfiguration 
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig, WadCFG, DiagnosticMonitorConfiguration*

 Обязательно 

|Атрибуты|Описание|  
|----------------|-----------------|  
| **overallQuotaInMB** | Максимальный объем дискового пространства, который может использоваться hello Hello различные типы диагностических данных, собранные системой диагностики Azure. Hello по умолчанию составляет 5120 МБ.<br />
|**useProxyServer** | Параметры диагностики Azure toouse hello прокси-сервера как указано в параметрах IE.|  

<br /> <br />

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**CrashDumps**|Ознакомьтесь с описанием в другом разделе на этой странице.|  
|**DiagnosticInfrastructureLogs**|Включает сбор журналов, создаваемых системой диагностикой Azure. журналы инфраструктуры диагностики Hello полезны для устранения неполадок hello самой системе диагностики. Необязательные атрибуты:<br /><br /> - **scheduledTransferLogLevelFilter** -настраивает hello минимальную степень серьезности выполняется сбор журналов hello.<br /><br /> - **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Directories**|Ознакомьтесь с описанием в другом разделе на этой странице.|  
|**EtwProviders**|Ознакомьтесь с описанием в другом разделе на этой странице.|  
|**Метрики**|Ознакомьтесь с описанием в другом разделе на этой странице.|  
|**PerformanceCounters**|Ознакомьтесь с описанием в другом разделе на этой странице.|  
|**WindowsEventLog**|Ознакомьтесь с описанием в другом разделе на этой странице.| 
|**DockerSources**|Ознакомьтесь с описанием в другом разделе на этой странице. | 



## <a name="crashdumps-element"></a>Элемент CrashDumps  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — CrashDumps*
 
 Включите сбор аварийных дампов hello.  

|Атрибуты|Описание|  
|----------------|-----------------|  
|**containerName**|необязательный параметр. Имя Hello hello контейнера BLOB-объектов в вашей toobe учетной записи хранилища Azure используется toostore аварийных дампов.|  
|**crashDumpType**|необязательный параметр.  Настройка системы диагностики Azure toocollect мини- или полный аварийных дампов.|  
|**directoryQuotaPercentage**|необязательный параметр.  Настраивает процент hello **overallQuotaInMB** toobe, зарезервированный для аварийные дампы на hello виртуальной Машины.|  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|обязательный параметр. Определяет значения конфигурации для каждого процесса.<br /><br /> требуется также Hello следующий атрибут:<br /><br /> **processName** - hello имя требуется toocollect диагностики Azure аварийного дампа для процесса hello.|  

## <a name="directories-element"></a>Элемент Directories 
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories*

 Включает Здравствуйте коллекцию hello содержимого каталога, IIS не удалось выполнить запрос журналы событий и журналы IIS.  

 Необязательный атрибут **scheduledTransferPeriod**. Ознакомьтесь с описанием выше.  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**IISLogs**|Включая этот элемент в конфигурации hello включает hello сбор журналов IIS:<br /><br /> **Имя контейнера** -журналы IIS hello toostore используется имя hello hello контейнер больших двоичных объектов в вашей toobe учетной записи хранилища Azure.|   
|**FailedRequestLogs**|Включая этот элемент в конфигурации hello включает сбор журналов обо всех невыполненных запросов tooan сайту или приложению IIS. Вам также необходимо включить параметры трассировки в разделе **system.WebServer** файла **Web.config**.|  
|**DataSources**|Список каталогов toomonitor.| 




## <a name="datasources-element"></a>Элемент DataSources  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories — DataSources*

 Список каталогов toomonitor.  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|обязательный параметр. Обязательный атрибут:<br /><br /> **Имя контейнера** - hello имя контейнера BLOB-объектов hello в вашей учетной записи хранилища Azure, что toobe использовать файлы журнала toostore hello.|  





## <a name="directoryconfiguration-element"></a>Элемент DirectoryConfiguration  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Directories — DataSources — DirectoryConfiguration*

 Может содержать либо hello **абсолютный** или **LocalResource** элемент, но не оба.  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**Absolute**|toomonitor directory toohello Hello абсолютный путь. Привет, следующие атрибуты не требуются:<br /><br /> - **Путь** -hello toomonitor directory toohello абсолютный путь.<br /><br /> - **expandEnvironment**: позволяет раскрыть переменные среды, указанные в пути.|  
|**LocalResource**|Здравствуйте, toomonitor локального ресурса tooa относительный путь. Ниже перечислены обязательные атрибуты.<br /><br /> - **Имя** -hello локального ресурса, содержащего hello directory toomonitor<br /><br /> - **relativePath** -hello tooName относительный путь, содержащий hello directory toomonitor|  



## <a name="etwproviders-element"></a>Элемент EtwProviders  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders*

 Настраивает сбор событий ETW (трассировка событий Windows) из поставщиков на основе EventSource и (или) манифеста ETW.  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Позволяет настроить сбор событий, создаваемых из [класса EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Обязательный атрибут:<br /><br /> **Поставщик** -hello имя класса событий EventSource hello.<br /><br /> Необязательные атрибуты:<br /><br /> - **scheduledTransferLogLevelFilter** -hello учетной записи хранилища tooyour уровня tootransfer Минимальная важность.<br /><br /> - **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Обязательный атрибут:<br /><br /> **Поставщик** -hello GUID поставщика событий hello<br /><br /> Необязательные атрибуты:<br /><br /> - **scheduledTransferLogLevelFilter** -hello учетной записи хранилища tooyour уровня tootransfer Минимальная важность.<br /><br /> - **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="etweventsourceproviderconfiguration-element"></a>Элемент EtwEventSourceProviderConfiguration  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders — EtwEventSourceProviderConfiguration*

 Позволяет настроить сбор событий, создаваемых из [класса EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**DefaultEvents**|Необязательный атрибут:<br/><br/> **eventDestination** — hello имя события hello toostore hello таблицы в|  
|**Event**|Обязательный атрибут:<br /><br /> **Идентификатор** -идентификатор hello hello события.<br /><br /> Необязательный атрибут:<br /><br /> **eventDestination** — hello имя события hello toostore hello таблицы в|  



## <a name="etwmanifestproviderconfiguration-element"></a>Элемент EtwManifestProviderConfiguration  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — EtwProviders — EtwManifestProviderConfiguration*

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**DefaultEvents**|Необязательный атрибут:<br /><br /> **eventDestination** — hello имя события hello toostore hello таблицы в|  
|**Event**|Обязательный атрибут:<br /><br /> **Идентификатор** -идентификатор hello hello события.<br /><br /> Необязательный атрибут:<br /><br /> **eventDestination** — hello имя события hello toostore hello таблицы в|  



## <a name="metrics-element"></a>Элемент Metrics  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Metrics*

 Позволяет toogenerate таблицу счетчика производительности, которая оптимизирована для быстрого запросов. Каждый счетчик производительности, который определен в hello **PerformanceCounters** элемент хранится в таблице показателей hello в таблице счетчиков производительности toohello сложения.  

 Hello **resourceId** атрибут является обязательным.  Идентификатор ресурса Hello hello развертывании диагностики Azure для виртуальной машины. Получить hello **resourceID** из hello [портал Azure](https://portal.azure.com). Выберите **Обзор** -> **Группы ресурсов** -> **<Имя\>**. Нажмите кнопку hello **свойства** плитку и скопируйте значение hello из hello **идентификатор** поля.  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**MetricAggregation**|Обязательный атрибут:<br /><br /> **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  



## <a name="performancecounters-element"></a>Элемент PerformanceCounters  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — PerformanceCounters*

 Включает сбор hello счетчиков производительности.  

 Необязательный атрибут:  

 Необязательный атрибут **scheduledTransferPeriod**. Ознакомьтесь с описанием выше.

|Дочерний элемент|Описание|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|Привет, следующие атрибуты не требуются:<br /><br /> - **counterSpecifier** — hello имя счетчика производительности "hello". Например, `\Processor(_Total)\% Processor Time`. tooget список производительности счетчиков на узле, выполните команду hello `typeperf`.<br /><br /> - **SampleRate содержит** -как часто hello счетчиков должны быть считаны.<br /><br /> Необязательный атрибут:<br /><br /> **Единица** -единица измерения счетчиков hello hello.|  




## <a name="windowseventlog-element"></a>Элемент WindowsEventLog
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — WindowsEventLog*
 
 Включает сбор hello журналов событий Windows.  

 Необязательный атрибут **scheduledTransferPeriod**. Ознакомьтесь с описанием выше.  

|Дочерний элемент|Описание|  
|-------------------|-----------------|  
|**DataSource**|toocollect журналы событий Windows Hello. Обязательный атрибут:<br /><br /> **имя** -собранные hello запрос XPath, описывающий toobe событий windows hello. Например:<br /><br /> `Application!*[System[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level <= 3)]`<br /><br /> Укажите все события toocollect «*»|  




## <a name="logs-element"></a>Элемент Logs  
 *Дерево:корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — Logs*

 Используется в версиях 1.0 и 1.1. Отсутствует в версии 1.2. Снова добавлен в версии 1.3.  

 Определяет конфигурацию буфера hello для базовых журналов Azure.  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|необязательный параметр. Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.<br /><br /> Hello по умолчанию — 0.|  
|**scheduledTransferLogLevelFilterr**|**string**|необязательный параметр. Указывает hello минимальную степень серьезности для передаваемых записей журнала. значение по умолчанию Hello — **Undefined**, который передает все журналы. Другие возможные значения (в порядке наиболее сведения tooleast) **Verbose**, **сведения**, **предупреждение**, **ошибка**и **Критические**.|  
|**scheduledTransferPeriod**|**duration**|необязательный параметр. Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.<br /><br /> по умолчанию Hello — PT0S.|  
|**sinks** (добавлен в версии 1.5)|**string**|необязательный параметр. Приемник расположение точки tooa tooalso отправлять диагностические данные. Например, Application Insights.|  

## <a name="dockersources"></a>DockerSources
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — DiagnosticMonitorConfiguration — DockerSources*

 Добавлен в версии 1.9.

|Имя элемента|Описание|  
|------------------|-----------------|  
|**Stats**|Сообщает системе hello toocollect статистики для контейнеров Docker|  

## <a name="sinksconfig-element"></a>Элемент SinksConfig  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig*

 Список расположений toosend данных tooand hello конфигурация диагностики связанных с этим местам.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**Приемник**|Ознакомьтесь с описанием в другом разделе на этой странице.|  

## <a name="sink-element"></a>Элемент Sink
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink*

 Добавлен в версии 1.5.  

 Определяет расположение toosend диагностические данные. Например hello служба Application Insights.  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**name**|string|Строка идентификации hello sinkname.|  

|Элемент|Тип|Описание|  
|-------------|----------|-----------------|  
|**Application Insights**|string|Используется только при отправке данных tooApplication аналитики. Содержать hello ключ инструментирования для активной, у вас есть доступ к учетной записи Application Insights.|  
|**Channels**|строка|Указывается для каждой дополнительной фильтрации, используемой при потоковой передаче.|  

## <a name="channels-element"></a>Элемент Channels  
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink — Channels*

 Добавлен в версии 1.5.  

 Определяет фильтры для потоков данных журнала, проходящих через приемник.  

|Элемент|Тип|Описание|  
|-------------|----------|-----------------|  
|**Channel**|строка|Ознакомьтесь с описанием в другом разделе на этой странице.|  

## <a name="channel-element"></a>Элемент Channel
 *Дерево: корневой элемент — DiagnosticsConfiguration — PublicConfig — WadCFG — SinksConfig — Sink — Channels — Channel*

 Добавлен в версии 1.5.  

 Определяет расположение toosend диагностические данные. Например hello служба Application Insights.  

|Атрибуты|Тип|Описание|  
|----------------|----------|-----------------|  
|**logLevel**|**string**|Указывает hello минимальную степень серьезности для передаваемых записей журнала. значение по умолчанию Hello — **Undefined**, который передает все журналы. Другие возможные значения (в порядке наиболее сведения tooleast) **Verbose**, **сведения**, **предупреждение**, **ошибка**и **Критические**.|  
|**name**|**string**|Уникальное имя toorefer hello канала для|  


## <a name="privateconfig-element"></a>Элемент PrivateConfig 
 *Дерево: корневой элемент — DiagnosticsConfiguration — PrivateConfig*

 Добавлен в версии 1.3.  

 Необязательно  

 Хранит hello закрытые сведения учетной записи хранения hello (имя, ключ и конечной точки). Эта информация отправляется toohello виртуальной машины, но не удается получить из него.  

|Дочерние элементы|Описание|  
|--------------------|-----------------|  
|**StorageAccount**|toouse учетной записи хранилища Hello. требуются следующие атрибуты Hello<br /><br /> - **имя** - hello имя учетной записи хранения hello.<br /><br /> - **ключ** - hello ключа toohello учетной записи хранилища.<br /><br /> - **Конечная точка** -конечная точка tooaccess hello hello учетной записи хранилища. <br /><br /> -**sasToken** (добавлена 1.8.1)-, можно указать маркер SAS, а не ключа учетной записи хранения в частной конфигурации hello. Если указано, ключ учетной записи хранения hello учитывается. <br />Требования для маркера SAS hello: <br />Поддерживает только маркер SAS учетной записи. <br />Требуемые типы служб: - *b*, *t*. <br /> Требуемые разрешения: - *a*, *c*, *u*, *w*. <br /> Требуемые типы ресурсов: - *c*, *o*. <br /> -Поддерживает только протокол HTTPS hello <br /> Время начала и окончания срока действия должно быть допустимым.|  


## <a name="isenabled-element"></a>Элемент IsEnabled  
 *Дерево: корневой элемент — DiagnosticsConfiguration — IsEnabled*

 Логическое значение. Используйте `true` tooenable hello диагностики или `false` toodisable hello диагностики.
