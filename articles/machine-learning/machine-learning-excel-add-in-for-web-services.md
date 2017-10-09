---
title: "aaaExcel-надстройка для служб веб-машины обучения | Документы Microsoft"
description: "Как toouse Azure Machine Learning Web services непосредственно в Microsoft Excel без написания кода."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="22078-103">Надстройка Excel для веб-служб машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="22078-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="22078-104">Excel позволяет легко toocall веб-службы непосредственно без hello требуется toowrite любого кода.</span><span class="sxs-lookup"><span data-stu-id="22078-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="22078-105">TooUse действия с существующие веб-службой в hello книги</span><span class="sxs-lookup"><span data-stu-id="22078-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="22078-106">Откройте hello [образец файла Excel](http://aka.ms/amlexcel-sample-2), содержащий hello надстройки и данные о пассажиров на hello Titanic.</span><span class="sxs-lookup"><span data-stu-id="22078-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="22078-107">Выберите веб-службу hello, щелкнув его-«Titanic выживших прогнозирования (пример надстройки Excel) [Оценка]» в этом примере.</span><span class="sxs-lookup"><span data-stu-id="22078-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Выберите веб-службу][01]
3. <span data-ttu-id="22078-109">После этого вы перейдете toohello **Predict** раздела.</span><span class="sxs-lookup"><span data-stu-id="22078-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="22078-110">Эта книга уже содержит образцы данных. В пустой книге можно выбрать ячейку в Excel и щелкнуть **Use sample data** (Использовать образцы данных).</span><span class="sxs-lookup"><span data-stu-id="22078-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="22078-111">Выберите данные hello с заголовками и щелкните значок диапазона hello входных данных.</span><span class="sxs-lookup"><span data-stu-id="22078-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="22078-112">Убедитесь, что поле «Мои данные содержат заголовки» hello.</span><span class="sxs-lookup"><span data-stu-id="22078-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="22078-113">В разделе **вывода**, введите номер ячейки hello, в котором требуется hello toobe выходных данных, например «H1» ниже.</span><span class="sxs-lookup"><span data-stu-id="22078-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="22078-114">Нажмите **Выполнить прогноз**.</span><span class="sxs-lookup"><span data-stu-id="22078-114">Click **Predict**.</span></span>
   
    ![Раздел «Прогноз»][02]

<span data-ttu-id="22078-116">Разверните новую веб-службу или используйте уже существующую.</span><span class="sxs-lookup"><span data-stu-id="22078-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="22078-117">Дополнительные сведения о развертывании веб-службы см. в разделе [шаг 5 пошагового руководства: развертывание службы Azure Machine Learning Web hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="22078-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="22078-118">Получите ключ API hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="22078-118">Get hello API key for your web service.</span></span> <span data-ttu-id="22078-119">Источник получения ключа зависит от способа публикации: как классическая или как новая веб-служба машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="22078-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="22078-120">**Использование классической веб-службы**</span><span class="sxs-lookup"><span data-stu-id="22078-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="22078-121">В студии машинного обучения, щелкните hello **веб-службы** статьи hello левой панели, а затем выберите hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="22078-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Выбор веб-службы в студии машинного обучения][04]
2. <span data-ttu-id="22078-123">Скопируйте ключ API hello hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="22078-123">Copy hello API key for hello web service.</span></span>
   
    ![Ключ API в Студии машинного обучения][05]
3. <span data-ttu-id="22078-125">На hello **МОНИТОРИНГА** hello веб-службы, нажмите кнопку hello **запрос-ОТВЕТ** ссылку.</span><span class="sxs-lookup"><span data-stu-id="22078-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="22078-126">Найдите hello **URI запроса** раздела.</span><span class="sxs-lookup"><span data-stu-id="22078-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="22078-127">Скопируйте и сохраните URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="22078-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="22078-128">Теперь стало возможно toosign в hello [веб-службы Azure Machine Learning](https://services.azureml.net) tooobtain портала ключ hello API веб-службы классический машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="22078-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="22078-129">**Использование новой веб-службы**</span><span class="sxs-lookup"><span data-stu-id="22078-129">**Use a New web service**</span></span>

1. <span data-ttu-id="22078-130">В hello [веб-службы Azure Machine Learning](https://services.azureml.net) портала, нажмите кнопку **веб-служб**, затем выберите веб-службу.</span><span class="sxs-lookup"><span data-stu-id="22078-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="22078-131">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="22078-131">Click **Consume**.</span></span>
3. <span data-ttu-id="22078-132">Найдите hello **потребления основные сведения о** раздела.</span><span class="sxs-lookup"><span data-stu-id="22078-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="22078-133">Скопируйте и сохраните hello **первичного ключа** и hello **запрос-ответ** URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="22078-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="22078-134">Действия tooAdd веб-службу</span><span class="sxs-lookup"><span data-stu-id="22078-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="22078-135">Разверните новую веб-службу или используйте уже существующую.</span><span class="sxs-lookup"><span data-stu-id="22078-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="22078-136">Дополнительные сведения о развертывании веб-службы см. в разделе [шаг 5 пошагового руководства: развертывание службы Azure Machine Learning Web hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="22078-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="22078-137">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="22078-137">Click **Consume**.</span></span>
3. <span data-ttu-id="22078-138">Найдите hello **потребления основные сведения о** раздела.</span><span class="sxs-lookup"><span data-stu-id="22078-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="22078-139">Скопируйте и сохраните hello **первичного ключа** и hello **запрос-ответ** URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="22078-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="22078-140">В Excel, выберите toohello **веб-службы** раздела (в hello **Predict** щелкните стрелку Назад hello toogo список toohello веб-службы).</span><span class="sxs-lookup"><span data-stu-id="22078-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![Выбор службы tooWeb перейти][03]
5. <span data-ttu-id="22078-142">Щелкните **Добавить веб-службу**.</span><span class="sxs-lookup"><span data-stu-id="22078-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="22078-143">Вставьте URL-адрес hello в Excel, добавьте в текстовое поле с меткой hello **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="22078-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="22078-144">Вставьте ключ API-источник hello в hello текстовое поле с меткой **ключ API**.</span><span class="sxs-lookup"><span data-stu-id="22078-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="22078-145">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="22078-145">Click **Add**.</span></span>
   
    ![URL-адрес и ключ API для классической веб-службы.][06]
9. <span data-ttu-id="22078-147">toouse hello веб-службы, следуйте предшествующий направлениях hello, «Шаги tooUse существующая web Service.»</span><span class="sxs-lookup"><span data-stu-id="22078-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="22078-148">Предоставление общего доступа к книге</span><span class="sxs-lookup"><span data-stu-id="22078-148">Sharing Your Workbook</span></span>
<span data-ttu-id="22078-149">При сохранении книги также сохранить ключ API-источник hello hello веб-служб, которые были добавлены.</span><span class="sxs-lookup"><span data-stu-id="22078-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="22078-150">Это означает, что совместно использовать hello книги следует только с тех пользователей, которым вы доверяете.</span><span class="sxs-lookup"><span data-stu-id="22078-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="22078-151">Вопросы в hello следующий раздел комментарий или на нашем [форум](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="22078-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
