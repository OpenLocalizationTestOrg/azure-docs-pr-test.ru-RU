---
title: "Устранение неполадок при повторном обучении классической веб-службы машинного обучения Azure | Документация Майкрософт"
description: "С помощью этой статьи вы сможете выявить и исправить распространенные проблемы, которые возникают при повторном обучении модели для веб-службы машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: fc36499ebff88c86635228ff899c85e9166aabed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="3290a-103">Устранение неполадок при повторном обучении классической веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="3290a-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="3290a-104">Сведения о повторном обучении</span><span class="sxs-lookup"><span data-stu-id="3290a-104">Retraining overview</span></span>
<span data-ttu-id="3290a-105">Когда вы развертываете прогнозный эксперимент в качестве оценивающей веб-службы, вы получаете статическую модель.</span><span class="sxs-lookup"><span data-stu-id="3290a-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="3290a-106">Если появляются новые данные или у пользователя API есть свои данные, эту модель нужно переобучить.</span><span class="sxs-lookup"><span data-stu-id="3290a-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="3290a-107">Полное описание повторного обучения классической веб-службы см. в статье [Программное переобучение моделей машинного обучения](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="3290a-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="3290a-108">Процесс повторного обучения</span><span class="sxs-lookup"><span data-stu-id="3290a-108">Retraining process</span></span>
<span data-ttu-id="3290a-109">Чтобы переобучить веб-службу, нужно добавить такие дополнительные компоненты.</span><span class="sxs-lookup"><span data-stu-id="3290a-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="3290a-110">Веб-службу, развернутую из обучающего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="3290a-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="3290a-111">В рамках эксперимента модуль **выходных данных веб-службы** нужно объединить с выходными данными модуля **Обучение модели**.</span><span class="sxs-lookup"><span data-stu-id="3290a-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![Присоедините выходные данные веб-службы к модели обучения.][image1]
* <span data-ttu-id="3290a-113">В оценивающую веб-службу нужно добавить новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="3290a-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="3290a-114">Сделать это можно программными средствами, воспользовавшись примером кода из статьи "Программное переобучение моделей машинного обучения", или на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3290a-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="3290a-115">Переобучить модель после этого вы можете с помощью примера кода C#, приведенного на странице справки, посвященной обучению API веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3290a-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="3290a-116">Если вы, оценив результаты, остались ими довольны, обновите оценивающую веб-службу обученной модели с помощью добавленной вами конечной точки.</span><span class="sxs-lookup"><span data-stu-id="3290a-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="3290a-117">Когда все компоненты будут готовы, для повторного обучения модели нужно выполнить следующие основные действия:</span><span class="sxs-lookup"><span data-stu-id="3290a-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="3290a-118">Вызовите обучающую веб-службу (службу пакетного выполнения (BES), а не службу отклика на запросы (RRS)).</span><span class="sxs-lookup"><span data-stu-id="3290a-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="3290a-119">Сделать вызов можно с помощью примера кода C#, приведенного на странице справки по интерфейсу API.</span><span class="sxs-lookup"><span data-stu-id="3290a-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="3290a-120">Найдите значения параметров *BaseLocation*, *RelativeLocation* и *SasBlobToken*. Они находятся в выходных данных, отправленных в ответ на ваш вызов обучающей веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3290a-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="3290a-121">![отображает выходные данные примера повторного обучения и значения параметров BaseLocation, RelativeLocation и SasBlobToken.][image6]</span><span class="sxs-lookup"><span data-stu-id="3290a-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="3290a-122">Обновите добавленную конечную точку оценивающей веб-службы с помощью повторно обученной модели. С помощью примера кода, приведенного в статье "Программное переобучение моделей машинного обучения", обновите новую конечную точку, добавленную вами в оценивающую модель, с помощью повторно обученной модели из обучающей веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3290a-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="3290a-123">Распространенные затруднения</span><span class="sxs-lookup"><span data-stu-id="3290a-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="3290a-124">Проверьте, правильно ли указан URL-адрес исправления</span><span class="sxs-lookup"><span data-stu-id="3290a-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="3290a-125">Используемый вами URL-адрес исправления должен быть связан с новой оценивающей конечной точкой, добавленной в оценивающую веб-службу.</span><span class="sxs-lookup"><span data-stu-id="3290a-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="3290a-126">Есть разные способы получить URL-адрес исправления.</span><span class="sxs-lookup"><span data-stu-id="3290a-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="3290a-127">**Вариант 1: программно**</span><span class="sxs-lookup"><span data-stu-id="3290a-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="3290a-128">Чтобы получить правильный URL-адрес исправления, выполните такие действия:</span><span class="sxs-lookup"><span data-stu-id="3290a-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="3290a-129">Выполните пример кода [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) .</span><span class="sxs-lookup"><span data-stu-id="3290a-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="3290a-130">В выходных данных AddEndpoint найдите значение *HelpLocation* и скопируйте URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3290a-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![HelpLocation в выходных данных примера addEndpoint.][image2]
3. <span data-ttu-id="3290a-132">Вставьте URL-адрес в браузер, чтобы перейти на страницу, содержащую ссылки на справочные статьи о веб-службе.</span><span class="sxs-lookup"><span data-stu-id="3290a-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="3290a-133">Щелкните ссылку **Обновить ресурс**, чтобы открыть страницу справки с информацией об исправлении.</span><span class="sxs-lookup"><span data-stu-id="3290a-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="3290a-134">**Вариант 2: с помощью классического портала Azure**</span><span class="sxs-lookup"><span data-stu-id="3290a-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="3290a-135">Перейдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3290a-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3290a-136">Перейдите на вкладку "Машинное обучение".</span><span class="sxs-lookup"><span data-stu-id="3290a-136">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="3290a-137">![Вкладка "Машинное обучение".][image4]</span><span class="sxs-lookup"><span data-stu-id="3290a-137">![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="3290a-138">Щелкните имя рабочей области, а затем выберите **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="3290a-138">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="3290a-139">Щелкните оценивающую веб-службу, с которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="3290a-139">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="3290a-140">Если вы не изменяли стандартное имя веб-службы, то ее название, скорее всего, заканчивается так: [Scoring Exp.].</span><span class="sxs-lookup"><span data-stu-id="3290a-140">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="3290a-141">Щелкните **Добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="3290a-141">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="3290a-142">После добавления конечной точки щелкните ее имя.</span><span class="sxs-lookup"><span data-stu-id="3290a-142">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="3290a-143">Щелкните **Обновить ресурс** , чтобы открыть страницу справки с информацией об исправлении.</span><span class="sxs-lookup"><span data-stu-id="3290a-143">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="3290a-144">Если вы добавите конечную точку не к прогнозной веб-службе, а к обучающей веб-службе, при выборе ссылки **Обновить ресурс** появится такая ошибка: Sorry, but this feature is not supported or available in this context (К сожалению, эта функция не поддерживается или недоступна в данном контексте).</span><span class="sxs-lookup"><span data-stu-id="3290a-144">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="3290a-145">Эта веб-служба не содержит обновляемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3290a-145">This Web Service has no updatable resources.</span></span> <span data-ttu-id="3290a-146">Приносим извинения за неудобства. Мы работаем над исправлением этого.</span><span class="sxs-lookup"><span data-stu-id="3290a-146">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Панель мониторинга новой конечной точки.][image3]

<span data-ttu-id="3290a-148">Страница исправления содержит URL-адрес исправления, который нужно использовать, и пример кода, с помощью которого можно выполнить вызов.</span><span class="sxs-lookup"><span data-stu-id="3290a-148">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![URL-адрес исправления.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="3290a-150">Проверьте, та ли оценивающая конечная точка обновляется</span><span class="sxs-lookup"><span data-stu-id="3290a-150">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="3290a-151">Исправлять нужно не обучающую, а оценивающую веб-службу.</span><span class="sxs-lookup"><span data-stu-id="3290a-151">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="3290a-152">Исправлять нужно не ту конечную точку, которая используется по умолчанию в веб-службе, а добавленную вами новую конечную точку оценивающей веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3290a-152">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="3290a-153">Чтобы проверить, в какой веб-службе находится конечная точка, посетите классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3290a-153">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="3290a-154">Важно добавить конечную точку к прогнозной веб-службе, а не к обучающей.</span><span class="sxs-lookup"><span data-stu-id="3290a-154">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="3290a-155">Если вы правильно развернули обучающую и прогнозную веб-службы, вы увидите две отдельные веб-службы.</span><span class="sxs-lookup"><span data-stu-id="3290a-155">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="3290a-156">Имя прогнозной веб-службы должно заканчиваться на [predictive exp.].</span><span class="sxs-lookup"><span data-stu-id="3290a-156">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="3290a-157">Перейдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3290a-157">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3290a-158">Перейдите на вкладку "Машинное обучение".</span><span class="sxs-lookup"><span data-stu-id="3290a-158">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="3290a-159">![Пользовательский интерфейс рабочей области машинного обучения.][image4]</span><span class="sxs-lookup"><span data-stu-id="3290a-159">![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="3290a-160">Щелкните рабочую область.</span><span class="sxs-lookup"><span data-stu-id="3290a-160">Select your workspace.</span></span>
4. <span data-ttu-id="3290a-161">Щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="3290a-161">Click **Web Services**.</span></span>
5. <span data-ttu-id="3290a-162">Выберите нужную прогнозную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="3290a-162">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="3290a-163">Проверьте, добавлена ли новая конечная точка к веб-службе.</span><span class="sxs-lookup"><span data-stu-id="3290a-163">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="3290a-164">Чтобы узнать, в правильном ли регионе находится веб-служба, проверьте ее рабочую область.</span><span class="sxs-lookup"><span data-stu-id="3290a-164">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="3290a-165">Перейдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="3290a-165">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="3290a-166">В меню выберите пункт "Машинное обучение".</span><span class="sxs-lookup"><span data-stu-id="3290a-166">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="3290a-167">![Пользовательский интерфейс региона машинного обучения.][image4]</span><span class="sxs-lookup"><span data-stu-id="3290a-167">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="3290a-168">Проверьте расположение своей рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3290a-168">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
