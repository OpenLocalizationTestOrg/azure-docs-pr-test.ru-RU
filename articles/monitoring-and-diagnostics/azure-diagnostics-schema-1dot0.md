---
title: "Схема конфигурации системы диагностики Azure версии 1.0 | Документация Майкрософт"
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
ms.openlocfilehash: a8fdfb52d5091d3fc9779657737c7430fcfada51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="48577-103">Схема конфигурации системы диагностики Azure версии 1.0</span><span class="sxs-lookup"><span data-stu-id="48577-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="48577-104">Система диагностики Azure — это компонент, который используется для сбора данных счетчиков производительности и других статистических данных из виртуальных машин Azure, масштабируемых наборов виртуальных машин, Service Fabric и облачных служб.</span><span class="sxs-lookup"><span data-stu-id="48577-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="48577-105">Данная страница применяется только в том случае, если вы используете одну из этих служб.</span><span class="sxs-lookup"><span data-stu-id="48577-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="48577-106">Система диагностики Azure используется с другими продуктами диагностики корпорации Майкрософт, такими как Azure Monitor, Application Insights и Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="48577-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="48577-107">Файл конфигурации системы диагностики Azure определяет значения, которые используются для инициализации монитора диагностики.</span><span class="sxs-lookup"><span data-stu-id="48577-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="48577-108">Этот файл используется для инициализации параметров конфигурации диагностики при запуске монитора диагностики.</span><span class="sxs-lookup"><span data-stu-id="48577-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="48577-109">По умолчанию файл схемы конфигурации системы диагностики Azure устанавливается в каталог `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas`.</span><span class="sxs-lookup"><span data-stu-id="48577-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="48577-110">Замените `<version>` установленной версией [пакета SDK для Azure](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="48577-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="48577-111">Файл конфигурации диагностики обычно используется в задачах запуска, переда запуском которых должны быть собраны нужные им диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="48577-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="48577-112">Дополнительные сведения об использовании системы диагностики Azure см. в статье [Включение системы диагностики Azure в облачных службах Azure](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="48577-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="48577-113">Пример файла конфигурации диагностики</span><span class="sxs-lookup"><span data-stu-id="48577-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="48577-114">В следующем примере показан типичный файл конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="48577-114">The following example shows a typical diagnostics configuration file:</span></span>  

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

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="48577-115">Пространство имен DiagnosticsConfiguration</span><span class="sxs-lookup"><span data-stu-id="48577-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="48577-116">Пространство имен XML для файла конфигурации диагностики:</span><span class="sxs-lookup"><span data-stu-id="48577-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="48577-117">Элементы схемы</span><span class="sxs-lookup"><span data-stu-id="48577-117">Schema Elements</span></span>  
 <span data-ttu-id="48577-118">Файл конфигурации диагностики содержит следующие элементы.</span><span class="sxs-lookup"><span data-stu-id="48577-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="48577-119">Элемент DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="48577-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="48577-120">Элемент верхнего уровня в файле конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="48577-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="48577-121">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-121">Attributes:</span></span>

|<span data-ttu-id="48577-122">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-122">Attribute</span></span>  |<span data-ttu-id="48577-123">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-123">Type</span></span>   |<span data-ttu-id="48577-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="48577-124">Required</span></span>| <span data-ttu-id="48577-125">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="48577-125">Default</span></span> | <span data-ttu-id="48577-126">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="48577-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="48577-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="48577-128">длительность</span><span class="sxs-lookup"><span data-stu-id="48577-128">duration</span></span>|<span data-ttu-id="48577-129">Необязательно</span><span class="sxs-lookup"><span data-stu-id="48577-129">Optional</span></span> | <span data-ttu-id="48577-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="48577-130">PT1M</span></span>| <span data-ttu-id="48577-131">Указывает интервал, с которым монитор диагностики опрашивает наличие изменений конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="48577-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="48577-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="48577-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-133">unsignedInt</span></span>|<span data-ttu-id="48577-134">Необязательно</span><span class="sxs-lookup"><span data-stu-id="48577-134">Optional</span></span>| <span data-ttu-id="48577-135">4000 МБ.</span><span class="sxs-lookup"><span data-stu-id="48577-135">4000 MB.</span></span> <span data-ttu-id="48577-136">Если указать значение, оно не должно превышать эту величину.</span><span class="sxs-lookup"><span data-stu-id="48577-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="48577-137">Общий объем хранилища файловой системы, выделенный для всех буферов ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="48577-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="48577-138">Элемент DiagnosticInfrastructureLogs</span><span class="sxs-lookup"><span data-stu-id="48577-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="48577-139">Определяет конфигурацию буфера для журналов, которые создает базовая инфраструктура диагностики.</span><span class="sxs-lookup"><span data-stu-id="48577-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="48577-140">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48577-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="48577-141">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-141">Attributes:</span></span>

|<span data-ttu-id="48577-142">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-142">Attribute</span></span>|<span data-ttu-id="48577-143">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-143">Type</span></span>|<span data-ttu-id="48577-144">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="48577-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48577-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-146">unsignedInt</span></span>|<span data-ttu-id="48577-147">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-147">Optional.</span></span> <span data-ttu-id="48577-148">Указывает максимальный объем хранилища файловой системы, который доступен для указанных данных.</span><span class="sxs-lookup"><span data-stu-id="48577-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="48577-149">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-149">The default is 0.</span></span>|  
|<span data-ttu-id="48577-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="48577-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="48577-151">строка</span><span class="sxs-lookup"><span data-stu-id="48577-151">string</span></span>|<span data-ttu-id="48577-152">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-152">Optional.</span></span> <span data-ttu-id="48577-153">Указывает минимальный уровень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="48577-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="48577-154">По умолчанию используется значение **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="48577-154">The default value is **Undefined**.</span></span> <span data-ttu-id="48577-155">Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.</span><span class="sxs-lookup"><span data-stu-id="48577-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="48577-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48577-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48577-157">длительность</span><span class="sxs-lookup"><span data-stu-id="48577-157">duration</span></span>|<span data-ttu-id="48577-158">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-158">Optional.</span></span> <span data-ttu-id="48577-159">Указывает интервал между запланированными передачами данных, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="48577-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="48577-160">По умолчанию используется значение PT0S.</span><span class="sxs-lookup"><span data-stu-id="48577-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="48577-161">Элемент Logs</span><span class="sxs-lookup"><span data-stu-id="48577-161">Logs Element</span></span>  
 <span data-ttu-id="48577-162">Определяет конфигурацию буфера для базовых журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="48577-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="48577-163">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48577-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="48577-164">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-164">Attributes:</span></span>  

|<span data-ttu-id="48577-165">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-165">Attribute</span></span>|<span data-ttu-id="48577-166">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-166">Type</span></span>|<span data-ttu-id="48577-167">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48577-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-169">unsignedInt</span></span>|<span data-ttu-id="48577-170">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-170">Optional.</span></span> <span data-ttu-id="48577-171">Указывает максимальный объем хранилища файловой системы, который доступен для указанных данных.</span><span class="sxs-lookup"><span data-stu-id="48577-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="48577-172">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-172">The default is 0.</span></span>|  
|<span data-ttu-id="48577-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="48577-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="48577-174">строка</span><span class="sxs-lookup"><span data-stu-id="48577-174">string</span></span>|<span data-ttu-id="48577-175">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-175">Optional.</span></span> <span data-ttu-id="48577-176">Указывает минимальный уровень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="48577-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="48577-177">По умолчанию используется значение **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="48577-177">The default value is **Undefined**.</span></span> <span data-ttu-id="48577-178">Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.</span><span class="sxs-lookup"><span data-stu-id="48577-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="48577-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48577-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48577-180">длительность</span><span class="sxs-lookup"><span data-stu-id="48577-180">duration</span></span>|<span data-ttu-id="48577-181">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-181">Optional.</span></span> <span data-ttu-id="48577-182">Указывает интервал между запланированными передачами данных, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="48577-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="48577-183">По умолчанию используется значение PT0S.</span><span class="sxs-lookup"><span data-stu-id="48577-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="48577-184">Элемент Directories</span><span class="sxs-lookup"><span data-stu-id="48577-184">Directories Element</span></span>  
<span data-ttu-id="48577-185">Определяет конфигурацию буфера для журналов на основе файлов, которые можно определить.</span><span class="sxs-lookup"><span data-stu-id="48577-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="48577-186">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48577-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="48577-187">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-187">Attributes:</span></span>  

|<span data-ttu-id="48577-188">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-188">Attribute</span></span>|<span data-ttu-id="48577-189">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-189">Type</span></span>|<span data-ttu-id="48577-190">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48577-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-192">unsignedInt</span></span>|<span data-ttu-id="48577-193">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-193">Optional.</span></span> <span data-ttu-id="48577-194">Указывает максимальный объем хранилища файловой системы, который доступен для указанных данных.</span><span class="sxs-lookup"><span data-stu-id="48577-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="48577-195">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-195">The default is 0.</span></span>|  
|<span data-ttu-id="48577-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48577-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48577-197">длительность</span><span class="sxs-lookup"><span data-stu-id="48577-197">duration</span></span>|<span data-ttu-id="48577-198">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-198">Optional.</span></span> <span data-ttu-id="48577-199">Указывает интервал между запланированными передачами данных, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="48577-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="48577-200">По умолчанию используется значение PT0S.</span><span class="sxs-lookup"><span data-stu-id="48577-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="48577-201">Элемент CrashDumps</span><span class="sxs-lookup"><span data-stu-id="48577-201">CrashDumps Element</span></span>  
 <span data-ttu-id="48577-202">Определяет каталог аварийных дампов.</span><span class="sxs-lookup"><span data-stu-id="48577-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="48577-203">Родительский элемент: [Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="48577-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="48577-204">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-204">Attributes:</span></span>  

|<span data-ttu-id="48577-205">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-205">Attribute</span></span>|<span data-ttu-id="48577-206">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-206">Type</span></span>|<span data-ttu-id="48577-207">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-208">**container**</span><span class="sxs-lookup"><span data-stu-id="48577-208">**container**</span></span>|<span data-ttu-id="48577-209">строка</span><span class="sxs-lookup"><span data-stu-id="48577-209">string</span></span>|<span data-ttu-id="48577-210">Имя контейнера, в который будет передаваться содержимое каталога.</span><span class="sxs-lookup"><span data-stu-id="48577-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="48577-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="48577-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-212">unsignedInt</span></span>|<span data-ttu-id="48577-213">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-213">Optional.</span></span> <span data-ttu-id="48577-214">Определяет максимальный размер каталога в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="48577-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="48577-215">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="48577-216">Элемент FailedRequestLogs</span><span class="sxs-lookup"><span data-stu-id="48577-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="48577-217">Определяет каталог журнала невыполненных запросов.</span><span class="sxs-lookup"><span data-stu-id="48577-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="48577-218">Родительский элемент: [Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="48577-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="48577-219">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-219">Attributes:</span></span>  

|<span data-ttu-id="48577-220">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-220">Attribute</span></span>|<span data-ttu-id="48577-221">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-221">Type</span></span>|<span data-ttu-id="48577-222">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-223">**container**</span><span class="sxs-lookup"><span data-stu-id="48577-223">**container**</span></span>|<span data-ttu-id="48577-224">строка</span><span class="sxs-lookup"><span data-stu-id="48577-224">string</span></span>|<span data-ttu-id="48577-225">Имя контейнера, в который будет передаваться содержимое каталога.</span><span class="sxs-lookup"><span data-stu-id="48577-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="48577-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="48577-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-227">unsignedInt</span></span>|<span data-ttu-id="48577-228">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-228">Optional.</span></span> <span data-ttu-id="48577-229">Определяет максимальный размер каталога в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="48577-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="48577-230">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="48577-231">Элемент IISLogs</span><span class="sxs-lookup"><span data-stu-id="48577-231">IISLogs Element</span></span>  
 <span data-ttu-id="48577-232">Определяет каталог журнала IIS.</span><span class="sxs-lookup"><span data-stu-id="48577-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="48577-233">Родительский элемент: [Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="48577-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="48577-234">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-234">Attributes:</span></span>  

|<span data-ttu-id="48577-235">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-235">Attribute</span></span>|<span data-ttu-id="48577-236">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-236">Type</span></span>|<span data-ttu-id="48577-237">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-238">**container**</span><span class="sxs-lookup"><span data-stu-id="48577-238">**container**</span></span>|<span data-ttu-id="48577-239">строка</span><span class="sxs-lookup"><span data-stu-id="48577-239">string</span></span>|<span data-ttu-id="48577-240">Имя контейнера, в который будет передаваться содержимое каталога.</span><span class="sxs-lookup"><span data-stu-id="48577-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="48577-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="48577-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-242">unsignedInt</span></span>|<span data-ttu-id="48577-243">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-243">Optional.</span></span> <span data-ttu-id="48577-244">Определяет максимальный размер каталога в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="48577-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="48577-245">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="48577-246">Элемент DataSources</span><span class="sxs-lookup"><span data-stu-id="48577-246">DataSources Element</span></span>  
 <span data-ttu-id="48577-247">Определяет ноль или более дополнительных каталогов журналов.</span><span class="sxs-lookup"><span data-stu-id="48577-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="48577-248">Родительский элемент: [Directories](#Directories).</span><span class="sxs-lookup"><span data-stu-id="48577-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="48577-249">Элемент DirectoryConfiguration</span><span class="sxs-lookup"><span data-stu-id="48577-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="48577-250">Определяет каталог файлов журнала для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="48577-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="48577-251">Родительский элемент: [DataSources](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="48577-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="48577-252">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-252">Attributes:</span></span>

|<span data-ttu-id="48577-253">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-253">Attribute</span></span>|<span data-ttu-id="48577-254">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-254">Type</span></span>|<span data-ttu-id="48577-255">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-256">**container**</span><span class="sxs-lookup"><span data-stu-id="48577-256">**container**</span></span>|<span data-ttu-id="48577-257">строка</span><span class="sxs-lookup"><span data-stu-id="48577-257">string</span></span>|<span data-ttu-id="48577-258">Имя контейнера, в который будет передаваться содержимое каталога.</span><span class="sxs-lookup"><span data-stu-id="48577-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="48577-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="48577-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-260">unsignedInt</span></span>|<span data-ttu-id="48577-261">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-261">Optional.</span></span> <span data-ttu-id="48577-262">Определяет максимальный размер каталога в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="48577-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="48577-263">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="48577-264">Элемент Absolute</span><span class="sxs-lookup"><span data-stu-id="48577-264">Absolute Element</span></span>  
 <span data-ttu-id="48577-265">Определяет абсолютный путь к отслеживаемому каталогу с необязательным раскрытием переменных среды.</span><span class="sxs-lookup"><span data-stu-id="48577-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="48577-266">Родительский элемент: [DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48577-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="48577-267">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-267">Attributes:</span></span>  

|<span data-ttu-id="48577-268">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-268">Attribute</span></span>|<span data-ttu-id="48577-269">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-269">Type</span></span>|<span data-ttu-id="48577-270">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-271">**path**</span><span class="sxs-lookup"><span data-stu-id="48577-271">**path**</span></span>|<span data-ttu-id="48577-272">строка</span><span class="sxs-lookup"><span data-stu-id="48577-272">string</span></span>|<span data-ttu-id="48577-273">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-273">Required.</span></span> <span data-ttu-id="48577-274">Абсолютный путь к отслеживаемому каталогу.</span><span class="sxs-lookup"><span data-stu-id="48577-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="48577-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="48577-275">**expandEnvironment**</span></span>|<span data-ttu-id="48577-276">Логическое</span><span class="sxs-lookup"><span data-stu-id="48577-276">boolean</span></span>|<span data-ttu-id="48577-277">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-277">Required.</span></span> <span data-ttu-id="48577-278">Если задано значение **true**, то переменные среды в пути раскрываются.</span><span class="sxs-lookup"><span data-stu-id="48577-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="48577-279">Элемент LocalResource</span><span class="sxs-lookup"><span data-stu-id="48577-279">LocalResource Element</span></span>  
 <span data-ttu-id="48577-280">Определяет путь относительно локального ресурса, заданного в определении службы.</span><span class="sxs-lookup"><span data-stu-id="48577-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="48577-281">Родительский элемент: [DirectoryConfiguration](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48577-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="48577-282">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-282">Attributes:</span></span>  

|<span data-ttu-id="48577-283">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-283">Attribute</span></span>|<span data-ttu-id="48577-284">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-284">Type</span></span>|<span data-ttu-id="48577-285">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-286">**name**</span><span class="sxs-lookup"><span data-stu-id="48577-286">**name**</span></span>|<span data-ttu-id="48577-287">строка</span><span class="sxs-lookup"><span data-stu-id="48577-287">string</span></span>|<span data-ttu-id="48577-288">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-288">Required.</span></span> <span data-ttu-id="48577-289">Имя локального ресурса, который содержит каталог для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="48577-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="48577-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="48577-290">**relativePath**</span></span>|<span data-ttu-id="48577-291">строка</span><span class="sxs-lookup"><span data-stu-id="48577-291">string</span></span>|<span data-ttu-id="48577-292">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-292">Required.</span></span> <span data-ttu-id="48577-293">Путь относительно отслеживаемого локального ресурса.</span><span class="sxs-lookup"><span data-stu-id="48577-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="48577-294">Элемент PerformanceCounters</span><span class="sxs-lookup"><span data-stu-id="48577-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="48577-295">Определяет путь к счетчику производительности, данные которого будут собираться.</span><span class="sxs-lookup"><span data-stu-id="48577-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="48577-296">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48577-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="48577-297">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-297">Attributes:</span></span>  

|<span data-ttu-id="48577-298">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-298">Attribute</span></span>|<span data-ttu-id="48577-299">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-299">Type</span></span>|<span data-ttu-id="48577-300">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48577-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-302">unsignedInt</span></span>|<span data-ttu-id="48577-303">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-303">Optional.</span></span> <span data-ttu-id="48577-304">Указывает максимальный объем хранилища файловой системы, который доступен для указанных данных.</span><span class="sxs-lookup"><span data-stu-id="48577-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="48577-305">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-305">The default is 0.</span></span>|  
|<span data-ttu-id="48577-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48577-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48577-307">длительность</span><span class="sxs-lookup"><span data-stu-id="48577-307">duration</span></span>|<span data-ttu-id="48577-308">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-308">Optional.</span></span> <span data-ttu-id="48577-309">Указывает интервал между запланированными передачами данных, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="48577-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="48577-310">По умолчанию используется значение PT0S.</span><span class="sxs-lookup"><span data-stu-id="48577-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="48577-311">Элемент PerformanceCounterConfiguration</span><span class="sxs-lookup"><span data-stu-id="48577-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="48577-312">Определяет счетчик производительности, данные которого будут собираться.</span><span class="sxs-lookup"><span data-stu-id="48577-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="48577-313">Родительский элемент: [PerformanceCounters](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="48577-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="48577-314">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-314">Attributes:</span></span>  

|<span data-ttu-id="48577-315">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-315">Attribute</span></span>|<span data-ttu-id="48577-316">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-316">Type</span></span>|<span data-ttu-id="48577-317">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="48577-318">**counterSpecifier**</span></span>|<span data-ttu-id="48577-319">строка</span><span class="sxs-lookup"><span data-stu-id="48577-319">string</span></span>|<span data-ttu-id="48577-320">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-320">Required.</span></span> <span data-ttu-id="48577-321">Путь к счетчику производительности, данные которого будут собираться.</span><span class="sxs-lookup"><span data-stu-id="48577-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="48577-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="48577-322">**sampleRate**</span></span>|<span data-ttu-id="48577-323">длительность</span><span class="sxs-lookup"><span data-stu-id="48577-323">duration</span></span>|<span data-ttu-id="48577-324">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-324">Required.</span></span> <span data-ttu-id="48577-325">Частота сбора данных счетчика производительности.</span><span class="sxs-lookup"><span data-stu-id="48577-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="48577-326">Элемент WindowsEventLog</span><span class="sxs-lookup"><span data-stu-id="48577-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="48577-327">Определяет журналы событий для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="48577-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="48577-328">Родительский элемент: [DiagnosticMonitorConfiguration](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="48577-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="48577-329">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-329">Attributes:</span></span>

|<span data-ttu-id="48577-330">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-330">Attribute</span></span>|<span data-ttu-id="48577-331">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-331">Type</span></span>|<span data-ttu-id="48577-332">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="48577-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="48577-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="48577-334">unsignedInt</span></span>|<span data-ttu-id="48577-335">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-335">Optional.</span></span> <span data-ttu-id="48577-336">Указывает максимальный объем хранилища файловой системы, который доступен для указанных данных.</span><span class="sxs-lookup"><span data-stu-id="48577-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="48577-337">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="48577-337">The default is 0.</span></span>|  
|<span data-ttu-id="48577-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="48577-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="48577-339">строка</span><span class="sxs-lookup"><span data-stu-id="48577-339">string</span></span>|<span data-ttu-id="48577-340">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-340">Optional.</span></span> <span data-ttu-id="48577-341">Указывает минимальный уровень серьезности для передаваемых записей журнала.</span><span class="sxs-lookup"><span data-stu-id="48577-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="48577-342">По умолчанию используется значение **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="48577-342">The default value is **Undefined**.</span></span> <span data-ttu-id="48577-343">Другие возможные значения: **Verbose**, **Information**, **Warning**, **Error** и **Critical**.</span><span class="sxs-lookup"><span data-stu-id="48577-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="48577-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="48577-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="48577-345">длительность</span><span class="sxs-lookup"><span data-stu-id="48577-345">duration</span></span>|<span data-ttu-id="48577-346">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-346">Optional.</span></span> <span data-ttu-id="48577-347">Указывает интервал между запланированными передачами данных, округленный с точностью до ближайшей минуты.</span><span class="sxs-lookup"><span data-stu-id="48577-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="48577-348">По умолчанию используется значение PT0S.</span><span class="sxs-lookup"><span data-stu-id="48577-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="48577-349">Элемент DataSource</span><span class="sxs-lookup"><span data-stu-id="48577-349">DataSource Element</span></span>  
 <span data-ttu-id="48577-350">Определяет журнал событий для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="48577-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="48577-351">Родительский элемент: [WindowsEventLog](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="48577-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="48577-352">Атрибуты:</span><span class="sxs-lookup"><span data-stu-id="48577-352">Attributes:</span></span>

|<span data-ttu-id="48577-353">Атрибут</span><span class="sxs-lookup"><span data-stu-id="48577-353">Attribute</span></span>|<span data-ttu-id="48577-354">Тип</span><span class="sxs-lookup"><span data-stu-id="48577-354">Type</span></span>|<span data-ttu-id="48577-355">Описание</span><span class="sxs-lookup"><span data-stu-id="48577-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="48577-356">**name**</span><span class="sxs-lookup"><span data-stu-id="48577-356">**name**</span></span>|<span data-ttu-id="48577-357">строка</span><span class="sxs-lookup"><span data-stu-id="48577-357">string</span></span>|<span data-ttu-id="48577-358">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="48577-358">Required.</span></span> <span data-ttu-id="48577-359">Выражение XPath, задающее журнал для сбора.</span><span class="sxs-lookup"><span data-stu-id="48577-359">An XPath expression specifying the log to collect.</span></span>|  
