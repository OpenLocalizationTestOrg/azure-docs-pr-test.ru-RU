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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="74775-103">Управление активами и связанными сущностями с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="74775-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74775-104">.NET</span><span class="sxs-lookup"><span data-stu-id="74775-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="74775-105">REST</span><span class="sxs-lookup"><span data-stu-id="74775-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="74775-106">В этом разделе показано, как toomanage служб мультимедиа Azure для сущностей в .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="74775-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="74775-107">Начиная с 1 апреля 2017 г., записи любого задания в вашей учетной записи старше 90 дней автоматически удаляется, а также связанные с ней записи задачи, даже если hello общее количество записей ниже максимальная квота hello.</span><span class="sxs-lookup"><span data-stu-id="74775-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="74775-108">Например, 1 апреля 2017 г. будет автоматически удалена любая запись задания в вашей учетной записи, созданная ранее 31 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="74775-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="74775-109">Если вам нужна информация задания или задачи tooarchive hello, можно использовать код hello, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="74775-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74775-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="74775-110">Prerequisites</span></span>

<span data-ttu-id="74775-111">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="74775-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="74775-112">Получение ссылки на актив</span><span class="sxs-lookup"><span data-stu-id="74775-112">Get an Asset Reference</span></span>
<span data-ttu-id="74775-113">Зачастую является tooget существующего средства tooan ссылку в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="74775-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="74775-114">Hello в следующем примере кода показано, как получить ссылку на актив из коллекции средств hello на сервере hello объекта контекста, основании hello активов идентификатор, следующий код в этом примере используется запроса Linq tooget существующий объект IAsset ссылки tooan.</span><span class="sxs-lookup"><span data-stu-id="74775-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

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

## <a name="list-all-assets"></a><span data-ttu-id="74775-115">Перечисление всех активов</span><span class="sxs-lookup"><span data-stu-id="74775-115">List All Assets</span></span>
<span data-ttu-id="74775-116">По мере роста числа hello активов, в хранилище, это полезно toolist активов.</span><span class="sxs-lookup"><span data-stu-id="74775-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="74775-117">Hello в следующем примере кода показано, как tooiterate через hello коллекции средств на hello объекта контекста сервера.</span><span class="sxs-lookup"><span data-stu-id="74775-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="74775-118">С каждым активом пример кода hello записывает некоторые из его свойств значения toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="74775-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="74775-119">Например, каждый актив может содержать множество файлов мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="74775-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="74775-120">пример кода Hello записывает все файлы, связанные с каждым активом.</span><span class="sxs-lookup"><span data-stu-id="74775-120">hello code example writes out all files associated with each asset.</span></span>

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

## <a name="get-a-job-reference"></a><span data-ttu-id="74775-121">Получение ссылки на задание</span><span class="sxs-lookup"><span data-stu-id="74775-121">Get a Job Reference</span></span>

<span data-ttu-id="74775-122">При работе с задачами в коде службы мультимедиа обработки часто требуется tooget ссылки tooan существующего задания, основанные на hello идентификатор, следующий пример кода показывает, как ссылка tooan IJob tooget объекта из коллекции заданий hello.</span><span class="sxs-lookup"><span data-stu-id="74775-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="74775-123">Вы может tooget ссылку на задание при запуске задания кодирования длительное время и состояние задания toocheck hello в потоке.</span><span class="sxs-lookup"><span data-stu-id="74775-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="74775-124">В таких случаях при возвращении метода hello из потока, необходимо tooretrieve задание tooa обновленную ссылку.</span><span class="sxs-lookup"><span data-stu-id="74775-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

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

## <a name="list-jobs-and-assets"></a><span data-ttu-id="74775-125">Перечисление заданий и активов</span><span class="sxs-lookup"><span data-stu-id="74775-125">List Jobs and Assets</span></span>
<span data-ttu-id="74775-126">Важная задача — toolist активов со связанным заданием в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="74775-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="74775-127">Hello следующем примере кода показано как toolist каждого объекта IJob и затем для каждого задания отображаются свойства задания hello, все связанные задачи, все входные и выходные активы.</span><span class="sxs-lookup"><span data-stu-id="74775-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="74775-128">в данном примере кода Hello можно использовать для множества других задач.</span><span class="sxs-lookup"><span data-stu-id="74775-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="74775-129">Например если требуется toolist hello выходные активы одного или нескольких заданий кодирования, которые были выполнены ранее, этот код показывает, как tooaccess hello выходные активы.</span><span class="sxs-lookup"><span data-stu-id="74775-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="74775-130">При наличии актива выходной tooan ссылку, вы можете предоставить hello содержимого tooother пользователям или приложениям, загрузив его или передав URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="74775-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="74775-131">Дополнительные сведения о вариантах предоставления активов см. в разделе [доставка активов с помощью пакета SDK служб мультимедиа для .NET hello](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="74775-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="list-all-access-policies"></a><span data-ttu-id="74775-132">Перечисление всех политик доступа</span><span class="sxs-lookup"><span data-stu-id="74775-132">List all Access Policies</span></span>
<span data-ttu-id="74775-133">В службах мультимедиа можно определить политику доступа для актива или его файлов.</span><span class="sxs-lookup"><span data-stu-id="74775-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="74775-134">Политика доступа задает hello разрешения для файла или актива (тип доступа и длительность hello).</span><span class="sxs-lookup"><span data-stu-id="74775-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="74775-135">В коде служб мультимедиа политика доступа обычно определяется путем создания объекта IAccessPolicy и последующей его привязки к существующему активу.</span><span class="sxs-lookup"><span data-stu-id="74775-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="74775-136">Затем создается объект ILocator, который позволяет предоставлять прямой доступ tooassets в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="74775-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="74775-137">проект Visual Studio Hello, поставляемый вместе с этой документацией содержит несколько примеров кода, которые показывают, как toocreate и назначить доступ к tooassets политик и указатели.</span><span class="sxs-lookup"><span data-stu-id="74775-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="74775-138">Здравствуйте, следуя примере кода показано, как все политики доступа на сервере hello и показывает тип hello разрешений, связанных с каждым toolist.</span><span class="sxs-lookup"><span data-stu-id="74775-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="74775-139">Политики доступа tooview другой удобным способом является toolist все ILocator объекты на сервере hello, а затем для каждого локатора можно перечислить связанную политику доступа, с помощью его свойства AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="74775-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="74775-140">Ограничение политик доступа</span><span class="sxs-lookup"><span data-stu-id="74775-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="74775-141">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="74775-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="74775-142">Следует использовать hello же идентификатор политики, если вы используете всегда hello же дни / доступа разрешения, например, политики для указатели, которые являются предполагаемого tooremain на месте в течение длительного времени (без передачи политики).</span><span class="sxs-lookup"><span data-stu-id="74775-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="74775-143">Например можно создать универсальный набор политик с hello, следующий код, который будет запускаться только один раз в приложении.</span><span class="sxs-lookup"><span data-stu-id="74775-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="74775-144">Файл журнала tooa идентификаторы для последующего использования можно записывать в журнал:</span><span class="sxs-lookup"><span data-stu-id="74775-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="74775-145">Затем можно использовать hello существующие идентификаторы в коде следующим образом:</span><span class="sxs-lookup"><span data-stu-id="74775-145">Then, you can use hello existing IDs in your code like this:</span></span>

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

## <a name="list-all-locators"></a><span data-ttu-id="74775-146">Перечисление всех указателей</span><span class="sxs-lookup"><span data-stu-id="74775-146">List All Locators</span></span>
<span data-ttu-id="74775-147">Указатель является URL-адрес tooaccess прямой путь к активу, а также разрешения toohello активов в соответствии с определением hello локатора связанную политику доступа.</span><span class="sxs-lookup"><span data-stu-id="74775-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="74775-148">Каждый актив может содержать коллекцию объектов ILocator, связанную с ним через его свойство Locators.</span><span class="sxs-lookup"><span data-stu-id="74775-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="74775-149">контекст сервера Hello также содержит указатели коллекция, содержащая все указатели.</span><span class="sxs-lookup"><span data-stu-id="74775-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="74775-150">Hello следующий пример кода перечисляет все локаторы на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="74775-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="74775-151">Для каждого локатора она отображает hello идентификатор для связанных активов hello и политики доступа.</span><span class="sxs-lookup"><span data-stu-id="74775-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="74775-152">Она также отображает hello типа разрешений, Дата окончания срока действия hello и активов toohello hello полный путь.</span><span class="sxs-lookup"><span data-stu-id="74775-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="74775-153">Обратите внимание, что ресурс tooan путь локатора только базовый URL-адрес toohello ресурс.</span><span class="sxs-lookup"><span data-stu-id="74775-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="74775-154">toocreate tooindividual прямой путь файлы, могут просматривать пользователя или приложения, код должен добавить hello конкретного файлового пути toohello указателя пути.</span><span class="sxs-lookup"><span data-stu-id="74775-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="74775-155">Дополнительные сведения о том, как toodo, см. раздел hello [доставка активов с помощью пакета SDK служб мультимедиа для .NET hello](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="74775-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="74775-156">Перечисление больших коллекций сущностей</span><span class="sxs-lookup"><span data-stu-id="74775-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="74775-157">При запросе сущности, имеется ограничение в 1000 сущностей, возвращаемых одновременно, так как открытые v2 REST ограничивает результаты too1000 результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="74775-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="74775-158">Потребуется toouse Skip и Take при перечисление больших коллекций сущностей.</span><span class="sxs-lookup"><span data-stu-id="74775-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="74775-159">Здравствуйте, следующая функция обрабатывает в цикле всех заданий hello в hello, предоставленные учетной записи службы мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="74775-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="74775-160">Службы мультимедиа возвращают 1000 заданий в коллекции заданий.</span><span class="sxs-lookup"><span data-stu-id="74775-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="74775-161">функции Hello делает или пропустить и toomake убедитесь, что это перечисление всех заданий (если у вас есть более чем на 1000 заданий в вашей учетной записи).</span><span class="sxs-lookup"><span data-stu-id="74775-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

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

## <a name="delete-an-asset"></a><span data-ttu-id="74775-162">Удаление актива</span><span class="sxs-lookup"><span data-stu-id="74775-162">Delete an Asset</span></span>
<span data-ttu-id="74775-163">Привет, следующий пример удаляет актив.</span><span class="sxs-lookup"><span data-stu-id="74775-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="74775-164">Удаление задания</span><span class="sxs-lookup"><span data-stu-id="74775-164">Delete a Job</span></span>
<span data-ttu-id="74775-165">toodelete задания, необходимо проверить состояние hello hello задания, как указано в свойстве состояние hello.</span><span class="sxs-lookup"><span data-stu-id="74775-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="74775-166">Можно удалить задания, которые завершены или отменены, в то время как задания, которые находятся в некоторых других состояниях (помещенные в очередь, запланированные или обрабатываемые), необходимо сначала отменить, а затем их можно будет удалить.</span><span class="sxs-lookup"><span data-stu-id="74775-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="74775-167">Hello примере кода показан метод для удаления задания, который проверяет состояния заданий и удаляет их, если состояние hello будет завершена или отменена.</span><span class="sxs-lookup"><span data-stu-id="74775-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="74775-168">Этот код зависит от hello выше в этом разделе для получения задания tooa ссылка: получение ссылки на задание.</span><span class="sxs-lookup"><span data-stu-id="74775-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

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


## <a name="delete-an-access-policy"></a><span data-ttu-id="74775-169">Удаление политики доступа</span><span class="sxs-lookup"><span data-stu-id="74775-169">Delete an Access Policy</span></span>
<span data-ttu-id="74775-170">Hello следующий пример кода показывает, как tooget политику доступа tooan ссылку на основе политики идентификатор, а затем toodelete hello политики.</span><span class="sxs-lookup"><span data-stu-id="74775-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="74775-171">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="74775-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="74775-172">Отзывы</span><span class="sxs-lookup"><span data-stu-id="74775-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

