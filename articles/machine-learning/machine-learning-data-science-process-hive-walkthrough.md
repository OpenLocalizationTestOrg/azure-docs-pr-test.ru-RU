---
title: "aaaExplore данные в Hadoop кластера и создания моделей в машинном обучении Azure | Документы Microsoft"
description: "С помощью hello процесс обработки и анализа данных для команды сценария конца в конец данных, построенных на HDInsight Hadoop кластера toobuild и развертывания модели с помощью общедоступных набора данных."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="5fc02-103">Hello командного процесса обработки и анализа данных в действии: использование Azure HDInsight Hadoop кластеров</span><span class="sxs-lookup"><span data-stu-id="5fc02-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="5fc02-104">В этом пошаговом руководстве мы используем hello [процесса обработки и анализа данных Team (TDSP)](data-science-process-overview.md) -сквозной сценарий, используя [кластера Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, исследовать и публично компонентов инженер данные из hello Доступные [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных и toodown образец hello данных.</span><span class="sxs-lookup"><span data-stu-id="5fc02-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="5fc02-105">Модели данных hello создаются с помощью машинного обучения Azure toohandle двоичными и мультиклассовой классификации и регрессии задач прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="5fc02-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="5fc02-106">Пошаговое руководство показывает, как toohandle большего набора данных (1 ТБ), аналогичный сценарий с помощью HDInsight Hadoop кластеры для обработки данных см. в разделе [процесс обработки и анализа данных для команды - с помощью Azure HDInsight Hadoop кластеров на набор данных 1 ТБ](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5fc02-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="5fc02-107">Это также возможно toouse hello tooaccomplish ноутбук IPython задач представленному hello Пошаговое руководство по использованию набора данных hello 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="5fc02-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="5fc02-108">Пользователей, которые бы как tootry, такой подход следует обратиться к hello [Criteo Пошаговое руководство по использованию соединений Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) раздела.</span><span class="sxs-lookup"><span data-stu-id="5fc02-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="5fc02-109"><a name="dataset"></a>Описание набора данных «Поездки такси Нью-Йорка»</span><span class="sxs-lookup"><span data-stu-id="5fc02-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="5fc02-110">Hello Trip такси NYC данных составляет около 20 ГБ файлы сжатых значений с разделителями запятыми (CSV) (~ 48 ГБ несжатого), включающего в себя более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута.</span><span class="sxs-lookup"><span data-stu-id="5fc02-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="5fc02-111">Каждая запись маршрута включает hello раскладки и истощение место и время, анонимные hack (драйвер) номер лицензии и medallion (уникальный идентификатор элемента такси) номер.</span><span class="sxs-lookup"><span data-stu-id="5fc02-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="5fc02-112">данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="5fc02-113">Hello «trip_data» CSV-файлы содержат обработки таких сведений, как количество пассажиров, раскладки и dropoff точек, длительность обработки и длина пути.</span><span class="sxs-lookup"><span data-stu-id="5fc02-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="5fc02-114">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="5fc02-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="5fc02-115">CSV-файлы «trip_fare» Hello содержат подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты.</span><span class="sxs-lookup"><span data-stu-id="5fc02-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="5fc02-116">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="5fc02-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="5fc02-117">Hello trip уникальных ключей toojoin\_данных и обработки\_тариф авиакомпании состоит из полей hello: medallion hack\_лицензии и раскладки\_даты и времени.</span><span class="sxs-lookup"><span data-stu-id="5fc02-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="5fc02-118">tooget все hello сведения о соответствующих tooa конкретного маршрута, он является достаточно toojoin с тремя ключами: «medallion» hello «hack\_лицензии» и «раскладки\_datetime».</span><span class="sxs-lookup"><span data-stu-id="5fc02-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="5fc02-119">Когда мы хранить их в таблицы Hive вскоре описаны некоторые дополнительные сведения о данных hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="5fc02-120"><a name="mltasks"></a>Примеры задач прогнозирования</span><span class="sxs-lookup"><span data-stu-id="5fc02-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="5fc02-121">При приближении к данным, определение типа hello прогнозов необходимо toomake на основе его анализа помогает прояснить hello задачи, которые понадобятся tooinclude в процессе.</span><span class="sxs-lookup"><span data-stu-id="5fc02-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="5fc02-122">Ниже приведены три примера прогноза проблемы, которые мы адрес в этом пошаговом руководстве, формирование основан на hello *совет\_сумма*:</span><span class="sxs-lookup"><span data-stu-id="5fc02-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="5fc02-123">**Двоичная классификация**: спрогнозировать, были ли оставлены чаевые после поездку, т. е. значение *tip\_amount* больше 0 $ является позитивным примером, а значение *tip\_amount* 0 $ является негативным примером.</span><span class="sxs-lookup"><span data-stu-id="5fc02-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="5fc02-124">**Мультиклассовая классификация**: диапазон hello toopredict совет суммы оплаты hello trip.</span><span class="sxs-lookup"><span data-stu-id="5fc02-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="5fc02-125">Разделен hello *совет\_сумма* в пять ячеек или классы:</span><span class="sxs-lookup"><span data-stu-id="5fc02-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="5fc02-126">**Задача регрессии**: оплачена сумма hello toopredict hello подсказки для маршрута.</span><span class="sxs-lookup"><span data-stu-id="5fc02-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="5fc02-127"><a name="setup"></a>Настройка кластера HDInsight Hadoop для расширенной аналитики</span><span class="sxs-lookup"><span data-stu-id="5fc02-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-128">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-129">Настроить среду Azure для использования расширенной аналитики, в которой задействуется кластер HDInsight, вы можете в три этапа.</span><span class="sxs-lookup"><span data-stu-id="5fc02-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="5fc02-130">[Создание учетной записи хранения](../storage/common/storage-create-storage-account.md). Эта учетная запись используется для хранения данных в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc02-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="5fc02-131">Здесь также находится Hello данные, используемые в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5fc02-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="5fc02-132">[Настройка Azure HDInsight Hadoop кластеры для hello Advanced Analytics процесса и технологии](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5fc02-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="5fc02-133">На этом этапе создается кластер Azure HDInsight Hadoop, на всех узлах которого установлена 64-разрядная версия Anaconda Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="5fc02-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="5fc02-134">Существует два важных шага tooremember при настройке кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5fc02-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="5fc02-135">Не забывайте toolink учетной записи хранилища hello созданной на шаге 1 с кластером HDInsight, при его создании.</span><span class="sxs-lookup"><span data-stu-id="5fc02-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="5fc02-136">Эта учетная запись хранения — используется tooaccess данных, обрабатываемых в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="5fc02-137">После создания кластера hello, включите удаленный доступ toohello головного узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="5fc02-138">Перейдите toohello **конфигурации** и нажмите кнопку **включить удаленный**.</span><span class="sxs-lookup"><span data-stu-id="5fc02-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="5fc02-139">Этот шаг определяет hello учетные данные пользователя для удаленного входа.</span><span class="sxs-lookup"><span data-stu-id="5fc02-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="5fc02-140">[Создайте рабочую область машинного обучения Azure](machine-learning-create-workspace.md): рабочей области машинного обучения этот Azure — используется toobuild машинного обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="5fc02-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="5fc02-141">Эта задача решается после завершения просмотра исходных данных и работу выборки с использованием кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="5fc02-142"><a name="getdata"></a>Получение данных hello из открытого источника</span><span class="sxs-lookup"><span data-stu-id="5fc02-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-143">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-144">tooget hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных из открытых расположения можно использовать любую из hello методов, описанных в [tooand перемещение данных из хранилища больших двоичных объектов](machine-learning-data-science-move-azure-blob.md) машина tooyour toocopy hello данных.</span><span class="sxs-lookup"><span data-stu-id="5fc02-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="5fc02-145">Здесь описывается, как использование AzCopy tootransfer hello файлов содержат данные.</span><span class="sxs-lookup"><span data-stu-id="5fc02-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="5fc02-146">toodownload и AzCopy установки следуйте инструкциям hello в [Приступая к работе с hello служебной программы командной строки AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5fc02-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="5fc02-147">Окно командной строки выполните hello следующие команды AzCopy, заменив *< path_to_data_folder >* с целевой hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="5fc02-148">По завершении копирования hello всего 24 ZIP-файлы находятся в выбранной папки данных hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="5fc02-149">Распакуйте файлы toohello загружаются hello один каталог на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="5fc02-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="5fc02-150">Запишите hello папку, где находятся файлы сжимаются hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="5fc02-151">Эта папка будет hello ссылка tooas *< путь\_для\_unzipped_data\_файлы\>*  — ниже.</span><span class="sxs-lookup"><span data-stu-id="5fc02-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="5fc02-152"><a name="upload"></a>Отправка контейнер по умолчанию hello данных toohello кластера Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="5fc02-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-153">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-154">Следующие команды AzCopy, замените hello следующие параметры фактическими значениями hello, указанный при создании кластера Hadoop hello и распаковки файлов данных hello в hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="5fc02-155">***&#60; path_to_data_folder >*** directory hello (а также путь) на этом компьютере, которые содержат файлы данных распаковал hello</span><span class="sxs-lookup"><span data-stu-id="5fc02-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="5fc02-156">***&#60; имя учетной записи хранения кластера Hadoop >*** hello учетной записи хранилища, связанной с кластером HDInsight</span><span class="sxs-lookup"><span data-stu-id="5fc02-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="5fc02-157">***&#60; контейнер по умолчанию для кластера Hadoop >*** контейнера по умолчанию hello, используемого кластера.</span><span class="sxs-lookup"><span data-stu-id="5fc02-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="5fc02-158">Hello имя по умолчанию hello является контейнер обычно hello точно такое же имя в качестве самого кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="5fc02-159">Например если кластер hello называется «abc123.azurehdinsight.net», контейнера по умолчанию hello — abc123.</span><span class="sxs-lookup"><span data-stu-id="5fc02-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="5fc02-160">***&#60; ключ учетной записи хранения >*** hello ключ учетной записи хранения hello, используемый в кластере</span><span class="sxs-lookup"><span data-stu-id="5fc02-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="5fc02-161">Из командной строки или окно Windows PowerShell на компьютере выполните следующие две команды AzCopy hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="5fc02-162">Эта команда отправляет данные маршрута hello слишком***nyctaxitripraw*** каталог в контейнере по умолчанию hello hello кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5fc02-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="5fc02-163">Эта команда отправляет данные тариф авиакомпании hello слишком***nyctaxifareraw*** каталог в контейнере по умолчанию hello hello кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5fc02-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="5fc02-164">Hello данных должны теперь в хранилище больших двоичных объектов Azure и готов toobe потребляет внутри кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="5fc02-165"><a name="#download-hql-files"></a>Войти в hello головного узла кластера Hadoop и и подготовка для исследовательского анализа</span><span class="sxs-lookup"><span data-stu-id="5fc02-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-166">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-167">tooaccess hello головного узла кластера hello для исследовательского анализа и вниз выборки данных hello выполните hello процедуры, описанной в [доступа hello головного узла кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="5fc02-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="5fc02-168">В этом пошаговом руководстве мы в первую очередь использовать запросы, написанные [Hive](https://hive.apache.org/), SQL-подобного языка запросов, tooperform предварительные данные исследования.</span><span class="sxs-lookup"><span data-stu-id="5fc02-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="5fc02-169">запросы Hive Hello хранятся в файлах .hql.</span><span class="sxs-lookup"><span data-stu-id="5fc02-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="5fc02-170">Мы затем вниз образец этого toobe данных, используемых в машинном обучении Azure для построения моделей.</span><span class="sxs-lookup"><span data-stu-id="5fc02-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="5fc02-171">tooprepare hello кластера для исследовательского анализа, мы загружать файлы .hql hello, содержащие соответствующие скрипты Hive hello из [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa локальный каталог (например, C:\temp) на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="5fc02-172">toodo это, откройте hello **командной строки** изнутри hello головного узла hello кластера и проблема hello, следующие две команды:</span><span class="sxs-lookup"><span data-stu-id="5fc02-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="5fc02-173">Эти две команды будут загружать все .hql файлы, необходимые в локальном каталоге этого пошагового руководства toohello ***C:\temp &#92;*** в hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="5fc02-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="5fc02-174"><a name="#hive-db-tables"></a>Создание базы данных Hive и таблиц, секционированных по месяцам</span><span class="sxs-lookup"><span data-stu-id="5fc02-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-175">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-176">Мы — теперь готовы toocreate Hive таблицы для наших NYC такси dataset.</span><span class="sxs-lookup"><span data-stu-id="5fc02-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="5fc02-177">В hello головного узла кластера Hadoop hello, откройте hello ***командной строки Hadoop*** hello desktop hello головного узла, а также введите hello Hive каталог, введя команду hello</span><span class="sxs-lookup"><span data-stu-id="5fc02-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="5fc02-178">**Выполнить все команды Hive в этом пошаговом руководстве из hello выше Hive bin / directory строки. Таким образом вы сможете автоматически избежать любых проблем с путем. Мы используем условия hello «Hive каталога prompt», «Hive bin / directory строки» и «Hadoop Командная строка», попеременно в этом пошаговом руководстве.**</span><span class="sxs-lookup"><span data-stu-id="5fc02-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="5fc02-179">Hello Hive каталога строке введите следующую команду в Hadoop Командная строка hello головного узла toosubmit hello Hive запроса toocreate Hive базы данных и таблиц hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="5fc02-180">Вот содержимое hello hello ***C:\temp\sample\_куст\_создания\_db\_и\_tables.hql*** файл, который создает базу данных Hive ***nyctaxidb *** и таблицы ***trip*** и ***тариф авиакомпании***.</span><span class="sxs-lookup"><span data-stu-id="5fc02-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="5fc02-181">Этот сценарий Hive создает две таблицы:</span><span class="sxs-lookup"><span data-stu-id="5fc02-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="5fc02-182">Таблица «маршрут» Hello содержит trip подробные сведения о каждом расстояния (сведения о драйвере, время отправки, расстояние маршрута и времени)</span><span class="sxs-lookup"><span data-stu-id="5fc02-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="5fc02-183">Таблица «тариф авиакомпании» Hello сведениями тариф авиакомпании (тариф авиакомпании сумма, сумма совет, тарифы и сборы).</span><span class="sxs-lookup"><span data-stu-id="5fc02-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="5fc02-184">Если требуется получить любые дополнительную помощь с помощью этих процедур или tooinvestigate альтернативные методы, см. раздел hello [отправить Hive запросы непосредственно из hello командной строки Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="5fc02-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="5fc02-185"><a name="#load-data"></a>Загрузка данных tooHive таблиц с секций</span><span class="sxs-lookup"><span data-stu-id="5fc02-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-186">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-187">набор данных такси Hello NYC имеет, естественным секционированием по месяцам, который мы используем tooenable запросов и обработки ускоряется.</span><span class="sxs-lookup"><span data-stu-id="5fc02-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="5fc02-188">Здравствуйте ниже команды PowerShell (из каталога hello Hive, с помощью hello **командной строки Hadoop**) Загрузка данных toohello «маршрут» и «тариф авиакомпании» Hive таблиц секционированной по месяцам.</span><span class="sxs-lookup"><span data-stu-id="5fc02-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="5fc02-189">Hello *пример\_куст\_загрузить\_данные\_по\_partitions.hql* файл содержит следующие hello **загрузить** команд.</span><span class="sxs-lookup"><span data-stu-id="5fc02-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="5fc02-190">Обратите внимание, что количество запросов Hive в процессе исследования hello вариант включают выглядит в одной секции или две секции.</span><span class="sxs-lookup"><span data-stu-id="5fc02-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="5fc02-191">Однако эти запросы, может быть запущен через hello все данные.</span><span class="sxs-lookup"><span data-stu-id="5fc02-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="5fc02-192"><a name="#show-db"></a>Показать базы данных в кластере HDInsight Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="5fc02-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="5fc02-193">tooshow hello баз данных, созданных в кластере HDInsight Hadoop в окне командной строки Hadoop hello, запустите следующую команду в командной строке Hadoop hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="5fc02-194"><a name="#show-tables"></a>Показать hello Hive таблицы в базе данных nyctaxidb hello</span><span class="sxs-lookup"><span data-stu-id="5fc02-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="5fc02-195">tooshow hello таблицы в базе данных nyctaxidb hello, запустите следующую команду в командной строке Hadoop hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="5fc02-196">Мы можете подтвердить, что hello таблицы секционированы, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="5fc02-197">Hello тесты на ожидаемые выходные данные приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="5fc02-197">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="5fc02-198">Аналогичным образом можно гарантировать, что этой таблицы тариф авиакомпании hello секционирована, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="5fc02-199">Hello тесты на ожидаемые выходные данные приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="5fc02-199">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <span data-ttu-id="5fc02-200"><a name="#explore-hive"></a>Исследование данных и проектирование признаков в Hive</span><span class="sxs-lookup"><span data-stu-id="5fc02-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-201">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-202">Здравствуйте, просмотр данных и компонентов технических задач, для данных, загруженных в таблицах Hive hello может выполняться с помощью запросов Hive hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="5fc02-203">Вот примеры задач, о которых пойдет речь в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="5fc02-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="5fc02-204">Просмотр hello top 10 записей в обеих таблицах.</span><span class="sxs-lookup"><span data-stu-id="5fc02-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="5fc02-205">Просмотрим распределение данных по нескольким полям в различных временных окнах.</span><span class="sxs-lookup"><span data-stu-id="5fc02-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="5fc02-206">Проверка качества данных полей hello широты и долготы.</span><span class="sxs-lookup"><span data-stu-id="5fc02-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="5fc02-207">Создание двоичного и мультиклассовой классификации меток, основываясь на hello **совет\_сумма**.</span><span class="sxs-lookup"><span data-stu-id="5fc02-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="5fc02-208">Создание функции путем вычисления расстояния hello прямого маршрута.</span><span class="sxs-lookup"><span data-stu-id="5fc02-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="5fc02-209">Просмотр: Просмотр hello top 10 записей в таблице обработки</span><span class="sxs-lookup"><span data-stu-id="5fc02-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-210">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-211">как выглядят данные hello toosee, мы изучаем 10 записей из каждой таблицы.</span><span class="sxs-lookup"><span data-stu-id="5fc02-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="5fc02-212">Выполните следующие два запроса отдельно из строки directory Hive hello hello командной строки Hadoop консоли tooinspect hello записей hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="5fc02-213">tooget hello top 10 записей в таблице hello «маршрут» из hello первого месяца:</span><span class="sxs-lookup"><span data-stu-id="5fc02-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="5fc02-214">tooget hello top 10 записей в таблице hello» успешного» из hello первого месяца:</span><span class="sxs-lookup"><span data-stu-id="5fc02-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="5fc02-215">Часто бывает полезным toosave записей hello tooa файл удобный просмотр.</span><span class="sxs-lookup"><span data-stu-id="5fc02-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="5fc02-216">Небольшое изменение toohello выше запрос выполняет эту процедуру:</span><span class="sxs-lookup"><span data-stu-id="5fc02-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="5fc02-217">Просмотр: Просмотр hello число записей в каждом из 12 разделов hello</span><span class="sxs-lookup"><span data-stu-id="5fc02-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-218">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-219">Интерес представляет hello, как изменяется номер hello приема-передачи данных во время hello календарного года.</span><span class="sxs-lookup"><span data-stu-id="5fc02-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="5fc02-220">Группирование по месяцам позволяет нам toosee как выглядит этот распространения приема-передачи данных.</span><span class="sxs-lookup"><span data-stu-id="5fc02-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="5fc02-221">Это дает нам hello выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5fc02-221">This gives us hello output :</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="5fc02-222">Здесь, hello первый столбец месяц hello и hello второй номер hello приема-передачи данных за данный месяц.</span><span class="sxs-lookup"><span data-stu-id="5fc02-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="5fc02-223">Мы также могут считаться hello общее количество записей в наш набор данных маршрута, выполнив следующую команду в строке directory Hive hello hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="5fc02-224">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="5fc02-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="5fc02-225">Аналогичные toothose команды для набора данных trip hello показаны мы можем выпустить запросов Hive из строки directory hello Hive для hello тариф авиакомпании набора данных toovalidate hello количество записей.</span><span class="sxs-lookup"><span data-stu-id="5fc02-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="5fc02-226">Это дает нам hello выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5fc02-226">This gives us hello output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="5fc02-227">Обратите внимание, что для обоих наборов данных возвращается hello точное одинаковое количество обращений в месяц.</span><span class="sxs-lookup"><span data-stu-id="5fc02-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="5fc02-228">Это обеспечивает проверку первый hello приветствия, данные были правильно загружены.</span><span class="sxs-lookup"><span data-stu-id="5fc02-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="5fc02-229">Подсчет hello общее число записей в наборе данных тариф авиакомпании hello можно сделать с помощью команды hello ниже hello Hive каталога строке:</span><span class="sxs-lookup"><span data-stu-id="5fc02-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="5fc02-230">Мы получаем такой результат.</span><span class="sxs-lookup"><span data-stu-id="5fc02-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="5fc02-231">Общее число записей в обеих таблицах Hello также является hello же.</span><span class="sxs-lookup"><span data-stu-id="5fc02-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="5fc02-232">Вторая проверка обеспечивает приветствия, данные были правильно загружены.</span><span class="sxs-lookup"><span data-stu-id="5fc02-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="5fc02-233">Просмотр: Распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="5fc02-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-234">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-235">В этом примере определяет medallion hello (номера такси) с более чем 100 приема-передачи данных в течение заданного периода времени.</span><span class="sxs-lookup"><span data-stu-id="5fc02-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="5fc02-236">преимущества hello запроса Hello секционированы доступа к таблице с момента обусловлено hello секции переменной **месяц**.</span><span class="sxs-lookup"><span data-stu-id="5fc02-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="5fc02-237">Hello результатов запроса на языке queryoutput.tsv локальный файл tooa `C:\temp` на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="5fc02-238">Вот содержимое hello *пример\_куст\_trip\_число\_по\_medallion.hql* файла для проверки.</span><span class="sxs-lookup"><span data-stu-id="5fc02-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="5fc02-239">medallion Hello в наборе данных такси NYC hello определяет уникальный CAB-файлов.</span><span class="sxs-lookup"><span data-stu-id="5fc02-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="5fc02-240">Мы можем определить, какие автомобили востребованы, запросив, какие из них выполнили более определенного количества поездок за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="5fc02-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="5fc02-241">Hello следующий пример определяет CAB-файлов, которые сделаны приема-передачи более чем на ста hello первые три месяца и сохраняет hello запроса результаты tooa локального файла, C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="5fc02-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="5fc02-242">Вот содержимое hello *пример\_куст\_trip\_число\_по\_medallion.hql* файла для проверки.</span><span class="sxs-lookup"><span data-stu-id="5fc02-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="5fc02-243">Из hello куста подсказки директории, проблема hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5fc02-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="5fc02-244">Просмотр: распределение поездок по параметрам medallion и hack_license</span><span class="sxs-lookup"><span data-stu-id="5fc02-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-245">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-246">Изучение набора данных, мы в большинстве случаев используется tooexamine hello число вхождений co групп значений.</span><span class="sxs-lookup"><span data-stu-id="5fc02-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="5fc02-247">В этом разделе приведены примеры как toodo для CAB-файлы и драйверы.</span><span class="sxs-lookup"><span data-stu-id="5fc02-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="5fc02-248">Hello *пример\_куст\_trip\_число\_по\_medallion\_license.hql* группы файлов данных тариф авиакомпании hello задания «medallion» и «hack_license» и возвращает количество всех возможных сочетаний.</span><span class="sxs-lookup"><span data-stu-id="5fc02-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="5fc02-249">Ниже приведено его содержимое.</span><span class="sxs-lookup"><span data-stu-id="5fc02-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="5fc02-250">Этот запрос возвращает комбинации автомобиля и конкретного водителя, упорядоченных по убыванию количества поездок.</span><span class="sxs-lookup"><span data-stu-id="5fc02-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="5fc02-251">Из hello Hive каталога строки, запустите:</span><span class="sxs-lookup"><span data-stu-id="5fc02-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="5fc02-252">локальный файл tooa C:\temp\queryoutput.tsv записываются результаты запроса Hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="5fc02-253">Исследование: оценка качества данных через проверку наличия недопустимых записей долготы и широты</span><span class="sxs-lookup"><span data-stu-id="5fc02-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-254">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-255">Общие цель разведочном анализе данных — tooweed неверный записей.</span><span class="sxs-lookup"><span data-stu-id="5fc02-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="5fc02-256">Hello пример в этом разделе определяет ли hello поля широты и долготы содержать либо значение далеко за пределами области NYC hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="5fc02-257">Так как это, вероятно, такие записи значения ошибочные долготы широты, мы хотим tooeliminate их из всех данных toobe используется для моделирования.</span><span class="sxs-lookup"><span data-stu-id="5fc02-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="5fc02-258">Вот содержимое hello *пример\_куст\_качество\_assessment.hql* файла для проверки.</span><span class="sxs-lookup"><span data-stu-id="5fc02-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="5fc02-259">Из hello Hive каталога строки, запустите:</span><span class="sxs-lookup"><span data-stu-id="5fc02-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="5fc02-260">Hello *-S* аргумент, включенных в этой команде подавляет распечатку экрана hello состояние задания Hive Map/Reduce hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="5fc02-261">Это полезно, поскольку это делает печать экрана приветствия hello Hive выходных данных запроса более удобном для чтения.</span><span class="sxs-lookup"><span data-stu-id="5fc02-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="5fc02-262">Исследования: двоичные классовые распределения чаевых за поездки</span><span class="sxs-lookup"><span data-stu-id="5fc02-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-263">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-264">Для проблемы бинарной классификации hello появлялся hello [примеры задач прогнозирования](machine-learning-data-science-process-hive-walkthrough.md#mltasks) разделе ли совет было задано или не является полезным tooknow.</span><span class="sxs-lookup"><span data-stu-id="5fc02-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="5fc02-265">Распределение чаевых является двоичным:</span><span class="sxs-lookup"><span data-stu-id="5fc02-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="5fc02-266">чаевые оставлены (класс 1, tip\_amount > $0);</span><span class="sxs-lookup"><span data-stu-id="5fc02-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="5fc02-267">чаевые не оставлены (класс 0, tip\_amount = $0).</span><span class="sxs-lookup"><span data-stu-id="5fc02-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="5fc02-268">Hello *пример\_куст\_чаевых оставил зависимости\_frequencies.hql* приведенный ниже файла делает это.</span><span class="sxs-lookup"><span data-stu-id="5fc02-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="5fc02-269">Из hello Hive каталога строки, запустите:</span><span class="sxs-lookup"><span data-stu-id="5fc02-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="5fc02-270">Просмотр: Класс распределения в мультиклассовой приветствия</span><span class="sxs-lookup"><span data-stu-id="5fc02-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-271">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-272">Для hello мультиклассовой классификации проблемы, описанные в hello [примеры задач прогнозирования](machine-learning-data-science-process-hive-walkthrough.md#mltasks) этот набор данных также решается tooa естественное классификации, где мы предлагаем toopredict hello объем hello советы по заданному раздела.</span><span class="sxs-lookup"><span data-stu-id="5fc02-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="5fc02-273">Совет диапазоны ячеек toodefine можно использовать в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="5fc02-274">tooget Здравствуйте класса распределения для hello различные диапазоны совет, мы используем hello *пример\_куст\_совет\_диапазон\_frequencies.hql* файла.</span><span class="sxs-lookup"><span data-stu-id="5fc02-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="5fc02-275">Ниже приведено его содержимое.</span><span class="sxs-lookup"><span data-stu-id="5fc02-275">Below are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="5fc02-276">Выполните следующую команду из командной строки Hadoop консоли hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="5fc02-277">Исследование: вычисление расстояния по прямой между двумя местоположениями, заданными долготой и широтой</span><span class="sxs-lookup"><span data-stu-id="5fc02-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-278">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-279">Наличие меру расстояния прямой hello позволяет нам toofind out hello несоответствие между ним и hello фактическое быть расстояние.</span><span class="sxs-lookup"><span data-stu-id="5fc02-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="5fc02-280">Эта функция мы мотивации, указав, что пассажира может быть меньше tootip скорее всего, если они понять, что драйвер hello намеренно было их с гораздо более длинный путь.</span><span class="sxs-lookup"><span data-stu-id="5fc02-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="5fc02-281">Сравнение hello toosee trip фактическое расстояние и hello [гаверсинуса](http://en.wikipedia.org/wiki/Haversine_formula) между двумя точками широты долготы (расстояние hello «circle отлично»), мы используем hello тригонометрические функции, доступные в пределах Hive, таким образом:</span><span class="sxs-lookup"><span data-stu-id="5fc02-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="5fc02-282">В приведенном выше запросе hello R hello радиус hello Земли в милях, который pi преобразованный tooradians.</span><span class="sxs-lookup"><span data-stu-id="5fc02-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="5fc02-283">Обратите внимание, что hello долготы широту точки «фильтрация» tooremove значения, которые могут значительно отличаться от области NYC hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="5fc02-284">В этом случае мы записи наши результаты tooa каталог с именем «queryoutputdir».</span><span class="sxs-lookup"><span data-stu-id="5fc02-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="5fc02-285">Hello последовательность команд, приведенных ниже сначала создает этот каталог выходных данных, а затем запускается команда Hive hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="5fc02-286">Из hello Hive каталога строки, запустите:</span><span class="sxs-lookup"><span data-stu-id="5fc02-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="5fc02-287">Hello результаты запроса записываются больших двоичных объектов too9 Azure ***queryoutputdir/000000\_0*** слишком ***queryoutputdir/000008\_0*** в контейнере по умолчанию hello hello кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5fc02-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="5fc02-288">размер hello toosee hello отдельных больших двоичных объектов, мы выполните следующую команду из каталога строки hello Hive hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="5fc02-289">toosee hello содержимое заданного файла, например 000000\_0, мы используем Hadoop `copyToLocal` команды, таким образом.</span><span class="sxs-lookup"><span data-stu-id="5fc02-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="5fc02-290">`copyToLocal` может выполняться очень медленно для больших файлов, и использовать его с ними не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="5fc02-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="5fc02-291">Ключевое преимущество всех данных находятся в большом двоичном объекте Azure — что мы может исследовать данные hello машинного обучения Azure с помощью hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="5fc02-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="5fc02-292"><a name="#downsample"></a>Сокращение выборки и построение моделей в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="5fc02-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="5fc02-293">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="5fc02-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="5fc02-294">После этапа анализа данных произвольного hello не теперь готовы toodown образец hello данных для построения моделей в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc02-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="5fc02-295">В этом разделе рассказывается, как toouse куст запрос toodown hello данные, которые затем осуществляется из hello [импорта данных] [ import-data] модуль в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc02-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="5fc02-296">Вниз hello данных выборки</span><span class="sxs-lookup"><span data-stu-id="5fc02-296">Down sampling hello data</span></span>
<span data-ttu-id="5fc02-297">Эта процедура состоит из двух шагов.</span><span class="sxs-lookup"><span data-stu-id="5fc02-297">There are two steps in this procedure.</span></span> <span data-ttu-id="5fc02-298">Сначала мы присоединить hello **nyctaxidb.trip** и **nyctaxidb.fare** таблиц на три ключа, которые представлены во всех записях: «medallion», «hack\_лицензии», и «раскладки\_datetime».</span><span class="sxs-lookup"><span data-stu-id="5fc02-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="5fc02-299">Затем мы создаем метку двоичной классификации **tipped** и метку мультиклассовой классификации **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="5fc02-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="5fc02-300">hello может toouse toobe работу выборки данных непосредственно из hello [импорта данных] [ import-data] модуля машинного обучения Azure, при необходимости toostore результаты hello hello выше запрос tooan внутренней таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="5fc02-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="5fc02-301">В ниже создайте внутреннюю таблицу Hive и заполнить его содержимое с объединить hello "и" вниз данных выборки.</span><span class="sxs-lookup"><span data-stu-id="5fc02-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="5fc02-302">Hello запросов применяет стандартные функции Hive непосредственно toogenerate hello час дня, недели года, дня недели (понедельник е. 1 и воскресенье. 7 е.) из hello» раскладки\_datetime» поля и hello прямой расстояние между раскладки hello и dropoff расположения.</span><span class="sxs-lookup"><span data-stu-id="5fc02-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="5fc02-303">Пользователи могут ссылаться слишком[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) полный список таких функций.</span><span class="sxs-lookup"><span data-stu-id="5fc02-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="5fc02-304">Здравствуйте, запрос, а затем вниз образцы данных hello, чтобы результаты запроса hello помещается в студии машинного обучения Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="5fc02-305">Лишь около 1% от исходного набора данных hello импортируется в hello Studio.</span><span class="sxs-lookup"><span data-stu-id="5fc02-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="5fc02-306">Ниже приведены hello содержимое *пример\_куст\_Подготовка\_для\_aml\_full.hql* файл, который подготавливает данные для модели сборки в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc02-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="5fc02-307">запрос для этого запроса из каталога Hive hello toorun:</span><span class="sxs-lookup"><span data-stu-id="5fc02-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="5fc02-308">Теперь у нас есть внутренняя таблица «nyctaxidb.nyctaxi_downsampled_dataset», к которому можно получить с помощью hello [импорта данных] [ import-data] модуля из машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc02-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="5fc02-309">Кроме того, мы можем использовать этот набор данных для построения моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="5fc02-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="5fc02-310">Использование модуля hello импорта данных в hello tooaccess машинного обучения Azure вниз выборки данных</span><span class="sxs-lookup"><span data-stu-id="5fc02-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="5fc02-311">В качестве необходимых компонентов для выдачи запросов Hive в hello [импорта данных] [ import-data] модуля машинного обучения Azure, необходимо получить доступ к рабочей области машинного обучения Azure tooan и доступ к параметрам toohello hello кластер и его соответствующей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5fc02-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="5fc02-312">Некоторые сведения о hello [импорта данных] [ import-data] tooinput параметры модуля и hello:</span><span class="sxs-lookup"><span data-stu-id="5fc02-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="5fc02-313">**URI сервера HCatalog**: Если имя кластера hello abc123, то это просто: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="5fc02-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="5fc02-314">**Имя учетной записи пользователя Hadoop** : hello имени пользователя, выбранного для кластера hello (**не** hello имя пользователя удаленного доступа)</span><span class="sxs-lookup"><span data-stu-id="5fc02-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="5fc02-315">**Пароль учетной записи пользователя Hadoop** : hello пароль, выбранные для кластера hello (**не** hello пароль удаленного доступа)</span><span class="sxs-lookup"><span data-stu-id="5fc02-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="5fc02-316">**Расположение выходных данных** : это выбирается toobe Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc02-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="5fc02-317">**Имя учетной записи хранилища Azure** : имя учетной записи хранения по умолчанию hello связанные с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="5fc02-318">**Имя контейнера Azure** : это имя контейнера по умолчанию hello hello кластера и обычно является Здравствуйте таким же, как имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="5fc02-319">Для кластера с именем «abc123» это будет просто abc123.</span><span class="sxs-lookup"><span data-stu-id="5fc02-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fc02-320">**Любой таблицы, мы обратиться с помощью hello tooquery [импорта данных] [ import-data] модуль в машинном обучении Azure должен быть внутренней таблицы.**</span><span class="sxs-lookup"><span data-stu-id="5fc02-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="5fc02-321">Определить, является ли таблица T в базе данных D.db внутренней таблицей, можно приведенным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="5fc02-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="5fc02-322">Из hello куста каталога строке команды hello проблемы:</span><span class="sxs-lookup"><span data-stu-id="5fc02-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="5fc02-323">Если таблица hello является внутренней таблицей, а он заполняется, его содержимое необходимо отображены здесь.</span><span class="sxs-lookup"><span data-stu-id="5fc02-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="5fc02-324">Другой способ toodetermine ли таблицы во внутреннюю таблицу — toouse hello обозреватель хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc02-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="5fc02-325">Использовать имя контейнера по умолчанию toohello toonavigate hello кластера, а затем отфильтровать по имени таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="5fc02-326">Если hello таблицы и ее содержимое отображается, это подтверждает, что это внутренней таблицы.</span><span class="sxs-lookup"><span data-stu-id="5fc02-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="5fc02-327">Ниже приведен снимок запроса Hive hello и hello [импорта данных] [ import-data] модуля:</span><span class="sxs-lookup"><span data-stu-id="5fc02-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![Запрос Hive для модуля "Импорт данных"](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="5fc02-329">Обратите внимание, что с момента наш список выборки данных располагается в контейнер по умолчанию hello, hello результирующий запрос Hive из машинного обучения Azure очень проста и только» ВЫБЕРИТЕ * из nyctaxidb.nyctaxi\_понижению разрешения\_данных».</span><span class="sxs-lookup"><span data-stu-id="5fc02-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="5fc02-330">набор данных Hello теперь может использоваться как начальная точка для построения моделей машинного обучения hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="5fc02-331"><a name="mlmodel"></a>Построение моделей в компоненте машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="5fc02-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="5fc02-332">Мы стали может tooproceed toomodel построение и развертывание модели в [машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="5fc02-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="5fc02-333">Hello данных готова к нам toouse в устранению проблем прогноза hello, указанных выше:</span><span class="sxs-lookup"><span data-stu-id="5fc02-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="5fc02-334">**1. Двоичная классификация**: toopredict ли уплаченной Совет для маршрута.</span><span class="sxs-lookup"><span data-stu-id="5fc02-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="5fc02-335">**Используемое средство обучения:** двухклассовая логистическая регрессия.</span><span class="sxs-lookup"><span data-stu-id="5fc02-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="5fc02-336">а.</span><span class="sxs-lookup"><span data-stu-id="5fc02-336">a.</span></span> <span data-ttu-id="5fc02-337">Для нашей задачи целевой меткой (меткой класса) будет «tipped» (чаевые выплачены).</span><span class="sxs-lookup"><span data-stu-id="5fc02-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="5fc02-338">В нашем исходном наборе данных с сокращенной выборкой есть несколько столбцов, содержащих целевые утечки сведений для данного эксперимента по классификации.</span><span class="sxs-lookup"><span data-stu-id="5fc02-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="5fc02-339">В частности: совет\_класса, совет\_сумма и общая\_сумма раскрывать информацию о целевой метке hello, который доступен не во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="5fc02-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="5fc02-340">Удалим эти столбцы из рассмотрения с помощью hello [Выбор столбцов в наборе данных] [ select-columns] модуля.</span><span class="sxs-lookup"><span data-stu-id="5fc02-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5fc02-341">моментальный снимок Hello ниже показано нашей toopredict эксперимента ли уплаченной Совет для данного маршрута.</span><span class="sxs-lookup"><span data-stu-id="5fc02-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="5fc02-343">b.</span><span class="sxs-lookup"><span data-stu-id="5fc02-343">b.</span></span> <span data-ttu-id="5fc02-344">Для этого эксперимента распределение наших целевых меток составляло примерно 1:1.</span><span class="sxs-lookup"><span data-stu-id="5fc02-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="5fc02-345">моментальный снимок Hello ниже показано распределение hello меток класса подсказки для проблемы бинарной классификации hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![Распределение меток класса чаевых](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="5fc02-347">В результате мы получаем AUC 0.987, как показано на следующем рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![Значение AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="5fc02-349">**2. Мультиклассовая классификация**: hello диапазон toopredict совет суммы оплаты trip hello, ранее с помощью hello определенных классов.</span><span class="sxs-lookup"><span data-stu-id="5fc02-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="5fc02-350">**Используемое средство обучения:** мультиклассовая логистическая регрессия.</span><span class="sxs-lookup"><span data-stu-id="5fc02-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="5fc02-351">а.</span><span class="sxs-lookup"><span data-stu-id="5fc02-351">a.</span></span> <span data-ttu-id="5fc02-352">Для этой задачи нашей целевой меткой (меткой класса) будет tip\_class, которая может принимать одно из пяти значений (0, 1, 2, 3, 4).</span><span class="sxs-lookup"><span data-stu-id="5fc02-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="5fc02-353">Как и случае hello двоичной классификации у нас есть несколько столбцов, целевой утечки в этом эксперименте.</span><span class="sxs-lookup"><span data-stu-id="5fc02-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="5fc02-354">В частности: чаевых оставил зависимости, совет\_сумма, общее\_сумма раскрывать информацию о целевой метке hello, который доступен не во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="5fc02-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="5fc02-355">Мы удаляем этих столбцов с помощью hello [Выбор столбцов в наборе данных] [ select-columns] модуля.</span><span class="sxs-lookup"><span data-stu-id="5fc02-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5fc02-356">Hello снимок ниже показан нашей toopredict эксперимент, в какие ячейки совет является вероятностью toofall (класса 0: совет = $0, класс 1: совет > $0 и совет < = $5, класса 2: совет > $5 и совет < = 10, 3 класса: совет > 10 и подсказки < = 20 Класс 4: совет > 20)</span><span class="sxs-lookup"><span data-stu-id="5fc02-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="5fc02-358">Теперь мы покажем, как выглядит наше фактическое тестовое классовое распределение.</span><span class="sxs-lookup"><span data-stu-id="5fc02-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="5fc02-359">Мы видим, хотя класса 0 и 1 класс распространено, hello другие классы происходят редко.</span><span class="sxs-lookup"><span data-stu-id="5fc02-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![Тестовое классовое распределение](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="5fc02-361">b.</span><span class="sxs-lookup"><span data-stu-id="5fc02-361">b.</span></span> <span data-ttu-id="5fc02-362">В этом эксперименте мы используем toolook матрицы путаницы в нашем точности прогноза.</span><span class="sxs-lookup"><span data-stu-id="5fc02-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="5fc02-363">Такой способ показан ниже.</span><span class="sxs-lookup"><span data-stu-id="5fc02-363">This is shown below.</span></span>

![Матрица неточностей](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="5fc02-365">Обратите внимание, что пока наш класс точности для наиболее распространенных классов hello достаточно хороша, hello модели не хорошие «обучение» для некоторых классов hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="5fc02-366">**3. Задача регрессии**: оплачена сумма hello toopredict подсказки для маршрута.</span><span class="sxs-lookup"><span data-stu-id="5fc02-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="5fc02-367">**Используемое средство обучения:** повышенное дерево принятия решений.</span><span class="sxs-lookup"><span data-stu-id="5fc02-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="5fc02-368">а.</span><span class="sxs-lookup"><span data-stu-id="5fc02-368">a.</span></span> <span data-ttu-id="5fc02-369">Для нашей задачи целевой меткой (меткой класса) будет "tip\_amount" (сумма чаевых).</span><span class="sxs-lookup"><span data-stu-id="5fc02-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="5fc02-370">Утечки нашей цели в данном случае являются: чаевых оставил зависимости, совет\_класса, общее\_сумма; эти переменные позволяют просматривать информацию о сумма hello подсказки, которая обычно недоступна во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="5fc02-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="5fc02-371">Мы удаляем этих столбцов с помощью hello [Выбор столбцов в наборе данных] [ select-columns] модуля.</span><span class="sxs-lookup"><span data-stu-id="5fc02-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="5fc02-372">belows Hello моментальных снимков отображается нашей эксперимента toopredict hello объем hello заданному подсказки.</span><span class="sxs-lookup"><span data-stu-id="5fc02-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="5fc02-374">b.</span><span class="sxs-lookup"><span data-stu-id="5fc02-374">b.</span></span> <span data-ttu-id="5fc02-375">Для проблем регрессии мы измерения точности hello нашей прогноза, просмотрев ошибки hello квадрат в прогнозах hello hello коэффициент смешанной корреляции и hello как.</span><span class="sxs-lookup"><span data-stu-id="5fc02-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="5fc02-376">Они показаны ниже.</span><span class="sxs-lookup"><span data-stu-id="5fc02-376">We show these below.</span></span>

![Статистические данные прогноза](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="5fc02-378">Мы видим, что о hello коэффициент детерминации это 0.709, подразумевая около 71% дисперсию hello объясняется коэффициенты нашей модели.</span><span class="sxs-lookup"><span data-stu-id="5fc02-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fc02-379">Дополнительные сведения о машинного обучения Azure toolearn и как tooaccess и использовать его, воспользуйтесь слишком[возможности машинного обучения?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="5fc02-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="5fc02-380">Очень полезным ресурсом для воспроизведения с кучей экспериментах машинного обучения на машинном обучении Azure — hello [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="5fc02-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="5fc02-381">Коллекция Hello охватывает охват экспериментов и подробное введение в hello диапазон возможностей машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc02-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="5fc02-382">Сведения о лицензии</span><span class="sxs-lookup"><span data-stu-id="5fc02-382">License Information</span></span>
<span data-ttu-id="5fc02-383">Это пошаговое руководство по примеру и его соответствующие сценарии совместно корпорацией Майкрософт в рамках лицензии MIT hello.</span><span class="sxs-lookup"><span data-stu-id="5fc02-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="5fc02-384">Проверьте файл LICENSE.txt hello в каталоге hello hello образца кода на GitHub для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="5fc02-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="5fc02-385">Ссылки</span><span class="sxs-lookup"><span data-stu-id="5fc02-385">References</span></span>
<span data-ttu-id="5fc02-386">•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="5fc02-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="5fc02-387">•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="5fc02-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="5fc02-388">•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="5fc02-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
