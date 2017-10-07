---
title: "aaaHow toouse диагностики Azure (.NET) с облачными службами | Документы Microsoft"
description: "С помощью диагностики Azure toogather данных из Azure облачных служб для отладки, измерения производительности, мониторинг, анализ трафика и многое другое."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 1525eac1e85955d8f05aa21a9805e0a80d0e4bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="5fc6e-103">Включение системы диагностики Azure в облачных службах Azure</span><span class="sxs-lookup"><span data-stu-id="5fc6e-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="5fc6e-104">Основные сведения о системе диагностики Azure см. в [обзоре системы диагностики Azure](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5fc6e-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-tooenable-diagnostics-in-a-worker-role"></a><span data-ttu-id="5fc6e-105">Как tooEnable диагностики в рабочей роли</span><span class="sxs-lookup"><span data-stu-id="5fc6e-105">How tooEnable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="5fc6e-106">В этом пошаговом руководстве описывается, как tooimplement рабочей роли Azure, создающего данные телеметрии с помощью hello класс .NET EventSource.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-106">This walkthrough describes how tooimplement an Azure worker role that emits telemetry data using hello .NET EventSource class.</span></span> <span data-ttu-id="5fc6e-107">Система диагностики Azure данные телеметрии используется toocollect hello и сохранить ее в учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-107">Azure Diagnostics is used toocollect hello telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="5fc6e-108">При создании рабочей роли, Visual Studio автоматически включает 1.0 диагностики как часть решения hello в пакеты SDK Azure для .NET 2.4 и более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of hello solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="5fc6e-109">Hello следующие инструкции описывают процесс hello создания hello рабочей роли, отключение 1.0 диагностики из решения hello и развертывание Diagnostics версии 1.2 или 1.3 tooyour рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-109">hello following instructions describe hello process for creating hello worker role, disabling Diagnostics 1.0 from hello solution, and deploying Diagnostics 1.2 or 1.3 tooyour worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="5fc6e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5fc6e-110">Prerequisites</span></span>
<span data-ttu-id="5fc6e-111">В этой статье предполагается есть подписка Azure и с помощью Visual Studio с hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-111">This article assumes you have an Azure subscription and are using Visual Studio with hello Azure SDK.</span></span> <span data-ttu-id="5fc6e-112">Если нет подписки Azure, вы можете зарегистрироваться для hello [бесплатной пробной версии][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="5fc6e-112">If you do not have an Azure subscription, you can sign up for hello [Free Trial][Free Trial].</span></span> <span data-ttu-id="5fc6e-113">Убедитесь, что слишком[Установка и настройка Azure PowerShell версии 0.8.7 или более поздней версии][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="5fc6e-113">Make sure too[Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="5fc6e-114">Шаг 1. Создание рабочей роли</span><span class="sxs-lookup"><span data-stu-id="5fc6e-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="5fc6e-115">Запустите **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="5fc6e-116">Создание **облачной службы Azure** проект из hello **облака** шаблона, ориентированном на .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-116">Create an **Azure Cloud Service** project from hello **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="5fc6e-117">Назовите проект hello «WadExample» и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-117">Name hello project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="5fc6e-118">Выберите **рабочую роль** и нажмите кнопку «ОК».</span><span class="sxs-lookup"><span data-stu-id="5fc6e-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="5fc6e-119">будет создан проект Hello.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-119">hello project will be created.</span></span>
4. <span data-ttu-id="5fc6e-120">В **обозревателе решений**, дважды щелкните hello **WorkerRole1** файла свойств.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-120">In **Solution Explorer**, double-click hello **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="5fc6e-121">В hello **конфигурации** вкладки, отмените **включить диагностику** toodisable диагностики 1.0 (Azure SDK 2.4 и более ранних версий).</span><span class="sxs-lookup"><span data-stu-id="5fc6e-121">In hello **Configuration** tab, un-check **Enable Diagnostics** toodisable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="5fc6e-122">Построение tooverify вашего решения, у вас нет ошибок.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-122">Build your solution tooverify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="5fc6e-123">Шаг 2. Инструментирование кода</span><span class="sxs-lookup"><span data-stu-id="5fc6e-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="5fc6e-124">Замените содержимое hello WorkerRole.cs hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-124">Replace hello contents of WorkerRole.cs with hello following code.</span></span> <span data-ttu-id="5fc6e-125">Здравствуйте, класс SampleEventSourceWriter, наследником hello [класса EventSource][EventSource Class], реализует четыре методы ведения журнала: **SendEnums**, **MessageMethod** , **SetOther** и **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-125">hello class SampleEventSourceWriter, inherited from hello [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="5fc6e-126">Здравствуйте, первый параметр toohello **WriteEvent** метод определяет идентификатор hello hello соответствующих событий.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-126">hello first parameter toohello **WriteEvent** method defines hello ID for hello respective event.</span></span> <span data-ttu-id="5fc6e-127">Метод Run Hello реализует бесконечный цикл, который вызывает каждую hello методы ведения журнала, реализованный в hello **SampleEventSourceWriter** класса каждые 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-127">hello Run method implements an infinite loop that calls each of hello logging methods implemented in hello **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums tooint for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through hello loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set hello maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="5fc6e-128">Шаг 3. Развертывание рабочей роли</span><span class="sxs-lookup"><span data-stu-id="5fc6e-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="5fc6e-129">Развертывание tooAzure рабочих ролей из среды Visual Studio, выбрав hello **WadExample** hello обозревателе решений выберите проект **публикации** из hello **построения** меню.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-129">Deploy your worker role tooAzure from within Visual Studio by selecting hello **WadExample** project in hello Solution Explorer then **Publish** from hello **Build** menu.</span></span>
2. <span data-ttu-id="5fc6e-130">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-130">Choose your subscription.</span></span>
3. <span data-ttu-id="5fc6e-131">В hello **параметры публикации Microsoft Azure** диалогового окна выберите **создать...** .</span><span class="sxs-lookup"><span data-stu-id="5fc6e-131">In hello **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="5fc6e-132">В hello **создать облачную службу и учетную запись хранения** диалоговое окно, введите **имя** (например, «WadExample») и выберите регион или территориальная группа.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-132">In hello **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="5fc6e-133">Набор hello **среды** слишком**промежуточной**.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-133">Set hello **Environment** too**Staging**.</span></span>
6. <span data-ttu-id="5fc6e-134">Измените любые другие **Параметры** по необходимости и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="5fc6e-135">После завершения развертывания, убедитесь в hello портал Azure, облачная служба **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-135">After deployment has completed, verify in hello Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-hello-extension"></a><span data-ttu-id="5fc6e-136">Шаг 4: Создание файла конфигурации диагностики и Установка расширения hello</span><span class="sxs-lookup"><span data-stu-id="5fc6e-136">Step 4: Create your Diagnostics configuration file and install hello extension</span></span>
1. <span data-ttu-id="5fc6e-137">Загрузите определение схемы файл открытой конфигурации hello, выполнив следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="5fc6e-137">Download hello public configuration file schema definition by executing hello following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="5fc6e-138">Добавьте файл XML tooyour **WorkerRole1** проект, щелкнув hello **WorkerRole1** проект и выберите **добавить** -> **новый элемент...**</span><span class="sxs-lookup"><span data-stu-id="5fc6e-138">Add an XML file tooyour **WorkerRole1** project by right-clicking on hello **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="5fc6e-139"> -> **Элементы Visual C#** -> **Данные** -> **XML-файл**.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="5fc6e-140">Имя файла hello «WadExample.xml».</span><span class="sxs-lookup"><span data-stu-id="5fc6e-140">Name hello file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="5fc6e-142">Hello WadConfig.xsd свяжите с файлом конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-142">Associate hello WadConfig.xsd with hello configuration file.</span></span> <span data-ttu-id="5fc6e-143">Убедитесь, что окно редактора WadExample.xml hello — активное окно приветствия.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-143">Make sure hello WadExample.xml editor window is hello active window.</span></span> <span data-ttu-id="5fc6e-144">Нажмите клавишу **F4** tooopen hello **свойства** окна.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-144">Press **F4** tooopen hello **Properties** window.</span></span> <span data-ttu-id="5fc6e-145">Нажмите кнопку hello **схемы** свойство в hello **свойства** окна.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-145">Click hello **Schemas** property in hello **Properties** window.</span></span> <span data-ttu-id="5fc6e-146">Нажмите кнопку hello **...**</span><span class="sxs-lookup"><span data-stu-id="5fc6e-146">Click hello **…**</span></span> <span data-ttu-id="5fc6e-147">в hello **схемы** свойство.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-147">in hello **Schemas** property.</span></span> <span data-ttu-id="5fc6e-148">Нажмите кнопку hello **добавить...**</span><span class="sxs-lookup"><span data-stu-id="5fc6e-148">Click hello **Add…**</span></span> <span data-ttu-id="5fc6e-149">кнопки и перейдите toohello расположение, где был сохранен файл XSD hello и выберите hello WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-149">button and navigate toohello location where you saved hello XSD file and select hello file WadConfig.xsd.</span></span> <span data-ttu-id="5fc6e-150">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-150">Click **OK**.</span></span>

4. <span data-ttu-id="5fc6e-151">Замените содержимое файла конфигурации WadExample.xml hello hello на hello следующий XML-код и сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-151">Replace hello contents of hello WadExample.xml configuration file with hello following XML and save hello file.</span></span> <span data-ttu-id="5fc6e-152">Этот файл конфигурации определяет несколько toocollect счетчиков производительности: для загрузки ЦП и использования памяти.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-152">This configuration file defines a couple performance counters toocollect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="5fc6e-153">Затем конфигурация hello определяет четыре события hello соответствующий toohello методы в классе SampleEventSourceWriter hello.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-153">Then hello configuration defines hello four events corresponding toohello methods in hello SampleEventSourceWriter class.</span></span>

```xml
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

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="5fc6e-154">Шаг 5. Установка системы диагностики в рабочей роли</span><span class="sxs-lookup"><span data-stu-id="5fc6e-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="5fc6e-155">Hello командлеты PowerShell для управления системой диагностики для рабочих и веб-роли являются: набор AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension и Remove AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-155">hello PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="5fc6e-156">Откройте Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="5fc6e-157">Выполните сценарий hello tooinstall диагностики в рабочей роли (Замените *StorageAccountKey* с hello ключ учетной записи хранения для вашей учетной записи wadexample и *config_path* с путем hello toohello *WadExample.xml* файла):</span><span class="sxs-lookup"><span data-stu-id="5fc6e-157">Execute hello script tooinstall Diagnostics on your worker role (replace *StorageAccountKey* with hello storage account key for your wadexample storage account and *config_path* with hello path toohello *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="5fc6e-158">Шаг 6. Просмотр данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="5fc6e-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="5fc6e-159">В Visual Studio hello **обозревателя серверов**, учетной записи хранилища wadexample toohello перехода.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-159">In hello Visual Studio **Server Explorer**, navigate toohello wadexample storage account.</span></span> <span data-ttu-id="5fc6e-160">После около пяти минут выполнения hello облачной службы, вы увидите таблицы hello **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** и **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-160">After hello cloud service has been running about five (5) minutes, you should see hello tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="5fc6e-161">Дважды щелкните одну из hello hello таблиц tooview телеметрии, собранных.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-161">Double-click one of hello tables tooview hello telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="5fc6e-163">Схема файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="5fc6e-163">Configuration File Schema</span></span>
<span data-ttu-id="5fc6e-164">файл конфигурации диагностики Hello определяет значения, используемые tooinitialize диагностические параметры конфигурации при запуске агента диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-164">hello Diagnostics configuration file defines values that are used tooinitialize diagnostic configuration settings when hello diagnostics agent starts.</span></span> <span data-ttu-id="5fc6e-165">В разделе hello [последняя ссылка на схему](https://msdn.microsoft.com/library/azure/mt634524.aspx) допустимые значения и примеры.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-165">See hello [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5fc6e-166">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="5fc6e-166">Troubleshooting</span></span>
<span data-ttu-id="5fc6e-167">Если возникли проблемы, см. сведения в статье [Устранение неполадок с помощью системы диагностики Azure](../azure-diagnostics-troubleshooting.md). Это поможет вам устранить распространенные проблемы.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fc6e-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5fc6e-168">Next Steps</span></span>
<span data-ttu-id="5fc6e-169">[Просмотреть список Azure виртуальной машины диагностики статей](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello данные собираются, устранения неполадок или Дополнительные сведения о диагностике в целом.</span><span class="sxs-lookup"><span data-stu-id="5fc6e-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) toochange hello data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
