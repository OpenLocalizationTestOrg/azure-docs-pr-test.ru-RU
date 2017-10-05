---
title: "Управление активами и связанными сущностями с помощью пакета SDK служб мультимедиа для .NET"
description: "Описание способов управления активами и связанными сущностями с помощью пакета SDK служб мультимедиа для .NET."
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
ms.openlocfilehash: 5efe16a09808267d0797521f9e1df2b60aec9cbb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="0d5a2-103">Управление активами и связанными сущностями с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="0d5a2-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d5a2-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0d5a2-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="0d5a2-105">REST</span><span class="sxs-lookup"><span data-stu-id="0d5a2-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="0d5a2-106">В этой статье показано, как управлять сущностями служб мультимедиа с помощью .NET.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-106">This topic shows how to manage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="0d5a2-107">Начиная с 1 апреля 2017 г. все записи задания в вашей учетной записи и связанные с ней записи задач старше 90 дней будут автоматически удалены, даже если общее число записей не превышает значение максимальной квоты.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="0d5a2-108">Например, 1 апреля 2017 г. будет автоматически удалена любая запись задания в вашей учетной записи, созданная ранее 31 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="0d5a2-109">Если необходимо архивировать данные задания или задачи, то можно использовать код, описанный в этой статье.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-109">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d5a2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0d5a2-110">Prerequisites</span></span>

<span data-ttu-id="0d5a2-111">Настройте среду разработки и укажите в файле app.config сведения о подключении, как описано в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0d5a2-111">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="0d5a2-112">Получение ссылки на актив</span><span class="sxs-lookup"><span data-stu-id="0d5a2-112">Get an Asset Reference</span></span>
<span data-ttu-id="0d5a2-113">Распространенной задачей является получение ссылки на существующий актив в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-113">A frequent task is to get a reference to an existing asset in Media Services.</span></span> <span data-ttu-id="0d5a2-114">В следующем примере кода показано, как можно получить ссылку на актив (Assets) из коллекции активов в объекте контекста сервера, указав идентификатор (Id) актива. В следующем примере кода используется запрос Linq для получения ссылки на существующий объект IAsset.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-114">The following code example shows how you can get an asset reference from the Assets collection on the server context object, based on an asset Id. The following code example uses a Linq query to get a reference to an existing IAsset object.</span></span>

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query to get an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference the asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a><span data-ttu-id="0d5a2-115">Перечисление всех активов</span><span class="sxs-lookup"><span data-stu-id="0d5a2-115">List All Assets</span></span>
<span data-ttu-id="0d5a2-116">По мере роста числа активов в хранилище полезно получать список всех активов.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-116">As the number of assets you have in storage grows, it is helpful to list your assets.</span></span> <span data-ttu-id="0d5a2-117">В следующем примере кода показано, как обойти всю коллекцию активов (Assets) в объекте контекста сервера.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-117">The following code example shows how to iterate through the Assets collection on the server context object.</span></span> <span data-ttu-id="0d5a2-118">С каждым активом пример также записывает некоторые значения его свойств в консоль.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-118">With each asset, the code example also writes some of its property values to the console.</span></span> <span data-ttu-id="0d5a2-119">Например, каждый актив может содержать множество файлов мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="0d5a2-120">Пример кода записывает все файлы, связанные с каждым активом.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-120">The code example writes out all files associated with each asset.</span></span>

    static void ListAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display the collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display the files associated with each asset. 
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

## <a name="get-a-job-reference"></a><span data-ttu-id="0d5a2-121">Получение ссылки на задание</span><span class="sxs-lookup"><span data-stu-id="0d5a2-121">Get a Job Reference</span></span>

<span data-ttu-id="0d5a2-122">При работе с задачами обработки в коде служб мультимедиа часто требуется получить ссылку на существующее задание по идентификатору. В следующем примере кода показано, как получить ссылку на объект IJob из коллекции заданий (Jobs).</span><span class="sxs-lookup"><span data-stu-id="0d5a2-122">When you work with processing tasks in Media Services code, you often need to get a reference to an existing job based on an Id. The following code example shows how to get a reference to an IJob object from the Jobs collection.</span></span>

<span data-ttu-id="0d5a2-123">Получение ссылки на задание может потребоваться при запуске длительного задания кодирования, когда необходимо проверять состояние задания в программном потоке.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-123">You may need to get a job reference when starting a long-running encoding job, and need to check the job status on a thread.</span></span> <span data-ttu-id="0d5a2-124">В таких случаях при возвращении метода из потока требуется получить обновленную ссылку на задание.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-124">In cases like this, when the method returns from a thread, you need to retrieve a refreshed reference to a job.</span></span>

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query to get an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return the job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a><span data-ttu-id="0d5a2-125">Перечисление заданий и активов</span><span class="sxs-lookup"><span data-stu-id="0d5a2-125">List Jobs and Assets</span></span>
<span data-ttu-id="0d5a2-126">Важная связанная задача — перечисление активов с заданиями, с которыми они связаны, в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-126">An important related task is to list assets with their associated job in Media Services.</span></span> <span data-ttu-id="0d5a2-127">В следующем примере кода показано, как перечислить каждый объект IJob, а затем для каждого задания отображаются свойства задания, все связанные задачи, все входные активы и все выходные активы.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-127">The following code example shows you how to list each IJob object, and then for each job, it displays properties about the job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="0d5a2-128">Данный пример кода может быть полезен для множества других задач.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-128">The code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="0d5a2-129">Например, если требуется перечислить выходные активы из одного или нескольких заданий кодирования, которые выполнялись ранее, данный код показывает, как получить доступ к этим выходным активам.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-129">For example, if you want to list the output assets from one or more encoding jobs that you ran previously, this code shows how to access the output assets.</span></span> <span data-ttu-id="0d5a2-130">При наличии ссылки на выходной актив можно затем доставлять содержимое другим пользователям или приложениям путем загрузки или передачи URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-130">When you have a reference to an output asset, you can then deliver the content to other users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="0d5a2-131">Дополнительные сведения о вариантах доставки ресурсов-контейнеров см. в статье [Доставка ресурсов-контейнеров с помощью пакета SDK служб мультимедиа для .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="0d5a2-131">For more information on options for delivering assets, see [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

    // List all jobs on the server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building the list. This may take a few "
            + "seconds to a few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder to store the list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display the collection of jobs on the server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display the associated tasks (a job  
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

            // For each job, display the list of input media assets.
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

            // For each job, display the list of output media assets.
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

## <a name="list-all-access-policies"></a><span data-ttu-id="0d5a2-132">Перечисление всех политик доступа</span><span class="sxs-lookup"><span data-stu-id="0d5a2-132">List all Access Policies</span></span>
<span data-ttu-id="0d5a2-133">В службах мультимедиа можно определить политику доступа для актива или его файлов.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="0d5a2-134">Политика доступа определяет разрешения для файла или актива (тип доступа и продолжительность).</span><span class="sxs-lookup"><span data-stu-id="0d5a2-134">An access policy defines the permissions for a file or an asset (what type of access, and the duration).</span></span> <span data-ttu-id="0d5a2-135">В коде служб мультимедиа политика доступа обычно определяется путем создания объекта IAccessPolicy и последующей его привязки к существующему активу.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="0d5a2-136">Затем создается объект ILocator, который позволяет предоставлять прямой доступ к активам в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-136">Then you create a ILocator object, which lets you provide direct access to assets in Media Services.</span></span> <span data-ttu-id="0d5a2-137">Проект Visual Studio, прилагаемый к этой документации, содержит несколько примеров кода, которые показывают, как создавать и назначать политики доступа и указатели на активы.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-137">The Visual Studio project that accompanies this documentation series contains several code examples that show how to create and assign access policies and locators to assets.</span></span>

<span data-ttu-id="0d5a2-138">В следующем примере кода показано, как перечислить все политики доступа на сервере, а также показаны связанные с каждой из них типы разрешений.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-138">The following code example shows how to list all access policies on the server, and shows the type of permissions associated with each.</span></span> <span data-ttu-id="0d5a2-139">Другой полезный способ просмотра политик доступа — получить список всех объектов ILocator на сервере, а затем для каждого указателя можно перечислить связанную политику доступа с помощью его свойства AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-139">Another useful way to view access policies is to list all ILocator objects on the server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="0d5a2-140">Ограничение политик доступа</span><span class="sxs-lookup"><span data-stu-id="0d5a2-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="0d5a2-141">Действует ограничение в 1 000 000 записей для разных политик AMS (например, для политики Locator или ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0d5a2-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0d5a2-142">Следует указывать один и тот же идентификатор политики, если вы используете те же дни, разрешения доступа и т. д. Например, политики для указателей, которые должны оставаться на месте в течение длительного времени (не политики передачи).</span><span class="sxs-lookup"><span data-stu-id="0d5a2-142">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="0d5a2-143">Например, вы можете создать универсальный набор политик, используя следующий код, который будет выполняться в приложении только один раз.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-143">For example, you can create a generic set of policies with the following code that would only run one time in your application.</span></span> <span data-ttu-id="0d5a2-144">Идентификаторы можно записать в файл журнала для последующего использования:</span><span class="sxs-lookup"><span data-stu-id="0d5a2-144">You can log IDs to a log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="0d5a2-145">Затем вы можете использовать существующие идентификаторы в своем коде, как показано здесь:</span><span class="sxs-lookup"><span data-stu-id="0d5a2-145">Then, you can use the existing IDs in your code like this:</span></span>

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get the standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get the existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("The locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a><span data-ttu-id="0d5a2-146">Перечисление всех указателей</span><span class="sxs-lookup"><span data-stu-id="0d5a2-146">List All Locators</span></span>
<span data-ttu-id="0d5a2-147">Указатель — это URL-адрес, предоставляющий прямой путь для доступа к активу, а также разрешения для этого актива, определенные связанной с указателем политикой доступа.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-147">A locator is a URL that provides a direct path to access an asset, along with permissions to the asset as defined by the locator's associated access policy.</span></span> <span data-ttu-id="0d5a2-148">Каждый актив может содержать коллекцию объектов ILocator, связанную с ним через его свойство Locators.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="0d5a2-149">Контекст сервера также содержит коллекцию Locators, содержащую все указатели.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-149">The server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="0d5a2-150">В следующем примере кода перечисляются все указатели на сервере.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-150">The following code example lists all locators on the server.</span></span> <span data-ttu-id="0d5a2-151">Для каждого указателя отображается идентификатор (Id) связанного актива и политики доступа.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-151">For each locator, it shows the Id for the related asset and access policy.</span></span> <span data-ttu-id="0d5a2-152">Также отображаются тип разрешений, дата окончания срока действия и полный путь к активу.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-152">It also displays the type of permissions, the expiration date, and the full path to the asset.</span></span>

<span data-ttu-id="0d5a2-153">Обратите внимание, что путь указателя к активу представляет собой только базовый URL-адрес актива.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-153">Note that a locator path to an asset is only a base URL to the asset.</span></span> <span data-ttu-id="0d5a2-154">Чтобы создать прямой путь к отдельным файлам, которые может просматривать пользователь или приложения, в коде необходимо добавить к пути указателя конкретный файловый путь.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-154">To create a direct path to individual files that a user or application could browse to, your code must add the specific file path to the locator path.</span></span> <span data-ttu-id="0d5a2-155">Сведения о том, как это сделать, см. в статье [Доставка ресурсов-контейнеров с помощью пакета SDK служб мультимедиа для .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="0d5a2-155">For more information on how to do this, see the topic [Deliver Assets with the Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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
            // The locator path is the base or parent path (with included permissions) to access  
            // the media content of an asset. To create a full URL to a specific media file, take 
            // the locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="0d5a2-156">Перечисление больших коллекций сущностей</span><span class="sxs-lookup"><span data-stu-id="0d5a2-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="0d5a2-157">При запросе сущностей существует ограничение в 1000 сущностей, возвращаемых за один раз, так как в открытой версии 2 REST количество результатов запросов ограничено 1000.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="0d5a2-158">При перечислении больших коллекций сущностей необходимо использовать предложения "Пропустить" и "Принять".</span><span class="sxs-lookup"><span data-stu-id="0d5a2-158">You need to use Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="0d5a2-159">Следующая функция перебирает все задания для предоставленной учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-159">The following function loops through all the jobs in the provided Media Services Account.</span></span> <span data-ttu-id="0d5a2-160">Службы мультимедиа возвращают 1000 заданий в коллекции заданий.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="0d5a2-161">Эта функция использует предложения "Пропустить" и "Принять", чтобы убедиться в том, что все задания перечислены (при наличии более 1000 заданий в учетной записи).</span><span class="sxs-lookup"><span data-stu-id="0d5a2-161">The function makes use of Skip and Take to make sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in the Media Services account
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

## <a name="delete-an-asset"></a><span data-ttu-id="0d5a2-162">Удаление актива</span><span class="sxs-lookup"><span data-stu-id="0d5a2-162">Delete an Asset</span></span>
<span data-ttu-id="0d5a2-163">В следующем примере удаляется актив.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-163">The following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete the asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted the Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="0d5a2-164">Удаление задания</span><span class="sxs-lookup"><span data-stu-id="0d5a2-164">Delete a Job</span></span>
<span data-ttu-id="0d5a2-165">Чтобы удалить задание, необходимо проверить состояние задания, как указано в свойстве State.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-165">To delete a job, you must check the state of the job as indicated in the State property.</span></span> <span data-ttu-id="0d5a2-166">Можно удалить задания, которые завершены или отменены, в то время как задания, которые находятся в некоторых других состояниях (помещенные в очередь, запланированные или обрабатываемые), необходимо сначала отменить, а затем их можно будет удалить.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="0d5a2-167">В следующем примере кода показан метод удаления задания, проверяющий состояния заданий и удаляющий их при завершенном или отмененном состоянии.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-167">The following code example shows a method for deleting a job by checking job states and then deleting when the state is finished or canceled.</span></span> <span data-ttu-id="0d5a2-168">Этот код зависит от содержащегося выше раздела данной статьи "Получение ссылки на задание".</span><span class="sxs-lookup"><span data-stu-id="0d5a2-168">This code depends on the previous section in this topic for getting a reference to a job: Get a job reference.</span></span>

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
                    // You can also call job.DeleteAsync to do async deletes.
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


## <a name="delete-an-access-policy"></a><span data-ttu-id="0d5a2-169">Удаление политики доступа</span><span class="sxs-lookup"><span data-stu-id="0d5a2-169">Delete an Access Policy</span></span>
<span data-ttu-id="0d5a2-170">В следующем примере кода показано, как получить ссылку на политику доступа на основе идентификатора (Id) политики, а затем удалить эту политику.</span><span class="sxs-lookup"><span data-stu-id="0d5a2-170">The following code example shows how to get a reference to an access policy based on a policy Id, and then to delete the policy.</span></span>

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // To delete a specific access policy, get a reference to the policy.  
        // based on the policy Id passed to the method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="0d5a2-171">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="0d5a2-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0d5a2-172">Отзывы</span><span class="sxs-lookup"><span data-stu-id="0d5a2-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

