---
title: "aaaHow toouse диагностики Azure в виртуальные машины | Документы Microsoft"
description: "С помощью диагностики Azure toogather данных из виртуальных машин Azure для отладки, измерения производительности, мониторинг, анализ трафика и многое другое."
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: 
editor: 
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 54cdfd30d7bbbb71af449826e90234faf5ecdf44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="6f605-103">Включение диагностики на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="6f605-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="6f605-104">Основные сведения о системе диагностики Azure см. в [обзоре системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6f605-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="6f605-105">Как tooEnable диагностики в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="6f605-105">How tooEnable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="6f605-106">Этот обход через описывается tooremotely установки tooan диагностики виртуальной машины Azure с компьютера разработчика.</span><span class="sxs-lookup"><span data-stu-id="6f605-106">This walk through describes how tooremotely install Diagnostics tooan Azure virtual machine from a development computer.</span></span> <span data-ttu-id="6f605-107">Вы также узнаете, как приложение, которое выполняется на этой виртуальной машине Azure и передает данные телеметрии с помощью tooimplement hello .NET [класса EventSource][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="6f605-107">You also learn how tooimplement an application that runs on that Azure virtual machine and emits telemetry data using hello .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="6f605-108">Диагностика Azure телеметрия используется toocollect hello и сохранить ее в учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="6f605-108">Azure Diagnostics is used toocollect hello telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="6f605-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6f605-109">Pre-requisites</span></span>
<span data-ttu-id="6f605-110">Этот проход по предполагается есть подписка Azure и с помощью Visual Studio 2017 г. с hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="6f605-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with hello Azure SDK.</span></span> <span data-ttu-id="6f605-111">Если нет подписки Azure, вы можете зарегистрироваться для hello [бесплатной пробной версии][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="6f605-111">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="6f605-112">Убедитесь, что слишком[Установка и настройка Azure PowerShell версии 0.8.7 или более поздней версии][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="6f605-112">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="6f605-113">Шаг 1. Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="6f605-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="6f605-114">На компьютере разработчика запустите Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6f605-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="6f605-115">В Visual Studio hello **обозревателя серверов** разверните **Azure**, щелкните правой кнопкой мыши **виртуальные машины** выберите **создания виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="6f605-115">In hello Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="6f605-116">Выберите подписку Azure в hello **выберите подписку** окна и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6f605-116">Select your Azure subscription in hello **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="6f605-117">Выберите **Windows Server 2012 R2 Datacenter июня 2017 г** в hello **выберите образ виртуальной машины** окна и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6f605-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in hello **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="6f605-118">В hello **основные параметры виртуальной машины**, задайте имя виртуальной машины hello слишком «wadexample».</span><span class="sxs-lookup"><span data-stu-id="6f605-118">In hello **Virtual Machine Basic Settings**, set hello virtual machine name too"wadexample".</span></span> <span data-ttu-id="6f605-119">Укажите имя пользователя и пароль администратора и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6f605-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="6f605-120">В hello **параметры облачной службы** диалоговое окно создания новой облачной службы с именем «wadexampleVM».</span><span class="sxs-lookup"><span data-stu-id="6f605-120">In hello **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="6f605-121">Создайте новую учетную запись хранения с именем wadexample и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6f605-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="6f605-122">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6f605-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="6f605-123">Шаг 2. Создание приложения</span><span class="sxs-lookup"><span data-stu-id="6f605-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="6f605-124">На компьютере разработчика запустите Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6f605-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="6f605-125">Создайте новое приложение консоли Visual C#, предназначенное для платформы .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="6f605-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="6f605-126">Имя проекта hello «WadExampleVM».</span><span class="sxs-lookup"><span data-stu-id="6f605-126">Name hello project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="6f605-128">Замените содержимое Program.cs hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="6f605-128">Replace hello contents of Program.cs with hello following code.</span></span> <span data-ttu-id="6f605-129">Здравствуйте, класс **SampleEventSourceWriter** реализует четыре методы ведения журнала: **SendEnums**, **MessageMethod**, **SetOther** и  **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="6f605-129">hello class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="6f605-130">Hello toohello первый параметр метода WriteEvent определяет идентификатор hello hello соответствующих событий.</span><span class="sxs-lookup"><span data-stu-id="6f605-130">hello first parameter toohello WriteEvent method defines hello ID for hello respective event.</span></span> <span data-ttu-id="6f605-131">Метод Run Hello реализует бесконечный цикл, который вызывает каждую hello методы ведения журнала, реализованный в hello **SampleEventSourceWriter** класса каждые 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="6f605-131">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums tooint for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through hello loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. <span data-ttu-id="6f605-132">Сохранить файл hello и выберите **построить решение** из hello **построения** меню toobuild кода.</span><span class="sxs-lookup"><span data-stu-id="6f605-132">Save hello file and select **Build Solution** from hello **Build** menu toobuild your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="6f605-133">Шаг 3. Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="6f605-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="6f605-134">Щелкните правой кнопкой мыши на hello **WadExampleVM** проекта в **обозревателе решений** и выберите **открыть папку в проводнике**.</span><span class="sxs-lookup"><span data-stu-id="6f605-134">Right-click on hello **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="6f605-135">Перейдите toohello *bin\Debug* папки и всех hello копирования файлов (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="6f605-135">Navigate toohello *bin\Debug* folder and copy all hello files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="6f605-136">В **обозревателя серверов** щелкните правой кнопкой мыши на виртуальной машине hello и выберите **подключиться с помощью удаленного рабочего стола**.</span><span class="sxs-lookup"><span data-stu-id="6f605-136">In **Server Explorer** right-click on hello virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="6f605-137">После подключения toohello виртуальной Машины создайте папку с именем WadExampleVM и вставьте файлы приложения в папке hello.</span><span class="sxs-lookup"><span data-stu-id="6f605-137">Once connected toohello VM create a folder named WadExampleVM and paste your application files into hello folder.</span></span>
5. <span data-ttu-id="6f605-138">Запуск приложения hello WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="6f605-138">Launch hello application WadExampleVM.exe.</span></span> <span data-ttu-id="6f605-139">Должно отобразиться пустое окно консоли.</span><span class="sxs-lookup"><span data-stu-id="6f605-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-hello-extension"></a><span data-ttu-id="6f605-140">Шаг 4: Создайте конфигурацию диагностики и установите расширение hello</span><span class="sxs-lookup"><span data-stu-id="6f605-140">Step 4: Create your Diagnostics configuration and install hello Extension</span></span>
1. <span data-ttu-id="6f605-141">Загрузите открытую конфигурацию hello файла определения схемы tooyour компьютера разработчика, выполнив следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="6f605-141">Download hello public configuration file schema definition tooyour development computer by executing hello following PowerShell command:</span></span>

     <span data-ttu-id="6f605-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="6f605-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="6f605-143">Откройте новый XML-файл в Visual Studio либо в уже открытом проекте, либо в экземпляре Visual Studio без открытых проектов.</span><span class="sxs-lookup"><span data-stu-id="6f605-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="6f605-144">В Visual Studio выберите **Добавить** -> **Новый элемент...**</span><span class="sxs-lookup"><span data-stu-id="6f605-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="6f605-145"> -> **Элементы Visual C#** -> **Данные** -> **XML-файл**.</span><span class="sxs-lookup"><span data-stu-id="6f605-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="6f605-146">Имя файла hello «WadExample.xml»</span><span class="sxs-lookup"><span data-stu-id="6f605-146">Name hello file "WadExample.xml"</span></span>
3. <span data-ttu-id="6f605-147">Hello WadConfig.xsd свяжите с файлом конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="6f605-147">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="6f605-148">Убедитесь, что окно редактора WadExample.xml hello — активное окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="6f605-148">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="6f605-149">Нажмите клавишу **F4** tooopen hello **свойства** окна.</span><span class="sxs-lookup"><span data-stu-id="6f605-149">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="6f605-150">Щелкните hello **схемы** свойство в hello **свойства** окна.</span><span class="sxs-lookup"><span data-stu-id="6f605-150">Click on hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="6f605-151">Нажмите кнопку hello **...**</span><span class="sxs-lookup"><span data-stu-id="6f605-151">Click hello **…**</span></span> <span data-ttu-id="6f605-152">в hello **схемы** свойство.</span><span class="sxs-lookup"><span data-stu-id="6f605-152">in hello **Schemas** property.</span></span> <span data-ttu-id="6f605-153">Нажмите кнопку hello **добавить...**</span><span class="sxs-lookup"><span data-stu-id="6f605-153">Click hello **Add…**</span></span> <span data-ttu-id="6f605-154">кнопки и перейдите toohello расположение, где был сохранен файл XSD hello и выберите hello WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="6f605-154">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="6f605-155">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6f605-155">Click **OK**.</span></span>
4. <span data-ttu-id="6f605-156">Замените содержимое файла конфигурации WadExample.xml hello hello на hello следующий XML-код и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="6f605-156">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="6f605-157">Этот файл конфигурации определяет несколько toocollect счетчиков производительности: для загрузки ЦП и использования памяти.</span><span class="sxs-lookup"><span data-stu-id="6f605-157">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="6f605-158">Затем конфигурация hello определяет четыре события hello соответствующий toohello методы в классе SampleEventSourceWriter hello.</span><span class="sxs-lookup"><span data-stu-id="6f605-158">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```
        <?xml version="1.0" encoding="utf-8"?>
        <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
              <WadCfg>
                <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
                  <PerformanceCounters scheduledTransferPeriod="PT1M">
                    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
                    <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
                      </PerformanceCounters>
                      <EtwProviders>
                        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
                              <Event id="1" eventDestination="EnumsTable"/>
                              <Event id="2" eventDestination="MessageTable"/>
                              <Event id="3" eventDestination="SetOtherTable"/>
                              <Event id="4" eventDestination="HighFreqTable"/>
                              <DefaultEvents eventDestination="DefaultTable" />
                        </EtwEventSourceProviderConfiguration>
                      </EtwProviders>
                </DiagnosticMonitorConfiguration>
              </WadCfg>
        </PublicConfig>
```

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="6f605-159">Шаг 5. Удаленная установка системы диагностики на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="6f605-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="6f605-160">Hello командлеты PowerShell для управления системой диагностики на виртуальной Машине являются: набор AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension и Remove AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="6f605-160">hello PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="6f605-161">На компьютере разработчика откройте Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f605-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="6f605-162">Выполнение установки tooremotely hello сценария диагностики на виртуальной Машине (Замените `<user>` с вашим именем пользователя каталога.</span><span class="sxs-lookup"><span data-stu-id="6f605-162">Execute hello script tooremotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="6f605-163">Замените `<StorageAccountKey>` с hello ключ учетной записи хранения для вашей учетной записи wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="6f605-163">Replace `<StorageAccountKey>` with hello storage account key for your wadexamplevm storage account):</span></span>
```
     $storage_name = "wadexamplevm"
     $key = "<StorageAccountKey>"
     $config_path="c:\users\<user>\documents\visual studio 2017\Projects\WadExampleVM\WadExampleVM\WadExample.xml"
     $service_name="wadexamplevm"
     $vm_name="WadExample"
     $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
     $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name
     $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.*" -VM $VM1 -StorageContext $storageContext
     $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM
```
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="6f605-164">Шаг 6. Просмотр данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="6f605-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="6f605-165">В Visual Studio hello **обозревателя серверов** учетной записи хранилища wadexample toohello перехода.</span><span class="sxs-lookup"><span data-stu-id="6f605-165">In hello Visual Studio **Server Explorer** navigate toohello wadexample storage account.</span></span> <span data-ttu-id="6f605-166">После hello ВМ работает около 5 минут вы должны увидеть hello таблицы **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**,  **WADPerformanceCountersTable** и **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="6f605-166">After hello VM has been running about 5 minutes you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="6f605-167">Дважды щелкните на одном hello телеметрии hello таблиц tooview, которые были собраны.</span><span class="sxs-lookup"><span data-stu-id="6f605-167">Double-click on one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="6f605-169">Схема файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="6f605-169">Configuration file schema</span></span>
<span data-ttu-id="6f605-170">файл конфигурации диагностики Hello определяет значения, используемые tooinitialize диагностические параметры конфигурации при запуске агента диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="6f605-170">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="6f605-171">В разделе hello [последняя ссылка на схему](https://msdn.microsoft.com/library/azure/mt634524.aspx) допустимые значения и примеры.</span><span class="sxs-lookup"><span data-stu-id="6f605-171">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6f605-172">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="6f605-172">Troubleshooting</span></span>
<span data-ttu-id="6f605-173">Дополнительные сведения см. в разделе [Устранение неполадок системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="6f605-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f605-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f605-174">Next steps</span></span>
<span data-ttu-id="6f605-175">[См. список виртуальных машин, других связанных статьях диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello данные собираются, устранения неполадок или Дополнительные сведения о диагностике в целом.</span><span class="sxs-lookup"><span data-stu-id="6f605-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
