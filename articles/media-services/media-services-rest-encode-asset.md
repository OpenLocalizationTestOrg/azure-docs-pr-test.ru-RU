---
title: "aaaHow tooencode актива Azure с помощью Media Encoder стандартные | Документы Microsoft"
description: "Узнайте, как стандартный кодировщик мультимедиа media tooencode toouse содержимого служб мультимедиа Azure. В примерах кода используется REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="0a23b-104">Как tooencode актива с помощью стандартных кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="0a23b-104">How tooencode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a23b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="0a23b-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="0a23b-106">REST</span><span class="sxs-lookup"><span data-stu-id="0a23b-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="0a23b-107">Портал</span><span class="sxs-lookup"><span data-stu-id="0a23b-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="0a23b-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="0a23b-108">Overview</span></span>
<span data-ttu-id="0a23b-109">toodeliver цифрового видео по Интернету hello, необходимо сжать мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-109">toodeliver digital video over hello Internet, you must compress hello media.</span></span> <span data-ttu-id="0a23b-110">Цифровые видеофайлы велики и может быть слишком большой toodeliver по hello Интернет или для клиентов устройств toodisplay должным образом.</span><span class="sxs-lookup"><span data-stu-id="0a23b-110">Digital video files are large and may be too big toodeliver over hello Internet, or for your customers’ devices toodisplay properly.</span></span> <span data-ttu-id="0a23b-111">Кодирование-это процесс сжатия видео и аудио, чтобы ваши клиенты могли просмотреть мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-111">Encoding is hello process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="0a23b-112">Задания кодирования — это один из самых распространенных операций обработки hello в службах мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="0a23b-112">Encoding jobs are one of hello most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="0a23b-113">Создать кодирования файлов мультимедиа tooconvert заданий из одной кодировки tooanother.</span><span class="sxs-lookup"><span data-stu-id="0a23b-113">You create encoding jobs tooconvert media files from one encoding tooanother.</span></span> <span data-ttu-id="0a23b-114">При кодировании можно использовать hello служб мультимедиа встроенный кодировщик (стандартный кодировщик мультимедиа).</span><span class="sxs-lookup"><span data-stu-id="0a23b-114">When you encode, you can use hello Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="0a23b-115">Можно также использовать кодировщик, предоставленный партнером служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0a23b-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="0a23b-116">Сторонние кодировщики можно найти hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0a23b-116">Third-party encoders are available through hello Azure Marketplace.</span></span> <span data-ttu-id="0a23b-117">Можно указать hello данные задач кодирования, используя предустановленные строки, заданные для кодировщика или используя предустановленные файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0a23b-117">You can specify hello details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="0a23b-118">toosee hello типов наборов параметров, доступных в разделе [предустановки задачи для Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="0a23b-118">toosee hello types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="0a23b-119">Каждое задание может включать один или несколько задач в зависимости от типа hello обработки, которую хотите tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="0a23b-119">Each job can have one or more tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="0a23b-120">Через hello REST API можно создать задания и связанные задачи одним из двух способов:</span><span class="sxs-lookup"><span data-stu-id="0a23b-120">Through hello REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="0a23b-121">Задачи могут быть определен как встроенный через hello свойства навигации Tasks объекта сущности задания.</span><span class="sxs-lookup"><span data-stu-id="0a23b-121">Tasks can be defined inline through hello Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="0a23b-122">можно использовать пакетную обработку OData.</span><span class="sxs-lookup"><span data-stu-id="0a23b-122">Use OData batch processing.</span></span>

<span data-ttu-id="0a23b-123">Рекомендуется всегда кодировать исходные файлы в набор MP4 с адаптивной скоростью, а затем преобразовать hello набор toohello нужный формат с помощью [динамической упаковки](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a23b-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert hello set toohello desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="0a23b-124">Если выходной актив является зашифрованного в хранилище, необходимо настроить политику доставки актива hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-124">If your output asset is storage encrypted, you must configure hello asset delivery policy.</span></span> <span data-ttu-id="0a23b-125">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="0a23b-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="0a23b-126">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="0a23b-126">Considerations</span></span>

<span data-ttu-id="0a23b-127">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="0a23b-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0a23b-128">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0a23b-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="0a23b-129">Прежде чем начать, ссылающиеся на обработчики мультимедиа, убедитесь, что имеют hello идентификатор правильный носитель процессора.</span><span class="sxs-lookup"><span data-stu-id="0a23b-129">Before you start referencing media processors, verify that you have hello correct media processor ID.</span></span> <span data-ttu-id="0a23b-130">Дополнительные сведения см. в статье [Получение экземпляра процессора мультимедиа](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="0a23b-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="0a23b-131">Подключение служб tooMedia</span><span class="sxs-lookup"><span data-stu-id="0a23b-131">Connect tooMedia Services</span></span>

<span data-ttu-id="0a23b-132">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0a23b-132">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="0a23b-133">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="0a23b-133">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0a23b-134">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="0a23b-134">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="0a23b-135">Создание задания с одной задачей кодирования</span><span class="sxs-lookup"><span data-stu-id="0a23b-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="0a23b-136">При работе с API REST служб мультимедиа hello hello действуют следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="0a23b-136">When you're working with hello Media Services REST API, hello following considerations apply:</span></span>
>
> <span data-ttu-id="0a23b-137">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="0a23b-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="0a23b-138">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0a23b-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="0a23b-139">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="0a23b-139">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="0a23b-140">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="0a23b-140">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="0a23b-141">Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="0a23b-141">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="0a23b-142">При использовании JSON и указав toouse hello **__metadata** ключевое слово в запросе hello (например, tooreferences связанный объект), необходимо задать hello **Accept** заголовок слишком[JSON в подробном формате ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Принять: приложение/json; odata = подробных сведений.</span><span class="sxs-lookup"><span data-stu-id="0a23b-142">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object), you must set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="0a23b-143">Hello в следующем примере показано, как toocreate и post задание с одной задачи набор tooencode видео с определенным разрешением и качества.</span><span class="sxs-lookup"><span data-stu-id="0a23b-143">hello following example shows you how toocreate and post a job with one task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="0a23b-144">При кодировании с помощью Media Encoder Standard вы можете использовать предустановки конфигурации задач, указанные [здесь](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="0a23b-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="0a23b-145">Запрос:</span><span class="sxs-lookup"><span data-stu-id="0a23b-145">Request:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

<span data-ttu-id="0a23b-146">Ответ:</span><span class="sxs-lookup"><span data-stu-id="0a23b-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a><span data-ttu-id="0a23b-147">Задайте имя выходного актива hello</span><span class="sxs-lookup"><span data-stu-id="0a23b-147">Set hello output asset's name</span></span>
<span data-ttu-id="0a23b-148">Привет, в следующем примере показано, как tooset hello атрибута assetName:</span><span class="sxs-lookup"><span data-stu-id="0a23b-148">hello following example shows how tooset hello assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="0a23b-149">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="0a23b-149">Considerations</span></span>
* <span data-ttu-id="0a23b-150">Свойства TaskBody должны использовать числовой литерал XML toodefine hello ввода или вывода ресурсы, которые используются задачей «hello».</span><span class="sxs-lookup"><span data-stu-id="0a23b-150">TaskBody properties must use literal XML toodefine hello number of input, or output assets that are used by hello task.</span></span> <span data-ttu-id="0a23b-151">раздел задача Hello содержит hello определения схемы XML для hello XML.</span><span class="sxs-lookup"><span data-stu-id="0a23b-151">hello task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="0a23b-152">В hello TaskBody определение каждого внутреннее значение атрибута <inputAsset> и <outputAsset> должен быть задан как JobInputAsset(value) или JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="0a23b-152">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="0a23b-153">В задаче может содержаться несколько выходных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0a23b-153">A task can have multiple output assets.</span></span> <span data-ttu-id="0a23b-154">Значение JobOutputAsset(x) может использоваться только один раз в качестве выходных данных задачи в задании.</span><span class="sxs-lookup"><span data-stu-id="0a23b-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="0a23b-155">В качестве входного ресурса задачи можно указать JobInputAsset или JobOutputAsset.</span><span class="sxs-lookup"><span data-stu-id="0a23b-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="0a23b-156">Задачи не должны образовывать цикл.</span><span class="sxs-lookup"><span data-stu-id="0a23b-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="0a23b-157">значение параметра Hello передается tooJobInputAsset или JobOutputAsset представляет hello значение индекса для актива.</span><span class="sxs-lookup"><span data-stu-id="0a23b-157">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an asset.</span></span> <span data-ttu-id="0a23b-158">Hello фактические ресурсы определяются в hello InputMediaAssets и OutputMediaAssets свойства навигации в определении объекта job hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-158">hello actual assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello job entity definition.</span></span>
* <span data-ttu-id="0a23b-159">Поскольку службы мультимедиа разработаны на основе OData v3, hello отдельные ресурсы в hello InputMediaAssets и коллекциях свойств навигации OutputMediaAssets указываются с помощью «__metadata: uri» пары "имя значение".</span><span class="sxs-lookup"><span data-stu-id="0a23b-159">Because Media Services is built on OData v3, hello individual assets in hello InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="0a23b-160">Объекты InputMediaAssets сопоставляются tooone или несколько ресурсов, созданные в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0a23b-160">InputMediaAssets maps tooone or more assets that you created in Media Services.</span></span> <span data-ttu-id="0a23b-161">Объекты OutputMediaAssets создаются системой hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-161">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="0a23b-162">Они не ссылаются на существующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="0a23b-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="0a23b-163">Может иметь имя OutputMediaAssets с помощью атрибута assetName hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-163">OutputMediaAssets can be named by using hello assetName attribute.</span></span> <span data-ttu-id="0a23b-164">Если этот атрибут не задан, то имя hello hello объекта OutputMediaAsset будет любое значение внутренний текст hello hello <outputAsset> существует элемент с суффиксом hello имя задания значение или значение идентификатора задания hello (в случае hello, где свойство Name hello не определено).</span><span class="sxs-lookup"><span data-stu-id="0a23b-164">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="0a23b-165">Например если задать значение для assetName слишком «Пример», а затем задать свойство Name объекта OutputMediaAsset hello слишком «Sample.»</span><span class="sxs-lookup"><span data-stu-id="0a23b-165">For example, if you set a value for assetName too"Sample," then hello OutputMediaAsset Name property is set too"Sample."</span></span> <span data-ttu-id="0a23b-166">Тем не менее если не задать значение для assetName, но был указан hello имя задания слишком «NewJob», а затем hello Name объекта OutputMediaAsset будет «JobOutputAsset (значение) _NewJob».</span><span class="sxs-lookup"><span data-stu-id="0a23b-166">However, if you didn't set a value for assetName, but did set hello job name too"NewJob," then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="0a23b-167">Создание задания с цепными задачами</span><span class="sxs-lookup"><span data-stu-id="0a23b-167">Create a job with chained tasks</span></span>
<span data-ttu-id="0a23b-168">Во многих сценариях приложений разработчики должны toocreate ряд задач обработки.</span><span class="sxs-lookup"><span data-stu-id="0a23b-168">In many application scenarios, developers want toocreate a series of processing tasks.</span></span> <span data-ttu-id="0a23b-169">В службах мультимедиа вы можете создавать серии цепных задач.</span><span class="sxs-lookup"><span data-stu-id="0a23b-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="0a23b-170">Каждая задача выполняет разные шаги обработки. Эти задачи также могут использовать разные обработчики мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="0a23b-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="0a23b-171">Hello связанных задач можно передавать актив из одной задачи tooanother, выполняя линейную последовательность задач в активе hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-171">hello chained tasks can hand off an asset from one task tooanother, performing a linear sequence of tasks on hello asset.</span></span> <span data-ttu-id="0a23b-172">Однако hello задачи, выполняемые в задании не требуется toobe в последовательности.</span><span class="sxs-lookup"><span data-stu-id="0a23b-172">However, hello tasks performed in a job are not required toobe in a sequence.</span></span> <span data-ttu-id="0a23b-173">При создании связанной задачи связанные hello **ITask** объекты создаются в одном **IJob** объекта.</span><span class="sxs-lookup"><span data-stu-id="0a23b-173">When you create a chained task, hello chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="0a23b-174">Сейчас количество задач ограничено 30 задачами на задание.</span><span class="sxs-lookup"><span data-stu-id="0a23b-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="0a23b-175">Если требуется более 30 задач toochain создайте более чем одному заданию toocontain hello задачи.</span><span class="sxs-lookup"><span data-stu-id="0a23b-175">If you need toochain more than 30 tasks, create more than one job toocontain hello tasks.</span></span>
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a><span data-ttu-id="0a23b-176">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="0a23b-176">Considerations</span></span>
<span data-ttu-id="0a23b-177">tooenable цепочки задач:</span><span class="sxs-lookup"><span data-stu-id="0a23b-177">tooenable task chaining:</span></span>

* <span data-ttu-id="0a23b-178">в задании должно быть по крайней мере две задачи;</span><span class="sxs-lookup"><span data-stu-id="0a23b-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="0a23b-179">Должен существовать хотя бы одна задача, входные данные — hello выходными данными другой задачи в задании hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-179">There must be at least one task whose input is hello output of another task in hello job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="0a23b-180">Использование пакетной обработки OData</span><span class="sxs-lookup"><span data-stu-id="0a23b-180">Use OData batch processing</span></span>
<span data-ttu-id="0a23b-181">Hello в следующем примере показано, как toouse OData пакетной обработки toocreate задания и задачи.</span><span class="sxs-lookup"><span data-stu-id="0a23b-181">hello following example shows how toouse OData batch processing toocreate a job and tasks.</span></span> <span data-ttu-id="0a23b-182">Чтобы узнать больше о пакетной обработке, ознакомьтесь с [пакетной обработкой посредством протокола OData](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="0a23b-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="0a23b-183">Создание задания с помощью сущности JobTemplate</span><span class="sxs-lookup"><span data-stu-id="0a23b-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="0a23b-184">При обработке нескольких активов с помощью общего набора задач, используйте стили задачу по умолчанию hello toospecify JobTemplate или tooset hello порядка задач.</span><span class="sxs-lookup"><span data-stu-id="0a23b-184">When you process multiple assets by using a common set of tasks, use a JobTemplate toospecify hello default task presets, or tooset hello order of tasks.</span></span>

<span data-ttu-id="0a23b-185">Привет, в следующем примере показан способ toocreate JobTemplate с TaskTemplate, который является встроенной.</span><span class="sxs-lookup"><span data-stu-id="0a23b-185">hello following example shows how toocreate a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="0a23b-186">Hello TaskTemplate использует стандартный кодировщик мультимедиа hello как файл актива hello tooencode обработчика мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="0a23b-186">hello TaskTemplate uses hello Media Encoder Standard as hello MediaProcessor tooencode hello asset file.</span></span> <span data-ttu-id="0a23b-187">Но также можно использовать и другие обработчики.</span><span class="sxs-lookup"><span data-stu-id="0a23b-187">However, other MediaProcessors can be used as well.</span></span>

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> <span data-ttu-id="0a23b-188">В отличие от других сущностей служб мультимедиа необходимо определить новый идентификатор GUID для каждого шаблона TaskTemplate и поместите его в свойства hello taskTemplateId и Id в тексте запроса.</span><span class="sxs-lookup"><span data-stu-id="0a23b-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in hello taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="0a23b-189">Схема идентификации контента Hello должны соответствовать схеме hello, описанной в идентификации сущностей служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="0a23b-189">hello content identification scheme must follow hello scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="0a23b-190">Кроме того, сущности JobTemplates нельзя обновлять.</span><span class="sxs-lookup"><span data-stu-id="0a23b-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="0a23b-191">Вместо этого необходимо создавать новые сущности с необходимыми изменениями.</span><span class="sxs-lookup"><span data-stu-id="0a23b-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="0a23b-192">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="0a23b-192">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="0a23b-193">Следующий пример показывает как Hello toocreate задание, которое ссылается на идентификатор JobTemplate:</span><span class="sxs-lookup"><span data-stu-id="0a23b-193">hello following example shows how toocreate a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="0a23b-194">В случае успешного выполнения возвращается следующий ответ hello:</span><span class="sxs-lookup"><span data-stu-id="0a23b-194">If successful, hello following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="0a23b-195">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="0a23b-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0a23b-196">Отзывы</span><span class="sxs-lookup"><span data-stu-id="0a23b-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0a23b-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a23b-197">Next steps</span></span>
<span data-ttu-id="0a23b-198">Теперь, когда вы знаете, как toocreate tooencode задания Создать файл, см. статью [как toocheck задания выполняется с помощью служб мультимедиа](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="0a23b-198">Now that you know how toocreate a job tooencode an asset, see [How toocheck job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0a23b-199">См. также</span><span class="sxs-lookup"><span data-stu-id="0a23b-199">See also</span></span>
[<span data-ttu-id="0a23b-200">Получение обработчиков мультимедиа</span><span class="sxs-lookup"><span data-stu-id="0a23b-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
