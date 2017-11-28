---
title: "Управление SDK для .NET для Azure Stream Analytics | Документация Майкрософт"
description: "Приступая к работе с пакетом SDK для .NET для управления Stream Analytics. Узнайте, как настраивать и выполнять задания аналитики. Создание проектов, входные и выходные данные, преобразования."
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
ms.openlocfilehash: f9aa812e6e82cc0f72d0cd1fe63058e53f794775
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="502dc-106">Управление SDK для .NET: настройка и запуск заданий аналитики с помощью API Azure Stream Analytics для .NET.</span><span class="sxs-lookup"><span data-stu-id="502dc-106">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="502dc-107">Узнайте, как настраивать и запускать задания аналитики с помощью API Azure Stream Analytics для .NET, используя управление SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="502dc-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="502dc-108">Настраивайте проект, создавайте источники входных и выходных данных и преобразования, а также запускайте и останавливайте задания.</span><span class="sxs-lookup"><span data-stu-id="502dc-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="502dc-109">Для выполнения заданий аналитики можно осуществлять потоковую передачу данных из хранилища больших двоичных объектов или из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="502dc-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="502dc-110">См. [справочную документацию по управлению API Stream Analytics для .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="502dc-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="502dc-111">Azure Stream Analytics является полностью управляемой службой, обеспечивающей низкую задержку и высокий уровень доступности, масштабируемую обработку сложных событий посредством потоковой передачи данных в облако.</span><span class="sxs-lookup"><span data-stu-id="502dc-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="502dc-112">Stream Analytics дает клиентам возможность настраивать задания потоковой передачи данных для анализа потоков данных и выполнять их в режиме, близком к режиму реального времени.</span><span class="sxs-lookup"><span data-stu-id="502dc-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="502dc-113">Мы обновили пример кода в этой статье с помощью управления SDK для .NET версии 2.х Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="502dc-113">We have updated the sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="502dc-114">Пример кода с использованием устаревших версий пакета SDK (1.x) см. в статье [Управление SDK для .NET: настройка и запуск заданий аналитики с помощью API Azure Stream Analytics для .NET](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="502dc-114">For sample code using the uses lagecy (1.x) SDK version, please see [Use the Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="502dc-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="502dc-115">Prerequisites</span></span>
<span data-ttu-id="502dc-116">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="502dc-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="502dc-117">Установленный экземпляр Visual Studio 2017 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="502dc-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="502dc-118">Скачанный и установленный [пакет SDK для Azure .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="502dc-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="502dc-119">Создайте группу ресурсов Azure в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="502dc-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="502dc-120">Ниже приведен пример сценария Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="502dc-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="502dc-121">Дополнительную информацию об Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="502dc-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="502dc-122">Задайте источник входных данных и назначение выходных данных.</span><span class="sxs-lookup"><span data-stu-id="502dc-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="502dc-123">Дальнейшие указания по настройке примера входных данных см. в статье [Подключение потоковой передачи входных или ссылочных данных к заданию Stream Analytics](stream-analytics-add-inputs.md), а по настройке примера выходных данных — в статье [Настройка выходов данных для заданий Stream Analytics](stream-analytics-add-outputs.md).</span><span class="sxs-lookup"><span data-stu-id="502dc-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="502dc-124">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="502dc-124">Set up a project</span></span>
<span data-ttu-id="502dc-125">Чтобы создать задание аналитики с использованием API Stream Analytics для .NET, сначала настройте проект.</span><span class="sxs-lookup"><span data-stu-id="502dc-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="502dc-126">Создайте консольное приложение Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="502dc-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="502dc-127">В консоли диспетчера пакетов выполните следующие команды, чтобы установить пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="502dc-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="502dc-128">Первый — пакет SDK для .NET для управления Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="502dc-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="502dc-129">Второй — для проверки подлинности клиента Azure.</span><span class="sxs-lookup"><span data-stu-id="502dc-129">The second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="502dc-130">Добавьте следующий раздел **appSettings** в файл App.config:</span><span class="sxs-lookup"><span data-stu-id="502dc-130">Add the following **appSettings** section to the App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="502dc-131">Замените значения **SubscriptionId** и **ActiveDirectoryTenantId** идентификаторами подписки Azure и клиента.</span><span class="sxs-lookup"><span data-stu-id="502dc-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="502dc-132">Вы можете получить эти значения, запустив следующий командлет Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="502dc-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="502dc-133">Добавьте следующую ссылку в CSPROJ-файле:</span><span class="sxs-lookup"><span data-stu-id="502dc-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="502dc-134">Добавьте следующие операторы **using** в файл исходного кода (Program.cs) в проекте:</span><span class="sxs-lookup"><span data-stu-id="502dc-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="502dc-135">Добавьте вспомогательный метод проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="502dc-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="502dc-136">Создание клиента управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="502dc-137">Объект **StreamAnalyticsManagementClient** позволяет управлять заданием и его компонентами, такими как входные и выходные данные, а также преобразованием.</span><span class="sxs-lookup"><span data-stu-id="502dc-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="502dc-138">Добавьте следующий код в начало метода **Main** :</span><span class="sxs-lookup"><span data-stu-id="502dc-138">Add the following code to the beginning of the **Main** method:</span></span>

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

<span data-ttu-id="502dc-139">Значение переменной **resourceGroupName** должно быть таким же, как имя группы ресурсов, созданной или выбранной на предварительных шагах.</span><span class="sxs-lookup"><span data-stu-id="502dc-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="502dc-140">Инструкции по автоматизации этапа создания задач, связанного с представлением учетных данных, см. в статье [Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="502dc-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="502dc-141">В дальнейших разделах этой статьи предполагается, что этот код находится в начале метода **Main** .</span><span class="sxs-lookup"><span data-stu-id="502dc-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="502dc-142">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="502dc-143">Следующий код создает задание Stream Analytics в группе ресурсов, которую вы определили.</span><span class="sxs-lookup"><span data-stu-id="502dc-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="502dc-144">Вы добавите входные и выходные данные, а также преобразование в задание позже.</span><span class="sxs-lookup"><span data-stu-id="502dc-144">You will add an input, output, and transformation to the job later.</span></span>

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

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="502dc-145">Создание источника входных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="502dc-146">Следующий код создает источник входных данных Stream Analytics с типом источника входных данных BLOB-объекта и сериализацией CSV.</span><span class="sxs-lookup"><span data-stu-id="502dc-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="502dc-147">Чтобы создать источник входных данных концентратора событий, используйте **EventHubStreamInputDataSource** вместо **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="502dc-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="502dc-148">Аналогично можно настроить тип сериализации источника входных данных.</span><span class="sxs-lookup"><span data-stu-id="502dc-148">Similarly, you can customize the serialization type of the input source.</span></span>

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

<span data-ttu-id="502dc-149">Источники входных данных из хранилища больших двоичных объектов или из концентратора событий привязываются к определенному заданию.</span><span class="sxs-lookup"><span data-stu-id="502dc-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="502dc-150">Чтобы использовать один источник для разных заданий, потребуется снова вызвать метод и указать другое имя задания.</span><span class="sxs-lookup"><span data-stu-id="502dc-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="502dc-151">Тестирование источника входных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="502dc-152">Метод **TestConnection** тестирует, может ли задание Stream Analytics подключиться к источнику входных данных, а также другие аспекты, относящиеся к этому типу источника входных данных.</span><span class="sxs-lookup"><span data-stu-id="502dc-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="502dc-153">Например, в источнике входных данных BLOB-объекта, созданном на более раннем шаге, метод проверит, может ли пара имени и ключа учетной записи хранения использоваться для подключения к учетной записи хранения, а также убедится, что указанный контекст существует.</span><span class="sxs-lookup"><span data-stu-id="502dc-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

   ```
   // Test the connection to the input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="502dc-154">Создание назначения выходных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="502dc-155">Создание назначения выходных данных аналогично созданию источника входных данных Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="502dc-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="502dc-156">Как и источники входных данных, назначения выходных данных привязываются к определенному заданию.</span><span class="sxs-lookup"><span data-stu-id="502dc-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="502dc-157">Чтобы использовать одно назначение выходных данных для разных заданий, потребуется повторно вызвать метод и указать другое имя задания.</span><span class="sxs-lookup"><span data-stu-id="502dc-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="502dc-158">Следующий код создает назначение выходных данных (базу данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="502dc-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="502dc-159">Вы можете настроить тип данных и тип сериализации назначения выходных данных.</span><span class="sxs-lookup"><span data-stu-id="502dc-159">You can customize the output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="502dc-160">Тестирование назначения выходных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="502dc-161">Назначение выходных данных Stream Analytics также содержит метод **TestConnection** для тестирования подключений.</span><span class="sxs-lookup"><span data-stu-id="502dc-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

   ```
   // Test the connection to the output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="502dc-162">Создание преобразования Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="502dc-163">Следующий код создает преобразование Stream Analytics с запросом select * from Input и задает выделение одной единицы потоковой передачи для задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="502dc-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="502dc-164">Дополнительные сведения о настройке единиц потоковой передачи см. в статье [Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="502dc-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with the value you put for the 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="502dc-165">Как и входные и выходные данные, преобразования также привязываются к определенному заданию Stream Analytics, в котором они были созданы.</span><span class="sxs-lookup"><span data-stu-id="502dc-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="502dc-166">Запуск задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="502dc-167">После создания задания Stream Analytics и его входных и выходных данных, а также преобразований, можно запустить задание, вызвав метод **Start** .</span><span class="sxs-lookup"><span data-stu-id="502dc-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="502dc-168">В следующем примере кода запускается задание Stream Analytics с пользовательским временем запуска выходных данных "12 декабря 2012 г., 12:12:12 UTC":</span><span class="sxs-lookup"><span data-stu-id="502dc-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="502dc-169">Остановка задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="502dc-170">Вы можете остановить выполняющееся задание Stream Analytics, вызвав метод **Stop** .</span><span class="sxs-lookup"><span data-stu-id="502dc-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="502dc-171">Удаление задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="502dc-172">Метод **Delete** удалит задание, а также базовые вложенные ресурсы, включая входные данные, выходные данные и преобразование задания.</span><span class="sxs-lookup"><span data-stu-id="502dc-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="502dc-173">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="502dc-173">Get support</span></span>
<span data-ttu-id="502dc-174">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="502dc-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="502dc-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="502dc-175">Next steps</span></span>
<span data-ttu-id="502dc-176">Вы изучили основы использования пакета SDK для .NET для создания и выполнения заданий аналитики.</span><span class="sxs-lookup"><span data-stu-id="502dc-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="502dc-177">См. также:</span><span class="sxs-lookup"><span data-stu-id="502dc-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="502dc-178">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="502dc-179">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="502dc-180">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="502dc-181">[Использование пакета SDK для .NET для управления Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn889315.aspx)</span><span class="sxs-lookup"><span data-stu-id="502dc-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="502dc-182">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="502dc-183">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="502dc-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
