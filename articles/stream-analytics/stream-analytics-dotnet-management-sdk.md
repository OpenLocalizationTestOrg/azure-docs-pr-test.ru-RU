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
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>Управление .NET SDK: Настройка и запуск задания analytics, выполняемые с помощью hello Azure Stream Analytics API для .NET
Узнайте, как tooset вверх и аналитика выполнения задания с помощью hello Stream Analytics API для .NET с помощью hello управления .NET SDK. Настраивайте проект, создавайте источники входных и выходных данных и преобразования, а также запускайте и останавливайте задания. Для выполнения заданий аналитики можно осуществлять потоковую передачу данных из хранилища больших двоичных объектов или из концентратора событий.

В разделе hello [управления справочную документацию по hello Stream Analytics API для .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Azure Stream Analytics является полностью управляемой службы, обеспечивая обработку событий с низкой задержкой, высокой надежности, масштабируемая и сложных потоковой передаче данных в облаке hello. Stream Analytics позволяет клиентам tooset копирование потоковой передачи данных в потоки tooanalyze заданий и их toodrive практически в режиме реального времени.  

> [!NOTE]
> Мы обновили с версией пакета SDK .NET Azure Stream Analytics управления v2.x hello образец кода в этой статье. Пример кода, с помощью hello применяется версия пакета SDK lagecy (1.x), см. в разделе [использовать v1.x hello .NET SDK управления Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* Установленный экземпляр Visual Studio 2017 или Visual Studio 2015.
* Скачанный и установленный [пакет SDK для Azure .NET](https://azure.microsoft.com/downloads/).
* Создайте группу ресурсов Azure в своей подписке. Hello ниже приведен пример сценария Azure PowerShell. Дополнительную информацию об Azure PowerShell см. в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Настройка источника входных данных и вывода toouse цели. Дополнительные инструкции см. в разделе [добавить входные данные](stream-analytics-add-inputs.md) tooset копирование входные данные выборки и [Добавление выходных элементов](stream-analytics-add-outputs.md) tooset копирование пример выходных данных.

## <a name="set-up-a-project"></a>Настройка проекта
toocreate задание analytics используйте hello Stream Analytics API для .NET, сначала настроить проект.

1. Создайте консольное приложение Visual Studio C# .NET.
2. В hello консоль диспетчера пакетов hello выполнения следующих команд пакеты NuGet tooinstall hello. Hello сначала он hello Azure Stream Analytics управления .NET SDK. Hello второй раз — для проверки подлинности клиента Azure.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. Добавьте следующее hello **appSettings** файл App.config toohello раздела:
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    Замените значения **SubscriptionId** и **ActiveDirectoryTenantId** идентификаторами подписки Azure и клиента. Эти значения можно получить, выполнив следующий командлет Azure PowerShell hello:

        Get-AzureAccount

4. Добавьте следующие ссылки в CSPROJ-файле hello:

        <Reference Include="System.Configuration" />

5. Добавьте следующее hello **с помощью** toohello инструкций исходный файл (Program.cs) в проекте hello:
   
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
Объект **StreamAnalyticsManagementClient** объект позволяет toomanage hello задания и hello задания компонентов, таких как ввода, вывода и преобразования.

Добавить после начала toohello кода hello hello **Main** метод:

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

Hello **resourceGroupName** значение переменной должно быть hello совпадает с именем hello hello ресурса группы можно создать или извлечь hello обязательные шаги.

tooautomate hello учетных данных презентации аспектом создания задания ссылаются слишком[проверки подлинности участника службы с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Hello остальных разделах данной статьи предположим, что этот код в начале hello hello **Main** метод.

## <a name="create-a-stream-analytics-job"></a>Создание задания Stream Analytics
Hello следующий код создает задание Stream Analytics в группе ресурсов hello, которое определено. Задание toohello ввода, вывода и преобразования будет добавить позже.

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
Hello следующий код создает Stream Analytics входной источник с типом источника входных данных большого двоичного объекта hello и сериализации CSV. использовать toocreate входной источник концентратора событий **EventHubStreamInputDataSource** вместо **BlobStreamInputDataSource**. Аналогичным образом можно настроить тип сериализации hello hello источник входных данных.

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

Источников входных данных из хранилища BLOB-объектов или концентратор событий, связанные tooa конкретного задания. toouse Здравствуйте того же источника входных данных для разных заданий, необходимо снова вызвать метод hello и указать другое имя задания.

## <a name="test-a-stream-analytics-input-source"></a>Тестирование источника входных данных Stream Analytics
Hello **TestConnection** тесты метод ли задание Stream Analytics hello может tooconnect toohello поступает источника, а также другие аспекты конкретных toohello входной тип источника. Например в hello BLOB-объект источника входных данных, созданный на предыдущем шаге, метод hello проверка, имя учетной записи хранения hello и пары ключей может быть toohello tooconnect используется учетная запись хранения а также проверка наличия указанного контейнера hello.

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a>Создание назначения выходных данных Stream Analytics
Создание целевого объекта выходных данных — это очень похоже toocreating источника входных данных Stream Analytics. Как и источников входных данных выходные данные целевых объектов, связанные tooa конкретного задания. toouse Здравствуйте того же конечного вывода для разных заданий, необходимо снова вызвать метод hello и указать другое имя задания.

Привет, следующий код создает целевого объекта выходных данных (база данных Azure SQL). Вы можете настроить hello выходных данных целевого типа данных и/или тип сериализации.

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
Выходные данные целевого объекта Stream Analytics также имеет hello **TestConnection** метод проверки подключения.

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a>Создание преобразования Stream Analytics
Hello следующий код создает Stream Analytics преобразование с запросом hello» выберите * из входных данных» и указывает один модуль потоковой передачи tooallocate для задания Stream Analytics hello. Дополнительные сведения о настройке единиц потоковой передачи см. в статье [Масштабирование заданий Azure Stream Analytics для повышения пропускной способности базы данных](stream-analytics-scale-jobs.md).

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

Как ввод и вывод преобразования также содержит связанные toohello конкретном задании Stream Analytics она была создана в разделе.

## <a name="start-a-stream-analytics-job"></a>Запуск задания Stream Analytics
После создания задания Stream Analytics и ее входными данными, выходов и преобразование, можно запустить задание hello, вызывающему Привет **запустить** метод.

Следующий пример кода Hello запускает задание Stream Analytics с пользовательский вывод начала времени набор tooDecember 12, 2012 г., 12:12:12 UTC:

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
Можно остановить работающее задание Stream Analytics, вызывающему Привет **остановить** метод.

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a>Удаление задания Stream Analytics
Hello **удалить** метода приведет к удалению hello задания, а также базовый вложенных ресурсов, включая входными данными, выходов и преобразование hello задания hello.

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a>Получение поддержки
За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Дальнейшие действия
Вы узнали основы использования toocreate .NET SDK hello и запуска заданий analytics. toolearn более, см. ниже hello:

* [Введение tooAzure Stream Analytics](stream-analytics-introduction.md)
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
