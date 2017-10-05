---
title: "Создание и развертывание модели машинного обучения с помощью SQL Server на виртуальной машине Azure | Документация Майкрософт"
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
ms.openlocfilehash: 6c5361c7e47209c8eb4d5630b44b3dcfeedeaf01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="0a71a-103">Процесс обработки и анализа данных группы на практике: использование SQL Server</span><span class="sxs-lookup"><span data-stu-id="0a71a-103">The Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="0a71a-104">В этом руководстве представлено пошаговое руководство по процессу создания и развертывания модели машинного обучения с помощью SQL Server и общедоступного набора данных [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="0a71a-104">In this tutorial, you walk through the process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="0a71a-105">Процедура соответствует стандартному рабочему процессу обработки и аналитики данных: прием и анализ данных, разработка функций для упрощения обучения, а затем сборка и развертывание модели.</span><span class="sxs-lookup"><span data-stu-id="0a71a-105">The procedure follows a standard data science workflow: ingest and explore the data, engineer features to facilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="0a71a-106"><a name="dataset"></a>Описание набора данных "Поездки такси Нью-Йорка"</span><span class="sxs-lookup"><span data-stu-id="0a71a-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="0a71a-107">Данные о поездках такси Нью-Йорка содержат около 20 ГБ сжатых CSV-файлов (~48 ГБ в несжатом виде), что составляет более 173 млн отдельных поездок и платежей за каждую поездку.</span><span class="sxs-lookup"><span data-stu-id="0a71a-107">The NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="0a71a-108">Каждая запись о поездке содержит расположение пунктов отправления и назначения и время, анонимизированный номер лицензии водителя и номер медальона (уникальный идентификатор такси).</span><span class="sxs-lookup"><span data-stu-id="0a71a-108">Each trip record includes the pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="0a71a-109">Данные включают в себя все поездки за 2013 год и предоставляются в виде следующих двух наборов данных за каждый месяц:</span><span class="sxs-lookup"><span data-stu-id="0a71a-109">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="0a71a-110">CSV-файл trip_data содержит подробную информацию о поездке, например число пассажиров, пункты отправления и назначения, продолжительность поездки и ее расстояние.</span><span class="sxs-lookup"><span data-stu-id="0a71a-110">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="0a71a-111">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="0a71a-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="0a71a-112">CSV-файл trip_fare содержит подробную информацию об оплате каждой поездки, такие как тип оплаты, сумма тарифа, надбавка и налоги, чаевые и пошлины, а также общая выплаченная сумма.</span><span class="sxs-lookup"><span data-stu-id="0a71a-112">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="0a71a-113">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="0a71a-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="0a71a-114">Уникальный ключ для объединения trip\_data и trip\_fare состоит из полей medallion, hack\_licence и pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="0a71a-114">The unique key to join trip\_data and trip\_fare is composed of the fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="0a71a-115"><a name="mltasks"></a>Примеры задач прогнозирования</span><span class="sxs-lookup"><span data-stu-id="0a71a-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="0a71a-116">Мы сформулируем три перечисленные ниже задачи прогнозирования на основе *tip\_amount*.</span><span class="sxs-lookup"><span data-stu-id="0a71a-116">We will formulate three prediction problems based on the *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="0a71a-117">Двоичная классификация. Позволяет спрогнозировать, были ли оставлены чаевые после поездки, т. е. значение *tip\_amount* > 0 $ — это положительный пример, а значение *tip\_amount* = 0 $ — отрицательный пример.</span><span class="sxs-lookup"><span data-stu-id="0a71a-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="0a71a-118">Мультиклассовая классификация: Спрогнозировать диапазон суммы чаевых за поездку.</span><span class="sxs-lookup"><span data-stu-id="0a71a-118">Multiclass classification: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="0a71a-119">Мы разделяем *tip\_amount* на пять ячеек или классов:</span><span class="sxs-lookup"><span data-stu-id="0a71a-119">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="0a71a-120">Задача регрессии: Спрогнозировать сумму чаевых, выплаченных за поездку.</span><span class="sxs-lookup"><span data-stu-id="0a71a-120">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="0a71a-121"><a name="setup"></a>Настройка среды обработки данных Azure для расширенной аналитики</span><span class="sxs-lookup"><span data-stu-id="0a71a-121"><a name="setup"></a>Setting Up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="0a71a-122">Как можно видеть по руководству [Планирование вашей среды](machine-learning-data-science-plan-your-environment.md) , существует несколько вариантов работы с набором данных "Поездки такси Нью-Йорка" в Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-122">As you can see from the [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options to work with the NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="0a71a-123">Работа с данными в BLOB-объектах Azure и последующее моделирование в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-123">Work with the data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="0a71a-124">Загрузка данных в базу данных SQL Server и последующее моделирование в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-124">Load the data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="0a71a-125">В этом учебнике мы продемонстрируем параллельный массовый импорт данных в SQL Server, просмотр данных, проектирование характеристик и уменьшение выборки с помощью SQL Server Management Studio, а также с помощью IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="0a71a-125">In this tutorial we will demonstrate parallel bulk import of the data to a SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="0a71a-126">[Примеры скриптов](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) и файлы [IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) предоставлены в общий доступ на GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a71a-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="0a71a-127">На этом же ресурсе доступен и образец файла IPython Notebook для работы с данными в BLOB-объектах.</span><span class="sxs-lookup"><span data-stu-id="0a71a-127">A sample IPython notebook to work with the data in Azure blobs is also available in the same location.</span></span>

<span data-ttu-id="0a71a-128">Чтобы настроить среду научной обработки данных в Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0a71a-128">To set up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="0a71a-129">создать учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="0a71a-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="0a71a-130">Создание рабочей области машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="0a71a-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="0a71a-131">[Подготовьте виртуальную машину для обработки и анализа данных](machine-learning-data-science-setup-sql-server-virtual-machine.md), которая будет служить сервером SQL Server и сервером IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="0a71a-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0a71a-132">Примеры сценариев и файлов IPython Notebook будут загружены в вашу виртуальную машину для обработки данных в процессе установки.</span><span class="sxs-lookup"><span data-stu-id="0a71a-132">The sample scripts and IPython notebooks will be downloaded to your Data Science virtual machine during the setup process.</span></span> <span data-ttu-id="0a71a-133">После завершения сценария, выполняемого после установки ВМ, примеры будут располагаться в библиотеке документов вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0a71a-133">When the VM post-installation script completes, the samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="0a71a-134">Примеры сценариев: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="0a71a-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="0a71a-135">Примеры IPython Notebook: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="0a71a-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="0a71a-136">where `<user_name>` является именем для входа Windows виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0a71a-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="0a71a-137">Эти папки с примерами в дальнейшем будут называться **Примеры скриптов** и **Примеры файлов IPython Notebook**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-137">We will refer to the sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="0a71a-138">По размеру набора данных, расположению источника данных и выбранной целевой среде Azure этот пример похож на [Сценарий \#№ 5. Большой набор данных в локальных файлах, загружаемый на сервер SQL Server в виртуальной машине Azure](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="0a71a-138">Based on the dataset size, data source location, and the selected Azure target environment, this scenario is similar to [Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="0a71a-139"><a name="getdata"></a>Получение данных из общедоступного источника</span><span class="sxs-lookup"><span data-stu-id="0a71a-139"><a name="getdata"></a>Get the Data from Public Source</span></span>
<span data-ttu-id="0a71a-140">Чтобы получить [набор данных о поездках такси Нью-Йорка](http://www.andresmh.com/nyctaxitrips/) из общедоступного расположения, скопируйте данные на новую виртуальную машину. Для этого можно воспользоваться любым из методов, описанных в статье [Перемещение данных в хранилище больших двоичных объектов Azure и из него](machine-learning-data-science-move-azure-blob.md).</span><span class="sxs-lookup"><span data-stu-id="0a71a-140">To get the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of the methods described in [Move Data to and from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) to copy the data to your new virtual machine.</span></span>

<span data-ttu-id="0a71a-141">Чтобы скопировать данные с помощью AzCopy, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0a71a-141">To copy the data using AzCopy:</span></span>

1. <span data-ttu-id="0a71a-142">Войдите на виртуальную машину (ВМ).</span><span class="sxs-lookup"><span data-stu-id="0a71a-142">Log in to your virtual machine (VM)</span></span>
2. <span data-ttu-id="0a71a-143">Создайте новый каталог на диске данных Виртуальной машины (Примечание: не используйте временный диск, который поставляется вместе с виртуальной Машиной в качестве диска с данными).</span><span class="sxs-lookup"><span data-stu-id="0a71a-143">Create a new directory in the VM's data disk (Note: Do not use the Temporary Disk which comes with the VM as a Data Disk).</span></span>
3. <span data-ttu-id="0a71a-144">В окне командной строки выполните следующую команду Azcopy, заменив <path_to_data_folder> соответствующей папкой данных, созданной на шаге (2):</span><span class="sxs-lookup"><span data-stu-id="0a71a-144">In a Command Prompt window, run the following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="0a71a-145">Когда программа AzCopy завершит работу, в папке данных появится 24 сжатых CSV-файла (по 12 для trip\_data и trip\_fare).</span><span class="sxs-lookup"><span data-stu-id="0a71a-145">When the AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in the data folder.</span></span>
4. <span data-ttu-id="0a71a-146">Распакуйте загруженные файлы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-146">Unzip the downloaded files.</span></span> <span data-ttu-id="0a71a-147">Обратите внимание на папку, в которой располагаются распакованные файлы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-147">Note the folder where the uncompressed files reside.</span></span> <span data-ttu-id="0a71a-148">Эта папка будет называться <path\_to\_data\_files\>.</span><span class="sxs-lookup"><span data-stu-id="0a71a-148">This folder will be referred to as the <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="0a71a-149"><a name="dbload"></a>Выполните массовый импорт данных в базу данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="0a71a-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="0a71a-150">Скорость загрузки или передачи больших объемов данных в базу данных SQL и последующих запросов можно оптимизировать с помощью *секционированных таблиц и представлений*.</span><span class="sxs-lookup"><span data-stu-id="0a71a-150">The performance of loading/transferring large amounts of data to an SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="0a71a-151">В этом разделе мы будем следовать инструкциям, описанным в разделе [Параллельный массовый импорт данных с помощью таблиц разделов SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) для создания новой базы данных и параллельной загрузки данных в секционированные таблицы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-151">In this section, we will follow the instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) to create a new database and load the data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="0a71a-152">Войдите на виртуальную машину и запустите **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-152">While logged in to your VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="0a71a-153">Подключитесь с использованием проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="0a71a-153">Connect using Windows Authentication.</span></span>
   
    ![Подключение SSMS][12]
3. <span data-ttu-id="0a71a-155">Если вы еще не изменили режим проверки подлинности SQL и не создали пользователя для входа в SQL, откройте файл сценария с именем **change\_auth.sql** в папке **Примеры скриптов**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-155">If you have not yet changed the SQL Server authentication mode and created a new SQL login user, open the script file named **change\_auth.sql** in the **Sample Scripts** folder.</span></span> <span data-ttu-id="0a71a-156">Измените имя пользователя и пароль, используемые по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0a71a-156">Change the  default user name and password.</span></span> <span data-ttu-id="0a71a-157">Нажмите **!Выполнить** на панели инструментов, чтобы запустить сценарий.</span><span class="sxs-lookup"><span data-stu-id="0a71a-157">Click **!Execute** in the toolbar to run the script.</span></span>
   
    ![Выполнение сценария][13]
4. <span data-ttu-id="0a71a-159">Проверьте и/или измените используемые по умолчанию папки базы данных и журнала SQL Server, чтобы обеспечить хранение новых создаваемых баз данных на диске с данными.</span><span class="sxs-lookup"><span data-stu-id="0a71a-159">Verify and/or change the SQL Server default database and log folders to ensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="0a71a-160">Образ виртуальной машины SQL Server, оптимизированный для нагрузок хранилищ данных, снабжен предварительными настройками дисков для данных и журнала.</span><span class="sxs-lookup"><span data-stu-id="0a71a-160">The SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="0a71a-161">Если ваша виртуальная машина не содержит диска с данными и вы добавили новые виртуальные жесткие диски в процессе установки ВМ, измените папки по умолчанию следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0a71a-161">If your VM did not include a Data Disk and you added new virtual hard disks during the VM setup process, change the default folders as follows:</span></span>
   
   * <span data-ttu-id="0a71a-162">Щелкните правой кнопкой мыши имя сервера SQL Server на левой панели и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-162">Right-click the SQL Server name in the left panel and click **Properties**.</span></span>
     
       ![Свойства сервера SQL][14]
   * <span data-ttu-id="0a71a-164">Щелкните **Параметры базы** данных в списке **Выбор страницы** слева.</span><span class="sxs-lookup"><span data-stu-id="0a71a-164">Select **Database Settings** from the **Select a page** list to the left.</span></span>
   * <span data-ttu-id="0a71a-165">Проверьте и (или) измените **расположения базы данных** по умолчанию на выбранные вами расположения **диска с данными**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-165">Verify and/or change the **Database default locations** to the **Data Disk** locations of your choice.</span></span> <span data-ttu-id="0a71a-166">Здесь будут располагаться новые базы, созданные с настройками расположения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0a71a-166">This is where new databases reside if created with the default location settings.</span></span>
     
       ![База данных SQL по умолчанию][15]  
5. <span data-ttu-id="0a71a-168">Чтобы создать базу данных и набор файловых групп для размещения секционированных таблиц, откройте образец скрипта **create\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-168">To create a new database and a set of filegroups to hold the partitioned tables, open the sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="0a71a-169">Сценарий создаст новую базу данных с именем **TaxiNYC** и 12 файловых групп в расположении данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0a71a-169">The script will create a new database named **TaxiNYC** and 12 filegroups in the default data location.</span></span> <span data-ttu-id="0a71a-170">Каждая файловая группа будет содержать данные trip\_data и trip\_fare за один месяц.</span><span class="sxs-lookup"><span data-stu-id="0a71a-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="0a71a-171">При желании можно изменить имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-171">Modify the database name, if desired.</span></span> <span data-ttu-id="0a71a-172">Нажмите **!Выполнить** , чтобы запустить сценарий.</span><span class="sxs-lookup"><span data-stu-id="0a71a-172">Click **!Execute** to run the script.</span></span>
6. <span data-ttu-id="0a71a-173">Затем создайте две таблицы секционирования: по одной для trip\_data и trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="0a71a-173">Next, create two partition tables, one for the trip\_data and another for the trip\_fare.</span></span> <span data-ttu-id="0a71a-174">Откройте образец скрипта **create\_partitioned\_table.sql**, который выполнит следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0a71a-174">Open the sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="0a71a-175">Создаст функцию секционирования для разделения данных по месяцам.</span><span class="sxs-lookup"><span data-stu-id="0a71a-175">Create a partition function to split the data by month.</span></span>
   * <span data-ttu-id="0a71a-176">Создаст схему секционирования для сопоставления данных за каждый месяц с отдельной файловой группой.</span><span class="sxs-lookup"><span data-stu-id="0a71a-176">Create a partition scheme to map each month's data to a different filegroup.</span></span>
   * <span data-ttu-id="0a71a-177">Создайте две таблицы секционирования для сопоставления со схемой секционирования: **nyctaxi\_trip** будет содержать данные trip\_data, а **nyctaxi\_fare** — данные trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="0a71a-177">Create two partitioned tables mapped to the partition scheme: **nyctaxi\_trip** will hold the trip\_data and **nyctaxi\_fare** will hold the trip\_fare data.</span></span>
     
     <span data-ttu-id="0a71a-178">Нажмите **!Выполнить** , чтобы запустить сценарий и создать секционированные таблицы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-178">Click **!Execute** to run the script and create the partitioned tables.</span></span>
7. <span data-ttu-id="0a71a-179">Папка **Примеры сценариев** содержит два образца сценариев PowerShell, предоставленные для демонстрации параллельного массового импорта данных в таблицы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a71a-179">In the **Sample Scripts** folder, there are two sample PowerShell scripts provided to demonstrate parallel bulk imports of data to SQL Server tables.</span></span>
   
   * <span data-ttu-id="0a71a-180">**bcp\_parallel\_generic.ps1** — универсальный скрипт для параллельного массового импорта данных в таблицу.</span><span class="sxs-lookup"><span data-stu-id="0a71a-180">**bcp\_parallel\_generic.ps1** is a generic script to parallel bulk import data into a table.</span></span> <span data-ttu-id="0a71a-181">Измените этот сценарий для установки входных и целевых переменных, как указано в строках комментариев в сценарии.</span><span class="sxs-lookup"><span data-stu-id="0a71a-181">Modify this script to set the input and target variables as indicated in the comment lines in the script.</span></span>
   * <span data-ttu-id="0a71a-182">**bcp\_parallel\_nyctaxi.ps1** — предварительно настроенная версия универсального скрипта, которая может использоваться для загрузки обеих таблиц с данными о поездках такси Нью-Йорка.</span><span class="sxs-lookup"><span data-stu-id="0a71a-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of the generic script and can be used to to load both tables for the NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="0a71a-183">Щелкните правой кнопкой мыши имя сценария **bcp\_parallel\_nyctaxi.ps1** и выберите **Изменить**, чтобы открыть его в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a71a-183">Right-click the **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** to open it in PowerShell.</span></span> <span data-ttu-id="0a71a-184">Просмотрите предустановленные переменные и измените их в соответствии с выбранным именем базы данных, папкой входных данных, целевой папкой журнала и путями к образцам файлов форматирования **nyctaxi_trip.xml** и **nyctaxi\_fare.xml** (расположены в папке **Примеры скриптов**).</span><span class="sxs-lookup"><span data-stu-id="0a71a-184">Review the preset variables and modify according to your selected database name, input data folder, target log folder, and paths to the  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in the **Sample Scripts** folder).</span></span>
   
    ![Массовый импорт данных][16]
   
    <span data-ttu-id="0a71a-186">Также можно выбрать режим проверки подлинности (по умолчанию — проверка подлинности Windows).</span><span class="sxs-lookup"><span data-stu-id="0a71a-186">You may also select the authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="0a71a-187">Для запуска щелкните зеленую стрелку на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="0a71a-187">Click the green arrow in the toolbar to run.</span></span> <span data-ttu-id="0a71a-188">Сценарий параллельно запустит 24 операции массового импорта — по 12 на каждую секционированную таблицу.</span><span class="sxs-lookup"><span data-stu-id="0a71a-188">The script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="0a71a-189">Чтобы отслеживать ход импорта данных, откройте папку данных SQL Server по умолчанию, настроенную выше.</span><span class="sxs-lookup"><span data-stu-id="0a71a-189">You may monitor the data import progress by opening the SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="0a71a-190">Сценарий PowerShell сообщает о времени начала и завершения операций.</span><span class="sxs-lookup"><span data-stu-id="0a71a-190">The PowerShell script reports the starting and ending times.</span></span> <span data-ttu-id="0a71a-191">После завершения всех операций массового импорта сообщается время завершения.</span><span class="sxs-lookup"><span data-stu-id="0a71a-191">When all bulk imports complete, the ending time is reported.</span></span> <span data-ttu-id="0a71a-192">Проверьте целевую папку журнала, чтобы убедиться в успешном выполнении массового импорта, т. е. в отсутствии сообщений об ошибках в целевой папке журнала.</span><span class="sxs-lookup"><span data-stu-id="0a71a-192">Check the target log folder to verify that the bulk imports were successful, i.e., no errors reported in the target log folder.</span></span>
10. <span data-ttu-id="0a71a-193">Теперь база данных готова к просмотру, проектированию характеристик и другим операциям.</span><span class="sxs-lookup"><span data-stu-id="0a71a-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="0a71a-194">Так как таблицы секционированы в соответствии с полем **pickup\_datetime**, запросы с условиями **pickup\_datetime** в предложении **WHERE** будут учитывать схему секционирования.</span><span class="sxs-lookup"><span data-stu-id="0a71a-194">Since the tables are partitioned according to the **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in the **WHERE** clause will benefit from the partition scheme.</span></span>
11. <span data-ttu-id="0a71a-195">В среде **SQL Server Management Studio** изучите предоставленный образец скрипта **sample\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-195">In **SQL Server Management Studio**, explore the provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="0a71a-196">Чтобы запустить любой из образцов запросов, выделите строки запроса, а затем щелкните **!Выполнить** на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="0a71a-196">To run any of the sample queries, highlight the query lines then click **!Execute** in the toolbar.</span></span>
12. <span data-ttu-id="0a71a-197">Данные "Поездки такси Нью-Йорка" будут загружены в две отдельные таблицы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-197">The NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="0a71a-198">Для улучшения операций объединения настоятельно рекомендуется проиндексировать таблицы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-198">To improve join operations, it is highly recommended to index the tables.</span></span> <span data-ttu-id="0a71a-199">Образец скрипта **create\_partitioned\_index.sql** создает секционированные индексы по ключу составного соединения **medallion, hack\_license и pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-199">The sample script **create\_partitioned\_index.sql** creates partitioned indexes on the composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="0a71a-200"><a name="dbexplore"></a>Просмотр данных и проектирование характеристик в SQL Server</span><span class="sxs-lookup"><span data-stu-id="0a71a-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="0a71a-201">В этом разделе мы выполним просмотр данных и создадим характеристики путем запуска SQL-запросов непосредственно в среде **SQL Server Management Studio** с использованием ранее созданной базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a71a-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in the **SQL Server Management Studio** using the SQL Server database created earlier.</span></span> <span data-ttu-id="0a71a-202">Образец скрипта с именем **sample\_queries.sql** расположен в папке **Примеры скриптов**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-202">A sample script named **sample\_queries.sql** is provided in the **Sample Scripts** folder.</span></span> <span data-ttu-id="0a71a-203">Измените в сценарии имя базы данных, если оно отличается от установленного по умолчанию **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-203">Modify the script to change the database name, if it is different from the default: **TaxiNYC**.</span></span>

<span data-ttu-id="0a71a-204">В этом упражнении мы выполним такие действия.</span><span class="sxs-lookup"><span data-stu-id="0a71a-204">In this exercise, we will:</span></span>

* <span data-ttu-id="0a71a-205">Подключимся к среде **SQL Server Management Studio** с помощью проверки подлинности Windows или проверки подлинности SQL, имени пользователя SQL и пароля.</span><span class="sxs-lookup"><span data-stu-id="0a71a-205">Connect to **SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and the SQL login name and password.</span></span>
* <span data-ttu-id="0a71a-206">Просмотрим распределение данных по нескольким полям в различных временных окнах.</span><span class="sxs-lookup"><span data-stu-id="0a71a-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="0a71a-207">Исследуем качество данных по полям долготы и широты.</span><span class="sxs-lookup"><span data-stu-id="0a71a-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="0a71a-208">Создадим метки двоичной и мультиклассовой классификации на основе **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="0a71a-209">Создадим характеристики и вычислим/сравним расстояния поездок.</span><span class="sxs-lookup"><span data-stu-id="0a71a-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="0a71a-210">Соединим две таблицы и извлечем случайную выборку, которая послужит основой для построения моделей.</span><span class="sxs-lookup"><span data-stu-id="0a71a-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

<span data-ttu-id="0a71a-211">Когда вы будете готовы перейти к машинному обучению Azure, вы можете:</span><span class="sxs-lookup"><span data-stu-id="0a71a-211">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="0a71a-212">Сохранить окончательный SQL-запрос для извлечения и выборки данных, скопировать и вставить этот запрос непосредственно в модуль [Импорт данных][import-data] в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-212">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="0a71a-213">Или сохранить выбранные и спроектированные данные, которые планируется использовать для построения модели в новой таблице базы данных, и использовать новую таблицу в модуле [Импорт данных][import-data] в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-213">Persist the sampled and engineered data you plan to use for model building in a new database table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="0a71a-214">В этом разделе мы сохраним финальный запрос для извлечения и выборки данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-214">In this section we will save the final query to extract and sample the data.</span></span> <span data-ttu-id="0a71a-215">Второй метод демонстрируется в разделе [Просмотр данных и проектирование характеристик в IPython Notebook](#ipnb) .</span><span class="sxs-lookup"><span data-stu-id="0a71a-215">The second method is demonstrated in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="0a71a-216">Быстрая проверка числа строк и столбцов в таблицах, заполненных ранее с помощью параллельного массового импорта:</span><span class="sxs-lookup"><span data-stu-id="0a71a-216">For a quick verification of the number of rows and columns in the tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="0a71a-217">Просмотр: Распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="0a71a-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="0a71a-218">В этом примере определяются медальоны (номера такси) с более чем 100 поездками за заданный период времени.</span><span class="sxs-lookup"><span data-stu-id="0a71a-218">This example identifies the medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="0a71a-219">Запрос будет использовать секционированный доступ к таблице, так как он обусловлен схемой секционирования **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-219">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="0a71a-220">При запросе к полному набору данных также будет задействовано сканирование секционированной таблицы и/или индекса.</span><span class="sxs-lookup"><span data-stu-id="0a71a-220">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="0a71a-221">Просмотр: распределение поездок по параметрам medallion и hack_license</span><span class="sxs-lookup"><span data-stu-id="0a71a-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="0a71a-222">Оценка качества данных: Проверка записей с неверными значениями долготы и/или широты</span><span class="sxs-lookup"><span data-stu-id="0a71a-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="0a71a-223">В этом примере анализируется, содержится ли в каких-либо полях долготы и/или широты неверное значение (количество градусов должно быть в пределах от -90 до 90) или значение координат (0, 0).</span><span class="sxs-lookup"><span data-stu-id="0a71a-223">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="0a71a-224">Просмотр: Выплаченные чаевые против Распределение поездок с чаевыми и без чаевых</span><span class="sxs-lookup"><span data-stu-id="0a71a-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="0a71a-225">В этом примере определяется число поездок, в которых были выплачены чаевые, против тех, в которых чаевые не были выплачены, за заданный период времени (или по полному набору данных в случае охвата целого года).</span><span class="sxs-lookup"><span data-stu-id="0a71a-225">This example finds the number of trips that were tipped vs. not tipped in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="0a71a-226">Это распределение отражает распределение двоичных меток, которые в дальнейшем будут использоваться для моделирования двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="0a71a-226">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="0a71a-227">Просмотр: распределение классов/диапазонов чаевых</span><span class="sxs-lookup"><span data-stu-id="0a71a-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="0a71a-228">В этом примере вычисляется распределение диапазонов чаевых за заданный период времени (или по полному набору данных в случае охвата целого года).</span><span class="sxs-lookup"><span data-stu-id="0a71a-228">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="0a71a-229">Это распределение классов меток, которое в дальнейшем будет использоваться для моделирования мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="0a71a-229">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

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

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="0a71a-230">Просмотр: Вычисление и сравнение расстояния поездок</span><span class="sxs-lookup"><span data-stu-id="0a71a-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="0a71a-231">В этом примере значения долготы и широты начальных и конечных пунктов поездок преобразуются в географические точки SQL, вычисляется расстояние поездки по разности географических точек и возвращается случайная выборка результатов для сравнения.</span><span class="sxs-lookup"><span data-stu-id="0a71a-231">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="0a71a-232">В примере результаты ограничиваются только допустимыми координатами с помощью запроса оценки качества данных, описанного ранее.</span><span class="sxs-lookup"><span data-stu-id="0a71a-232">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

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

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="0a71a-233">Проектирование характеристик в запросах SQL</span><span class="sxs-lookup"><span data-stu-id="0a71a-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="0a71a-234">Запросы на создание меток и просмотр преобразования географии можно также использовать для создания меток/характеристик путем удаления части, производящей подсчет.</span><span class="sxs-lookup"><span data-stu-id="0a71a-234">The label generation and geography conversion exploration queries can also be used to generate labels/features by removing the counting part.</span></span> <span data-ttu-id="0a71a-235">Дополнительные примеры проектирования характеристик на SQL содержатся в разделе [Просмотр данных и проектирование характеристик в IPython Notebook](#ipnb) .</span><span class="sxs-lookup"><span data-stu-id="0a71a-235">Additional feature engineering SQL examples are provided in the [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="0a71a-236">Более эффективно выполнять запросы на создание характеристик для полного набора данных или его большого подмножества, используя SQL-запросы, выполняемые непосредственно на экземпляре базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a71a-236">It is more efficient to run the feature generation queries on the full dataset or a large subset of it using SQL queries which run directly on the SQL Server database instance.</span></span> <span data-ttu-id="0a71a-237">Запросы могут выполняться в **SQL Server Management Studio**, IPython Notebook или любом средстве/среде разработки, которое может обращаться к базе данных локально или удаленно.</span><span class="sxs-lookup"><span data-stu-id="0a71a-237">The queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access the database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="0a71a-238">Подготовка данных для построения модели</span><span class="sxs-lookup"><span data-stu-id="0a71a-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="0a71a-239">Следующий запрос соединяет таблицы **nyctaxi\_trip** и **nyctaxi\_fare**, создает метку двоичной классификации **tipped**, метку многоклассовой классификации **tip\_class**, а также извлекает малую выборку из полного соединенного набора данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-239">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from the full joined dataset.</span></span> <span data-ttu-id="0a71a-240">Этот запрос можно скопировать, а затем вставить непосредственно в модуль [Импорт данных](https://studio.azureml.net) [Студии машинного обучения Azure][import-data] для прямого приема данных из экземпляра базы данных SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-240">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL Server database instance in Azure.</span></span> <span data-ttu-id="0a71a-241">Запрос исключает записи с неверными (0, 0) координатами.</span><span class="sxs-lookup"><span data-stu-id="0a71a-241">The query excludes records with incorrect (0, 0) coordinates.</span></span>

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


## <span data-ttu-id="0a71a-242"><a name="ipnb"></a>Просмотр данных и проектирование характеристик в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="0a71a-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="0a71a-243">В этом разделе мы выполним просмотр данных и проектирование характеристик используя как Python, так и SQL-запросы, в отличии от созданной ранее базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0a71a-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL Server database created earlier.</span></span> <span data-ttu-id="0a71a-244">Образец файла IPython Notebook с именем**machine-Learning-data-science-process-sql-story.ipynb** расположен в папке **Примеры файлов IPython Notebook**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in the **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="0a71a-245">Этот файл также доступен на [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="0a71a-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="0a71a-246">Рекомендованный порядок действий при работе с данными большого размера.</span><span class="sxs-lookup"><span data-stu-id="0a71a-246">The recommended sequence when working with big data is the following:</span></span>

* <span data-ttu-id="0a71a-247">Считайте небольшую выборку данных во фрейм данных, размещенный в памяти.</span><span class="sxs-lookup"><span data-stu-id="0a71a-247">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="0a71a-248">Выполните несколько визуализаций и просмотров с использованием выборки данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-248">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="0a71a-249">Поэкспериментируйте с проектированием характеристик с использованием выборки данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-249">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="0a71a-250">Для просмотра большего объема данных, манипуляций с данными и проектирования характеристик используйте Python для подачи SQL-запросов непосредственно к базе данных SQL Server на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-250">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL Server database in the Azure VM.</span></span>
* <span data-ttu-id="0a71a-251">Определите размер выборки, который будет использоваться для построения модели в службе машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-251">Decide the sample size to use for Azure Machine Learning model building.</span></span>

<span data-ttu-id="0a71a-252">Когда вы будете готовы перейти к машинному обучению Azure, можно выполнить одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="0a71a-252">When ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="0a71a-253">Сохранить окончательный SQL-запрос для извлечения и выборки данных, скопировать и вставить этот запрос непосредственно в модуль [Импорт данных][import-data] в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-253">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="0a71a-254">Этот метод демонстрируется в разделе [Построение моделей в машинном обучении Azure](#mlmodel) .</span><span class="sxs-lookup"><span data-stu-id="0a71a-254">This method is demonstrated in the [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="0a71a-255">Сохранить выбранные и спроектированные данные, которые планируется использовать для построения модели, в новой таблице базы данных, затем использовать эту новую таблицу в модуле [Импорт данных][import-data].</span><span class="sxs-lookup"><span data-stu-id="0a71a-255">Persist the sampled and engineered data you plan to use for model building in a new database table, then use the new table in the [Import Data][import-data] module.</span></span>

<span data-ttu-id="0a71a-256">Ниже приведены несколько примеров просмотра данных, визуализации данных и проектирования характеристик.</span><span class="sxs-lookup"><span data-stu-id="0a71a-256">The following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="0a71a-257">Дополнительные примеры см. в образце файла IPython Notebook с SQL-запросом в папке **Примеры файлов IPython Notebook**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-257">For more examples, see the sample SQL IPython notebook in the **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="0a71a-258">Инициализация учетных данных базы данных</span><span class="sxs-lookup"><span data-stu-id="0a71a-258">Initialize Database Credentials</span></span>
<span data-ttu-id="0a71a-259">Инициализируйте параметры подключения к базе данных в следующих переменных:</span><span class="sxs-lookup"><span data-stu-id="0a71a-259">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="0a71a-260">Создание подключения к базе данных</span><span class="sxs-lookup"><span data-stu-id="0a71a-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="0a71a-261">Сообщение числа строк и столбцов в таблице nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="0a71a-261">Report number of rows and columns in table nyctaxi_trip</span></span>
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

* <span data-ttu-id="0a71a-262">Общее число строк = 173179759</span><span class="sxs-lookup"><span data-stu-id="0a71a-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="0a71a-263">Общее число столбцов = 14</span><span class="sxs-lookup"><span data-stu-id="0a71a-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-the-sql-server-database"></a><span data-ttu-id="0a71a-264">Считывание небольшой выборки данных из базы данных SQL Server</span><span class="sxs-lookup"><span data-stu-id="0a71a-264">Read-in a small data sample from the SQL Server Database</span></span>
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
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="0a71a-265">Время чтения таблицы выборки равно 6,492000 секунды</span><span class="sxs-lookup"><span data-stu-id="0a71a-265">Time to read the sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="0a71a-266">Число извлеченных строк и столбцов = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="0a71a-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="0a71a-267">Описательная статистика</span><span class="sxs-lookup"><span data-stu-id="0a71a-267">Descriptive Statistics</span></span>
<span data-ttu-id="0a71a-268">Теперь все готово для просмотра выборки данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-268">Now are ready to explore the sampled data.</span></span> <span data-ttu-id="0a71a-269">Начнем с изучения описательной статистики для **trip\_distance** (или любых других полей).</span><span class="sxs-lookup"><span data-stu-id="0a71a-269">We start with looking at descriptive statistics for the **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="0a71a-270">Визуализация: Пример блочной диаграммы</span><span class="sxs-lookup"><span data-stu-id="0a71a-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="0a71a-271">Далее рассмотрим блочную диаграмму расстояний поездок для визуализации квантилей</span><span class="sxs-lookup"><span data-stu-id="0a71a-271">Next we look at the box plot for the trip distance to visualize the quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![График #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="0a71a-273">Визуализация: Пример графика распределения</span><span class="sxs-lookup"><span data-stu-id="0a71a-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![График #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="0a71a-275">Визуализация: Гистограммы и линейные графики</span><span class="sxs-lookup"><span data-stu-id="0a71a-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="0a71a-276">В этом примере мы сегментируем расстояния поездок на пять ячеек и визуализируем результаты сегментирования.</span><span class="sxs-lookup"><span data-stu-id="0a71a-276">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="0a71a-277">Мы можем изобразить описанное выше распределение по ячейкам в виде гистограммы или линейного графика, как показано ниже</span><span class="sxs-lookup"><span data-stu-id="0a71a-277">We can plot the above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![График #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![График #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="0a71a-280">Визуализация: Пример точечной диаграммы</span><span class="sxs-lookup"><span data-stu-id="0a71a-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="0a71a-281">Мы отобразим точечную диаграмму для параметров **trip\_time\_in\_secs** и **trip\_distance**, чтобы проверить возможную корреляцию.</span><span class="sxs-lookup"><span data-stu-id="0a71a-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![График #6][6]

<span data-ttu-id="0a71a-283">Точно также мы можем проверить связь между **rate\_code** и **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-283">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![График #8][8]

### <a name="sub-sampling-the-data-in-sql"></a><span data-ttu-id="0a71a-285">Вложенная выборка данных в SQL</span><span class="sxs-lookup"><span data-stu-id="0a71a-285">Sub-Sampling the Data in SQL</span></span>
<span data-ttu-id="0a71a-286">Подготавливая данные к созданию модели в [Студии машинного обучения Azure](https://studio.azureml.net), вы можете определить **SQL-запрос для использования непосредственно в модуле импорта данных** или сохранить спроектированные и выбранные данные в новой таблице, которую можно использовать в модуле [Импорт данных][import-data] с помощью простого запроса **SELECT * FROM <имя\_вашей\_новой\_таблицы>**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on the **SQL query to use directly in the Import Data module** or persist the engineered and sampled data in a new table, which you could use in the [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="0a71a-287">В этом разделе мы создадим новую таблицу для размещения выбранных и спроектированных данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-287">In this section we will create a new table to hold the sampled and engineered data.</span></span> <span data-ttu-id="0a71a-288">Пример прямого SQL-запроса для построения модели содержится в разделе [Просмотр данных и проектирование характеристик в SQL Server](#dbexplore) .</span><span class="sxs-lookup"><span data-stu-id="0a71a-288">An example of a direct SQL query for model building is provided in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-the-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="0a71a-289">Создайте таблицу выборки и заполните ее 1 % данных из соединенных таблиц.</span><span class="sxs-lookup"><span data-stu-id="0a71a-289">Create a Sample Table and Populate with 1% of the Joined Tables.</span></span> <span data-ttu-id="0a71a-290">Сначала удалите таблицу, если она существует.</span><span class="sxs-lookup"><span data-stu-id="0a71a-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="0a71a-291">В этом разделе мы соединим таблицы **nyctaxi\_trip** и **nyctaxi\_fare**, извлечем однопроцентную случайную выборку и сохраним выбранные данные в новой таблице с именем **nyctaxi\_one\_percent**:</span><span class="sxs-lookup"><span data-stu-id="0a71a-291">In this section, we join the tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist the sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

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

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="0a71a-292">Просмотр данных с помощью SQL-запросов в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="0a71a-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="0a71a-293">В этом разделе мы рассмотрим распределение данных с использованием 1%-ной выборки данных, которая сохранена в созданной нами выше новой таблице.</span><span class="sxs-lookup"><span data-stu-id="0a71a-293">In this section, we explore data distributions using the 1% sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="0a71a-294">Обратите внимание, что подобные просмотры можно выполнять с помощью исходных таблиц. При необходимости можно использовать **TABLESAMPLE**, чтобы ограничить выборку для просмотра или для фильтрации результатов по заданному периоду времени с помощью разделов **pickup\_datetime**, как описано в разделе [Просмотр данных и проектирование характеристик в SQL Server](#dbexplore).</span><span class="sxs-lookup"><span data-stu-id="0a71a-294">Note that similar explorations can be performed using the original tables, optionally using **TABLESAMPLE** to limit the exploration sample or by limiting the results to a given time period using the **pickup\_datetime** partitions, as illustrated in the [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="0a71a-295">Исследование: ежедневное распределение поездок</span><span class="sxs-lookup"><span data-stu-id="0a71a-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="0a71a-296">Исследование: распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="0a71a-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="0a71a-297">Создание характеристик с помощью SQL-запросов в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="0a71a-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="0a71a-298">В этом разделе мы создадим новые метки и характеристики непосредственно с помощью SQL-запросов, работая над таблицей 1%-ной выборки, которую мы создали в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="0a71a-298">In this section we will generate new labels and features directly using SQL queries, operating on the 1% sample table we created in the previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="0a71a-299">Создание метки: Создать метки классов</span><span class="sxs-lookup"><span data-stu-id="0a71a-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="0a71a-300">В следующем примере мы создадим два набора меток, используемых для моделирования.</span><span class="sxs-lookup"><span data-stu-id="0a71a-300">In the following example, we generate two sets of labels to use for modeling:</span></span>

1. <span data-ttu-id="0a71a-301">Метки двоичной классификации **tipped** (прогнозирование, будут ли выплачены чаевые).</span><span class="sxs-lookup"><span data-stu-id="0a71a-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="0a71a-302">Мультиклассовые метки **tip\_class** (прогнозирование сегмента или диапазона чаевых).</span><span class="sxs-lookup"><span data-stu-id="0a71a-302">Multiclass Labels **tip\_class** (predicting the tip bin or range)</span></span>
   
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

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="0a71a-303">Проектирование характеристик: Количественные характеристики для столбцов категорий</span><span class="sxs-lookup"><span data-stu-id="0a71a-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="0a71a-304">Этот пример преобразует поле категории в числовое поле, заменяя каждую категорию количеством ее появлений в данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-304">This example transforms a categorical field into a numeric field by replacing each category with the count of its occurrences in the data.</span></span>

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

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="0a71a-305">Проектирование характеристик: Ячейка характеристик для числовых столбцов</span><span class="sxs-lookup"><span data-stu-id="0a71a-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="0a71a-306">Этот пример преобразует непрерывное числовое поле в предустановленные диапазоны категорий, т. е. преобразует числовое поле в поле категории.</span><span class="sxs-lookup"><span data-stu-id="0a71a-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

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

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="0a71a-307">Проектирование характеристик: Извлечение характеристик местоположения из десятичных значений широты/долготы</span><span class="sxs-lookup"><span data-stu-id="0a71a-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="0a71a-308">В этом примере десятичное представление поля широты и/или долготы разбивается на несколько полей регионов с различной степенью детализации, таких как страна, город, район, квартал и т. д. Обратите внимание, что новые географические поля не сопоставляются с фактическим расположением.</span><span class="sxs-lookup"><span data-stu-id="0a71a-308">This example breaks down the decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that the new geo-fields are not mapped to actual locations.</span></span> <span data-ttu-id="0a71a-309">Дополнительные сведения о сопоставлении местоположений геокодов см. в статье о [службах REST карт Bing](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a71a-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

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

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="0a71a-310">Проверка конечной формы таблицы с признаками</span><span class="sxs-lookup"><span data-stu-id="0a71a-310">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="0a71a-311">Теперь мы готовы перейти к построению и развертыванию модели в [машинном обучении Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="0a71a-311">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="0a71a-312">Данные готовы для любой из задач прогнозирования, определенных ранее.</span><span class="sxs-lookup"><span data-stu-id="0a71a-312">The data is ready for any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="0a71a-313">Двоичная классификация: Спрогнозировать, были ли выплачены чаевые за поездку.</span><span class="sxs-lookup"><span data-stu-id="0a71a-313">Binary classification: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="0a71a-314">Мультиклассовая классификация. Спрогнозировать диапазон выплаченных чаевых в соответствии с ранее определенными классами.</span><span class="sxs-lookup"><span data-stu-id="0a71a-314">Multiclass classification: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="0a71a-315">Задача регрессии: Спрогнозировать сумму чаевых, выплаченных за поездку.</span><span class="sxs-lookup"><span data-stu-id="0a71a-315">Regression task: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="0a71a-316"><a name="mlmodel"></a>Построение моделей в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="0a71a-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="0a71a-317">Чтобы начать упражнение по моделированию, войдите в рабочую область машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-317">To begin the modeling exercise, log in to your Azure Machine Learning workspace.</span></span> <span data-ttu-id="0a71a-318">Если вы еще не создали рабочую область машинного обучения, см. статью [Создание рабочей области машинного обучения Azure и предоставление к ней общего доступа](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="0a71a-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="0a71a-319">Чтобы приступить к работе с машинным обучением Azure, см. статью [Что такое студия машинного обучения Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="0a71a-319">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="0a71a-320">Войдите в [Студию машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="0a71a-320">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="0a71a-321">На главной странице Студии содержится множество информации, видеороликов, учебников, ссылок на справочник модулей и другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-321">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="0a71a-322">Дополнительные сведения о машинном обучении Azure см. в [центре документации по машинному обучению Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="0a71a-322">Fore more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="0a71a-323">Типичный учебный эксперимент состоит из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="0a71a-323">A typical training experiment consists of the following:</span></span>

1. <span data-ttu-id="0a71a-324">Создать **+НОВЫЙ** эксперимент.</span><span class="sxs-lookup"><span data-stu-id="0a71a-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="0a71a-325">Получить данные для Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-325">Get the data to Azure Machine Learning.</span></span>
3. <span data-ttu-id="0a71a-326">Предварительно обработать, преобразовать данные и выполнить необходимые манипуляции с ними.</span><span class="sxs-lookup"><span data-stu-id="0a71a-326">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="0a71a-327">Создать необходимые характеристики.</span><span class="sxs-lookup"><span data-stu-id="0a71a-327">Generate features as needed.</span></span>
5. <span data-ttu-id="0a71a-328">Разбить данные на учебные/проверочные/тестовые наборы данных (или иметь отдельные наборы данных для каждой из этих целей).</span><span class="sxs-lookup"><span data-stu-id="0a71a-328">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="0a71a-329">Выбрать один или несколько алгоритмов машинного обучения в зависимости от решаемой задачи обучения.</span><span class="sxs-lookup"><span data-stu-id="0a71a-329">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="0a71a-330">Например, двоичная классификация, мультиклассовая классификация, регрессия.</span><span class="sxs-lookup"><span data-stu-id="0a71a-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="0a71a-331">Обучить одну или несколько моделей с помощью учебного набора данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-331">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="0a71a-332">Оценить проверочный набор данных с помощью обученных моделей.</span><span class="sxs-lookup"><span data-stu-id="0a71a-332">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="0a71a-333">Вычислить модель (модели) для расчета соответствующих показателей для задачи по обучению.</span><span class="sxs-lookup"><span data-stu-id="0a71a-333">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="0a71a-334">Провести тонкую настройку моделей и выбрать лучшую из них для развертывания.</span><span class="sxs-lookup"><span data-stu-id="0a71a-334">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="0a71a-335">В этом упражнении мы уже просмотрели и спроектировали данные на сервере SQL Server и определились с размером выборки для приема в Машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-335">In this exercise, we have already explored and engineered the data in SQL Server, and decided on the sample size to ingest in Azure Machine Learning.</span></span> <span data-ttu-id="0a71a-336">Чтобы построить одну или несколько моделей прогнозирования, которые мы определили, выполните эти действия.</span><span class="sxs-lookup"><span data-stu-id="0a71a-336">To build one or more of the prediction models we decided:</span></span>

1. <span data-ttu-id="0a71a-337">Загрузите данные в Машинное обучение Azure, используя модуль [Импорт данных][import-data], доступный в разделе **Data Input and Output** (Ввод и вывод данных).</span><span class="sxs-lookup"><span data-stu-id="0a71a-337">Get the data to Azure Machine Learning using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="0a71a-338">Дополнительные сведения см. на странице справки модуля [Import Data][import-data] (Импорт данных).</span><span class="sxs-lookup"><span data-stu-id="0a71a-338">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Импорт данных в Машинное обучение Azure][17]
2. <span data-ttu-id="0a71a-340">На панели **Properties** (Свойства) в списке **Data source** (Источник данных) выберите **Azure SQL Database** (База данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="0a71a-340">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="0a71a-341">Введите DNS-имя базы данных в поле **Имя сервера базы данных** .</span><span class="sxs-lookup"><span data-stu-id="0a71a-341">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="0a71a-342">Формат: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="0a71a-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="0a71a-343">Введите **Имя базы данных** в соответствующее поле.</span><span class="sxs-lookup"><span data-stu-id="0a71a-343">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="0a71a-344">Введите **имя пользователя SQL** в поле **Server user aqccount name (Имя учетной записи пользователя сервера) и пароль в поле **Server user account password** (Пароль учетной записи пользователя сервера).</span><span class="sxs-lookup"><span data-stu-id="0a71a-344">Enter the **SQL user name** in the **Server user aqccount name, and the password in the **Server user account password**.</span></span>
6. <span data-ttu-id="0a71a-345">Установите флажок **Принимать любой сертификат сервера** .</span><span class="sxs-lookup"><span data-stu-id="0a71a-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="0a71a-346">В текстовой области **Запрос к базе данных** вставьте запрос, который извлекает необходимые поля базы данных (включая возможные вычисляемые поля, например метки) и уменьшает размер выборки данных до требуемого.</span><span class="sxs-lookup"><span data-stu-id="0a71a-346">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="0a71a-347">Пример эксперимента по двоичной классификации со считыванием данных непосредственно из базы данных SQL Server показан на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="0a71a-347">An example of a binary classification experiment reading data directly from the SQL Server database is in the figure below.</span></span> <span data-ttu-id="0a71a-348">Подобные эксперименты можно сконструировать для задач мультиклассовой классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="0a71a-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Обучение моделей Машинного обучения Azure][10]

> [!IMPORTANT]
> <span data-ttu-id="0a71a-350">В примерах запросов на извлечение и выборку данных для моделирования, указанных в предыдущих разделах, **все метки для трех упражнений по моделированию включены в запрос**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-350">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="0a71a-351">Важным (обязательным) шагом каждого из упражнений по моделированию является **исключение** ненужных меток для двух остальных задач, а также любых **целевых утечек**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-351">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="0a71a-352">Например, при двоичной классификации используйте метку **tipped** и исключите поля **tip\_class**, **tip\_amount** и **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="0a71a-352">For e.g., when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="0a71a-353">Последние являются целевыми утечками, поскольку подразумевают, что чаевые выплачены.</span><span class="sxs-lookup"><span data-stu-id="0a71a-353">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="0a71a-354">Чтобы исключить ненужные столбцы и/или целевые утечки, можно воспользоваться модулем [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных) или [Edit Metadata][edit-metadata] (Изменение метаданных).</span><span class="sxs-lookup"><span data-stu-id="0a71a-354">To exclude unnecessary columns and/or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="0a71a-355">Дополнительные сведения см. на страницах справки модулей [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных) и [Edit Metadata][edit-metadata] (Изменение метаданных).</span><span class="sxs-lookup"><span data-stu-id="0a71a-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="0a71a-356"><a name="mldeploy"></a>Развертывание моделей в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="0a71a-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="0a71a-357">Когда модель готова, ее можно легко развернуть в виде веб-службы непосредственно из эксперимента.</span><span class="sxs-lookup"><span data-stu-id="0a71a-357">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="0a71a-358">Дополнительные сведения см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0a71a-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="0a71a-359">Чтобы развернуть новую веб-службу, необходимо выполнить такие действия.</span><span class="sxs-lookup"><span data-stu-id="0a71a-359">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="0a71a-360">Создать эксперимент по количественной оценке.</span><span class="sxs-lookup"><span data-stu-id="0a71a-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="0a71a-361">Развернуть веб-службу.</span><span class="sxs-lookup"><span data-stu-id="0a71a-361">Deploy the web service.</span></span>

<span data-ttu-id="0a71a-362">Чтобы создать оценивающий эксперимент на основе учебного эксперимента со статусом **Завершено**, щелкните **Create scoring experiment** (Создать оценивающий эксперимент) на нижней панели действий.</span><span class="sxs-lookup"><span data-stu-id="0a71a-362">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Система оценок Azure][18]

<span data-ttu-id="0a71a-364">Служба машинного обучения Azure попытается создать эксперимент по количественной оценке на основе компонентов учебного эксперимента.</span><span class="sxs-lookup"><span data-stu-id="0a71a-364">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="0a71a-365">В частности, она:</span><span class="sxs-lookup"><span data-stu-id="0a71a-365">In particular, it will:</span></span>

1. <span data-ttu-id="0a71a-366">Сохранит обученную модель и удалит модули обучения модели.</span><span class="sxs-lookup"><span data-stu-id="0a71a-366">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="0a71a-367">Идентифицирует логический **порт ввода** для представления ожидаемой схемы входных данных.</span><span class="sxs-lookup"><span data-stu-id="0a71a-367">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="0a71a-368">Идентифицирует логический **порт вывода** для представления ожидаемой схемы вывода веб-службы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-368">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="0a71a-369">При создании эксперимента по количественной оценке просмотрите его и скорректируйте по необходимости.</span><span class="sxs-lookup"><span data-stu-id="0a71a-369">When the scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="0a71a-370">Типичной корректировкой является замена входного набора данных и/или запроса таким, который исключает поля меток, поскольку они не будут доступны при вызове службы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-370">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="0a71a-371">Также рекомендуется уменьшить размер входного набора данных и/или запроса до нескольких записей, которых достаточно для обозначения входной схемы.</span><span class="sxs-lookup"><span data-stu-id="0a71a-371">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="0a71a-372">Для порта вывода зачастую исключаются все входные поля и в вывод включаются только **Scored Labels** (Оцененные метки) и **Scored Probabilities** (Оцененные вероятности) с помощью модуля [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных).</span><span class="sxs-lookup"><span data-stu-id="0a71a-372">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="0a71a-373">Образец эксперимента по количественной оценке показан на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="0a71a-373">A sample scoring experiment is in the figure below.</span></span> <span data-ttu-id="0a71a-374">Когда все будет готово к развертыванию, нажмите кнопку **ОПУБЛИКОВАТЬ ВЕБ-СЛУЖБУ** на нижней панели действий.</span><span class="sxs-lookup"><span data-stu-id="0a71a-374">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Публикация в Машинном обучении Azure][11]

<span data-ttu-id="0a71a-376">Итак, в этом пошаговом руководстве мы создали среду обработки данных, работали с большим общедоступным набором данных на протяжении всего процесса от получения данных до обучения модели и развертывания веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="0a71a-376">To recap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all the way from data acquisition to model training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="0a71a-377">Сведения о лицензии</span><span class="sxs-lookup"><span data-stu-id="0a71a-377">License Information</span></span>
<span data-ttu-id="0a71a-378">Этот образец пошагового руководства и сопровождающие его сценарии и файлы IPython Notebook предоставлены корпорацией Майкрософт на условиях лицензии MIT.</span><span class="sxs-lookup"><span data-stu-id="0a71a-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="0a71a-379">Дополнительные сведения см. в файле LICENSE.txt в каталоге примеров кода на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a71a-379">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="0a71a-380">Ссылки</span><span class="sxs-lookup"><span data-stu-id="0a71a-380">References</span></span>
<span data-ttu-id="0a71a-381">•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="0a71a-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="0a71a-382">•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="0a71a-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="0a71a-383">•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="0a71a-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
