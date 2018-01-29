---
title: "Управление SDK для .NET для Azure Stream Analytics | Документация Майкрософт"
description: "Приступая к работе с пакетом SDK для .NET для управления Stream Analytics. Узнайте, как настраивать и выполнять задания аналитики. Создание проектов, входные и выходные данные, преобразования."
keywords: "SDK .net, API аналитики"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: samacha
ms.openlocfilehash: 2ac5d305aae110eff46459ecb7d89ca50ae1823d
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a>Управление SDK для .NET: настройка и запуск заданий аналитики с помощью API Azure Stream Analytics для .NET.
Узнайте, как настраивать и запускать задания аналитики с помощью API Azure Stream Analytics для .NET, используя управление SDK для .NET. Настраивайте проект, создавайте источники входных и выходных данных и преобразования, а также запускайте и останавливайте задания. Для выполнения заданий аналитики можно осуществлять потоковую передачу данных из хранилища больших двоичных объектов или из концентратора событий.

См. [справочную документацию по управлению API Stream Analytics для .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Azure Stream Analytics является полностью управляемой службой, обеспечивающей низкую задержку и высокий уровень доступности, масштабируемую обработку сложных событий посредством потоковой передачи данных в облако. Stream Analytics дает клиентам возможность настраивать задания потоковой передачи данных для анализа потоков данных и выполнять их в режиме, близком к режиму реального времени.  

> [!NOTE]
> Мы обновили пример кода в этой статье с помощью управления SDK для .NET версии 2.х Azure Stream Analytics. Пример кода с использованием устаревших версий пакета SDK (1.x) см. в статье [Управление SDK для .NET: настройка и запуск заданий аналитики с помощью API Azure Stream Analytics для .NET](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).

## <a name="prerequisites"></a>Технические условия
Перед началом работы с этой статьей необходимо иметь следующее:

* Установленный экземпляр Visual Studio 2017 или Visual Studio 2015.
* Скачанный и установленный [пакет SDK для Azure .NET](https://azure.microsoft.com/downloads/).
* Создайте группу ресурсов Azure в своей подписке. Ниже приведен пример сценария Azure PowerShell. Дополнительную информацию об Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Задайте источник входных данных и назначение выходных данных. Дальнейшие указания по настройке примера входных данных см. в статье [Подключение потоковой передачи входных или ссылочных данных к заданию Stream Analytics](stream-analytics-add-inputs.md), а по настройке примера выходных данных — в статье [Настройка выходов данных для заданий Stream Analytics](stream-analytics-add-outputs.md).

## <a name="set-up-a-project"></a>Настройка проекта
Чтобы создать задание аналитики с использованием API Stream Analytics для .NET, сначала настройте проект.

1. Создайте консольное приложение Visual Studio C# .NET.
2. В консоли диспетчера пакетов выполните следующие команды, чтобы установить пакеты NuGet. Первый — пакет SDK для .NET для управления Azure Stream Analytics. Второй — для проверки подлинности клиента Azure.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. Добавьте следующий раздел **appSettings** в файл App.config:
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    Замените значения **SubscriptionId** и **ActiveDirectoryTenantId** идентификаторами подписки Azure и клиента. Вы можете получить эти значения, запустив следующий командлет Azure PowerShell:

        Get-AzureAccount

4. Добавьте следующую ссылку в CSPROJ-файле:

        <Reference Include="System.Configuration" />

5. Добавьте следующие операторы **using** в файл исходного кода (Program.cs) в проекте:
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. Добавьте вспомогательный метод проверки подлинности:

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a>Создание клиента управления Stream Analytics
Объект **StreamAnalyticsManagementClient** позволяет управлять заданием и его компонентами, такими как входные и выходные данные, а также преобразованием.

Добавьте следующий код в начало метода **Main** :

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

Значение переменной **resourceGroupName** должно быть таким же, как имя группы ресурсов, созданной или выбранной на предварительных шагах.

Инструкции по автоматизации этапа создания задач, связанного с представлением учетных данных, см. в статье [Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам](../azure-resource-manager/resource-group-authenticate-service-principal.md).

В дальнейших разделах этой статьи предполагается, что этот код находится в начале метода **Main** .

## <a name="create-a-stream-analytics-job"></a>Создание задания Stream Analytics
Следующий код создает задание Stream Analytics в группе ресурсов, которую вы определили. Вы добавите входные и выходные данные, а также преобразование в задание позже.

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

## <a name="create-a-stream-analytics-input-source"></a>Создание источника входных данных Stream Analytics
Следующий код создает источник входных данных Stream Analytics с типом источника входных данных BLOB-объекта и сериализацией CSV. Чтобы создать источник входных данных концентратора событий, используйте **EventHubStreamInputDataSource** вместо **BlobStreamInputDataSource**. Аналогично можно настроить тип сериализации источника входных данных.

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

Источники входных данных из хранилища больших двоичных объектов или из концентратора событий привязываются к определенному заданию. Чтобы использовать один источник для разных заданий, потребуется снова вызвать метод и указать другое имя задания.

## <a name="test-a-stream-analytics-input-source"></a>Тестирование источника входных данных Stream Analytics
Метод **TestConnection** тестирует, может ли задание Stream Analytics подключиться к источнику входных данных, а также другие аспекты, относящиеся к этому типу источника входных данных. Например, в источнике входных данных BLOB-объекта, созданном на более раннем шаге, метод проверит, может ли пара имени и ключа учетной записи хранения использоваться для подключения к учетной записи хранения, а также убедится, что указанный контекст существует.

   ```
   // Test the connection to the input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a>Создание назначения выходных данных Stream Analytics
Создание назначения выходных данных аналогично созданию источника входных данных Stream Analytics. Как и источники входных данных, назначения выходных данных привязываются к определенному заданию. Чтобы использовать одно назначение выходных данных для разных заданий, потребуется повторно вызвать метод и указать другое имя задания.

Следующий код создает назначение выходных данных (базу данных SQL Azure). Вы можете настроить тип данных и тип сериализации назначения выходных данных.

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

## <a name="test-a-stream-analytics-output-target"></a>Тестирование назначения выходных данных Stream Analytics
Назначение выходных данных Stream Analytics также содержит метод **TestConnection** для тестирования подключений.

   ```
   // Test the connection to the output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a>Создание преобразования Stream Analytics
Следующий код создает преобразование Stream Analytics с запросом select * from Input и задает выделение одной единицы потоковой передачи для задания Stream Analytics. Дополнительные сведения о настройке единиц потоковой передачи см. в статье [Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных](stream-analytics-scale-jobs.md).

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with the value you put for the 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

Как и входные и выходные данные, преобразования также привязываются к определенному заданию Stream Analytics, в котором они были созданы.

## <a name="start-a-stream-analytics-job"></a>Запуск задания Stream Analytics
После создания задания Stream Analytics и его входных и выходных данных, а также преобразований, можно запустить задание, вызвав метод **Start** .

В следующем примере кода запускается задание Stream Analytics с пользовательским временем запуска выходных данных "12 декабря 2012 г., 12:12:12 UTC":

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a>Остановка задания Stream Analytics
Вы можете остановить выполняющееся задание Stream Analytics, вызвав метод **Stop** .

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a>Удаление задания Stream Analytics
Метод **Delete** удалит задание, а также базовые вложенные ресурсы, включая входные данные, выходные данные и преобразование задания.

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a>Получение поддержки
За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
Вы изучили основы использования пакета SDK для .NET для создания и выполнения заданий аналитики. См. также:

* [Введение в Azure Stream Analytics](stream-analytics-introduction.md)
* [Приступая к работе с Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Масштабирование заданий в службе Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Использование пакета SDK для .NET для управления Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn889315.aspx)
* [Справочник по языку запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Справочник по API-интерфейсу REST управления Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
