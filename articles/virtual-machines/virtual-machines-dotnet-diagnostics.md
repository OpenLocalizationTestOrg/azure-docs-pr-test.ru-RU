---
title: "Как использовать систему диагностики Azure на виртуальных машинах | Документация Майкрософт"
description: "Сбор данных виртуальных машин Azure с помощью системы диагностики Azure для отладки, оценки производительности, мониторинга, анализа трафика и многого другого."
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
ms.openlocfilehash: 8ff6b9825212359617b748aba1c78ed789b130dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="0f275-103">Включение диагностики на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="0f275-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="0f275-104">Основные сведения о системе диагностики Azure см. в [обзоре системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="0f275-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="0f275-105">Как включить диагностику в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="0f275-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="0f275-106">Мы рассмотрим, как удаленно установить систему диагностики на виртуальной машине Azure с компьютера разработчика.</span><span class="sxs-lookup"><span data-stu-id="0f275-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="0f275-107">Также вы узнаете, как реализовать приложение, которое выполняется на виртуальной машине Azure и отправляет данные телеметрии через класс .NET [EventSource][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="0f275-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="0f275-108">Система диагностики Azure используется для сбора телеметрии и хранения ее в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="0f275-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="0f275-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0f275-109">Pre-requisites</span></span>
<span data-ttu-id="0f275-110">В этом пошаговом учебнике предполагается, что у вас есть подписка Azure и вы используете Visual Studio 2017 с пакетом SDK для Azure.</span><span class="sxs-lookup"><span data-stu-id="0f275-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2017 with the Azure SDK.</span></span> <span data-ttu-id="0f275-111">Если у вас нет подписки Azure, можно зарегистрироваться для получения [бесплатной пробной версии][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="0f275-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="0f275-112">Следует обязательно [установить и настроить Azure PowerShell версии 0.8.7 или более поздней][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="0f275-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="0f275-113">Шаг 1. Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0f275-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="0f275-114">На компьютере разработчика запустите Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="0f275-114">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="0f275-115">В **обозревателе сервера** Visual Studio разверните **Azure**, щелкните правой кнопкой мыши элемент **Виртуальные машины** и выберите команду **Создать виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="0f275-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="0f275-116">В диалоговом окне **Выбор подписки** выберите свою подписку Azure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0f275-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="0f275-117">В диалоговом окне **Выбор образа виртуальной машины** выберите **Windows Server 2012 R2 Datacenter, June 2017** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0f275-117">Select **Windows Server 2012 R2 Datacenter, June 2017** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="0f275-118">В разделе **базовых параметров виртуальной машины**укажите для виртуальной машины имя wadexample.</span><span class="sxs-lookup"><span data-stu-id="0f275-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="0f275-119">Укажите имя пользователя и пароль администратора и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0f275-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="0f275-120">В диалоговом окне **Параметры облачной службы** создайте новую облачную службу с именем wadexampleVM.</span><span class="sxs-lookup"><span data-stu-id="0f275-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="0f275-121">Создайте новую учетную запись хранения с именем wadexample и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0f275-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="0f275-122">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0f275-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="0f275-123">Шаг 2. Создание приложения</span><span class="sxs-lookup"><span data-stu-id="0f275-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="0f275-124">На компьютере разработчика запустите Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="0f275-124">On your development computer, launch Visual Studio 2017.</span></span>
2. <span data-ttu-id="0f275-125">Создайте новое приложение консоли Visual C#, предназначенное для платформы .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="0f275-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="0f275-126">Назовите проект «WadExampleVM».</span><span class="sxs-lookup"><span data-stu-id="0f275-126">Name the project "WadExampleVM".</span></span>

   ![CloudServices_diag_new_project](./media/virtual-machines-dotnet-diagnostics/NewProject.png)
3. <span data-ttu-id="0f275-128">Замените содержимое файла Program.cs на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="0f275-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="0f275-129">Класс **SampleEventSourceWriter** реализует четыре метода ведения журнала: **SendEnums**, **MessageMethod**, **SetOther** и **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="0f275-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="0f275-130">Первый параметр для метода WriteEvent определяет идентификатор соответствующего события.</span><span class="sxs-lookup"><span data-stu-id="0f275-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="0f275-131">Метод Run реализует бесконечный цикл, который вызывает каждый из методов ведения журнала, реализованных в классе **SampleEventSourceWriter** , каждые 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="0f275-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
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

             // Emit several events every time we go through the loop
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
4. <span data-ttu-id="0f275-132">Сохраните файл и в меню **Сборка** выберите **Собрать решение**, чтобы выполнить сборку кода.</span><span class="sxs-lookup"><span data-stu-id="0f275-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="0f275-133">Шаг 3. Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="0f275-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="0f275-134">В **обозревателе решений** щелкните правой кнопкой мыши проект **WadExampleVM** и выберите **Открыть папку в проводнике**.</span><span class="sxs-lookup"><span data-stu-id="0f275-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="0f275-135">Перейдите к папке *bin\Debug* и скопируйте все файлы (WadExampleVM.*)</span><span class="sxs-lookup"><span data-stu-id="0f275-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.*)</span></span>
3. <span data-ttu-id="0f275-136">В **обозревателе сервера** щелкните правой кнопкой мыши виртуальную машину и выберите **Подключиться с помощью удаленного рабочего стола**.</span><span class="sxs-lookup"><span data-stu-id="0f275-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="0f275-137">После подключения к виртуальной машине создайте папку с именем WadExampleVM и вставьте в нее свои файлы приложения.</span><span class="sxs-lookup"><span data-stu-id="0f275-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="0f275-138">Запустите приложение WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="0f275-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="0f275-139">Должно отобразиться пустое окно консоли.</span><span class="sxs-lookup"><span data-stu-id="0f275-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="0f275-140">Шаг 4. Создание конфигурации системы диагностики и установка расширения</span><span class="sxs-lookup"><span data-stu-id="0f275-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="0f275-141">Скачайте общедоступное определение схемы файла конфигурации на свой компьютер для разработки, выполнив следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0f275-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="0f275-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="0f275-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="0f275-143">Откройте новый XML-файл в Visual Studio либо в уже открытом проекте, либо в экземпляре Visual Studio без открытых проектов.</span><span class="sxs-lookup"><span data-stu-id="0f275-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="0f275-144">В Visual Studio выберите **Добавить** -> **Новый элемент...**</span><span class="sxs-lookup"><span data-stu-id="0f275-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="0f275-145"> -> **Элементы Visual C#** -> **Данные** -> **XML-файл**.</span><span class="sxs-lookup"><span data-stu-id="0f275-145"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="0f275-146">Назовите файл «WadExample.xml».</span><span class="sxs-lookup"><span data-stu-id="0f275-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="0f275-147">Свяжите файл WadConfig.xsd с файлом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0f275-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="0f275-148">Убедитесь, что окно редактора WadExample.xml активно.</span><span class="sxs-lookup"><span data-stu-id="0f275-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="0f275-149">Нажмите клавишу **F4**, чтобы открыть окно **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0f275-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="0f275-150">Щелкните свойство **Schemas** в окне **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0f275-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="0f275-151">Щелкните **…**</span><span class="sxs-lookup"><span data-stu-id="0f275-151">Click the **…**</span></span> <span data-ttu-id="0f275-152">in the **Schemas** .</span><span class="sxs-lookup"><span data-stu-id="0f275-152">in the **Schemas** property.</span></span> <span data-ttu-id="0f275-153">Щелкните **Добавить…**</span><span class="sxs-lookup"><span data-stu-id="0f275-153">Click the **Add…**</span></span> <span data-ttu-id="0f275-154">, перейдите в расположение, где сохранен XSD-файл, и выберите файл WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="0f275-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="0f275-155">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0f275-155">Click **OK**.</span></span>
4. <span data-ttu-id="0f275-156">Замените содержимое файла настройки WadExample.xml приведенным кодом XML и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="0f275-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="0f275-157">Этот файл конфигурации определяет пару счетчиков производительности: один — для использование ЦП, и один — для использования памяти.</span><span class="sxs-lookup"><span data-stu-id="0f275-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="0f275-158">Затем конфигурация определяет четыре события, соответствующие методам в классе SampleEventSourceWriter.</span><span class="sxs-lookup"><span data-stu-id="0f275-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="0f275-159">Шаг 5. Удаленная установка системы диагностики на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="0f275-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="0f275-160">Командлеты PowerShell для управления диагностикой на виртуальной машине: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension и Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="0f275-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="0f275-161">На компьютере разработчика откройте Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f275-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="0f275-162">Выполните сценарий, чтобы удаленно установить диагностику на виртуальной машине (Замените `<user>` своим именем пользователя каталога.</span><span class="sxs-lookup"><span data-stu-id="0f275-162">Execute the script to remotely install Diagnostics on your VM (Replace `<user>` with your user directory name.</span></span> <span data-ttu-id="0f275-163">Замените `<StorageAccountKey>` ключом учетной записи хранения для вашей учетной записи wadexamplevm):</span><span class="sxs-lookup"><span data-stu-id="0f275-163">Replace `<StorageAccountKey>` with the storage account key for your wadexamplevm storage account):</span></span>
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
### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="0f275-164">Шаг 6. Просмотр данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="0f275-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="0f275-165">В **обозревателе решений** Visual Studio перейдите к учетной записи хранения wadexample.</span><span class="sxs-lookup"><span data-stu-id="0f275-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="0f275-166">После того, как виртуальная машина проработала около пяти минут, следует посмотреть таблицы **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** и **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="0f275-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="0f275-167">Дважды щелкните одну из таблиц, чтобы просмотреть собранную телеметрию.</span><span class="sxs-lookup"><span data-stu-id="0f275-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](./media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="0f275-169">Схема файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="0f275-169">Configuration file schema</span></span>
<span data-ttu-id="0f275-170">Файл конфигурации системы диагностики определяет значения, которые используются для инициализации параметров конфигурации диагностики, когда запускается агент диагностики.</span><span class="sxs-lookup"><span data-stu-id="0f275-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="0f275-171">Допустимые значения и примеры см. в [последнем справочнике по схеме](https://msdn.microsoft.com/library/azure/mt634524.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f275-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0f275-172">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="0f275-172">Troubleshooting</span></span>
<span data-ttu-id="0f275-173">Дополнительные сведения см. в разделе [Устранение неполадок системы диагностики Azure](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="0f275-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f275-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f275-174">Next steps</span></span>
<span data-ttu-id="0f275-175">[См. перечень статей о системе диагностики Azure, связанных с виртуальными машинами](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) , чтобы изменить данные, которые собираются, устранить неполадки или больше узнать о диагностике в целом.</span><span class="sxs-lookup"><span data-stu-id="0f275-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
