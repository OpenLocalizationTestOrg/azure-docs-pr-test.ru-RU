---
title: "Использование веб-службы машинного обучения через Excel | Документация Майкрософт"
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
ms.openlocfilehash: 9f1aac04d54221888ee9374317be339400dcf085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="fce74-103">Использование веб-службы Машинного обучения Azure в Excel</span><span class="sxs-lookup"><span data-stu-id="fce74-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="fce74-104">Студия машинного обучения Azure упрощает вызов веб-службы оценки непосредственно из Excel, избавляя от необходимости написания какого-либо кода.</span><span class="sxs-lookup"><span data-stu-id="fce74-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="fce74-105">При использовании Excel 2013 (или более поздней версии) или Excel Online рекомендуется также использовать [надстройку Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="fce74-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="fce74-106">Действия</span><span class="sxs-lookup"><span data-stu-id="fce74-106">Steps</span></span>
<span data-ttu-id="fce74-107">Опубликуйте веб-службу.</span><span class="sxs-lookup"><span data-stu-id="fce74-107">Publish a web service.</span></span> <span data-ttu-id="fce74-108">[этой странице](machine-learning-walkthrough-5-publish-web-service.md) объясняется, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="fce74-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="fce74-109">В настоящее время функция книги Excel поддерживается только для служб обработки запросов и ответов с один выходом (то есть с одной меткой оценки).</span><span class="sxs-lookup"><span data-stu-id="fce74-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="fce74-110">После создания веб-службы щелкните раздел **ВЕБ-СЛУЖБЫ** в левой части студии, а затем выберите веб-службу, которую нужно использовать в Excel.</span><span class="sxs-lookup"><span data-stu-id="fce74-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="fce74-111">**Классическая веб-служба**</span><span class="sxs-lookup"><span data-stu-id="fce74-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="fce74-112">На вкладке **Панель мониторинга** веб-службы есть строка для службы обработки **Запрос — ответ**.</span><span class="sxs-lookup"><span data-stu-id="fce74-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="fce74-113">Если бы в этой службе был один выход, в строке отобразилась бы ссылка **Загрузить книгу Excel** .</span><span class="sxs-lookup"><span data-stu-id="fce74-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="fce74-114">Щелкните **Download Excel Workbook**(Скачать книгу Excel).</span><span class="sxs-lookup"><span data-stu-id="fce74-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="fce74-115">**Новая веб-служба**</span><span class="sxs-lookup"><span data-stu-id="fce74-115">**New Web Service**</span></span>

1. <span data-ttu-id="fce74-116">На портале веб-служб Машинного обучения Azure выберите **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="fce74-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="fce74-117">На странице "Consume" (Использование) в разделе **Web service consumption options** (Параметры использования веб-службы) щелкните значок Excel.</span><span class="sxs-lookup"><span data-stu-id="fce74-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="fce74-118">**Использование книги**</span><span class="sxs-lookup"><span data-stu-id="fce74-118">**Using the workbook**</span></span>

1. <span data-ttu-id="fce74-119">Откройте книгу.</span><span class="sxs-lookup"><span data-stu-id="fce74-119">Open the workbook.</span></span>
2. <span data-ttu-id="fce74-120">Отобразится предупреждение системы безопасности. Нажмите кнопку **Разрешить изменение**.</span><span class="sxs-lookup"><span data-stu-id="fce74-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="fce74-121">Отобразится предупреждение системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="fce74-121">A Security Warning appears.</span></span> <span data-ttu-id="fce74-122">Нажмите кнопку **Включить содержимое** , чтобы запустить макросы в электронной таблице.</span><span class="sxs-lookup"><span data-stu-id="fce74-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="fce74-123">После включения макросов будет создана таблица.</span><span class="sxs-lookup"><span data-stu-id="fce74-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="fce74-124">Синие столбцы представляют собой входные данные, или **ПАРАМЕТРЫ**, для веб-службы RRS.</span><span class="sxs-lookup"><span data-stu-id="fce74-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="fce74-125">Обратите внимание на выходные данные службы RRS ( **ПРОГНОЗИРУЕМЫЕ ЗНАЧЕНИЯ** ), отмеченные зеленым цветом.</span><span class="sxs-lookup"><span data-stu-id="fce74-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="fce74-126">После заполнения всех столбцов для указанной строки книга автоматически вызывает API оценки и отображает результаты оценки.</span><span class="sxs-lookup"><span data-stu-id="fce74-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="fce74-127">Чтобы оценить несколько строк, заполните вторую строку данными, и вы получите прогнозируемые значения.</span><span class="sxs-lookup"><span data-stu-id="fce74-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="fce74-128">Можно даже вставить несколько строк одновременно.</span><span class="sxs-lookup"><span data-stu-id="fce74-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="fce74-129">Для лучшей визуализации данных к прогнозируемым значениям можно применять все функции Excel (графики, Power Map, условное форматирование и пр.).</span><span class="sxs-lookup"><span data-stu-id="fce74-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="fce74-130">Предоставление общего доступа к книге</span><span class="sxs-lookup"><span data-stu-id="fce74-130">Sharing your workbook</span></span>
<span data-ttu-id="fce74-131">Для выполнения макросов в электронную таблицу должен входить ключ API.</span><span class="sxs-lookup"><span data-stu-id="fce74-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="fce74-132">Это означает, что общий доступ к книге нужно предоставлять только тем организациям и людям, которым вы доверяете.</span><span class="sxs-lookup"><span data-stu-id="fce74-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="fce74-133">Автоматическое обновление</span><span class="sxs-lookup"><span data-stu-id="fce74-133">Automatic updates</span></span>
<span data-ttu-id="fce74-134">Служба RRS вызывается в двух следующих случаях:</span><span class="sxs-lookup"><span data-stu-id="fce74-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="fce74-135">когда впервые встречается строка, содержащая значения во всех столбцах **ПАРАМЕТРЫ**</span><span class="sxs-lookup"><span data-stu-id="fce74-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="fce74-136">в любое время при изменении значения в любом столбце **Параметры** в строке, содержащей значения во всех столбцах **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="fce74-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
