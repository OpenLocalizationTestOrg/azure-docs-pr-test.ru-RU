---
title: "Подключитесь к веб-службе машинного обучения | Документация Майкрософт"
description: "При использовании C# или Python для подключения к веб-службе машинного обучения Azure используется ключ авторизации."
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
redirect_document_id: TRUE
ms.openlocfilehash: 0fc6c7e921b18eb14a95fb737d8fb5ab5cc7e687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-an-azure-machine-learning-web-service"></a><span data-ttu-id="9ecb8-103">Подключение к веб-службе машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="9ecb8-103">Connect to an Azure Machine Learning Web Service</span></span>
<span data-ttu-id="9ecb8-104">Среда разработки Машинного обучения Azure — это API веб-службы, предназначенный для прогнозирования на основе входных данных в режиме реального времени или в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="9ecb8-105">Студия машинного обучения Azure используется для создания прогнозов и их развертывания в веб-службе машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="9ecb8-106">Чтобы узнать, как создать и развернуть веб-службу машинного обучения с помощью Студии машинного обучения Azure, см. следующие разделы:</span><span class="sxs-lookup"><span data-stu-id="9ecb8-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="9ecb8-107">Руководство по созданию эксперимента в Студии машинного обучения см. в [этой статье](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="9ecb8-108">Дополнительные сведения о развертывании веб-службы см. в [этой статье](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="9ecb8-109">Дополнительные сведения о машинном обучении см. в [центре документации по Машинному обучению Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="9ecb8-110">Веб-служба машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="9ecb8-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="9ecb8-111">С помощью веб-службы машинного обучения Azure внешнее приложение взаимодействует с рабочим процессом машинного обучения, оценивая модель в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="9ecb8-112">Вызов веб-службы машинного обучения возвращает результаты прогноза внешнему приложению.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="9ecb8-113">Чтобы вызвать веб-службу машинного обучения, следует передать ключ API, создаваемый при развертывании прогноза.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="9ecb8-114">Веб-служба машинного обучения работает на основе архитектуры REST, используемой в основном в проектах с веб-программированием.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="9ecb8-115">Машинное обучение Azure содержит два типа служб:</span><span class="sxs-lookup"><span data-stu-id="9ecb8-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="9ecb8-116">Служба обработки запросов и ответов (RRS) — высокомасштабируемая служба с малым временем задержки, используемая в качестве интерфейса для моделей без изменения состояния, которые создаются и развертываются в студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="9ecb8-117">Служба пакетного выполнения (BES) — асинхронная служба, оценивающая пакет записей данных.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="9ecb8-118">Дополнительные сведения о веб-службах машинного обучения приведены в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="9ecb8-119">Получение ключа авторизации машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="9ecb8-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="9ecb8-120">При развертывании эксперимента создаются ключи API для веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="9ecb8-121">Ключи можно извлечь из нескольких расположений.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="9ecb8-122">Из портала веб-службы Машинного обучения Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9ecb8-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="9ecb8-123">Войдите на портал [веб-службы Машинного обучения Microsoft Azure](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="9ecb8-124">Чтобы получить ключ API для новой веб-службы машинного обучения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9ecb8-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="9ecb8-125">На портале веб-служб Машинного обучения Azure в верхнем меню щелкните **Веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="9ecb8-126">Щелкните веб-службу, для которой требуется получить ключ.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="9ecb8-127">В верхнем меню щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="9ecb8-128">Скопируйте и сохраните **Primary Key**(Первичный ключ).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="9ecb8-129">Чтобы получить ключ API для классической веб-службы машинного обучения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9ecb8-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="9ecb8-130">На портале веб-служб Машинного обучения Azure в верхнем меню щелкните **Classic Web Services** (Классические веб-службы).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="9ecb8-131">Выберите веб-службу, с которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="9ecb8-132">Щелкните конечную точку, для которой требуется получить ключ.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="9ecb8-133">В верхнем меню щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="9ecb8-134">Скопируйте и сохраните **Primary Key**(Первичный ключ).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="9ecb8-135">Классическая веб-служба</span><span class="sxs-lookup"><span data-stu-id="9ecb8-135">Classic Web service</span></span>
 <span data-ttu-id="9ecb8-136">Ключ для классической веб-службы можно также получить в Студии машинного обучения или на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="9ecb8-137">Студия машинного обучения</span><span class="sxs-lookup"><span data-stu-id="9ecb8-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="9ecb8-138">В студии машинного обучения щелкните **WEB SERVICES** (ВЕБ-СЛУЖБЫ) слева.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="9ecb8-139">Щелкните веб-службу.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-139">Click a Web service.</span></span> <span data-ttu-id="9ecb8-140">**Ключ API** указан на вкладке **Панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="9ecb8-141">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="9ecb8-141">Azure classic portal</span></span>
1. <span data-ttu-id="9ecb8-142">Щелкните **МАШИННОЕ ОБУЧЕНИЕ** слева.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="9ecb8-143">Щелкните рабочую область, в которой находится веб-служба.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="9ecb8-144">Щелкните **ВЕБ-СЛУЖБЫ**.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="9ecb8-145">Щелкните веб-службу.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-145">Click a Web service.</span></span>
5. <span data-ttu-id="9ecb8-146">Щелкните конечную точку.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-146">Click an endpoint.</span></span> <span data-ttu-id="9ecb8-147">Элемент "КЛЮЧ API" находится в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-147">The “API KEY” is down at the lower-right.</span></span>

## <span data-ttu-id="9ecb8-148"><a id="connect"></a>Подключение к веб-службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="9ecb8-148"><a id="connect"></a>Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="9ecb8-149">К веб-службе машинного обучения можно подключиться, используя любой язык программирования, поддерживающий HTTP-запрос и HTTP-ответ.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="9ecb8-150">Примеры на языках C#, Python и R можно просмотреть на странице справки веб-службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="9ecb8-151">**Справка по API машинного обучения.** Страница справки по API машинного обучения Azure создается при развертывании веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="9ecb8-152">См. статью [Шаг 5. Развертывание веб-службы машинного обучения Azure](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="9ecb8-153">Справка по API машинного обучения содержит сведения о веб-службе прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="9ecb8-154">Выберите веб-службу, с которой вы работаете.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="9ecb8-155">Щелкните конечную точку, для которой требуется просмотреть страницу справки по API.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="9ecb8-156">В верхнем меню щелкните **Consume**(Использование).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="9ecb8-157">Щелкните **API help page** (Страница справки API) под конечными точками "Запрос — ответ" или "Выполнение пакета".</span><span class="sxs-lookup"><span data-stu-id="9ecb8-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="9ecb8-158">**Просмотр справки по API машинного обучения для новой веб-службы**</span><span class="sxs-lookup"><span data-stu-id="9ecb8-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="9ecb8-159">На портале веб-служб Машинного обучения Azure:</span><span class="sxs-lookup"><span data-stu-id="9ecb8-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="9ecb8-160">В верхнем меню щелкните **WEB SERVICES** (ВЕБ-СЛУЖБЫ).</span><span class="sxs-lookup"><span data-stu-id="9ecb8-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="9ecb8-161">Щелкните веб-службу, для которой требуется получить ключ.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="9ecb8-162">Щелкните **Consume** (Использование), чтобы получить URI для службы "запрос-ответ" и службы пакетного выполнения, а также для примера кода на C#, R и Python.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="9ecb8-163">Щелкните **Swagger API**, чтобы получить документацию на основе Swagger для интерфейсов API, вызываемых из передаваемых URI.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="9ecb8-164">Пример на языке C#</span><span class="sxs-lookup"><span data-stu-id="9ecb8-164">C# Sample</span></span>
<span data-ttu-id="9ecb8-165">Для подключения к веб-службе машинного обучения воспользуйтесь клиентом **HttpClient**, передав ScoreData.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="9ecb8-166">Данные набора содержат Вектор свойств, n-мерный вектор числовых параметров, представляющий Данные набора.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="9ecb8-167">Службу машинного обучения можно аутентифицировать с помощью ключа API.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="9ecb8-168">Для подключения к веб-службе машинного обучения должен быть установлен пакет NuGet **Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="9ecb8-169">**Установка Microsoft.AspNet.WebApi.Client NuGet в Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="9ecb8-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="9ecb8-170">Опубликуйте набор данных Загрузки из набора UCI: Adult 2 веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="9ecb8-171">Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="9ecb8-172">Выберите **Установить пакет Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="9ecb8-173">**Для запуска примера выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9ecb8-173">**To run the code sample**</span></span>

1. <span data-ttu-id="9ecb8-174">Опубликуйте эксперимент "Пример 1. Загрузка набора данных из UCI: набор данных для класса Adult 2", входящий в набор примеров машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="9ecb8-175">Назначьте apiKey ключ из веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="9ecb8-176">См. раздел **Получение ключа авторизации Машинного обучения Azure** выше.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="9ecb8-177">Назначьте serviceUri универсальный код ресурса запроса.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="9ecb8-178">Пример на Python</span><span class="sxs-lookup"><span data-stu-id="9ecb8-178">Python Sample</span></span>
<span data-ttu-id="9ecb8-179">Для подключения к веб-службе машинного обучения воспользуйтесь библиотекой **urllib2**, передав ScoreData.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="9ecb8-180">Данные набора содержат FeatureVector, n-мерный вектор числовых параметров, представляющий ScoreData.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="9ecb8-181">Службу машинного обучения можно аутентифицировать с помощью ключа API.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="9ecb8-182">**Для запуска примера выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9ecb8-182">**To run the code sample**</span></span>

1. <span data-ttu-id="9ecb8-183">Разверните эксперимент "Sample 1: Download dataset from UCI: Adult 2 class dataset" (Пример 1. Скачивание набора данных из UCI: набор данных для класса Adult 2), входящий в набор примеров машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="9ecb8-184">Назначьте apiKey ключ из веб-службы.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="9ecb8-185">См. раздел **Получение ключа авторизации Машинного обучения Azure** в начале этой статьи.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="9ecb8-186">Назначьте serviceUri универсальный код ресурса запроса.</span><span class="sxs-lookup"><span data-stu-id="9ecb8-186">Assign serviceUri with the Request URI.</span></span>

