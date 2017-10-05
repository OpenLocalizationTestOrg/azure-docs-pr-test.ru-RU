---
title: "Как закодировать ресурс Azure с помощью Media Encoder Standard | Документация Майкрософт"
description: "Узнайте, как использовать Media Encoder Standard для кодирования мультимедийного содержимого в службах мультимедиа Azure. В примерах кода используется REST API."
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
ms.openlocfilehash: 796f3b5a4dd56a0160986600cbbcf38faf8add56
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-encode-an-asset-by-using-media-encoder-standard"></a><span data-ttu-id="eca3c-104">Как закодировать ресурс с помощью Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="eca3c-104">How to encode an asset by using Media Encoder Standard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eca3c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="eca3c-105">.NET</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [<span data-ttu-id="eca3c-106">REST</span><span class="sxs-lookup"><span data-stu-id="eca3c-106">REST</span></span>](media-services-rest-encode-asset.md)
> * [<span data-ttu-id="eca3c-107">Портал</span><span class="sxs-lookup"><span data-stu-id="eca3c-107">Portal</span></span>](media-services-portal-encode.md)
>
>

## <a name="overview"></a><span data-ttu-id="eca3c-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="eca3c-108">Overview</span></span>
<span data-ttu-id="eca3c-109">Для поставки цифрового видео по Интернету необходимо сжатие мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="eca3c-109">To deliver digital video over the Internet, you must compress the media.</span></span> <span data-ttu-id="eca3c-110">Размер цифровых видеофайлов достаточно велик и может быть слишком большим для доставки через Интернет или правильного отображения на устройствах клиентов.</span><span class="sxs-lookup"><span data-stu-id="eca3c-110">Digital video files are large and may be too big to deliver over the Internet, or for your customers’ devices to display properly.</span></span> <span data-ttu-id="eca3c-111">Кодирование — это процесс сжатия аудио- и видеофайлов, чтобы их могли просматривать клиенты.</span><span class="sxs-lookup"><span data-stu-id="eca3c-111">Encoding is the process of compressing video and audio so your customers can view your media.</span></span>

<span data-ttu-id="eca3c-112">Задания кодирования — одни из самых распространенных операций обработки в службах мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="eca3c-112">Encoding jobs are one of the most common processing operations in Azure Media Services.</span></span> <span data-ttu-id="eca3c-113">Они создаются для преобразования файлов мультимедиа из одного формата кодирования в другой.</span><span class="sxs-lookup"><span data-stu-id="eca3c-113">You create encoding jobs to convert media files from one encoding to another.</span></span> <span data-ttu-id="eca3c-114">При кодировании можно использовать встроенный кодировщик служб мультимедиа (стандартный кодировщик мультимедиа).</span><span class="sxs-lookup"><span data-stu-id="eca3c-114">When you encode, you can use the Media Services built-in encoder (Media Encoder Standard).</span></span> <span data-ttu-id="eca3c-115">Можно также использовать кодировщик, предоставленный партнером служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="eca3c-115">You can also use an encoder provided by a Media Services partner.</span></span> <span data-ttu-id="eca3c-116">Кодировщики сторонних производителей доступны в магазине Azure.</span><span class="sxs-lookup"><span data-stu-id="eca3c-116">Third-party encoders are available through the Azure Marketplace.</span></span> <span data-ttu-id="eca3c-117">Информацию о задачах кодировки можно указать с помощью строк предустановок, заданных для кодировщика, или файлов конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eca3c-117">You can specify the details of encoding tasks by using preset strings defined for your encoder, or by using preset configuration files.</span></span> <span data-ttu-id="eca3c-118">Типы доступных предустановок см. в разделе [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960) (Предустановки задач для Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="eca3c-118">To see the types of presets that are available, see [Task Presets for Media Encoder Standard](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="eca3c-119">Каждое задание может состоять из одной или нескольких задач в зависимости от типа обработки, которую необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="eca3c-119">Each job can have one or more tasks depending on the type of processing that you want to accomplish.</span></span> <span data-ttu-id="eca3c-120">REST API позволяет создавать задания и связанные с ними задачи одним из двух способов:</span><span class="sxs-lookup"><span data-stu-id="eca3c-120">Through the REST API, you can create jobs and their related tasks in one of two ways:</span></span>

* <span data-ttu-id="eca3c-121">задачи можно определить встроенными средствами с помощью свойства навигации Tasks в сущностях Job;</span><span class="sxs-lookup"><span data-stu-id="eca3c-121">Tasks can be defined inline through the Tasks navigation property on Job entities.</span></span>
* <span data-ttu-id="eca3c-122">можно использовать пакетную обработку OData.</span><span class="sxs-lookup"><span data-stu-id="eca3c-122">Use OData batch processing.</span></span>

<span data-ttu-id="eca3c-123">Мы рекомендуем всегда кодировать исходные файлы в набор MP4-файлов с переменной скоростью, а затем преобразовывать его в нужный формат, используя [динамическую упаковку](media-services-dynamic-packaging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eca3c-123">We recommend that you always encode your source files into an adaptive bitrate MP4 set, and then convert the set to the desired format by using [dynamic packaging](media-services-dynamic-packaging-overview.md).</span></span>

<span data-ttu-id="eca3c-124">Если выходной ресурс зашифрован в хранилище, необходимо настроить политику доставки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eca3c-124">If your output asset is storage encrypted, you must configure the asset delivery policy.</span></span> <span data-ttu-id="eca3c-125">Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="eca3c-125">For more information, see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="eca3c-126">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="eca3c-126">Considerations</span></span>

<span data-ttu-id="eca3c-127">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="eca3c-127">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="eca3c-128">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="eca3c-128">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

<span data-ttu-id="eca3c-129">Прежде чем начать ссылаться на обработчики мультимедиа, убедитесь, что у вас есть правильный идентификатор обработчика мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="eca3c-129">Before you start referencing media processors, verify that you have the correct media processor ID.</span></span> <span data-ttu-id="eca3c-130">Дополнительные сведения см. в статье [Получение экземпляра процессора мультимедиа](media-services-rest-get-media-processor.md).</span><span class="sxs-lookup"><span data-stu-id="eca3c-130">For more information, see [Get media processors](media-services-rest-get-media-processor.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="eca3c-131">Подключение к службам мультимедиа</span><span class="sxs-lookup"><span data-stu-id="eca3c-131">Connect to Media Services</span></span>

<span data-ttu-id="eca3c-132">Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="eca3c-132">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="eca3c-133">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="eca3c-133">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="eca3c-134">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="eca3c-134">You must make subsequent calls to the new URI.</span></span>

## <a name="create-a-job-with-a-single-encoding-task"></a><span data-ttu-id="eca3c-135">Создание задания с одной задачей кодирования</span><span class="sxs-lookup"><span data-stu-id="eca3c-135">Create a job with a single encoding task</span></span>
> [!NOTE]
> <span data-ttu-id="eca3c-136">При работе с REST API служб мультимедиа следует руководствоваться следующими рекомендациями.</span><span class="sxs-lookup"><span data-stu-id="eca3c-136">When you're working with the Media Services REST API, the following considerations apply:</span></span>
>
> <span data-ttu-id="eca3c-137">При доступе к сущностям в службах мультимедиа необходимо задать определенные поля и значения заголовков в HTTP-запросах.</span><span class="sxs-lookup"><span data-stu-id="eca3c-137">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="eca3c-138">Дополнительную информацию см. в статье [Обзор интерфейса REST API служб мультимедиа](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="eca3c-138">For more information, see [Setup for Media Services REST API development](media-services-rest-how-to-use.md).</span></span>
>
> <span data-ttu-id="eca3c-139">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="eca3c-139">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="eca3c-140">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="eca3c-140">You must make subsequent calls to the new URI.</span></span> <span data-ttu-id="eca3c-141">Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="eca3c-141">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
>
> <span data-ttu-id="eca3c-142">Если вы используете JSON и указали ключевое слово **__metadata** в запросе (например, для ссылки на связанный объект), то вам НЕОБХОДИМО задать для заголовка **Accept** [подробный формат JSON](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span><span class="sxs-lookup"><span data-stu-id="eca3c-142">When using JSON and specifying to use the **__metadata** keyword in the request (for example, to references a linked object), you must set the **Accept** header to [JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/): Accept: application/json;odata=verbose.</span></span>
>
>

<span data-ttu-id="eca3c-143">В следующем примере показано, как создать и опубликовать задание с одной задачей, предназначенной для кодирования видео с определенным разрешением и качеством.</span><span class="sxs-lookup"><span data-stu-id="eca3c-143">The following example shows you how to create and post a job with one task set to encode a video at a specific resolution and quality.</span></span> <span data-ttu-id="eca3c-144">При кодировании с помощью Media Encoder Standard вы можете использовать предустановки конфигурации задач, указанные [здесь](http://msdn.microsoft.com/library/mt269960).</span><span class="sxs-lookup"><span data-stu-id="eca3c-144">When you encode with Media Encoder Standard, you can use task configuration presets specified [here](http://msdn.microsoft.com/library/mt269960).</span></span>

<span data-ttu-id="eca3c-145">Запрос:</span><span class="sxs-lookup"><span data-stu-id="eca3c-145">Request:</span></span>

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

<span data-ttu-id="eca3c-146">Ответ:</span><span class="sxs-lookup"><span data-stu-id="eca3c-146">Response:</span></span>

    HTTP/1.1 201 Created

    . . .

### <a name="set-the-output-assets-name"></a><span data-ttu-id="eca3c-147">Задание имени выходного актива</span><span class="sxs-lookup"><span data-stu-id="eca3c-147">Set the output asset's name</span></span>
<span data-ttu-id="eca3c-148">В следующем примере показано, как установить атрибут assetName:</span><span class="sxs-lookup"><span data-stu-id="eca3c-148">The following example shows how to set the assetName attribute:</span></span>

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a><span data-ttu-id="eca3c-149">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="eca3c-149">Considerations</span></span>
* <span data-ttu-id="eca3c-150">Чтобы определить количество входных или выходных ресурсов, используемых задачей, в свойствах TaskBody необходимо использовать XML-литерал.</span><span class="sxs-lookup"><span data-stu-id="eca3c-150">TaskBody properties must use literal XML to define the number of input, or output assets that are used by the task.</span></span> <span data-ttu-id="eca3c-151">В разделе задачи приведено определение схемы XML.</span><span class="sxs-lookup"><span data-stu-id="eca3c-151">The task topic contains the XML Schema Definition for the XML.</span></span>
* <span data-ttu-id="eca3c-152">В определении TaskBody каждое внутреннее значение <inputAsset> и <outputAsset> необходимо установить как JobInputAsset(value) или JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="eca3c-152">In the TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="eca3c-153">В задаче может содержаться несколько выходных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eca3c-153">A task can have multiple output assets.</span></span> <span data-ttu-id="eca3c-154">Значение JobOutputAsset(x) может использоваться только один раз в качестве выходных данных задачи в задании.</span><span class="sxs-lookup"><span data-stu-id="eca3c-154">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="eca3c-155">В качестве входного ресурса задачи можно указать JobInputAsset или JobOutputAsset.</span><span class="sxs-lookup"><span data-stu-id="eca3c-155">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="eca3c-156">Задачи не должны образовывать цикл.</span><span class="sxs-lookup"><span data-stu-id="eca3c-156">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="eca3c-157">Значение параметра, которое передается в JobInputAsset или JobOutputAsset, — это значение индекса для ресурса.</span><span class="sxs-lookup"><span data-stu-id="eca3c-157">The value parameter that you pass to JobInputAsset or JobOutputAsset represents the index value for an asset.</span></span> <span data-ttu-id="eca3c-158">Фактические ресурсы определяются в свойствах навигации ресурса InputMediaAsset и OutputMediaAsset в определении сущности Job.</span><span class="sxs-lookup"><span data-stu-id="eca3c-158">The actual assets are defined in the InputMediaAssets and OutputMediaAssets navigation properties on the job entity definition.</span></span>
* <span data-ttu-id="eca3c-159">Так как службы мультимедиа созданы на платформе OData версии 3, ссылки на отдельные ресурсы в коллекциях свойств навигации ресурсов InputMediaAsset и OutputMediaAsset добавляются в виде пары "имя-значение": "__metadata : uri".</span><span class="sxs-lookup"><span data-stu-id="eca3c-159">Because Media Services is built on OData v3, the individual assets in the InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
* <span data-ttu-id="eca3c-160">Ресурсы InputMediaAsset сопоставляются с одним или несколькими ресурсами, созданными в службах мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="eca3c-160">InputMediaAssets maps to one or more assets that you created in Media Services.</span></span> <span data-ttu-id="eca3c-161">Ресурсы OutputMediaAsset создаются системой.</span><span class="sxs-lookup"><span data-stu-id="eca3c-161">OutputMediaAssets are created by the system.</span></span> <span data-ttu-id="eca3c-162">Они не ссылаются на существующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="eca3c-162">They don't reference an existing asset.</span></span>
* <span data-ttu-id="eca3c-163">Ресурсам OutputMediaAsset можно присвоить имя с помощью атрибута assetName.</span><span class="sxs-lookup"><span data-stu-id="eca3c-163">OutputMediaAssets can be named by using the assetName attribute.</span></span> <span data-ttu-id="eca3c-164">Если этот атрибут отсутствует, то именем ресурса OutputMediaAsset будет внутреннее текстовое значение элемента <outputAsset> с суффиксом, которым может быть значение параметра имени задания или параметра идентификатора задания (если свойство Name не определено).</span><span class="sxs-lookup"><span data-stu-id="eca3c-164">If this attribute is not present, then the name of the OutputMediaAsset is whatever the inner text value of the <outputAsset> element is with a suffix of either the Job Name value, or the Job Id value (in the case where the Name property isn't defined).</span></span> <span data-ttu-id="eca3c-165">Например, если задать для атрибута assetName значение Sample, то для свойства Name ресурса OutputMediaAsset будет задано значение Sample.</span><span class="sxs-lookup"><span data-stu-id="eca3c-165">For example, if you set a value for assetName to "Sample," then the OutputMediaAsset Name property is set to "Sample."</span></span> <span data-ttu-id="eca3c-166">Тем не менее, если значение атрибута assetName не задано, но в качестве имени задания задано NewJob, имя OutputMediaAsset будет выглядеть следующим образом: JobOutputAsset(значение)_NewJob.</span><span class="sxs-lookup"><span data-stu-id="eca3c-166">However, if you didn't set a value for assetName, but did set the job name to "NewJob," then the OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob."</span></span>

## <a name="create-a-job-with-chained-tasks"></a><span data-ttu-id="eca3c-167">Создание задания с цепными задачами</span><span class="sxs-lookup"><span data-stu-id="eca3c-167">Create a job with chained tasks</span></span>
<span data-ttu-id="eca3c-168">Во многих сценариях приложений разработчикам необходимо создать серию задач обработки.</span><span class="sxs-lookup"><span data-stu-id="eca3c-168">In many application scenarios, developers want to create a series of processing tasks.</span></span> <span data-ttu-id="eca3c-169">В службах мультимедиа вы можете создавать серии цепных задач.</span><span class="sxs-lookup"><span data-stu-id="eca3c-169">In Media Services, you can create a series of chained tasks.</span></span> <span data-ttu-id="eca3c-170">Каждая задача выполняет разные шаги обработки. Эти задачи также могут использовать разные обработчики мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="eca3c-170">Each task performs different processing steps and can use different media processors.</span></span> <span data-ttu-id="eca3c-171">Цепные задачи могут передать ресурсы из одной задачи в другую, следуя линейной последовательности задач ресурса.</span><span class="sxs-lookup"><span data-stu-id="eca3c-171">The chained tasks can hand off an asset from one task to another, performing a linear sequence of tasks on the asset.</span></span> <span data-ttu-id="eca3c-172">Тем не менее, в последовательность не должны быть включены задачи, выполняемые в задании.</span><span class="sxs-lookup"><span data-stu-id="eca3c-172">However, the tasks performed in a job are not required to be in a sequence.</span></span> <span data-ttu-id="eca3c-173">При создании цепной задачи цепные объекты **ITask** создаются в одном объекте **IJob**.</span><span class="sxs-lookup"><span data-stu-id="eca3c-173">When you create a chained task, the chained **ITask** objects are created in a single **IJob** object.</span></span>

> [!NOTE]
> <span data-ttu-id="eca3c-174">Сейчас количество задач ограничено 30 задачами на задание.</span><span class="sxs-lookup"><span data-stu-id="eca3c-174">There is currently a limit of 30 tasks per job.</span></span> <span data-ttu-id="eca3c-175">Если вам необходимо создать цепь из более чем 30 задач, создайте для них несколько заданий.</span><span class="sxs-lookup"><span data-stu-id="eca3c-175">If you need to chain more than 30 tasks, create more than one job to contain the tasks.</span></span>
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


### <a name="considerations"></a><span data-ttu-id="eca3c-176">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="eca3c-176">Considerations</span></span>
<span data-ttu-id="eca3c-177">Чтобы включить создание цепных задач:</span><span class="sxs-lookup"><span data-stu-id="eca3c-177">To enable task chaining:</span></span>

* <span data-ttu-id="eca3c-178">в задании должно быть по крайней мере две задачи;</span><span class="sxs-lookup"><span data-stu-id="eca3c-178">A job must have at least two tasks.</span></span>
* <span data-ttu-id="eca3c-179">должна существовать хотя бы одна задача, входные данные которой являются выходными данными другой задачи в задании.</span><span class="sxs-lookup"><span data-stu-id="eca3c-179">There must be at least one task whose input is the output of another task in the job.</span></span>

## <a name="use-odata-batch-processing"></a><span data-ttu-id="eca3c-180">Использование пакетной обработки OData</span><span class="sxs-lookup"><span data-stu-id="eca3c-180">Use OData batch processing</span></span>
<span data-ttu-id="eca3c-181">В следующем примере показано, как использовать пакетную обработку OData для создания задания и задач.</span><span class="sxs-lookup"><span data-stu-id="eca3c-181">The following example shows how to use OData batch processing to create a job and tasks.</span></span> <span data-ttu-id="eca3c-182">Чтобы узнать больше о пакетной обработке, ознакомьтесь с [пакетной обработкой посредством протокола OData](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="eca3c-182">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

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



## <a name="create-a-job-by-using-a-jobtemplate"></a><span data-ttu-id="eca3c-183">Создание задания с помощью сущности JobTemplate</span><span class="sxs-lookup"><span data-stu-id="eca3c-183">Create a job by using a JobTemplate</span></span>
<span data-ttu-id="eca3c-184">При обработке нескольких ресурсов с помощью обычного набора задач используйте сущности JobTemplate для определения предустановок задач по умолчанию или установления порядка задач.</span><span class="sxs-lookup"><span data-stu-id="eca3c-184">When you process multiple assets by using a common set of tasks, use a JobTemplate to specify the default task presets, or to set the order of tasks.</span></span>

<span data-ttu-id="eca3c-185">В следующем примере показано, как создать сущность JobTemplate, определив сущность TaskTemplate внутренними средствами.</span><span class="sxs-lookup"><span data-stu-id="eca3c-185">The following example shows how to create a JobTemplate with a TaskTemplate that is defined inline.</span></span> <span data-ttu-id="eca3c-186">Сущность TaskTemplate кодирует файл ресурса, используя в качестве обработчика мультимедиа Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="eca3c-186">The TaskTemplate uses the Media Encoder Standard as the MediaProcessor to encode the asset file.</span></span> <span data-ttu-id="eca3c-187">Но также можно использовать и другие обработчики.</span><span class="sxs-lookup"><span data-stu-id="eca3c-187">However, other MediaProcessors can be used as well.</span></span>

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
> <span data-ttu-id="eca3c-188">В отличие от других сущностей служб мультимедиа вы должны определить новый идентификатор GUID для каждой сущности TaskTemplate и указать его в тексте запроса в taskTemplateId и свойстве Id.</span><span class="sxs-lookup"><span data-stu-id="eca3c-188">Unlike other Media Services entities, you must define a new GUID identifier for each TaskTemplate and place it in the taskTemplateId and Id property in your request body.</span></span> <span data-ttu-id="eca3c-189">Схема идентификации содержимого должна соответствовать схеме, описанной в статье "Идентификация сущностей служб мультимедиа Azure".</span><span class="sxs-lookup"><span data-stu-id="eca3c-189">The content identification scheme must follow the scheme described in Identify Azure Media Services Entities.</span></span> <span data-ttu-id="eca3c-190">Кроме того, сущности JobTemplates нельзя обновлять.</span><span class="sxs-lookup"><span data-stu-id="eca3c-190">Also, JobTemplates cannot be updated.</span></span> <span data-ttu-id="eca3c-191">Вместо этого необходимо создавать новые сущности с необходимыми изменениями.</span><span class="sxs-lookup"><span data-stu-id="eca3c-191">Instead, you must create a new one with your updated changes.</span></span>
>
>

<span data-ttu-id="eca3c-192">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="eca3c-192">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .


<span data-ttu-id="eca3c-193">В следующем примере показано, как создать задание, которое ссылается на идентификатор JobTemplate.</span><span class="sxs-lookup"><span data-stu-id="eca3c-193">The following example shows how to create a job that references a JobTemplate Id:</span></span>

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


<span data-ttu-id="eca3c-194">При успешном выполнении возвращается следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="eca3c-194">If successful, the following response is returned:</span></span>

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a><span data-ttu-id="eca3c-195">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="eca3c-195">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="eca3c-196">Отзывы</span><span class="sxs-lookup"><span data-stu-id="eca3c-196">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="eca3c-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eca3c-197">Next steps</span></span>
<span data-ttu-id="eca3c-198">Теперь, когда вы узнали, как создать задание для кодирования ресурса, ознакомьтесь со статьей [Практическое руководство. Проверка хода выполнения задания](media-services-rest-check-job-progress.md).</span><span class="sxs-lookup"><span data-stu-id="eca3c-198">Now that you know how to create a job to encode an asset, see [How to check job progress with Media Services](media-services-rest-check-job-progress.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="eca3c-199">См. также</span><span class="sxs-lookup"><span data-stu-id="eca3c-199">See also</span></span>
[<span data-ttu-id="eca3c-200">Получение обработчиков мультимедиа</span><span class="sxs-lookup"><span data-stu-id="eca3c-200">Get Media Processors</span></span>](media-services-rest-get-media-processor.md)
