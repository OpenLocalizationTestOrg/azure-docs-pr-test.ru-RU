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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Создание монитора заданий Stream Analytics программным способом

В этой статье показано, как мониторинг tooenable для задания Stream Analytics. Отслеживание заданий Stream Analytics, созданных с помощью интерфейсов API REST, пакета SDK для Azure и оболочки PowerShell, по умолчанию отключено. Вы можете вручную включить его в hello портал Azure, перейдите на страницу toohello задания монитора и щелкнув hello включить кнопку или этот процесс можно автоматизировать с помощью инструкции hello в этой статье. Hello данные мониторинга будут отображаться в области метрики hello hello портал Azure для задания Stream Analytics.

## <a name="prerequisites"></a>Предварительные требования

Перед началом этого процесса необходимо иметь следующие hello.

* Visual Studio 2017 или Visual Studio 2015.
* Скачанный и установленный [пакет SDK Azure для .NET](https://azure.microsoft.com/downloads/).
* Задание Stream Analytics, требуется toohave мониторинг включен

## <a name="create-a-project"></a>Создание проекта

1. Создайте консольное приложение Visual Studio C# .NET.
2. В hello консоль диспетчера пакетов hello выполнения следующих команд пакеты NuGet tooinstall hello. Hello сначала он hello Azure Stream Analytics управления .NET SDK. Hello второй раз — hello Azure SDK монитор, который будет использоваться tooenable наблюдения. Hello последнего он hello Azure Active Directory клиента, который будет использоваться для проверки подлинности.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Добавьте следующий файл App.config toohello раздела appSettings hello.
   
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
   Замените значения *SubscriptionId* и *ActiveDirectoryTenantId* идентификаторами подписки Azure и клиента. Эти значения можно получить, выполнив следующий командлет PowerShell hello:
   
   ```
   Get-AzureAccount
   ```
4. Добавьте следующее hello с помощью инструкций toohello исходный файл (Program.cs) в проекте hello.
   
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
5. Добавьте вспомогательный метод проверки подлинности.
   
     public static string GetAuthorizationHeader()
   
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
     }

## <a name="create-management-clients"></a>Создание клиентов управления

Hello следующий код будет настроить необходимые переменные hello и управления клиентами.

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>Включение отслеживания существующего задания Stream Analytics

Hello следующий код включает наблюдение для **существующие** задания Stream Analytics. Первая часть кода hello Hello выполняет запрос GET для hello Stream Analytics службы tooretrieve сведения о конкретном задании Stream Analytics hello. Она использует hello *идентификатор* свойство (извлечены из запроса на получение hello) в качестве параметра для метода Put в hello hello вторая часть кода hello, который отправляет запрос PUT toohello аналитики службы tooenable наблюдение за hello Stream Analytics задание.

>[!WARNING]
>Если было включено наблюдение за другое задание Stream Analytics, помощи hello портал Azure или программным способом через hello ниже кода, **рекомендуется предоставлять hello же имя учетной записи хранилища, используемый при вы ранее включен мониторинг.**
> 
> Учетная запись хранения Hello — область связанного toohello, создать задание Stream Analytics, в частности не само задание toohello.
> 
> Stream Analytics, все задания (и все ресурсы Azure) в этом же регионе совместно используют этот toostore учетной записи хранилища, наблюдение за данными. Если указать другую учетную запись хранения, она может привести к непредвиденные побочные эффекты hello мониторинг заданий Stream Analytics или другим ресурсам Azure.
> 
> используется tooreplace имя учетной записи хранения Hello `<YOUR STORAGE ACCOUNT NAME>` hello, следующий код должен быть учетную запись хранилища в hello той же подписке, hello задания Stream Analytics, назначенный для мониторинга.
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



## <a name="get-support"></a>Получение поддержки

За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия

* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

