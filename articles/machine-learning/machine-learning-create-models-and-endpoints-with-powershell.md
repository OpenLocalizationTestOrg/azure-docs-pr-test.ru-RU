---
title: "Создание множества моделей из одного эксперимента | Документация Майкрософт"
description: "Используйте PowerShell для создания нескольких моделей машинного обучения и конечных точек веб-службы с одним алгоритмом, но разными наборами данных для обучения."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 21d8c1ee0877df8d317d5a14131dc574fa5303c4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="b3349-103">Создание множества моделей машинного обучения и конечных точек веб-службы из одного эксперимента с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3349-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="b3349-104">С машинным обучением часто возникает следующая проблема: требуется создать множество моделей, имеющих одинаковый рабочий процесс обучения и одинаковый алгоритм, но использующих разные наборы данных для обучения на входе.</span><span class="sxs-lookup"><span data-stu-id="b3349-104">Here's a common machine learning problem: You want to create many models that have the same training workflow and use the same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="b3349-105">В этой статье показано, как это сделать с требуемым масштабом в Студии машинного обучения Azure, используя всего один эксперимент.</span><span class="sxs-lookup"><span data-stu-id="b3349-105">This article shows you how to do this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="b3349-106">Предположим, что вы являетесь владельцем международного бизнеса по предоставлению франшиз на аренду велосипедов.</span><span class="sxs-lookup"><span data-stu-id="b3349-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="b3349-107">Вы хотите создать модель регрессии, чтобы прогнозировать спрос, основываясь на исторических данных.</span><span class="sxs-lookup"><span data-stu-id="b3349-107">You want to build a regression model to predict the rental demand based on historic data.</span></span> <span data-ttu-id="b3349-108">Вы управляете 1000 пунктов аренды точек по всему миру и собрали для каждой из них набор данных, включающий важные показатели по каждому расположению, например даты, время, погоду и дорожное движение.</span><span class="sxs-lookup"><span data-stu-id="b3349-108">You have 1,000 rental locations across the world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific to each location.</span></span>

<span data-ttu-id="b3349-109">Вы можете обучить модель один раз, используя совокупную версию всех наборов данных для всех расположений.</span><span class="sxs-lookup"><span data-stu-id="b3349-109">You could train your model once using a merged version of all the datasets across all locations.</span></span> <span data-ttu-id="b3349-110">Однако, так как каждая точка работает в уникальной среде, модель регрессии лучше обучить, используя отдельные наборы данных для каждого расположения.</span><span class="sxs-lookup"><span data-stu-id="b3349-110">But because each of your locations has a unique environment, a better approach would be to train your regression model separately using the dataset for each location.</span></span> <span data-ttu-id="b3349-111">При этом каждая обученная модель может учитывать различные показатели размера, объема, географического положения, населения, наличия условий для езды на велосипеде *и т. д.*у точек.</span><span class="sxs-lookup"><span data-stu-id="b3349-111">That way, each trained model could take into account the different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="b3349-112">Возможно, это и лучший подход, но вы не захотите создавать 1000 экспериментов по машинному обучению Azure, каждый из которых представляет отдельную точку.</span><span class="sxs-lookup"><span data-stu-id="b3349-112">That may be the best approach, but you don't want to create 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="b3349-113">Кроме перегруженности, такой подход довольно неэффективен, так как каждый эксперимент будет иметь одинаковые компоненты, за исключением набора данных для обучения.</span><span class="sxs-lookup"><span data-stu-id="b3349-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all the same components except for the training dataset.</span></span>

<span data-ttu-id="b3349-114">К счастью, этой цели можно достичь, используя [API переобучения Машинного обучения Azure](machine-learning-retrain-models-programmatically.md) и автоматизировав задачу с помощью [PowerShell для Машинного обучения Microsoft Azure](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="b3349-114">Fortunately, we can accomplish this by using the [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating the task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b3349-115">Чтобы ускорить выполнение , мы уменьшаем количество расположений с 1000 до 10.</span><span class="sxs-lookup"><span data-stu-id="b3349-115">To make our sample run faster, we'll reduce the number of locations from 1,000 to 10.</span></span> <span data-ttu-id="b3349-116">Однако в случае с 1000 расположений применяются все те же принципы и процедуры.</span><span class="sxs-lookup"><span data-stu-id="b3349-116">But the same principles and procedures apply to 1,000 locations.</span></span> <span data-ttu-id="b3349-117">Единственное отличие заключается в том, что при обучении по 1000 наборам данных следует рассмотреть возможность параллельного выполнения приведенных ниже сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3349-117">The only difference is that if you want to train from 1,000 datasets you probably want to think of running the following PowerShell scripts in parallel.</span></span> <span data-ttu-id="b3349-118">Этот вопрос выходит за рамки данной статьи, но примеры многопоточности PowerShell можно найти в Интернете.</span><span class="sxs-lookup"><span data-stu-id="b3349-118">How to do that is beyond the scope of this article, but you can find examples of PowerShell multi-threading on the Internet.</span></span>  
> 
> 

## <a name="set-up-the-training-experiment"></a><span data-ttu-id="b3349-119">настройка обучающего эксперимента</span><span class="sxs-lookup"><span data-stu-id="b3349-119">Set up the training experiment</span></span>
<span data-ttu-id="b3349-120">Мы будем использовать уже готовый пример [обучающего эксперимента](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) из [коллекции Cortana Intelligence](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="b3349-120">We're going to use an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="b3349-121">Откройте этот эксперимент в рабочей области [Студии машинного обучения Azure](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="b3349-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="b3349-122">Для работы с этим примером рекомендуется использовать стандартную рабочую область, а не бесплатную.</span><span class="sxs-lookup"><span data-stu-id="b3349-122">In order to follow along with this example, you may want to use a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="b3349-123">Мы создадим одну конечную точку для каждого заказчика общим числом 10, и для этого потребуется стандартная рабочая область, так как бесплатная рабочая область ограничена 3 конечными точками.</span><span class="sxs-lookup"><span data-stu-id="b3349-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited to 3 endpoints.</span></span> <span data-ttu-id="b3349-124">Если у вас имеется только бесплатная рабочая область, просто измените приведенные ниже сценарии, чтобы разрешить только 3 расположения.</span><span class="sxs-lookup"><span data-stu-id="b3349-124">If you only have a free workspace, just modify the scripts below to allow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="b3349-125">Эксперимент использует модуль **Импорт данных** , чтобы импортировать набор данных для обучения *customer001.csv* из учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b3349-125">The experiment uses an **Import Data** module to import the training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="b3349-126">Предположим, что мы собрали наборы данных для обучения из всех пунктов аренды велосипедов и сохранили их в одном хранилище BLOB-объектов с именами от *rentalloc001.csv* до *rentalloc10.csv*.</span><span class="sxs-lookup"><span data-stu-id="b3349-126">Let's assume we have collected training datasets from all bike rental locations and stored them in the same blob storage location with file names ranging from *rentalloc001.csv* to *rentalloc10.csv*.</span></span>

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="b3349-128">Обратите внимание, что в модуль **Обучение модели** добавлен модуль **Web Service Output** (Выходные данные веб-службы).</span><span class="sxs-lookup"><span data-stu-id="b3349-128">Note that a **Web Service Output** module has been added to the **Train Model** module.</span></span>
<span data-ttu-id="b3349-129">При развертывании эксперимента в виде веб-службы конечная точка, связанная с этими выходными данными, будет возвращать обученную модель в формате ILEARNER-файла.</span><span class="sxs-lookup"><span data-stu-id="b3349-129">When this experiment is deployed as a web service, the endpoint associated with that output will return the trained model in the format of a .ilearner file.</span></span>

<span data-ttu-id="b3349-130">Обратите внимание и на то, что мы устанавливаем для параметра веб-службы URL-адрес, используемый модулем **Импорт данных** .</span><span class="sxs-lookup"><span data-stu-id="b3349-130">Also note that we set up a web service parameter for the URL that the **Import Data** module uses.</span></span> <span data-ttu-id="b3349-131">Это позволяет использовать такой параметр, чтобы указать отдельные наборы данных в целях обучения модели для каждого расположения.</span><span class="sxs-lookup"><span data-stu-id="b3349-131">This allows us to use the parameter to specify individual training datasets to train the model for each location.</span></span>
<span data-ttu-id="b3349-132">Есть и другие способы выполнения этой задачи, например с помощью SQL-запроса с параметром веб-службы для получения данных из базы данных SQL Azure или простое использование модуля **Web Service Input** (Входные данные веб-службы) для передачи набора данных в веб-службу.</span><span class="sxs-lookup"><span data-stu-id="b3349-132">There are other ways we could have done this, such as using a SQL query with a web service parameter to get data from a SQL Azure database, or simply using a  **Web Service Input** module to pass in a dataset to the web service.</span></span>

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="b3349-134">Теперь давайте запустим этот обучающий эксперимент, используя значение по умолчанию *rental001.csv* в качестве набора данных для обучения.</span><span class="sxs-lookup"><span data-stu-id="b3349-134">Now, let's run this training experiment using the default value *rental001.csv* as the training dataset.</span></span> <span data-ttu-id="b3349-135">Если просмотреть выходные данные модуля **Оценка** (щелкните выходные данные и выберите **Визуализировать**), вы увидите, что мы получаем неплохую производительность с *AUC* = 0,91.</span><span class="sxs-lookup"><span data-stu-id="b3349-135">If you view the output of the **Evaluate** module (click the output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="b3349-136">На этом этапе мы готовы развернуть веб-службу из этого обучающего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="b3349-136">At this point, we're ready to deploy a web service out of this training experiment.</span></span>

## <a name="deploy-the-training-and-scoring-web-services"></a><span data-ttu-id="b3349-137">Развертывание обучающей и оценивающей веб-служб</span><span class="sxs-lookup"><span data-stu-id="b3349-137">Deploy the training and scoring web services</span></span>
<span data-ttu-id="b3349-138">Чтобы развернуть обучающую веб-службу, нажмите кнопку **Set Up Web Service** (Настройка веб-службы) ниже холста эксперимента и выберите **Deploy Web Service** (Развертывание веб-службы).</span><span class="sxs-lookup"><span data-stu-id="b3349-138">To deploy the training web service, click the **Set Up Web Service** button below the experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="b3349-139">Назовите эту веб-службу Bike Rental Training (Обучение аренды велосипедов).</span><span class="sxs-lookup"><span data-stu-id="b3349-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="b3349-140">Теперь нам требуется развернуть оценивающую веб-службу.</span><span class="sxs-lookup"><span data-stu-id="b3349-140">Now we need to deploy the scoring web service.</span></span>
<span data-ttu-id="b3349-141">Для этого можно нажать кнопку **Set Up Web Service** (Настройка веб-службы) ниже холста и выбрать **Predictive Web Service** (Прогнозная веб-служба).</span><span class="sxs-lookup"><span data-stu-id="b3349-141">To do this, we can click **Set Up Web Service** below the canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="b3349-142">При этом создается оценивающий эксперимент.</span><span class="sxs-lookup"><span data-stu-id="b3349-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="b3349-143">Необходимо внести несколько небольших корректировок, чтобы он заработал как веб-служба, например удалить столбец метки cnt из входных данных и ограничить выходные данные лишь идентификатором экземпляра и соответствующим прогнозируемым значением.</span><span class="sxs-lookup"><span data-stu-id="b3349-143">We'll need to make a few minor adjustments to make it work as a web service, such as removing the label column "cnt" from the input data and limiting the output to only the instance id and the corresponding predicted value.</span></span>

<span data-ttu-id="b3349-144">Чтобы не выполнять все это самостоятельно, можно просто открыть уже подготовленный [прогнозный эксперимент](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) из коллекции.</span><span class="sxs-lookup"><span data-stu-id="b3349-144">To save yourself that work, you can simply open the [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in the Gallery that's already been prepared.</span></span>

<span data-ttu-id="b3349-145">Чтобы развернуть веб-службы, запустите прогнозный эксперимент, а затем щелкните **Deploy Web Service** (Развертывание веб-службы) внизу холста.</span><span class="sxs-lookup"><span data-stu-id="b3349-145">To deploy the web service, run the predictive experiment, then click the **Deploy Web Service** button below the canvas.</span></span> <span data-ttu-id="b3349-146">Назовите оценивающую веб-службу Bike Rental Scoring (Оценка аренды велосипедов).</span><span class="sxs-lookup"><span data-stu-id="b3349-146">Name the scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="b3349-147">Создание 10 идентичных конечных точек веб-службы с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3349-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="b3349-148">Эта веб-служба предоставляется с конечной точкой по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b3349-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="b3349-149">Однако нас эта конечная точка не интересует, так как ее нельзя обновить.</span><span class="sxs-lookup"><span data-stu-id="b3349-149">But we're not as interested in the default endpoint since it can't be updated.</span></span> <span data-ttu-id="b3349-150">Нам нужно создать 10 дополнительных конечных точек — по одной для каждого расположения.</span><span class="sxs-lookup"><span data-stu-id="b3349-150">What we need to do is to create 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="b3349-151">Для этого мы воспользуемся PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3349-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="b3349-152">Сначала настроим среду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b3349-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and is properly set to point to the valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="b3349-153">Затем выполним следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b3349-153">Then, run the following PowerShell command:</span></span>

    # Create 10 endpoints on the scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="b3349-154">Итак, мы создали 10 конечных точек, содержащих одинаковую модель, обученную по *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="b3349-154">Now we've created 10 endpoints and they all contain the same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="b3349-155">Их можно просмотреть на портале управления Azure.</span><span class="sxs-lookup"><span data-stu-id="b3349-155">You can view them in the Azure Management Portal.</span></span>

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-the-endpoints-to-use-separate-training-datasets-using-powershell"></a><span data-ttu-id="b3349-157">Обновление конечных точек для использования отдельных наборов данных для обучения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3349-157">Update the endpoints to use separate training datasets using PowerShell</span></span>
<span data-ttu-id="b3349-158">Следующим шагом является обновление конечных точек с использованием моделей, обученных по отдельным данным каждого из клиентов.</span><span class="sxs-lookup"><span data-stu-id="b3349-158">The next step is to update the endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="b3349-159">Но сначала необходимо создать эти модели из веб-службы **Bike Rental Training** .</span><span class="sxs-lookup"><span data-stu-id="b3349-159">But first we need to produce these models from the **Bike Rental Training** web service.</span></span> <span data-ttu-id="b3349-160">Вернемся к веб-службе **Bike Rental Training** .</span><span class="sxs-lookup"><span data-stu-id="b3349-160">Let's go back to the **Bike Rental Training** web service.</span></span> <span data-ttu-id="b3349-161">Необходимо вызвать ее конечную точку BES 10 раз с 10 разными наборами данных для обучения, чтобы создать 10 разных моделей.</span><span class="sxs-lookup"><span data-stu-id="b3349-161">We need to call its BES endpoint 10 times with 10 different training datasets in order to produce 10 different models.</span></span> <span data-ttu-id="b3349-162">Для этого мы используем командлет **InovkeAmlWebServiceBESEndpoint** PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3349-162">We'll use the **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet to do this.</span></span>

<span data-ttu-id="b3349-163">Также необходимо указать учетные данные для учетной записи хранения BLOB-объектов в `$configContent`, то есть в полях `AccountName`, `AccountKey` и `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="b3349-163">You will also need to provide credentials for your blob storage account into `$configContent`, namely, at the fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="b3349-164">В поле `AccountName` можно указать одно из имен учетной записи, как показано на **классическом портале управления Azure** (вкладка *Хранилище*).</span><span class="sxs-lookup"><span data-stu-id="b3349-164">The `AccountName` can be one of your account names, as seen in the **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="b3349-165">Выберите учетную запись хранения. Чтобы найти ее `AccountKey`, нажмите кнопку **Управление ключами доступа** и скопируйте значение поля *Первичный ключ доступа*.</span><span class="sxs-lookup"><span data-stu-id="b3349-165">Once you click on a storage account, its `AccountKey` can be found by pressing the **Manage Access Keys** button at the bottom and copying the *Primary Access Key*.</span></span> <span data-ttu-id="b3349-166">`RelativeLocation` — это путь к хранилищу, в котором будет храниться новая модель.</span><span class="sxs-lookup"><span data-stu-id="b3349-166">The `RelativeLocation` is the path relative to your storage where a new model will be stored.</span></span> <span data-ttu-id="b3349-167">Например, путь `hai/retrain/bike_rental/` в сценарии ниже указывает на контейнер с именем `hai`, а `/retrain/bike_rental/` — это вложенные папки.</span><span class="sxs-lookup"><span data-stu-id="b3349-167">For instance, the path `hai/retrain/bike_rental/` in the script below points to a container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="b3349-168">Сейчас невозможно создать вложенные папки с помощью пользовательского интерфейса портала. Но это можно сделать с помощью [нескольких обозревателей службы хранилища Azure](../storage/common/storage-explorers.md).</span><span class="sxs-lookup"><span data-stu-id="b3349-168">Currently, you cannot create subfolders through the portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you to do so.</span></span> <span data-ttu-id="b3349-169">Рекомендуется создать контейнер в хранилище для хранения новых обученных моделей (ILEARNER-файлы) следующим образом. На странице хранилища нажмите кнопку **Добавить** внизу и назовите контейнер `retrain`.</span><span class="sxs-lookup"><span data-stu-id="b3349-169">It is recommended that you create a new container in your storage to store the new trained models (.ilearner files) as follows: from your storage page, click on the **Add** button at the bottom and name it `retrain`.</span></span> <span data-ttu-id="b3349-170">Таким образом, все необходимые изменения в сценарии ниже относятся к `AccountName`, `AccountKey` и `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="b3349-170">In summary, the necassary changes to the script below pertain to `AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke the retraining API 10 times
    # This is the default (and the only) endpoint on the training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="b3349-171">Конечная точка BES является единственным поддерживаемым режимом для этой операции.</span><span class="sxs-lookup"><span data-stu-id="b3349-171">The BES endpoint is the only supported mode for this operation.</span></span> <span data-ttu-id="b3349-172">RRS использовать для создания обученных моделей нельзя.</span><span class="sxs-lookup"><span data-stu-id="b3349-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="b3349-173">Как можно заметить, вместо создания 10 разных JSON-файлов конфигурации заданий BES мы динамически создали строку конфигурации и передали ее в параметр *jobConfigString* командлета **InvokeAmlWebServceBESEndpoint** , так как в этом случае нет необходимости сохранять копию на диске.</span><span class="sxs-lookup"><span data-stu-id="b3349-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create the config string instead and feed it to the *jobConfigString* parameter of the **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need to keep a copy on disk.</span></span>

<span data-ttu-id="b3349-174">Если все работает правильно, через некоторое время в вашей учетной записи хранения Azure появятся 10 ILEARNER-файлов: от *model001.ilearner* до *model010.ilearner*.</span><span class="sxs-lookup"><span data-stu-id="b3349-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* to *model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="b3349-175">Теперь все готово для того, чтобы обновить 10 конечных точек оценивающей веб-службы с помощью этих моделей, используя командлет PowerShell **Patch-AmlWebServiceEndpoint** .</span><span class="sxs-lookup"><span data-stu-id="b3349-175">Now we're ready to update our 10 scoring web service endpoints with these models using the **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="b3349-176">Не забывайте, что изменить можно только нестандартные конечные точки, созданные ранее программным образом.</span><span class="sxs-lookup"><span data-stu-id="b3349-176">Remember again that we can only patch the non-default endpoints we programmatically created earlier.</span></span>

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="b3349-177">Процесс должен выполняться довольно быстро.</span><span class="sxs-lookup"><span data-stu-id="b3349-177">This should run fairly quickly.</span></span> <span data-ttu-id="b3349-178">По завершении выполнения создается 10 конечных точек прогнозной веб-службы, каждая из которых содержит уникальную модель, обученную по набору данных для конкретного пункта аренды, и все это — из одного обучающего эксперимента.</span><span class="sxs-lookup"><span data-stu-id="b3349-178">When the execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on the dataset specific to a rental location, all from a single training experiment.</span></span> <span data-ttu-id="b3349-179">Чтобы проверить это, попробуйте вызвать эти конечные точки с помощью командлета **InvokeAmlWebServiceRRSEndpoint**, предоставляя им одинаковые входные данные. Результаты прогноза должны отличаться, так как модели обучались с использованием разных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="b3349-179">To verify this, you can try calling these endpoints using the **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with the same input data, and you should expect to see different prediction results since the models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="b3349-180">Полный сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3349-180">Full PowerShell script</span></span>
<span data-ttu-id="b3349-181">Ниже приведен полный исходный код.</span><span class="sxs-lookup"><span data-stu-id="b3349-181">Here's the listing of the full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and properly set to point to the valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on the scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke the retraining API 10 times to produce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
