---
title: "Программное переобучение моделей машинного обучения | Документация Майкрософт"
description: "Узнайте о том, как осуществить программное переобучение модели и обновить веб-службу так, чтобы она использовала переобученную модель при задействовании функций машинного обучения Azure."
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
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="238d0-103">Программное переобучение моделей машинного обучения</span><span class="sxs-lookup"><span data-stu-id="238d0-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="238d0-104">В этом пошаговом руководстве вы узнаете, как выполнить программное переобучение веб-службы машинного обучения Azure с использованием C# и службы пакетного выполнения машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="238d0-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="238d0-105">Следующие руководства содержат инструкции по обновлению модели в прогнозной веб-службе после переобучения модели.</span><span class="sxs-lookup"><span data-stu-id="238d0-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="238d0-106">Если вы ранее развернули классическую веб-службу на портале веб-служб машинного обучения, изучите статью [Переобучение классической веб-службы](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="238d0-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="238d0-107">Если вы используете новую веб-службу, см. статью [Переобучение новой веб-службы с помощью командлетов управления PowerShell машинного обучения](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="238d0-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="238d0-108">Сам процесс повторного обучения описан в статье [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md) (Переобучение модели машинного обучения).</span><span class="sxs-lookup"><span data-stu-id="238d0-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="238d0-109">Если вы работаете с уже существующей веб-службой на основе Azure Resource Manager, см. статью [Retrain an existing Predictive Web service](machine-learning-retrain-existing-resource-manager-based-web-service.md) (Переобучение существующей прогнозной веб-службы).</span><span class="sxs-lookup"><span data-stu-id="238d0-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="238d0-110">Создание обучающего эксперимента</span><span class="sxs-lookup"><span data-stu-id="238d0-110">Create a training experiment</span></span>
<span data-ttu-id="238d0-111">В этой статье используется пример "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" (Образец 5. Обучение, тестирование, анализ для классификации бинарных файлов: набор данных с содержимым для взрослых) из каталога образцов Машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="238d0-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="238d0-112">Чтобы создать эксперимент:</span><span class="sxs-lookup"><span data-stu-id="238d0-112">To create the experiment:</span></span>

1. <span data-ttu-id="238d0-113">Войдите в Студию машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="238d0-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="238d0-114">В нижнем правом углу панели мониторинга щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="238d0-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="238d0-115">В списке образцов Майкрософт выберите образец 5.</span><span class="sxs-lookup"><span data-stu-id="238d0-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="238d0-116">Чтобы переименовать эксперимент, в верхней части холста эксперимента выберите имя эксперимента "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" (Образец 5. Обучение, тестирование, анализ для классификации бинарных файлов: набор данных с содержимым для взрослых).</span><span class="sxs-lookup"><span data-stu-id="238d0-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="238d0-117">Введите "Модель ценза".</span><span class="sxs-lookup"><span data-stu-id="238d0-117">Type Census Model.</span></span>
6. <span data-ttu-id="238d0-118">В нижней части холста эксперимента нажмите кнопку **Run**(Выполнить).</span><span class="sxs-lookup"><span data-stu-id="238d0-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="238d0-119">Щелкните **Set Up Web Service** (Настроить веб-службу) и выберите **Retraining Web Service** (Переобучение веб-службы).</span><span class="sxs-lookup"><span data-stu-id="238d0-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="238d0-120">Ниже приведен исходный эксперимент.</span><span class="sxs-lookup"><span data-stu-id="238d0-120">The following shows the initial experiment.</span></span>
   
   ![Исходный эксперимент][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="238d0-122">Создание прогнозного эксперимента и его публикация в виде веб-службы</span><span class="sxs-lookup"><span data-stu-id="238d0-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="238d0-123">Теперь нужно создать прогнозный эксперимент.</span><span class="sxs-lookup"><span data-stu-id="238d0-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="238d0-124">В нижней части холста эксперимента щелкните **Set Up Web Service** (Настроить веб-службу) и выберите **Predictive Web Service** (Прогнозная веб-служба).</span><span class="sxs-lookup"><span data-stu-id="238d0-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="238d0-125">При этом модель сохраняется в качестве обученной и добавляются модули входных и выходных данных веб-службы.</span><span class="sxs-lookup"><span data-stu-id="238d0-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="238d0-126">Щелкните **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="238d0-126">Click **Run**.</span></span> 
3. <span data-ttu-id="238d0-127">Когда эксперимент будет выполнен, щелкните **Deploy Web Service [Classic]** (Развернуть веб-службу [классическую]) или **Deploy Web Service [New]** (Развернуть веб-службу [новую]).</span><span class="sxs-lookup"><span data-stu-id="238d0-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="238d0-128">Для развертывания новой веб-службы у вас должен быть достаточный уровень разрешений в подписке, в которую выполняется развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="238d0-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="238d0-129">Дополнительные сведения см. в статье [Управление веб-службой с помощью портала веб-служб машинного обучения Azure](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="238d0-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="238d0-130">Развертывание обучающего эксперимента в качестве обучающей веб-службы</span><span class="sxs-lookup"><span data-stu-id="238d0-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="238d0-131">Чтобы переобучить обученную модель, необходимо развернуть обучающий эксперимент, созданный в качестве веб-службы переобучения.</span><span class="sxs-lookup"><span data-stu-id="238d0-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="238d0-132">Для создания обученных моделей этой веб-службе потребуется модуль *Web Service Output* (Выходные данные веб-службы), подключенный к модулю *[Обучение модели][train-model]*.</span><span class="sxs-lookup"><span data-stu-id="238d0-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="238d0-133">Чтобы вернуться в обучающий эксперимент, щелкните значок "Эксперименты" на левой панели, а затем выберите эксперимент "Модель ценза".</span><span class="sxs-lookup"><span data-stu-id="238d0-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="238d0-134">В поле поиска "Search Experiment Items" (Поиск элементов эксперимента) введите "Web service".</span><span class="sxs-lookup"><span data-stu-id="238d0-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="238d0-135">Перетащите модуль *входных данных веб-службы* на холст эксперимента и присоедините его вывод к модулю *Очистка недостающих данных*.</span><span class="sxs-lookup"><span data-stu-id="238d0-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="238d0-136">Это гарантирует, что данные для переобучения будут обработаны так же, как исходный набор обучающих данных.</span><span class="sxs-lookup"><span data-stu-id="238d0-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="238d0-137">Перетащите два модуля *Web service Output* (Выходные данные веб-службы) на холст эксперимента.</span><span class="sxs-lookup"><span data-stu-id="238d0-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="238d0-138">Присоедините к одному из них вывод модуля *Обучение модели*, а к другому — вывод модуля *Анализ модели*.</span><span class="sxs-lookup"><span data-stu-id="238d0-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="238d0-139">Выходные данные веб-службы для модуля **Train Model** (Обучение модели) позволяют создать обученную модель.</span><span class="sxs-lookup"><span data-stu-id="238d0-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="238d0-140">Выходные данные, прикрепленные к модулю **Анализ модели**, возвращают результаты анализа, подготовленные модулем.</span><span class="sxs-lookup"><span data-stu-id="238d0-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="238d0-141">Щелкните **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="238d0-141">Click **Run**.</span></span> 

<span data-ttu-id="238d0-142">Затем необходимо развернуть обучающий эксперимент в качестве веб-службы, которая создает обученную модель и результаты ее оценки.</span><span class="sxs-lookup"><span data-stu-id="238d0-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="238d0-143">Для этого необходимо выполнить действия, которые зависят от того, как развернут эксперимент: как классическая веб-служба или как новая веб-служба.</span><span class="sxs-lookup"><span data-stu-id="238d0-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="238d0-144">**Классическая веб-служба**</span><span class="sxs-lookup"><span data-stu-id="238d0-144">**Classic web service**</span></span>

<span data-ttu-id="238d0-145">В нижней части холста эксперимента щелкните **Set Up Web Service** (Настроить веб-службу) и выберите **Deploy Web Service [Classic]** (Развернуть веб-службу [классическую]).</span><span class="sxs-lookup"><span data-stu-id="238d0-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="238d0-146">**Панель мониторинга** веб-службы отображается с ключом API и страницей справки API для пакетного выполнения.</span><span class="sxs-lookup"><span data-stu-id="238d0-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="238d0-147">Для создания обученных моделей может использоваться только метод пакетного выполнения.</span><span class="sxs-lookup"><span data-stu-id="238d0-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="238d0-148">**Новая веб-служба**</span><span class="sxs-lookup"><span data-stu-id="238d0-148">**New web service**</span></span>

<span data-ttu-id="238d0-149">В нижней части холста эксперимента щелкните **Set Up Web Service** (Настроить веб-службу) и выберите **Deploy Web Service [New]** (Развернуть веб-службу [новую]).</span><span class="sxs-lookup"><span data-stu-id="238d0-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="238d0-150">Портал веб-служб машинного обучения Azure откроется на странице "Deploy Web service" (Развертывание веб-службы).</span><span class="sxs-lookup"><span data-stu-id="238d0-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="238d0-151">Введите имя веб-службы и выберите план платежей, а затем нажмите кнопку **Deploy**(Развернуть).</span><span class="sxs-lookup"><span data-stu-id="238d0-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="238d0-152">Для создания обученных моделей может использоваться только метод пакетного выполнения.</span><span class="sxs-lookup"><span data-stu-id="238d0-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="238d0-153">В любом случае, после завершения эксперимента итоговый рабочий процесс должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="238d0-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![Итоговый рабочий процесс после выполнения][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="238d0-155">Переобучение модели с использованием новых данных и BES</span><span class="sxs-lookup"><span data-stu-id="238d0-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="238d0-156">В этом примере вы создадите приложение повторного обучения на языке C#.</span><span class="sxs-lookup"><span data-stu-id="238d0-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="238d0-157">Также для этих целей можно использовать образцы кода на R или Python.</span><span class="sxs-lookup"><span data-stu-id="238d0-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="238d0-158">Чтобы вызвать интерфейсы API:</span><span class="sxs-lookup"><span data-stu-id="238d0-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="238d0-159">Создайте консольное приложение C# в Visual Studio (**Создать** > **Проект** > **Visual C#** > **Классический рабочий стол Windows** > **Консольное приложение (.NET Framework**).</span><span class="sxs-lookup"><span data-stu-id="238d0-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="238d0-160">Войдите на портал веб-служб Машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="238d0-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="238d0-161">Если вы работаете с классической веб-службой, щелкните **Classic Web Services**(Классические веб-службы).</span><span class="sxs-lookup"><span data-stu-id="238d0-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="238d0-162">Щелкните веб-службу, с которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="238d0-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="238d0-163">Щелкните конечную точку по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="238d0-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="238d0-164">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="238d0-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="238d0-165">В нижней части страницы **Consume** (Использование) в разделе **Sample Code** (Пример кода) щелкните **Batch** (Пакет).</span><span class="sxs-lookup"><span data-stu-id="238d0-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="238d0-166">Перейдите к шагу 5 этой процедуры.</span><span class="sxs-lookup"><span data-stu-id="238d0-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="238d0-167">Если вы работаете с новой веб-службой, щелкните **Web Services**(Веб-службы).</span><span class="sxs-lookup"><span data-stu-id="238d0-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="238d0-168">Щелкните веб-службу, с которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="238d0-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="238d0-169">Щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="238d0-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="238d0-170">В нижней части страницы использования в разделе **Sample Code** (Пример кода) щелкните **Batch** (Пакет).</span><span class="sxs-lookup"><span data-stu-id="238d0-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="238d0-171">Скопируйте пример кода на C# для пакетного выполнения и вставьте его в файл Program.cs, убедившись, что пространство имен остается в неизменном виде.</span><span class="sxs-lookup"><span data-stu-id="238d0-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="238d0-172">Добавьте пакет Nuget Microsoft.AspNet.WebApi.Client, как указано в комментариях.</span><span class="sxs-lookup"><span data-stu-id="238d0-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="238d0-173">Чтобы добавить ссылку на файл Microsoft.WindowsAzure.Storage.dll, может потребоваться сначала установить клиентскую библиотеку для служб хранилища Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="238d0-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="238d0-174">Дополнительные сведения см. в документации о [Службе хранилища Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="238d0-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="238d0-175">Обновление объявления apiKey</span><span class="sxs-lookup"><span data-stu-id="238d0-175">Update the apikey declaration</span></span>
<span data-ttu-id="238d0-176">Найдите объявление **apiKey** .</span><span class="sxs-lookup"><span data-stu-id="238d0-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="238d0-177">В разделе **Basic consumption info** (Основные сведения об использовании) на странице **Consume** (Использование) найдите первичный ключ и скопируйте его в объявление **apiKey**.</span><span class="sxs-lookup"><span data-stu-id="238d0-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="238d0-178">Обновление сведений о службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="238d0-178">Update the Azure Storage information</span></span>
<span data-ttu-id="238d0-179">Пример кода BES отправляет файл из локального диска (например, C:\temp\CensusIpnput.csv) в службу хранилища Azure, обрабатывает его и записывает результаты обратно в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="238d0-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="238d0-180">Для этого нужно получить имя учетной записи хранения, ключ и сведения о контейнере для вашей учетной записи хранения на классическом портале Azure, а затем обновить соответствующие значения в коде.</span><span class="sxs-lookup"><span data-stu-id="238d0-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="238d0-181">Войдите на классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="238d0-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="238d0-182">В левой области навигации щелкните **Хранилище**.</span><span class="sxs-lookup"><span data-stu-id="238d0-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="238d0-183">Выберите в списке учетную запись хранения, которая будет использоваться для хранения переобученной модели.</span><span class="sxs-lookup"><span data-stu-id="238d0-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="238d0-184">В нижней части страницы щелкните **Управление ключами доступа**.</span><span class="sxs-lookup"><span data-stu-id="238d0-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="238d0-185">Скопируйте и сохраните **Первичный ключ доступа** , а затем закройте диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="238d0-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="238d0-186">В верхней части страницы щелкните **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="238d0-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="238d0-187">Выберите существующий контейнер или создайте новый и сохраните его имя.</span><span class="sxs-lookup"><span data-stu-id="238d0-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="238d0-188">Найдите объявления *StorageAccountName*, *StorageAccountKey* и *StorageContainerName* и обновите их, используя значения, взятые с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="238d0-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="238d0-189">Кроме этого, необходимо обеспечить доступность файла входных данных в расположении, указанном в коде.</span><span class="sxs-lookup"><span data-stu-id="238d0-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="238d0-190">Указание расположения выходных данных</span><span class="sxs-lookup"><span data-stu-id="238d0-190">Specify the output location</span></span>
<span data-ttu-id="238d0-191">В описании расположения выходных данных, указанном в полезных данных запроса, указанный в параметре *RelativeLocation* файл должен иметь расширение ilearner.</span><span class="sxs-lookup"><span data-stu-id="238d0-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="238d0-192">Как в этом примере:</span><span class="sxs-lookup"><span data-stu-id="238d0-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="238d0-193">Имена расположений для выходных данных могут отличаться от указанных в этом пошаговом руководстве в зависимости от того, в каком порядке добавлены модули выходных данных веб-службы.</span><span class="sxs-lookup"><span data-stu-id="238d0-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="238d0-194">Так как для этого обучающего эксперимента настроены два вывода, в результатах будет содержаться информация о расположении хранения для обоих выводов.</span><span class="sxs-lookup"><span data-stu-id="238d0-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![Выходные данные переобучения][6]

<span data-ttu-id="238d0-196">Схема 4. Выходные данные переобучения</span><span class="sxs-lookup"><span data-stu-id="238d0-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="238d0-197">Анализ результатов переобучения</span><span class="sxs-lookup"><span data-stu-id="238d0-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="238d0-198">При выполнении приложения выходные данные содержат URL-адрес и маркер SAS, необходимые для доступа к результатам оценки.</span><span class="sxs-lookup"><span data-stu-id="238d0-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="238d0-199">Чтобы увидеть результаты работы переобученной модели, введите в адресную строку браузера полный URL-адрес, составленный из значений параметров *BaseLocation*, *RelativeLocaiton* и *SasBlobToken*, содержащихся в выходных данных *output2* (как показано на изображении выше).</span><span class="sxs-lookup"><span data-stu-id="238d0-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="238d0-200">Проанализируйте результаты и определите, достаточно ли хорошо работает только что обученная модель, чтобы заменить имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="238d0-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="238d0-201">В полученных выходных данных скопируйте значения параметров *BaseLocation*, *RelativeLocation* и *SasBlobToken*. Они вам потребуются в процессе переобучения.</span><span class="sxs-lookup"><span data-stu-id="238d0-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="238d0-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="238d0-202">Next steps</span></span>
<span data-ttu-id="238d0-203">Если вы развернули прогнозную веб-службу с помощью команды **Deploy Web Service [Classic]** (Развернуть веб-службу [классическую]), см. статью [Переобучение классической веб-службы](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="238d0-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="238d0-204">Если вы развернули прогнозную веб-службу с помощью команды **Deploy Web Service [New]** (Развернуть веб-службу [новую]), см. статью [Переобучение новой веб-службы с помощью командлетов управления PowerShell машинного обучения](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="238d0-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
