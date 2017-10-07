---
title: "aaaBuild и развернуть модель машинного обучения, с помощью SQL Server на Виртуальной машине Azure | Документы Microsoft"
description: "Расширенный процесс аналитики и технологии в действии"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="704af-103">Hello командного процесса обработки и анализа данных в действии: с помощью SQL Server</span><span class="sxs-lookup"><span data-stu-id="704af-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="704af-104">В этом учебнике перемещайтесь hello процесс построения и развертывания модели машинного обучения с помощью SQL Server и общедоступным набор данных — hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных.</span><span class="sxs-lookup"><span data-stu-id="704af-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="704af-105">рабочий процесс обработки и анализа данных, ниже представлена процедура Hello: приема и исследовать данные hello, проектировать возможности toofacilitate обучения, а затем построения и развертывания модели.</span><span class="sxs-lookup"><span data-stu-id="704af-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="704af-106"><a name="dataset"></a>Описание набора данных "Поездки такси Нью-Йорка"</span><span class="sxs-lookup"><span data-stu-id="704af-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="704af-107">Hello Trip такси NYC данных составляет около 20 ГБ сжатые файлы CSV (~ 48 ГБ несжатого), включающего в себя более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута.</span><span class="sxs-lookup"><span data-stu-id="704af-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="704af-108">Каждая запись маршрута включает hello раскладки и истощение место и время, анонимные hack (драйвер) номер лицензии и medallion (уникальный идентификатор элемента такси) номер.</span><span class="sxs-lookup"><span data-stu-id="704af-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="704af-109">данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:</span><span class="sxs-lookup"><span data-stu-id="704af-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="704af-110">Hello «trip_data» CSV содержит обработки таких сведений, как количество пассажиров, раскладки и dropoff точек, длительность обработки и длина пути.</span><span class="sxs-lookup"><span data-stu-id="704af-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="704af-111">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="704af-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="704af-112">Здравствуйте, trip_fare CSV содержит подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты.</span><span class="sxs-lookup"><span data-stu-id="704af-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="704af-113">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="704af-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="704af-114">Hello trip уникальных ключей toojoin\_данных и обработки\_тариф авиакомпании состоит из полей hello: medallion hack\_лицензии и раскладки\_даты и времени.</span><span class="sxs-lookup"><span data-stu-id="704af-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="704af-115"><a name="mltasks"></a>Примеры задач прогнозирования</span><span class="sxs-lookup"><span data-stu-id="704af-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="704af-116">Мы сможет сформулировать три прогноза проблемы с учетом hello *совет\_сумма*, а именно:</span><span class="sxs-lookup"><span data-stu-id="704af-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="704af-117">Двоичная классификация. Позволяет спрогнозировать, были ли оставлены чаевые после поездки, т. е. значение *tip\_amount* > 0 $ — это положительный пример, а значение *tip\_amount* = 0 $ — отрицательный пример.</span><span class="sxs-lookup"><span data-stu-id="704af-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="704af-118">Мультиклассовая классификация: диапазон hello toopredict подсказки оплаты hello trip.</span><span class="sxs-lookup"><span data-stu-id="704af-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="704af-119">Разделен hello *совет\_сумма* в пять ячеек или классы:</span><span class="sxs-lookup"><span data-stu-id="704af-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="704af-120">Задача регрессии: оплачена сумма hello toopredict подсказки для маршрута.</span><span class="sxs-lookup"><span data-stu-id="704af-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="704af-121"><a name="setup"></a>Установка hello данных Azure обработки и анализа среды для расширенной аналитики</span><span class="sxs-lookup"><span data-stu-id="704af-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="704af-122">Как видно из hello [планирование среды](machine-learning-data-science-plan-your-environment.md) руководства, существует несколько вариантов toowork с набором данных приема-передачи такси NYC hello в Azure:</span><span class="sxs-lookup"><span data-stu-id="704af-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="704af-123">Работать с данным hello в BLOB-объекты Azure, а затем модель в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="704af-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="704af-124">Загрузка данных hello в базе данных SQL Server, а затем модель в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="704af-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="704af-125">В этом учебнике мы покажем, параллельный массовый импорт tooa hello данных SQL Server, просмотра данных, функция проектирование и работу выборки с помощью SQL Server Management Studio, а также с помощью ноутбук IPython.</span><span class="sxs-lookup"><span data-stu-id="704af-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="704af-126">[Примеры скриптов](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) и файлы [IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) предоставлены в общий доступ на GitHub.</span><span class="sxs-lookup"><span data-stu-id="704af-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="704af-127">Toowork записной книжки образец IPython с данными hello в BLOB-объекты Azure доступен также в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="704af-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="704af-128">tooset настройку среды обработки и анализа данных Azure:</span><span class="sxs-lookup"><span data-stu-id="704af-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="704af-129">создать учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="704af-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="704af-130">Создание рабочей области машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="704af-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="704af-131">[Подготовьте виртуальную машину для обработки и анализа данных](machine-learning-data-science-setup-sql-server-virtual-machine.md), которая будет служить сервером SQL Server и сервером IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="704af-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="704af-132">Примеры сценариев Hello и IPython Notebook будет загруженный tooyour обработки и анализа данных виртуальной машины во время процесса установки hello.</span><span class="sxs-lookup"><span data-stu-id="704af-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="704af-133">По завершении hello ВМ после установки скрипт hello образцы будут в библиотеке документов Виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="704af-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="704af-134">Примеры сценариев: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="704af-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="704af-135">Примеры IPython Notebook: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="704af-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="704af-136">where `<user_name>` является именем для входа Windows виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="704af-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="704af-137">Мы будем называть папки образца toohello **примеры сценариев** и **ноутбуков IPython пример**.</span><span class="sxs-lookup"><span data-stu-id="704af-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="704af-138">На основании hello размер набора данных, расположение источника данных и hello выбранного Azure целевой среды, этот случай похож слишком[сценарий \#5: больших наборов данных в локальных файлах, целевой сервер SQL Server в виртуальной Машине Azure](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="704af-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="704af-139"><a name="getdata"></a>Получить hello данных из открытых источника</span><span class="sxs-lookup"><span data-stu-id="704af-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="704af-140">tooget hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных из открытых расположения можно использовать любую из hello методов, описанных в [tooand перемещение данных из хранилища больших двоичных объектов](machine-learning-data-science-move-azure-blob.md) toocopy hello данных tooyour новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="704af-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="704af-141">toocopy hello данных с помощью AzCopy:</span><span class="sxs-lookup"><span data-stu-id="704af-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="704af-142">Войдите в tooyour виртуальной машины (VM)</span><span class="sxs-lookup"><span data-stu-id="704af-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="704af-143">Создать новый каталог в диска данных виртуальной Машины hello (Примечание: не используйте hello временного диска, который поставляется вместе с hello виртуальную Машину в качестве диска с данными).</span><span class="sxs-lookup"><span data-stu-id="704af-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="704af-144">В окне командной строки запустите hello следующей командной строкой Azcopy, заменив < path_to_data_folder > в папке данных, созданный на (2):</span><span class="sxs-lookup"><span data-stu-id="704af-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="704af-145">По завершении hello AzCopy всего 24 ZIP-файлы CSV (12 для обработки\_данных и 12 для обработки\_тариф авиакомпании) должны находиться в папке данных hello.</span><span class="sxs-lookup"><span data-stu-id="704af-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="704af-146">Распакуйте файлы загружаются hello.</span><span class="sxs-lookup"><span data-stu-id="704af-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="704af-147">Обратите внимание, hello папку, где находятся файлы сжимаются hello.</span><span class="sxs-lookup"><span data-stu-id="704af-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="704af-148">Эта папка будет ссылка tooas hello < путь\_для\_данные\_файлы\>.</span><span class="sxs-lookup"><span data-stu-id="704af-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="704af-149"><a name="dbload"></a>Выполните массовый импорт данных в базу данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="704af-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="704af-150">Hello производительности передачи или загрузки больших объемов данных базы данных SQL tooan и последующие запросы, может быть повышена путем использования *секционированных таблиц и представлений*.</span><span class="sxs-lookup"><span data-stu-id="704af-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="704af-151">В этом разделе мы будем следовать hello инструкциям, описанным в [параллельного массового импорта с помощью SQL секционирования таблиц данных](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate новой базы данных и загрузки данных hello в секционированные таблицы в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="704af-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="704af-152">Войдя в систему tooyour виртуальных Машин, запустите **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="704af-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="704af-153">Подключитесь с использованием проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="704af-153">Connect using Windows Authentication.</span></span>
   
    ![Подключение SSMS][12]
3. <span data-ttu-id="704af-155">Если вы еще не изменить режим проверки подлинности SQL Server hello и создать новое имя входа пользователя SQL, откройте файл скрипта hello с именем **изменить\_auth.sql** в hello **примеры сценариев** папки.</span><span class="sxs-lookup"><span data-stu-id="704af-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="704af-156">Изменение hello по умолчанию имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="704af-156">Change hello  default user name and password.</span></span> <span data-ttu-id="704af-157">Нажмите кнопку **! Выполнение** в скрипте hello toorun инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="704af-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Выполнение сценария][13]
4. <span data-ttu-id="704af-159">Проверка или изменение hello SQL Server по умолчанию базы данных и журнала папки tooensure, вновь создаваемых баз данных сохраняются на диск с данными.</span><span class="sxs-lookup"><span data-stu-id="704af-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="704af-160">образ виртуальной Машины SQL Server Hello, оптимизированный для загрузки datawarehousing предварительно настраивается с дисками данных и журналов.</span><span class="sxs-lookup"><span data-stu-id="704af-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="704af-161">Если ВМ не содержит диск данных, и добавление новых виртуальных жестких дисков во время hello процесс установки виртуальной Машины, измените папки по умолчанию hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="704af-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="704af-162">Щелкните правой кнопкой мыши имя сервера SQL Server hello в hello слева панели и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="704af-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![Свойства сервера SQL][14]
   * <span data-ttu-id="704af-164">Выберите **параметры базы данных** из hello **Выбор страницы** списка toohello влево.</span><span class="sxs-lookup"><span data-stu-id="704af-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="704af-165">Проверьте или измените hello **базы данных по умолчанию расположений** toohello **диск данных** расположения по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="704af-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="704af-166">Это местоположение новых баз данных, если при создании параметры расположения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="704af-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![База данных SQL по умолчанию][15]  
5. <span data-ttu-id="704af-168">toocreate новую базу данных и набор toohold файловые группы hello секционированных таблиц, откройте образец скрипта hello **создания\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="704af-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="704af-169">Hello скрипт создает новую базу данных с именем **TaxiNYC** и 12 файловых групп в расположении данных по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="704af-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="704af-170">Каждая файловая группа будет содержать данные trip\_data и trip\_fare за один месяц.</span><span class="sxs-lookup"><span data-stu-id="704af-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="704af-171">Измените имя базы данных hello, если требуется.</span><span class="sxs-lookup"><span data-stu-id="704af-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="704af-172">Нажмите кнопку **! Выполнение** toorun hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="704af-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="704af-173">Создайте две секции таблицы, один для обработки hello\_данных и другой для обработки hello\_тариф авиакомпании.</span><span class="sxs-lookup"><span data-stu-id="704af-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="704af-174">Откройте образец скрипта hello **создания\_секционированных\_table.sql**, которой будет:</span><span class="sxs-lookup"><span data-stu-id="704af-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="704af-175">Создание данных hello toosplit функции секционирования по месяцам.</span><span class="sxs-lookup"><span data-stu-id="704af-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="704af-176">Создайте схему секционирования toomap данных каждого месяца tooa другую файловую группу.</span><span class="sxs-lookup"><span data-stu-id="704af-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="704af-177">Создать схему секционирования сопоставленных toohello два секционированных таблиц: **nyctaxi\_trip** будет содержать hello trip\_данных и **nyctaxi\_тариф авиакомпании** будет содержать hello trip \_успешного данных.</span><span class="sxs-lookup"><span data-stu-id="704af-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="704af-178">Нажмите кнопку **! Выполнение** toorun hello скрипта и создания hello секционированных таблиц.</span><span class="sxs-lookup"><span data-stu-id="704af-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="704af-179">В hello **примеры сценариев** папке, есть два примера скриптов PowerShell предоставленный toodemonstrate параллельный массовый импорт данных tooSQL Server таблиц.</span><span class="sxs-lookup"><span data-stu-id="704af-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="704af-180">**BCP\_параллельных\_generic.ps1** является Универсальный сценарий tooparallel массового импорта данных в таблицу.</span><span class="sxs-lookup"><span data-stu-id="704af-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="704af-181">Изменение этого сценария tooset hello входных данных и целевой переменных как указано в hello строки комментариев в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="704af-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="704af-182">**BCP\_параллельных\_nyctaxi.ps1** имеет предварительно настроенную версию универсального сценария hello и может принимать используется tootooload обе таблицы для hello NYC такси приема-передачи данных.</span><span class="sxs-lookup"><span data-stu-id="704af-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="704af-183">Щелкните правой кнопкой мыши hello **bcp\_параллельных\_nyctaxi.ps1** имя скрипта и нажмите кнопку **изменить** tooopen в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="704af-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="704af-184">Просмотрите hello предустановленный набор переменных и изменить имя выбранной базы данных соответствующим tooyour, папка входных данных, целевую папку журнала и пути toohello образцы файлов форматирования **nyctaxi_trip.xml** и **nyctaxi\_ fare.XML** (в hello **примеры сценариев** папки).</span><span class="sxs-lookup"><span data-stu-id="704af-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Массовый импорт данных][16]
   
    <span data-ttu-id="704af-186">Можно также выбрать режим проверки подлинности hello, по умолчанию используется проверка подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="704af-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="704af-187">Нажмите стрелку зеленый hello в toorun инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="704af-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="704af-188">сценарий Hello запустит 24 операций массового импорта в параллельных, 12 для каждой секционированной таблицы.</span><span class="sxs-lookup"><span data-stu-id="704af-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="704af-189">Может отслеживать ход выполнения импорта данных hello путем открытия папки данных по умолчанию hello SQL Server как набор выше.</span><span class="sxs-lookup"><span data-stu-id="704af-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="704af-190">отчеты сценария PowerShell Hello hello времени начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="704af-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="704af-191">При всех массового импорта завершения, сообщается hello времени окончания.</span><span class="sxs-lookup"><span data-stu-id="704af-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="704af-192">Проверьте hello журнала целевой папки tooverify, массовый импорт hello выполнено успешно, т. е., ошибки не обнаружены в папке журналов целевой hello.</span><span class="sxs-lookup"><span data-stu-id="704af-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="704af-193">Теперь база данных готова к просмотру, проектированию характеристик и другим операциям.</span><span class="sxs-lookup"><span data-stu-id="704af-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="704af-194">Поскольку hello таблиц секционируются в соответствии с toohello **раскладки\_datetime** поле запросы, включающие **раскладки\_datetime** условия в hello  **ГДЕ** предложение будет обеспечен hello схемы секционирования.</span><span class="sxs-lookup"><span data-stu-id="704af-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="704af-195">В **SQL Server Management Studio**, исследовать hello предоставленный пример сценария **пример\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="704af-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="704af-196">toorun любой из запросов образец hello, hello выделение строки запроса, затем щелкните **! Выполнение** инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="704af-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="704af-197">загружаются Hello NYC такси приема-передачи данных в двух отдельных таблицах.</span><span class="sxs-lookup"><span data-stu-id="704af-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="704af-198">tooimprove операций соединения, настоятельно рекомендуется tooindex hello таблиц.</span><span class="sxs-lookup"><span data-stu-id="704af-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="704af-199">Hello пример сценария **создания\_секционированных\_index.sql** создает секционированные индексы для ключа составным hello **medallion hack\_лицензии и раскладки\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="704af-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="704af-200"><a name="dbexplore"></a>Просмотр данных и проектирование характеристик в SQL Server</span><span class="sxs-lookup"><span data-stu-id="704af-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="704af-201">В этом разделе мы выполним возможности просмотра и создания данных с помощью запросов SQL непосредственно в hello **SQL Server Management Studio** hello базы данных SQL Server с помощью созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="704af-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="704af-202">Пример сценария с именем **пример\_queries.sql** предоставляется в hello **примеры сценариев** папки.</span><span class="sxs-lookup"><span data-stu-id="704af-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="704af-203">Изменить имя базы данных hello toochange сценария hello, если он отличается от значения по умолчанию hello: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="704af-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="704af-204">В этом упражнении мы выполним такие действия.</span><span class="sxs-lookup"><span data-stu-id="704af-204">In this exercise, we will:</span></span>

* <span data-ttu-id="704af-205">Подключение слишком**SQL Server Management Studio** используется проверка подлинности Windows или проверки подлинности SQL и hello имени входа SQL и пароля.</span><span class="sxs-lookup"><span data-stu-id="704af-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="704af-206">Просмотрим распределение данных по нескольким полям в различных временных окнах.</span><span class="sxs-lookup"><span data-stu-id="704af-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="704af-207">Проверка качества данных полей hello широты и долготы.</span><span class="sxs-lookup"><span data-stu-id="704af-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="704af-208">Создание двоичного и мультиклассовой классификации меток, основываясь на hello **совет\_сумма**.</span><span class="sxs-lookup"><span data-stu-id="704af-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="704af-209">Создадим характеристики и вычислим/сравним расстояния поездок.</span><span class="sxs-lookup"><span data-stu-id="704af-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="704af-210">Объединение hello двух таблиц и извлеките случайную выборку, который будет использоваться toobuild моделей.</span><span class="sxs-lookup"><span data-stu-id="704af-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="704af-211">Когда вы будете готовы tooproceed tooAzure машинного обучения, можно либо:</span><span class="sxs-lookup"><span data-stu-id="704af-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="704af-212">Сохранить hello окончательного SQL запроса tooextract и образец hello данных и копирования и вставки hello запрос непосредственно в [импорта данных] [ import-data] в машинном обучении Azure, или</span><span class="sxs-lookup"><span data-stu-id="704af-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="704af-213">Сохранять hello выборки и социотехники данных планируется toouse для построения в новую базу данных модели и использовать новую таблицу hello в hello [импорта данных] [ import-data] модуль в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="704af-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="704af-214">В этом разделе мы сохранит hello окончательный запрос tooextract и образец hello данных.</span><span class="sxs-lookup"><span data-stu-id="704af-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="704af-215">Второй метод Hello демонстрируется hello [исследование данных и разработки компонентов в записной книжке IPython](#ipnb) раздела.</span><span class="sxs-lookup"><span data-stu-id="704af-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="704af-216">Для быстрой проверки количества строк и столбцов в hello hello таблиц заполняется ранее с помощью параллельный массовый импорт</span><span class="sxs-lookup"><span data-stu-id="704af-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="704af-217">Просмотр: Распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="704af-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="704af-218">В этом примере определяет medallion hello (номера такси) с более чем 100 приема-передачи данных в течение заданного периода времени.</span><span class="sxs-lookup"><span data-stu-id="704af-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="704af-219">запрос Hello получают преимущества от доступа hello секционированные таблицы с момента обусловлено схему секционирования hello **раскладки\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="704af-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="704af-220">Запрос hello полного набора данных следует использовать hello секционированные таблицы и/или сканирование индекса.</span><span class="sxs-lookup"><span data-stu-id="704af-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="704af-221">Просмотр: распределение поездок по параметрам medallion и hack_license</span><span class="sxs-lookup"><span data-stu-id="704af-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="704af-222">Оценка качества данных: Проверка записей с неверными значениями долготы и/или широты</span><span class="sxs-lookup"><span data-stu-id="704af-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="704af-223">В этом примере анализируется, если любая из поля долготы и широты hello либо содержит недопустимое значение (градусов в радианах должно быть от -90 до 90), или иметь (0, 0) координаты.</span><span class="sxs-lookup"><span data-stu-id="704af-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="704af-224">Просмотр: Выплаченные чаевые против Распределение поездок с чаевыми и без чаевых</span><span class="sxs-lookup"><span data-stu-id="704af-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="704af-225">Этот пример возвращает числовой hello приема-передачи, которые были чаевых оставил зависимости и не чаевых оставил зависимости в определенный момент времени периода (или hello полного набора данных Если охватывающие hello полный год).</span><span class="sxs-lookup"><span data-stu-id="704af-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="704af-226">Это распределение отражает hello двоичных метки распространения toobe впоследствии использовать для моделирования двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="704af-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="704af-227">Просмотр: распределение классов/диапазонов чаевых</span><span class="sxs-lookup"><span data-stu-id="704af-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="704af-228">Этот пример вычисляет распределение hello диапазоны подсказки в определенный момент времени периода (или hello полного набора данных Если охватывающие hello полный год).</span><span class="sxs-lookup"><span data-stu-id="704af-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="704af-229">Это распределение hello hello метки классы, которые будут использоваться позже для моделирования мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="704af-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="704af-230">Просмотр: Вычисление и сравнение расстояния поездок</span><span class="sxs-lookup"><span data-stu-id="704af-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="704af-231">Этот пример преобразует hello раскладки и истощение долготы и широты tooSQL geography указывает, вычисляет расстояние trip hello, с помощью точек различие SQL geography и возвращает случайную выборку hello результатов для сравнения.</span><span class="sxs-lookup"><span data-stu-id="704af-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="704af-232">пример Hello ограничивает результаты hello, координирует toovalid только с помощью hello качества данных оценки запроса, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="704af-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="704af-233">Проектирование характеристик в запросах SQL</span><span class="sxs-lookup"><span data-stu-id="704af-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="704af-234">Hello метки поколения geography преобразования просмотра запросов и также может быть используется toogenerate метки или компоненты, удалив подсчета часть hello.</span><span class="sxs-lookup"><span data-stu-id="704af-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="704af-235">Дополнительные функции проектирования SQL приведены примеры в hello [исследование данных и разработки компонентов в записной книжке IPython](#ipnb) раздела.</span><span class="sxs-lookup"><span data-stu-id="704af-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="704af-236">Это более эффективные запросы toorun hello возможность формирования на hello полного набора данных или подмножества его с помощью SQL-запросов, которые выполняются непосредственно в экземпляре базы данных SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="704af-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="704af-237">Hello запросы могут производиться в **SQL Server Management Studio**, ноутбук IPython или любого средства и среда разработки доступ к которому hello базы данных, локально или удаленно.</span><span class="sxs-lookup"><span data-stu-id="704af-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="704af-238">Подготовка данных для построения модели</span><span class="sxs-lookup"><span data-stu-id="704af-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="704af-239">Hello следующий запрос соединения hello **nyctaxi\_trip** и **nyctaxi\_тариф авиакомпании** таблицы, приводит к возникновению ошибки двоичной классификации метки **чаевых оставил зависимости**, Метка многоклассовый классификатор **совет\_класса**и извлекает из полного объединенном наборе данных hello случайной выборки 1%.</span><span class="sxs-lookup"><span data-stu-id="704af-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="704af-240">Этот запрос можно скопировать, затем вставить непосредственно в hello [студии машинного обучения Azure](https://studio.azureml.net) [импорта данных] [ import-data] модуль для приема прямой данных из базы данных SQL Server hello экземпляр в Azure.</span><span class="sxs-lookup"><span data-stu-id="704af-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="704af-241">запрос Hello исключает записи с неверным (0, 0) координаты.</span><span class="sxs-lookup"><span data-stu-id="704af-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="704af-242"><a name="ipnb"></a>Просмотр данных и проектирование характеристик в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="704af-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="704af-243">В этом разделе мы выполним исследование данных и создание функции, с помощью запросов Python и SQL для базы данных SQL Server hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="704af-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="704af-244">Образец ноутбук IPython с именем **machine-Learning-data-science-process-sql-story.ipynb** предоставляется в hello **ноутбуков IPython пример** папки.</span><span class="sxs-lookup"><span data-stu-id="704af-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="704af-245">Этот файл также доступен на [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="704af-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="704af-246">Привет, рекомендуется последовательность при работе с большими данными необходимо hello в следующем:</span><span class="sxs-lookup"><span data-stu-id="704af-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="704af-247">Чтение в небольшую выборку данных hello в кадр данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="704af-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="704af-248">Выполните некоторые визуализации и исследования с помощью hello выборки данных.</span><span class="sxs-lookup"><span data-stu-id="704af-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="704af-249">Поэкспериментируйте с помощью hello конструируются выборке данных.</span><span class="sxs-lookup"><span data-stu-id="704af-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="704af-250">Для просмотра данных большего размера обработку данных и конструируются, использовать tooissue Python SQL-запросы непосредственно к базе данных SQL Server hello в hello виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="704af-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="704af-251">Решите, toouse размер образца hello для построения модели машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="704af-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="704af-252">Окончании tooproceed tooAzure машинного обучения, вы можете либо:</span><span class="sxs-lookup"><span data-stu-id="704af-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="704af-253">Сохранить hello окончательного SQL запроса tooextract и образец hello данных и копирования и вставки hello запрос непосредственно в [импорта данных] [ import-data] модуль в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="704af-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="704af-254">Этот метод, представленный в hello [построение моделей в машинном обучении Azure](#mlmodel) раздела.</span><span class="sxs-lookup"><span data-stu-id="704af-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="704af-255">Hello выборки и сохранялись социотехники планирование toouse для построения таблицы базы данных модели, а затем использовать новую таблицу hello в hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="704af-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="704af-256">Hello ниже приведены несколько исследования данных, визуализация данных и проектирование примеры компонентов.</span><span class="sxs-lookup"><span data-stu-id="704af-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="704af-257">Дополнительные примеры см. в разделе ноутбук SQL IPython образец hello в hello **ноутбуков IPython пример** папки.</span><span class="sxs-lookup"><span data-stu-id="704af-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="704af-258">Инициализация учетных данных базы данных</span><span class="sxs-lookup"><span data-stu-id="704af-258">Initialize Database Credentials</span></span>
<span data-ttu-id="704af-259">Инициализируйте параметры подключения к базе данных в hello следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="704af-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="704af-260">Создание подключения к базе данных</span><span class="sxs-lookup"><span data-stu-id="704af-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="704af-261">Сообщение числа строк и столбцов в таблице nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="704af-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="704af-262">Общее число строк = 173179759</span><span class="sxs-lookup"><span data-stu-id="704af-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="704af-263">Общее число столбцов = 14</span><span class="sxs-lookup"><span data-stu-id="704af-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="704af-264">Чтение в образец небольшой данных из базы данных SQL Server hello</span><span class="sxs-lookup"><span data-stu-id="704af-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="704af-265">Время tooread hello образец таблицы — 6.492000 секунд</span><span class="sxs-lookup"><span data-stu-id="704af-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="704af-266">Число извлеченных строк и столбцов = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="704af-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="704af-267">Описательная статистика</span><span class="sxs-lookup"><span data-stu-id="704af-267">Descriptive Statistics</span></span>
<span data-ttu-id="704af-268">Теперь все готово tooexplore hello выборки данных.</span><span class="sxs-lookup"><span data-stu-id="704af-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="704af-269">Мы начнем с рассмотрения Описательная статистика для hello **trip\_расстояние** (или любой другой) полей:</span><span class="sxs-lookup"><span data-stu-id="704af-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="704af-270">Визуализация: Пример блочной диаграммы</span><span class="sxs-lookup"><span data-stu-id="704af-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="704af-271">Теперь рассмотрим hello Блочная для hello trip расстояние toovisualize hello квантилей</span><span class="sxs-lookup"><span data-stu-id="704af-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![График #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="704af-273">Визуализация: Пример графика распределения</span><span class="sxs-lookup"><span data-stu-id="704af-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![График #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="704af-275">Визуализация: Гистограммы и линейные графики</span><span class="sxs-lookup"><span data-stu-id="704af-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="704af-276">В этом примере мы bin расстояние trip hello в пять ячеек и визуализировать hello группирование результатов.</span><span class="sxs-lookup"><span data-stu-id="704af-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="704af-277">Мы построения hello выше распространения ячейки в строку или строки построения, как показано ниже</span><span class="sxs-lookup"><span data-stu-id="704af-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![График #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![График #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="704af-280">Визуализация: Пример точечной диаграммы</span><span class="sxs-lookup"><span data-stu-id="704af-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="704af-281">Мы покажем точечной диаграммы между **trip\_время\_в\_сек** и **trip\_расстояние** toosee при наличии корреляции</span><span class="sxs-lookup"><span data-stu-id="704af-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![График #6][6]

<span data-ttu-id="704af-283">Аналогичным образом можно проверить hello связь между **скорость\_кода** и **trip\_расстояние**.</span><span class="sxs-lookup"><span data-stu-id="704af-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![График #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="704af-285">Hello вложенных выборки данных в SQL</span><span class="sxs-lookup"><span data-stu-id="704af-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="704af-286">При подготовке данных для построения модели [студии машинного обучения Azure](https://studio.azureml.net), либо можно на hello **toouse запроса SQL непосредственно в модуль импорта данных hello** или сохранить hello разработан и выборки данные в новую таблицу, которая может использоваться при hello [импорта данных] [ import-data] модуля с помощью простого **ВЫБЕРИТЕ * FROM < ваш\_новый\_таблицы\_имя >**.</span><span class="sxs-lookup"><span data-stu-id="704af-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="704af-287">В этом разделе мы создадим новый hello toohold таблицу выборки и разработан данных.</span><span class="sxs-lookup"><span data-stu-id="704af-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="704af-288">Приводятся примеры прямых запросов SQL для построения модели в hello [Engineering функции в SQL Server и просмотра данных](#dbexplore) раздела.</span><span class="sxs-lookup"><span data-stu-id="704af-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="704af-289">Создайте образец таблицы и заполнить с % 1, hello объединить таблиц.</span><span class="sxs-lookup"><span data-stu-id="704af-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="704af-290">Сначала удалите таблицу, если она существует.</span><span class="sxs-lookup"><span data-stu-id="704af-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="704af-291">В этом разделе мы соединения таблиц hello **nyctaxi\_trip** и **nyctaxi\_тариф авиакомпании**, извлечь случайной выборки 1%, и сохранения данных выборки hello в новое имя таблицы  **nyctaxi\_один\_процентов**:</span><span class="sxs-lookup"><span data-stu-id="704af-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="704af-292">Просмотр данных с помощью SQL-запросов в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="704af-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="704af-293">В этом разделе мы исследуем распределения данных с использованием данных hello выборки % 1, который сохраняется в новой таблице hello, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="704af-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="704af-294">Обратите внимание, что аналогично просмотров может осуществляться с помощью hello исходных таблиц, при необходимости используя **TABLESAMPLE** tooa данный период времени с помощью hello результаты просмотра hello toolimit, образец или ограничивая hello **раскладки \_datetime** секции, как показано в hello [Engineering функции в SQL Server и просмотра данных](#dbexplore) раздела.</span><span class="sxs-lookup"><span data-stu-id="704af-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="704af-295">Исследование: ежедневное распределение поездок</span><span class="sxs-lookup"><span data-stu-id="704af-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="704af-296">Исследование: распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="704af-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="704af-297">Создание характеристик с помощью SQL-запросов в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="704af-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="704af-298">В этом разделе мы создадим новые метки и компонентов непосредственно с использованием SQL-запросов, на 1% Образец таблицы hello созданную в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="704af-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="704af-299">Создание метки: Создать метки классов</span><span class="sxs-lookup"><span data-stu-id="704af-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="704af-300">В следующем примере hello мы создаем два набора toouse метки для моделирования:</span><span class="sxs-lookup"><span data-stu-id="704af-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="704af-301">Метки двоичной классификации **tipped** (прогнозирование, будут ли выплачены чаевые).</span><span class="sxs-lookup"><span data-stu-id="704af-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="704af-302">Метки мультиклассовой **совет\_класс** (прогнозирование hello совет bin или диапазона)</span><span class="sxs-lookup"><span data-stu-id="704af-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="704af-303">Проектирование характеристик: Количественные характеристики для столбцов категорий</span><span class="sxs-lookup"><span data-stu-id="704af-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="704af-304">Этот пример преобразует поле категории в числовое поле, заменяя hello число вхождений в данных hello каждой категории.</span><span class="sxs-lookup"><span data-stu-id="704af-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="704af-305">Проектирование характеристик: Ячейка характеристик для числовых столбцов</span><span class="sxs-lookup"><span data-stu-id="704af-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="704af-306">Этот пример преобразует непрерывное числовое поле в предустановленные диапазоны категорий, т. е. преобразует числовое поле в поле категории.</span><span class="sxs-lookup"><span data-stu-id="704af-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="704af-307">Проектирование характеристик: Извлечение характеристик местоположения из десятичных значений широты/долготы</span><span class="sxs-lookup"><span data-stu-id="704af-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="704af-308">В этом примере разбивает hello десятичное представление поля широты и долготы в нескольких полей области с различной степенью детализации, например, страны, города, города, блок, и т. д. Обратите внимание, что новый hello geo поля не сопоставлены tooactual расположения.</span><span class="sxs-lookup"><span data-stu-id="704af-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="704af-309">Дополнительные сведения о сопоставлении местоположений геокодов см. в статье о [службах REST карт Bing](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="704af-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="704af-310">Проверьте hello конечная форма hello признак таблицы</span><span class="sxs-lookup"><span data-stu-id="704af-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="704af-311">Мы стали готовы tooproceed toomodel построение и развертывание модели в [машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="704af-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="704af-312">Hello данных готов для hello прогноза причинами, описанных выше, а именно:</span><span class="sxs-lookup"><span data-stu-id="704af-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="704af-313">Двоичная классификация: toopredict ли уплаченной Совет для маршрута.</span><span class="sxs-lookup"><span data-stu-id="704af-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="704af-314">Мультиклассовая классификация: диапазон hello toopredict совета оплачен, в соответствии с toohello ранее определенных классов.</span><span class="sxs-lookup"><span data-stu-id="704af-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="704af-315">Задача регрессии: оплачена сумма hello toopredict подсказки для маршрута.</span><span class="sxs-lookup"><span data-stu-id="704af-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="704af-316"><a name="mlmodel"></a>Построение моделей в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="704af-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="704af-317">toobegin hello моделирования упражнения журнала в рабочей области машинного обучения Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="704af-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="704af-318">Если вы еще не создали рабочую область машинного обучения, см. статью [Создание рабочей области машинного обучения Azure и предоставление к ней общего доступа](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="704af-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="704af-319">tooget к выполнению машинного обучения Azure в разделе [возможности студии машинного обучения Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="704af-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="704af-320">Войдите в слишком[студии машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="704af-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="704af-321">Hello Studio домашней странице предоставляет широкий набор сведений, видео, учебники, ссылки toohello Справочник по модулям и другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="704af-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="704af-322">Дополнительные сведения о машинного обучения Azure обратитесь к hello [центр документации машинного обучения Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="704af-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="704af-323">Эксперимента обучения обычно состоит из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="704af-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="704af-324">Создать **+НОВЫЙ** эксперимент.</span><span class="sxs-lookup"><span data-stu-id="704af-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="704af-325">Получение данных hello tooAzure машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="704af-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="704af-326">Предварительно обработать, преобразование данных и управления ими hello при необходимости.</span><span class="sxs-lookup"><span data-stu-id="704af-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="704af-327">Создать необходимые характеристики.</span><span class="sxs-lookup"><span data-stu-id="704af-327">Generate features as needed.</span></span>
5. <span data-ttu-id="704af-328">Разбиение данных hello в набор данных, обучения и проверки и тестирования (или иметь отдельный набор данных для каждого).</span><span class="sxs-lookup"><span data-stu-id="704af-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="704af-329">Выберите один или несколько алгоритмов машинного обучения в зависимости от hello обучения toosolve проблему.</span><span class="sxs-lookup"><span data-stu-id="704af-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="704af-330">Например, двоичная классификация, мультиклассовая классификация, регрессия.</span><span class="sxs-lookup"><span data-stu-id="704af-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="704af-331">Обучение одной или нескольких моделей с помощью hello обучающий набор данных.</span><span class="sxs-lookup"><span data-stu-id="704af-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="704af-332">Оценка hello проверочного набора данных с помощью обученной модели hello.</span><span class="sxs-lookup"><span data-stu-id="704af-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="704af-333">Оцените hello модели toocompute hello соответствующие метрики для изучения проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="704af-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="704af-334">Настройка модели hello и выберите hello наиболее toodeploy модели.</span><span class="sxs-lookup"><span data-stu-id="704af-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="704af-335">В этом упражнении мы уже изучена разработан hello данных в SQL Server и решили tooingest размер образца hello в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="704af-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="704af-336">toobuild один или несколько моделей прогнозирования hello мы решили:</span><span class="sxs-lookup"><span data-stu-id="704af-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="704af-337">Получение данных hello tooAzure машинного обучения с помощью hello [импорта данных] [ import-data] модуля, доступные в hello **ввод и вывод данных** раздела.</span><span class="sxs-lookup"><span data-stu-id="704af-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="704af-338">Дополнительные сведения см. в разделе hello [импорта данных] [ import-data] справочной странице модуля.</span><span class="sxs-lookup"><span data-stu-id="704af-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Импорт данных в Машинное обучение Azure][17]
2. <span data-ttu-id="704af-340">Выберите **базы данных SQL Azure** как hello **источника данных** в hello **свойства** панель.</span><span class="sxs-lookup"><span data-stu-id="704af-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="704af-341">Введите имя DNS hello базы данных в hello **имя сервера базы данных** поля.</span><span class="sxs-lookup"><span data-stu-id="704af-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="704af-342">Формат: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="704af-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="704af-343">Введите hello **имя базы данных** в соответствующее поле hello.</span><span class="sxs-lookup"><span data-stu-id="704af-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="704af-344">Введите hello **имя пользователя SQL** в hello ** aqccount имени пользователя и пароль hello в hello **пароль учетной записи пользователя сервера**.</span><span class="sxs-lookup"><span data-stu-id="704af-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="704af-345">Установите флажок **Принимать любой сертификат сервера** .</span><span class="sxs-lookup"><span data-stu-id="704af-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="704af-346">В hello **запроса базы данных** Измените текстовое поле, вставьте запрос hello какие извлекает hello необходимые поля (включая все вычисляемые поля, такие как метки hello) базы данных и вниз образцы размер выборки toohello требуемого hello данных.</span><span class="sxs-lookup"><span data-stu-id="704af-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="704af-347">Примером бинарной классификации эксперимент, чтение данных непосредственно из базы данных SQL Server hello является hello рис. ниже.</span><span class="sxs-lookup"><span data-stu-id="704af-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="704af-348">Подобные эксперименты можно сконструировать для задач мультиклассовой классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="704af-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Обучение моделей Машинного обучения Azure][10]

> [!IMPORTANT]
> <span data-ttu-id="704af-350">В hello моделирования данных по извлечению и выборки запроса примеры, приведенные в предыдущих разделах **все метки для моделирования упражнений hello трех включаются в запрос hello**.</span><span class="sxs-lookup"><span data-stu-id="704af-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="704af-351">(Обязательный) в каждом hello моделирования упражнения важно слишком**исключить** hello ненужные метки для hello другие две проблемы и любые другие **целевой утечки**.</span><span class="sxs-lookup"><span data-stu-id="704af-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="704af-352">Для например, при использовании двоичной классификации, используйте метки hello **чаевых оставил зависимости** и исключить hello поля **совет\_класса**, **совет\_сумма**, и **общее\_сумма**.</span><span class="sxs-lookup"><span data-stu-id="704af-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="704af-353">последний Hello оплачиваются утечки целевой, так как они предполагают совет hello.</span><span class="sxs-lookup"><span data-stu-id="704af-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="704af-354">tooexclude ненужных столбцов и/или целевой утечки, можно использовать hello [Выбор столбцов в наборе данных] [ select-columns] модуля или hello [редактирование метаданных] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="704af-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="704af-355">Дополнительные сведения см. на страницах справки модулей [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных) и [Edit Metadata][edit-metadata] (Изменение метаданных).</span><span class="sxs-lookup"><span data-stu-id="704af-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="704af-356"><a name="mldeploy"></a>Развертывание моделей в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="704af-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="704af-357">Когда модель готова, можно легко развернуть его веб-службы непосредственно из эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="704af-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="704af-358">Дополнительные сведения см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="704af-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="704af-359">toodeploy веб-службу, необходимо:</span><span class="sxs-lookup"><span data-stu-id="704af-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="704af-360">Создать эксперимент по количественной оценке.</span><span class="sxs-lookup"><span data-stu-id="704af-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="704af-361">Развертывание веб-службы hello.</span><span class="sxs-lookup"><span data-stu-id="704af-361">Deploy hello web service.</span></span>

<span data-ttu-id="704af-362">оценки поэкспериментировать с toocreate **завершен** обучения, эксперимента, нажмите кнопку **создать ЭКСПЕРИМЕНТ ОЦЕНКИ** hello нижней панели действий.</span><span class="sxs-lookup"><span data-stu-id="704af-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Система оценок Azure][18]

<span data-ttu-id="704af-364">Машинное обучение Azure попытается toocreate эксперимент оценки на основе компонентов hello эксперимента обучения hello.</span><span class="sxs-lookup"><span data-stu-id="704af-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="704af-365">В частности, она:</span><span class="sxs-lookup"><span data-stu-id="704af-365">In particular, it will:</span></span>

1. <span data-ttu-id="704af-366">Сохранить обученную модель hello и удалите hello модели обучающих модулей.</span><span class="sxs-lookup"><span data-stu-id="704af-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="704af-367">Определение логических **входному порту** toorepresent hello требуется схема входных данных.</span><span class="sxs-lookup"><span data-stu-id="704af-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="704af-368">Определение логических **выходного порта** toorepresent hello ожидаемый web службы выходные данные схемы.</span><span class="sxs-lookup"><span data-stu-id="704af-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="704af-369">При создании hello эксперимент оценки, просмотра и при необходимости измените.</span><span class="sxs-lookup"><span data-stu-id="704af-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="704af-370">Типичные корректировки — входного набора данных hello tooreplace или запроса с одним, что исключает поля меток, их будет недоступен при вызове службы hello.</span><span class="sxs-lookup"><span data-stu-id="704af-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="704af-371">Это также размером хорошей практикой tooreduce hello hello входной набор данных или запроса tooa несколько записей, достаточно tooindicate hello входной схемы.</span><span class="sxs-lookup"><span data-stu-id="704af-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="704af-372">Для порта вывода hello, он общие tooexclude всех полей ввода и включать только hello **меток оцененных значений** и **оцененных вероятностей** в выходных данных с помощью hello hello [Выбор столбцов в наборе данных ] [ select-columns] модуля.</span><span class="sxs-lookup"><span data-stu-id="704af-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="704af-373">Пример оценки экспериментов — hello рис. ниже.</span><span class="sxs-lookup"><span data-stu-id="704af-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="704af-374">Окончании toodeploy, нажмите кнопку hello **публикации веб-службы** кнопку hello нижней панели действий.</span><span class="sxs-lookup"><span data-stu-id="704af-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Публикация в Машинном обучении Azure][11]

<span data-ttu-id="704af-376">toorecap, в этом учебнике пошаговом руководстве вы создали среде обработки и анализа данных Azure, работали с большим набором данных открытый все возможности hello со toomodel приобретения данных обучения и развертывание веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="704af-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="704af-377">Сведения о лицензии</span><span class="sxs-lookup"><span data-stu-id="704af-377">License Information</span></span>
<span data-ttu-id="704af-378">Это пошаговое руководство по примеру и соответствующую ему коллекцию скриптов и IPython notebook(s) совместно корпорацией Майкрософт в рамках лицензии MIT hello.</span><span class="sxs-lookup"><span data-stu-id="704af-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="704af-379">Проверьте файл LICENSE.txt hello в каталоге hello hello образца кода на GitHub для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="704af-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="704af-380">Ссылки</span><span class="sxs-lookup"><span data-stu-id="704af-380">References</span></span>
<span data-ttu-id="704af-381">•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="704af-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="704af-382">•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="704af-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="704af-383">•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="704af-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
