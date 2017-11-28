---
title: "Использование Blitline для работы с изображениями — руководство по компонентам Azure"
description: "Узнайте, как использовать службу Blitline для обработки изображений в приложении Azure."
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
ms.openlocfilehash: 1d90599e028b3407a513b04b878e3aefc39928a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="25f30-103">Как использовать Blitline с Azure и службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="25f30-103">How to use Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="25f30-104">В этом руководстве объясняется, как получить доступ к службам Blitline и отправлять задания в Blitline.</span><span class="sxs-lookup"><span data-stu-id="25f30-104">This guide will explain how to access Blitline services and how to submit jobs to Blitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="25f30-105">Что такое Blitline?</span><span class="sxs-lookup"><span data-stu-id="25f30-105">What is Blitline?</span></span>
<span data-ttu-id="25f30-106">Blitline — это облачная служба обработки изображений, обеспечивающая обработку изображений корпоративного класса по доступной цене, которая значительно меньше стоимости самостоятельной разработки аналогичного решения.</span><span class="sxs-lookup"><span data-stu-id="25f30-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of the price that it would cost to build it yourself.</span></span>

<span data-ttu-id="25f30-107">Фактически, обработка изображений осуществляется довольно регулярно, при этом для каждого отдельного сайта соответствующие функции обычно реализуются "с нуля".</span><span class="sxs-lookup"><span data-stu-id="25f30-107">The fact is that image processing has been done over and over again, usually rebuilt from the ground up for each and every website.</span></span> <span data-ttu-id="25f30-108">Мы понимаем это, так как сами множество раз делали это.</span><span class="sxs-lookup"><span data-stu-id="25f30-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="25f30-109">Однажды мы решили, что пора создать универсальное решение.</span><span class="sxs-lookup"><span data-stu-id="25f30-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="25f30-110">Мы знаем, как быстро и эффективно добиться этого, сохранив при этом работу всех сотрудников.</span><span class="sxs-lookup"><span data-stu-id="25f30-110">We know how to do it, to do it fast and efficiently, and save everyone work in the meantime.</span></span>

<span data-ttu-id="25f30-111">Дополнительные сведения см. на веб-сайте [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="25f30-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="25f30-112">Чем Blitline НЕ является...</span><span class="sxs-lookup"><span data-stu-id="25f30-112">What Blitline is NOT...</span></span>
<span data-ttu-id="25f30-113">Чтобы прояснить преимущества Blitline, проще определить, что Blitline НЕ делает.</span><span class="sxs-lookup"><span data-stu-id="25f30-113">To clarify what Blitline is useful for, it is often easier to identify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="25f30-114">Blitline НЕ содержит мини-приложения HTML для отправки изображений.</span><span class="sxs-lookup"><span data-stu-id="25f30-114">Blitline does NOT have HTML widgets to upload images.</span></span> <span data-ttu-id="25f30-115">Для Blitline необходимо использовать общедоступные изображения или изображения с ограниченными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="25f30-115">You must have images available publicly or with restricted permissions available for Blitline to reach.</span></span>
* <span data-ttu-id="25f30-116">Blitline НЕ поддерживает функции динамической обработки изображений, аналогичных Aviary.com.</span><span class="sxs-lookup"><span data-stu-id="25f30-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="25f30-117">Blitline НЕ поддерживает отправку изображений, то есть принудительная отправка изображений напрямую в Blitline невозможна.</span><span class="sxs-lookup"><span data-stu-id="25f30-117">Blitline does NOT accept image uploads, you cannot push your images to Blitline directly.</span></span> <span data-ttu-id="25f30-118">Необходимо передавать их в хранилище Azure или в другие места, поддерживаемые Blitline, и затем указывать их расположение службе Blitline.</span><span class="sxs-lookup"><span data-stu-id="25f30-118">You must push them to Azure Storage or other places Blitline supports and then tell Blitline where to go get them.</span></span>
* <span data-ttu-id="25f30-119">Blitline использует массовый параллелизм и НЕ выполняет синхронную обработку.</span><span class="sxs-lookup"><span data-stu-id="25f30-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="25f30-120">То есть вы должны предоставить нам URL-адрес обратной передачи postback_url, чтобы мы могли сообщить, когда обработка завершена.</span><span class="sxs-lookup"><span data-stu-id="25f30-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="25f30-121">Создание учетной записи Blitline</span><span class="sxs-lookup"><span data-stu-id="25f30-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-to-create-a-blitline-job"></a><span data-ttu-id="25f30-122">Создание задания Blitline</span><span class="sxs-lookup"><span data-stu-id="25f30-122">How to create a Blitline job</span></span>
<span data-ttu-id="25f30-123">Blitline использует JSON для определения действий, которые вы хотите выполнить для изображения.</span><span class="sxs-lookup"><span data-stu-id="25f30-123">Blitline uses JSON to define the actions you want to take on an image.</span></span> <span data-ttu-id="25f30-124">Эта JSON состоит из нескольких простых полей.</span><span class="sxs-lookup"><span data-stu-id="25f30-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="25f30-125">Ниже приведен простейший пример:</span><span class="sxs-lookup"><span data-stu-id="25f30-125">The simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="25f30-126">Здесь приведена JSON, которая обратится к изображению SRC "... boys.jpeg" и увеличит его размер до 240x140.</span><span class="sxs-lookup"><span data-stu-id="25f30-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image to 240x140.</span></span>

<span data-ttu-id="25f30-127">Идентификатор приложения можно найти на вкладке **Сведения о подключении** или **Управление** в Azure.</span><span class="sxs-lookup"><span data-stu-id="25f30-127">The Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="25f30-128">Это ваш секретный идентификатор, который позволяет выполнять задания в Blitline.</span><span class="sxs-lookup"><span data-stu-id="25f30-128">It is your secret identifier that allows you to run jobs on Blitline.</span></span>

<span data-ttu-id="25f30-129">Параметр "save" определяет сведения о расположении, куда требуется поместить изображение после обработки.</span><span class="sxs-lookup"><span data-stu-id="25f30-129">The "save" parameter identifies information about where you want to put the image once we have processed it.</span></span> <span data-ttu-id="25f30-130">В этом простейшем случае такое расположение не задано.</span><span class="sxs-lookup"><span data-stu-id="25f30-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="25f30-131">Если расположение не определено, Blitline сохраняет изображение локально (и временно) в уникальном расположении в облаке.</span><span class="sxs-lookup"><span data-stu-id="25f30-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="25f30-132">Сведения об этом расположении можно получить из JSON, возвращаемой Blitline при вызове.</span><span class="sxs-lookup"><span data-stu-id="25f30-132">You will be able to get that location from the JSON returned by Blitline when you make the Blitline.</span></span> <span data-ttu-id="25f30-133">Идентификатор "image" является обязательным и возвращается, когда требуется идентифицировать данное конкретное сохраненное изображение.</span><span class="sxs-lookup"><span data-stu-id="25f30-133">The "image" identifier is required and is returned to you when to identify this particular saved image.</span></span>

<span data-ttu-id="25f30-134">Дополнительную информацию о поддерживаемых *функциях* см. здесь: <http://www.blitline.com/docs/functions>.</span><span class="sxs-lookup"><span data-stu-id="25f30-134">You can find more information about the *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="25f30-135">Кроме того, документация по параметрам заданий доступна здесь: <http://www.blitline.com/docs/api>.</span><span class="sxs-lookup"><span data-stu-id="25f30-135">You can also find documentation about the job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="25f30-136">Получив объект JSON, достаточно отправить его с помощью команды **POST** на адрес `http://api.blitline.com/job`.</span><span class="sxs-lookup"><span data-stu-id="25f30-136">Once you have your JSON all you need to do is **POST** it to `http://api.blitline.com/job`</span></span>

<span data-ttu-id="25f30-137">Обратно возвращается JSON следующего вида:</span><span class="sxs-lookup"><span data-stu-id="25f30-137">You will get JSON back that looks something like this:</span></span>

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


<span data-ttu-id="25f30-138">Это означает, что ваш запрос поступил в Blitline и был поставлен в очередь обработки. Когда же запрос будет выполнен, готовое изображение будет доступно по адресу: **https://s3.amazonaws.com/dev.blitline/2011110722/{ИД\_вашего\_приложения}/CK3f0xBF_2bV6wf7gEZE8w.jpg**.</span><span class="sxs-lookup"><span data-stu-id="25f30-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed the image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-to-save-an-image-to-your-azure-storage-account"></a><span data-ttu-id="25f30-139">Как сохранить изображение в учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="25f30-139">How to save an image to your Azure Storage account</span></span>
<span data-ttu-id="25f30-140">При наличии учетной записи хранения Azure можно легко настроить Blitline на принудительную отправку обработанных изображений в ваш контейнер Azure.</span><span class="sxs-lookup"><span data-stu-id="25f30-140">If you have an Azure Storage account, you can easily have Blitline push the processed images into your Azure container.</span></span> <span data-ttu-id="25f30-141">Добавив "azure_destination", вы определяете место и разрешения для принудительной отправки изображения службой Blitline.</span><span class="sxs-lookup"><span data-stu-id="25f30-141">By adding an "azure_destination" you define the location and permissions for Blitline to push to.</span></span>

<span data-ttu-id="25f30-142">Пример:</span><span class="sxs-lookup"><span data-stu-id="25f30-142">Here is an example:</span></span>

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


<span data-ttu-id="25f30-143">Указав необходимые значения для параметров, ВЫДЕЛЕННЫХ ЗАГЛАВНЫМИ БУКВАМИ, вы можете отправить этот объект JSON на адрес http://api.blitline.com/job. SRC-изображение будет обработано с использованием фильтра размытия и затем отправлено в заданное расположение Azure.</span><span class="sxs-lookup"><span data-stu-id="25f30-143">By filling in the CAPITALIZED values with your own, you can submit this JSON to http://api.blitline.com/job and the "src" image will be processed with a blur filter and then pushed to you Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="25f30-144">Обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="25f30-144">Please note:</span></span>
<span data-ttu-id="25f30-145">Подпись общего доступа (SAS) должна содержать весь URL-адрес SAS, включая имя конечного файла.</span><span class="sxs-lookup"><span data-stu-id="25f30-145">The SAS must contain the entire SAS url, including the filename of the destination file.</span></span>

<span data-ttu-id="25f30-146">Пример:</span><span class="sxs-lookup"><span data-stu-id="25f30-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="25f30-147">Вы также можете ознакомиться с последней версией документов о хранилище Azure от Blitline [здесь](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="25f30-147">You can also read the latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="25f30-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25f30-148">Next Steps</span></span>
<span data-ttu-id="25f30-149">Посетите сайт blitline.com, чтобы узнать обо всех других возможностях:</span><span class="sxs-lookup"><span data-stu-id="25f30-149">Visit blitline.com to read about all our other features:</span></span>

* <span data-ttu-id="25f30-150">Документы о конечных точках API Blitline: <http://www.blitline.com/docs/api>.</span><span class="sxs-lookup"><span data-stu-id="25f30-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="25f30-151">Функции API Blitline: <http://www.blitline.com/docs/functions>.</span><span class="sxs-lookup"><span data-stu-id="25f30-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="25f30-152">Примеры API Blitline: <http://www.blitline.com/docs/examples>.</span><span class="sxs-lookup"><span data-stu-id="25f30-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="25f30-153">Библиотека Nuget стороннего поставщика: <http://nuget.org/packages/Blitline.Net>.</span><span class="sxs-lookup"><span data-stu-id="25f30-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

