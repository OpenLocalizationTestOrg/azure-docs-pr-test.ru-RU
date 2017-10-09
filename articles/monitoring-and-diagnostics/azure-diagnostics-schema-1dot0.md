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
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="60769-103">Схема конфигурации системы диагностики Azure версии 1.0</span><span class="sxs-lookup"><span data-stu-id="60769-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="60769-104">Система диагностики Azure — счетчики производительности toocollect компонент, используемый hello и другие статистические данные из виртуальных машин Azure, наборы масштабирования виртуальных машин, Service Fabric и облачных служб.</span><span class="sxs-lookup"><span data-stu-id="60769-104">Azure Diagnostics is hello component used toocollect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="60769-105">Данная страница применяется только в том случае, если вы используете одну из этих служб.</span><span class="sxs-lookup"><span data-stu-id="60769-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="60769-106">Система диагностики Azure используется с другими продуктами диагностики корпорации Майкрософт, такими как Azure Monitor, Application Insights и Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="60769-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="60769-107">файл конфигурации Azure Diagnostics Hello определяет значения, используемые tooinitialize hello монитор диагностики.</span><span class="sxs-lookup"><span data-stu-id="60769-107">hello Azure Diagnostics configuration file defines values that are used tooinitialize hello Diagnostics Monitor.</span></span> <span data-ttu-id="60769-108">Этот файл является используется tooinitialize диагностические параметры конфигурации при запуске монитора диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="60769-108">This file is used tooinitialize diagnostic configuration settings when hello diagnostics monitor starts.</span></span>  

 <span data-ttu-id="60769-109">По умолчанию файл схемы конфигурации Azure Diagnostics hello является установленных toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` каталога.</span><span class="sxs-lookup"><span data-stu-id="60769-109">By default, hello Azure Diagnostics configuration schema file is installed toohello `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="60769-110">Замените `<version>` с версией hello установлен hello [пакета Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="60769-110">Replace `<version>` with hello installed version of hello [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="60769-111">файл конфигурации диагностики Hello обычно используется с запуска задачи, которые требуют toobe диагностические данные, собранные ранее в процессе запуска hello.</span><span class="sxs-lookup"><span data-stu-id="60769-111">hello diagnostics configuration file is typically used with startup tasks that require diagnostic data toobe collected earlier in hello startup process.</span></span> <span data-ttu-id="60769-112">Дополнительные сведения об использовании системы диагностики Azure см. в статье [Включение системы диагностики Azure в облачных службах Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="60769-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-hello-diagnostics-configuration-file"></a><span data-ttu-id="60769-113">Пример файла конфигурации диагностики hello</span><span class="sxs-lookup"><span data-stu-id="60769-113">Example of hello diagnostics configuration file</span></span>  
 <span data-ttu-id="60769-114">Следующий пример Hello показан типичный файл конфигурации диагностики:</span><span class="sxs-lookup"><span data-stu-id="60769-114">hello following example shows a typical diagnostics configuration file:</span></span>  

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

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="60769-115">Пространство имен DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="60769-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="60769-116">пространство имен XML Hello для hello файла конфигурации диагностики таково:</span><span class="sxs-lookup"><span data-stu-id="60769-116">hello XML namespace for hello diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="60769-117">Элементы схемы</span><span class="sxs-lookup"><span data-stu-id="60769-117">Schema Elements</span></span>  
 <span data-ttu-id="60769-118">файл конфигурации диагностики Hello содержит следующие элементы hello.</span><span class="sxs-lookup"><span data-stu-id="60769-118">hello diagnostics configuration file includes hello following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="60769-119">Элемент DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="60769-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="60769-120">элемент верхнего уровня Hello hello файла конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="60769-120">hello top-level element of hello diagnostics configuration file.</span></span>  

<span data-ttu-id="60769-121">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-121">Attributes:</span></span>

|<span data-ttu-id="60769-122">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-122">Attribute</span></span>  |<span data-ttu-id="60769-123">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-123">Type</span></span>   |<span data-ttu-id="60769-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60769-124">Required</span></span>| <span data-ttu-id="60769-125">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="60769-125">Default</span></span> | <span data-ttu-id="60769-126">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="60769-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="60769-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="60769-128">длительность</span><span class="sxs-lookup"><span data-stu-id="60769-128">duration</span></span>|<span data-ttu-id="60769-129">Необязательно</span><span class="sxs-lookup"><span data-stu-id="60769-129">Optional</span></span> | <span data-ttu-id="60769-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="60769-130">PT1M</span></span>| <span data-ttu-id="60769-131">Указывает интервал hello в какой hello монитор диагностики опрашивает изменения в конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="60769-131">Specifies hello interval at which hello diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="60769-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="60769-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-133">unsignedInt</span></span>|<span data-ttu-id="60769-134">Необязательно</span><span class="sxs-lookup"><span data-stu-id="60769-134">Optional</span></span>| <span data-ttu-id="60769-135">4000 МБ.</span><span class="sxs-lookup"><span data-stu-id="60769-135">4000 MB.</span></span> <span data-ttu-id="60769-136">Если указать значение, оно не должно превышать эту величину.</span><span class="sxs-lookup"><span data-stu-id="60769-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="60769-137">общий объем хранилища файловой системы для всех буферов ведения журнала Hello.</span><span class="sxs-lookup"><span data-stu-id="60769-137">hello total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="60769-138">Элемент DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="60769-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="60769-139">Определяет конфигурацию буфера hello hello журналы, созданные hello базовой инфраструктурой диагностики.</span><span class="sxs-lookup"><span data-stu-id="60769-139">Defines hello buffer configuration for hello logs that are generated by hello underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="60769-140">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="60769-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="60769-141">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-141">Attributes:</span></span>

|<span data-ttu-id="60769-142">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-142">Attribute</span></span>|<span data-ttu-id="60769-143">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-143">Type</span></span>|<span data-ttu-id="60769-144">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="60769-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="60769-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-146">unsignedInt</span></span>|<span data-ttu-id="60769-147">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-147">Optional.</span></span> <span data-ttu-id="60769-148">Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.</span><span class="sxs-lookup"><span data-stu-id="60769-148">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="60769-149">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-149">hello default is 0.</span></span>|  
|<span data-ttu-id="60769-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="60769-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="60769-151">строка</span><span class="sxs-lookup"><span data-stu-id="60769-151">string</span></span>|<span data-ttu-id="60769-152">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-152">Optional.</span></span> <span data-ttu-id="60769-153">Указывает hello минимальную степень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="60769-153">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="60769-154">значение по умолчанию Hello — **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="60769-154">hello default value is **Undefined**.</span></span> <span data-ttu-id="60769-155">Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.</span><span class="sxs-lookup"><span data-stu-id="60769-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="60769-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="60769-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="60769-157">длительность</span><span class="sxs-lookup"><span data-stu-id="60769-157">duration</span></span>|<span data-ttu-id="60769-158">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-158">Optional.</span></span> <span data-ttu-id="60769-159">Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="60769-159">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="60769-160">по умолчанию Hello — PT0S.</span><span class="sxs-lookup"><span data-stu-id="60769-160">hello default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="60769-161">Элемент Logs</span><span class="sxs-lookup"><span data-stu-id="60769-161">Logs Element</span></span>  
 <span data-ttu-id="60769-162">Определяет конфигурацию буфера hello для базовых журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="60769-162">Defines hello buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="60769-163">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="60769-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="60769-164">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-164">Attributes:</span></span>  

|<span data-ttu-id="60769-165">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-165">Attribute</span></span>|<span data-ttu-id="60769-166">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-166">Type</span></span>|<span data-ttu-id="60769-167">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="60769-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-169">unsignedInt</span></span>|<span data-ttu-id="60769-170">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-170">Optional.</span></span> <span data-ttu-id="60769-171">Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.</span><span class="sxs-lookup"><span data-stu-id="60769-171">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="60769-172">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-172">hello default is 0.</span></span>|  
|<span data-ttu-id="60769-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="60769-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="60769-174">строка</span><span class="sxs-lookup"><span data-stu-id="60769-174">string</span></span>|<span data-ttu-id="60769-175">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-175">Optional.</span></span> <span data-ttu-id="60769-176">Указывает hello минимальную степень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="60769-176">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="60769-177">значение по умолчанию Hello — **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="60769-177">hello default value is **Undefined**.</span></span> <span data-ttu-id="60769-178">Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.</span><span class="sxs-lookup"><span data-stu-id="60769-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="60769-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="60769-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="60769-180">длительность</span><span class="sxs-lookup"><span data-stu-id="60769-180">duration</span></span>|<span data-ttu-id="60769-181">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-181">Optional.</span></span> <span data-ttu-id="60769-182">Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="60769-182">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="60769-183">по умолчанию Hello — PT0S.</span><span class="sxs-lookup"><span data-stu-id="60769-183">hello default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="60769-184">Элемент Directories</span><span class="sxs-lookup"><span data-stu-id="60769-184">Directories Element</span></span>  
<span data-ttu-id="60769-185">Определяет конфигурацию буфера hello файлы журналов, можно определить.</span><span class="sxs-lookup"><span data-stu-id="60769-185">Defines hello buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="60769-186">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="60769-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="60769-187">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-187">Attributes:</span></span>  

|<span data-ttu-id="60769-188">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-188">Attribute</span></span>|<span data-ttu-id="60769-189">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-189">Type</span></span>|<span data-ttu-id="60769-190">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="60769-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-192">unsignedInt</span></span>|<span data-ttu-id="60769-193">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-193">Optional.</span></span> <span data-ttu-id="60769-194">Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.</span><span class="sxs-lookup"><span data-stu-id="60769-194">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="60769-195">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-195">hello default is 0.</span></span>|  
|<span data-ttu-id="60769-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="60769-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="60769-197">длительность</span><span class="sxs-lookup"><span data-stu-id="60769-197">duration</span></span>|<span data-ttu-id="60769-198">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-198">Optional.</span></span> <span data-ttu-id="60769-199">Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="60769-199">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="60769-200">по умолчанию Hello — PT0S.</span><span class="sxs-lookup"><span data-stu-id="60769-200">hello default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="60769-201">Элемент CrashDumps</span><span class="sxs-lookup"><span data-stu-id="60769-201">CrashDumps Element</span></span>  
 <span data-ttu-id="60769-202">Определяет каталог аварийных дампов hello.</span><span class="sxs-lookup"><span data-stu-id="60769-202">Defines hello crash dumps directory.</span></span>

 <span data-ttu-id="60769-203">Родительский элемент: [Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="60769-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="60769-204">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-204">Attributes:</span></span>  

|<span data-ttu-id="60769-205">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-205">Attribute</span></span>|<span data-ttu-id="60769-206">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-206">Type</span></span>|<span data-ttu-id="60769-207">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-208">**container**</span><span class="sxs-lookup"><span data-stu-id="60769-208">**container**</span></span>|<span data-ttu-id="60769-209">string</span><span class="sxs-lookup"><span data-stu-id="60769-209">string</span></span>|<span data-ttu-id="60769-210">передано имя Hello hello контейнера, где toobe hello содержимое каталога hello.</span><span class="sxs-lookup"><span data-stu-id="60769-210">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="60769-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="60769-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-212">unsignedInt</span></span>|<span data-ttu-id="60769-213">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-213">Optional.</span></span> <span data-ttu-id="60769-214">Указывает максимальный размер hello hello каталога в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="60769-214">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="60769-215">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-215">hello default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="60769-216">Элемент FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="60769-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="60769-217">Определяет каталог журнала hello невыполненных запросов.</span><span class="sxs-lookup"><span data-stu-id="60769-217">Defines hello failed request log directory.</span></span>

 <span data-ttu-id="60769-218">Родительский элемент: [Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="60769-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="60769-219">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-219">Attributes:</span></span>  

|<span data-ttu-id="60769-220">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-220">Attribute</span></span>|<span data-ttu-id="60769-221">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-221">Type</span></span>|<span data-ttu-id="60769-222">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-223">**container**</span><span class="sxs-lookup"><span data-stu-id="60769-223">**container**</span></span>|<span data-ttu-id="60769-224">string</span><span class="sxs-lookup"><span data-stu-id="60769-224">string</span></span>|<span data-ttu-id="60769-225">передано имя Hello hello контейнера, где toobe hello содержимое каталога hello.</span><span class="sxs-lookup"><span data-stu-id="60769-225">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="60769-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="60769-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-227">unsignedInt</span></span>|<span data-ttu-id="60769-228">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-228">Optional.</span></span> <span data-ttu-id="60769-229">Указывает максимальный размер hello hello каталога в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="60769-229">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="60769-230">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-230">hello default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="60769-231">Элемент IISLogs</span><span class="sxs-lookup"><span data-stu-id="60769-231">IISLogs Element</span></span>  
 <span data-ttu-id="60769-232">Определяет каталог журнала IIS hello.</span><span class="sxs-lookup"><span data-stu-id="60769-232">Defines hello IIS log directory.</span></span>

 <span data-ttu-id="60769-233">Родительский элемент: [Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="60769-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="60769-234">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-234">Attributes:</span></span>  

|<span data-ttu-id="60769-235">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-235">Attribute</span></span>|<span data-ttu-id="60769-236">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-236">Type</span></span>|<span data-ttu-id="60769-237">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-238">**container**</span><span class="sxs-lookup"><span data-stu-id="60769-238">**container**</span></span>|<span data-ttu-id="60769-239">string</span><span class="sxs-lookup"><span data-stu-id="60769-239">string</span></span>|<span data-ttu-id="60769-240">передано имя Hello hello контейнера, где toobe hello содержимое каталога hello.</span><span class="sxs-lookup"><span data-stu-id="60769-240">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="60769-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="60769-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-242">unsignedInt</span></span>|<span data-ttu-id="60769-243">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-243">Optional.</span></span> <span data-ttu-id="60769-244">Указывает максимальный размер hello hello каталога в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="60769-244">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="60769-245">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-245">hello default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="60769-246">Элемент DataSources</span><span class="sxs-lookup"><span data-stu-id="60769-246">DataSources Element</span></span>  
 <span data-ttu-id="60769-247">Определяет ноль или более дополнительных каталогов журналов.</span><span class="sxs-lookup"><span data-stu-id="60769-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="60769-248">Родительский элемент: [Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="60769-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="60769-249">Элемент DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="60769-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="60769-250">Определяет каталог hello toomonitor файлы журнала.</span><span class="sxs-lookup"><span data-stu-id="60769-250">Defines hello directory of log files toomonitor.</span></span>

 <span data-ttu-id="60769-251">Родительский элемент: [DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="60769-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="60769-252">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-252">Attributes:</span></span>

|<span data-ttu-id="60769-253">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-253">Attribute</span></span>|<span data-ttu-id="60769-254">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-254">Type</span></span>|<span data-ttu-id="60769-255">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-256">**container**</span><span class="sxs-lookup"><span data-stu-id="60769-256">**container**</span></span>|<span data-ttu-id="60769-257">string</span><span class="sxs-lookup"><span data-stu-id="60769-257">string</span></span>|<span data-ttu-id="60769-258">передано имя Hello hello контейнера, где toobe hello содержимое каталога hello.</span><span class="sxs-lookup"><span data-stu-id="60769-258">hello name of hello container where hello contents of hello directory is toobe transferred.</span></span>|  
|<span data-ttu-id="60769-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="60769-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-260">unsignedInt</span></span>|<span data-ttu-id="60769-261">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-261">Optional.</span></span> <span data-ttu-id="60769-262">Указывает максимальный размер hello hello каталога в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="60769-262">Specifies hello maximum size of hello directory in megabytes.</span></span><br /><br /> <span data-ttu-id="60769-263">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-263">hello default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="60769-264">Элемент Absolute</span><span class="sxs-lookup"><span data-stu-id="60769-264">Absolute Element</span></span>  
 <span data-ttu-id="60769-265">Определяет, является абсолютным hello toomonitor каталога с необязательным расширением среды.</span><span class="sxs-lookup"><span data-stu-id="60769-265">Defines an absolute path of hello directory toomonitor with optional environment expansion.</span></span>

 <span data-ttu-id="60769-266">Родительский элемент: [DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="60769-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="60769-267">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-267">Attributes:</span></span>  

|<span data-ttu-id="60769-268">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-268">Attribute</span></span>|<span data-ttu-id="60769-269">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-269">Type</span></span>|<span data-ttu-id="60769-270">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-271">**path**</span><span class="sxs-lookup"><span data-stu-id="60769-271">**path**</span></span>|<span data-ttu-id="60769-272">строка</span><span class="sxs-lookup"><span data-stu-id="60769-272">string</span></span>|<span data-ttu-id="60769-273">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="60769-273">Required.</span></span> <span data-ttu-id="60769-274">toomonitor directory toohello Hello абсолютный путь.</span><span class="sxs-lookup"><span data-stu-id="60769-274">hello absolute path toohello directory toomonitor.</span></span>|  
|<span data-ttu-id="60769-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="60769-275">**expandEnvironment**</span></span>|<span data-ttu-id="60769-276">Логическое</span><span class="sxs-lookup"><span data-stu-id="60769-276">boolean</span></span>|<span data-ttu-id="60769-277">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="60769-277">Required.</span></span> <span data-ttu-id="60769-278">Если задать слишком**true**, переменные окружения по пути hello разворачиваются.</span><span class="sxs-lookup"><span data-stu-id="60769-278">If set too**true**, environment variables in hello path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="60769-279">Элемент LocalResource</span><span class="sxs-lookup"><span data-stu-id="60769-279">LocalResource Element</span></span>  
 <span data-ttu-id="60769-280">Определяет путь относительный tooa локальному ресурсу, заданному в определении службы hello.</span><span class="sxs-lookup"><span data-stu-id="60769-280">Defines a path relative tooa local resource defined in hello service definition.</span></span>

 <span data-ttu-id="60769-281">Родительский элемент: [DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="60769-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="60769-282">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-282">Attributes:</span></span>  

|<span data-ttu-id="60769-283">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-283">Attribute</span></span>|<span data-ttu-id="60769-284">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-284">Type</span></span>|<span data-ttu-id="60769-285">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-286">**name**</span><span class="sxs-lookup"><span data-stu-id="60769-286">**name**</span></span>|<span data-ttu-id="60769-287">строка</span><span class="sxs-lookup"><span data-stu-id="60769-287">string</span></span>|<span data-ttu-id="60769-288">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="60769-288">Required.</span></span> <span data-ttu-id="60769-289">Имя Hello hello локального ресурса, содержащего hello directory toomonitor.</span><span class="sxs-lookup"><span data-stu-id="60769-289">hello name of hello local resource that contains hello directory toomonitor.</span></span>|  
|<span data-ttu-id="60769-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="60769-290">**relativePath**</span></span>|<span data-ttu-id="60769-291">строка</span><span class="sxs-lookup"><span data-stu-id="60769-291">string</span></span>|<span data-ttu-id="60769-292">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="60769-292">Required.</span></span> <span data-ttu-id="60769-293">Здравствуйте, toomonitor локального ресурса toohello относительный путь.</span><span class="sxs-lookup"><span data-stu-id="60769-293">hello path relative toohello local resource toomonitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="60769-294">Элемент PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="60769-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="60769-295">Определяет hello путь toohello производительности для счетчика toocollect.</span><span class="sxs-lookup"><span data-stu-id="60769-295">Defines hello path toohello performance counter toocollect.</span></span>

 <span data-ttu-id="60769-296">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="60769-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="60769-297">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-297">Attributes:</span></span>  

|<span data-ttu-id="60769-298">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-298">Attribute</span></span>|<span data-ttu-id="60769-299">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-299">Type</span></span>|<span data-ttu-id="60769-300">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="60769-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-302">unsignedInt</span></span>|<span data-ttu-id="60769-303">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-303">Optional.</span></span> <span data-ttu-id="60769-304">Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.</span><span class="sxs-lookup"><span data-stu-id="60769-304">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="60769-305">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-305">hello default is 0.</span></span>|  
|<span data-ttu-id="60769-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="60769-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="60769-307">длительность</span><span class="sxs-lookup"><span data-stu-id="60769-307">duration</span></span>|<span data-ttu-id="60769-308">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-308">Optional.</span></span> <span data-ttu-id="60769-309">Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="60769-309">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="60769-310">по умолчанию Hello — PT0S.</span><span class="sxs-lookup"><span data-stu-id="60769-310">hello default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="60769-311">Элемент PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="60769-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="60769-312">Определяет toocollect счетчика производительности hello.</span><span class="sxs-lookup"><span data-stu-id="60769-312">Defines hello performance counter toocollect.</span></span>

 <span data-ttu-id="60769-313">Родительский элемент: [PerformanceCounters](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="60769-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="60769-314">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-314">Attributes:</span></span>  

|<span data-ttu-id="60769-315">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-315">Attribute</span></span>|<span data-ttu-id="60769-316">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-316">Type</span></span>|<span data-ttu-id="60769-317">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="60769-318">**counterSpecifier**</span></span>|<span data-ttu-id="60769-319">строка</span><span class="sxs-lookup"><span data-stu-id="60769-319">string</span></span>|<span data-ttu-id="60769-320">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="60769-320">Required.</span></span> <span data-ttu-id="60769-321">toocollect счетчик производительности toohello путь Hello.</span><span class="sxs-lookup"><span data-stu-id="60769-321">hello path toohello performance counter toocollect.</span></span>|  
|<span data-ttu-id="60769-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="60769-322">**sampleRate**</span></span>|<span data-ttu-id="60769-323">длительность</span><span class="sxs-lookup"><span data-stu-id="60769-323">duration</span></span>|<span data-ttu-id="60769-324">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="60769-324">Required.</span></span> <span data-ttu-id="60769-325">частота Hello какие hello счетчиков производительности должны собираться.</span><span class="sxs-lookup"><span data-stu-id="60769-325">hello rate at which hello performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="60769-326">Элемент WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="60769-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="60769-327">Определяет toomonitor hello журналы событий.</span><span class="sxs-lookup"><span data-stu-id="60769-327">Defines hello event logs toomonitor.</span></span>

 <span data-ttu-id="60769-328">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="60769-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="60769-329">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-329">Attributes:</span></span>

|<span data-ttu-id="60769-330">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-330">Attribute</span></span>|<span data-ttu-id="60769-331">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-331">Type</span></span>|<span data-ttu-id="60769-332">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="60769-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="60769-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="60769-334">unsignedInt</span></span>|<span data-ttu-id="60769-335">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-335">Optional.</span></span> <span data-ttu-id="60769-336">Указывает максимальный объем хранилища файловой системы, доступные для указанного hello hello данных.</span><span class="sxs-lookup"><span data-stu-id="60769-336">Specifies hello maximum amount of file system storage that is available for hello specified data.</span></span><br /><br /> <span data-ttu-id="60769-337">Hello по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="60769-337">hello default is 0.</span></span>|  
|<span data-ttu-id="60769-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="60769-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="60769-339">строка</span><span class="sxs-lookup"><span data-stu-id="60769-339">string</span></span>|<span data-ttu-id="60769-340">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-340">Optional.</span></span> <span data-ttu-id="60769-341">Указывает hello минимальную степень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="60769-341">Specifies hello minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="60769-342">значение по умолчанию Hello — **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="60769-342">hello default value is **Undefined**.</span></span> <span data-ttu-id="60769-343">Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.</span><span class="sxs-lookup"><span data-stu-id="60769-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="60769-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="60769-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="60769-345">длительность</span><span class="sxs-lookup"><span data-stu-id="60769-345">duration</span></span>|<span data-ttu-id="60769-346">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="60769-346">Optional.</span></span> <span data-ttu-id="60769-347">Hello интервал между запланированными передачами данных, округленный toohello ближайшего минуты.</span><span class="sxs-lookup"><span data-stu-id="60769-347">Specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span><br /><br /> <span data-ttu-id="60769-348">по умолчанию Hello — PT0S.</span><span class="sxs-lookup"><span data-stu-id="60769-348">hello default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="60769-349">Элемент DataSource</span><span class="sxs-lookup"><span data-stu-id="60769-349">DataSource Element</span></span>  
 <span data-ttu-id="60769-350">Определяет toomonitor hello журнала событий.</span><span class="sxs-lookup"><span data-stu-id="60769-350">Defines hello event log toomonitor.</span></span>

 <span data-ttu-id="60769-351">Родительский элемент: [WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="60769-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="60769-352">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="60769-352">Attributes:</span></span>

|<span data-ttu-id="60769-353">Атрибут</span><span class="sxs-lookup"><span data-stu-id="60769-353">Attribute</span></span>|<span data-ttu-id="60769-354">Тип</span><span class="sxs-lookup"><span data-stu-id="60769-354">Type</span></span>|<span data-ttu-id="60769-355">Описание</span><span class="sxs-lookup"><span data-stu-id="60769-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="60769-356">**name**</span><span class="sxs-lookup"><span data-stu-id="60769-356">**name**</span></span>|<span data-ttu-id="60769-357">строка</span><span class="sxs-lookup"><span data-stu-id="60769-357">string</span></span>|<span data-ttu-id="60769-358">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="60769-358">Required.</span></span> <span data-ttu-id="60769-359">Выражение XPath, задающее toocollect журнала hello.</span><span class="sxs-lookup"><span data-stu-id="60769-359">An XPath expression specifying hello log toocollect.</span></span>|  
