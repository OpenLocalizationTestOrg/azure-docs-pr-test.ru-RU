---
title: "toouse aaaHow Blitline для обработки изображений - функция руководство по Azure"
description: "Узнайте, как toouse hello Blitline обслуживания образов tooprocess приложении Azure."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="c7f5f-103">Как toouse Blitline с Azure и хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c7f5f-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="c7f5f-104">В этом руководстве объясняется, как tooaccess Blitline службы и как toosubmit заданий tooBlitline.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="c7f5f-105">Что такое Blitline?</span><span class="sxs-lookup"><span data-stu-id="c7f5f-105">What is Blitline?</span></span>
<span data-ttu-id="c7f5f-106">Blitline является служба, которая обеспечивает обработку образа на уровне предприятия в малую долю hello цену, что он будет стоить toobuild обработки изображений на основе облака его самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="c7f5f-107">факт Hello является, что обработка изображений выполняются снова и снова, обычно перестроен с нуля hello для каждого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="c7f5f-108">Мы понимаем это, так как сами множество раз делали это.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="c7f5f-109">Однажды мы решили, что пора создать универсальное решение.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="c7f5f-110">Мы знаем, как toodo его toodo он быстро и эффективно и сохраните все работать в hello это время.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="c7f5f-111">Дополнительные сведения см. на веб-сайте [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="c7f5f-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="c7f5f-112">Чем Blitline НЕ является...</span><span class="sxs-lookup"><span data-stu-id="c7f5f-112">What Blitline is NOT...</span></span>
<span data-ttu-id="c7f5f-113">tooclarify что Blitline полезно для — часто проще tooidentify Blitline не возможности перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="c7f5f-114">Blitline не поддерживает изображения tooupload мини-приложений HTML.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="c7f5f-115">Необходимо иметь изображений, доступных публично или с ограниченными разрешениями для Blitline tooreach.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="c7f5f-116">Blitline НЕ поддерживает функции динамической обработки изображений, аналогичных Aviary.com.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="c7f5f-117">Blitline не поддерживает отправку изображений, невозможно принудительно вашей tooBlitline изображения непосредственно.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="c7f5f-118">Необходимо отправить их tooAzure хранилища или других местах, который поддерживает Blitline и затем укажите, где toogo получить их Blitline.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="c7f5f-119">Blitline использует массовый параллелизм и НЕ выполняет синхронную обработку.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="c7f5f-120">То есть вы должны предоставить нам URL-адрес обратной передачи postback_url, чтобы мы могли сообщить, когда обработка завершена.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="c7f5f-121">Создание учетной записи Blitline</span><span class="sxs-lookup"><span data-stu-id="c7f5f-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="c7f5f-122">Как toocreate Blitline задания</span><span class="sxs-lookup"><span data-stu-id="c7f5f-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="c7f5f-123">Blitline использует JSON toodefine hello действия должны tootake на изображении.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="c7f5f-124">Эта JSON состоит из нескольких простых полей.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="c7f5f-125">Простейший пример Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c7f5f-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="c7f5f-126">Здесь у нас есть JSON, которое займет изображения «src»»... boys.jpeg», а затем увеличить too240x140 этого образа.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="c7f5f-127">Идентификатор приложения Hello-то можно найти в вашей **сведений о СОЕДИНЕНИИ** или **УПРАВЛЕНИЕ** вкладку в Azure.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="c7f5f-128">Это ваш идентификатор секрета, который позволяет toorun заданий на Blitline.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="c7f5f-129">Привет, параметр «Сохранить» определяет сведения о нужное изображение hello tooput после мы еще обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="c7f5f-130">В этом простейшем случае такое расположение не задано.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="c7f5f-131">Если расположение не определено, Blitline сохраняет изображение локально (и временно) в уникальном расположении в облаке.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="c7f5f-132">Можно будет tooget, откуда hello JSON, возвращенные функцией Blitline при внесении hello Blitline.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="c7f5f-133">Идентификатор Hello «изображения» является обязательным и возвращается tooyou при tooidentify данного конкретного сохранении изображения.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="c7f5f-134">Можно найти дополнительные сведения о hello *функции* мы поддерживаем здесь: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="c7f5f-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="c7f5f-135">Также можно найти документацию по hello здесь параметры задания: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="c7f5f-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="c7f5f-136">При наличии JSON является все, что нужно toodo **POST** он слишком`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="c7f5f-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="c7f5f-137">Обратно возвращается JSON следующего вида:</span><span class="sxs-lookup"><span data-stu-id="c7f5f-137">You will get JSON back that looks something like this:</span></span>

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


<span data-ttu-id="c7f5f-138">Это означает, что запрос получен Blitline, он помещена в очередь обработки, а после ее завершения hello изображения можно найти по адресу: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_приложения\_идентификатор /CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="c7f5f-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="c7f5f-139">Как toosave tooyour изображения учетной записи хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c7f5f-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="c7f5f-140">Если у вас есть учетная запись хранилища Azure, легко может иметь Blitline принудительной hello обработки изображений в контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="c7f5f-141">Путем добавления «azure_destination» определяют расположение hello и разрешения для toopush Blitline для.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="c7f5f-142">Пример:</span><span class="sxs-lookup"><span data-stu-id="c7f5f-142">Here is an example:</span></span>

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


<span data-ttu-id="c7f5f-143">Заполнив hello CAPITALIZED значения собственными, вы можете отправить этот toohttp://api.blitline.com/job JSON и hello «src» образ будет обрабатываться с помощью фильтра размытия и затем помещаются tooyou Azure назначения.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="c7f5f-144">Обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="c7f5f-144">Please note:</span></span>
<span data-ttu-id="c7f5f-145">Hello SAS должен содержать hello весь URL-адрес SAS, включая имя файла hello hello конечный файл.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="c7f5f-146">Пример:</span><span class="sxs-lookup"><span data-stu-id="c7f5f-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="c7f5f-147">Также может считывать hello последний выпуск docs хранилища Azure Blitline [здесь](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="c7f5f-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7f5f-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7f5f-148">Next Steps</span></span>
<span data-ttu-id="c7f5f-149">Посетите tooread blitline.com о нашем остальные функции:</span><span class="sxs-lookup"><span data-stu-id="c7f5f-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="c7f5f-150">Документы о конечных точках API Blitline: <http://www.blitline.com/docs/api>.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="c7f5f-151">Функции API Blitline: <http://www.blitline.com/docs/functions>.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="c7f5f-152">Примеры API Blitline: <http://www.blitline.com/docs/examples>.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="c7f5f-153">Библиотека Nuget стороннего поставщика: <http://nuget.org/packages/Blitline.Net>.</span><span class="sxs-lookup"><span data-stu-id="c7f5f-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

