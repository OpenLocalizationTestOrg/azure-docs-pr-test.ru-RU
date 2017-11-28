---
title: "Надстройка Excel для веб-служб машинного обучения | Документация Майкрософт"
description: "Использование веб-служб машинного обучения Azure непосредственно из Excel без написания кода."
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
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="85d9d-103">Надстройка Excel для веб-служб машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="85d9d-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="85d9d-104">Excel упрощает непосредственный вызов веб-служб без необходимости написания какого-либо кода.</span><span class="sxs-lookup"><span data-stu-id="85d9d-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="85d9d-105">Использование существующей веб-службы в книге Excel</span><span class="sxs-lookup"><span data-stu-id="85d9d-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="85d9d-106">Откройте [пример файла Excel](http://aka.ms/amlexcel-sample-2), который содержит надстройки Excel и данные о пассажирах "Титаника".</span><span class="sxs-lookup"><span data-stu-id="85d9d-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="85d9d-107">Выберите веб-службу, щелкнув по ней. В данном примере это "Прогноз выживших на "Титанике" (пример надстройки Excel)".</span><span class="sxs-lookup"><span data-stu-id="85d9d-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Выберите веб-службу][01]
3. <span data-ttu-id="85d9d-109">Вы перейдете в раздел **Прогноз**.</span><span class="sxs-lookup"><span data-stu-id="85d9d-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="85d9d-110">Эта книга уже содержит образцы данных. В пустой книге можно выбрать ячейку в Excel и щелкнуть **Use sample data** (Использовать образцы данных).</span><span class="sxs-lookup"><span data-stu-id="85d9d-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="85d9d-111">Выделите данные с заголовками и щелкните значок диапазона входных данных.</span><span class="sxs-lookup"><span data-stu-id="85d9d-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="85d9d-112">Убедитесь, что установлен флажок "Мои данные содержат заголовки".</span><span class="sxs-lookup"><span data-stu-id="85d9d-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="85d9d-113">В разделе **Вывод** введите номер ячейки, в которую следует поместить выходные данные, в нашем примере это "H1".</span><span class="sxs-lookup"><span data-stu-id="85d9d-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="85d9d-114">Нажмите **Выполнить прогноз**.</span><span class="sxs-lookup"><span data-stu-id="85d9d-114">Click **Predict**.</span></span>
   
    ![Раздел «Прогноз»][02]

<span data-ttu-id="85d9d-116">Разверните новую веб-службу или используйте уже существующую.</span><span class="sxs-lookup"><span data-stu-id="85d9d-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="85d9d-117">Дополнительные сведения о развертывании веб-служб можно найти в статье [Шаг 5. Развертывание веб-службы машинного обучения Azure](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="85d9d-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="85d9d-118">Получите ключ API для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="85d9d-118">Get the API key for your web service.</span></span> <span data-ttu-id="85d9d-119">Источник получения ключа зависит от способа публикации: как классическая или как новая веб-служба машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="85d9d-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="85d9d-120">**Использование классической веб-службы**</span><span class="sxs-lookup"><span data-stu-id="85d9d-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="85d9d-121">Щелкните **ВЕБ-СЛУЖБЫ** на левой панели Студии машинного обучения, а затем выберите веб-службу.</span><span class="sxs-lookup"><span data-stu-id="85d9d-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Выбор веб-службы в студии машинного обучения][04]
2. <span data-ttu-id="85d9d-123">Скопируйте ключ API для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="85d9d-123">Copy the API key for the web service.</span></span>
   
    ![Ключ API в Студии машинного обучения][05]
3. <span data-ttu-id="85d9d-125">На вкладке **Панель мониторинга** веб-службы щелкните ссылку **Запрос-ответ**.</span><span class="sxs-lookup"><span data-stu-id="85d9d-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="85d9d-126">Найдите раздел **Request URI** (URI запроса).</span><span class="sxs-lookup"><span data-stu-id="85d9d-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="85d9d-127">Скопируйте и сохраните URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="85d9d-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="85d9d-128">Теперь вы можете войти на портал [веб-служб машинного обучения Azure](https://services.azureml.net) и получить ключ API для классической веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="85d9d-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="85d9d-129">**Использование новой веб-службы**</span><span class="sxs-lookup"><span data-stu-id="85d9d-129">**Use a New web service**</span></span>

1. <span data-ttu-id="85d9d-130">На портале [веб-служб машинного обучения Azure](https://services.azureml.net) щелкните **Веб-службы**, а затем выберите нужную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="85d9d-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="85d9d-131">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="85d9d-131">Click **Consume**.</span></span>
3. <span data-ttu-id="85d9d-132">Найдите раздел **Basic consumption info** (Основные сведения об использовании).</span><span class="sxs-lookup"><span data-stu-id="85d9d-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="85d9d-133">Скопируйте и сохраните **первичный ключ** и URL-адрес **запроса-ответа**.</span><span class="sxs-lookup"><span data-stu-id="85d9d-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="85d9d-134">Действия для добавления новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="85d9d-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="85d9d-135">Разверните новую веб-службу или используйте уже существующую.</span><span class="sxs-lookup"><span data-stu-id="85d9d-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="85d9d-136">Дополнительные сведения о развертывании веб-служб можно найти в статье [Шаг 5. Развертывание веб-службы машинного обучения Azure](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="85d9d-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="85d9d-137">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="85d9d-137">Click **Consume**.</span></span>
3. <span data-ttu-id="85d9d-138">Найдите раздел **Basic consumption info** (Основные сведения об использовании).</span><span class="sxs-lookup"><span data-stu-id="85d9d-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="85d9d-139">Скопируйте и сохраните **первичный ключ** и URL-адрес **запроса-ответа**.</span><span class="sxs-lookup"><span data-stu-id="85d9d-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="85d9d-140">В Excel перейдите в раздел **Веб-службы** (если вы находитесь в разделе **Прогноз**, то щелкните стрелку "Назад", чтобы перейти к списку веб-служб).</span><span class="sxs-lookup"><span data-stu-id="85d9d-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Переход к выбору веб-службы][03]
5. <span data-ttu-id="85d9d-142">Щелкните **Добавить веб-службу**.</span><span class="sxs-lookup"><span data-stu-id="85d9d-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="85d9d-143">Вставьте URL-адрес в текстовое поле с меткой **URL**в надстройке Excel.</span><span class="sxs-lookup"><span data-stu-id="85d9d-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="85d9d-144">Вставьте ключ API (или первичный ключ) в текстовое поле с меткой **Ключ API**.</span><span class="sxs-lookup"><span data-stu-id="85d9d-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="85d9d-145">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="85d9d-145">Click **Add**.</span></span>
   
    ![URL-адрес и ключ API для классической веб-службы.][06]
9. <span data-ttu-id="85d9d-147">Чтобы использовать веб-службу, следуйте инструкциям, указанным выше в разделе "Использование существующей веб-службы".</span><span class="sxs-lookup"><span data-stu-id="85d9d-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="85d9d-148">Предоставление общего доступа к книге</span><span class="sxs-lookup"><span data-stu-id="85d9d-148">Sharing Your Workbook</span></span>
<span data-ttu-id="85d9d-149">Во время сохранения книги также сохраняются ключи API (или первичные ключи) для веб-служб, которые вы добавили.</span><span class="sxs-lookup"><span data-stu-id="85d9d-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="85d9d-150">Это означает, что доступ к книге следует предоставлять только тем лицам, которым вы доверяете.</span><span class="sxs-lookup"><span data-stu-id="85d9d-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="85d9d-151">Любые вопросы можно задать ниже в разделе комментариев или на нашем [форуме](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="85d9d-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
