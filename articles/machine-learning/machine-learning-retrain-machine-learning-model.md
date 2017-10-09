---
title: "Модель машинного обучения aaaRetrain | Документы Microsoft"
description: "Узнайте, как tooretrain модели и обновление hello Web toouse службы hello вновь обученной модели машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="42981-103">Переобучение модели машинного обучения</span><span class="sxs-lookup"><span data-stu-id="42981-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="42981-104">В рамках процесса "hello" ввода в эксплуатацию моделей машинного обучения в машинном обучении Azure обучения модели, который сохраняется.</span><span class="sxs-lookup"><span data-stu-id="42981-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="42981-105">Затем используется toocreate predicative веб-службы.</span><span class="sxs-lookup"><span data-stu-id="42981-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="42981-106">Hello веб-службы могут быть впоследствии использованы в веб-сайтов, панели мониторинга и мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="42981-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="42981-107">Модели, создаваемые с помощью машинного обучения, обычно не статические.</span><span class="sxs-lookup"><span data-stu-id="42981-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="42981-108">По мере появления новых данных, или когда потребитель hello hello API имеет свои собственные модели данных hello должен toobe повторное обучение.</span><span class="sxs-lookup"><span data-stu-id="42981-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="42981-109">Переобучение может требоваться достаточно часто.</span><span class="sxs-lookup"><span data-stu-id="42981-109">Retraining may occur frequently.</span></span> <span data-ttu-id="42981-110">С помощью функции hello программный API переподготовки можно программным способом повторного обучения модели hello, с помощью hello переподготовки API и обновление hello веб-службы с вновь обученной модели hello.</span><span class="sxs-lookup"><span data-stu-id="42981-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="42981-111">Этот документ описывает hello переподготовки процесса и показывает, как toouse hello переподготовки API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="42981-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="42981-112">Почему обучение: определения проблемы hello</span><span class="sxs-lookup"><span data-stu-id="42981-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="42981-113">В рамках машинного обучения hello обучения процесса обучения модели с помощью набора данных.</span><span class="sxs-lookup"><span data-stu-id="42981-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="42981-114">Модели, создаваемые с помощью машинного обучения, обычно не статические.</span><span class="sxs-lookup"><span data-stu-id="42981-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="42981-115">По мере появления новых данных, или когда потребитель hello hello API имеет свои собственные модели данных hello должен toobe повторное обучение.</span><span class="sxs-lookup"><span data-stu-id="42981-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="42981-116">В этих сценариях программный интерфейс API предоставляет tooallow удобным способом вы или hello потребитель вашей toocreate интерфейсов API клиента, который может на основе однократное или регулярное Обучение модели hello, используя свои собственные данные.</span><span class="sxs-lookup"><span data-stu-id="42981-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="42981-117">Их можно оценить результаты hello переподготовки и обновить hello Web API toouse hello вновь обученной модели службы.</span><span class="sxs-lookup"><span data-stu-id="42981-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="42981-118">Если имеется существующий эксперимента обучения и новых веб-службы, вы можете toocheck ожидания повторного обучения существующих прогнозных Web службы вместо следующего пошагового руководства hello, упомянутые в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="42981-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="42981-119">Комплексный рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="42981-119">End-to-end workflow</span></span>
<span data-ttu-id="42981-120">Hello процесс включает в себя следующие компоненты hello: эксперимента обучения и прогнозирования эксперимента опубликованы как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="42981-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="42981-121">tooenable переподготовки обученной модели hello эксперимента обучения должны быть опубликованы как веб-службы с выходом hello обученной модели.</span><span class="sxs-lookup"><span data-stu-id="42981-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="42981-122">Это позволяет модель toohello API доступа для повторного обучения.</span><span class="sxs-lookup"><span data-stu-id="42981-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="42981-123">Привет, следующие шаги применяются tooboth New и классического веб-службы.</span><span class="sxs-lookup"><span data-stu-id="42981-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="42981-124">Создайте hello начальной прогнозирующей веб-службы:</span><span class="sxs-lookup"><span data-stu-id="42981-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="42981-125">Создание обучающего эксперимента</span><span class="sxs-lookup"><span data-stu-id="42981-125">Create a training experiment</span></span>
* <span data-ttu-id="42981-126">Создайте прогнозный веб-эксперимент.</span><span class="sxs-lookup"><span data-stu-id="42981-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="42981-127">Разверните прогнозную веб-службу.</span><span class="sxs-lookup"><span data-stu-id="42981-127">Deploy a predictive web service</span></span>

<span data-ttu-id="42981-128">Обучение hello веб-службы:</span><span class="sxs-lookup"><span data-stu-id="42981-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="42981-129">Обновить tooallow эксперимента обучения для повторного обучения</span><span class="sxs-lookup"><span data-stu-id="42981-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="42981-130">Развертывание hello переподготовки веб-службы</span><span class="sxs-lookup"><span data-stu-id="42981-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="42981-131">Использовать модель hello службы пакетного выполнения кода tooretrain hello</span><span class="sxs-lookup"><span data-stu-id="42981-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="42981-132">Пошаговое руководство по hello в предыдущих шагах, в разделе [машинного обучения, повторного обучения моделей программным способом](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="42981-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="42981-133">toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="42981-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="42981-134">Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="42981-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="42981-135">Если развернута классическая веб-служба, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="42981-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="42981-136">Создайте новую конечную точку на hello прогнозирующей веб-службы</span><span class="sxs-lookup"><span data-stu-id="42981-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="42981-137">Получить URL-адрес обновления hello и кода</span><span class="sxs-lookup"><span data-stu-id="42981-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="42981-138">Исправление для URL-адрес toopoint используйте hello hello новую конечную точку на hello повторное Обучение модели</span><span class="sxs-lookup"><span data-stu-id="42981-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="42981-139">Пошаговое руководство по hello в предыдущих шагах, в разделе [обучение классического веб-службы](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="42981-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="42981-140">Если возникли трудности, переподготовки классического веб-службы, см. раздел [Устранение неполадок hello переподготовки машины Azure обучения классического веб-службы](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="42981-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="42981-141">Если развернута новая веб-служба, необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="42981-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="42981-142">Войдите в tooyour учетной записи диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="42981-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="42981-143">Получить определение hello веб-службы</span><span class="sxs-lookup"><span data-stu-id="42981-143">Get hello Web service definition</span></span>
* <span data-ttu-id="42981-144">Экспорт hello определение веб-службы как JSON</span><span class="sxs-lookup"><span data-stu-id="42981-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="42981-145">Обновить ссылку toohello hello `ilearner` большого двоичного объекта в hello JSON</span><span class="sxs-lookup"><span data-stu-id="42981-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="42981-146">Импортировать hello JSON в определении веб-службы</span><span class="sxs-lookup"><span data-stu-id="42981-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="42981-147">Обновить hello веб-службы с помощью нового определения веб-службы</span><span class="sxs-lookup"><span data-stu-id="42981-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="42981-148">Пошаговое руководство по hello в предыдущих шагах, в разделе [обучение новых веб-службы с помощью командлетов PowerShell для управления обучения машины hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="42981-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="42981-149">Hello процесс настройки переподготовки классического веб-службы включает в себя hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="42981-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![Обзор процесса переобучения][1]

<span data-ttu-id="42981-151">Hello процесс настройки переподготовки новый веб-службы включает в себя hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="42981-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![Обзор процесса переобучения][7]

## <a name="other-resources"></a><span data-ttu-id="42981-153">Другие ресурсы</span><span class="sxs-lookup"><span data-stu-id="42981-153">Other Resources</span></span>
* <span data-ttu-id="42981-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/) (Переобучение и обновление моделей машинного обучения Azure с фабрикой данных Azure).</span><span class="sxs-lookup"><span data-stu-id="42981-154">[Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)</span></span>
* <span data-ttu-id="42981-155">[Создание множества моделей машинного обучения и конечных точек веб-службы из одного эксперимента с помощью PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="42981-155">[Create many Machine Learning models and web service endpoints from one experiment using PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md)</span></span>
* <span data-ttu-id="42981-156">Hello [AML переподготовки моделей с помощью API-интерфейсов](https://www.youtube.com/watch?v=wwjglA8xllg) видео показано, как tooretrain машинного обучения модели созданы в машинном обучении Azure с помощью hello, переподготовки API и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="42981-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

