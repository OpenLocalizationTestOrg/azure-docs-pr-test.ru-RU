---
title: "Изучение данных в кластере Hadoop и создание моделей в Машинном обучении Azure | Документация Майкрософт"
description: "Применение процесса обработки и анализа данных группы в комплексном сценарии, включающем в себя использование кластера HDInsight Hadoop для создания и развертывания модели на основе общедоступного набора данных."
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
ms.openlocfilehash: e48d59ca467e3e7fd772389e6e48a2d81726f859
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="c006d-103">Процесс обработки и анализа данных группы на практике: использование кластеров Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="c006d-103">The Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="c006d-104">В этом пошаговом руководстве показано комплексное использование [процесса обработки и анализа данных группы (TDSP)](data-science-process-overview.md), где [кластер Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) используется для хранения и просмотра данных из общедоступного набора данных [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) (Поездки такси Нью-Йорка), реконструирования их характеристик и сокращения их выборки.</span><span class="sxs-lookup"><span data-stu-id="c006d-104">In this walkthrough, we use the [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore and feature engineer data from the publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and to down sample the data.</span></span> <span data-ttu-id="c006d-105">Модели данных создаются с помощью машинного обучения Azure для обработки двоичных и мультиклассовых классификационных и регрессионных прогнозных задач.</span><span class="sxs-lookup"><span data-stu-id="c006d-105">Models of the data are built with Azure Machine Learning to handle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="c006d-106">Пошаговое руководство, показывающее, как обработать более крупный (1 ТБ) набор данных для подобного сценария с помощью кластеров HDInsight Hadoop для обработки данных, см. в статье [Процесс обработки и анализа данных группы на практике: использование кластеров Azure HDInsight Hadoop с набором данных объемом 1 ТБ](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c006d-106">For a walkthrough that shows how to handle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="c006d-107">Кроме того, для выполнения заданий, представленных в этом пошаговом руководстве, с помощью набора данных объемом 1 ТБ, можно использовать iPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="c006d-107">It is also possible to use an IPython notebook to accomplish the tasks presented the walkthrough using the 1 TB dataset.</span></span> <span data-ttu-id="c006d-108">Пользователям, которые хотят применить этот подход, следует просмотреть раздел [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) (Пошаговое руководство Criteo по использованию подключения Hive ODBC).</span><span class="sxs-lookup"><span data-stu-id="c006d-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="c006d-109"><a name="dataset"></a>Описание набора данных «Поездки такси Нью-Йорка»</span><span class="sxs-lookup"><span data-stu-id="c006d-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="c006d-110">Сведения о поездках на такси в Нью-Йорке заключены в сжатые файлы данных с разделителями-запятыми (CSV) объемом около 20 ГБ (~48 ГБ без сжатия), которые содержат более 173 миллионов записей о поездках и о стоимости каждой из них.</span><span class="sxs-lookup"><span data-stu-id="c006d-110">The NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="c006d-111">Каждая запись о поездке содержит расположение пунктов отправления и назначения и время, анонимизированный номер лицензии водителя и номер медальона (уникальный идентификатор такси).</span><span class="sxs-lookup"><span data-stu-id="c006d-111">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="c006d-112">Данные включают в себя все поездки за 2013 год и предоставляются в виде следующих двух наборов данных за каждый месяц:</span><span class="sxs-lookup"><span data-stu-id="c006d-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="c006d-113">В CSV-файлах trip_data содержатся сведения о поездках, например количество пассажиров, места посадки и высадки, продолжительность и дальность поездок.</span><span class="sxs-lookup"><span data-stu-id="c006d-113">The 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="c006d-114">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="c006d-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="c006d-115">В CSV-файлах trip_fare содержатся сведения о плате за каждую поездку, например тип оплаты, стоимость поездки, добавочная стоимость и налоги, чаевые и специальные тарифы, а также общая сумма оплаты.</span><span class="sxs-lookup"><span data-stu-id="c006d-115">The 'trip_fare' CSV files contain details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="c006d-116">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="c006d-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="c006d-117">Уникальный ключ для объединения trip\_data и trip\_fare состоит из полей medallion, hack\_licence и pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="c006d-117">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="c006d-118">Чтобы получить все данные, относящиеся к определенной поездке, достаточно выполнить объединение с тремя ключами: "medallion", "hack\_license" и "pickup\_datetime".</span><span class="sxs-lookup"><span data-stu-id="c006d-118">To get all of the details relevant to a particular trip, it is sufficient to join with three keys: the "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="c006d-119">Дополнительную информацию о данных мы предоставим ниже, в разделе о сохранении данных в таблицах Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-119">We describe some more details of the data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="c006d-120"><a name="mltasks"></a>Примеры задач прогнозирования</span><span class="sxs-lookup"><span data-stu-id="c006d-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="c006d-121">При работе с данными определение типа прогноза, который вам нужен, на основе анализа поможет выяснить задачи, которые нужно будет включить в процесс обработки.</span><span class="sxs-lookup"><span data-stu-id="c006d-121">When approaching data, determining the kind of predictions you want to make based on its analysis helps clarify the tasks that you will need to include in your process.</span></span>
<span data-ttu-id="c006d-122">Ниже приведены три примера проблем прогнозирования, с которыми мы будем разбираться в рамках данного руководства и которые сформулированы на основе *tip\_amount*.</span><span class="sxs-lookup"><span data-stu-id="c006d-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on the *tip\_amount*:</span></span>

1. <span data-ttu-id="c006d-123">**Двоичная классификация**: спрогнозировать, были ли оставлены чаевые после поездку, т. е. значение *tip\_amount* больше 0 $ является позитивным примером, а значение *tip\_amount* 0 $ является негативным примером.</span><span class="sxs-lookup"><span data-stu-id="c006d-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="c006d-124">**Мультиклассовая классификация**: спрогнозировать диапазон суммы чаевых за поездку.</span><span class="sxs-lookup"><span data-stu-id="c006d-124">**Multiclass classification**: To predict the range of tip amounts paid for the trip.</span></span> <span data-ttu-id="c006d-125">Мы разделяем *tip\_amount* на пять ячеек или классов:</span><span class="sxs-lookup"><span data-stu-id="c006d-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="c006d-126">**Задача регрессии**: спрогнозировать сумму чаевых, выплаченных за поездку.</span><span class="sxs-lookup"><span data-stu-id="c006d-126">**Regression task**: To predict the amount of the tip paid for a trip.</span></span>  

## <span data-ttu-id="c006d-127"><a name="setup"></a>Настройка кластера HDInsight Hadoop для расширенной аналитики</span><span class="sxs-lookup"><span data-stu-id="c006d-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-128">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="c006d-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c006d-129">Настроить среду Azure для использования расширенной аналитики, в которой задействуется кластер HDInsight, вы можете в три этапа.</span><span class="sxs-lookup"><span data-stu-id="c006d-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="c006d-130">[Создание учетной записи хранения](../storage/common/storage-create-storage-account.md). Эта учетная запись используется для хранения данных в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="c006d-131">Здесь находятся также и данные, используемые в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c006d-131">The data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="c006d-132">[Настройка кластеров Azure HDInsight Hadoop для технологии и процесса расширенного анализа](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c006d-132">[Customize Azure HDInsight Hadoop clusters for the Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="c006d-133">На этом этапе создается кластер Azure HDInsight Hadoop, на всех узлах которого установлена 64-разрядная версия Anaconda Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="c006d-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="c006d-134">Существует два важных действия, которые нужно не забыть выполнить при настройке кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c006d-134">There are two important steps to remember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="c006d-135">Во время создания кластера HDInsight не забудьте связать учетную запись хранения, созданную на шаге 1, с этим кластером.</span><span class="sxs-lookup"><span data-stu-id="c006d-135">Remember to link the storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="c006d-136">Эта учетная запись хранения используется для доступа к данным, которые обрабатываются в пределах кластера.</span><span class="sxs-lookup"><span data-stu-id="c006d-136">This storage account is used to access data that is processed within the cluster.</span></span>
   * <span data-ttu-id="c006d-137">После создания кластера включите удаленный доступ к головному узлу кластера.</span><span class="sxs-lookup"><span data-stu-id="c006d-137">After the cluster is created, enable Remote Access to the head node of the cluster.</span></span> <span data-ttu-id="c006d-138">Перейдите на вкладку **Конфигурация** и нажмите кнопку **Включить удаленный доступ**.</span><span class="sxs-lookup"><span data-stu-id="c006d-138">Navigate to the **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="c006d-139">На этом шаге указываются учетные данные пользователя для удаленного входа.</span><span class="sxs-lookup"><span data-stu-id="c006d-139">This step specifies the user credentials used for remote login.</span></span>
3. <span data-ttu-id="c006d-140">[Создание рабочей области машинного обучения Azure](machine-learning-create-workspace.md): эта рабочая область используется для построения моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="c006d-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used to build machine learning models.</span></span> <span data-ttu-id="c006d-141">Эта задача решается после начального исследования данных и сокращения выборки с использованием кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c006d-141">This task is addressed after completing an initial data exploration and down sampling using the HDInsight cluster.</span></span>

## <span data-ttu-id="c006d-142"><a name="getdata"></a>Получение данных из общедоступного источника</span><span class="sxs-lookup"><span data-stu-id="c006d-142"><a name="getdata"></a>Get the data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-143">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="c006d-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c006d-144">Если вам нужно получить набор данных [Поездки такси Нью-Йорка](http://www.andresmh.com/nyctaxitrips/) из общедоступного расположения, чтобы скопировать их на свой компьютер, вы можете воспользоваться любым из методов, описанных в статье [Перемещение данных в хранилище больших двоичных объектов Azure и из него](machine-learning-data-science-move-azure-blob.md).</span><span class="sxs-lookup"><span data-stu-id="c006d-144">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your machine.</span></span>

<span data-ttu-id="c006d-145">Здесь рассматривается использование AzCopy для передачи файлов, содержащих данные.</span><span class="sxs-lookup"><span data-stu-id="c006d-145">Here we describe how use AzCopy to transfer the files containing data.</span></span> <span data-ttu-id="c006d-146">Чтобы загрузить и установить AzCopy, следуйте инструкциям в статье [Приступая к работе со служебной программой командной строки AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="c006d-146">To download and install AzCopy follow the instructions at [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="c006d-147">В окне командной строки выполните приведенные ниже команды AzCopy, заменяя *<path_to_data_folder>* путем к нужному месту назначения.</span><span class="sxs-lookup"><span data-stu-id="c006d-147">From a Command Prompt window, issue the following AzCopy commands, replacing *<path_to_data_folder>* with the desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="c006d-148">По завершении копирования выбранная папка данных будет содержать в общей сложности 24 ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="c006d-148">When the copy completes, a total of 24 zipped files are in the data folder chosen.</span></span> <span data-ttu-id="c006d-149">Распакуйте загруженные файлы в тот же каталог на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c006d-149">Unzip the downloaded files to the same directory on your local machine.</span></span> <span data-ttu-id="c006d-150">Обратите внимание на папку, в которой располагаются распакованные файлы.</span><span class="sxs-lookup"><span data-stu-id="c006d-150">Make a note of the folder where the uncompressed files reside.</span></span> <span data-ttu-id="c006d-151">Далее по тексту мы будем называть эту папку *<path\_to\_unzipped_data\_files\>*.</span><span class="sxs-lookup"><span data-stu-id="c006d-151">This folder will be referred to as the *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="c006d-152"><a name="upload"></a>Отправка данных в контейнер по умолчанию кластера Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="c006d-152"><a name="upload"></a>Upload the data to the default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-153">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="c006d-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c006d-154">В следующих командах AzCopy замените приведенные ниже параметры фактическими значениями, указанными при создании кластера Hadoop и распаковке файлов данных.</span><span class="sxs-lookup"><span data-stu-id="c006d-154">In the following AzCopy commands, replace the following parameters with the actual values that you specified when creating the Hadoop cluster and unzipping the data files.</span></span>

* <span data-ttu-id="c006d-155">***&#60;path_to_data_folder>*** — каталог (вместе с путем) на компьютере, где содержатся распакованные файлы данных.</span><span class="sxs-lookup"><span data-stu-id="c006d-155">***&#60;path_to_data_folder>*** the directory (along with path) on your machine that contain the unzipped data files</span></span>  
* <span data-ttu-id="c006d-156">***&#60;storage account name of Hadoop cluster>*** — учетная запись хранения, связанная с вашим кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c006d-156">***&#60;storage account name of Hadoop cluster>*** the storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="c006d-157">***&#60;default container of Hadoop cluster>*** — контейнер по умолчанию, используемый кластером.</span><span class="sxs-lookup"><span data-stu-id="c006d-157">***&#60;default container of Hadoop cluster>*** the default container used by your cluster.</span></span> <span data-ttu-id="c006d-158">Обратите внимание, что имя контейнера по умолчанию обычно совпадает с именем самого кластера.</span><span class="sxs-lookup"><span data-stu-id="c006d-158">Note that the name of the default container is usually the same name as the cluster itself.</span></span> <span data-ttu-id="c006d-159">Например, если кластер называется abc123.azurehdinsight.net, контейнером по умолчанию будет abc123.</span><span class="sxs-lookup"><span data-stu-id="c006d-159">For example, if the cluster is called "abc123.azurehdinsight.net", the default container is abc123.</span></span>
* <span data-ttu-id="c006d-160">***&#60;storage account key>*** — ключ для учетной записи хранения, используемой вашим кластером.</span><span class="sxs-lookup"><span data-stu-id="c006d-160">***&#60;storage account key>*** the key for the storage account used by your cluster</span></span>

<span data-ttu-id="c006d-161">В командной строке или окне Windows PowerShell выполните две приведенные ниже команды AzCopy.</span><span class="sxs-lookup"><span data-stu-id="c006d-161">From a Command Prompt or a Windows PowerShell window in your machine, run the following two AzCopy commands.</span></span>

<span data-ttu-id="c006d-162">Эта команда передает данные о поездке в каталог ***nyctaxitripraw*** в контейнере по умолчанию кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c006d-162">This command uploads the trip data to ***nyctaxitripraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="c006d-163">Эта команда передает данные о тарифе в каталог ***nyctaxifareraw*** в контейнере по умолчанию кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c006d-163">This command uploads the fare data to ***nyctaxifareraw*** directory in the default container of the Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="c006d-164">Теперь данные должны находиться в хранилище больших двоичных объектов Azure и быть готовы к использованию в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c006d-164">The data should now in Azure Blob Storage and ready to be consumed within the HDInsight cluster.</span></span>

## <span data-ttu-id="c006d-165"><a name="#download-hql-files"></a>Вход в головной узел кластера Hadoop и подготовка к исследовательскому анализу данных</span><span class="sxs-lookup"><span data-stu-id="c006d-165"><a name="#download-hql-files"></a>Log into the head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-166">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="c006d-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c006d-167">Чтобы получить доступ к головному узлу кластера в целях исследовательского анализа данных и сокращения их выборки, выполните процедуру, описанную в разделе [Доступ к головному узлу кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="c006d-167">To access the head node of the cluster for exploratory data analysis and down sampling of the data, follow the procedure outlined in [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="c006d-168">Для предварительных исследований данных мы в этом пошаговом руководстве в основном используем запросы, написанные на языке запросов [Hive](https://hive.apache.org/)(он похож на язык SQL).</span><span class="sxs-lookup"><span data-stu-id="c006d-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, to perform preliminary data explorations.</span></span> <span data-ttu-id="c006d-169">Запросы Hive хранятся в HQL-файлах.</span><span class="sxs-lookup"><span data-stu-id="c006d-169">The Hive queries are stored in .hql files.</span></span> <span data-ttu-id="c006d-170">Затем мы сокращаем выборку этих данных, которые будут использоваться в машинном обучении Azure для построения моделей.</span><span class="sxs-lookup"><span data-stu-id="c006d-170">We then down sample this data to be used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="c006d-171">Чтобы подготовить кластер к исследовательскому анализу, мы загрузим HQL-файлы, содержащие соответствующие сценарии Hive, с [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) в локальный каталог (C:\temp) на головном узле.</span><span class="sxs-lookup"><span data-stu-id="c006d-171">To prepare the cluster for exploratory data analysis, we download the .hql files containing the relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) to a local directory (C:\temp) on the head node.</span></span> <span data-ttu-id="c006d-172">Чтобы сделать это, откройте **командную строку** на головном узле кластера и введите две приведенные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="c006d-172">To do this, open the **Command Prompt** from within the head node of the cluster and issue the following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="c006d-173">Эти две команды загрузят все необходимые в этом пошаговом руководстве HQL-файлы в локальный каталог ***C:\temp&#92;*** головного узла.</span><span class="sxs-lookup"><span data-stu-id="c006d-173">These two commands will download all .hql files needed in this walkthrough to the local directory ***C:\temp&#92;*** in the head node.</span></span>

## <span data-ttu-id="c006d-174"><a name="#hive-db-tables"></a>Создание базы данных Hive и таблиц, секционированных по месяцам</span><span class="sxs-lookup"><span data-stu-id="c006d-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-175">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="c006d-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c006d-176">Теперь мы готовы создать таблицы Hive для нашего набора данных о такси Нью-Йорка.</span><span class="sxs-lookup"><span data-stu-id="c006d-176">We are now ready to create Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="c006d-177">На головном узле кластера Hadoop откройте ***командной строки Hadoop*** на рабочем столе головного узла и войдите в каталог Hive с помощью команды</span><span class="sxs-lookup"><span data-stu-id="c006d-177">In the head node of the Hadoop cluster, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="c006d-178">**Выполняйте все команды Hive в этом пошаговом руководстве из указанного выше запроса командной строки bin/directory. Таким образом вы сможете автоматически избежать любых проблем с путем. Термины "командная строка каталога Hive", "командная строка Hive bin/directory" и "командная строка Hadoop" в этом руководстве являются взаимозаменяемыми.**</span><span class="sxs-lookup"><span data-stu-id="c006d-178">**Run all Hive commands in this walkthrough from the above Hive bin/ directory prompt. This will take care of any path issues automatically. We use the terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="c006d-179">В командной строке каталога Hive введите приведенную ниже команду в командную строку Hadoop головного узла, чтобы отправить запрос Hive для создания базы данных и таблиц Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-179">From the Hive directory prompt, enter the following command in Hadoop Command Line of the head node to submit the Hive query to create Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="c006d-180">Ниже приведено содержимое файла ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql***, который создает базу данных Hive ***nyctaxidb*** и таблицы ***trip*** и ***fare***.</span><span class="sxs-lookup"><span data-stu-id="c006d-180">Here is the content of the ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

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

<span data-ttu-id="c006d-181">Этот сценарий Hive создает две таблицы:</span><span class="sxs-lookup"><span data-stu-id="c006d-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="c006d-182">в таблице «trip» содержатся подробные сведения о каждой поездке (сведения о водителе, время отправки, расстояние поездки и время);</span><span class="sxs-lookup"><span data-stu-id="c006d-182">the "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="c006d-183">в таблице «fare» содержатся подробные сведения о тарифе (сумма тарифа, сумма чаевых, сборы и наценки).</span><span class="sxs-lookup"><span data-stu-id="c006d-183">the "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="c006d-184">Если вам требуется дополнительная помощь в работе с этими процедурами или вы хотите изучить альтернативы, см. раздел [Отправка запросов Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="c006d-184">If you need any additional assistance with these procedures or want to investigate alternative ones, see the section [Submit Hive queries directly from the Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="c006d-185"><a name="#load-data"></a>Загрузка данных в таблицы Hive по разделам</span><span class="sxs-lookup"><span data-stu-id="c006d-185"><a name="#load-data"></a>Load Data to Hive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-186">Эту задачу обычно выполняет **администратор** .</span><span class="sxs-lookup"><span data-stu-id="c006d-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="c006d-187">Набор данных о такси Нью-Йорка содержит естественное секционирование по месяцам, которое используется для ускорения обработки и выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="c006d-187">The NYC taxi dataset has a natural partitioning by month, which we use to enable faster processing and query times.</span></span> <span data-ttu-id="c006d-188">Приведенные ниже команды PowerShell (которые вводятся из каталога Hive с помощью **командной строки Hadoop**) загружают данные в таблицы Hive «trip» и «fare», секционированные по месяцам.</span><span class="sxs-lookup"><span data-stu-id="c006d-188">The PowerShell commands below (issued from the Hive directory using the **Hadoop Command Line**) load data to the "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="c006d-189">В файле *sample\_hive\_load\_data\_by\_partitions.hql* содержатся приведенные ниже команды **LOAD**.</span><span class="sxs-lookup"><span data-stu-id="c006d-189">The *sample\_hive\_load\_data\_by\_partitions.hql* file contains the following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="c006d-190">Обратите внимание, что ряд запросов Hive, которые мы используем здесь в процессе исследования, предусматривает поиск только в одном разделе или в небольшом их количестве.</span><span class="sxs-lookup"><span data-stu-id="c006d-190">Note that a number of Hive queries we use here in the exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="c006d-191">Однако эти запросы можно выполнять по всем данным.</span><span class="sxs-lookup"><span data-stu-id="c006d-191">But these queries could be run across the entire data.</span></span>

### <span data-ttu-id="c006d-192"><a name="#show-db"></a>Отображение баз данных в кластере HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="c006d-192"><a name="#show-db"></a>Show databases in the HDInsight Hadoop cluster</span></span>
<span data-ttu-id="c006d-193">Чтобы отобразить базы данных, созданные в кластере HDInsight Hadoop в окне командной строки Hadoop, выполните в командной строке Hadoop приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-193">To show the databases created in HDInsight Hadoop cluster inside the Hadoop Command Line window, run the following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="c006d-194"><a name="#show-tables"></a>Отображение таблиц Hive в базе данных nyctaxidb</span><span class="sxs-lookup"><span data-stu-id="c006d-194"><a name="#show-tables"></a>Show the Hive tables in the nyctaxidb database</span></span>
<span data-ttu-id="c006d-195">Для отображения таблиц в базе данных nyctaxidb выполните в командной строке Hadoop приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-195">To show the tables in the nyctaxidb database, run the following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="c006d-196">Мы можем убедиться, что таблицы секционированы, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-196">We can confirm that the tables are partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="c006d-197">Ожидаемые выходные данные показаны ниже.</span><span class="sxs-lookup"><span data-stu-id="c006d-197">The expected output is shown below:</span></span>

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

<span data-ttu-id="c006d-198">Аналогично мы можем убедиться в том, что таблица fare секционирована, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-198">Similarly, we can ensure that the fare table is partitioned by issuing the command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="c006d-199">Ожидаемые выходные данные показаны ниже.</span><span class="sxs-lookup"><span data-stu-id="c006d-199">The expected output is shown below:</span></span>

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

## <span data-ttu-id="c006d-200"><a name="#explore-hive"></a>Исследование данных и проектирование признаков в Hive</span><span class="sxs-lookup"><span data-stu-id="c006d-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-201">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-202">Задачи, которые связаны с просмотром данных и созданием функций и которые относятся к данным, загруженным в таблицы Hive, вы можете выполнить с помощью запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-202">The data exploration and feature engineering tasks for the data loaded into the Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="c006d-203">Вот примеры задач, о которых пойдет речь в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="c006d-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="c006d-204">Просмотр 10 верхних записей в обеих таблицах.</span><span class="sxs-lookup"><span data-stu-id="c006d-204">View the top 10 records in both tables.</span></span>
* <span data-ttu-id="c006d-205">Просмотрим распределение данных по нескольким полям в различных временных окнах.</span><span class="sxs-lookup"><span data-stu-id="c006d-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="c006d-206">Исследуем качество данных по полям долготы и широты.</span><span class="sxs-lookup"><span data-stu-id="c006d-206">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="c006d-207">Создадим метки двоичной и мультиклассовой классификации на основе **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="c006d-207">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="c006d-208">Создание функций путем вычисления дальности поездки.</span><span class="sxs-lookup"><span data-stu-id="c006d-208">Generate features by computing the direct trip distances.</span></span>

### <a name="exploration-view-the-top-10-records-in-table-trip"></a><span data-ttu-id="c006d-209">Исследование: просмотр 10 верхних записей в таблице trip</span><span class="sxs-lookup"><span data-stu-id="c006d-209">Exploration: View the top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-210">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-211">Чтобы увидеть, как выглядят данные, мы изучим по 10 записей из каждой таблицы.</span><span class="sxs-lookup"><span data-stu-id="c006d-211">To see what the data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="c006d-212">Чтобы просмотреть записи, выполните приведенные ниже два запроса по отдельности в консоли командной строки Hadoop из каталога Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-212">Run the following two queries separately from the Hive directory prompt in the Hadoop Command Line console to inspect the records.</span></span>

<span data-ttu-id="c006d-213">Чтобы получить первые 10 записей в таблице «trip» за первый месяц:</span><span class="sxs-lookup"><span data-stu-id="c006d-213">To get the top 10 records in the table "trip" from the first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="c006d-214">Чтобы получить первые 10 записей в таблице «fare» за первый месяц:</span><span class="sxs-lookup"><span data-stu-id="c006d-214">To get the top 10 records in the table "fare" from the first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="c006d-215">Часто полезно сохранять записи в файл для удобного просмотра.</span><span class="sxs-lookup"><span data-stu-id="c006d-215">It is often useful to save the records to a file for convenient viewing.</span></span> <span data-ttu-id="c006d-216">Это достигается небольшим изменением приведенного выше запроса:</span><span class="sxs-lookup"><span data-stu-id="c006d-216">A small change to the above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-the-number-of-records-in-each-of-the-12-partitions"></a><span data-ttu-id="c006d-217">Исследование: просмотр количества записей в каждом из 12 разделов</span><span class="sxs-lookup"><span data-stu-id="c006d-217">Exploration: View the number of records in each of the 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-218">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-219">Интерес представляет варьирование числа поездок в течение календарного года.</span><span class="sxs-lookup"><span data-stu-id="c006d-219">Of interest is the how the number of trips varies during the calendar year.</span></span> <span data-ttu-id="c006d-220">Группирование по месяцам позволяет увидеть, как выглядит такое распределение поездок.</span><span class="sxs-lookup"><span data-stu-id="c006d-220">Grouping by month allows us to see what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="c006d-221">Мы получаем приведенные ниже выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c006d-221">This gives us the output :</span></span>

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

<span data-ttu-id="c006d-222">Здесь первый столбец обозначает месяц, а второй содержит количество поездок за этот месяц.</span><span class="sxs-lookup"><span data-stu-id="c006d-222">Here, the first column is the month and the second is the number of trips for that month.</span></span>

<span data-ttu-id="c006d-223">Кроме того, мы можем подсчитать общее число записей в нашем наборе данных о поездках, выполнив следующую команду в командной строке каталога Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-223">We can also count the total number of records in our trip data set by issuing the following command at the Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="c006d-224">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="c006d-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="c006d-225">Чтобы проверить количество записей, мы можем с помощью команд, подобных показанным для набора данных о поездках (trip), выполнить запросы Hive в командной строке каталога Hive для набора данных о тарифах (fare).</span><span class="sxs-lookup"><span data-stu-id="c006d-225">Using commands similar to those shown for the trip data set, we can issue Hive queries from the Hive directory prompt for the fare data set to validate the number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="c006d-226">Мы получаем приведенные ниже выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c006d-226">This gives us the output:</span></span>

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

<span data-ttu-id="c006d-227">Обратите внимание, что для обоих наборов данных возвращается в точности одинаковое количество поездок в месяц.</span><span class="sxs-lookup"><span data-stu-id="c006d-227">Note that the exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="c006d-228">Это первое подтверждение правильности загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="c006d-228">This provides the first validation that the data has been loaded correctly.</span></span>

<span data-ttu-id="c006d-229">Подсчет общего числа записей в наборе данных о тарифах можно выполнить с помощью приведенной ниже команды в командной строке каталога Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-229">Counting the total number of records in the fare data set can be done using the command below from the Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="c006d-230">Мы получаем такой результат.</span><span class="sxs-lookup"><span data-stu-id="c006d-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="c006d-231">Совпадает и общее число записей в обеих таблицах.</span><span class="sxs-lookup"><span data-stu-id="c006d-231">The total number of records in both tables is also the same.</span></span> <span data-ttu-id="c006d-232">Это второе подтверждение правильности загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="c006d-232">This provides a second validation that the data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="c006d-233">Просмотр: распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="c006d-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-234">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-235">В этом примере определяются медальоны (номера такси) с более чем 100 поездками за заданный период времени.</span><span class="sxs-lookup"><span data-stu-id="c006d-235">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="c006d-236">Этот запрос выигрывает от доступа к секционированной таблице, поскольку в нем содержится условие, заданное переменной раздела **month**.</span><span class="sxs-lookup"><span data-stu-id="c006d-236">The query benefits from the partitioned table access since it is conditioned by the partition variable **month**.</span></span> <span data-ttu-id="c006d-237">Результаты запроса записываются в локальный файл queryoutput.tsv в `C:\temp` на головном узле.</span><span class="sxs-lookup"><span data-stu-id="c006d-237">The query results are written to a local file queryoutput.tsv in `C:\temp` on the head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="c006d-238">Вот содержимое файла *sample\_hive\_trip\_count\_by\_medallion.hql* для проверки.</span><span class="sxs-lookup"><span data-stu-id="c006d-238">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="c006d-239">Медальон в наборе данных о такси Нью-Йорка идентифицирует уникальный автомобиль такси.</span><span class="sxs-lookup"><span data-stu-id="c006d-239">The medallion in the NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="c006d-240">Мы можем определить, какие автомобили востребованы, запросив, какие из них выполнили более определенного количества поездок за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="c006d-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="c006d-241">В следующем примере идентифицируются автомобили, которые выполнили более ста поездок за первые три месяца, и результаты запроса сохраняются в локальном файле C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="c006d-241">The following example identifies cabs that made more than a hundred trips in the first three months, and saves the query results to a local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="c006d-242">Вот содержимое файла *sample\_hive\_trip\_count\_by\_medallion.hql* для проверки.</span><span class="sxs-lookup"><span data-stu-id="c006d-242">Here is the content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="c006d-243">В командной строке каталога Hive выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-243">From the Hive directory prompt, issue the command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="c006d-244">Просмотр: распределение поездок по параметрам medallion и hack_license</span><span class="sxs-lookup"><span data-stu-id="c006d-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-245">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-246">При исследовании набора данных нам часто требуется проверить количество вхождений тех или иных групп значений.</span><span class="sxs-lookup"><span data-stu-id="c006d-246">When exploring a dataset, we frequently want to examine the number of co-occurences of groups of values.</span></span> <span data-ttu-id="c006d-247">В этом разделе приводится пример того, как сделать это для автомобилей и водителей.</span><span class="sxs-lookup"><span data-stu-id="c006d-247">This section provide an example of how to do this for cabs and drivers.</span></span>

<span data-ttu-id="c006d-248">Файл *sample\_hive\_trip\_count\_by\_medallion\_license.hql* группирует набор данных о тарифах по параметрам medallion и hack_license и возвращает количество вхождений каждой из комбинаций.</span><span class="sxs-lookup"><span data-stu-id="c006d-248">The *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups the fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="c006d-249">Ниже приведено его содержимое.</span><span class="sxs-lookup"><span data-stu-id="c006d-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="c006d-250">Этот запрос возвращает комбинации автомобиля и конкретного водителя, упорядоченных по убыванию количества поездок.</span><span class="sxs-lookup"><span data-stu-id="c006d-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="c006d-251">В командной строке каталога Hive выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-251">From the Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="c006d-252">Результаты запроса записываются в локальный файл C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="c006d-252">The query results are written to a local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="c006d-253">Исследование: оценка качества данных через проверку наличия недопустимых записей долготы и широты</span><span class="sxs-lookup"><span data-stu-id="c006d-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-254">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-255">Общей целью исследовательского анализа данных является отсеивание недопустимых или неверных записей.</span><span class="sxs-lookup"><span data-stu-id="c006d-255">A common objective of exploratory data analysis is to weed out invalid or bad records.</span></span> <span data-ttu-id="c006d-256">Пример в этом разделе определяет, содержатся ли в полях долготы (longitude) и широты (latitude) значения, указывающие на местоположения далеко за пределами региона Нью-Йорка.</span><span class="sxs-lookup"><span data-stu-id="c006d-256">The example in this section determines whether either the longitude or latitude fields contain a value far outside the NYC area.</span></span> <span data-ttu-id="c006d-257">Так как вероятно, что в таких записях будут содержаться ошибочные значения долготы и широты, нам следует устранить их из любых данных, которые будут использоваться для моделирования.</span><span class="sxs-lookup"><span data-stu-id="c006d-257">Since it is likely that such records have an erroneous longitude-latitude values, we want to eliminate them from any data that is to be used for modeling.</span></span>

<span data-ttu-id="c006d-258">Вот содержимое файла *sample\_hive\_quality\_assessment.hql* для проверки.</span><span class="sxs-lookup"><span data-stu-id="c006d-258">Here is the content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="c006d-259">В командной строке каталога Hive выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-259">From the Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="c006d-260">Аргумент *-S* этой команды скрывает окно состояния задач Hive Map/Reduce.</span><span class="sxs-lookup"><span data-stu-id="c006d-260">The *-S* argument included in this command suppresses the status screen printout of the Hive Map/Reduce jobs.</span></span> <span data-ttu-id="c006d-261">Это очень полезно, так как отображение запроса Hive становится более удобочитаемым.</span><span class="sxs-lookup"><span data-stu-id="c006d-261">This is useful because it makes the screen print of the Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="c006d-262">Исследования: двоичные классовые распределения чаевых за поездки</span><span class="sxs-lookup"><span data-stu-id="c006d-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-263">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-264">Касательно проблемы двоичной классификации, изложенной в разделе [Примеры задач прогнозирования](machine-learning-data-science-process-hive-walkthrough.md#mltasks) , полезно знать, были ли выплачены чаевые за поездку.</span><span class="sxs-lookup"><span data-stu-id="c006d-264">For the binary classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful to know whether a tip was given or not.</span></span> <span data-ttu-id="c006d-265">Распределение чаевых является двоичным:</span><span class="sxs-lookup"><span data-stu-id="c006d-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="c006d-266">чаевые оставлены (класс 1, tip\_amount > $0);</span><span class="sxs-lookup"><span data-stu-id="c006d-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="c006d-267">чаевые не оставлены (класс 0, tip\_amount = $0).</span><span class="sxs-lookup"><span data-stu-id="c006d-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="c006d-268">Для этого следует использовать приведенный ниже файл *sample\_hive\_tipped\_frequencies.hql*.</span><span class="sxs-lookup"><span data-stu-id="c006d-268">The *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="c006d-269">В командной строке каталога Hive выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-269">From the Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-the-multiclass-setting"></a><span data-ttu-id="c006d-270">Исследование: классовые распределения при мультиклассовой настройке</span><span class="sxs-lookup"><span data-stu-id="c006d-270">Exploration: Class distributions in the multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-271">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-272">Для проблемы мультиклассовой классификации, изложенной в разделе [Примеры задач прогнозирования](machine-learning-data-science-process-hive-walkthrough.md#mltasks) , этот набор данных тоже поддается естественной классификации, если нам нужно спрогнозировать сумму выплачиваемых чаевых.</span><span class="sxs-lookup"><span data-stu-id="c006d-272">For the multiclass classification problem outlined in the [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself to a natural classification where we would like to predict the amount of the tips given.</span></span> <span data-ttu-id="c006d-273">Для определения диапазонов чаевых в запросе можно использовать ячейки.</span><span class="sxs-lookup"><span data-stu-id="c006d-273">We can use bins to define tip ranges in the query.</span></span> <span data-ttu-id="c006d-274">Для получения классовых распределений различных диапазонов чаевых мы используем файл *sample\_hive\_tip\_range\_frequencies.hql*.</span><span class="sxs-lookup"><span data-stu-id="c006d-274">To get the class distributions for the various tip ranges, we use the *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="c006d-275">Ниже приведено его содержимое.</span><span class="sxs-lookup"><span data-stu-id="c006d-275">Below are its contents.</span></span>

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

<span data-ttu-id="c006d-276">В консоли командной строки Hadoop выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-276">Run the following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="c006d-277">Исследование: вычисление расстояния по прямой между двумя местоположениями, заданными долготой и широтой</span><span class="sxs-lookup"><span data-stu-id="c006d-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-278">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-279">Наличие меры расстояния по прямой позволяет нам находить расхождение между ним и фактическим расстоянием поездки.</span><span class="sxs-lookup"><span data-stu-id="c006d-279">Having a measure of the direct distance allows us to find out the discrepancy between it and the actual trip distance.</span></span> <span data-ttu-id="c006d-280">Мы мотивируем использование этой характеристики тем, что пассажир с меньшей вероятностью выплатит чаевые, если определит, что водитель намеренно вез его намного более длинным маршрутом.</span><span class="sxs-lookup"><span data-stu-id="c006d-280">We motivate this feature by pointing out that a passenger might be less likely to tip if they figure out that the driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="c006d-281">Для просмотра сравнения между фактическим расстоянием поездки и [расстоянием гаверсинуса](http://en.wikipedia.org/wiki/Haversine_formula) между двумя точками долготы и широты (расстоянием по "большому кругу") мы используем доступные в Hive тригонометрические функции (результат см. ниже).</span><span class="sxs-lookup"><span data-stu-id="c006d-281">To see the comparison between actual trip distance and the [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (the "great circle" distance), we use the trigonometric functions available within Hive, thus :</span></span>

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

<span data-ttu-id="c006d-282">В приведенном выше запросе R — это радиус Земли в милях, а число пи (pi) преобразуется в радианы.</span><span class="sxs-lookup"><span data-stu-id="c006d-282">In the query above, R is the radius of the Earth in miles, and pi is converted to radians.</span></span> <span data-ttu-id="c006d-283">Обратите внимание, что точки долготы и широты «фильтруются» для удаления значений, расположенных далеко от региона Нью-Йорка.</span><span class="sxs-lookup"><span data-stu-id="c006d-283">Note that the longitude-latitude points are "filtered" to remove values that are far from the NYC area.</span></span>

<span data-ttu-id="c006d-284">В данном случае мы запишем результаты в каталог с именем «queryoutputdir».</span><span class="sxs-lookup"><span data-stu-id="c006d-284">In this case, we write our results to a directory called "queryoutputdir".</span></span> <span data-ttu-id="c006d-285">Последовательность команд, приведенных ниже, сначала создает этот выходной каталог, а затем выполняет команду Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-285">The sequence of commands shown below first creates this output directory, and then runs the Hive command.</span></span>

<span data-ttu-id="c006d-286">В командной строке каталога Hive выполните приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-286">From the Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="c006d-287">Результаты запроса записываются в 9 больших двоичных объектов Azure с ***queryoutputdir/000000\_0*** по ***queryoutputdir/000008\_0*** в используемом по умолчанию контейнере кластера Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c006d-287">The query results are written to 9 Azure blobs ***queryoutputdir/000000\_0*** to  ***queryoutputdir/000008\_0*** under the default container of the Hadoop cluster.</span></span>

<span data-ttu-id="c006d-288">Чтобы просмотреть размер отдельных больших двоичных объектов, мы выполняем приведенную ниже команду в командной строке каталога Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-288">To see the size of the individual blobs, we run the following command from the Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="c006d-289">Чтобы просмотреть содержимое заданного файла, скажем 000000\_0, мы используем команду Hadoop `copyToLocal` (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="c006d-289">To see the contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="c006d-290">`copyToLocal` может выполняться очень медленно для больших файлов, и использовать его с ними не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="c006d-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="c006d-291">Ключевое преимущество размещения этих данных в большом двоичном объекте Azure заключается в том, что мы можем исследовать данные в Машинном обучении Azure с помощью модуля [Импорт данных][import-data].</span><span class="sxs-lookup"><span data-stu-id="c006d-291">A key advantage of having this data reside in an Azure blob is that we may explore the data within Azure Machine Learning using the [Import Data][import-data] module.</span></span>

## <span data-ttu-id="c006d-292"><a name="#downsample"></a>Сокращение выборки и построение моделей в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="c006d-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="c006d-293">Обычно эту задачу выполняет **специалист по обработке и анализу данных** .</span><span class="sxs-lookup"><span data-stu-id="c006d-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="c006d-294">После исследовательской фазы анализа данных мы готовы к сокращению их выборки для построения моделей в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-294">After the exploratory data analysis phase, we are now ready to down sample the data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="c006d-295">В этом разделе мы покажем, как использовать запрос Hive для сокращения выборки данных, к которым затем будет обращаться модуль [Импорт данных][import-data] в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-295">In this section, we show how to use a Hive query to down sample the data, which is then accessed from the [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-the-data"></a><span data-ttu-id="c006d-296">Сокращение выборки данных</span><span class="sxs-lookup"><span data-stu-id="c006d-296">Down sampling the data</span></span>
<span data-ttu-id="c006d-297">Эта процедура состоит из двух шагов.</span><span class="sxs-lookup"><span data-stu-id="c006d-297">There are two steps in this procedure.</span></span> <span data-ttu-id="c006d-298">Сначала мы соединяем таблицы **nyctaxidb.trip** и **nyctaxidb.fare** по трем ключам, присутствующим во всех записях: medallion, hack\_license и pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="c006d-298">First we join the **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="c006d-299">Затем мы создаем метку двоичной классификации **tipped** и метку мультиклассовой классификации **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="c006d-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="c006d-300">Чтобы использовать данные сокращенной выборки непосредственно из модуля [Импорт данных][import-data] в Машинном обучении Azure, необходимо сохранить результаты приведенного выше запроса во внутренней таблице Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-300">To be able to use the down sampled data directly from the [Import Data][import-data] module in Azure Machine Learning, it is necessary to store the results of the above query to an internal Hive table.</span></span> <span data-ttu-id="c006d-301">В дальнейшем мы создаем внутреннюю таблицу Hive и заполняем ее содержимое объединенными данными с сокращенной выборкой.</span><span class="sxs-lookup"><span data-stu-id="c006d-301">In what follows, we create an internal Hive table and populate its contents with the joined and down sampled data.</span></span>

<span data-ttu-id="c006d-302">Запрос применяет стандартные функции Hive непосредственно для формирования часа дня, недели года, дня недели (1 — понедельник, 7 — воскресенье) из поля pickup\_datetime, а также расстояния по прямой между местоположениями посадки и высадки.</span><span class="sxs-lookup"><span data-stu-id="c006d-302">The query applies standard Hive functions directly to generate the hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from the "pickup\_datetime" field,  and the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="c006d-303">Полный список определяемых пользователем функций см. на странице [Руководство по языку: определяемые пользователем функций](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF).</span><span class="sxs-lookup"><span data-stu-id="c006d-303">Users can refer to [LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="c006d-304">Затем запрос сокращает выборку данных так, чтобы результаты запроса можно было загрузить в Студию машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-304">The query then down samples the data so that the query results can fit into the Azure Machine Learning Studio.</span></span> <span data-ttu-id="c006d-305">В студию импортируется только около 1 % исходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="c006d-305">Only about 1% of the original dataset is imported into the Studio.</span></span>

<span data-ttu-id="c006d-306">Ниже приведено содержимое файла *sample\_hive\_prepare\_for\_aml\_full.hql*, подготавливающего данные к построению моделей в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-306">Below are the contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

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

        --- now insert contents of the join into the above internal table

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

<span data-ttu-id="c006d-307">Выполнение этого запроса в командной строке каталога Hive.</span><span class="sxs-lookup"><span data-stu-id="c006d-307">To run this query, from the Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="c006d-308">Теперь у нас есть внутренняя таблица nyctaxidb.nyctaxi_downsampled_dataset, к которой можно получить доступ с помощью модуля [Импорт данных][import-data] в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using the [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="c006d-309">Кроме того, мы можем использовать этот набор данных для построения моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="c006d-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-the-import-data-module-in-azure-machine-learning-to-access-the-down-sampled-data"></a><span data-ttu-id="c006d-310">Использование модуля "Импорт данных" в Машинном обучении Azure для доступа к данным сокращенной выборки</span><span class="sxs-lookup"><span data-stu-id="c006d-310">Use the Import Data module in Azure Machine Learning to access the down sampled data</span></span>
<span data-ttu-id="c006d-311">В качестве предварительного условия для выполнения запросов Hive в модуле [Импорт данных][import-data] Машинного обучения Azure нам понадобится доступ к рабочей области Машинного обучения Azure, а также доступ к учетным данным кластера и связанной с ним учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c006d-311">As prerequisites for issuing Hive queries in the [Import Data][import-data] module of Azure Machine Learning, we need access to an Azure Machine Learning workspace and access to the credentials of the cluster and its associated storage account.</span></span>

<span data-ttu-id="c006d-312">Ниже приведены некоторые сведения о модуле [Импорт данных][import-data] и входных параметрах.</span><span class="sxs-lookup"><span data-stu-id="c006d-312">Some details on the [Import Data][import-data] module and the parameters to input :</span></span>

<span data-ttu-id="c006d-313">**URI сервера HCatalog**: если именем кластера является abc123, то это просто: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="c006d-313">**HCatalog server URI**: If the cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="c006d-314">**Имя учетной записи пользователя Hadoop**: имя пользователя, выбранное для кластера (**не** имя пользователя удаленного доступа)</span><span class="sxs-lookup"><span data-stu-id="c006d-314">**Hadoop user account name** : The user name chosen for the cluster (**not** the remote access user name)</span></span>

<span data-ttu-id="c006d-315">**Пароль учетной записи пользователя Hadoop**: пароль, выбранный для кластера (**не** пароль удаленного доступа)</span><span class="sxs-lookup"><span data-stu-id="c006d-315">**Hadoop ser account password** : The password chosen for the cluster (**not** the remote access password)</span></span>

<span data-ttu-id="c006d-316">**Расположение выходных данных** : этим расположением выбирается Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-316">**Location of output data** : This is chosen to be Azure.</span></span>

<span data-ttu-id="c006d-317">**Имя учетной записи хранения Azure** : имя учетной записи хранения по умолчанию, связанной с кластером.</span><span class="sxs-lookup"><span data-stu-id="c006d-317">**Azure storage account name** : Name of the default storage account associated with the cluster.</span></span>

<span data-ttu-id="c006d-318">**Имя контейнера Azure** : имя контейнера по умолчанию для кластера, которое обычно совпадает с именем кластера.</span><span class="sxs-lookup"><span data-stu-id="c006d-318">**Azure container name** : This is the default container name for the cluster, and is typically the same as the cluster name.</span></span> <span data-ttu-id="c006d-319">Для кластера с именем «abc123» это будет просто abc123.</span><span class="sxs-lookup"><span data-stu-id="c006d-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c006d-320">**Любая таблица, к которой нам требуется отправить запрос с помощью модуля [Импорт данных][import-data] в Машинном обучении Azure, должна быть внутренней таблицей.**</span><span class="sxs-lookup"><span data-stu-id="c006d-320">**Any table we wish to query using the [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="c006d-321">Определить, является ли таблица T в базе данных D.db внутренней таблицей, можно приведенным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="c006d-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="c006d-322">В командной строке каталога Hive выполните такую команду.</span><span class="sxs-lookup"><span data-stu-id="c006d-322">From the Hive directory prompt, issue the command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="c006d-323">Если таблица является внутренней и заполнена, ее содержимое должно отобразиться здесь.</span><span class="sxs-lookup"><span data-stu-id="c006d-323">If the table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="c006d-324">Другой способ определить, является ли таблица внутренней, — использовать обозреватель хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-324">Another way to determine whether a table is an internal table is to use the Azure Storage Explorer.</span></span> <span data-ttu-id="c006d-325">С его помощью перейдите к используемому по умолчанию имени контейнера кластера, а затем выполните фильтрацию по имени таблицы.</span><span class="sxs-lookup"><span data-stu-id="c006d-325">Use it to navigate to the default container name of the cluster, and then filter by the table name.</span></span> <span data-ttu-id="c006d-326">Если таблица и ее содержимое отображаются, это подтверждает, что таблица является внутренней.</span><span class="sxs-lookup"><span data-stu-id="c006d-326">If the table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="c006d-327">Ниже приведен моментальный снимок запроса Hive и модуля [Импорт данных][import-data].</span><span class="sxs-lookup"><span data-stu-id="c006d-327">Here is a snapshot of the Hive query and the [Import Data][import-data] module:</span></span>

![Запрос Hive для модуля "Импорт данных"](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="c006d-329">Обратите внимание, так как наши данные с сокращенной выборкой располагаются в контейнере по умолчанию, итоговый запрос Hive в машинном обучении Azure будет очень простым — "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span><span class="sxs-lookup"><span data-stu-id="c006d-329">Note that since our down sampled data resides in the default container, the resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="c006d-330">Теперь набор данных можно использовать в качестве отправной точки для построения моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="c006d-330">The dataset may now be used as the starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="c006d-331"><a name="mlmodel"></a>Построение моделей в компоненте машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="c006d-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="c006d-332">Теперь мы можем перейти к построению и развертыванию модели в [компоненте машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="c006d-332">We are now able to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="c006d-333">Данные готовы к использованию для решения задач прогнозирования, определенных выше.</span><span class="sxs-lookup"><span data-stu-id="c006d-333">The data is ready for us to use in addressing the prediction problems identified above:</span></span>

<span data-ttu-id="c006d-334">**1. Двоичная классификация**: спрогнозировать, были ли выплачены чаевые за поездку.</span><span class="sxs-lookup"><span data-stu-id="c006d-334">**1. Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="c006d-335">**Используемое средство обучения:** двухклассовая логистическая регрессия.</span><span class="sxs-lookup"><span data-stu-id="c006d-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="c006d-336">а.</span><span class="sxs-lookup"><span data-stu-id="c006d-336">a.</span></span> <span data-ttu-id="c006d-337">Для нашей задачи целевой меткой (меткой класса) будет «tipped» (чаевые выплачены).</span><span class="sxs-lookup"><span data-stu-id="c006d-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="c006d-338">В нашем исходном наборе данных с сокращенной выборкой есть несколько столбцов, содержащих целевые утечки сведений для данного эксперимента по классификации.</span><span class="sxs-lookup"><span data-stu-id="c006d-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="c006d-339">В частности, tip\_class, tip\_amount и total\_amount раскрывают информацию о целевой метке, которая недоступна во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="c006d-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="c006d-340">Мы удаляем эти столбцы из рассмотрения с помощью модуля [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных).</span><span class="sxs-lookup"><span data-stu-id="c006d-340">We remove these columns from consideration using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="c006d-341">На снимке ниже показан наш эксперимент по прогнозированию выплаты чаевых за данную поездку.</span><span class="sxs-lookup"><span data-stu-id="c006d-341">The snapshot below shows our experiment to predict whether or not a tip was paid for a given trip.</span></span>

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="c006d-343">b.</span><span class="sxs-lookup"><span data-stu-id="c006d-343">b.</span></span> <span data-ttu-id="c006d-344">Для этого эксперимента распределение наших целевых меток составляло примерно 1:1.</span><span class="sxs-lookup"><span data-stu-id="c006d-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="c006d-345">На снимке ниже показано распределение меток класса чаевых для задачи двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="c006d-345">The snapshot below shows the distribution of tip class labels for the binary classification problem.</span></span>

![Распределение меток класса чаевых](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="c006d-347">В результате мы получаем AUC величиной 0,987, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="c006d-347">As a result, we obtain an AUC of 0.987 as shown in the figure below.</span></span>

![Значение AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="c006d-349">**2. Мультиклассовая классификация**: прогнозирование диапазона сумм чаевых за поездку с использованием заранее определенных классов.</span><span class="sxs-lookup"><span data-stu-id="c006d-349">**2. Multiclass classification**: To predict the range of tip amounts paid for the trip, using the previously defined classes.</span></span>

<span data-ttu-id="c006d-350">**Используемое средство обучения:** мультиклассовая логистическая регрессия.</span><span class="sxs-lookup"><span data-stu-id="c006d-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="c006d-351">а.</span><span class="sxs-lookup"><span data-stu-id="c006d-351">a.</span></span> <span data-ttu-id="c006d-352">Для этой задачи нашей целевой меткой (меткой класса) будет tip\_class, которая может принимать одно из пяти значений (0, 1, 2, 3, 4).</span><span class="sxs-lookup"><span data-stu-id="c006d-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="c006d-353">Как и в случае двоичной классификации, у нас есть несколько столбцов с утечкой целевой информации для этого эксперимента.</span><span class="sxs-lookup"><span data-stu-id="c006d-353">As in the binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="c006d-354">В частности, tipped, tip\_amount и total\_amount раскрывают информацию о целевой метке, которая недоступна во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="c006d-354">In particular : tipped, tip\_amount, total\_amount reveal information about the target label that is not available at testing time.</span></span> <span data-ttu-id="c006d-355">Мы удаляем эти столбцы с помощью модуля [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных).</span><span class="sxs-lookup"><span data-stu-id="c006d-355">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="c006d-356">На снимке ниже показан наш эксперимент по прогнозированию ячейки, в которую вероятнее всего попадет сумма чаевых (класс 0: tip = $0, класс 1 : tip > $0 и tip <= $5, класс 2: tip > $5 и tip <= $10, класс 3: tip > $10 и tip <= $20, класс 4: tip > $20)</span><span class="sxs-lookup"><span data-stu-id="c006d-356">The snapshot below shows our experiment to predict in which bin a tip is likely to fall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="c006d-358">Теперь мы покажем, как выглядит наше фактическое тестовое классовое распределение.</span><span class="sxs-lookup"><span data-stu-id="c006d-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="c006d-359">Мы видим, что в то время как классы 0 и 1 являются наиболее распространенными, другие классы редки.</span><span class="sxs-lookup"><span data-stu-id="c006d-359">We see that while Class 0 and Class 1 are prevalent, the other classes are rare.</span></span>

![Тестовое классовое распределение](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="c006d-361">b.</span><span class="sxs-lookup"><span data-stu-id="c006d-361">b.</span></span> <span data-ttu-id="c006d-362">Для этого эксперимента мы используем матрицу неточностей для проверки точности наших прогнозов.</span><span class="sxs-lookup"><span data-stu-id="c006d-362">For this experiment, we use a confusion matrix to look at our prediction accuracies.</span></span> <span data-ttu-id="c006d-363">Такой способ показан ниже.</span><span class="sxs-lookup"><span data-stu-id="c006d-363">This is shown below.</span></span>

![Матрица неточностей](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="c006d-365">Обратите внимание, что при вполне неплохой точности для наиболее распространенных классов модель не особо хорошо «учится» на более редких классах.</span><span class="sxs-lookup"><span data-stu-id="c006d-365">Note that while our class accuracies on the prevalent classes is quite good, the model does not do a good job of "learning" on the rarer classes.</span></span>

<span data-ttu-id="c006d-366">**3. Задача регрессии**: спрогнозировать сумму чаевых, выплаченных за поездку.</span><span class="sxs-lookup"><span data-stu-id="c006d-366">**3. Regression task**: To predict the amount of tip paid for a trip.</span></span>

<span data-ttu-id="c006d-367">**Используемое средство обучения:** повышенное дерево принятия решений.</span><span class="sxs-lookup"><span data-stu-id="c006d-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="c006d-368">а.</span><span class="sxs-lookup"><span data-stu-id="c006d-368">a.</span></span> <span data-ttu-id="c006d-369">Для нашей задачи целевой меткой (меткой класса) будет "tip\_amount" (сумма чаевых).</span><span class="sxs-lookup"><span data-stu-id="c006d-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="c006d-370">Целевые утечки в данном случае: tipped, tip\_class, total\_amount. Все эти переменные раскрывают информацию о сумме чаевых, которая обычно недоступна во время тестирования.</span><span class="sxs-lookup"><span data-stu-id="c006d-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about the tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="c006d-371">Мы удаляем эти столбцы с помощью модуля [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных).</span><span class="sxs-lookup"><span data-stu-id="c006d-371">We remove these columns using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="c006d-372">На снимке ниже показан наш эксперимент по прогнозированию суммы выплаченных чаевых.</span><span class="sxs-lookup"><span data-stu-id="c006d-372">The snapshot belows shows our experiment to predict the amount of the given tip.</span></span>

![Моментальный снимок эксперимента](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="c006d-374">b.</span><span class="sxs-lookup"><span data-stu-id="c006d-374">b.</span></span> <span data-ttu-id="c006d-375">Для задач регрессии мы измеряем величины точности нашего прогноза, рассматривая квадратичную ошибку в прогнозах, коэффициент детерминации и тому подобное.</span><span class="sxs-lookup"><span data-stu-id="c006d-375">For regression problems, we measure the accuracies of our prediction by looking at the squared error in the predictions, the coefficient of determination, and the like.</span></span> <span data-ttu-id="c006d-376">Они показаны ниже.</span><span class="sxs-lookup"><span data-stu-id="c006d-376">We show these below.</span></span>

![Статистические данные прогноза](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="c006d-378">Мы видим, что коэффициент детерминации равен 0,709, что подразумевает, что коэффициенты нашей модели объясняют примерно 71% дисперсии.</span><span class="sxs-lookup"><span data-stu-id="c006d-378">We see that about the coefficient of determination is 0.709, implying about 71% of the variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c006d-379">Чтобы узнать больше о машинном обучении Azure, о доступе к машинному обучению и его использовании, см. статью [Введение в машинное обучение в облаке](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="c006d-379">To learn more about Azure Machine Learning and how to access and use it, please refer to [What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="c006d-380">Полезным ресурсом для экспериментов с машинным обучением Azure является [коллекция Cortana Intelligence](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="c006d-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="c006d-381">Коллекция охватывает спектр экспериментов и служит подробным введением в диапазон возможностей машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="c006d-381">The Gallery covers a gamut of experiments and provides a thorough introduction into the range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="c006d-382">Сведения о лицензии</span><span class="sxs-lookup"><span data-stu-id="c006d-382">License Information</span></span>
<span data-ttu-id="c006d-383">Доступ к этому учебнику и включенным в него скриптам предоставляет корпорация Майкрософт на основании лицензии свободного ПО.</span><span class="sxs-lookup"><span data-stu-id="c006d-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="c006d-384">Дополнительные сведения см. в файле LICENSE.txt в каталоге примеров кода на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="c006d-384">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="c006d-385">Ссылки</span><span class="sxs-lookup"><span data-stu-id="c006d-385">References</span></span>
<span data-ttu-id="c006d-386">•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="c006d-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="c006d-387">•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="c006d-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="c006d-388">•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="c006d-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
