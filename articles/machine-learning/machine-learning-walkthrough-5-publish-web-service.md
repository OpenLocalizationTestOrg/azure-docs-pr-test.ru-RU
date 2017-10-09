---
title: "Шаг 5: Развертывание веб-службы машинного обучения hello | Документы Microsoft"
description: "Шаг 5 из hello разработка прогнозирующего решения Пошаговое руководство: развертывание прогнозной эксперимента в студии машинного обучения веб-службы."
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
ms.openlocfilehash: 76391010972ed1450bbda8bfb2352c7b22b51ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-5-deploy-hello-azure-machine-learning-web-service"></a><span data-ttu-id="374d4-103">Пошаговое руководство шаг 5: Развертывание веб-службы машинного обучения Azure hello</span><span class="sxs-lookup"><span data-stu-id="374d4-103">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>
<span data-ttu-id="374d4-104">Это пятый шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="374d4-104">This is hello fifth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="374d4-105">Создание рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="374d4-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="374d4-106">Отправка существующих данных</span><span class="sxs-lookup"><span data-stu-id="374d4-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="374d4-107">Создание нового эксперимента</span><span class="sxs-lookup"><span data-stu-id="374d4-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="374d4-108">Обучать и оценивать модели hello</span><span class="sxs-lookup"><span data-stu-id="374d4-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. <span data-ttu-id="374d4-109">**Развернуть веб-службу hello**</span><span class="sxs-lookup"><span data-stu-id="374d4-109">**Deploy hello web service**</span></span>
6. [<span data-ttu-id="374d4-110">Веб-службы доступа hello</span><span class="sxs-lookup"><span data-stu-id="374d4-110">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="374d4-111">toogive другие toouse вероятность hello прогнозной модели, разработанный в этом пошаговом руководстве, мы можно развернуть его как веб-службы в Azure.</span><span class="sxs-lookup"><span data-stu-id="374d4-111">toogive others a chance toouse hello predictive model we've developed in this walkthrough, we can deploy it as a web service on Azure.</span></span>

<span data-ttu-id="374d4-112">Точку toothis мы пробовал экспериментировать с нашей модели обучения.</span><span class="sxs-lookup"><span data-stu-id="374d4-112">Up toothis point we've been experimenting with training our model.</span></span> <span data-ttu-id="374d4-113">Но hello развернуты службы больше не будет обучающих toodo — он будет toogenerate новые прогнозы путем оценки hello введенных на основе нашей модели.</span><span class="sxs-lookup"><span data-stu-id="374d4-113">But hello deployed service is no longer going toodo training - it's going toogenerate new predictions by scoring hello user's input based on our model.</span></span> <span data-ttu-id="374d4-114">Так мы будем toodo некоторые tooconvert подготовки это поэкспериментировать с ***обучения*** поэкспериментировать tooa ***прогнозной*** поэкспериментировать.</span><span class="sxs-lookup"><span data-stu-id="374d4-114">So we're going toodo some preparation tooconvert this experiment from a ***training*** experiment tooa ***predictive*** experiment.</span></span> 

<span data-ttu-id="374d4-115">Этот процесс состоит из трех этапов.</span><span class="sxs-lookup"><span data-stu-id="374d4-115">This is a three-step process:</span></span>  

1. <span data-ttu-id="374d4-116">Удалите одну из моделей hello</span><span class="sxs-lookup"><span data-stu-id="374d4-116">Remove one of hello models</span></span>
2. <span data-ttu-id="374d4-117">Преобразовать hello *эксперимента обучения* мы создали в *прогнозной эксперимента*</span><span class="sxs-lookup"><span data-stu-id="374d4-117">Convert hello *training experiment* we've created into a *predictive experiment*</span></span>
3. <span data-ttu-id="374d4-118">Развертывание hello прогнозной эксперимент как веб-службы</span><span class="sxs-lookup"><span data-stu-id="374d4-118">Deploy hello predictive experiment as a web service</span></span>

## <a name="remove-one-of-hello-models"></a><span data-ttu-id="374d4-119">Удалите одну из моделей hello</span><span class="sxs-lookup"><span data-stu-id="374d4-119">Remove one of hello models</span></span>

<span data-ttu-id="374d4-120">Во-первых мы должны tootrim этом эксперименте работу немного.</span><span class="sxs-lookup"><span data-stu-id="374d4-120">First, we need tootrim this experiment down a little.</span></span> <span data-ttu-id="374d4-121">В настоящее время имеется две различные модели в эксперименте hello, но нам нужен только одна модель toouse когда мы развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="374d4-121">We currently have two different models in hello experiment, but we only want toouse one model when we deploy this as a web service.</span></span>  

<span data-ttu-id="374d4-122">Предположим, мы решили hello повышенного дерева модели выполняется быстрее, чем модель SVM hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-122">Let's say we've decided that hello boosted tree model performed better than hello SVM model.</span></span> <span data-ttu-id="374d4-123">Поэтому первая самое toodo hello remove hello [Двухклассовая машина опорных векторов] [ two-class-support-vector-machine] модуль и hello модули, которые были использованы для ее обучения.</span><span class="sxs-lookup"><span data-stu-id="374d4-123">So hello first thing toodo is remove hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module and hello modules that were used for training it.</span></span> <span data-ttu-id="374d4-124">Вы можете toomake копию эксперимента hello сначала, нажав кнопку **Сохранить как** внизу hello hello поэкспериментировать холста.</span><span class="sxs-lookup"><span data-stu-id="374d4-124">You may want toomake a copy of hello experiment first by clicking **Save As** at hello bottom of hello experiment canvas.</span></span>

<span data-ttu-id="374d4-125">Нужны hello toodelete следующие модули:</span><span class="sxs-lookup"><span data-stu-id="374d4-125">We need toodelete hello following modules:</span></span>  

* <span data-ttu-id="374d4-126">[Two-Class Support Vector Machine][two-class-support-vector-machine] (Двухклассовый метод опорных векторов);</span><span class="sxs-lookup"><span data-stu-id="374d4-126">[Two-Class Support Vector Machine][two-class-support-vector-machine]</span></span>
* <span data-ttu-id="374d4-127">[Обучение модели] [ train-model] и [модель оценки] [ score-model] модули, которые были подключенные tooit</span><span class="sxs-lookup"><span data-stu-id="374d4-127">[Train Model][train-model] and [Score Model][score-model] modules that were connected tooit</span></span>
* <span data-ttu-id="374d4-128">оба модуля [Normalize Data][normalize-data] (Нормализация данных);</span><span class="sxs-lookup"><span data-stu-id="374d4-128">[Normalize Data][normalize-data] (both of them)</span></span>
* <span data-ttu-id="374d4-129">[Модель оценки] [ evaluate-model] (поскольку мы работаем завершения оценки hello моделей)</span><span class="sxs-lookup"><span data-stu-id="374d4-129">[Evaluate Model][evaluate-model] (because we're finished evaluating hello models)</span></span>

<span data-ttu-id="374d4-130">Выберите каждый модуль и нажмите клавишу Delete hello или модуля hello щелкните правой кнопкой мыши и выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="374d4-130">Select each module and press hello Delete key, or right-click hello module and select **Delete**.</span></span> 

![Удалить модель SVM hello][3a]

<span data-ttu-id="374d4-132">Теперь ваша модель должна выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="374d4-132">Our model should now look something like this:</span></span>

![Удалить модель SVM hello][3]

<span data-ttu-id="374d4-134">Теперь мы готовы toodeploy это модели с помощью hello [Двухклассового повышенного дерева принятия решений][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="374d4-134">Now we're ready toodeploy this model using hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree].</span></span>

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a><span data-ttu-id="374d4-135">Преобразовать прогнозной эксперимента эксперимента обучения tooa hello</span><span class="sxs-lookup"><span data-stu-id="374d4-135">Convert hello training experiment tooa predictive experiment</span></span>

<span data-ttu-id="374d4-136">tooget это модели готовый для развертывания, то необходимо tooconvert это прогнозной эксперимента tooa эксперимента обучения.</span><span class="sxs-lookup"><span data-stu-id="374d4-136">tooget this model ready for deployment, we need tooconvert this training experiment tooa predictive experiment.</span></span> <span data-ttu-id="374d4-137">Этот процесс состоит из трех этапов.</span><span class="sxs-lookup"><span data-stu-id="374d4-137">This involves three steps:</span></span>

1. <span data-ttu-id="374d4-138">Сохранить модель hello мы обучена и замените наших обучающих модулей</span><span class="sxs-lookup"><span data-stu-id="374d4-138">Save hello model we've trained and then replace our training modules</span></span>
2. <span data-ttu-id="374d4-139">Trim hello эксперимента tooremove модули, которые требовались только для обучения</span><span class="sxs-lookup"><span data-stu-id="374d4-139">Trim hello experiment tooremove modules that were only needed for training</span></span>
3. <span data-ttu-id="374d4-140">Определите, где hello веб-служба будет принимать входные данные и где он создает выходные данные hello</span><span class="sxs-lookup"><span data-stu-id="374d4-140">Define where hello web service will accept input and where it generates hello output</span></span>

<span data-ttu-id="374d4-141">Мы могли сделать это вручную, но к счастью, все три действия могут быть выполнены, щелкнув **настройки веб-службы** внизу hello холст эксперимента hello (и выбрав hello **прогнозной веб-служба** параметр).</span><span class="sxs-lookup"><span data-stu-id="374d4-141">We could do this manually, but fortunately all three steps can be accomplished by clicking **Set Up Web Service** at hello bottom of hello experiment canvas (and selecting hello **Predictive Web Service** option).</span></span>

> [!TIP]
> <span data-ttu-id="374d4-142">Если для получения дополнительных сведений на что происходит при преобразовании tooa эксперимента обучения прогнозной поэкспериментировать см. в разделе [как tooprepare модели для развертывания в Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="374d4-142">If you want more details on what happens when you convert a training experiment tooa predictive experiment, see [How tooprepare your model for deployment in Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).</span></span>

<span data-ttu-id="374d4-143">При щелчке **Set Up Web Service**(Настроить веб-службу) происходит следующее.</span><span class="sxs-lookup"><span data-stu-id="374d4-143">When you click **Set Up Web Service**, several things happen:</span></span>

* <span data-ttu-id="374d4-144">Hello обученной модели — один преобразованный tooa **обученной модели** модуля и хранятся в toohello палитры модуля hello слева от hello поэкспериментировать холст (его можно найти в разделе **обученных моделей**)</span><span class="sxs-lookup"><span data-stu-id="374d4-144">hello trained model is converted tooa single **Trained Model** module and stored in hello module palette toohello left of hello experiment canvas (you can find it under **Trained Models**)</span></span>
* <span data-ttu-id="374d4-145">Удаляются следующие модули, которые мы использовали для обучения:</span><span class="sxs-lookup"><span data-stu-id="374d4-145">Modules that were used for training are removed; specifically:</span></span>
  * <span data-ttu-id="374d4-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] (Двухклассовое увеличивающееся дерево принятия решений);</span><span class="sxs-lookup"><span data-stu-id="374d4-146">[Two-Class Boosted Decision Tree][two-class-boosted-decision-tree]</span></span>
  * <span data-ttu-id="374d4-147">[Train Model][train-model] (Обучение модели);</span><span class="sxs-lookup"><span data-stu-id="374d4-147">[Train Model][train-model]</span></span>
  * <span data-ttu-id="374d4-148">[Split Data][split] (Разделение данных);</span><span class="sxs-lookup"><span data-stu-id="374d4-148">[Split Data][split]</span></span>
  * <span data-ttu-id="374d4-149">Во-вторых Hello [выполнение скрипта R] [ execute-r-script] модуля, который был использован для тестовых данных</span><span class="sxs-lookup"><span data-stu-id="374d4-149">hello second [Execute R Script][execute-r-script] module that was used for test data</span></span>
* <span data-ttu-id="374d4-150">Сохранить Hello обученной модели добавляется обратно в эксперименте hello</span><span class="sxs-lookup"><span data-stu-id="374d4-150">hello saved trained model is added back into hello experiment</span></span>
* <span data-ttu-id="374d4-151">**Веб-службе входные данные** и **веб-службы вывода** модули будут добавлены (они определяют, где hello пользовательских данных перейдет в модели hello, и какие данные возвращаются при обращении к веб-службе hello)</span><span class="sxs-lookup"><span data-stu-id="374d4-151">**Web service input** and **Web service output** modules are added (these identify where hello user's data will enter hello model, and what data is returned, when hello web service is accessed)</span></span>

> [!NOTE]
> <span data-ttu-id="374d4-152">Вы увидите, hello эксперимента сохраняется в двух частях вкладках, которые были добавлены вверху hello холст эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-152">You can see that hello experiment is saved in two parts under tabs that have been added at hello top of hello experiment canvas.</span></span> <span data-ttu-id="374d4-153">Hello исходного эксперимента обучения — вкладка "hello" **эксперимента обучения**, и только что созданный прогнозной эксперимента hello находится под **прогнозной эксперимента**.</span><span class="sxs-lookup"><span data-stu-id="374d4-153">hello original training experiment is under hello tab **Training experiment**, and hello newly created predictive experiment is under **Predictive experiment**.</span></span> <span data-ttu-id="374d4-154">Hello прогнозной эксперимента — hello, который мы будем развертывание веб-службы.</span><span class="sxs-lookup"><span data-stu-id="374d4-154">hello predictive experiment is hello one we'll deploy as a web service.</span></span>

<span data-ttu-id="374d4-155">Мы должны tootake один дополнительный шаг с этой конкретной эксперимента.</span><span class="sxs-lookup"><span data-stu-id="374d4-155">We need tootake one additional step with this particular experiment.</span></span>
<span data-ttu-id="374d4-156">Мы добавили два [выполнение скрипта R] [ execute-r-script] tooprovide модули весовой коэффициент функции toohello данных.</span><span class="sxs-lookup"><span data-stu-id="374d4-156">We added two [Execute R Script][execute-r-script] modules tooprovide a weighting function toohello data.</span></span> <span data-ttu-id="374d4-157">Это было просто прием, необходимые для обучения и проверки, чтобы мы могли out этих модулей в конечной модели hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-157">That was just a trick we needed for training and testing, so we can take out those modules in hello final model.</span></span>
<span data-ttu-id="374d4-158">Студия машинного обучения удалены один [выполнение скрипта R] [ execute-r-script] модуля при его удалении hello [разбиение] [ split] модуля.</span><span class="sxs-lookup"><span data-stu-id="374d4-158">Machine Learning Studio removed one [Execute R Script][execute-r-script] module when it removed hello [Split][split] module.</span></span> <span data-ttu-id="374d4-159">Теперь мы можем удалить другие hello и подключите [редактор метаданных] [ metadata-editor] непосредственно слишком[модель оценки][score-model].</span><span class="sxs-lookup"><span data-stu-id="374d4-159">Now we can remove hello other and connect [Metadata Editor][metadata-editor] directly too[Score Model][score-model].</span></span>    

<span data-ttu-id="374d4-160">Теперь наш эксперимент должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="374d4-160">Our experiment should now look like this:</span></span>  

![Оценка обученной модели hello][4]  

> [!NOTE]
> <span data-ttu-id="374d4-162">Возможно, вас интересует почему мы оставили набора данных UCI данных кредитной карты немецкий hello в эксперименте прогнозной hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-162">You may be wondering why we left hello UCI German Credit Card Data dataset in hello predictive experiment.</span></span> <span data-ttu-id="374d4-163">Hello службы будет tooscore hello пользовательских данных, не hello исходного набора данных, поэтому почему оставьте hello исходный набор данных в модели hello?</span><span class="sxs-lookup"><span data-stu-id="374d4-163">hello service is going tooscore hello user's data, not hello original dataset, so why leave hello original dataset in hello model?</span></span>
> 
> <span data-ttu-id="374d4-164">Это правда, что hello службы не требуется hello исходные данные кредитной карты.</span><span class="sxs-lookup"><span data-stu-id="374d4-164">It's true that hello service doesn't need hello original credit card data.</span></span> <span data-ttu-id="374d4-165">Но он должен hello схемы для этих данных, которая содержит сведения, такие как число столбцов существует и какие столбцы являются числовыми.</span><span class="sxs-lookup"><span data-stu-id="374d4-165">But it does need hello schema for that data, which includes information such as how many columns there are and which columns are numeric.</span></span> <span data-ttu-id="374d4-166">Эта информация схемы является необходимые toointerpret hello пользовательских данных.</span><span class="sxs-lookup"><span data-stu-id="374d4-166">This schema information is necessary toointerpret hello user's data.</span></span> <span data-ttu-id="374d4-167">Оставить эти компоненты подключены таким образом, чтобы hello оценки модуль имеет hello схемы набора данных при запуске службы hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-167">We leave these components connected so that hello scoring module has hello dataset schema when hello service is running.</span></span> <span data-ttu-id="374d4-168">Hello данные не используются, только что hello схемы.</span><span class="sxs-lookup"><span data-stu-id="374d4-168">hello data isn't used, just hello schema.</span></span>  
> 
> 

<span data-ttu-id="374d4-169">Запустите эксперимент hello последний раз (щелкните **запуска**.) Tooverify, hello модели по-прежнему работает, нажмите кнопку Выход hello hello [модель оценки] [ score-model] модуль и выберите **Просмотр результатов**.</span><span class="sxs-lookup"><span data-stu-id="374d4-169">Run hello experiment one last time (click **Run**.) If you want tooverify that hello model is still working, click hello output of hello [Score Model][score-model] module and select **View Results**.</span></span> <span data-ttu-id="374d4-170">Вы увидите, что исходные данные hello отображается hello кредит риск значение («меток оцененных значений»), а также hello оценки значение вероятности («оцененных вероятностей».)</span><span class="sxs-lookup"><span data-stu-id="374d4-170">You can see that hello original data is displayed, along with hello credit risk value ("Scored Labels") and hello scoring probability value ("Scored Probabilities".)</span></span> 

## <a name="deploy-hello-web-service"></a><span data-ttu-id="374d4-171">Развернуть веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="374d4-171">Deploy hello web service</span></span>
<span data-ttu-id="374d4-172">Можно развернуть hello эксперимент как веб-служба классическом или как новую веб-службу, которая основана на Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="374d4-172">You can deploy hello experiment as either a Classic web service, or as a New web service that's based on Azure Resource Manager.</span></span>

### <a name="deploy-as-a-classic-web-service"></a><span data-ttu-id="374d4-173">Развертывание в виде классической веб-службы</span><span class="sxs-lookup"><span data-stu-id="374d4-173">Deploy as a Classic web service</span></span>
<span data-ttu-id="374d4-174">toodeploy классические веб-службе, производной от наших эксперименты, нажмите кнопку **развертывание веб-службы** ниже hello холсте и выберите **развертывание веб-службы [классический]**.</span><span class="sxs-lookup"><span data-stu-id="374d4-174">toodeploy a Classic web service derived from our experiment, click **Deploy Web Service** below hello canvas and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="374d4-175">Студия машинного обучения развертывает hello эксперимент как веб-службы и осуществляется переход toohello панель мониторинга для этой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="374d4-175">Machine Learning Studio deploys hello experiment as a web service and takes you toohello dashboard for that web service.</span></span> <span data-ttu-id="374d4-176">На этой странице можно вернуть эксперимента toohello (**Просмотр снимка** или **просмотреть последние**) и выполнить простую проверку hello веб-службы (см. **проверить веб-службу hello** ниже).</span><span class="sxs-lookup"><span data-stu-id="374d4-176">From this page you can return toohello experiment (**View snapshot** or **View latest**) and run a simple test of hello web service (see **Test hello web service** below).</span></span> <span data-ttu-id="374d4-177">Также есть сведения для создания приложений, которые могут обращаться к веб-службе hello (Подробнее об этом в hello далее в этом пошаговом руководстве).</span><span class="sxs-lookup"><span data-stu-id="374d4-177">There is also information here for creating applications that can access hello web service (more on that in hello next step of this walkthrough).</span></span>

![Панель мониторинга веб-службы][6]

<span data-ttu-id="374d4-179">Можно настроить службу hello, щелкнув hello **конфигурации** вкладки. Здесь вы можете изменить имя службы hello (это имя эксперимента hello заданного по умолчанию) и предоставить его описание.</span><span class="sxs-lookup"><span data-stu-id="374d4-179">You can configure hello service by clicking hello **CONFIGURATION** tab. Here you can modify hello service name (it's given hello experiment name by default) and give it a description.</span></span> <span data-ttu-id="374d4-180">Можно также предоставить более понятные метки для hello входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="374d4-180">You can also give more friendly labels for hello input and output data.</span></span>  

![Настройка веб-службы hello][5]  

### <a name="deploy-as-a-new-web-service"></a><span data-ttu-id="374d4-182">Развертывание в качестве новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="374d4-182">Deploy as a New web service</span></span>

> [!NOTE] 
> <span data-ttu-id="374d4-183">toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки, на которых развертываются hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="374d4-183">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you are deploying hello web service.</span></span> <span data-ttu-id="374d4-184">Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="374d4-184">For more information, see [Manage a web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="374d4-185">toodeploy веб-службу, производным от наших экспериментов:</span><span class="sxs-lookup"><span data-stu-id="374d4-185">toodeploy a New web service derived from our experiment:</span></span>

1. <span data-ttu-id="374d4-186">Нажмите кнопку **развертывание веб-службы** ниже hello холсте и выберите **развертывания [новое] веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="374d4-186">Click **Deploy Web Service** below hello canvas and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="374d4-187">Студия машинного обучения передает веб-службы машинного обучения Azure toohello **развертывание эксперимента** страницы.</span><span class="sxs-lookup"><span data-stu-id="374d4-187">Machine Learning Studio transfers you toohello Azure Machine Learning web services **Deploy Experiment** page.</span></span>

2. <span data-ttu-id="374d4-188">Введите имя для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="374d4-188">Enter a name for hello web service.</span></span> 

3. <span data-ttu-id="374d4-189">Для **цена плана**, можно выбрать существующий ценовой план, или выберите «создать» и предоставьте hello новый план имя и выберите hello ежемесячные параметр плана.</span><span class="sxs-lookup"><span data-stu-id="374d4-189">For **Price Plan**, you can select an existing pricing plan, or select "Create new" and give hello new plan a name and select hello monthly plan option.</span></span> <span data-ttu-id="374d4-190">Hello плана уровней по умолчанию toohello планы для своего региона по умолчанию и веб-службы — развернутой toothat область.</span><span class="sxs-lookup"><span data-stu-id="374d4-190">hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

4. <span data-ttu-id="374d4-191">Щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="374d4-191">Click **Deploy**.</span></span>

<span data-ttu-id="374d4-192">Через несколько минут hello **краткое руководство** открывается страница для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="374d4-192">After a few minutes, hello **Quickstart** page for your web service opens.</span></span>

<span data-ttu-id="374d4-193">Можно настроить службу hello, щелкнув hello **Настройка** вкладки. Здесь вы можете изменить службу hello title и предоставить его описание.</span><span class="sxs-lookup"><span data-stu-id="374d4-193">You can configure hello service by clicking hello **Configure** tab. Here you can modify hello service title and give it a description.</span></span> 

<span data-ttu-id="374d4-194">tootest hello веб-службы, нажмите кнопку hello **тест** вкладка (см. **проверить веб-службу hello** ниже).</span><span class="sxs-lookup"><span data-stu-id="374d4-194">tootest hello web service, click hello **Test** tab (see **Test hello web service** below).</span></span> <span data-ttu-id="374d4-195">Дополнительные сведения о создании приложений, которые могут обращаться к веб-службе hello щелкните hello **использование** вкладка (hello далее в этом пошаговом руководстве будет более подробно).</span><span class="sxs-lookup"><span data-stu-id="374d4-195">For information on creating applications that can access hello web service, click hello **Consume** tab (hello next step in this walkthrough will go into more detail).</span></span>

> [!TIP]
> <span data-ttu-id="374d4-196">После развертывания его можно обновить hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="374d4-196">You can update hello web service after you've deployed it.</span></span> <span data-ttu-id="374d4-197">Например, следует toochange модели затем можно изменить эксперимента обучения hello, настраивать параметры модели hello и нажмите кнопку **развертывание веб-службы**, выбрав **развертывание веб-службы [классический]** или  **Развертывание веб-службы [новое]**.</span><span class="sxs-lookup"><span data-stu-id="374d4-197">For example, if you want toochange your model, then you can edit hello training experiment, tweak hello model parameters, and click **Deploy Web Service**, selecting **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span> <span data-ttu-id="374d4-198">При развертывании hello эксперимент, он заменяет hello веб-службы с помощью обновленной модели.</span><span class="sxs-lookup"><span data-stu-id="374d4-198">When you deploy hello experiment again, it replaces hello web service, now using your updated model.</span></span>  
> 
> 

## <a name="test-hello-web-service"></a><span data-ttu-id="374d4-199">Проверить веб-службу hello</span><span class="sxs-lookup"><span data-stu-id="374d4-199">Test hello web service</span></span>

<span data-ttu-id="374d4-200">При обращении к веб-службе hello hello пользовательских данных поступает через hello **веб-службе входные данные** модуля, где он прошел toohello [модель оценки] [ score-model] модуля и оцененных.</span><span class="sxs-lookup"><span data-stu-id="374d4-200">When hello web service is accessed, hello user's data enters through hello **Web service input** module where it's passed toohello [Score Model][score-model] module and scored.</span></span> <span data-ttu-id="374d4-201">способ мы настроили прогнозной эксперимента hello Hello hello модель ожидает данных в том же формате, как набор данных исходной кредит риск hello hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-201">hello way we've set up hello predictive experiment, hello model expects data in hello same format as hello original credit risk dataset.</span></span>
<span data-ttu-id="374d4-202">Hello результатов toohello пользователя веб-службу hello hello **веб-службы вывода** модуля.</span><span class="sxs-lookup"><span data-stu-id="374d4-202">hello results are returned toohello user from hello web service through hello **Web service output** module.</span></span>

> [!TIP]
> <span data-ttu-id="374d4-203">у нас есть hello прогнозной эксперимента настройки hello всего способом Hello результатом hello [модель оценки] [ score-model] возвращаются модуля.</span><span class="sxs-lookup"><span data-stu-id="374d4-203">hello way we have hello predictive experiment configured, hello entire results from hello [Score Model][score-model] module are returned.</span></span> <span data-ttu-id="374d4-204">Сюда входят все hello входных данных, а также значение риска кредитной hello и hello оценки вероятности.</span><span class="sxs-lookup"><span data-stu-id="374d4-204">This includes all hello input data plus hello credit risk value and hello scoring probability.</span></span> <span data-ttu-id="374d4-205">Иначе может обнаружить, если требуется, но — например, может вернуть только значение риска кредитной hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-205">But you can return something different if you want - for example, you could return just hello credit risk value.</span></span> <span data-ttu-id="374d4-206">toodo, вставьте [столбцы проекта] [ project-columns] модуль между [модель оценки] [ score-model] и hello **веб-службы вывода** tooeliminate столбцы, вы не хотите hello web service tooreturn.</span><span class="sxs-lookup"><span data-stu-id="374d4-206">toodo this, insert a [Project Columns][project-columns] module between [Score Model][score-model] and hello **Web service output** tooeliminate columns you don't want hello web service tooreturn.</span></span> 
> 
> 

<span data-ttu-id="374d4-207">Можно проверить классического веб-узла службы в **студии машинного обучения** или в hello **веб-службы Azure Machine Learning** портала.</span><span class="sxs-lookup"><span data-stu-id="374d4-207">You can test a Classic web service either in **Machine Learning Studio** or in hello **Azure Machine Learning Web Services** portal.</span></span>
<span data-ttu-id="374d4-208">Вы можете протестировать новую веб-службу только в hello **веб-службы обучения машины** портала.</span><span class="sxs-lookup"><span data-stu-id="374d4-208">You can test a New web service only in hello **Machine Learning Web Services** portal.</span></span>

> [!TIP]
> <span data-ttu-id="374d4-209">При тестировании веб-службы Azure Machine Learning портале hello, возможно создать демонстрационные данные, можно использовать службу hello запрос-ответ tootest портала hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-209">When testing in hello Azure Machine Learning Web Services portal, you can have hello portal create sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="374d4-210">На hello **Настройка** выберите «Да» для **включен образец данных?**.</span><span class="sxs-lookup"><span data-stu-id="374d4-210">On hello **Configure** page, select "Yes" for **Sample Data Enabled?**.</span></span> <span data-ttu-id="374d4-211">При открытии вкладки hello запрос-ответ на hello **тест** странице портала hello заполняет образец данных, полученных из набора данных исходной кредит риск hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-211">When you open hello Request-Response tab on hello **Test** page, hello portal fills in sample data taken from hello original credit risk dataset.</span></span>

### <a name="test-a-classic-web-service"></a><span data-ttu-id="374d4-212">Тестирование классической веб-службы</span><span class="sxs-lookup"><span data-stu-id="374d4-212">Test a Classic web service</span></span>

<span data-ttu-id="374d4-213">Классический веб-службы можно проверить в студии машинного обучения или портале hello машины обучения веб-служб.</span><span class="sxs-lookup"><span data-stu-id="374d4-213">You can test a Classic web service in Machine Learning Studio or in hello Machine Learning Web Services portal.</span></span> 

#### <a name="test-in-machine-learning-studio"></a><span data-ttu-id="374d4-214">Тестирование в студии машинного обучения</span><span class="sxs-lookup"><span data-stu-id="374d4-214">Test in Machine Learning Studio</span></span>

1. <span data-ttu-id="374d4-215">На hello **МОНИТОРИНГА** hello веб-службы и щелкните hello **тест** под заголовком **конечной точки по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="374d4-215">On hello **DASHBOARD** page for hello web service, click hello **Test** button under **Default Endpoint**.</span></span> <span data-ttu-id="374d4-216">Диалоговое окно появляется и выводится hello входных данных для службы hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-216">A dialog pops up and asks you for hello input data for hello service.</span></span> <span data-ttu-id="374d4-217">Они являются hello же столбцы, которые присутствовали в наборе данных исходного кредит риск hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-217">These are hello same columns that appeared in hello original credit risk dataset.</span></span>  

2. <span data-ttu-id="374d4-218">Введите набор данных и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="374d4-218">Enter a set of data and then click **OK**.</span></span> 

#### <a name="test-in-hello-machine-learning-web-services-portal"></a><span data-ttu-id="374d4-219">Тестирование на портале веб-службы обучения машины hello</span><span class="sxs-lookup"><span data-stu-id="374d4-219">Test in hello Machine Learning Web Services portal</span></span>

1. <span data-ttu-id="374d4-220">На hello **МОНИТОРИНГА** hello веб-службы и щелкните hello **предварительного просмотра теста** ссылку в списке **конечной точки по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="374d4-220">On hello **DASHBOARD** page for hello web service, click hello **Test preview** link under **Default Endpoint**.</span></span> <span data-ttu-id="374d4-221">тестовой страницы приветствия на портале веб-службы Azure Machine Learning hello для конечной веб-службы hello открывается и запросит hello входные данные для службы hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-221">hello test page in hello Azure Machine Learning Web Services portal for hello web service endpoint opens and asks you for hello input data for hello service.</span></span> <span data-ttu-id="374d4-222">Они являются hello же столбцы, которые присутствовали в наборе данных исходного кредит риск hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-222">These are hello same columns that appeared in hello original credit risk dataset.</span></span>

2. <span data-ttu-id="374d4-223">Щелкните **Test Request-Response** (Тестировать "запрос-ответ").</span><span class="sxs-lookup"><span data-stu-id="374d4-223">Click **Test Request-Response**.</span></span> 

### <a name="test-a-new-web-service"></a><span data-ttu-id="374d4-224">Тестирование новой веб-службы</span><span class="sxs-lookup"><span data-stu-id="374d4-224">Test a New web service</span></span>

<span data-ttu-id="374d4-225">Веб-службу можно проверить только на портале веб-службы обучения машины hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-225">You can test a New web service only in hello Machine Learning Web Services portal.</span></span>

1. <span data-ttu-id="374d4-226">В hello [веб-службы Azure Machine Learning](https://services.azureml.net/quickstart) портала, нажмите кнопку **тест** вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="374d4-226">In hello [Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal, click **Test** at hello top of hello page.</span></span> <span data-ttu-id="374d4-227">Hello **тест** открывается страница, и можно ввести данные для службы hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-227">hello **Test** page opens and you can input data for hello service.</span></span> <span data-ttu-id="374d4-228">поля Hello ввода соответствуют toohello столбцы, которые присутствовали в наборе данных исходного кредит риск hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-228">hello input fields displayed correspond toohello columns that appeared in hello original credit risk dataset.</span></span> 

2. <span data-ttu-id="374d4-229">Введите набор данных и щелкните **Test Request-Response**(Тестировать "запрос-ответ").</span><span class="sxs-lookup"><span data-stu-id="374d4-229">Enter a set of data and then click **Test Request-Response**.</span></span>

<span data-ttu-id="374d4-230">Hello результаты теста hello отображаются с правой стороны страницы приветствия в выходном столбце hello hello.</span><span class="sxs-lookup"><span data-stu-id="374d4-230">hello results of hello test are displayed on hello right-hand side of hello page in hello output column.</span></span> 


## <a name="manage-hello-web-service"></a><span data-ttu-id="374d4-231">Управление hello веб-службы</span><span class="sxs-lookup"><span data-stu-id="374d4-231">Manage hello web service</span></span>

### <a name="manage-a-classic-web-service-in-hello-azure-classic-portal"></a><span data-ttu-id="374d4-232">Управление классического веб-службы в hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="374d4-232">Manage a Classic web service in hello Azure classic portal</span></span>

<span data-ttu-id="374d4-233">После развертывания классического веб-службы, вы можете управлять из hello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="374d4-233">Once you've deployed your Classic web service, you can manage it from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="374d4-234">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="374d4-234">Sign in toohello [Azure classic portal](https://manage.windowsazure.com)</span></span>
2. <span data-ttu-id="374d4-235">На панели служб Microsoft Azure hello щелкните **МАШИННОГО ОБУЧЕНИЯ**</span><span class="sxs-lookup"><span data-stu-id="374d4-235">In hello Microsoft Azure services panel, click **MACHINE LEARNING**</span></span>
3. <span data-ttu-id="374d4-236">Щелкните рабочую область.</span><span class="sxs-lookup"><span data-stu-id="374d4-236">Click your workspace</span></span>
4. <span data-ttu-id="374d4-237">Нажмите кнопку hello **веб-службы** вкладка</span><span class="sxs-lookup"><span data-stu-id="374d4-237">Click hello **Web services** tab</span></span>
5. <span data-ttu-id="374d4-238">Нажмите кнопку hello веб-службы, которую мы создали</span><span class="sxs-lookup"><span data-stu-id="374d4-238">Click hello web service we created</span></span>
6. <span data-ttu-id="374d4-239">Щелкните конечную точку «default» hello</span><span class="sxs-lookup"><span data-stu-id="374d4-239">Click hello "default" endpoint</span></span>

<span data-ttu-id="374d4-240">Здесь можно, например, отслеживать, насколько hello веб-службы и выполнить модификации производительности, изменив количество одновременных вызовов hello служба может обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="374d4-240">From here, you can do things like monitor how hello web service is doing and make performance tweaks by changing how many concurrent calls hello service can handle.</span></span>

<span data-ttu-id="374d4-241">Дополнительные сведения см. в статье</span><span class="sxs-lookup"><span data-stu-id="374d4-241">For more details, see:</span></span>

* [<span data-ttu-id="374d4-242">Создание конечных точек</span><span class="sxs-lookup"><span data-stu-id="374d4-242">Creating Endpoints</span></span>](machine-learning-create-endpoint.md)
* [<span data-ttu-id="374d4-243">Масштабирование веб-службы</span><span class="sxs-lookup"><span data-stu-id="374d4-243">Scaling web service</span></span>](machine-learning-scaling-webservice.md)

### <a name="manage-a-classic-or-new-web-service-in-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="374d4-244">Управление классического или веб-службу на портале веб-службы Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="374d4-244">Manage a Classic or New web service in hello Azure Machine Learning Web Services portal</span></span>

<span data-ttu-id="374d4-245">После развертывания веб-службы, классических или новый, вы можете управлять из hello [веб-службы Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) портала.</span><span class="sxs-lookup"><span data-stu-id="374d4-245">Once you've deployed your web service, whether Classic or New, you can manage it from hello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal.</span></span>

<span data-ttu-id="374d4-246">производительность hello toomonitor веб-службы:</span><span class="sxs-lookup"><span data-stu-id="374d4-246">toomonitor hello performance of your web service:</span></span>

1. <span data-ttu-id="374d4-247">Войдите в toohello [веб-службы Microsoft Azure Machine Learning](https://services.azureml.net/quickstart) портала</span><span class="sxs-lookup"><span data-stu-id="374d4-247">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal</span></span>
2. <span data-ttu-id="374d4-248">Щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="374d4-248">Click **Web services**</span></span>
3. <span data-ttu-id="374d4-249">Щелкните нужную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="374d4-249">Click your web service</span></span>
4. <span data-ttu-id="374d4-250">Нажмите кнопку hello **панели мониторинга**</span><span class="sxs-lookup"><span data-stu-id="374d4-250">Click hello **Dashboard**</span></span>

- - -
<span data-ttu-id="374d4-251">**Далее: [доступ к веб-службе hello](machine-learning-walkthrough-6-access-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="374d4-251">**Next: [Access hello web service](machine-learning-walkthrough-6-access-web-service.md)**</span></span>

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
