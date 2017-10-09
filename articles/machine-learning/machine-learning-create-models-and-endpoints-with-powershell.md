---
title: "aaaCreate нескольких моделей из одной эксперимента | Документы Microsoft"
description: "С помощью PowerShell toocreate несколько моделей машинного обучения и веб-конечные точки службы с hello того же алгоритма, но разных обучающих наборах данных."
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
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="1198c-103">Создание множества моделей машинного обучения и конечных точек веб-службы из одного эксперимента с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1198c-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="1198c-104">Вот распространенные задачи машинного обучения: требуется несколько моделей, имеющих hello toocreate же рабочий процесс обучения и использования hello того же алгоритма, но имеют разные обучающих наборов данных в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="1198c-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="1198c-105">В этой статье показано, как toodo это в масштабе в студии машинного обучения Azure с помощью только одного эксперимента.</span><span class="sxs-lookup"><span data-stu-id="1198c-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="1198c-106">Предположим, что вы являетесь владельцем международного бизнеса по предоставлению франшиз на аренду велосипедов.</span><span class="sxs-lookup"><span data-stu-id="1198c-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="1198c-107">Вы хотите toobuild требование аренды hello toopredict модели регрессии на основе исторических данных.</span><span class="sxs-lookup"><span data-stu-id="1198c-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="1198c-108">Имеется 1000 расположения аренды через Здравствуй, мир! и собрали набора данных для каждого расположение, которое включает в себя важные компоненты, например даты, времени, погоды и трафика, которые tooeach определенного расположения.</span><span class="sxs-lookup"><span data-stu-id="1198c-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="1198c-109">Удалось обучить модель один раз с помощью объединенной версии всех наборов данных hello по всем местоположениям.</span><span class="sxs-lookup"><span data-stu-id="1198c-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="1198c-110">Но поскольку каждого из своих расположений уникальной средой, лучшим вариантом будет иметь tootrain модели регрессии отдельно с помощью hello набора данных для каждого расположения.</span><span class="sxs-lookup"><span data-stu-id="1198c-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="1198c-111">Таким образом, каждый обученной модели может занять в размеры другое хранилище hello учетной записи, тома, geography, заполнение, среды трафика понятного имени bike *т. д.*.</span><span class="sxs-lookup"><span data-stu-id="1198c-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="1198c-112">Которые могут быть hello лучшим подходом, но вы не хотите toocreate 1000 обучения экспериментов в машинном обучении Azure с каждый из которых представляет отдельную папку.</span><span class="sxs-lookup"><span data-stu-id="1198c-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="1198c-113">Помимо возможности использования задачу затруднительным, кроме того, он кажется довольно неэффективным, поскольку каждый эксперимента будет иметь все hello же компоненты, за исключением hello обучающий набор данных.</span><span class="sxs-lookup"><span data-stu-id="1198c-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="1198c-114">К счастью, этого можно достичь, используя hello [переподготовки API машинного обучения Azure](machine-learning-retrain-models-programmatically.md) и автоматизация задачу hello с [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="1198c-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1198c-115">toomake выборка выполняться быстрее, мы будем Сократите число hello расположений из 1000 too10.</span><span class="sxs-lookup"><span data-stu-id="1198c-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="1198c-116">Но hello применяются те же принципы и процедуры too1 000 расположения.</span><span class="sxs-lookup"><span data-stu-id="1198c-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="1198c-117">Hello отличается только, если требуется tootrain из 1000 наборов данных возможно, необходимо toothink выполнения hello следующие скрипты PowerShell в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="1198c-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="1198c-118">Как toodo, который выходит за пределы области hello в этой статье, но можно найти примеры PowerShell многопоточность на hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="1198c-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="1198c-119">Настройка эксперимента обучения hello</span><span class="sxs-lookup"><span data-stu-id="1198c-119">Set up hello training experiment</span></span>
<span data-ttu-id="1198c-120">Мы будем toouse пример [эксперимента обучения](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) , мы уже создали в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1198c-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="1198c-121">Откройте этот эксперимент в рабочей области [Студии машинного обучения Azure](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="1198c-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="1198c-122">В toofollow порядке, а также в этом примере может понадобиться toouse стандартной рабочей области, а не бесплатную рабочую область.</span><span class="sxs-lookup"><span data-stu-id="1198c-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="1198c-123">Будут созданы одну конечную точку для каждого клиента - всего 10 конечные точки — и, потребует стандартной рабочей области, поскольку бесплатную рабочую область ограниченного too3 конечных точек.</span><span class="sxs-lookup"><span data-stu-id="1198c-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="1198c-124">Если бесплатную рабочую область, просто измените скрипты hello ниже tooallow для всего 3 расположений.</span><span class="sxs-lookup"><span data-stu-id="1198c-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="1198c-125">использует эксперимента Hello **импорта данных** модуль tooimport hello обучающий набор данных *customer001.csv* из учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1198c-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="1198c-126">Предположим, что мы сбора обучающих наборах данных из всех расположений прокат велосипедов и их хранятся в hello же больших двоичных объектов место хранения с именами файлов, от *rentalloc001.csv* слишком*rentalloc10.csv* .</span><span class="sxs-lookup"><span data-stu-id="1198c-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="1198c-128">Обратите внимание, что **вывод веб-службы** модуль будет добавлен toohello **Обучение модели** модуля.</span><span class="sxs-lookup"><span data-stu-id="1198c-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="1198c-129">При этом эксперименте развертывается как веб-службы, hello конечная точка, связанная с выходного файла будет возвращать обученной модели hello в формат файла .ilearner hello.</span><span class="sxs-lookup"><span data-stu-id="1198c-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="1198c-130">Также Обратите внимание, что мы устанавливаем параметр веб-службы для URL-адреса hello, hello **импорта данных** использует модуль.</span><span class="sxs-lookup"><span data-stu-id="1198c-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="1198c-131">Это позволяет нам toouse hello toospecify отдельных обучающих наборов данных tootrain hello модели параметров для каждого расположения.</span><span class="sxs-lookup"><span data-stu-id="1198c-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="1198c-132">Существуют другие способы, это можно было сделать это, например с помощью SQL-запроса с веб-службы параметр tooget данными из базы данных SQL Azure, или просто **входных данных для службы Web** toopass модуля в toohello набора данных, веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1198c-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="1198c-134">Теперь запустим этого эксперимента обучения, используется значение по умолчанию hello *rental001.csv* как hello обучающий набор данных.</span><span class="sxs-lookup"><span data-stu-id="1198c-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="1198c-135">Если просмотреть выходные данные hello hello **Evaluate** модуля (щелкните выходной hello и выберите **визуализировать**), вы видите, мы получаем довольно производительность *AUC* = 0.91.</span><span class="sxs-lookup"><span data-stu-id="1198c-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="1198c-136">На этом этапе мы готовы toodeploy веб-службы за пределы этого эксперимента обучения.</span><span class="sxs-lookup"><span data-stu-id="1198c-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="1198c-137">Развертывание hello обучения и оценки веб-службы</span><span class="sxs-lookup"><span data-stu-id="1198c-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="1198c-138">toodeploy hello обучения веб-службы, нажмите кнопку hello **настройки веб-службы** ниже холст эксперимента hello и выберите **развертывание веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="1198c-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="1198c-139">Назовите эту веб-службу Bike Rental Training (Обучение аренды велосипедов).</span><span class="sxs-lookup"><span data-stu-id="1198c-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="1198c-140">Теперь нам требуется toodeploy hello оценки веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1198c-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="1198c-141">toodo это, можно нажать кнопку **настройки веб-службы** ниже hello холсте и выберите **прогнозной веб-службы**.</span><span class="sxs-lookup"><span data-stu-id="1198c-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="1198c-142">При этом создается оценивающий эксперимент.</span><span class="sxs-lookup"><span data-stu-id="1198c-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="1198c-143">Нам нужно toomake несколько toomake небольшие изменения работы веб-службы, например удаление столбца меток hello «cnt» из hello входные данные и ограничений идентификатора экземпляра hello tooonly вывода hello и соответствующий hello прогнозируемое значение.</span><span class="sxs-lookup"><span data-stu-id="1198c-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="1198c-144">toosave самостоятельно, что работает, можно просто открыть hello [прогнозной эксперимента](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) в коллекции, которые уже были подготовлены hello.</span><span class="sxs-lookup"><span data-stu-id="1198c-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="1198c-145">toodeploy hello веб-службы, запустите hello прогнозной эксперимента, а затем нажмите кнопку hello **развертывание веб-службы** кнопки ниже hello холста.</span><span class="sxs-lookup"><span data-stu-id="1198c-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="1198c-146">Hello имя оценки «Оценки прокат велосипедов» веб-служба».</span><span class="sxs-lookup"><span data-stu-id="1198c-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="1198c-147">Создание 10 идентичных конечных точек веб-службы с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1198c-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="1198c-148">Эта веб-служба предоставляется с конечной точкой по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1198c-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="1198c-149">Но мы не интересует, как конечную точку по умолчанию hello с момента его нельзя обновить.</span><span class="sxs-lookup"><span data-stu-id="1198c-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="1198c-150">Мы должны toodo — toocreate 10 дополнительных конечных точек, одно для каждого расположения.</span><span class="sxs-lookup"><span data-stu-id="1198c-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="1198c-151">Для этого мы воспользуемся PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1198c-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="1198c-152">Сначала настроим среду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1198c-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="1198c-153">Затем выполните следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="1198c-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="1198c-154">Теперь мы создали 10 конечные точки и все они содержат hello же обученной модели, обучение которых производилось на *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="1198c-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="1198c-155">Их можно просмотреть в hello портала управления Azure.</span><span class="sxs-lookup"><span data-stu-id="1198c-155">You can view them in hello Azure Management Portal.</span></span>

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="1198c-157">Обновить hello конечные точки toouse отдельные обучающих наборах данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="1198c-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="1198c-158">Hello следующий шаг — конечные точки hello tooupdate с моделями, уникальным образом обучена на отдельных данных каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="1198c-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="1198c-159">Но сначала необходимо tooproduce эти модели из hello **обучения прокат велосипедов** веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1198c-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="1198c-160">Давайте рассмотрим назад toohello **обучения прокат велосипедов** веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1198c-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="1198c-161">Мы должны toocall BES конечной точки с 10 разных обучающих наборах данных в разных моделях порядок tooproduce 10 10 раз.</span><span class="sxs-lookup"><span data-stu-id="1198c-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="1198c-162">Мы будем использовать hello **InovkeAmlWebServiceBESEndpoint** toodo командлет PowerShell это.</span><span class="sxs-lookup"><span data-stu-id="1198c-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="1198c-163">Необходимо также tooprovide учетные данные для учетной записи хранилища больших двоичных объектов в `$configContent`, а именно, в поля hello `AccountName`, `AccountKey` и `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="1198c-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="1198c-164">Hello `AccountName` может быть одно из имен учетной записи, как показано в hello **классический портал управления Azure** (*хранения* вкладке).</span><span class="sxs-lookup"><span data-stu-id="1198c-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="1198c-165">После нажатия кнопки на учетную запись хранилища, его `AccountKey` можно получить, нажав клавишу hello **управление ключами доступа** кнопку в нижней hello и копирование hello *первичный ключ доступа*.</span><span class="sxs-lookup"><span data-stu-id="1198c-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="1198c-166">Hello `RelativeLocation` — hello путь относительный tooyour хранилища для хранения новой модели.</span><span class="sxs-lookup"><span data-stu-id="1198c-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="1198c-167">Например, путь hello `hai/retrain/bike_rental/` в скрипте hello ниже точки tooa контейнер с именем `hai`, и `/retrain/bike_rental/` являются вложенными папками.</span><span class="sxs-lookup"><span data-stu-id="1198c-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="1198c-168">В настоящее время не удается создать подпапки через портал hello пользовательского интерфейса, но существуют [несколько обозреватели хранилища Azure](../storage/common/storage-explorers.md) , которые позволяют toodo таким образом.</span><span class="sxs-lookup"><span data-stu-id="1198c-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="1198c-169">Рекомендуется создать новый контейнер в вашей hello toostore хранилища новый обученных моделей (файлы .ilearner) следующим образом: страница «хранение», выберите на hello **добавить** кнопку внизу hello и назовите его `retrain`.</span><span class="sxs-lookup"><span data-stu-id="1198c-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="1198c-170">Таким образом, следующий сценарий toohello необходимые изменения hello относятся слишком`AccountName`, `AccountKey` и `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="1198c-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
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
> <span data-ttu-id="1198c-171">Hello BES конечной точки — hello поддерживается только режим для этой операции.</span><span class="sxs-lookup"><span data-stu-id="1198c-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="1198c-172">RRS использовать для создания обученных моделей нельзя.</span><span class="sxs-lookup"><span data-stu-id="1198c-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="1198c-173">Как показано выше, вместо создания 10 разных BES задания json файлы конфигурации, мы динамически вместо этого создать строка hello настройки и передать его toohello *jobConfigString* параметр hello  **InvokeAmlWebServceBESEndpoint** командлета, так как на диске нет копии действительно tookeep нет необходимости.</span><span class="sxs-lookup"><span data-stu-id="1198c-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="1198c-174">Если все пойдет хорошо, через некоторое время вы увидите 10 файлов .ilearner из *model001.ilearner* слишком*model010.ilearner*, в вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1198c-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="1198c-175">Теперь мы готовы tooupdate конечных точек с этими моделями с помощью hello службы нашей 10 оценки web **AmlWebServiceEndpoint исправление** командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1198c-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="1198c-176">Еще раз, следует помните, что мы только исправление конечные точки не по умолчанию hello программно созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="1198c-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="1198c-177">Процесс должен выполняться довольно быстро.</span><span class="sxs-lookup"><span data-stu-id="1198c-177">This should run fairly quickly.</span></span> <span data-ttu-id="1198c-178">После завершения выполнения hello, мы будем успешно создана 10 конечных точек службы прогнозной web, каждый из которых содержит обученной модели однозначно обучена на hello набора данных определенного tooa расположение аренды, все из эксперимента обучения одного.</span><span class="sxs-lookup"><span data-stu-id="1198c-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="1198c-179">tooverify это, попробуйте выполнить вызов этих конечных точек с помощью hello **InvokeAmlWebServiceRRSEndpoint** командлета, обеспечивая им hello же входные данные и следует ожидать, что результаты различных прогноза toosee с момента hello модели, обучение с помощью разных обучающих наборов.</span><span class="sxs-lookup"><span data-stu-id="1198c-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="1198c-180">Полный сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="1198c-180">Full PowerShell script</span></span>
<span data-ttu-id="1198c-181">Ниже приведен список hello hello полный исходный код:</span><span class="sxs-lookup"><span data-stu-id="1198c-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
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

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
