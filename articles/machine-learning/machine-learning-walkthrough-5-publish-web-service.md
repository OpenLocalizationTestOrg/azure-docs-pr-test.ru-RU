---
title: "Шаг 5. Развертывание веб-службы машинного обучения | Документация Майкрософт"
description: "Шаг 5 пошагового руководства по разработке прогностического решения. Развертывание прогностического эксперимента в студии машинного обучения в качестве веб-службы."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 3fca74a3-c44b-4583-a218-c14c46ee5338
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cec1bcceea158a20742c7019a266dcefaac4c9cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-5-deploy-the-azure-machine-learning-web-service"></a><span data-ttu-id="a3c56-103">Шаг 5. Развертывание веб-службы машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="a3c56-103">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>
<span data-ttu-id="a3c56-104">Это пятый этап пошагового руководства [Разработка решения для прогнозной аналитики в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="a3c56-104">This is the fifth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="a3c56-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a3c56-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="a3c56-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="a3c56-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="a3c56-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="a3c56-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="a3c56-108">Обучение и анализ моделей</span><span class="sxs-lookup"><span data-stu-id="a3c56-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="a3c56-109">**Развертывание веб-службы**</span><span class="sxs-lookup"><span data-stu-id="a3c56-109">**Deploy the web service**</span></span>
6. [<span data-ttu-id="a3c56-110">Доступ к веб-службе</span><span class="sxs-lookup"><span data-stu-id="a3c56-110">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="a3c56-111">Чтобы другие пользователи могли применить прогнозную модель, которую мы создали в этом руководстве, мы развернем ее как веб-службу в Azure.</span><span class="sxs-lookup"><span data-stu-id="a3c56-111">To give others a chance to use the predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="a3c56-112">Вплоть до этого момента мы экспериментировали с обучением нашей модели.</span><span class="sxs-lookup"><span data-stu-id="a3c56-112">Up to this point we've been experimenting with training our model.</span></span> <span data-ttu-id="a3c56-113">Но развернутая служба больше не будет обучаться. Теперь она создает новые прогнозы на основе нашей модели, оценивая введенные пользователем данные.</span><span class="sxs-lookup"><span data-stu-id="a3c56-113">But the deployed service is no longer going to do training - it's going to generate new predictions by scoring the user's input based on our model.</span></span> <span data-ttu-id="a3c56-114">Поэтому мы собираемся выполнить некоторую подготовку для преобразования этого эксперимента из ***обучающего*** в ***прогнозный***.</span><span class="sxs-lookup"><span data-stu-id="a3c56-114">So we're going to do some preparation to convert this experiment from a ***training*** experiment to a ***predictive*** experiment.</span></span> 

<span data-ttu-id="a3c56-115">Этот процесс состоит из трех этапов.</span><span class="sxs-lookup"><span data-stu-id="a3c56-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="a3c56-116">Удаление одной из моделей</span><span class="sxs-lookup"><span data-stu-id="a3c56-116">Remove one of the models</span></span>
2. <span data-ttu-id="a3c56-117">Преобразование *обучающего эксперимента* в *прогнозный эксперимент*</span><span class="sxs-lookup"><span data-stu-id="a3c56-117">Convert the *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="a3c56-118">Развертывание прогностического эксперимента в качестве веб-службы</span><span class="sxs-lookup"><span data-stu-id="a3c56-118">Deploy the predictive experiment as a web service</span></span>

## <a name="remove-one-of-the-models"></a><span data-ttu-id="a3c56-119">Удаление одной из моделей</span><span class="sxs-lookup"><span data-stu-id="a3c56-119">Remove one of the models</span></span>

<span data-ttu-id="a3c56-120">Прежде всего нам нужно немного сократить этот эксперимент.</span><span class="sxs-lookup"><span data-stu-id="a3c56-120">First, we need to trim this experiment down a little.</span></span> <span data-ttu-id="a3c56-121">Сейчас в эксперименте есть две разные модели, но для развертывания в качестве веб-службы используется только одна.</span><span class="sxs-lookup"><span data-stu-id="a3c56-121">We currently have two different models in the experiment, but we only want to use one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="a3c56-122">Допустим, мы решили, что модель увеличивающегося дерева подходит нам лучше, чем модель опорных векторов.</span><span class="sxs-lookup"><span data-stu-id="a3c56-122">Let's say we've decided that the boosted tree model performed better than the SVM model.</span></span> <span data-ttu-id="a3c56-123">Поэтому сначала мы удалим модуль [Two-Class Support Vector Machine][two-class-support-vector-machine] (Двухклассовый метод опорных векторов) и все модули, которые использовались для его обучения.</span><span class="sxs-lookup"><span data-stu-id="a3c56-123">So the first thing to do is remove the [Two-Class Support Vector Machine][two-class-support-vector-machine] module and the modules that were used for training it.</span></span> <span data-ttu-id="a3c56-124">Сначала создайте копию эксперимента, нажав кнопку **Сохранить как** в нижней части полотна эксперимента.</span><span class="sxs-lookup"><span data-stu-id="a3c56-124">You may want to make a copy of the experiment first by clicking **Save As** at the bottom of the experiment canvas.</span></span>

<span data-ttu-id="a3c56-125">Необходимо удалить следующие модули:</span><span class="sxs-lookup"><span data-stu-id="a3c56-125">We need to delete the following modules:</span></span>  

* <span data-ttu-id="a3c56-126">[Two-Class Support Vector Machine][two-class-support-vector-machine] (Двухклассовый метод опорных векторов);</span><span class="sxs-lookup"><span data-stu-id="a3c56-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="a3c56-127">модули [Train Model][train-model] (Обучение модели) и [Score Model][score-model] (Оценка модели), которые были к нему подключены;</span><span class="sxs-lookup"><span data-stu-id="a3c56-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected to it</span></span>
* <span data-ttu-id="a3c56-128">оба модуля [Normalize Data][normalize-data] (Нормализация данных);</span><span class="sxs-lookup"><span data-stu-id="a3c56-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="a3c56-129">[Evaluate Model][evaluate-model] (Анализ модели) — так как процесс анализа уже завершен.</span><span class="sxs-lookup"><span data-stu-id="a3c56-129">[Evaluate Model][evaluate-model] (because we're finished evaluating the models)</span></span>

<span data-ttu-id="a3c56-130">Поочередно выберите каждый из этих модулей и нажмите клавишу DELETE или щелкните модуль правой кнопкой мыши и выберите **Delete** (Удалить).</span><span class="sxs-lookup"><span data-stu-id="a3c56-130">Select each module and press the Delete key, or right-click the module and select **Delete**.</span></span> 

![После удаления модели SVM][3a]

<span data-ttu-id="a3c56-132">Теперь ваша модель должна выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="a3c56-132">Our model should now look something like this:</span></span>

![После удаления модели SVM][3]

<span data-ttu-id="a3c56-134">Теперь мы готовы к развертыванию этой модели с помощью модуля [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Двухклассовое увеличивающееся дерево принятия решений).</span><span class="sxs-lookup"><span data-stu-id="a3c56-134">Now we're ready to deploy this model using the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-the-training-experiment-to-a-predictive-experiment"></a><span data-ttu-id="a3c56-135">Преобразование обучающего эксперимента в прогностический эксперимент</span><span class="sxs-lookup"><span data-stu-id="a3c56-135">Convert the training experiment to a predictive experiment</span></span>

<span data-ttu-id="a3c56-136">Чтобы подготовить модель к развертыванию, следует преобразовать обучающий эксперимент в прогнозный.</span><span class="sxs-lookup"><span data-stu-id="a3c56-136">To get this model ready for deployment, we need to convert this training experiment to a predictive experiment.</span></span> <span data-ttu-id="a3c56-137">Этот процесс состоит из трех этапов.</span><span class="sxs-lookup"><span data-stu-id="a3c56-137">This involves three steps:</span></span>

1. <span data-ttu-id="a3c56-138">Сохраните обученную модуль и замените обучающие модули.</span><span class="sxs-lookup"><span data-stu-id="a3c56-138">Save the model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="a3c56-139">удаление из эксперимента модулей, которые были необходимы только для обучения;</span><span class="sxs-lookup"><span data-stu-id="a3c56-139">Trim the experiment to remove modules that were only needed for training</span></span>
3. <span data-ttu-id="a3c56-140">Определение расположений для получения входных данных и создания выходных данных веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-140">Define where the web service will accept input and where it generates the output</span></span>

<span data-ttu-id="a3c56-141">Эти действия можно выполнять вручную, вы также можете выполнить все три шага автоматически. Для этого щелкните в нижней части холста эксперимента **Set Up Web Service** (Настроить веб-службу) и выберите **Predictive Web Service** (Прогнозная веб-служба).</span><span class="sxs-lookup"><span data-stu-id="a3c56-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at the bottom of the experiment canvas (and selecting the **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="a3c56-142">Процесс преобразовании обучающего эксперимента в прогнозный эксперимент подробно описан в [этой статье](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="a3c56-142">If you want more details on what happens when you convert a training experiment to a predictive experiment, see [How to prepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="a3c56-143">При щелчке **Set Up Web Service**(Настроить веб-службу) происходит следующее.</span><span class="sxs-lookup"><span data-stu-id="a3c56-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="a3c56-144">Обученная модель сохраняется как отдельный модуль **Trained Model** (Обученная модель) и доступна в палитре модулей слева от холста эксперимента (в разделе **Trained Models** (Обученные модели)).</span><span class="sxs-lookup"><span data-stu-id="a3c56-144">The trained model is converted to a single **Trained Model** module and stored in the module palette to the left of the experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="a3c56-145">Удаляются следующие модули, которые мы использовали для обучения:</span><span class="sxs-lookup"><span data-stu-id="a3c56-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="a3c56-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Двухклассовое увеличивающееся дерево принятия решений);</span><span class="sxs-lookup"><span data-stu-id="a3c56-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="a3c56-147">[Train Model][train-model] (Обучение модели);</span><span class="sxs-lookup"><span data-stu-id="a3c56-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="a3c56-148">[Split Data][split] (Разделение данных);</span><span class="sxs-lookup"><span data-stu-id="a3c56-148">[Split Data][split]</span></span>
  * <span data-ttu-id="a3c56-149">второй модуль [Execute R Script][execute-r-script] (Выполнение скрипта R), который использовался для тестовых данных.</span><span class="sxs-lookup"><span data-stu-id="a3c56-149">the second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="a3c56-150">Сохраненная обученная модель добавляется обратно в эксперимент.</span><span class="sxs-lookup"><span data-stu-id="a3c56-150">The saved trained model is added back into the experiment</span></span>
* <span data-ttu-id="a3c56-151">Добавляются модули **Web service input** (Входные данные веб-службы) и **Web service output** (Выходные данные веб-службы). Они определяют, откуда поступают пользовательские данные при обращении к веб-службе и какие данные возвращаются.</span><span class="sxs-lookup"><span data-stu-id="a3c56-151">**Web service input** and **Web service output** modules are added (these identify where the user's data will enter the model, and what data is returned, when the web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="a3c56-152">Как можно заметить, эксперимент сохраняется на двух вкладках, которые добавляются в верхней части холста эксперимента.</span><span class="sxs-lookup"><span data-stu-id="a3c56-152">You can see that the experiment is saved in two parts under tabs that have been added at the top of the experiment canvas.</span></span> <span data-ttu-id="a3c56-153">Исходный обучающий эксперимент теперь размещается на вкладке **Training experiment** (Обучающий эксперимент), а только что созданный прогнозный эксперимент — на вкладке **Predictive experiment** (Прогнозный эксперимент).</span><span class="sxs-lookup"><span data-stu-id="a3c56-153">The original training experiment is under the tab **Training experiment**, and the newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="a3c56-154">В качестве веб-службы мы будем развертывать именно прогнозный эксперимент.</span><span class="sxs-lookup"><span data-stu-id="a3c56-154">The predictive experiment is the one we'll deploy as a web service.</span></span>

<span data-ttu-id="a3c56-155">С этим экспериментом необходимо выполнить одно дополнительное действие.</span><span class="sxs-lookup"><span data-stu-id="a3c56-155">We need to take one additional step with this particular experiment.</span></span>
<span data-ttu-id="a3c56-156">Ранее мы добавили два модуля [Execute R Script][execute-r-script] (Выполнение скрипта R), чтобы реализовать функцию взвешивания данных.</span><span class="sxs-lookup"><span data-stu-id="a3c56-156">We added two [Execute R Script][execute-r-script] modules to provide a weighting function to the data.</span></span> <span data-ttu-id="a3c56-157">Этот маневр нам был нужен только для обучения и тестирования, поэтому из итоговой модели эти модули можно удалить.</span><span class="sxs-lookup"><span data-stu-id="a3c56-157">That was just a trick we needed for training and testing, so we can take out those modules in the final model.</span></span>
<span data-ttu-id="a3c56-158">Студия машинного обучения уже удалила один из модулей [Execute R Script][execute-r-script] (Выполнение скрипта R) при удалении модуля [Split][split] (Разделение данных).</span><span class="sxs-lookup"><span data-stu-id="a3c56-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed the [Split][split] module.</span></span> <span data-ttu-id="a3c56-159">Теперь можно удалить второй модуль и подключить модуль [Metadata Editor][metadata-editor] (Редактор метаданных) непосредственно к модулю [Score Model][score-model] (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="a3c56-159">Now we can remove the other and connect [Metadata Editor][metadata-editor] directly to [Score Model][score-model].</span></span>    

<span data-ttu-id="a3c56-160">Теперь наш эксперимент должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a3c56-160">Our experiment should now look like this:</span></span>  

![Оценка обученной модели][4]  

> [!NOTE]
> <span data-ttu-id="a3c56-162">Возможно, вас удивляет, почему мы оставили набор данных UCI German Credit Card Data в прогностическом эксперименте.</span><span class="sxs-lookup"><span data-stu-id="a3c56-162">You may be wondering why we left the UCI German Credit Card Data dataset in the predictive experiment.</span></span> <span data-ttu-id="a3c56-163">Служба будет использовать только данные пользователя. Изначальный набор данных больше не используется, зачем же оставлять его в модели?</span><span class="sxs-lookup"><span data-stu-id="a3c56-163">The service is going to score the user's data, not the original dataset, so why leave the original dataset in the model?</span></span>
> 
> <span data-ttu-id="a3c56-164">Действительно, службе не нужны исходные данные кредитных карт.</span><span class="sxs-lookup"><span data-stu-id="a3c56-164">It's true that the service doesn't need the original credit card data.</span></span> <span data-ttu-id="a3c56-165">Но по-прежнему нужна схема для этих данных, включающая такие сведения, как общее число столбцов, а также какие столбцы являются числовыми.</span><span class="sxs-lookup"><span data-stu-id="a3c56-165">But it does need the schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="a3c56-166">Эти данные схемы необходимы для интерпретации пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="a3c56-166">This schema information is necessary to interpret the user's data.</span></span> <span data-ttu-id="a3c56-167">Мы оставили эти компоненты подключенными, чтобы модуль оценки имел схему набора данных при запуске службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-167">We leave these components connected so that the scoring module has the dataset schema when the service is running.</span></span> <span data-ttu-id="a3c56-168">Данные не используются, используется только схема.</span><span class="sxs-lookup"><span data-stu-id="a3c56-168">The data isn't used, just the schema.</span></span>  
> 
> 

<span data-ttu-id="a3c56-169">Запустите эксперимент в последний раз (нажмите **Выполнить**). Чтобы убедиться в том, что модуль по-прежнему работает, щелкните по выходным данным модуля [Score Model][score-model] (Оценка модели) и выберите **View Results** (Показать результаты).</span><span class="sxs-lookup"><span data-stu-id="a3c56-169">Run the experiment one last time (click **Run**.) If you want to verify that the model is still working, click the output of the [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="a3c56-170">Вы увидите, что изначальные данные отображаются вместе со значением кредитного риска (расчетные метки) и оценочным значением вероятности (расчетные вероятности).</span><span class="sxs-lookup"><span data-stu-id="a3c56-170">You can see that the original data is displayed, along with the credit risk value ("Scored Labels") and the scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-the-web-service"></a><span data-ttu-id="a3c56-171">Развертывание веб-службы</span><span class="sxs-lookup"><span data-stu-id="a3c56-171">Deploy the web service</span></span>
<span data-ttu-id="a3c56-172">Эксперимент можно развернуть в виде классической веб-службы или новой веб-службы на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a3c56-172">You can deploy the experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="a3c56-173">Развертывание в виде классической веб-службы</span><span class="sxs-lookup"><span data-stu-id="a3c56-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="a3c56-174">Чтобы развернуть классическую веб-службу на основе нашего эксперимента, щелкните **Deploy Web Service** (Развернуть веб-службу) под холстом и выберите пункт **Deploy Web Service [Classic]** (Развернуть веб-службу [классическую]).</span><span class="sxs-lookup"><span data-stu-id="a3c56-174">To deploy a Classic web service derived from our experiment, click **Deploy Web Service** below the canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="a3c56-175">Студия машинного обучения развернет эксперимент как веб-службу и откроет панель мониторинга для этой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-175">Machine Learning Studio deploys the experiment as a web service and takes you to the dashboard for that web service.</span></span> <span data-ttu-id="a3c56-176">Отсюда можно вернуться к эксперименту (**View snapshot** (Просмотр снимка) или **View latest** (Просмотр последних)) и выполнить простой тест веб-службы (см. раздел **Тестирование веб-службы** ниже).</span><span class="sxs-lookup"><span data-stu-id="a3c56-176">From this page you can return to the experiment (**View snapshot** or **View latest**) and run a simple test of the web service (see **Test the web service** below).</span></span> <span data-ttu-id="a3c56-177">На ней также приведены сведения о создании приложений, которые могут обращаться к веб-службе (подробнее об этом в следующем шаге пошагового руководства).</span><span class="sxs-lookup"><span data-stu-id="a3c56-177">There is also information here for creating applications that can access the web service (more on that in the next step of this walkthrough).</span></span>

![Панель мониторинга веб-службы][6]

<span data-ttu-id="a3c56-179">Службу можно настраивать на вкладке **КОНФИГУРАЦИЯ** .</span><span class="sxs-lookup"><span data-stu-id="a3c56-179">You can configure the service by clicking the **CONFIGURATION** tab.</span></span> <span data-ttu-id="a3c56-180">На этой вкладке можно изменить имя службы (по умолчанию она получает имя эксперимента) и предоставить ее описание.</span><span class="sxs-lookup"><span data-stu-id="a3c56-180">Here you can modify the service name (it's given the experiment name by default) and give it a description.</span></span> <span data-ttu-id="a3c56-181">Можно также задать более удобочитаемые метки для входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a3c56-181">You can also give more friendly labels for the input and output data.</span></span>  

![Настройка веб-службы][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="a3c56-183">Развертывание в качестве новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="a3c56-183">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="a3c56-184">Для развертывания новой веб-службы у вас должен быть достаточный уровень разрешений в подписке, в которую выполняется развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-184">To deploy a New web service you must have sufficient permissions in the subscription to which you are deploying the web service.</span></span> <span data-ttu-id="a3c56-185">Дополнительные сведения см. в статье [Управление веб-службой с помощью портала веб-служб машинного обучения Azure](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="a3c56-185">For more information, see [Manage a web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="a3c56-186">Чтобы развернуть новую веб-службу на основе нашего эксперимента, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="a3c56-186">To deploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="a3c56-187">Щелкните под холстом действие **Deploy Web Service** (Развернуть веб-службу) и выберите **Deploy Web Service [New]** (Развернуть веб-службу [новую]).</span><span class="sxs-lookup"><span data-stu-id="a3c56-187">Click **Deploy Web Service** below the canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="a3c56-188">Студия машинного обучения направит вас на страницу **развертывания эксперимента** в веб-службах машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a3c56-188">Machine Learning Studio transfers you to the Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="a3c56-189">Введите имя этой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-189">Enter a name for the web service.</span></span> 

3. <span data-ttu-id="a3c56-190">Выберите **план ценообразования** в списке существующих планов. Также можно нажать кнопку "Create new" (Создать), а затем ввести имя и выбрать вариант ежемесячной оплаты для нового плана.</span><span class="sxs-lookup"><span data-stu-id="a3c56-190">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give the new plan a name and select the monthly plan option.</span></span> <span data-ttu-id="a3c56-191">По умолчанию указаны уровни плана для вашего региона по умолчанию, и веб-служба развертывается именно в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="a3c56-191">The plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

4. <span data-ttu-id="a3c56-192">Щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="a3c56-192">Click **Deploy**.</span></span>

<span data-ttu-id="a3c56-193">Через несколько минут откроется **страница быстрого запуска** для новой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-193">After a few minutes, the **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="a3c56-194">Службу можно настраивать на вкладке **Configure** (Конфигурация).</span><span class="sxs-lookup"><span data-stu-id="a3c56-194">You can configure the service by clicking the **Configure** tab.</span></span> <span data-ttu-id="a3c56-195">Здесь вы можете изменить заголовок службы или ввести для нее описание.</span><span class="sxs-lookup"><span data-stu-id="a3c56-195">Here you can modify the service title and give it a description.</span></span> 

<span data-ttu-id="a3c56-196">Чтобы проверить работу веб-службы, щелкните вкладку **Test** (Тестирование) (см. раздел **Тестирование веб-службы** ниже).</span><span class="sxs-lookup"><span data-stu-id="a3c56-196">To test the web service, click the **Test** tab (see **Test the web service** below).</span></span> <span data-ttu-id="a3c56-197">Чтобы получить сведения о создании приложений, которые могут обращаться к веб-службе, щелкните вкладку **Consume** (Использование) (дополнительные сведения см. в следующем шаге этого руководства).</span><span class="sxs-lookup"><span data-stu-id="a3c56-197">For information on creating applications that can access the web service, click the **Consume** tab (the next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="a3c56-198">После развертывания веб-службы ее можно обновить.</span><span class="sxs-lookup"><span data-stu-id="a3c56-198">You can update the web service after you've deployed it.</span></span> <span data-ttu-id="a3c56-199">Например, если требуется скорректировать модель, измените обучающий эксперимент, настройте параметры модели и нажмите кнопку **Deploy Web Service** (Развернуть веб-службу), а затем выберите вариант **Deploy Web Service [Classic]** (Развернуть веб-службу [классическую]) или **Deploy Web Service [New]** (Развернуть веб-службу [новую]).</span><span class="sxs-lookup"><span data-stu-id="a3c56-199">For example, if you want to change your model, then you can edit the training experiment, tweak the model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="a3c56-200">При повторном развертывании эксперимента веб-служба заменяется обновленной моделью.</span><span class="sxs-lookup"><span data-stu-id="a3c56-200">When you deploy the experiment again, it replaces the web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-the-web-service"></a><span data-ttu-id="a3c56-201">Тестирование веб-службы</span><span class="sxs-lookup"><span data-stu-id="a3c56-201">Test the web service</span></span>

<span data-ttu-id="a3c56-202">При обращении к веб-службе пользовательские данные поступают в модуль **Web service input** (Входные данные веб-службы), а оттуда передаются для оценки в модуль [Score Model][score-model] (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="a3c56-202">When the web service is accessed, the user's data enters through the **Web service input** module where it's passed to the [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="a3c56-203">Мы настроили наш прогнозный эксперимент так, чтобы модель ожидала поступления данных в том же формате, в котором был исходный набор данных о кредитных рисках.</span><span class="sxs-lookup"><span data-stu-id="a3c56-203">The way we've set up the predictive experiment, the model expects data in the same format as the original credit risk dataset.</span></span>
<span data-ttu-id="a3c56-204">Результаты возвращаются из веб-службы пользователю через модуль **Web service output** (Выходные данные веб-службы).</span><span class="sxs-lookup"><span data-stu-id="a3c56-204">The results are returned to the user from the web service through the **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="a3c56-205">Мы настроили наш прогнозный эксперимент так, чтобы возвращались полные результаты из модуля [Score Model][score-model] (Оценка модели).</span><span class="sxs-lookup"><span data-stu-id="a3c56-205">The way we have the predictive experiment configured, the entire results from the [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="a3c56-206">Они включают все входные данные, а также значение кредитного риска и оценку вероятности.</span><span class="sxs-lookup"><span data-stu-id="a3c56-206">This includes all the input data plus the credit risk value and the scoring probability.</span></span> <span data-ttu-id="a3c56-207">Но если нужно, вы можете возвращать что-нибудь другое, например только значение кредитного риска.</span><span class="sxs-lookup"><span data-stu-id="a3c56-207">But you can return something different if you want - for example, you could return just the credit risk value.</span></span> <span data-ttu-id="a3c56-208">Для этого добавьте модуль [Project Columns][project-columns] (Столбцы проекта) между модулями [Score Model][score-model] (Оценка модели) и **Web service output** (Выходные данные веб-службы), чтобы исключить ненужные столбцы из возвращаемых данных веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-208">To do this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and the **Web service output** to eliminate columns you don't want the web service to return.</span></span> 
> 
> 

<span data-ttu-id="a3c56-209">Классическую веб-службу можно протестировать **в студии машинного обучения** или на портале **веб-служб машинного обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="a3c56-209">You can test a Classic web service either in **Machine Learning Studio** or in the **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="a3c56-210">Новую веб-службу можно протестировать только на портале **веб-служб машинного обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="a3c56-210">You can test a New web service only in the **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="a3c56-211">При тестировании на портале веб-служб машинного обучения Azure можно подготовить с помощью портала образец данных для проверки службы "запрос-ответ".</span><span class="sxs-lookup"><span data-stu-id="a3c56-211">When testing in the Azure Machine Learning Web Services portal, you can have the portal create sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="a3c56-212">Для этого на странице **Настройка** выберите "Да" для параметра **Sample Data Enabled?** (Использовать образец данных?).</span><span class="sxs-lookup"><span data-stu-id="a3c56-212">On the **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="a3c56-213">Теперь, когда вы откроете вкладку "Запрос-ответ" на странице **Тестирование**, портал создаст образец данных на основе исходного набора данных о кредитных рисках.</span><span class="sxs-lookup"><span data-stu-id="a3c56-213">When you open the Request-Response tab on the **Test** page, the portal fills in sample data taken from the original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="a3c56-214">Тестирование классической веб-службы</span><span class="sxs-lookup"><span data-stu-id="a3c56-214">Test a Classic web service</span></span>

<span data-ttu-id="a3c56-215">Классическую веб-службу можно протестировать в студии машинного обучения или на портале веб-служб машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="a3c56-215">You can test a Classic web service in Machine Learning Studio or in the Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="a3c56-216">Тестирование в студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a3c56-216">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="a3c56-217">На странице **DASHBOARD** (Панель мониторинга) нажмите кнопку **Test** (Тестировать) в разделе **Default Endpoint** (Конечная точка по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="a3c56-217">On the **DASHBOARD** page for the web service, click the **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="a3c56-218">Появится диалоговое окно, предлагающее ввести входные данные для службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-218">A dialog pops up and asks you for the input data for the service.</span></span> <span data-ttu-id="a3c56-219">Это те же столбцы, которые были в исходном наборе данных о кредитных рисках.</span><span class="sxs-lookup"><span data-stu-id="a3c56-219">These are the same columns that appeared in the original credit risk dataset.</span></span>  

2. <span data-ttu-id="a3c56-220">Введите набор данных и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a3c56-220">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-the-machine-learning-web-services-portal"></a><span data-ttu-id="a3c56-221">Тестирование на портале веб-служб машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a3c56-221">Test in the Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="a3c56-222">На странице **DASHBOARD** (Панель мониторинга) нажмите кнопку **Test preview** (Предварительный просмотр теста) в разделе **Default Endpoint** (Конечная точка по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="a3c56-222">On the **DASHBOARD** page for the web service, click the **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="a3c56-223">На портале веб-служб машинного обучения Azure откроется страница тестирования конечной точки веб-службы, где будет предложено ввести входные данные для службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-223">The test page in the Azure Machine Learning Web Services portal for the web service endpoint opens and asks you for the input data for the service.</span></span> <span data-ttu-id="a3c56-224">Это те же столбцы, которые были в исходном наборе данных о кредитных рисках.</span><span class="sxs-lookup"><span data-stu-id="a3c56-224">These are the same columns that appeared in the original credit risk dataset.</span></span>

2. <span data-ttu-id="a3c56-225">Щелкните **Test Request-Response** (Тестировать "запрос-ответ").</span><span class="sxs-lookup"><span data-stu-id="a3c56-225">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="a3c56-226">Тестирование новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="a3c56-226">Test a New web service</span></span>

<span data-ttu-id="a3c56-227">Новую веб-службу можно протестировать только на портале веб-служб машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a3c56-227">You can test a New web service only in the Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="a3c56-228">На портале [веб-служб машинного обучения Azure](https://services.azureml.net/quickstart) щелкните **Test** (Тестировать) в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-228">In the [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at the top of the page.</span></span> <span data-ttu-id="a3c56-229">Откроется страница **Test** (Тестирование), на которой можно ввести данные для службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-229">The **Test** page opens and you can input data for the service.</span></span> <span data-ttu-id="a3c56-230">Отображаемые поля ввода соответствуют столбцам, которые существовали в исходном наборе данных о кредитных рисках.</span><span class="sxs-lookup"><span data-stu-id="a3c56-230">The input fields displayed correspond to the columns that appeared in the original credit risk dataset.</span></span> 

2. <span data-ttu-id="a3c56-231">Введите набор данных и щелкните **Test Request-Response**(Тестировать "запрос-ответ").</span><span class="sxs-lookup"><span data-stu-id="a3c56-231">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="a3c56-232">Результаты теста отображаются в правой части страницы, в столбце выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a3c56-232">The results of the test are displayed on the right-hand side of the page in the output column.</span></span> 


## <a name="manage-the-web-service"></a><span data-ttu-id="a3c56-233">Управление веб-службой</span><span class="sxs-lookup"><span data-stu-id="a3c56-233">Manage the web service</span></span>

### <a name="manage-a-classic-web-service-in-the-azure-classic-portal"></a><span data-ttu-id="a3c56-234">Управление классической веб-службой на классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="a3c56-234">Manage a Classic web service in the Azure classic portal</span></span>

<span data-ttu-id="a3c56-235">После развертывания классической веб-службой можно управлять с помощью [классического портала Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a3c56-235">Once you've deployed your Classic web service, you can manage it from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="a3c56-236">Войдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a3c56-236">Sign in to the [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="a3c56-237">На панели служб Microsoft Azure выберите **Машинное обучение**.</span><span class="sxs-lookup"><span data-stu-id="a3c56-237">In the Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="a3c56-238">Щелкните рабочую область.</span><span class="sxs-lookup"><span data-stu-id="a3c56-238">Click your workspace</span></span>
4. <span data-ttu-id="a3c56-239">Щелкните вкладку **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="a3c56-239">Click the **Web services** tab</span></span>
5. <span data-ttu-id="a3c56-240">Щелкните созданную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="a3c56-240">Click the web service we created</span></span>
6. <span data-ttu-id="a3c56-241">Щелкните конечную точку по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a3c56-241">Click the "default" endpoint</span></span>

<span data-ttu-id="a3c56-242">Здесь можно отслеживать работу веб-службы и корректировать ее производительность, изменяя число одновременных обрабатываемых вызовов.</span><span class="sxs-lookup"><span data-stu-id="a3c56-242">From here, you can do things like monitor how the web service is doing and make performance tweaks by changing how many concurrent calls the service can handle.</span></span>

<span data-ttu-id="a3c56-243">Дополнительные сведения см. в статье</span><span class="sxs-lookup"><span data-stu-id="a3c56-243">For more details, see:</span></span>

* [<span data-ttu-id="a3c56-244">Создание конечных точек</span><span class="sxs-lookup"><span data-stu-id="a3c56-244">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="a3c56-245">Масштабирование веб-службы</span><span class="sxs-lookup"><span data-stu-id="a3c56-245">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="a3c56-246">Управление классической или новой веб-службой на портале веб-служб машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="a3c56-246">Manage a Classic or New web service in the Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="a3c56-247">Развернутой веб-службой (классической или новой) можно управлять с помощью портала [веб-служб Машинного обучения Microsoft Azure](https://services.azureml.net/quickstart).</span><span class="sxs-lookup"><span data-stu-id="a3c56-247">Once you've deployed your web service, whether Classic or New, you can manage it from the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="a3c56-248">Вот как можно отслеживать производительность веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a3c56-248">To monitor the performance of your web service:</span></span>

1. <span data-ttu-id="a3c56-249">Войдите на портал [веб-служб Машинного обучения Microsoft Azure](https://services.azureml.net/quickstart).</span><span class="sxs-lookup"><span data-stu-id="a3c56-249">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="a3c56-250">Щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="a3c56-250">Click **Web services**</span></span>
3. <span data-ttu-id="a3c56-251">Щелкните нужную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="a3c56-251">Click your web service</span></span>
4. <span data-ttu-id="a3c56-252">Щелкните **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="a3c56-252">Click the **Dashboard**</span></span>

- - -
<span data-ttu-id="a3c56-253">**Далее: [доступ к веб-службе](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="a3c56-253">**Next: [Access the web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

[3]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3.png
[3a]: ./media/machine-learning-walkthrough-5-publish-web-service/publish3a.png
[4]: ./media/machine-learning-walkthrough-5-publish-web-service/publish4.png
[5]: ./media/machine-learning-walkthrough-5-publish-web-service/publish5.png
[6]: ./media/machine-learning-walkthrough-5-publish-web-service/publish6.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[metadata-editor]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[project-columns]: https://msdn.microsoft.com/en-us/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
