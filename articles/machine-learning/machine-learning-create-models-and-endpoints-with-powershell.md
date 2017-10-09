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
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>Создание множества моделей машинного обучения и конечных точек веб-службы из одного эксперимента с помощью PowerShell
Вот распространенные задачи машинного обучения: требуется несколько моделей, имеющих hello toocreate же рабочий процесс обучения и использования hello того же алгоритма, но имеют разные обучающих наборов данных в качестве входных данных. В этой статье показано, как toodo это в масштабе в студии машинного обучения Azure с помощью только одного эксперимента.

Предположим, что вы являетесь владельцем международного бизнеса по предоставлению франшиз на аренду велосипедов. Вы хотите toobuild требование аренды hello toopredict модели регрессии на основе исторических данных. Имеется 1000 расположения аренды через Здравствуй, мир! и собрали набора данных для каждого расположение, которое включает в себя важные компоненты, например даты, времени, погоды и трафика, которые tooeach определенного расположения.

Удалось обучить модель один раз с помощью объединенной версии всех наборов данных hello по всем местоположениям. Но поскольку каждого из своих расположений уникальной средой, лучшим вариантом будет иметь tootrain модели регрессии отдельно с помощью hello набора данных для каждого расположения. Таким образом, каждый обученной модели может занять в размеры другое хранилище hello учетной записи, тома, geography, заполнение, среды трафика понятного имени bike *т. д.*.

Которые могут быть hello лучшим подходом, но вы не хотите toocreate 1000 обучения экспериментов в машинном обучении Azure с каждый из которых представляет отдельную папку. Помимо возможности использования задачу затруднительным, кроме того, он кажется довольно неэффективным, поскольку каждый эксперимента будет иметь все hello же компоненты, за исключением hello обучающий набор данных.

К счастью, этого можно достичь, используя hello [переподготовки API машинного обучения Azure](machine-learning-retrain-models-programmatically.md) и автоматизация задачу hello с [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).

> [!NOTE]
> toomake выборка выполняться быстрее, мы будем Сократите число hello расположений из 1000 too10. Но hello применяются те же принципы и процедуры too1 000 расположения. Hello отличается только, если требуется tootrain из 1000 наборов данных возможно, необходимо toothink выполнения hello следующие скрипты PowerShell в параллельном режиме. Как toodo, который выходит за пределы области hello в этой статье, но можно найти примеры PowerShell многопоточность на hello Интернета.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Настройка эксперимента обучения hello
Мы будем toouse пример [эксперимента обучения](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) , мы уже создали в hello [коллекции аналитики Cortana](http://gallery.cortanaintelligence.com). Откройте этот эксперимент в рабочей области [Студии машинного обучения Azure](https://studio.azureml.net) .

> [!NOTE]
> В toofollow порядке, а также в этом примере может понадобиться toouse стандартной рабочей области, а не бесплатную рабочую область. Будут созданы одну конечную точку для каждого клиента - всего 10 конечные точки — и, потребует стандартной рабочей области, поскольку бесплатную рабочую область ограниченного too3 конечных точек. Если бесплатную рабочую область, просто измените скрипты hello ниже tooallow для всего 3 расположений.
> 
> 

использует эксперимента Hello **импорта данных** модуль tooimport hello обучающий набор данных *customer001.csv* из учетной записи хранилища Azure. Предположим, что мы сбора обучающих наборах данных из всех расположений прокат велосипедов и их хранятся в hello же больших двоичных объектов место хранения с именами файлов, от *rentalloc001.csv* слишком*rentalloc10.csv* .

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Обратите внимание, что **вывод веб-службы** модуль будет добавлен toohello **Обучение модели** модуля.
При этом эксперименте развертывается как веб-службы, hello конечная точка, связанная с выходного файла будет возвращать обученной модели hello в формат файла .ilearner hello.

Также Обратите внимание, что мы устанавливаем параметр веб-службы для URL-адреса hello, hello **импорта данных** использует модуль. Это позволяет нам toouse hello toospecify отдельных обучающих наборов данных tootrain hello модели параметров для каждого расположения.
Существуют другие способы, это можно было сделать это, например с помощью SQL-запроса с веб-службы параметр tooget данными из базы данных SQL Azure, или просто **входных данных для службы Web** toopass модуля в toohello набора данных, веб-службы.

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

Теперь запустим этого эксперимента обучения, используется значение по умолчанию hello *rental001.csv* как hello обучающий набор данных. Если просмотреть выходные данные hello hello **Evaluate** модуля (щелкните выходной hello и выберите **визуализировать**), вы видите, мы получаем довольно производительность *AUC* = 0.91. На этом этапе мы готовы toodeploy веб-службы за пределы этого эксперимента обучения.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Развертывание hello обучения и оценки веб-службы
toodeploy hello обучения веб-службы, нажмите кнопку hello **настройки веб-службы** ниже холст эксперимента hello и выберите **развертывание веб-службы**. Назовите эту веб-службу Bike Rental Training (Обучение аренды велосипедов).

Теперь нам требуется toodeploy hello оценки веб-службы.
toodo это, можно нажать кнопку **настройки веб-службы** ниже hello холсте и выберите **прогнозной веб-службы**. При этом создается оценивающий эксперимент.
Нам нужно toomake несколько toomake небольшие изменения работы веб-службы, например удаление столбца меток hello «cnt» из hello входные данные и ограничений идентификатора экземпляра hello tooonly вывода hello и соответствующий hello прогнозируемое значение.

toosave самостоятельно, что работает, можно просто открыть hello [прогнозной эксперимента](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) в коллекции, которые уже были подготовлены hello.

toodeploy hello веб-службы, запустите hello прогнозной эксперимента, а затем нажмите кнопку hello **развертывание веб-службы** кнопки ниже hello холста. Hello имя оценки «Оценки прокат велосипедов» веб-служба».

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>Создание 10 идентичных конечных точек веб-службы с помощью PowerShell
Эта веб-служба предоставляется с конечной точкой по умолчанию. Но мы не интересует, как конечную точку по умолчанию hello с момента его нельзя обновить. Мы должны toodo — toocreate 10 дополнительных конечных точек, одно для каждого расположения. Для этого мы воспользуемся PowerShell.

Сначала настроим среду PowerShell:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

Затем выполните следующую команду PowerShell hello:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Теперь мы создали 10 конечные точки и все они содержат hello же обученной модели, обучение которых производилось на *customer001.csv*. Их можно просмотреть в hello портала управления Azure.

![изображение](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>Обновить hello конечные точки toouse отдельные обучающих наборах данных с помощью PowerShell
Hello следующий шаг — конечные точки hello tooupdate с моделями, уникальным образом обучена на отдельных данных каждого клиента. Но сначала необходимо tooproduce эти модели из hello **обучения прокат велосипедов** веб-службы. Давайте рассмотрим назад toohello **обучения прокат велосипедов** веб-службы. Мы должны toocall BES конечной точки с 10 разных обучающих наборах данных в разных моделях порядок tooproduce 10 10 раз. Мы будем использовать hello **InovkeAmlWebServiceBESEndpoint** toodo командлет PowerShell это.

Необходимо также tooprovide учетные данные для учетной записи хранилища больших двоичных объектов в `$configContent`, а именно, в поля hello `AccountName`, `AccountKey` и `RelativeLocation`. Hello `AccountName` может быть одно из имен учетной записи, как показано в hello **классический портал управления Azure** (*хранения* вкладке). После нажатия кнопки на учетную запись хранилища, его `AccountKey` можно получить, нажав клавишу hello **управление ключами доступа** кнопку в нижней hello и копирование hello *первичный ключ доступа*. Hello `RelativeLocation` — hello путь относительный tooyour хранилища для хранения новой модели. Например, путь hello `hai/retrain/bike_rental/` в скрипте hello ниже точки tooa контейнер с именем `hai`, и `/retrain/bike_rental/` являются вложенными папками. В настоящее время не удается создать подпапки через портал hello пользовательского интерфейса, но существуют [несколько обозреватели хранилища Azure](../storage/common/storage-explorers.md) , которые позволяют toodo таким образом. Рекомендуется создать новый контейнер в вашей hello toostore хранилища новый обученных моделей (файлы .ilearner) следующим образом: страница «хранение», выберите на hello **добавить** кнопку внизу hello и назовите его `retrain`. Таким образом, следующий сценарий toohello необходимые изменения hello относятся слишком`AccountName`, `AccountKey` и `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).

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
> Hello BES конечной точки — hello поддерживается только режим для этой операции. RRS использовать для создания обученных моделей нельзя.
> 
> 

Как показано выше, вместо создания 10 разных BES задания json файлы конфигурации, мы динамически вместо этого создать строка hello настройки и передать его toohello *jobConfigString* параметр hello  **InvokeAmlWebServceBESEndpoint** командлета, так как на диске нет копии действительно tookeep нет необходимости.

Если все пойдет хорошо, через некоторое время вы увидите 10 файлов .ilearner из *model001.ilearner* слишком*model010.ilearner*, в вашей учетной записи хранилища Azure. Теперь мы готовы tooupdate конечных точек с этими моделями с помощью hello службы нашей 10 оценки web **AmlWebServiceEndpoint исправление** командлета PowerShell. Еще раз, следует помните, что мы только исправление конечные точки не по умолчанию hello программно созданную ранее.

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

Процесс должен выполняться довольно быстро. После завершения выполнения hello, мы будем успешно создана 10 конечных точек службы прогнозной web, каждый из которых содержит обученной модели однозначно обучена на hello набора данных определенного tooa расположение аренды, все из эксперимента обучения одного. tooverify это, попробуйте выполнить вызов этих конечных точек с помощью hello **InvokeAmlWebServiceRRSEndpoint** командлета, обеспечивая им hello же входные данные и следует ожидать, что результаты различных прогноза toosee с момента hello модели, обучение с помощью разных обучающих наборов.

## <a name="full-powershell-script"></a>Полный сценарий PowerShell
Ниже приведен список hello hello полный исходный код:

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
