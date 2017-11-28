---
title: "aaaRetrain машинного обучения моделей программным способом | Документы Microsoft"
description: "Узнайте, как tooprogrammatically повторного обучения модели и обновление hello web service toouse hello вновь обученной модели в машинном обучении Azure."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="f8c36-103">Программное переобучение моделей машинного обучения</span><span class="sxs-lookup"><span data-stu-id="f8c36-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="f8c36-104">В этом пошаговом руководстве вы узнаете, как tooprogrammatically обучение машины обучения веб-службы Azure с помощью C# и hello машины обучения Пакетное выполнение службы.</span><span class="sxs-lookup"><span data-stu-id="f8c36-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="f8c36-105">Повторное Обучение модели hello, следующие пошаговые руководства hello отображены как tooupdate hello модели в прогнозирующем веб-службы:</span><span class="sxs-lookup"><span data-stu-id="f8c36-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="f8c36-106">При развертывании классического веб-службы на портале веб-службы обучения машины hello. в разделе [обучение классического веб-службы](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f8c36-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="f8c36-107">Если вы развернули веб-службу, см. раздел [обучение новых веб-службы с помощью командлетов управления обучения машины hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f8c36-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="f8c36-108">Обзор hello переподготовки процесса см. в разделе [Обучение модели машинного обучения](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="f8c36-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="f8c36-109">Если вы хотите toostart с существующие новый диспетчер ресурсов Azure на основе веб-службы см. в разделе [обучение существующих прогнозирующей веб-службы](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f8c36-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="f8c36-110">Создание обучающего эксперимента</span><span class="sxs-lookup"><span data-stu-id="f8c36-110">Create a training experiment</span></span>
<span data-ttu-id="f8c36-111">В этом примере используется «пример 5: обучение теста оценки для двоичной классификации: для взрослых набора данных» из примеров hello машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f8c36-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="f8c36-112">эксперимент hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="f8c36-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="f8c36-113">Войдите с tooMicrosoft студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="f8c36-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="f8c36-114">Щелкните hello нижнем правом углу панели мониторинга hello **New**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="f8c36-115">Выберите 5 образец hello образцы Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f8c36-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="f8c36-116">toorename hello эксперименте вверху hello hello холст эксперимента, выберите имя эксперимента hello «пример 5: обучение теста оценки для двоичной классификации: для взрослых набора данных».</span><span class="sxs-lookup"><span data-stu-id="f8c36-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="f8c36-117">Введите "Модель ценза".</span><span class="sxs-lookup"><span data-stu-id="f8c36-117">Type Census Model.</span></span>
6. <span data-ttu-id="f8c36-118">Внизу hello холст эксперимента hello, нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="f8c36-119">Щелкните **Set Up Web Service** (Настроить веб-службу) и выберите **Retraining Web Service** (Переобучение веб-службы).</span><span class="sxs-lookup"><span data-stu-id="f8c36-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="f8c36-120">Hello ниже показан эксперимент начальной hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-120">hello following shows hello initial experiment.</span></span>
   
   ![Исходный эксперимент][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="f8c36-122">Создание прогнозного эксперимента и его публикация в виде веб-службы</span><span class="sxs-lookup"><span data-stu-id="f8c36-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="f8c36-123">Теперь нужно создать прогнозный эксперимент.</span><span class="sxs-lookup"><span data-stu-id="f8c36-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="f8c36-124">Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы** и выберите **прогнозной веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="f8c36-125">Это сохраняет hello модели как обученной модели и добавляет веб-службы: модули ввода и вывода.</span><span class="sxs-lookup"><span data-stu-id="f8c36-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="f8c36-126">Щелкните **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-126">Click **Run**.</span></span> 
3. <span data-ttu-id="f8c36-127">После эксперимента hello закончит работу, нажмите кнопку **развертывание веб-службы [классический]** или **развертывания [новое] веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="f8c36-128">toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f8c36-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="f8c36-129">Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="f8c36-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="f8c36-130">Развертывание эксперимента обучения hello обучения веб-службы</span><span class="sxs-lookup"><span data-stu-id="f8c36-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="f8c36-131">tooretrain hello обученной модели, необходимо развернуть эксперимента обучения hello, созданный Retraining веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f8c36-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="f8c36-132">Эта веб-служба должна *вывод веб-службы* модуль подключен toohello  *[Обучение модели] [ train-model]*  модуль, может tooproduce toobe новый обученных моделей.</span><span class="sxs-lookup"><span data-stu-id="f8c36-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="f8c36-133">эксперимента обучения toohello tooreturn значок экспериментов hello hello левой панели выберите hello эксперимент с именем модели переписи населения.</span><span class="sxs-lookup"><span data-stu-id="f8c36-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="f8c36-134">В поле поиска поиск элементов эксперимента hello введите веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f8c36-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="f8c36-135">Перетащите *входных данных для службы Web* модуля на hello экспериментов холст и подключения его toohello выходные данные *Очистка недостающих данных* модуля.</span><span class="sxs-lookup"><span data-stu-id="f8c36-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="f8c36-136">Это гарантирует, что цикл данных обрабатывается hello таким же, как и исходный обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="f8c36-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="f8c36-137">Перетащите два *веб-службы вывода* модулей на hello поэкспериментировать холста.</span><span class="sxs-lookup"><span data-stu-id="f8c36-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="f8c36-138">Подсоедините hello выход hello *Обучение модели* модуль tooone и hello выходные данные hello *модель оценки* модуль toohello других.</span><span class="sxs-lookup"><span data-stu-id="f8c36-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="f8c36-139">Здравствуйте, вывод службы web для **Обучение модели** дает нам hello новой обученной модели.</span><span class="sxs-lookup"><span data-stu-id="f8c36-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="f8c36-140">Здравствуйте, выходных данных, вложенные слишком**модель оценки** возвращает выходных этого модуля, который является результаты производительности hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="f8c36-141">Щелкните **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-141">Click **Run**.</span></span> 

<span data-ttu-id="f8c36-142">Далее необходимо развернуть эксперимента обучения hello как веб-службу, которая создает обученной модели и результаты оценки модели.</span><span class="sxs-lookup"><span data-stu-id="f8c36-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="f8c36-143">tooaccomplish это ваш следующий набор действий зависят от используемой классического веб-службы или веб-службу.</span><span class="sxs-lookup"><span data-stu-id="f8c36-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="f8c36-144">**Классическая веб-служба**</span><span class="sxs-lookup"><span data-stu-id="f8c36-144">**Classic web service**</span></span>

<span data-ttu-id="f8c36-145">Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы** и выберите **развертывание веб-службы [классический]**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="f8c36-146">Hello веб-службы **мониторинга** отображается страница справки hello ключ API и hello API для пакетного обновления.</span><span class="sxs-lookup"><span data-stu-id="f8c36-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="f8c36-147">Только hello способ выполнения пакета можно использовать для создания обученных моделей.</span><span class="sxs-lookup"><span data-stu-id="f8c36-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="f8c36-148">**Новая веб-служба**</span><span class="sxs-lookup"><span data-stu-id="f8c36-148">**New web service**</span></span>

<span data-ttu-id="f8c36-149">Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы** и выберите **развертывания [новое] веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="f8c36-150">портал веб-службы Web службы Azure Machine Learning Hello открывается страница toohello развернуть веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f8c36-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="f8c36-151">Введите имя веб-службы и выберите план платежей, а затем нажмите кнопку **Deploy**(Развернуть).</span><span class="sxs-lookup"><span data-stu-id="f8c36-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="f8c36-152">Только hello способ выполнения пакета можно использовать для создания обученных моделей</span><span class="sxs-lookup"><span data-stu-id="f8c36-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="f8c36-153">В любом случае после завершения выполнения эксперимента hello полученный рабочий процесс должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f8c36-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![Итоговый рабочий процесс после выполнения][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="f8c36-155">Обучение модели hello новыми данными, с помощью СРЕД</span><span class="sxs-lookup"><span data-stu-id="f8c36-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="f8c36-156">Например вы используете C# toocreate hello переподготовки приложения.</span><span class="sxs-lookup"><span data-stu-id="f8c36-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="f8c36-157">Также можно hello Python или R образец кода tooaccomplish этой задачи.</span><span class="sxs-lookup"><span data-stu-id="f8c36-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="f8c36-158">toocall hello переподготовки API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="f8c36-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="f8c36-159">Создайте консольное приложение C# в Visual Studio (**Создать** > **Проект** > **Visual C#** > **Классический рабочий стол Windows** > **Консольное приложение (.NET Framework**).</span><span class="sxs-lookup"><span data-stu-id="f8c36-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="f8c36-160">Войдите в систему toohello портала машины обучения веб-службы.</span><span class="sxs-lookup"><span data-stu-id="f8c36-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="f8c36-161">Если вы работаете с классической веб-службой, щелкните **Classic Web Services**(Классические веб-службы).</span><span class="sxs-lookup"><span data-stu-id="f8c36-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="f8c36-162">Щелкните hello веб-службы, которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="f8c36-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="f8c36-163">Щелкните конечную точку по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="f8c36-164">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="f8c36-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="f8c36-165">Внизу hello hello **использование** страницы в hello **образец кода** щелкните **пакета**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="f8c36-166">По-прежнему toostep 5 этой процедуры.</span><span class="sxs-lookup"><span data-stu-id="f8c36-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="f8c36-167">Если вы работаете с новой веб-службой, щелкните **Web Services**(Веб-службы).</span><span class="sxs-lookup"><span data-stu-id="f8c36-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="f8c36-168">Щелкните hello веб-службы, которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="f8c36-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="f8c36-169">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="f8c36-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="f8c36-170">Hello нижней части страницы Consume hello в hello **образец кода** щелкните **пакета**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="f8c36-171">Скопируйте hello пример кода C# для пакетного выполнения и вставьте его в файл Program.cs hello, убедившись, что пространство имен hello остается без изменений.</span><span class="sxs-lookup"><span data-stu-id="f8c36-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="f8c36-172">Добавьте пакет Nuget hello Microsoft.AspNet.WebApi.Client, как указано в комментариях hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="f8c36-173">tooMicrosoft.WindowsAzure.Storage.dll ссылки tooadd hello, сначала для может потребоваться tooinstall hello клиентской библиотеки службы хранилища Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f8c36-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="f8c36-174">Дополнительные сведения см. в документации о [Службе хранилища Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="f8c36-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="f8c36-175">Обновление декларации apikey hello</span><span class="sxs-lookup"><span data-stu-id="f8c36-175">Update hello apikey declaration</span></span>
<span data-ttu-id="f8c36-176">Найдите hello **apikey** объявления.</span><span class="sxs-lookup"><span data-stu-id="f8c36-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="f8c36-177">В hello **потребления основные сведения о** раздел hello **использование** найдите hello первичный ключ и скопируйте его toohello **apikey** объявления.</span><span class="sxs-lookup"><span data-stu-id="f8c36-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="f8c36-178">Обновить сведения о хранилище Azure hello</span><span class="sxs-lookup"><span data-stu-id="f8c36-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="f8c36-179">Hello BES образец кода отправляет файл с локального диска (например, «C:\temp\CensusIpnput.csv») tooAzure хранилища, обрабатывает его и записывает hello результаты назад tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="f8c36-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="f8c36-180">tooaccomplish этой задачи необходимо получить hello данных учетной записи хранения имя ключа и контейнер для вашей учетной записи хранения из классического портала Azure hello и соответствующие значения в коде hello обновления hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="f8c36-181">Войдите на классический портал Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="f8c36-182">В столбце hello навигации слева щелкните **хранения**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="f8c36-183">Из списка hello учетных записей хранения выберите один toostore hello повторное Обучение модели.</span><span class="sxs-lookup"><span data-stu-id="f8c36-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="f8c36-184">Внизу hello страницы приветствия щелкните **управление ключами доступа**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="f8c36-185">Скопируйте и сохраните hello **первичный ключ доступа** и hello закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="f8c36-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="f8c36-186">В начале hello страницы приветствия, нажмите кнопку **контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="f8c36-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="f8c36-187">Выберите существующий контейнер или создайте новую и сохраните имя hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="f8c36-188">Найдите hello *StorageAccountName*, *StorageAccountKey*, и *StorageContainerName* объявления и обновлять значения hello, сохраненный при выполнении hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f8c36-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="f8c36-189">Также необходимо убедиться, что входной файл hello доступен в месте hello, указанных в коде hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="f8c36-190">Укажите расположение выходных данных hello</span><span class="sxs-lookup"><span data-stu-id="f8c36-190">Specify hello output location</span></span>
<span data-ttu-id="f8c36-191">При указании расположения вывода hello в полезных данных запроса hello, hello расширение файла hello, указанный в *RelativeLocation* должен быть указан как ilearner.</span><span class="sxs-lookup"><span data-stu-id="f8c36-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="f8c36-192">См. следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="f8c36-193">имена Hello вашего расположения вывода может отличаться от hello в этом пошаговом руководстве на основе hello порядка добавления hello веб-службы вывода модули в.</span><span class="sxs-lookup"><span data-stu-id="f8c36-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="f8c36-194">Поскольку настройка этого эксперимента обучения с двумя выходами, hello результаты содержат сведения о расположении хранилища для них.</span><span class="sxs-lookup"><span data-stu-id="f8c36-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![Выходные данные переобучения][6]

<span data-ttu-id="f8c36-196">Схема 4. Выходные данные переобучения</span><span class="sxs-lookup"><span data-stu-id="f8c36-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="f8c36-197">Оценка результатов переподготовки hello</span><span class="sxs-lookup"><span data-stu-id="f8c36-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="f8c36-198">При запуске приложения hello hello выходные данные содержат hello URL-адрес и маркера необходимые tooaccess SAS hello результаты оценки.</span><span class="sxs-lookup"><span data-stu-id="f8c36-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="f8c36-199">Можно просмотреть результаты производительности hello hello повторное Обучение модели путем объединения hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken* из hello выходных результатов для *output2* (как показано в предыдущем переподготовки изображения вывода hello) и вставка hello полный URL-адрес в адресной строке браузера hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="f8c36-200">Проверьте результаты toodetermine hello ли вновь обученной модели hello выполняет также достаточно hello tooreplace один существующий.</span><span class="sxs-lookup"><span data-stu-id="f8c36-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="f8c36-201">Копировать hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken* из hello выходные результаты, будет использовать их во время процесса переподготовки hello.</span><span class="sxs-lookup"><span data-stu-id="f8c36-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8c36-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8c36-202">Next steps</span></span>
<span data-ttu-id="f8c36-203">При развертывании hello прогнозирующей веб-службы, щелкнув **развертывание веб-службы [классический]**, в разделе [обучение классического веб-службы](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f8c36-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="f8c36-204">При развертывании hello прогнозирующей веб-службы, щелкнув **развертывания [новое] веб-службы**, см. [обучение новых веб-службы с помощью командлетов управления обучения машины hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f8c36-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
