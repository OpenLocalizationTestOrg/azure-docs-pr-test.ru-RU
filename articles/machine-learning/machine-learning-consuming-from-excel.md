---
title: "веб-службы обучения машины из Excel aaaConsume | Документы Microsoft"
description: "Использование веб-службы Машинного обучения Azure в Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="b8aac-103">Использование веб-службы Машинного обучения Azure в Excel</span><span class="sxs-lookup"><span data-stu-id="b8aac-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="b8aac-104">Студия машинного обучения позволяет легко toocall веб-службы непосредственно из Excel без hello требуется toowrite любого кода.</span><span class="sxs-lookup"><span data-stu-id="b8aac-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="b8aac-105">Если вы используете Excel 2013 (или более поздней версии) или Excel Online, то рекомендуется использовать hello Excel [надстройка Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="b8aac-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="b8aac-106">Действия</span><span class="sxs-lookup"><span data-stu-id="b8aac-106">Steps</span></span>
<span data-ttu-id="b8aac-107">Опубликуйте веб-службу.</span><span class="sxs-lookup"><span data-stu-id="b8aac-107">Publish a web service.</span></span> <span data-ttu-id="b8aac-108">[Эта страница](machine-learning-walkthrough-5-publish-web-service.md) объясняет, как toodo его.</span><span class="sxs-lookup"><span data-stu-id="b8aac-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="b8aac-109">В настоящее время функция книги Excel hello поддерживается только для запросов и ответов службы, имеющие один выход (то есть одну оценки метку).</span><span class="sxs-lookup"><span data-stu-id="b8aac-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="b8aac-110">При наличии веб-службы, щелкните hello **веб-службы** статьи hello левой стороны hello studio, а затем выберите hello web service tooconsume из Excel.</span><span class="sxs-lookup"><span data-stu-id="b8aac-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="b8aac-111">**Классическая веб-служба**</span><span class="sxs-lookup"><span data-stu-id="b8aac-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="b8aac-112">На hello **МОНИТОРИНГА** вкладке hello веб-службы по одной строке на hello **запрос-ОТВЕТ** службы.</span><span class="sxs-lookup"><span data-stu-id="b8aac-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="b8aac-113">Если эта служба имеет один выход, вы увидите hello **загрузить книгу Excel** ссылку в этой строке.</span><span class="sxs-lookup"><span data-stu-id="b8aac-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="b8aac-114">Щелкните **Download Excel Workbook**(Скачать книгу Excel).</span><span class="sxs-lookup"><span data-stu-id="b8aac-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="b8aac-115">**Новая веб-служба**</span><span class="sxs-lookup"><span data-stu-id="b8aac-115">**New Web Service**</span></span>

1. <span data-ttu-id="b8aac-116">Веб-служба Azure Machine Learning hello портале выберите **использование**.</span><span class="sxs-lookup"><span data-stu-id="b8aac-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="b8aac-117">На странице приветствия использование в hello **веб-параметров службы потребления** щелкните значок Excel hello.</span><span class="sxs-lookup"><span data-stu-id="b8aac-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="b8aac-118">**С помощью книги hello**</span><span class="sxs-lookup"><span data-stu-id="b8aac-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="b8aac-119">Привет открыть книгу.</span><span class="sxs-lookup"><span data-stu-id="b8aac-119">Open hello workbook.</span></span>
2. <span data-ttu-id="b8aac-120">Появляется предупреждение системы безопасности; Щелкните hello **Разрешить изменение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b8aac-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="b8aac-121">Отобразится предупреждение системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="b8aac-121">A Security Warning appears.</span></span> <span data-ttu-id="b8aac-122">Щелкните hello **включить содержимое** кнопку макросы toorun электронной таблицы.</span><span class="sxs-lookup"><span data-stu-id="b8aac-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="b8aac-123">После включения макросов будет создана таблица.</span><span class="sxs-lookup"><span data-stu-id="b8aac-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="b8aac-124">Столбцы в синей являются требуется в качестве входных данных в hello записей Ресурсов веб-службы, или **параметры**.</span><span class="sxs-lookup"><span data-stu-id="b8aac-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="b8aac-125">Обратите внимание, выходные данные hello hello обновления записей Ресурсов **ПРОГНОЗИРУЕМЫЕ значения** зеленым цветом.</span><span class="sxs-lookup"><span data-stu-id="b8aac-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="b8aac-126">Когда все столбцы для строки заполняются, hello книги автоматически вызывает API оценки hello и отображает hello оцененных результатов.</span><span class="sxs-lookup"><span data-stu-id="b8aac-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="b8aac-127">tooscore более одной строки, вторая строка hello заполнения с данными и hello спрогнозировала, что созданные значения.</span><span class="sxs-lookup"><span data-stu-id="b8aac-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="b8aac-128">Можно даже вставить несколько строк одновременно.</span><span class="sxs-lookup"><span data-stu-id="b8aac-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="b8aac-129">Функциональные возможности Excel hello (диаграммы, карты power, условного форматирования, т. д.) можно использовать с hello прогнозируемые значения toohelp визуализации данных hello.</span><span class="sxs-lookup"><span data-stu-id="b8aac-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="b8aac-130">Предоставление общего доступа к книге</span><span class="sxs-lookup"><span data-stu-id="b8aac-130">Sharing your workbook</span></span>
<span data-ttu-id="b8aac-131">Чтобы toowork макросы hello ваш ключ API должна входить hello электронной таблицы.</span><span class="sxs-lookup"><span data-stu-id="b8aac-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="b8aac-132">Это означает, что должно использовать hello книги только с сущностями и частных лиц, которым вы доверяете.</span><span class="sxs-lookup"><span data-stu-id="b8aac-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="b8aac-133">Автоматическое обновление</span><span class="sxs-lookup"><span data-stu-id="b8aac-133">Automatic updates</span></span>
<span data-ttu-id="b8aac-134">Служба RRS вызывается в двух следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="b8aac-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="b8aac-135">Здравствуйте, первый раз, когда строка имеет содержимое во всех его **параметров**</span><span class="sxs-lookup"><span data-stu-id="b8aac-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="b8aac-136">Каждый раз любой hello **параметры** изменения в строку, которая имеет все его **параметры** введены.</span><span class="sxs-lookup"><span data-stu-id="b8aac-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
