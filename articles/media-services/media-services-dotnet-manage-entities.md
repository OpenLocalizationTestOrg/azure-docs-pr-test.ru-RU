---
title: "Активы aaaManaging и связанных сущностей с помощью пакета SDK .NET служб мультимедиа"
description: "Узнайте, как активы toomanage и связанных сущностей с hello пакета SDK служб мультимедиа для .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Управление активами и связанными сущностями с помощью пакета SDK служб мультимедиа для .NET
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

В этом разделе показано, как toomanage служб мультимедиа Azure для сущностей в .NET Framework. 

>[!NOTE]
> Начиная с 1 апреля 2017 г., записи любого задания в вашей учетной записи старше 90 дней автоматически удаляется, а также связанные с ней записи задачи, даже если hello общее количество записей ниже максимальная квота hello. Например, 1 апреля 2017 г. будет автоматически удалена любая запись задания в вашей учетной записи, созданная ранее 31 декабря 2016 г. Если вам нужна информация задания или задачи tooarchive hello, можно использовать код hello, описанные в этом разделе.

## <a name="prerequisites"></a>Предварительные требования

Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Получение ссылки на актив
Зачастую является tooget существующего средства tooan ссылку в службах мультимедиа. Hello в следующем примере кода показано, как получить ссылку на актив из коллекции средств hello на сервере hello объекта контекста, основании hello активов идентификатор, следующий код в этом примере используется запроса Linq tooget существующий объект IAsset ссылки tooan.

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a>Перечисление всех активов
По мере роста числа hello активов, в хранилище, это полезно toolist активов. Hello в следующем примере кода показано, как tooiterate через hello коллекции средств на hello объекта контекста сервера. С каждым активом пример кода hello записывает некоторые из его свойств значения toohello консоли. Например, каждый актив может содержать множество файлов мультимедиа. пример кода Hello записывает все файлы, связанные с каждым активом.

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a>Получение ссылки на задание

При работе с задачами в коде службы мультимедиа обработки часто требуется tooget ссылки tooan существующего задания, основанные на hello идентификатор, следующий пример кода показывает, как ссылка tooan IJob tooget объекта из коллекции заданий hello.

Вы может tooget ссылку на задание при запуске задания кодирования длительное время и состояние задания toocheck hello в потоке. В таких случаях при возвращении метода hello из потока, необходимо tooretrieve задание tooa обновленную ссылку.

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a>Перечисление заданий и активов
Важная задача — toolist активов со связанным заданием в службах мультимедиа. Hello следующем примере кода показано как toolist каждого объекта IJob и затем для каждого задания отображаются свойства задания hello, все связанные задачи, все входные и выходные активы. в данном примере кода Hello можно использовать для множества других задач. Например если требуется toolist hello выходные активы одного или нескольких заданий кодирования, которые были выполнены ранее, этот код показывает, как tooaccess hello выходные активы. При наличии актива выходной tooan ссылку, вы можете предоставить hello содержимого tooother пользователям или приложениям, загрузив его или передав URL-адреса. 

Дополнительные сведения о вариантах предоставления активов см. в разделе [доставка активов с помощью пакета SDK служб мультимедиа для .NET hello](media-services-deliver-streaming-content.md).

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a>Перечисление всех политик доступа
В службах мультимедиа можно определить политику доступа для актива или его файлов. Политика доступа задает hello разрешения для файла или актива (тип доступа и длительность hello). В коде служб мультимедиа политика доступа обычно определяется путем создания объекта IAccessPolicy и последующей его привязки к существующему активу. Затем создается объект ILocator, который позволяет предоставлять прямой доступ tooassets в службах мультимедиа. проект Visual Studio Hello, поставляемый вместе с этой документацией содержит несколько примеров кода, которые показывают, как toocreate и назначить доступ к tooassets политик и указатели.

Здравствуйте, следуя примере кода показано, как все политики доступа на сервере hello и показывает тип hello разрешений, связанных с каждым toolist. Политики доступа tooview другой удобным способом является toolist все ILocator объекты на сервере hello, а затем для каждого локатора можно перечислить связанную политику доступа, с помощью его свойства AccessPolicy.

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a>Ограничение политик доступа 

>[!NOTE]
> Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy). Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики). 

Например можно создать универсальный набор политик с hello, следующий код, который будет запускаться только один раз в приложении. Файл журнала tooa идентификаторы для последующего использования можно записывать в журнал:

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

Затем можно использовать hello существующие идентификаторы в коде следующим образом:

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a>Перечисление всех указателей
Указатель является URL-адрес tooaccess прямой путь к активу, а также разрешения toohello активов в соответствии с определением hello локатора связанную политику доступа. Каждый актив может содержать коллекцию объектов ILocator, связанную с ним через его свойство Locators. контекст сервера Hello также содержит указатели коллекция, содержащая все указатели.

Hello следующий пример кода перечисляет все локаторы на сервере hello. Для каждого локатора она отображает hello идентификатор для связанных активов hello и политики доступа. Она также отображает hello типа разрешений, Дата окончания срока действия hello и активов toohello hello полный путь.

Обратите внимание, что ресурс tooan путь локатора только базовый URL-адрес toohello ресурс. toocreate tooindividual прямой путь файлы, могут просматривать пользователя или приложения, код должен добавить hello конкретного файлового пути toohello указателя пути. Дополнительные сведения о том, как toodo, см. раздел hello [доставка активов с помощью пакета SDK служб мультимедиа для .NET hello](media-services-deliver-streaming-content.md).

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a>Перечисление больших коллекций сущностей
При запросе сущности, имеется ограничение в 1000 сущностей, возвращаемых одновременно, так как открытые v2 REST ограничивает результаты too1000 результаты запроса. Потребуется toouse Skip и Take при перечисление больших коллекций сущностей. 

Здравствуйте, следующая функция обрабатывает в цикле всех заданий hello в hello, предоставленные учетной записи службы мультимедиа. Службы мультимедиа возвращают 1000 заданий в коллекции заданий. функции Hello делает или пропустить и toomake убедитесь, что это перечисление всех заданий (если у вас есть более чем на 1000 заданий в вашей учетной записи).

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a>Удаление актива
Привет, следующий пример удаляет актив.

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>Удаление задания
toodelete задания, необходимо проверить состояние hello hello задания, как указано в свойстве состояние hello. Можно удалить задания, которые завершены или отменены, в то время как задания, которые находятся в некоторых других состояниях (помещенные в очередь, запланированные или обрабатываемые), необходимо сначала отменить, а затем их можно будет удалить.

Hello примере кода показан метод для удаления задания, который проверяет состояния заданий и удаляет их, если состояние hello будет завершена или отменена. Этот код зависит от hello выше в этом разделе для получения задания tooa ссылка: получение ссылки на задание.

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a>Удаление политики доступа
Hello следующий пример кода показывает, как tooget политику доступа tooan ссылку на основе политики идентификатор, а затем toodelete hello политики.

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

