---
title: "aaaConnect tooa веб-службы обучения машины | Документы Microsoft"
description: "С помощью C# или Python подключаться tooan Azure машины обучения, веб-службы, с помощью ключа авторизации."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a><span data-ttu-id="e0e0d-103">Подключение веб-служба Azure Machine Learning tooan</span><span class="sxs-lookup"><span data-stu-id="e0e0d-103">Connect tooan Azure Machine Learning Web Service</span></span>
<span data-ttu-id="e0e0d-104">Hello опыт разработки машинного обучения Azure является прогнозы веб-службы API toomake из входных данных в режиме реального времени или в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-104">hello Azure Machine Learning developer experience is a Web service API toomake predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="e0e0d-105">Используйте прогнозы toocreate студии машинного обучения Azure и развертывания служб Azure Machine Learning Web.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-105">You use Azure Machine Learning Studio toocreate predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="e0e0d-106">toolearn о том, как toocreate и развертывать веб-машины обучения службы с помощью студии машинного обучения:</span><span class="sxs-lookup"><span data-stu-id="e0e0d-106">toolearn about how toocreate and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="e0e0d-107">Учебник по toocreate эксперимента в студии машинного обучения. в статье [создать свой первый эксперимент](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="e0e0d-107">For a tutorial on how toocreate an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="e0e0d-108">Дополнительные сведения о том, как toodeploy веб-службы, в разделе [развертывание веб-машины обучения службы](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e0e0d-108">For details on how toodeploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="e0e0d-109">Дополнительные сведения о машинного обучения в целом посетите hello [центр документации машинного обучения](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="e0e0d-109">For more information about Machine Learning in general, visit hello [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="e0e0d-110">Веб-служба машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e0e0d-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="e0e0d-111">С hello Azure Machine Learning, веб-службы внешнее приложение взаимодействует с оценки модели машинного обучения рабочего процесса в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-111">With hello Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="e0e0d-112">Вызов веб-машины обучения службы возвращает результаты прогноза tooan внешнее приложение.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-112">A Machine Learning Web service call returns prediction results tooan external application.</span></span> <span data-ttu-id="e0e0d-113">toomake вызов веб-машины обучения службы передать ключ API, который создается при развертывании прогноз.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-113">toomake a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="e0e0d-114">Hello веб-машины обучения служба основана на REST является вариантом популярных архитектура веб-программирования проектов.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-114">hello Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="e0e0d-115">Машинное обучение Azure содержит два типа служб:</span><span class="sxs-lookup"><span data-stu-id="e0e0d-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="e0e0d-116">Запрос-ответ службы (RR) — небольшую задержку, высокую масштабируемость службы, которая предоставляет интерфейс toohello без сохранения состояния модели созданы и развертываются из hello студии машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface toohello stateless models created and deployed from hello Machine Learning Studio.</span></span>
* <span data-ttu-id="e0e0d-117">Служба пакетного выполнения (BES) — асинхронная служба, оценивающая пакет записей данных.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="e0e0d-118">Дополнительные сведения о веб-службах машинного обучения приведены в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e0e0d-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="e0e0d-119">Получение ключа авторизации машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="e0e0d-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="e0e0d-120">При развертывании эксперимента ключи API создаются для hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-120">When you deploy your experiment, API keys are generated for hello Web service.</span></span> <span data-ttu-id="e0e0d-121">Можно получить hello ключи из нескольких мест.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-121">You can retrieve hello keys from several locations.</span></span>

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="e0e0d-122">Из портала веб-службы Microsoft Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="e0e0d-122">From hello Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="e0e0d-123">Войдите в toohello [веб-службы Microsoft Azure Machine Learning](https://services.azureml.net) портала.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="e0e0d-124">ключ hello API tooretrieve новый обучения машины веб-службы:</span><span class="sxs-lookup"><span data-stu-id="e0e0d-124">tooretrieve hello API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="e0e0d-125">На портале веб-службы Azure Machine Learning hello щелкните **веб-службы** hello верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-125">In hello Azure Machine Learning Web Services portal, click **Web Services** hello top menu.</span></span>
2. <span data-ttu-id="e0e0d-126">Щелкните hello веб-службы, для которого требуется ключ tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-126">Click hello Web service for which you want tooretrieve hello key.</span></span>
3. <span data-ttu-id="e0e0d-127">Hello верхнего меню **использование**.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-127">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="e0e0d-128">Скопируйте и сохраните hello **первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-128">Copy and save hello **Primary Key**.</span></span>

<span data-ttu-id="e0e0d-129">ключ hello API tooretrieve классический обучения машины веб-службы:</span><span class="sxs-lookup"><span data-stu-id="e0e0d-129">tooretrieve hello API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="e0e0d-130">На портале веб-службы Azure Machine Learning hello щелкните **классического веб-служб** hello верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-130">In hello Azure Machine Learning Web Services portal, click **Classic Web Services** hello top menu.</span></span>
2. <span data-ttu-id="e0e0d-131">Щелкните hello веб-службы, с которым вы работаете.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-131">Click hello Web service with which you are working.</span></span>
3. <span data-ttu-id="e0e0d-132">Щелкните конечную точку hello, для которого требуется ключ tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-132">Click hello endpoint for which you want tooretrieve hello key.</span></span>
4. <span data-ttu-id="e0e0d-133">Hello верхнего меню **использование**.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-133">On hello top menu, click **Consume**.</span></span>
5. <span data-ttu-id="e0e0d-134">Скопируйте и сохраните hello **первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-134">Copy and save hello **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="e0e0d-135">Классическая веб-служба</span><span class="sxs-lookup"><span data-stu-id="e0e0d-135">Classic Web service</span></span>
 <span data-ttu-id="e0e0d-136">Также можно извлечь ключ для классического веб-службы из студии машинного обучения или hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or hello Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="e0e0d-137">Студия машинного обучения</span><span class="sxs-lookup"><span data-stu-id="e0e0d-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="e0e0d-138">В студии машинного обучения, нажмите кнопку **веб-службы** hello левой части экрана.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-138">In Machine Learning Studio, click **WEB SERVICES** on hello left.</span></span>
2. <span data-ttu-id="e0e0d-139">Щелкните веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-139">Click a Web service.</span></span> <span data-ttu-id="e0e0d-140">Hello **ключ API** на hello **МОНИТОРИНГА** вкладки.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-140">hello **API key** is on hello **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="e0e0d-141">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="e0e0d-141">Azure classic portal</span></span>
1. <span data-ttu-id="e0e0d-142">Нажмите кнопку **МАШИННОГО ОБУЧЕНИЯ** hello левой части экрана.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-142">Click **MACHINE LEARNING** on hello left.</span></span>
2. <span data-ttu-id="e0e0d-143">Щелкните рабочую область hello, в котором находится веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-143">Click hello workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="e0e0d-144">Щелкните **ВЕБ-СЛУЖБЫ**.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="e0e0d-145">Щелкните веб-службу.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-145">Click a Web service.</span></span>
5. <span data-ttu-id="e0e0d-146">Щелкните конечную точку.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-146">Click an endpoint.</span></span> <span data-ttu-id="e0e0d-147">Hello «API-ключ» не работает в правый нижний hello.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-147">hello “API KEY” is down at hello lower-right.</span></span>

## <span data-ttu-id="e0e0d-148"><a id="connect"></a>Подключение tooa веб-машины обучения службы</span><span class="sxs-lookup"><span data-stu-id="e0e0d-148"><a id="connect"></a>Connect tooa Machine Learning Web service</span></span>
<span data-ttu-id="e0e0d-149">Можно подключить tooa веб-машины обучения службы, с помощью любого языка программирования, которая поддерживает HTTP-запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-149">You can connect tooa Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="e0e0d-150">Примеры на языках C#, Python и R можно просмотреть на странице справки веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="e0e0d-151">**Справка по API машинного обучения.** Страница справки по API машинного обучения Azure создается при развертывании веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="e0e0d-152">См. статью [Шаг 5. Развертывание веб-службы машинного обучения Azure](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e0e0d-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="e0e0d-153">Hello API обучения машины справки содержит сведения об прогноз веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-153">hello Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="e0e0d-154">Щелкните hello веб-службы, с которым вы работаете.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-154">Click hello Web service with which you are working.</span></span>
2. <span data-ttu-id="e0e0d-155">Щелкните конечную точку hello, для которого требуется hello tooview страница справки по API.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-155">Click hello endpoint for which you want tooview hello API Help Page.</span></span>
3. <span data-ttu-id="e0e0d-156">Hello верхнего меню **использование**.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-156">On hello top menu, click **Consume**.</span></span>
4. <span data-ttu-id="e0e0d-157">Нажмите кнопку **страница справки по API** hello запрос-ответ или конечные точки выполнения пакета.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-157">Click **API help page** under either hello Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="e0e0d-158">**tooview API обучения машины справки для нового веб-службы**</span><span class="sxs-lookup"><span data-stu-id="e0e0d-158">**tooview Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="e0e0d-159">В hello Azure машины обучения веб-служб портала:</span><span class="sxs-lookup"><span data-stu-id="e0e0d-159">In hello Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="e0e0d-160">Нажмите кнопку **веб-службы** hello верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-160">Click **WEB SERVICES** on hello top menu.</span></span>
2. <span data-ttu-id="e0e0d-161">Щелкните hello веб-службы, для которого требуется ключ tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-161">Click hello Web service for which you want tooretrieve hello key.</span></span>

<span data-ttu-id="e0e0d-162">Нажмите кнопку **использование** tooget hello идентификаторы URI для hello Reposonse запрос и службы выполнения пакета и образец кода на C#, R и Python.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-162">Click **Consume** tooget hello URIs for hello Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="e0e0d-163">Нажмите кнопку **Swagger API** tooget Swagger документации hello API-интерфейсы на основе вызова из hello предоставленный идентификаторы URI.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-163">Click **Swagger API** tooget Swagger based documentation for hello APIs called from hello supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="e0e0d-164">Пример на языке C#</span><span class="sxs-lookup"><span data-stu-id="e0e0d-164">C# Sample</span></span>
<span data-ttu-id="e0e0d-165">Используйте tooconnect tooa веб-машины обучения службы **HttpClient** ScoreData передачи.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-165">tooconnect tooa Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="e0e0d-166">ScoreData содержит FeatureVector n мерный вектор числовые функции, представляющий hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="e0e0d-167">Можно проверить подлинность службы машинного обучения toohello ключ API.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-167">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="e0e0d-168">hello tooconnect tooa веб-машины обучения службы **Microsoft.AspNet.WebApi.Client** необходимо установить пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-168">tooconnect tooa Machine Learning Web service, hello **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="e0e0d-169">**Установка Microsoft.AspNet.WebApi.Client NuGet в Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="e0e0d-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="e0e0d-170">Опубликовать данные загрузки hello из UCI: dataset для взрослых 2 класса веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-170">Publish hello Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="e0e0d-171">Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="e0e0d-172">Выберите **Установить пакет Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="e0e0d-173">**Образец кода hello toorun**</span><span class="sxs-lookup"><span data-stu-id="e0e0d-173">**toorun hello code sample**</span></span>

1. <span data-ttu-id="e0e0d-174">Опубликовать «пример 1: загрузить набора данных UCI: взрослого 2 класса dataset» эксперимент, являющееся частью коллекции машинного обучения образец hello.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="e0e0d-175">Назначьте apiKey с ключом hello из веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-175">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="e0e0d-176">См. раздел **Получение ключа авторизации Машинного обучения Azure** выше.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="e0e0d-177">Назначьте serviceUri с hello URI запроса.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-177">Assign serviceUri with hello Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="e0e0d-178">Пример на Python</span><span class="sxs-lookup"><span data-stu-id="e0e0d-178">Python Sample</span></span>
<span data-ttu-id="e0e0d-179">tooconnect tooa веб-машины обучения службы, используйте hello **urllib2** передачи ScoreData библиотеки.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-179">tooconnect tooa Machine Learning Web service, use hello **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="e0e0d-180">ScoreData содержит FeatureVector n мерный вектор числовые функции, представляющий hello ScoreData.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents hello ScoreData.</span></span> <span data-ttu-id="e0e0d-181">Можно проверить подлинность службы машинного обучения toohello ключ API.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-181">You authenticate toohello Machine Learning service with an API key.</span></span>

<span data-ttu-id="e0e0d-182">**Образец кода hello toorun**</span><span class="sxs-lookup"><span data-stu-id="e0e0d-182">**toorun hello code sample**</span></span>

1. <span data-ttu-id="e0e0d-183">Развертывание «пример 1: загрузить набора данных UCI: взрослого 2 класса dataset» эксперимент, являющееся частью коллекции машинного обучения образец hello.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of hello Machine Learning sample collection.</span></span>
2. <span data-ttu-id="e0e0d-184">Назначьте apiKey с ключом hello из веб-службы.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-184">Assign apiKey with hello key from a Web service.</span></span> <span data-ttu-id="e0e0d-185">В разделе hello **получить ключ авторизации машинного обучения Azure** раздел hello начале этой статьи.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-185">See hello **Get an Azure Machine Learning authorization key** section near hello beginning of this article.</span></span>
3. <span data-ttu-id="e0e0d-186">Назначьте serviceUri с hello URI запроса.</span><span class="sxs-lookup"><span data-stu-id="e0e0d-186">Assign serviceUri with hello Request URI.</span></span>

