---
title: "aaaManagement .NET SDK для Azure Stream Analytics | Документы Microsoft"
description: "Приступая к работе с пакетом SDK для .NET для управления Stream Analytics. Узнайте, как tooset Настройка и запуск заданий analytics. Создание проектов, входные и выходные данные, преобразования."
keywords: "SDK .net, API аналитики"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: 507c11938bc5bf2249a2e41f6bcc076db8ead3f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="8ee35-106">Управление .NET SDK: Настройка и запуск задания analytics, выполняемые с помощью hello Azure Stream Analytics API для .NET</span><span class="sxs-lookup"><span data-stu-id="8ee35-106">Management .NET SDK: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="8ee35-107">Узнайте, как tooset вверх и аналитика выполнения задания с помощью hello Stream Analytics API для .NET с помощью hello управления .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="8ee35-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="8ee35-108">Настраивайте проект, создавайте источники входных и выходных данных и преобразования, а также запускайте и останавливайте задания.</span><span class="sxs-lookup"><span data-stu-id="8ee35-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="8ee35-109">Для выполнения заданий аналитики можно осуществлять потоковую передачу данных из хранилища больших двоичных объектов или из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="8ee35-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="8ee35-110">В разделе hello [управления справочную документацию по hello Stream Analytics API для .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="8ee35-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="8ee35-111">Azure Stream Analytics является полностью управляемой службы, обеспечивая обработку событий с низкой задержкой, высокой надежности, масштабируемая и сложных потоковой передаче данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="8ee35-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="8ee35-112">Stream Analytics позволяет клиентам tooset копирование потоковой передачи данных в потоки tooanalyze заданий и их toodrive практически в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="8ee35-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="8ee35-113">Мы обновили с версией пакета SDK .NET Azure Stream Analytics управления v2.x hello образец кода в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8ee35-113">We have updated hello sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="8ee35-114">Пример кода, с помощью hello применяется версия пакета SDK lagecy (1.x), см. в разделе [использовать v1.x hello .NET SDK управления Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="8ee35-114">For sample code using hello uses lagecy (1.x) SDK version, please see [Use hello Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ee35-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8ee35-115">Prerequisites</span></span>
<span data-ttu-id="8ee35-116">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="8ee35-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="8ee35-117">Установленный экземпляр Visual Studio 2017 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8ee35-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="8ee35-118">Скачанный и установленный [пакет SDK для Azure .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8ee35-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="8ee35-119">Создайте группу ресурсов Azure в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="8ee35-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="8ee35-120">Hello ниже приведен пример сценария Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ee35-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="8ee35-121">Дополнительную информацию об Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ee35-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="8ee35-122">Настройка источника входных данных и вывода toouse цели.</span><span class="sxs-lookup"><span data-stu-id="8ee35-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="8ee35-123">Дополнительные инструкции см. в разделе [добавить входные данные](stream-analytics-add-inputs.md) tooset копирование входные данные выборки и [Добавление выходных элементов](stream-analytics-add-outputs.md) tooset копирование пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="8ee35-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="8ee35-124">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="8ee35-124">Set up a project</span></span>
<span data-ttu-id="8ee35-125">toocreate задание analytics используйте hello Stream Analytics API для .NET, сначала настроить проект.</span><span class="sxs-lookup"><span data-stu-id="8ee35-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="8ee35-126">Создайте консольное приложение Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="8ee35-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="8ee35-127">В hello консоль диспетчера пакетов hello выполнения следующих команд пакеты NuGet tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="8ee35-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="8ee35-128">Hello сначала он hello Azure Stream Analytics управления .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="8ee35-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="8ee35-129">Hello второй раз — для проверки подлинности клиента Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee35-129">hello second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="8ee35-130">Добавьте следующее hello **appSettings** файл App.config toohello раздела:</span><span class="sxs-lookup"><span data-stu-id="8ee35-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="8ee35-131">Замените значения **SubscriptionId** и **ActiveDirectoryTenantId** идентификаторами подписки Azure и клиента.</span><span class="sxs-lookup"><span data-stu-id="8ee35-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="8ee35-132">Эти значения можно получить, выполнив следующий командлет Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="8ee35-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="8ee35-133">Добавьте следующие ссылки в CSPROJ-файле hello:</span><span class="sxs-lookup"><span data-stu-id="8ee35-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="8ee35-134">Добавьте следующее hello **с помощью** toohello инструкций исходный файл (Program.cs) в проекте hello:</span><span class="sxs-lookup"><span data-stu-id="8ee35-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="8ee35-135">Добавьте вспомогательный метод проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="8ee35-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="8ee35-136">Создание клиента управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="8ee35-137">Объект **StreamAnalyticsManagementClient** объект позволяет toomanage hello задания и hello задания компонентов, таких как ввода, вывода и преобразования.</span><span class="sxs-lookup"><span data-stu-id="8ee35-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="8ee35-138">Добавить после начала toohello кода hello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="8ee35-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

<span data-ttu-id="8ee35-139">Hello **resourceGroupName** значение переменной должно быть hello совпадает с именем hello hello ресурса группы можно создать или извлечь hello обязательные шаги.</span><span class="sxs-lookup"><span data-stu-id="8ee35-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="8ee35-140">tooautomate hello учетных данных презентации аспектом создания задания ссылаются слишком[проверки подлинности участника службы с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="8ee35-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="8ee35-141">Hello остальных разделах данной статьи предположим, что этот код в начале hello hello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="8ee35-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="8ee35-142">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="8ee35-143">Hello следующий код создает задание Stream Analytics в группе ресурсов hello, которое определено.</span><span class="sxs-lookup"><span data-stu-id="8ee35-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="8ee35-144">Задание toohello ввода, вывода и преобразования будет добавить позже.</span><span class="sxs-lookup"><span data-stu-id="8ee35-144">You will add an input, output, and transformation toohello job later.</span></span>

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="8ee35-145">Создание источника входных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="8ee35-146">Hello следующий код создает Stream Analytics входной источник с типом источника входных данных большого двоичного объекта hello и сериализации CSV.</span><span class="sxs-lookup"><span data-stu-id="8ee35-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="8ee35-147">использовать toocreate входной источник концентратора событий **EventHubStreamInputDataSource** вместо **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="8ee35-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="8ee35-148">Аналогичным образом можно настроить тип сериализации hello hello источник входных данных.</span><span class="sxs-lookup"><span data-stu-id="8ee35-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

<span data-ttu-id="8ee35-149">Источников входных данных из хранилища BLOB-объектов или концентратор событий, связанные tooa конкретного задания.</span><span class="sxs-lookup"><span data-stu-id="8ee35-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="8ee35-150">toouse Здравствуйте того же источника входных данных для разных заданий, необходимо снова вызвать метод hello и указать другое имя задания.</span><span class="sxs-lookup"><span data-stu-id="8ee35-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="8ee35-151">Тестирование источника входных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="8ee35-152">Hello **TestConnection** тесты метод ли задание Stream Analytics hello может tooconnect toohello поступает источника, а также другие аспекты конкретных toohello входной тип источника.</span><span class="sxs-lookup"><span data-stu-id="8ee35-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="8ee35-153">Например в hello BLOB-объект источника входных данных, созданный на предыдущем шаге, метод hello проверка, имя учетной записи хранения hello и пары ключей может быть toohello tooconnect используется учетная запись хранения а также проверка наличия указанного контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="8ee35-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="8ee35-154">Создание назначения выходных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="8ee35-155">Создание целевого объекта выходных данных — это очень похоже toocreating источника входных данных Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="8ee35-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="8ee35-156">Как и источников входных данных выходные данные целевых объектов, связанные tooa конкретного задания.</span><span class="sxs-lookup"><span data-stu-id="8ee35-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="8ee35-157">toouse Здравствуйте того же конечного вывода для разных заданий, необходимо снова вызвать метод hello и указать другое имя задания.</span><span class="sxs-lookup"><span data-stu-id="8ee35-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="8ee35-158">Привет, следующий код создает целевого объекта выходных данных (база данных Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="8ee35-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="8ee35-159">Вы можете настроить hello выходных данных целевого типа данных и/или тип сериализации.</span><span class="sxs-lookup"><span data-stu-id="8ee35-159">You can customize hello output target's data type and/or serialization type.</span></span>

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="8ee35-160">Тестирование назначения выходных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="8ee35-161">Выходные данные целевого объекта Stream Analytics также имеет hello **TestConnection** метод проверки подключения.</span><span class="sxs-lookup"><span data-stu-id="8ee35-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="8ee35-162">Создание преобразования Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="8ee35-163">Hello следующий код создает Stream Analytics преобразование с запросом hello» выберите * из входных данных» и указывает один модуль потоковой передачи tooallocate для задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="8ee35-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="8ee35-164">Дополнительные сведения о настройке единиц потоковой передачи см. в статье [Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="8ee35-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="8ee35-165">Как ввод и вывод преобразования также содержит связанные toohello конкретном задании Stream Analytics она была создана в разделе.</span><span class="sxs-lookup"><span data-stu-id="8ee35-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="8ee35-166">Запуск задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="8ee35-167">После создания задания Stream Analytics и ее входными данными, выходов и преобразование, можно запустить задание hello, вызывающему Привет **запустить** метод.</span><span class="sxs-lookup"><span data-stu-id="8ee35-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="8ee35-168">Следующий пример кода Hello запускает задание Stream Analytics с пользовательский вывод начала времени набор tooDecember 12, 2012 г., 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="8ee35-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="8ee35-169">Остановка задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="8ee35-170">Можно остановить работающее задание Stream Analytics, вызывающему Привет **остановить** метод.</span><span class="sxs-lookup"><span data-stu-id="8ee35-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="8ee35-171">Удаление задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="8ee35-172">Hello **удалить** метода приведет к удалению hello задания, а также базовый вложенных ресурсов, включая входными данными, выходов и преобразование hello задания hello.</span><span class="sxs-lookup"><span data-stu-id="8ee35-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="8ee35-173">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="8ee35-173">Get support</span></span>
<span data-ttu-id="8ee35-174">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="8ee35-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ee35-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8ee35-175">Next steps</span></span>
<span data-ttu-id="8ee35-176">Вы узнали основы использования toocreate .NET SDK hello и запуска заданий analytics.</span><span class="sxs-lookup"><span data-stu-id="8ee35-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="8ee35-177">toolearn более, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="8ee35-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="8ee35-178">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="8ee35-179">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="8ee35-180">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="8ee35-181">[Использование пакета SDK для .NET для управления Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn889315.aspx)</span><span class="sxs-lookup"><span data-stu-id="8ee35-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="8ee35-182">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="8ee35-183">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="8ee35-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
