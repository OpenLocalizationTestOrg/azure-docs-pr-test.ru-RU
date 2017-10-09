---
title: "отслеживание заданий aaaProgrammatically в Stream Analytics | Документы Microsoft"
description: "Узнайте, как tooprogrammatically мониторинг заданий Stream Analytics, созданные с помощью API-интерфейс REST, пакет Azure SDK или PowerShell."
keywords: "монитор .net, монитор заданий, мониторинг приложения"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="5c0d1-104">Создание монитора заданий Stream Analytics программным способом</span><span class="sxs-lookup"><span data-stu-id="5c0d1-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="5c0d1-105">В этой статье показано, как мониторинг tooenable для задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="5c0d1-106">Отслеживание заданий Stream Analytics, созданных с помощью интерфейсов API REST, пакета SDK для Azure и оболочки PowerShell, по умолчанию отключено.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="5c0d1-107">Вы можете вручную включить его в hello портал Azure, перейдите на страницу toohello задания монитора и щелкнув hello включить кнопку или этот процесс можно автоматизировать с помощью инструкции hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="5c0d1-108">Hello данные мониторинга будут отображаться в области метрики hello hello портал Azure для задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c0d1-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c0d1-109">Prerequisites</span></span>

<span data-ttu-id="5c0d1-110">Перед началом этого процесса необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="5c0d1-111">Visual Studio 2017 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="5c0d1-112">Скачанный и установленный [пакет SDK Azure для .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5c0d1-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="5c0d1-113">Задание Stream Analytics, требуется toohave мониторинг включен</span><span class="sxs-lookup"><span data-stu-id="5c0d1-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="5c0d1-114">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="5c0d1-114">Create a project</span></span>

1. <span data-ttu-id="5c0d1-115">Создайте консольное приложение Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="5c0d1-116">В hello консоль диспетчера пакетов hello выполнения следующих команд пакеты NuGet tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="5c0d1-117">Hello сначала он hello Azure Stream Analytics управления .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="5c0d1-118">Hello второй раз — hello Azure SDK монитор, который будет использоваться tooenable наблюдения.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="5c0d1-119">Hello последнего он hello Azure Active Directory клиента, который будет использоваться для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="5c0d1-120">Добавьте следующий файл App.config toohello раздела appSettings hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-120">Add hello following appSettings section toohello App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="5c0d1-121">Замените значения *SubscriptionId* и *ActiveDirectoryTenantId* идентификаторами подписки Azure и клиента.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="5c0d1-122">Эти значения можно получить, выполнив следующий командлет PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="5c0d1-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="5c0d1-123">Добавьте следующее hello с помощью инструкций toohello исходный файл (Program.cs) в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="5c0d1-124">Добавьте вспомогательный метод проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="5c0d1-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="5c0d1-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="5c0d1-126">}</span><span class="sxs-lookup"><span data-stu-id="5c0d1-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="5c0d1-127">Создание клиентов управления</span><span class="sxs-lookup"><span data-stu-id="5c0d1-127">Create management clients</span></span>

<span data-ttu-id="5c0d1-128">Hello следующий код будет настроить необходимые переменные hello и управления клиентами.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-128">hello following code will set up hello necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="5c0d1-129">Включение отслеживания существующего задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5c0d1-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="5c0d1-130">Hello следующий код включает наблюдение для **существующие** задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="5c0d1-131">Первая часть кода hello Hello выполняет запрос GET для hello Stream Analytics службы tooretrieve сведения о конкретном задании Stream Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="5c0d1-132">Она использует hello *идентификатор* свойство (извлечены из запроса на получение hello) в качестве параметра для метода Put в hello hello вторая часть кода hello, который отправляет запрос PUT toohello аналитики службы tooenable наблюдение за hello Stream Analytics задание.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="5c0d1-133">Если было включено наблюдение за другое задание Stream Analytics, помощи hello портал Azure или программным способом через hello ниже кода, **рекомендуется предоставлять hello же имя учетной записи хранилища, используемый при вы ранее включен мониторинг.**</span><span class="sxs-lookup"><span data-stu-id="5c0d1-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="5c0d1-134">Учетная запись хранения Hello — область связанного toohello, создать задание Stream Analytics, в частности не само задание toohello.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="5c0d1-135">Stream Analytics, все задания (и все ресурсы Azure) в этом же регионе совместно используют этот toostore учетной записи хранилища, наблюдение за данными.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="5c0d1-136">Если указать другую учетную запись хранения, она может привести к непредвиденные побочные эффекты hello мониторинг заданий Stream Analytics или другим ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="5c0d1-137">используется tooreplace имя учетной записи хранения Hello `<YOUR STORAGE ACCOUNT NAME>` hello, следующий код должен быть учетную запись хранилища в hello той же подписке, hello задания Stream Analytics, назначенный для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="5c0d1-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="5c0d1-138">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="5c0d1-138">Get support</span></span>

<span data-ttu-id="5c0d1-139">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="5c0d1-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c0d1-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c0d1-140">Next steps</span></span>

* [<span data-ttu-id="5c0d1-141">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5c0d1-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5c0d1-142">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5c0d1-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5c0d1-143">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5c0d1-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5c0d1-144">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5c0d1-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5c0d1-145">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5c0d1-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

