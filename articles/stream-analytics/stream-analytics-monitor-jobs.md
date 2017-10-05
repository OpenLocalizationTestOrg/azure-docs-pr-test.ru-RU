---
title: "Отслеживание заданий Stream Analytics программным способом | Документация Майкрософт"
description: "Узнайте, как отслеживать задания Stream Analytics, созданные с помощью API REST, пакета SDK для Azure или PowerShell."
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
ms.openlocfilehash: 0d39e77316a03a705586af3ba970a7be1208ec85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="7bc69-104">Создание монитора заданий Stream Analytics программным способом</span><span class="sxs-lookup"><span data-stu-id="7bc69-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="7bc69-105">В этой статье рассказывается, как включить функцию отслеживания задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7bc69-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="7bc69-106">Отслеживание заданий Stream Analytics, созданных с помощью интерфейсов API REST, пакета SDK для Azure и оболочки PowerShell, по умолчанию отключено.</span><span class="sxs-lookup"><span data-stu-id="7bc69-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="7bc69-107">Вы можете вручную включить отслеживание на портале Azure. Для этого перейдите на страницу "Отслеживание" задания и нажмите кнопку "Включить". Этот процесс также можно автоматизировать, выполнив описанные в этой статье действия.</span><span class="sxs-lookup"><span data-stu-id="7bc69-107">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="7bc69-108">Данные отслеживания будут отображаться в области метрики на портале Azure для задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7bc69-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bc69-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7bc69-109">Prerequisites</span></span>

<span data-ttu-id="7bc69-110">Перед началом работы необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="7bc69-110">Before you begin this process, you must have the following:</span></span>

* <span data-ttu-id="7bc69-111">Visual Studio 2017 или Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7bc69-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="7bc69-112">Скачанный и установленный [пакет SDK Azure для .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7bc69-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="7bc69-113">Существующее задание Stream Analytics, отслеживание которого нужно включить.</span><span class="sxs-lookup"><span data-stu-id="7bc69-113">An existing Stream Analytics job that needs to have monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="7bc69-114">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="7bc69-114">Create a project</span></span>

1. <span data-ttu-id="7bc69-115">Создайте консольное приложение Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="7bc69-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="7bc69-116">В консоли диспетчера пакетов выполните следующие команды, чтобы установить пакеты NuGet.</span><span class="sxs-lookup"><span data-stu-id="7bc69-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="7bc69-117">Первый — пакет SDK для .NET для управления Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7bc69-117">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="7bc69-118">Второй — пакет SDK для Azure Monitor, который будет использоваться для включения отслеживания.</span><span class="sxs-lookup"><span data-stu-id="7bc69-118">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span></span> <span data-ttu-id="7bc69-119">Последний — клиент Azure Active Directory, который будет использоваться для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7bc69-119">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="7bc69-120">Добавьте следующий раздел appSettings в файл App.config.</span><span class="sxs-lookup"><span data-stu-id="7bc69-120">Add the following appSettings section to the App.config file.</span></span>
   
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
   <span data-ttu-id="7bc69-121">Замените значения *SubscriptionId* и *ActiveDirectoryTenantId* идентификаторами подписки Azure и клиента.</span><span class="sxs-lookup"><span data-stu-id="7bc69-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="7bc69-122">Вы можете получить эти значения, запустив следующий командлет Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7bc69-122">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="7bc69-123">Добавьте следующие инструкции с оператором using в исходный файл (Program.cs) в проекте.</span><span class="sxs-lookup"><span data-stu-id="7bc69-123">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
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
5. <span data-ttu-id="7bc69-124">Добавьте вспомогательный метод проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7bc69-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="7bc69-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="7bc69-125">public static string GetAuthorizationHeader()</span></span>
   
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
   
             throw new InvalidOperationException("Failed to acquire token");
     <span data-ttu-id="7bc69-126">}</span><span class="sxs-lookup"><span data-stu-id="7bc69-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="7bc69-127">Создание клиентов управления</span><span class="sxs-lookup"><span data-stu-id="7bc69-127">Create management clients</span></span>

<span data-ttu-id="7bc69-128">С помощью следующего кода можно настроить необходимые переменные и клиенты управления.</span><span class="sxs-lookup"><span data-stu-id="7bc69-128">The following code will set up the necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="7bc69-129">Включение отслеживания существующего задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7bc69-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="7bc69-130">С помощью следующего кода можно включить отслеживание **имеющегося** задания Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7bc69-130">The following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="7bc69-131">В первой части кода в службу Stream Analytics отправляется запрос GET, что позволяет получить сведения о конкретном задании Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="7bc69-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="7bc69-132">Во второй части кода, где запрос PUT отправляется в службу Insights для включения отслеживания задания Stream Analytics, свойство *Id* (полученное в результате выполнения запроса GET) используется в качестве параметра метода Put.</span><span class="sxs-lookup"><span data-stu-id="7bc69-132">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="7bc69-133">Если ранее вы включили функцию отслеживания для другого задания Stream Analytics либо на портале Azure, либо программным способом с помощью указанного ниже кода, **мы рекомендуем использовать ту же учетную запись хранения, которую вы использовали для включения функции отслеживания.**</span><span class="sxs-lookup"><span data-stu-id="7bc69-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="7bc69-134">Учетная запись хранения связана с регионом, в котором вы создали свое задание Stream Analytics, а не с самим заданием.</span><span class="sxs-lookup"><span data-stu-id="7bc69-134">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="7bc69-135">Все задания Stream Analytics (и все остальные ресурсы Azure) в этом регионе совместно используют эту учетную запись хранения для хранения данных отслеживания.</span><span class="sxs-lookup"><span data-stu-id="7bc69-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="7bc69-136">Если указать другую учетную запись хранения, это может привести к непредвиденным побочным эффектам при отслеживании других заданий Stream Analytics или других ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="7bc69-136">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="7bc69-137">Имя учетной записи хранения, используемой для замены `<YOUR STORAGE ACCOUNT NAME>` в следующем коде, должно представлять собой учетную запись хранения, которая входит в ту же подписку, что и задание Stream Analytics, для которого вы включаете функцию отслеживания.</span><span class="sxs-lookup"><span data-stu-id="7bc69-137">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="7bc69-138">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="7bc69-138">Get support</span></span>

<span data-ttu-id="7bc69-139">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="7bc69-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bc69-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7bc69-140">Next steps</span></span>

* [<span data-ttu-id="7bc69-141">Введение в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7bc69-141">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7bc69-142">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7bc69-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7bc69-143">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7bc69-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7bc69-144">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7bc69-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7bc69-145">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7bc69-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

