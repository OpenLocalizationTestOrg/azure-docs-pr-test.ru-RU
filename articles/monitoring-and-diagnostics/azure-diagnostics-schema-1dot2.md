---
title: "Схема конфигурации системы диагностики 1.2 aaaAzure | Документы Microsoft"
description: "Применимо ТОЛЬКО при использовании пакета Azure SDK 2.5 с виртуальными машинами Azure, масштабируемыми наборами виртуальных машин, Service Fabric или облачными службами."
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
ms.openlocfilehash: 31559317b696556a64b51b58800b176ade9a4679
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-12-configuration-schema"></a>Схема конфигурации системы диагностики Azure 1.2
> [!NOTE]
> Система диагностики Azure — счетчики производительности toocollect компонент, используемый hello и другие статистические данные из виртуальных машин Azure, наборы масштабирования виртуальных машин, Service Fabric и облачных служб.  Данная страница применяется только в том случае, если вы используете одну из этих служб.
>

Система диагностики Azure используется с другими продуктами диагностики корпорации Майкрософт, такими как Azure Monitor, Application Insights и Log Analytics.

Эта схема определяет возможные значения hello tooinitialize диагностические параметры конфигурации можно использовать при запуске монитора диагностики hello.  


 Загрузите определение схемы файл открытой конфигурации hello, выполнив следующую команду PowerShell hello:  

```PowerShell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 Дополнительные сведения об использовании системы диагностики Azure см. в статье [Включение системы диагностики Azure в облачных службах Azure](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-hello-diagnostics-configuration-file"></a>Пример файла конфигурации диагностики hello  
 Следующий пример Hello показан типичный файл конфигурации диагностики:  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">  
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
        <EtwEventSourceProviderConfiguration provider="MyProviderClass" scheduledTransferPeriod="PT5M">  
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
      <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
        <CrashDumpConfiguration processName="mynewprocess.exe" />  
        <CrashDumpConfiguration processName="badapp.exe"/>  
      </CrashDumps>  
    </DiagnosticMonitorConfiguration>  
  </WadCfg>  
</PublicConfig>  

```  

## <a name="diagnostics-configuration-namespace"></a>Пространство имен конфигурации диагностики  
 пространство имен XML Hello для hello файла конфигурации диагностики таково:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="publicconfig-element"></a>Элемент PublicConfig  
 Элемент верхнего уровня файла конфигурации диагностики hello. Hello следующей таблице описываются элементы hello hello файла конфигурации.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**WadCfg**|Обязательный элемент. Сбор параметров конфигурации для toobe данных телеметрии hello.|  
|**StorageAccount**|Имя данных hello toostore учетной записи хранилища Azure hello в Hello. Это может также быть указан как параметр при выполнении командлета hello AzureServiceDiagnosticsExtension набор.|  
|**LocalResourceDirectory**|Hello каталог на виртуальной машине toobe hello используется hello данные события toostore Monitoring Agent. Если нет, используется набор каталог по умолчанию hello.<br /><br /> для рабочей роли или веб-роли: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> для виртуальной машины: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Ниже перечислены обязательные атрибуты.<br /><br /> -                      **путь** - hello на toobe системы hello, применяемые в диагностике Azure.<br /><br /> -                      **expandEnvironment** -управляет ли переменные среды раскрываются в имени пути hello.|  

## <a name="wadcfg-element"></a>Элемент WadCFG  
Определяет параметры конфигурации для сбора данных toobe с телеметрии hello. Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|обязательный параметр. Необязательные атрибуты:<br /><br /> -                     **overallQuotaInMB** -hello максимальный объем дискового пространства, который может использоваться hello различные типы диагностических данных, собранные системой диагностики Azure. Hello по умолчанию составляет 5120 МБ.<br /><br /> -                     **useProxyServer** -параметры настройки системы диагностики Azure toouse hello прокси-сервера, как указано в параметрах IE.|  
|**CrashDumps**|Включает сбор аварийных дампов. Необязательные атрибуты:<br /><br /> -                     **Имя контейнера** -hello имя контейнера BLOB-объектов hello в вашей toobe учетной записи хранилища Azure используется toostore аварийных дампов.<br /><br /> -                     **crashDumpType** -дампов toocollect диагностики Azure настраивает Mini или полный сбой.<br /><br /> -                     **directoryQuotaPercentage**-настраивает процент hello **overallQuotaInMB** toobe, зарезервированный для аварийные дампы на hello виртуальной Машины.|  
|**DiagnosticInfrastructureLogs**|Включает сбор журналов, создаваемых системой диагностикой Azure. журналы инфраструктуры диагностики Hello полезны для устранения неполадок hello самой системе диагностики. Необязательные атрибуты:<br /><br /> -                     **scheduledTransferLogLevelFilter** -настраивает hello минимальную степень серьезности выполняется сбор журналов hello.<br /><br /> -                     **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**Directories**|Включает Здравствуйте коллекцию hello содержимого каталога, IIS не удалось выполнить запрос журналы событий и журналы IIS. Необязательный атрибут:<br /><br /> **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. значение Hello [XML «Введите данные о длительности».](http://www.w3schools.com/schema/schema_dtypes_date.asp)|  
|**EtwProviders**|Настраивает сбор событий ETW (трассировка событий Windows) из поставщиков на основе EventSource и (или) манифеста ETW.|  
|**Метрики**|Этот элемент включает toogenerate таблицу счетчика производительности, которая оптимизирована для быстрого запросов. Каждый счетчик производительности, который определен в hello **PerformanceCounters** элемент хранится в таблице показателей hello в таблице счетчиков производительности toohello сложения. Обязательный атрибут:<br /><br /> **resourceId** — это идентификатор ресурса hello hello развертывании диагностики Azure для виртуальной машины. Получить hello **resourceID** из hello [портал Azure](https://portal.azure.com). Выберите **Обзор** -> **Группы ресурсов** -> **<Имя\>**. Нажмите кнопку hello **свойства** плитку и скопируйте значение hello из hello **идентификатор** поля.|  
|**PerformanceCounters**|Включает сбор hello счетчиков производительности. Необязательный атрибут:<br /><br /> **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**WindowsEventLog**|Включает сбор hello журналов событий Windows. Необязательный атрибут:<br /><br /> **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="crashdumps-element"></a>Элемент CrashDumps  
 Включает сбор аварийных дампов. Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**CrashDumpConfiguration**|обязательный параметр. Обязательный атрибут:<br /><br /> **processName** - hello имя требуется toocollect диагностики Azure аварийного дампа для процесса hello.|  
|**crashDumpType**|Настройка системы диагностики Azure toocollect мини- или полный аварийных дампов.|  
|**directoryQuotaPercentage**|Настраивает процент hello **overallQuotaInMB** toobe, зарезервированный для аварийные дампы на hello виртуальной Машины.|  

## <a name="directories-element"></a>Элемент Directories  
 Включает Здравствуйте коллекцию hello содержимого каталога, IIS не удалось выполнить запрос журналы событий и журналы IIS. Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**DataSources**|Список каталогов toomonitor.|  
|**FailedRequestLogs**|Включая этот элемент в конфигурации hello включает сбор журналов обо всех невыполненных запросов tooan сайту или приложению IIS. Вам также необходимо включить параметры трассировки в разделе **system.WebServer** файла **Web.config**.|  
|**IISLogs**|Включая этот элемент в конфигурации hello включает hello сбор журналов IIS:<br /><br /> **Имя контейнера** -журналы IIS hello toostore используется имя hello hello контейнер больших двоичных объектов в вашей toobe учетной записи хранилища Azure.|  

## <a name="datasources-element"></a>Элемент DataSources  
 Список каталогов toomonitor. Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**DirectoryConfiguration**|обязательный параметр. Обязательный атрибут:<br /><br /> **Имя контейнера** -имя hello hello контейнера BLOB-объектов в хранилище Azure учетной toostore toobe использовать файлы журнала hello.|  

## <a name="directoryconfiguration-element"></a>Элемент DirectoryConfiguration  
 **DirectoryConfiguration** может содержать либо hello **абсолютный** или **LocalResource** элемент, но не оба. Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**Absolute**|toomonitor directory toohello Hello абсолютный путь. Привет, следующие атрибуты не требуются:<br /><br /> -                     **Путь** -hello toomonitor directory toohello абсолютный путь.<br /><br /> -                      **expandEnvironment**: позволяет раскрыть переменные среды, указанные в пути.|  
|**LocalResource**|Здравствуйте, toomonitor локального ресурса tooa относительный путь. Ниже перечислены обязательные атрибуты.<br /><br /> -                     **Имя** -hello локального ресурса, содержащего hello directory toomonitor<br /><br /> -                     **relativePath** -hello tooName относительный путь, содержащий hello directory toomonitor|  

## <a name="etwproviders-element"></a>Элемент EtwProviders  
 Настраивает сбор событий ETW (трассировка событий Windows) из поставщиков на основе EventSource и (или) манифеста ETW. Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Позволяет настроить сбор событий, создаваемых из [класса EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Обязательный атрибут:<br /><br /> **Поставщик** -hello имя класса событий EventSource hello.<br /><br /> Необязательные атрибуты:<br /><br /> -                     **scheduledTransferLogLevelFilter** -hello учетной записи хранилища tooyour уровня tootransfer Минимальная важность.<br /><br /> -                     **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  
|**EtwManifestProviderConfiguration**|Обязательный атрибут:<br /><br /> **Поставщик** -hello GUID поставщика событий hello<br /><br /> Необязательные атрибуты:<br /><br /> - **scheduledTransferLogLevelFilter** -hello учетной записи хранилища tooyour уровня tootransfer Минимальная важность.<br /><br /> -                     **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="etweventsourceproviderconfiguration-element"></a>Элемент EtwEventSourceProviderConfiguration  
 Позволяет настроить сбор событий, создаваемых из [класса EventSource](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**DefaultEvents**|Необязательный атрибут:<br /><br /> **eventDestination** — hello имя события hello toostore hello таблицы в|  
|**Event**|Обязательный атрибут:<br /><br /> **Идентификатор** -идентификатор hello hello события.<br /><br /> Необязательный атрибут:<br /><br /> **eventDestination** — hello имя события hello toostore hello таблицы в|  

## <a name="etwmanifestproviderconfiguration-element"></a>Элемент EtwManifestProviderConfiguration  
 Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**DefaultEvents**|Необязательный атрибут:<br /><br /> **eventDestination** — hello имя события hello toostore hello таблицы в|  
|**Event**|Обязательный атрибут:<br /><br /> **Идентификатор** -идентификатор hello hello события.<br /><br /> Необязательный атрибут:<br /><br /> **eventDestination** — hello имя события hello toostore hello таблицы в|  

## <a name="metrics-element"></a>Элемент Metrics  
 Позволяет toogenerate таблицу счетчика производительности, которая оптимизирована для быстрого запросов. Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**MetricAggregation**|Обязательный атрибут:<br /><br /> **scheduledTransferPeriod** -hello интервал между запланированными передачами toostorage округляется в сторону увеличения toohello ближайшего минуты. Значение относится к [типу данных XML "Duration"](http://www.w3schools.com/schema/schema_dtypes_date.asp).|  

## <a name="performancecounters-element"></a>Элемент PerformanceCounters  
 Включает сбор hello счетчиков производительности. Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**PerformanceCounterConfiguration**|Привет, следующие атрибуты не требуются:<br /><br /> -                     **counterSpecifier** — hello имя счетчика производительности "hello". Например, `\Processor(_Total)\% Processor Time`. список счетчиков производительности на вашем узле, выполните команду hello tooget `typeperf`.<br /><br /> -                     **SampleRate содержит** -как часто hello счетчиков должны быть считаны.<br /><br /> Необязательный атрибут:<br /><br /> **Единица** -единица измерения счетчиков hello hello.|  

## <a name="performancecounterconfiguration-element"></a>Элемент PerformanceCounterConfiguration  
 Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**annotation**|Обязательный атрибут:<br /><br /> **отображаемое имя** -hello отображаемое имя для счетчика "hello"<br /><br /> Необязательный атрибут:<br /><br /> **языковой стандарт** -hello toouse языкового стандарта, при отображении hello имя счетчика|  

## <a name="windowseventlog-element"></a>Элемент WindowsEventLog  
 Привет, в следующей таблице описаны дочерние элементы.  

|Имя элемента|Описание|  
|------------------|-----------------|  
|**DataSource**|toocollect журналы событий Windows Hello. Обязательный атрибут:<br /><br /> **имя** -собранные hello запрос XPath, описывающий toobe событий windows hello. Например:<br /><br /> `Application!*[System[(Level >= 3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[System[(Level >= 3]]`<br /><br /> Укажите все события toocollect «*».|
