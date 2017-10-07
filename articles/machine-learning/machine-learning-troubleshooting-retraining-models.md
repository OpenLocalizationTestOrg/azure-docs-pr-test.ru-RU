---
title: "aaaTroubleshoot переподготовки Azure Machine Learning классического веб-службы | Документы Microsoft"
description: "Определить и устранить распространенные проблемы обнаружено при переподготовки модели hello Azure Machine Learning веб-службы."
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
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="4d939-103">Устранение неполадок hello переподготовки машины Azure обучения классического веб-службы</span><span class="sxs-lookup"><span data-stu-id="4d939-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="4d939-104">Сведения о повторном обучении</span><span class="sxs-lookup"><span data-stu-id="4d939-104">Retraining overview</span></span>
<span data-ttu-id="4d939-105">Когда вы развертываете прогнозный эксперимент в качестве оценивающей веб-службы, вы получаете статическую модель.</span><span class="sxs-lookup"><span data-stu-id="4d939-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="4d939-106">По мере появления новых данных или hello потребитель hello API имеет свои собственные данные модели hello должен toobe обучить повторно.</span><span class="sxs-lookup"><span data-stu-id="4d939-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="4d939-107">Полное Пошаговое руководство hello переподготовки процесса классического веб-службы см. в разделе [обучение машины обучения моделей программным способом](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="4d939-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="4d939-108">Процесс повторного обучения</span><span class="sxs-lookup"><span data-stu-id="4d939-108">Retraining process</span></span>
<span data-ttu-id="4d939-109">Если вам требуется tooretrain hello веб-службы, необходимо добавить некоторые дополнительные элементы:</span><span class="sxs-lookup"><span data-stu-id="4d939-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="4d939-110">Веб-служба, развернутых из hello эксперимента обучения.</span><span class="sxs-lookup"><span data-stu-id="4d939-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="4d939-111">должен иметь эксперимента Hello **вывод веб-службы** модуль присоединенного выходные данные toohello hello **Обучение модели** модуля.</span><span class="sxs-lookup"><span data-stu-id="4d939-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Присоедините Обучение модели toohello вывода hello веб-служб.][image1]
* <span data-ttu-id="4d939-113">Новая конечная точка добавлен tooyour оценки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="4d939-114">Добавить конечную точку hello можно программным образом с использованием примера кода hello, на которые ссылается hello машинного обучения, повторного обучения моделей программным способом раздела или с помощью классического портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d939-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="4d939-115">Затем можно использовать hello пример кода C# из модели tooretrain страницы справки API hello обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="4d939-116">После оценивал результаты hello и их пригодности обновлении hello обученной модели оценки с помощью hello новую конечную точку, которая была добавлена веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="4d939-117">С все составляющие hello в месте hello основных шагов, необходимо выполнить tooretrain модели hello связаны следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4d939-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="4d939-118">Вызовите hello обучения веб-службы: hello вызовов toohello службы пакетного выполнения (BES), не hello запроса ответа службы (RR).</span><span class="sxs-lookup"><span data-stu-id="4d939-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="4d939-119">При вызове функции hello toomake страницы справки hello API можно использовать hello пример кода C#.</span><span class="sxs-lookup"><span data-stu-id="4d939-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="4d939-120">Найти значение hello для hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken*: эти значения возвращаются в выходных данных hello из вашего вызова toohello обучения веб Служба.</span><span class="sxs-lookup"><span data-stu-id="4d939-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="4d939-121">![отображая выходные данные hello hello переподготовки образец и hello BaseLocation, RelativeLocation и SasBlobToken значения.][image6]</span><span class="sxs-lookup"><span data-stu-id="4d939-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="4d939-122">Обновление hello добавить конечную точку из hello новые оценки веб-службы с hello обученной модели: с использованием примера кода hello, входящем в hello обучение машинного обучения моделей программным способом, обновить hello новой конечной точки добавлены toohello вновь оценки модели с hello обученной модели из hello обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="4d939-123">Распространенные затруднения</span><span class="sxs-lookup"><span data-stu-id="4d939-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="4d939-124">Проверьте toosee при наличии hello исправьте ИСПРАВЛЕНИЯ URL-адрес</span><span class="sxs-lookup"><span data-stu-id="4d939-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="4d939-125">Hello ИСПРАВЛЕНИЯ URL-адрес используется должен быть связан с hello hello новой конечной точки оценки вы добавили toohello оценки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="4d939-126">Существует ряд способов tooobtain hello ИСПРАВЛЕНИЯ URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="4d939-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="4d939-127">**Вариант 1: программно**</span><span class="sxs-lookup"><span data-stu-id="4d939-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="4d939-128">tooget hello исправьте ИСПРАВЛЕНИЯ URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="4d939-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="4d939-129">Запустите hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) пример кода.</span><span class="sxs-lookup"><span data-stu-id="4d939-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="4d939-130">Из вывода hello AddEndpoint, найти hello *HelpLocation* значение и скопируйте URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="4d939-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation в выходных данных hello addEndpoint образца hello.][image2]
3. <span data-ttu-id="4d939-132">Вставьте URL-адрес hello в браузере страницу tooa toonavigate, предоставляющий ссылки на справку для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="4d939-133">Нажмите кнопку hello **обновления ресурса** страницы справки исправления hello tooopen ссылку.</span><span class="sxs-lookup"><span data-stu-id="4d939-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="4d939-134">**Вариант 2: Использование hello классический портал Azure**</span><span class="sxs-lookup"><span data-stu-id="4d939-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="4d939-135">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4d939-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4d939-136">Привет открыть вкладку машинного обучения. ![Вкладка "Машинное обучение".][image4]</span><span class="sxs-lookup"><span data-stu-id="4d939-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="4d939-137">Щелкните имя рабочей области, а затем выберите **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="4d939-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="4d939-138">Щелкните hello оценки веб-службы, которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="4d939-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="4d939-139">(Если не удалось изменить имя по умолчанию hello hello веб-службы, он будет помещен в [Exp оценки.].)</span><span class="sxs-lookup"><span data-stu-id="4d939-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="4d939-140">Щелкните **Добавить конечную точку**.</span><span class="sxs-lookup"><span data-stu-id="4d939-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="4d939-141">После добавления конечной точки hello, щелкните имя конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="4d939-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="4d939-142">Нажмите кнопку **обновления ресурса** tooopen hello исправления страницы справки.</span><span class="sxs-lookup"><span data-stu-id="4d939-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="4d939-143">При добавлении конечной точки hello toohello обучения веб-службы вместо hello прогнозной веб-службы, появится следующая ошибка при нажатии кнопки hello hello **обновления ресурса** ссылку: к сожалению, но эта функция не поддерживается или доступные в данном контексте.</span><span class="sxs-lookup"><span data-stu-id="4d939-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="4d939-144">Эта веб-служба не содержит обновляемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4d939-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="4d939-145">Мы приносим свои извинения за неудобства hello и работают на улучшение этот рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="4d939-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Панель мониторинга новой конечной точки.][image3]

<span data-ttu-id="4d939-147">страницы справки ИСПРАВЛЕНИЯ Hello содержит hello исправление для URL-адреса необходимо использовать и примеры кода можно использовать toocall его.</span><span class="sxs-lookup"><span data-stu-id="4d939-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![URL-адрес исправления.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="4d939-149">Проверьте toosee, что выполняется обновление конечной точки оценки правильный hello</span><span class="sxs-lookup"><span data-stu-id="4d939-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="4d939-150">Не patch hello обучения веб-службы: hello исправление операция должна выполняться на hello оценки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="4d939-151">Не исправление для конечной точки по умолчанию hello в веб-службы: hello исправление операция должна выполняться на новые оценки конечной веб-службы, которая была добавлена hello.</span><span class="sxs-lookup"><span data-stu-id="4d939-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="4d939-152">Вы можете проверить, какие hello конечной веб-службы включена по обходу hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4d939-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="4d939-153">Убедитесь, что вы добавляете toohello hello конечную точку прогнозируемого веб-службы, hello обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="4d939-154">Если вы правильно развернули обучающую и прогнозную веб-службы, вы увидите две отдельные веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="4d939-155">Hello прогнозной веб-службы должно заканчиваться «[прогнозной exp.]».</span><span class="sxs-lookup"><span data-stu-id="4d939-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="4d939-156">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4d939-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4d939-157">Привет открыть вкладку машинного обучения. ![Пользовательский интерфейс рабочей области машинного обучения.][image4]</span><span class="sxs-lookup"><span data-stu-id="4d939-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="4d939-158">Щелкните рабочую область.</span><span class="sxs-lookup"><span data-stu-id="4d939-158">Select your workspace.</span></span>
4. <span data-ttu-id="4d939-159">Щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="4d939-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="4d939-160">Выберите нужную прогнозную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="4d939-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="4d939-161">Убедитесь, что новой конечной точкой, добавлено toohello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4d939-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="4d939-162">Проверьте hello рабочее пространство, веб-службу в tooensure, где находится необходимый регион hello</span><span class="sxs-lookup"><span data-stu-id="4d939-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="4d939-163">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4d939-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4d939-164">Выберите меню hello машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="4d939-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="4d939-165">![Пользовательский интерфейс региона машинного обучения.][image4]</span><span class="sxs-lookup"><span data-stu-id="4d939-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="4d939-166">Проверьте расположение hello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="4d939-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
