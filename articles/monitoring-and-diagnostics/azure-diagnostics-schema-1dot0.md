---
title: "Схема конфигурации службы диагностики 1.0 aaaAzure | Документы Microsoft"
description: "Применимо ТОЛЬКО при использовании пакета Azure SDK 2.4 и ниже с виртуальными машинами Azure, масштабируемыми наборами виртуальных машин, Service Fabric или облачными службами."
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
ms.openlocfilehash: bdd2b26217d6ea28f19e651ab429e7e7401ff57b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a>Схема конфигурации системы диагностики Azure версии 1.0
> [!NOTE]
> Система диагностики Azure — счетчики производительности toocollect компонент, используемый hello и другие статистические данные из виртуальных машин Azure, наборы масштабирования виртуальных машин, Service Fabric и облачных служб.  Данная страница применяется только в том случае, если вы используете одну из этих служб.
>

Система диагностики Azure используется с другими продуктами диагностики корпорации Майкрософт, такими как Azure Monitor, Application Insights и Log Analytics.

файл конфигурации Azure Diagnostics Hello определяет значения, используемые tooinitialize hello монитор диагностики. Этот файл является используется tooinitialize диагностические параметры конфигурации при запуске монитора диагностики hello.  

 По умолчанию файл схемы конфигурации Azure Diagnostics hello является установленных toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` каталога. Замените `<version>` с версией hello установлен hello [пакета Azure SDK](http://www.windowsazure.com/develop/downloads/).  

> [!NOTE]
>  файл конфигурации диагностики Hello обычно используется с запуска задачи, которые требуют toobe диагностические данные, собранные ранее в процессе запуска hello. Дополнительные сведения об использовании системы диагностики Azure см. в статье [Включение системы диагностики Azure в облачных службах Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Пример файла конфигурации диагностики hello  
 Следующий пример Hello показан типичный файл конфигурации диагностики:  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify hello special directories   
           that are set up for hello log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories hello DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative tooa local   
                 resource defined in hello service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- hello counter specifier is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- hello event log name is in hello same format as hello imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a>Пространство имен DiagnosticsConfiguration  
 пространство имен XML Hello для hello файла конфигурации диагностики таково:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a>Элементы схемы  
 файл конфигурации диагностики Hello содержит следующие элементы hello.


## <a name="diagnosticmonitorconfiguration-element"></a>Элемент DiagnosticMonitorConfiguration  
элемент верхнего уровня Hello hello файла конфигурации диагностики.  

Атрибуты:

|Атрибут  |Тип   |Обязательно| значение по умолчанию | Описание|  
|-----------|-------|--------|---------|------------|  
|**configurationChangePollInterval**|длительность|Необязательно | PT1M| Указывает интервал hello в какой hello монитор диагностики опрашивает изменения в конфигурации диагностики.|  
|**overallQuotaInMB**|unsignedInt|Необязательно| 4000 МБ. Если указать значение, оно не должно превышать эту величину. |общий объем хранилища файловой системы для всех буферов ведения журнала Hello.|  

## <a name="diagnosticinfrastructurelogs-element"></a>Элемент DiagnosticInfrastructureLogs  
Определяет конфигурацию буфера hello hello журналы, созданные hello базовой инфраструктурой диагностики.

Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Атрибуты:

|Атрибут|Тип|Описание|  
|---------|----|-----------------|  
|**bufferQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.<br /><br /> Hello по умолчанию — 0.|  
|**scheduledTransferLogLevelFilter**|строка|необязательный параметр. Указывает hello минимальную степень серьезности для передаваемых записей журнала. значение по умолчанию Hello — **Undefined**. Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.|  
|**scheduledTransferPeriod**|длительность|необязательный параметр. Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.<br /><br /> по умолчанию Hello — PT0S.|  

## <a name="logs-element"></a>Элемент Logs  
 Определяет конфигурацию буфера hello для базовых журналов Azure.

 Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  

Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.<br /><br /> Hello по умолчанию — 0.|  
|**scheduledTransferLogLevelFilter**|строка|необязательный параметр. Указывает hello минимальную степень серьезности для передаваемых записей журнала. значение по умолчанию Hello — **Undefined**. Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.|  
|**scheduledTransferPeriod**|длительность|необязательный параметр. Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.<br /><br /> по умолчанию Hello — PT0S.|  

## <a name="directories-element"></a>Элемент Directories  
Определяет конфигурацию буфера hello файлы журналов, можно определить.

Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).  


Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.<br /><br /> Hello по умолчанию — 0.|  
|**scheduledTransferPeriod**|длительность|необязательный параметр. Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.<br /><br /> по умолчанию Hello — PT0S.|  

## <a name="crashdumps-element"></a>Элемент CrashDumps  
 Определяет каталог аварийных дампов hello.

 Родительский элемент: [Directories](#Directories).  

Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**container**|string|передано имя Hello hello контейнера, где toobe hello содержимое каталога hello.|  
|**directoryQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный размер hello hello каталога в мегабайтах.<br /><br /> Hello по умолчанию — 0.|  

## <a name="failedrequestlogs-element"></a>Элемент FailedRequestLogs  
 Определяет каталог журнала hello невыполненных запросов.

 Родительский элемент: [Directories](#Directories).  

Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**container**|string|передано имя Hello hello контейнера, где toobe hello содержимое каталога hello.|  
|**directoryQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный размер hello hello каталога в мегабайтах.<br /><br /> Hello по умолчанию — 0.|  

##  <a name="iislogs-element"></a>Элемент IISLogs  
 Определяет каталог журнала IIS hello.

 Родительский элемент: [Directories](#Directories).  

Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**container**|string|передано имя Hello hello контейнера, где toobe hello содержимое каталога hello.|  
|**directoryQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный размер hello hello каталога в мегабайтах.<br /><br /> Hello по умолчанию — 0.|  

## <a name="datasources-element"></a>Элемент DataSources  
 Определяет ноль или более дополнительных каталогов журналов.

 Родительский элемент: [Directories](#Directories).

## <a name="directoryconfiguration-element"></a>Элемент DirectoryConfiguration  
 Определяет каталог hello toomonitor файлы журнала.

 Родительский элемент: [DataSources](#DataSources).

Атрибуты:

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**container**|string|передано имя Hello hello контейнера, где toobe hello содержимое каталога hello.|  
|**directoryQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный размер hello hello каталога в мегабайтах.<br /><br /> Hello по умолчанию — 0.|  

## <a name="absolute-element"></a>Элемент Absolute  
 Определяет, является абсолютным hello toomonitor каталога с необязательным расширением среды.

 Родительский элемент: [DirectoryConfiguration](#DirectoryConfiguration).  

Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**path**|строка|Обязательный элемент. toomonitor directory toohello Hello абсолютный путь.|  
|**expandEnvironment**|Логическое|Обязательный элемент. Если задать слишком**true**, переменные окружения по пути hello разворачиваются.|  

## <a name="localresource-element"></a>Элемент LocalResource  
 Определяет путь относительный tooa локальному ресурсу, заданному в определении службы hello.

 Родительский элемент: [DirectoryConfiguration](#DirectoryConfiguration).  

Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**name**|строка|Обязательный элемент. Имя Hello hello локального ресурса, содержащего hello directory toomonitor.|  
|**relativePath**|строка|Обязательный элемент. Здравствуйте, toomonitor локального ресурса toohello относительный путь.|  

## <a name="performancecounters-element"></a>Элемент PerformanceCounters  
 Определяет hello путь toohello производительности для счетчика toocollect.

 Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).


 Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.<br /><br /> Hello по умолчанию — 0.|  
|**scheduledTransferPeriod**|длительность|необязательный параметр. Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.<br /><br /> по умолчанию Hello — PT0S.|  

## <a name="performancecounterconfiguration-element"></a>Элемент PerformanceCounterConfiguration  
 Определяет toocollect счетчика производительности hello.

 Родительский элемент: [PerformanceCounters](#PerformanceCounters).  

 Атрибуты:  

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**counterSpecifier**|строка|Обязательный элемент. toocollect счетчик производительности toohello путь Hello.|  
|**sampleRate**|длительность|Обязательный элемент. частота Hello какие hello счетчиков производительности должны собираться.|  

## <a name="windowseventlog-element"></a>Элемент WindowsEventLog  
 Определяет toomonitor hello журналы событий.

 Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).

  Атрибуты:

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|unsignedInt|необязательный параметр. Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.<br /><br /> Hello по умолчанию — 0.|  
|**scheduledTransferLogLevelFilter**|строка|необязательный параметр. Указывает hello минимальную степень серьезности для передаваемых записей журнала. значение по умолчанию Hello — **Undefined**. Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.|  
|**scheduledTransferPeriod**|длительность|необязательный параметр. Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.<br /><br /> по умолчанию Hello — PT0S.|  

## <a name="datasource-element"></a>Элемент DataSource  
 Определяет toomonitor hello журнала событий.

 Родительский элемент: [WindowsEventLog](#windowsEventLog).  

 Атрибуты:

|Атрибут|Тип|Описание|  
|---------------|----------|-----------------|  
|**name**|строка|Обязательный элемент. Выражение XPath, задающее toocollect журнала hello.|  
