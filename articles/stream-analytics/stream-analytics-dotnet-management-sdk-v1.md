---
title: "aaaManagement v1.x .NET SDK для Azure Stream Analytics | Документы Microsoft"
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
ms.openlocfilehash: d205c388880e3d9c2ca5df218f4b68abac8c9780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="9adfb-106">V1.x управления .NET SDK: Настройка и аналитика выполнения заданий, с помощью hello Azure Stream Analytics API для .NET</span><span class="sxs-lookup"><span data-stu-id="9adfb-106">Management .NET SDK v1.x: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="9adfb-107">Узнайте, как tooset вверх и аналитика выполнения задания с помощью hello Stream Analytics API для .NET с помощью hello управления .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9adfb-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="9adfb-108">Настраивайте проект, создавайте источники входных и выходных данных и преобразования, а также запускайте и останавливайте задания.</span><span class="sxs-lookup"><span data-stu-id="9adfb-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="9adfb-109">Для выполнения заданий аналитики можно осуществлять потоковую передачу данных из хранилища больших двоичных объектов или из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="9adfb-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="9adfb-110">В разделе hello [управления справочную документацию по hello Stream Analytics API для .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="9adfb-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="9adfb-111">Azure Stream Analytics является полностью управляемой службы, обеспечивая обработку событий с низкой задержкой, высокой надежности, масштабируемая и сложных потоковой передаче данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="9adfb-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="9adfb-112">Stream Analytics позволяет клиентам tooset копирование потоковой передачи данных в потоки tooanalyze заданий и их toodrive практически в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="9adfb-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="9adfb-113">Пример кода в этой статье по-прежнему использует устаревшую версию (1.х) управления SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="9adfb-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="9adfb-114">Пример кода с помощью hello последняя версия пакета SDK, см. в разделе [используйте hello .NET SDK управления Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span><span class="sxs-lookup"><span data-stu-id="9adfb-114">For sample code using hello up-to-date SDK version, please see [Use hello Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9adfb-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9adfb-115">Prerequisites</span></span>
<span data-ttu-id="9adfb-116">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="9adfb-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="9adfb-117">Установленный экземпляр Visual Studio 2017 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9adfb-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="9adfb-118">Скачанный и установленный [пакет SDK для Azure .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9adfb-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="9adfb-119">Создайте группу ресурсов Azure в своей подписке.</span><span class="sxs-lookup"><span data-stu-id="9adfb-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="9adfb-120">Hello ниже приведен пример сценария Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9adfb-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="9adfb-121">Дополнительную информацию об Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9adfb-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="9adfb-122">Настройка источника входных данных и вывода toouse цели.</span><span class="sxs-lookup"><span data-stu-id="9adfb-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="9adfb-123">Дополнительные инструкции см. в разделе [добавить входные данные](stream-analytics-add-inputs.md) tooset копирование входные данные выборки и [Добавление выходных элементов](stream-analytics-add-outputs.md) tooset копирование пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9adfb-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="9adfb-124">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="9adfb-124">Set up a project</span></span>
<span data-ttu-id="9adfb-125">toocreate задание analytics используйте hello Stream Analytics API для .NET, сначала настроить проект.</span><span class="sxs-lookup"><span data-stu-id="9adfb-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="9adfb-126">Создайте консольное приложение Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="9adfb-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="9adfb-127">В hello консоль диспетчера пакетов hello выполнения следующих команд пакеты NuGet tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="9adfb-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="9adfb-128">Hello сначала он hello Azure Stream Analytics управления .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="9adfb-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="9adfb-129">Hello второй раз — hello Azure Active Directory клиента, который будет использоваться для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9adfb-129">hello second one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="9adfb-130">Добавьте следующее hello **appSettings** файл App.config toohello раздела:</span><span class="sxs-lookup"><span data-stu-id="9adfb-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <!--CSM Prod related values-->
          <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
          <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
          <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
          <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION" />
          <add key="ActiveDirectoryTenantId" value="YOU TENANT ID" />
        </appSettings>

    <span data-ttu-id="9adfb-131">Замените значения **SubscriptionId** и **ActiveDirectoryTenantId** идентификаторами подписки Azure и клиента.</span><span class="sxs-lookup"><span data-stu-id="9adfb-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="9adfb-132">Эти значения можно получить, выполнив следующий командлет Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="9adfb-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="9adfb-133">Добавьте следующие ссылки в CSPROJ-файле hello:</span><span class="sxs-lookup"><span data-stu-id="9adfb-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="9adfb-134">Добавьте следующее hello **с помощью** toohello инструкций исходный файл (Program.cs) в проекте hello:</span><span class="sxs-lookup"><span data-stu-id="9adfb-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="9adfb-135">Добавьте вспомогательный метод проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="9adfb-135">Add an authentication helper method:</span></span>

   ```   
   private static async Task<string> GetAuthorizationHeader()
   {
       var context = new AuthenticationContext(
           ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
           ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);

        AuthenticationResult result = await context.AcquireTokenASync(
           resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
           clientId: ConfigurationManager.AppSettings["AsaClientId"],
           redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
           promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

       throw new InvalidOperationException("Failed tooacquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="9adfb-136">Создание клиента управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="9adfb-137">Объект **StreamAnalyticsManagementClient** объект позволяет toomanage hello задания и hello задания компонентов, таких как ввода, вывода и преобразования.</span><span class="sxs-lookup"><span data-stu-id="9adfb-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="9adfb-138">Добавить после начала toohello кода hello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="9adfb-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";
    string streamAnalyticsInputName = "<YOUR JOB INPUT NAME>";
    string streamAnalyticsOutputName = "<YOUR JOB OUTPUT NAME>";
    string streamAnalyticsTransformationName = "<YOUR JOB TRANSFORMATION NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
        ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);

    // Create Stream Analytics management client
    StreamAnalyticsManagementClient client = new StreamAnalyticsManagementClient(aadTokenCredentials);

<span data-ttu-id="9adfb-139">Hello **resourceGroupName** значение переменной должно быть hello совпадает с именем hello hello ресурса группы можно создать или извлечь hello обязательные шаги.</span><span class="sxs-lookup"><span data-stu-id="9adfb-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="9adfb-140">tooautomate hello учетных данных презентации аспектом создания задания ссылаются слишком[проверки подлинности участника службы с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="9adfb-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="9adfb-141">Hello остальных разделах данной статьи предположим, что этот код в начале hello hello **Main** метод.</span><span class="sxs-lookup"><span data-stu-id="9adfb-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="9adfb-142">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="9adfb-143">Hello следующий код создает задание Stream Analytics в группе ресурсов hello, которое определено.</span><span class="sxs-lookup"><span data-stu-id="9adfb-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="9adfb-144">Задание toohello ввода, вывода и преобразования будет добавить позже.</span><span class="sxs-lookup"><span data-stu-id="9adfb-144">You will add an input, output, and transformation toohello job later.</span></span>

    // Create a Stream Analytics job
    JobCreateOrUpdateParameters jobCreateParameters = new JobCreateOrUpdateParameters()
    {
        Job = new Job()
        {
            Name = streamAnalyticsJobName,
            Location = "<LOCATION>",
            Properties = new JobProperties()
            {
                EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Adjust,
                Sku = new Sku()
                {
                    Name = "Standard"
                }
            }
        }
    };

    JobCreateOrUpdateResponse jobCreateResponse = client.StreamingJobs.CreateOrUpdate(resourceGroupName, jobCreateParameters);


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="9adfb-145">Создание источника входных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="9adfb-146">Hello следующий код создает Stream Analytics входной источник с типом источника входных данных большого двоичного объекта hello и сериализации CSV.</span><span class="sxs-lookup"><span data-stu-id="9adfb-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="9adfb-147">использовать toocreate входной источник концентратора событий **EventHubStreamInputDataSource** вместо **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="9adfb-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="9adfb-148">Аналогичным образом можно настроить тип сериализации hello hello источник входных данных.</span><span class="sxs-lookup"><span data-stu-id="9adfb-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

    // Create a Stream Analytics input source
    InputCreateOrUpdateParameters jobInputCreateParameters = new InputCreateOrUpdateParameters()
    {
        Input = new Input()
        {
            Name = streamAnalyticsInputName,
            Properties = new StreamInputProperties()
            {
                Serialization = new CsvSerialization
                {
                    Properties = new CsvSerializationProperties
                    {
                        Encoding = "UTF8",
                        FieldDelimiter = ","
                    }
                },
                DataSource = new BlobStreamInputDataSource
                {
                    Properties = new BlobStreamInputDataSourceProperties
                    {
                        StorageAccounts = new StorageAccount[]
                        {
                            new StorageAccount()
                            {
                                AccountName = "<YOUR STORAGE ACCOUNT NAME>",
                                AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
                            }
                        },
                        Container = "samples",
                        PathPattern = ""
                    }
                }
            }
        }
    };

    InputCreateOrUpdateResponse inputCreateResponse =
        client.Inputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobInputCreateParameters);

<span data-ttu-id="9adfb-149">Источников входных данных из хранилища BLOB-объектов или концентратор событий, связанные tooa конкретного задания.</span><span class="sxs-lookup"><span data-stu-id="9adfb-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="9adfb-150">toouse Здравствуйте того же источника входных данных для разных заданий, необходимо снова вызвать метод hello и указать другое имя задания.</span><span class="sxs-lookup"><span data-stu-id="9adfb-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="9adfb-151">Тестирование источника входных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="9adfb-152">Hello **TestConnection** тесты метод ли задание Stream Analytics hello может tooconnect toohello поступает источника, а также другие аспекты конкретных toohello входной тип источника.</span><span class="sxs-lookup"><span data-stu-id="9adfb-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="9adfb-153">Например в hello BLOB-объект источника входных данных, созданный на предыдущем шаге, метод hello проверка, имя учетной записи хранения hello и пары ключей может быть toohello tooconnect используется учетная запись хранения а также проверка наличия указанного контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="9adfb-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="9adfb-154">Создание назначения выходных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="9adfb-155">Создание целевого объекта выходных данных — это очень похоже toocreating источника входных данных Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="9adfb-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="9adfb-156">Как и источников входных данных выходные данные целевых объектов, связанные tooa конкретного задания.</span><span class="sxs-lookup"><span data-stu-id="9adfb-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="9adfb-157">toouse Здравствуйте того же конечного вывода для разных заданий, необходимо снова вызвать метод hello и указать другое имя задания.</span><span class="sxs-lookup"><span data-stu-id="9adfb-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="9adfb-158">Привет, следующий код создает целевого объекта выходных данных (база данных Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="9adfb-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="9adfb-159">Вы можете настроить hello выходных данных целевого типа данных и/или тип сериализации.</span><span class="sxs-lookup"><span data-stu-id="9adfb-159">You can customize hello output target's data type and/or serialization type.</span></span>

    // Create a Stream Analytics output target
    OutputCreateOrUpdateParameters jobOutputCreateParameters = new OutputCreateOrUpdateParameters()
    {
        Output = new Output()
        {
            Name = streamAnalyticsOutputName,
            Properties = new OutputProperties()
            {
                DataSource = new SqlAzureOutputDataSource()
                {
                    Properties = new SqlAzureOutputDataSourceProperties()
                    {
                        Server = "<YOUR DATABASE SERVER NAME>",
                        Database = "<YOUR DATABASE NAME>",
                        User = "<YOUR DATABASE LOGIN>",
                        Password = "<YOUR DATABASE LOGIN PASSWORD>",
                        Table = "<YOUR DATABASE TABLE NAME>"
                    }
                }
            }
        }
    };

    OutputCreateOrUpdateResponse outputCreateResponse =
        client.Outputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobOutputCreateParameters);

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="9adfb-160">Тестирование назначения выходных данных Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="9adfb-161">Выходные данные целевого объекта Stream Analytics также имеет hello **TestConnection** метод проверки подключения.</span><span class="sxs-lookup"><span data-stu-id="9adfb-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="9adfb-162">Создание преобразования Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="9adfb-163">Hello следующий код создает Stream Analytics преобразование с запросом hello» выберите * из входных данных» и указывает один модуль потоковой передачи tooallocate для задания Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="9adfb-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="9adfb-164">Дополнительные сведения о настройке единиц потоковой передачи см. в статье [Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="9adfb-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

    // Create a Stream Analytics transformation
    TransformationCreateOrUpdateParameters transformationCreateParameters = new TransformationCreateOrUpdateParameters()
    {
        Transformation = new Transformation()
        {
            Name = streamAnalyticsTransformationName,
            Properties = new TransformationProperties()
            {
                StreamingUnits = 1,
                Query = "select * from Input"
            }
        }
    };

    var transformationCreateResp =
        client.Transformations.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, transformationCreateParameters);

<span data-ttu-id="9adfb-165">Как ввод и вывод преобразования также содержит связанные toohello конкретном задании Stream Analytics она была создана в разделе.</span><span class="sxs-lookup"><span data-stu-id="9adfb-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="9adfb-166">Запуск задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="9adfb-167">После создания задания Stream Analytics и ее входными данными, выходов и преобразование, можно запустить задание hello, вызывающему Привет **запустить** метод.</span><span class="sxs-lookup"><span data-stu-id="9adfb-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="9adfb-168">Следующий пример кода Hello запускает задание Stream Analytics с пользовательский вывод начала времени набор tooDecember 12, 2012 г., 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="9adfb-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="9adfb-169">Остановка задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="9adfb-170">Можно остановить работающее задание Stream Analytics, вызывающему Привет **остановить** метод.</span><span class="sxs-lookup"><span data-stu-id="9adfb-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="9adfb-171">Удаление задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="9adfb-172">Hello **удалить** метода приведет к удалению hello задания, а также базовый вложенных ресурсов, включая входными данными, выходов и преобразование hello задания hello.</span><span class="sxs-lookup"><span data-stu-id="9adfb-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="9adfb-173">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="9adfb-173">Get support</span></span>
<span data-ttu-id="9adfb-174">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="9adfb-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9adfb-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9adfb-175">Next steps</span></span>
<span data-ttu-id="9adfb-176">Вы узнали основы использования toocreate .NET SDK hello и запуска заданий analytics.</span><span class="sxs-lookup"><span data-stu-id="9adfb-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="9adfb-177">toolearn более, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="9adfb-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="9adfb-178">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9adfb-179">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9adfb-180">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="9adfb-181">[Использование пакета SDK для .NET для управления Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn889315.aspx)</span><span class="sxs-lookup"><span data-stu-id="9adfb-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="9adfb-182">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9adfb-183">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9adfb-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
