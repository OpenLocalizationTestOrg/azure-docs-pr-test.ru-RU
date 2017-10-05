---
title: "Процесс обработки и анализа данных группы на практике: использование хранилища данных SQL | Документация Майкрософт"
description: "Расширенный процесс аналитики и технологии в действии"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: ce7de48af0f2f21576c66a962b88635a0f9f8333
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="a4ba2-103">Процесс обработки и анализа данных группы на практике: использование хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a4ba2-103">The Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="a4ba2-104">В этом руководстве описаны шаги по созданию и развертыванию модели машинного обучения с использованием хранилища данных SQL для общедоступного набора данных [Поездки такси Нью-Йорка](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="a4ba2-105">Модель двоичной классификации позволяет спрогнозировать получение чаевых за поездку. Кроме того, здесь рассматриваются модели многоклассовой классификации и регрессии, которые помогают спрогнозировать распространение сумм чаевых, оплачиваемых за поездку.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-105">The binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict the distribution for the tip amounts paid.</span></span>

<span data-ttu-id="a4ba2-106">Ниже представлена процедура рабочего процесса [обработки и анализа данных группы (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) .</span><span class="sxs-lookup"><span data-stu-id="a4ba2-106">The procedure follows the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="a4ba2-107">Здесь мы покажем, как настроить среду обработки и анализа данных, загрузить данные в хранилище SQL, а также изучить данные с помощью хранилища данных SQL и IPython Notebook и спроектировать признаки в модель.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-107">We show how to setup a data science environment, how to load the data into SQL DW, and how use either SQL DW or an IPython Notebook to explore the data and engineer features to model.</span></span> <span data-ttu-id="a4ba2-108">Затем мы рассмотрим, как создать и развернуть модель в службе машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-108">We then show how to build and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="a4ba2-109"><a name="dataset"></a>Набор данных "Поездки такси Нью-Йорка"</span><span class="sxs-lookup"><span data-stu-id="a4ba2-109"><a name="dataset"></a>The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="a4ba2-110">Данные о поездках такси Нью-Йорка содержатся в сжатых CSV-файлах размером около 20 ГБ (примерно 48 ГБ в несжатом виде), которые включают в себя сведения о более 173 млн отдельных поездок и платежах за каждую поездку.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-110">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="a4ba2-111">В каждой записи о поездке содержатся данные о расположении пунктов посадки и высадки, а также времени, анонимизированный номер лицензии водителя и номер медальона (уникальный идентификатор такси).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-111">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="a4ba2-112">Данные включают в себя все поездки за 2013 год и предоставляются в виде следующих двух наборов данных за каждый месяц:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="a4ba2-113">CSV-файл **trip_data.csv** содержит подробные сведения о поездке, например число пассажиров, пункты отправления и назначения, продолжительность поездки и ее расстояние.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-113">The **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="a4ba2-114">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="a4ba2-115">CSV-файл **trip_fare** содержит подробные сведения об оплате каждой поездки, такие как тип оплаты, сумма тарифа, надбавка и налоги, чаевые и пошлины, а также общая выплаченная сумма.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-115">The **trip_fare.csv** file contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="a4ba2-116">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="a4ba2-117">**Уникальный ключ** для соединения trip\_data и trip\_fare состоит из следующих трех полей:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-117">The **unique key** used to join trip\_data and trip\_fare is composed of the following three fields:</span></span>

* <span data-ttu-id="a4ba2-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="a4ba2-118">medallion,</span></span>
* <span data-ttu-id="a4ba2-119">hack\_license и</span><span class="sxs-lookup"><span data-stu-id="a4ba2-119">hack\_license and</span></span>
* <span data-ttu-id="a4ba2-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-120">pickup\_datetime.</span></span>

## <span data-ttu-id="a4ba2-121"><a name="mltasks"></a>Определение трех типов задач прогнозирования</span><span class="sxs-lookup"><span data-stu-id="a4ba2-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="a4ba2-122">На основе *tip\_amount* мы сформулировали три проблемы прогнозирования, чтобы проиллюстрировать три типа задач моделирования.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-122">We formulate three prediction problems based on the *tip\_amount* to illustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="a4ba2-123">**Двоичная классификация:** спрогнозировать, были ли оставлены чаевые после поездки, т. е. значение *tip\_amount* больше 0 $ является позитивным примером, а значение *tip\_amount* 0 $ является негативным примером.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-123">**Binary classification**: To predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="a4ba2-124">**Мультиклассовая классификация**: спрогнозировать диапазон суммы чаевых за поездку.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-124">**Multiclass classification**: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="a4ba2-125">Мы разделяем *tip\_amount* на пять ячеек или классов:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="a4ba2-126">**Задача регрессии**: спрогнозировать сумму чаевых, выплаченных за поездку.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-126">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="a4ba2-127"><a name="setup"></a>Настройка среды обработки и анализа данных Azure для расширенной аналитики</span><span class="sxs-lookup"><span data-stu-id="a4ba2-127"><a name="setup"></a>Set up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="a4ba2-128">Чтобы настроить среду обработки и анализа данных в Azure, выполните следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-128">To set up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="a4ba2-129">**Создайте собственную учетную запись хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="a4ba2-130">Во время подготовки своего хранилища BLOB-объектов Azure выберите географическое расположение как можно ближе к **юго-центральной части США**, где будут храниться данные о такси Нью-Йорка.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible to **South Central US**, which is where the NYC Taxi data is stored.</span></span> <span data-ttu-id="a4ba2-131">С помощью AzCopy данные будут скопированы из контейнера общедоступного хранилища BLOB-объектов в контейнер в вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-131">The data will be copied using AzCopy from the public blob storage container to a container in your own storage account.</span></span> <span data-ttu-id="a4ba2-132">Чем ближе хранилище BLOB-объектов Azure к юго-центральной части США, тем быстрее будет выполнена эта задача (шаг 4).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-132">The closer your Azure blob storage is to South Central US, the faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="a4ba2-133">Чтобы создать учетную запись хранения Azure, выполните шаги, описанные в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-133">To create your own Azure storage account, follow the steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="a4ba2-134">Убедитесь, что вы записали значения данных учетной записи хранения, так как они потребуются позже в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-134">Be sure to make notes on the values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="a4ba2-135">**Имя учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="a4ba2-136">**Ключ учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="a4ba2-137">**Имя контейнера** (контейнер в хранилище BLOB-объектов Azure, где будут храниться данные)</span><span class="sxs-lookup"><span data-stu-id="a4ba2-137">**Container Name** (which you want the data to be stored in the Azure blob storage)</span></span>

<span data-ttu-id="a4ba2-138">**Подготовьте экземпляр хранилища данных SQL Azure.**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="a4ba2-139">Во время его подготовки следуйте инструкциям в статье [Создание хранилища данных SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) .</span><span class="sxs-lookup"><span data-stu-id="a4ba2-139">Follow the documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) to provision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="a4ba2-140">Убедитесь, что записали учетные данные хранилища данных SQL, так как они потребуются на следующих шагах:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-140">Make sure that you make notations on the following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="a4ba2-141">**Имя сервера**: <server Name>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="a4ba2-142">**имя (базы данных) хранилища данных SQL;**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="a4ba2-143">**Имя пользователя**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-143">**Username**</span></span>
* <span data-ttu-id="a4ba2-144">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-144">**Password**</span></span>

<span data-ttu-id="a4ba2-145">**Установите Visual Studio и SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="a4ba2-146">Инструкции можно найти в статье [Установка Visual Studio 2015 и SSDT для хранилища данных SQL](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="a4ba2-147">**Установите подключение к своему хранилищу данных SQL Azure с помощью Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-147">**Connect to your Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="a4ba2-148">Инструкции приведены в шагах 1 и 2 статьи [Подключение к хранилищу данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-148">For instructions, see steps 1 & 2 in [Connect to Azure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a4ba2-149">Выполните следующий SQL-запрос в базе данных, созданной в хранилище данных SQL (вместо запроса, указанного на шаге 3 раздела о подключении), чтобы **создать главный ключ**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-149">Run the following SQL query on the database you created in your SQL Data Warehouse (instead of the query provided in step 3 of the connect topic,) to **create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try to create the master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If the master key exists, do nothing
    END CATCH;

<span data-ttu-id="a4ba2-150">**Создайте рабочую область Машинного обучения Azure, используя подписку Azure.**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="a4ba2-151">Инструкции можно найти в статье [Создание рабочей области машинного обучения Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="a4ba2-152"><a name="getdata"></a>Загрузка данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="a4ba2-152"><a name="getdata"></a>Load the data into SQL Data Warehouse</span></span>
<span data-ttu-id="a4ba2-153">Откройте командную консоль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="a4ba2-154">Выполните следующие команды PowerShell, чтобы скачать файлы примеров сценариев SQL, доступные на сайте GitHub, в локальный каталог, указанный с помощью параметра *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-154">Run the following PowerShell commands to download the example SQL script files that we share with you on GitHub to a local directory that you specify with the parameter *-DestDir*.</span></span> <span data-ttu-id="a4ba2-155">Значение параметра *-DestDir* можно изменить и указать любой другой локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-155">You can change the value of parameter *-DestDir* to any local directory.</span></span> <span data-ttu-id="a4ba2-156">Если *-DestDir* отсутствует, он будет создан в рамках сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-156">If *-DestDir* does not exist, it will be created by the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="a4ba2-157">При выполнении следующего сценария PowerShell может потребоваться **запуск от имени администратора** , если для создания каталога *DestDir* или записи в него нужны права администратора.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-157">You might need to **Run as Administrator** when executing the following PowerShell script if your *DestDir* directory needs Administrator privilege to create or to write to it.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="a4ba2-158">После успешного выполнения текущий рабочий каталог изменится на *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-158">After successful execution, your current working directory changes to *-DestDir*.</span></span> <span data-ttu-id="a4ba2-159">Должен отобразиться экран, аналогичный показанному ниже:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-159">You should be able to see screen like below:</span></span>

![][19]

<span data-ttu-id="a4ba2-160">В каталоге *-DestDir*выполните следующий сценарий PowerShell в режиме администратора:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-160">In your *-DestDir*, execute the following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="a4ba2-161">При первом выполнении сценария PowerShell будет предложено ввести данные хранилища данных SQL Azure и учетной записи хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-161">When the PowerShell script runs for the first time, you will be asked to input the information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="a4ba2-162">После первого завершения этого сценария PowerShell введенные учетные данные будут записаны в файл конфигурации SQLDW.conf в используемом рабочем каталоге.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-162">When this PowerShell script completes running for the first time, the credentials you input will have been written to a configuration file SQLDW.conf in the present working directory.</span></span> <span data-ttu-id="a4ba2-163">При последующем запуске этого файла сценария PowerShell можно будет считать все необходимые параметры из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-163">The future run of this PowerShell script file has the option to read all needed parameters from this configuration file.</span></span> <span data-ttu-id="a4ba2-164">Если некоторые параметры нужно изменить, их можно ввести на экране, когда отобразится запрос. Для этого нужно удалить файл конфигурации и ввести значения параметров по запросу. Кроме того, значения параметров можно изменить в файле SQLDW.conf в каталоге *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-164">If you need to change some parameters, you can choose to input the parameters on the screen upon prompt by deleting this configuration file and inputting the parameters values as prompted or to change the parameter values by editing the SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="a4ba2-165">Чтобы избежать конфликтов имени схемы с именами, которые уже есть в хранилище данных SQL Azure, при каждом запуске во время чтения параметров из файла SQLDW.conf к имени схемы добавляется случайное число из 3 цифр. Затем это имя используется по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-165">In order to avoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from the SQLDW.conf file, a 3-digit random number is added to the schema name from the SQLDW.conf file as the default schema name for each run.</span></span> <span data-ttu-id="a4ba2-166">Сценарий PowerShell может запросить имя схемы. Имя указывается по усмотрению пользователя.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-166">The PowerShell script may prompt you for a schema name: the name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="a4ba2-167">Запуск этого файла **сценария PowerShell** предусматривает выполнение следующих задач:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-167">This **PowerShell script** file completes the following tasks:</span></span>

* <span data-ttu-id="a4ba2-168">**Скачивание и установка AzCopy**, если она еще не установлена.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="a4ba2-169">**Копирование данных в учетную запись частного хранилища BLOB-объектов** из общедоступного BLOB-объекта с помощью AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-169">**Copies data to your private blob storage account** from the public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob to yo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account to verify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob to your storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="a4ba2-170">**Загрузка данных с помощью Polybase (путем выполнения LoadDataToSQLDW.sql) в хранилище данных SQL Azure** из вашей учетной записи частного хранилища BLOB-объектов c помощью следующих команд.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) to your Azure SQL DW** from your private blob storage account with the following commands.</span></span>
  
  * <span data-ttu-id="a4ba2-171">Создание схемы</span><span class="sxs-lookup"><span data-stu-id="a4ba2-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="a4ba2-172">Создание учетных данных для определенной базы данных</span><span class="sxs-lookup"><span data-stu-id="a4ba2-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="a4ba2-173">Создание внешнего источника данных для BLOB-объекта хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a4ba2-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="a4ba2-174">Создание формата внешнего файла для CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="a4ba2-175">Данные не сжимаются, а поля разделяются символом вертикальной черты.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-175">Data is uncompressed and fields are separated with the pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="a4ba2-176">Создание внешних таблиц (trip и fare) для хранения набора данных такси Нью-Йорка в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="a4ba2-177">Загрузка данных из внешних таблиц хранилища BLOB-объектов Azure в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-177">Load data from external tables in Azure blob storage to SQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="a4ba2-178">Создание примера таблицы данных (NYCTaxi_Sample) и вставка данных из него. Предполагает выбор SQL-запросов на таблицы trip и fare.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-178">Create a sample data table (NYCTaxi_Sample) and insert data to it from selecting SQL queries on the trip and fare tables.</span></span> <span data-ttu-id="a4ba2-179">(Этот пример таблицы необходимо будет использовать при выполнении некоторых шагов этого руководства.)</span><span class="sxs-lookup"><span data-stu-id="a4ba2-179">(Some steps of this walkthrough needs to use this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="a4ba2-180">Географическое расположение учетных записей хранения влияет на время загрузки.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-180">The geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="a4ba2-181">От географического расположения учетной записи частного хранилища BLOB-объектов зависит длительность копирования данных из учетной записи общедоступного хранилища в учетную запись частного хранилища. Оно может длиться дольше 15 минут. Загрузка данных из учетной записи хранения в хранилище данных SQL Azure может занимать больше 20 минут.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-181">Depending on the geographical location of your private blob storage account, the process of copying data from a public blob to your private storage account can take about 15 minutes, or even longer,and the process of loading data from your storage account to your Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="a4ba2-182">Необходимо решить, какие действия предпринимать, если исходные и конечные файлы совпадают.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-182">You will have to decide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="a4ba2-183">Если CSV-файлы, копируемые из общедоступного хранилища BLOB-объектов в учетную запись частного хранилища BLOB-объектов, уже существуют в учетной записи частного хранилища BLOB-объектов, AzCopy выведет запрос на их перезапись.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-183">If the .csv files to be copied from the public blob storage to your private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want to overwrite them.</span></span> <span data-ttu-id="a4ba2-184">Если перезаписывать их не нужно, введите **n**, когда появится соответствующий запрос.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-184">If you do not want to overwrite them, input **n** when prompted.</span></span> <span data-ttu-id="a4ba2-185">Чтобы перезаписать **все** файлы, по запросу системы введите **a**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-185">If you want to overwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="a4ba2-186">Чтобы перезаписать отдельные CSV-файлы, по запросу системы введите **y** .</span><span class="sxs-lookup"><span data-stu-id="a4ba2-186">You can also input **y** to overwrite .csv files individually.</span></span>
> 
> 

![График № 21][21]

<span data-ttu-id="a4ba2-188">Можно использовать собственные данные.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-188">You can use your own data.</span></span> <span data-ttu-id="a4ba2-189">Если данные находятся на локальном компьютере в работающем приложении, AzCopy можно использовать для передачи локальных данных в частное хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy to upload on-premises data to your private Azure blob storage.</span></span> <span data-ttu-id="a4ba2-190">Для этого в команде AzCopy в файле скрипта PowerShell необходимо лишь изменить расположение **источника** `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, указав для него локальный каталог, содержащий данные.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-190">You only need to change the **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in the AzCopy command of the PowerShell script file to the local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="a4ba2-191">Если данные уже размещены в частном хранилище BLOB-объектов Azure в работающем приложении, шаг AzCopy в сценарии PowerShell можно пропустить и напрямую загрузить данные в хранилище данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-191">If your data is already in your private Azure blob storage in your real life application, you can skip the AzCopy step in the PowerShell script and directly upload the data to Azure SQL DW.</span></span> <span data-ttu-id="a4ba2-192">В сценарий потребуется внести дополнительные изменения, чтобы настроить его согласно формату данных.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-192">This will require additional edits of the script to tailor it to the format of your data.</span></span>
> 
> 

<span data-ttu-id="a4ba2-193">Этот сценарий Powershell также предусматривает использование сведений хранилища данных SQL Azure в файлах примеров исследований данных SQLDW_Explorations.sql, SQLDW_Explorations.ipynb и SQLDW_Explorations_Scripts.py. Таким образом эти три файла можно использовать сразу же по завершении сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-193">This Powershell script also plugs in the Azure SQL DW information into the data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready to be tried out instantly after the PowerShell script completes.</span></span>

<span data-ttu-id="a4ba2-194">После успешного выполнения вы увидите экран, аналогичный этому:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="a4ba2-195"><a name="dbexplore"></a>Изучение данных и проектирование признаков в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="a4ba2-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a4ba2-196">В этом разделе мы исследуем данные и создадим признаки, используя SQL-запросы для хранилища данных SQL Azure с помощью **средств работы с данными Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="a4ba2-197">Все SQL-запросы, используемые в этом разделе, можно найти в примере скрипта *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-197">All SQL queries used in this section can be found in the sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="a4ba2-198">Этот файл скачан в локальный каталог во время выполнения сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-198">This file has already been downloaded to your local directory by the PowerShell script.</span></span> <span data-ttu-id="a4ba2-199">Кроме того, его также можно получить на сайте [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="a4ba2-200">Но в файл с сайта GitHub не включены данные хранилища SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-200">But the file in GitHub does not have the Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="a4ba2-201">Подключитесь к хранилищу данных SQL Azure с помощью Visual Studio, используя имя входа и пароль хранилища данных SQL, и откройте **обозреватель объектов SQL** для подтверждения импорта базы данных и таблиц.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-201">Connect to your Azure SQL DW using Visual Studio with the SQL DW login name and password and open up the **SQL Object Explorer** to confirm the database and tables have been imported.</span></span> <span data-ttu-id="a4ba2-202">Получите файл *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-202">Retrieve the *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="a4ba2-203">Чтобы открыть редактор запросов хранилища параллельных данных (PDW), используйте команду **New Query**, выбрав PDW в **обозревателе объектов SQL**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-203">To open a Parallel Data Warehouse (PDW) query editor, use the **New Query** command while your PDW is selected in the **SQL Object Explorer**.</span></span> <span data-ttu-id="a4ba2-204">PDW не поддерживает стандартный редактор SQL-запросов.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-204">The standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="a4ba2-205">В этом разделе мы выполним следующие задачи по исследованию данных и созданию признаков.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-205">Here are the type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="a4ba2-206">Просмотрим распределение данных по нескольким полям в различных временных окнах.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="a4ba2-207">Исследуем качество данных по полям долготы и широты.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="a4ba2-208">Создадим метки двоичной и мультиклассовой классификации на основе **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="a4ba2-209">Создадим характеристики и вычислим/сравним расстояния поездок.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="a4ba2-210">Соединим две таблицы и извлечем случайную выборку, которая послужит основой для построения моделей.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="a4ba2-211">Проверка импорта данных</span><span class="sxs-lookup"><span data-stu-id="a4ba2-211">Data import verification</span></span>
<span data-ttu-id="a4ba2-212">Эти запросы обеспечивают быструю проверку числа строк и столбцов в таблицах, заполненных ранее с помощью параллельного массового импорта Polybase.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-212">These queries provide a quick verification of the number of rows and columns in the tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="a4ba2-213">**Выходные данные.** Вы должны получить 173 179 759 строк и 14 столбцов.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="a4ba2-214">Просмотр: Распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="a4ba2-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="a4ba2-215">В этом примере запроса определяются медальоны (номера) такси, которые осуществили больше 100 поездок за заданный период времени.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-215">This example query identifies the medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="a4ba2-216">Запрос будет использовать секционированный доступ к таблице, так как он обусловлен схемой секционирования **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-216">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="a4ba2-217">При запросе к полному набору данных также будет задействовано сканирование секционированной таблицы и/или индекса.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-217">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="a4ba2-218">**Выходные данные.** По результатам запроса возвращается таблица, строки которой содержат 13 369 медальонов (номеров такси) и количество поездок, осуществленных ими за 2013 год.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-218">**Output:** The query should return a table with rows specifying the 13,369 medallions (taxis) and the number of trip completed by them in 2013.</span></span> <span data-ttu-id="a4ba2-219">В последнем столбце отображается счетчик поездок.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-219">The last column contains the count of the number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="a4ba2-220">Просмотр: распределение поездок по параметрам medallion и hack_license</span><span class="sxs-lookup"><span data-stu-id="a4ba2-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="a4ba2-221">В этом примере определяются медальоны (номера) такси и номера hack_license (лицензий) водителей, которые осуществили больше 100 поездок за заданный период времени.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-221">This example identifies the medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="a4ba2-222">**Выходные данные.** По результатам запроса возвращается таблица, в 13 369 строках которой перечислены 13 369 автомобилей (водителей), осуществивших в 2013 году более 100 поездок.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-222">**Output:** The query should return a table with 13,369 rows specifying the 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="a4ba2-223">В последнем столбце отображается счетчик поездок.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-223">The last column contains the count of the number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="a4ba2-224">Оценка качества данных: проверка записей с неправильными значениями долготы и/или широты</span><span class="sxs-lookup"><span data-stu-id="a4ba2-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="a4ba2-225">В этом примере анализируется, содержится ли в каких-либо полях долготы и/или широты неверное значение (количество градусов должно быть в пределах от -90 до 90) или значение координат (0, 0).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-225">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="a4ba2-226">**Выходные данные.** По результатам запроса возвращаются 837 467 поездок с недопустимыми значениями долготы и (или) широты.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-226">**Output:** The query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="a4ba2-227">Изучение: распределение поездок с чаевыми и без чаевых</span><span class="sxs-lookup"><span data-stu-id="a4ba2-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="a4ba2-228">В этом примере пользователь узнает о соотношении количества поездок, когда водителю дали на чай, к количеству поездок, когда чаевых не было (пользователь ищет сведения за определенный период времени или, если нужны сведения за полный год, во всех данных набора).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-228">This example finds the number of trips that were tipped vs. the number that were not tipped in a specified time period (or in the full dataset if covering the full year as it is set up here).</span></span> <span data-ttu-id="a4ba2-229">Это распределение отражает распределение двоичных меток, которые в дальнейшем будут использоваться для моделирования двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-229">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="a4ba2-230">**Выходные данные.** По результатам запроса возвращаются следующие результаты по частотности чаевых за 2013 год: 90 447 622 поездок с чаевыми и 82 264 709 — без чаевых.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-230">**Output:** The query should return the following tip frequencies for the year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="a4ba2-231">Изучение: распределение классов и диапазонов чаевых</span><span class="sxs-lookup"><span data-stu-id="a4ba2-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="a4ba2-232">В этом примере вычисляется распределение диапазонов чаевых за заданный период времени (или по полному набору данных в случае охвата целого года).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-232">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="a4ba2-233">Это распределение классов меток, которое в дальнейшем будет использоваться для моделирования мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-233">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="a4ba2-234">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="a4ba2-234">**Output:**</span></span>

| <span data-ttu-id="a4ba2-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="a4ba2-235">tip_class</span></span> | <span data-ttu-id="a4ba2-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="a4ba2-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="a4ba2-237">1</span><span class="sxs-lookup"><span data-stu-id="a4ba2-237">1</span></span> |<span data-ttu-id="a4ba2-238">82230915</span><span class="sxs-lookup"><span data-stu-id="a4ba2-238">82230915</span></span> |
| <span data-ttu-id="a4ba2-239">2</span><span class="sxs-lookup"><span data-stu-id="a4ba2-239">2</span></span> |<span data-ttu-id="a4ba2-240">6198803</span><span class="sxs-lookup"><span data-stu-id="a4ba2-240">6198803</span></span> |
| <span data-ttu-id="a4ba2-241">3</span><span class="sxs-lookup"><span data-stu-id="a4ba2-241">3</span></span> |<span data-ttu-id="a4ba2-242">1932223</span><span class="sxs-lookup"><span data-stu-id="a4ba2-242">1932223</span></span> |
| <span data-ttu-id="a4ba2-243">0</span><span class="sxs-lookup"><span data-stu-id="a4ba2-243">0</span></span> |<span data-ttu-id="a4ba2-244">82264625</span><span class="sxs-lookup"><span data-stu-id="a4ba2-244">82264625</span></span> |
| <span data-ttu-id="a4ba2-245">4</span><span class="sxs-lookup"><span data-stu-id="a4ba2-245">4</span></span> |<span data-ttu-id="a4ba2-246">85765</span><span class="sxs-lookup"><span data-stu-id="a4ba2-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="a4ba2-247">Изучение: вычисление и сравнение расстояния поездок</span><span class="sxs-lookup"><span data-stu-id="a4ba2-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="a4ba2-248">В этом примере значения долготы и широты начальных и конечных пунктов поездок преобразуются в географические точки SQL, вычисляется расстояние поездки по разности географических точек и возвращается случайная выборка результатов для сравнения.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-248">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="a4ba2-249">В примере результаты ограничиваются только допустимыми координатами с помощью запроса оценки качества данных, описанного ранее.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-249">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function to calculate the direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="a4ba2-250">Проектирование признаков с помощью функций SQL</span><span class="sxs-lookup"><span data-stu-id="a4ba2-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="a4ba2-251">Иногда функции SQL могут быть полезны при проектировании признаков.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="a4ba2-252">В этом пошаговом руководстве мы определили функцию SQL для расчета прямого расстояния между расположениями посадки и высадки.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-252">In this walkthrough, we defined a SQL function to calculate the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="a4ba2-253">Описанные ниже сценарии SQL можно выполнять в **средствах Visual Studio для работы с данными**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-253">You can run the following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="a4ba2-254">Вот сценарий SQL для определения функции расстояния:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-254">Here is the SQL script that defines the distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate the direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="a4ba2-255">Вот пример вызова этой функции в SQL-запросе для создания признаков:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-255">Here is an example to call this function to generate features in your SQL query:</span></span>

    -- Sample query to call the function to create features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="a4ba2-256">**Выходные данные.** По результатам запроса формируется таблица (из 2 803 538 строк) с координатами посадки и высадки пассажиров и дальностью поездок в милях.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and the corresponding direct distances in miles.</span></span> <span data-ttu-id="a4ba2-257">Вот результаты для первых трех строк:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-257">Here are the results for first 3 rows:</span></span>

|  | <span data-ttu-id="a4ba2-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="a4ba2-258">pickup_latitude</span></span> | <span data-ttu-id="a4ba2-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="a4ba2-259">pickup_longitude</span></span> | <span data-ttu-id="a4ba2-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="a4ba2-260">dropoff_latitude</span></span> | <span data-ttu-id="a4ba2-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="a4ba2-261">dropoff_longitude</span></span> | <span data-ttu-id="a4ba2-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="a4ba2-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="a4ba2-263">1</span><span class="sxs-lookup"><span data-stu-id="a4ba2-263">1</span></span> |<span data-ttu-id="a4ba2-264">40,731804</span><span class="sxs-lookup"><span data-stu-id="a4ba2-264">40.731804</span></span> |<span data-ttu-id="a4ba2-265">–74,001083</span><span class="sxs-lookup"><span data-stu-id="a4ba2-265">-74.001083</span></span> |<span data-ttu-id="a4ba2-266">40,736622</span><span class="sxs-lookup"><span data-stu-id="a4ba2-266">40.736622</span></span> |<span data-ttu-id="a4ba2-267">–73,988953</span><span class="sxs-lookup"><span data-stu-id="a4ba2-267">-73.988953</span></span> |<span data-ttu-id="a4ba2-268">0,7169601222</span><span class="sxs-lookup"><span data-stu-id="a4ba2-268">.7169601222</span></span> |
| <span data-ttu-id="a4ba2-269">2</span><span class="sxs-lookup"><span data-stu-id="a4ba2-269">2</span></span> |<span data-ttu-id="a4ba2-270">40,715794</span><span class="sxs-lookup"><span data-stu-id="a4ba2-270">40.715794</span></span> |<span data-ttu-id="a4ba2-271">–74,010635</span><span class="sxs-lookup"><span data-stu-id="a4ba2-271">-74,010635</span></span> |<span data-ttu-id="a4ba2-272">40,725338</span><span class="sxs-lookup"><span data-stu-id="a4ba2-272">40.725338</span></span> |<span data-ttu-id="a4ba2-273">–74,00399</span><span class="sxs-lookup"><span data-stu-id="a4ba2-273">-74.00399</span></span> |<span data-ttu-id="a4ba2-274">0,7448343721</span><span class="sxs-lookup"><span data-stu-id="a4ba2-274">.7448343721</span></span> |
| <span data-ttu-id="a4ba2-275">3</span><span class="sxs-lookup"><span data-stu-id="a4ba2-275">3</span></span> |<span data-ttu-id="a4ba2-276">40,761456</span><span class="sxs-lookup"><span data-stu-id="a4ba2-276">40.761456</span></span> |<span data-ttu-id="a4ba2-277">–73,999886</span><span class="sxs-lookup"><span data-stu-id="a4ba2-277">-73.999886</span></span> |<span data-ttu-id="a4ba2-278">40,766544</span><span class="sxs-lookup"><span data-stu-id="a4ba2-278">40.766544</span></span> |<span data-ttu-id="a4ba2-279">–73,988228</span><span class="sxs-lookup"><span data-stu-id="a4ba2-279">-73.988228</span></span> |<span data-ttu-id="a4ba2-280">0,7037227967</span><span class="sxs-lookup"><span data-stu-id="a4ba2-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="a4ba2-281">Подготовка данных для построения модели</span><span class="sxs-lookup"><span data-stu-id="a4ba2-281">Prepare data for model building</span></span>
<span data-ttu-id="a4ba2-282">Следующий запрос соединяет таблицы **nyctaxi\_trip** и **nyctaxi\_fare**, создает метку двоичной классификации **tipped**, метку многоклассовой классификации **tip\_class**, а также извлекает выборку из полного соединенного набора данных.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-282">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from the full joined dataset.</span></span> <span data-ttu-id="a4ba2-283">Выборка предполагает получение подмножества поездок на основе данных времени посадок.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-283">The sampling is done by retrieving a subset of the trips based on pickup time.</span></span>  <span data-ttu-id="a4ba2-284">Этот запрос можно скопировать, а затем вставить непосредственно в модуль [Импорт данных](https://studio.azureml.net) [Студии машинного обучения Azure][import-data] для прямого приема данных из экземпляра базы данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-284">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL database instance in Azure.</span></span> <span data-ttu-id="a4ba2-285">Запрос исключает записи с неверными (0, 0) координатами.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-285">The query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="a4ba2-286">Когда вы будете готовы перейти к машинному обучению Azure, вы можете:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-286">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="a4ba2-287">Сохранить окончательный SQL-запрос для извлечения и выборки данных, скопировать и вставить этот запрос непосредственно в модуль [Импорт данных][import-data] в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-287">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="a4ba2-288">Сохранить выбранные и спроектированные данные, которые планируется использовать для построения модели в новой таблице хранилища данных SQL, и использовать новую таблицу в модуле [Импорт данных][import-data] в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-288">Persist the sampled and engineered data you plan to use for model building in a new SQL DW table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="a4ba2-289">Это уже сделано на одном из предыдущих шагов сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-289">The PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="a4ba2-290">Данные можно считать прямо из этой таблицы в модуле "Импорт данных".</span><span class="sxs-lookup"><span data-stu-id="a4ba2-290">You can read directly from this table in the Import Data module.</span></span>

## <span data-ttu-id="a4ba2-291"><a name="ipnb"></a>Просмотр данных и проектирование характеристик в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="a4ba2-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="a4ba2-292">В этом разделе мы изучим данные и спроектируем признаки, используя как Python, так и SQL-запросы, для созданного ранее хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL DW created earlier.</span></span> <span data-ttu-id="a4ba2-293">Пример файла IPython Notebook с именем **SQLDW_Explorations.ipynb** и файла скрипта Python **SQLDW_Explorations_Scripts.py** скачаны в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded to your local directory.</span></span> <span data-ttu-id="a4ba2-294">Они также доступны на веб-сайте [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="a4ba2-295">В сценариях Python эти два файла идентичны.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="a4ba2-296">Файл сценария Python предоставляется, если нет сервера IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-296">The Python script file is provided to you in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="a4ba2-297">Эти два примера файлов Python предназначены для использования с **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="a4ba2-298">Необходимые данные хранилища данных SQL Azure в примере IPython Notebook и файле сценария Python, скачанные на локальный компьютер, уже включены во время выполнения сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-298">The needed Azure SQL DW information in the sample IPython Notebook and the Python script file downloaded to your local machine has been plugged in by the PowerShell script previously.</span></span> <span data-ttu-id="a4ba2-299">Они выполняются без изменений.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-299">They are executable without any modification.</span></span>

<span data-ttu-id="a4ba2-300">Если ранее вы уже настроили рабочую область Машинного обучения Azure, пример IPython Notebook можно напрямую загрузить в службу IPython Notebook Машинного обучения Azure и там же запустить.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-300">If you have already set up an AzureML workspace, you can directly upload the sample IPython Notebook to the AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="a4ba2-301">Ниже приведены шаги по передаче в службу IPython Notebook Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-301">Here are the steps to upload to AzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="a4ba2-302">Войдите в рабочую область Машинного обучения Azure, щелкните "Студия" в верхней части, а затем — NOTEBOOKS в левой части веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-302">Log in to your AzureML workspace, click "Studio" at the top, and click "NOTEBOOKS" on the left side of the web page.</span></span>
   
    ![График № 22][22]
2. <span data-ttu-id="a4ba2-304">Щелкните вкладку "СОЗДАТЬ" в левом верхнем углу веб-страницы и выберите плитку Python 2.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-304">Click "NEW" on the left bottom corner of the web page, and select "Python 2".</span></span> <span data-ttu-id="a4ba2-305">Затем введите имя для Notebook и щелкните значок галочки для создания пустого IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-305">Then, provide a name to the notebook and click the check mark to create the new blank IPython Notebook.</span></span>
   
    ![График № 23][23]
3. <span data-ttu-id="a4ba2-307">Щелкните символ Jupyter в левом верхнем углу нового IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-307">Click the "Jupyter" symbol on the left top corner of the new IPython Notebook.</span></span>
   
    ![График № 24][24]
4. <span data-ttu-id="a4ba2-309">Перетащите пример IPython Notebook на страницу **дерева** службы IPython Notebook машинного обучения Azure и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-309">Drag and drop the sample IPython Notebook to the **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="a4ba2-310">После этого пример IPython Notebook будет отправлен в службу IPython Notebook Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-310">Then, the sample IPython Notebook will be uploaded to the AzureML IPython Notebook service.</span></span>
   
    ![График № 25][25]

<span data-ttu-id="a4ba2-312">Чтобы запустить пример IPython Notebook или файл сценария Python, необходимо установить следующие пакеты Python.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-312">In order to run the sample IPython Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="a4ba2-313">Если вы используете службу IPython Notebook Машинного обучения Azure, эти пакеты уже установлены.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-313">If you are using the AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="a4ba2-314">pandas</span><span class="sxs-lookup"><span data-stu-id="a4ba2-314">pandas</span></span>
    - <span data-ttu-id="a4ba2-315">numpy</span><span class="sxs-lookup"><span data-stu-id="a4ba2-315">numpy</span></span>
    - <span data-ttu-id="a4ba2-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="a4ba2-316">matplotlib</span></span>
    - <span data-ttu-id="a4ba2-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="a4ba2-317">pyodbc</span></span>
    - <span data-ttu-id="a4ba2-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="a4ba2-318">PyTables</span></span>

<span data-ttu-id="a4ba2-319">Во время создания расширенных аналитических решений с использованием данных больших объемов с помощью Машинного обучения Azure рекомендуется придерживаться такой последовательности действий:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-319">The recommended sequence when building advanced analytical solutions on AzureML with large data is the following:</span></span>

* <span data-ttu-id="a4ba2-320">Считайте небольшую выборку данных во фрейм данных, размещенный в памяти.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-320">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="a4ba2-321">Выполните несколько визуализаций и просмотров с использованием выборки данных.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-321">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="a4ba2-322">Поэкспериментируйте с проектированием характеристик с использованием выборки данных.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-322">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="a4ba2-323">При изучении данных большого объема, манипуляциях с данными и проектировании признаков используйте Python, чтобы напрямую передавать SQL-запросы в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-323">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL DW.</span></span>
* <span data-ttu-id="a4ba2-324">Определите размер выборки, подходящий для создания модели машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-324">Decide the sample size to be suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="a4ba2-325">Ниже приведены несколько примеров изучения данных, визуализации данных и проектирования признаков.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-325">The followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="a4ba2-326">Дополнительные исследования данных можно найти в примере IPython Notebook и файле сценария Python.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-326">More data explorations can be found in the sample IPython Notebook and the sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="a4ba2-327">Инициализация учетных данных базы данных</span><span class="sxs-lookup"><span data-stu-id="a4ba2-327">Initialize database credentials</span></span>
<span data-ttu-id="a4ba2-328">Инициализируйте параметры подключения к базе данных в следующих переменных:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-328">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="a4ba2-329">Создание подключения к базе данных</span><span class="sxs-lookup"><span data-stu-id="a4ba2-329">Create database connection</span></span>
<span data-ttu-id="a4ba2-330">Вот строка, которая создает подключение к базе данных.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-330">Here is the connection string that creates the connection to the database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="a4ba2-331">Сообщение числа строк и столбцов в таблице <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="a4ba2-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="a4ba2-332">Общее число строк = 173179759</span><span class="sxs-lookup"><span data-stu-id="a4ba2-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="a4ba2-333">Общее число столбцов = 14</span><span class="sxs-lookup"><span data-stu-id="a4ba2-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="a4ba2-334">Сообщение числа строк и столбцов в таблице <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="a4ba2-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="a4ba2-335">Общее число строк = 173179759</span><span class="sxs-lookup"><span data-stu-id="a4ba2-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="a4ba2-336">Общее количество столбцов — 11.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-the-sql-data-warehouse-database"></a><span data-ttu-id="a4ba2-337">Считывание небольшой выборки данных из хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a4ba2-337">Read-in a small data sample from the SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="a4ba2-338">Время чтения таблицы выборки — 14,096 495 секунды.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-338">Time to read the sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="a4ba2-339">Количество полученных строк и столбцов — 1000 и 21.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="a4ba2-340">Описательная статистика</span><span class="sxs-lookup"><span data-stu-id="a4ba2-340">Descriptive statistics</span></span>
<span data-ttu-id="a4ba2-341">Теперь все готово для изучения данных выборки.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-341">Now you are ready to explore the sampled data.</span></span> <span data-ttu-id="a4ba2-342">Начнем с рассмотрения описательной статистики для **trip\_distance** (или любых других выбранных полей).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-342">We start with looking at some descriptive statistics for the **trip\_distance** (or any other fields you choose to specify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="a4ba2-343">Визуализация: пример блочной диаграммы</span><span class="sxs-lookup"><span data-stu-id="a4ba2-343">Visualization: Box plot example</span></span>
<span data-ttu-id="a4ba2-344">Далее рассмотрим блочную диаграмму расстояний поездок для визуализации квантилей.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-344">Next we look at the box plot for the trip distance to visualize the quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![График #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="a4ba2-346">Визуализация: пример графика распределения</span><span class="sxs-lookup"><span data-stu-id="a4ba2-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="a4ba2-347">Это график, на котором показано распределение и гистограмма для примеров расстояний выборки.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-347">Plots that visualize the distribution and a histogram for the sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![График #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="a4ba2-349">Визуализация: гистограммы и линейные графики</span><span class="sxs-lookup"><span data-stu-id="a4ba2-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="a4ba2-350">В этом примере мы сегментируем расстояния поездок на пять ячеек и визуализируем результаты сегментирования.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-350">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="a4ba2-351">Мы можем изобразить описанное выше распределение по ячейкам в виде гистограммы или линейного графика, выполнив</span><span class="sxs-lookup"><span data-stu-id="a4ba2-351">We can plot the above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![График #3][3]

<span data-ttu-id="a4ba2-353">и</span><span class="sxs-lookup"><span data-stu-id="a4ba2-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![График #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="a4ba2-355">Визуализация: примеры точечных диаграмм</span><span class="sxs-lookup"><span data-stu-id="a4ba2-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="a4ba2-356">Мы отобразим точечную диаграмму для параметров **trip\_time\_in\_secs** и **trip\_distance**, чтобы проверить возможную корреляцию.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![График #6][6]

<span data-ttu-id="a4ba2-358">Точно также мы можем проверить связь между **rate\_code** и **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-358">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![График #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="a4ba2-360">Изучение выборки данных с помощью SQL-запросов в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="a4ba2-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="a4ba2-361">В этом разделе мы рассмотрим распределение данных с использованием выборки, которая сохранена в созданной ранее таблице.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-361">In this section, we explore data distributions using the sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="a4ba2-362">Обратите внимание, что для подобных исследований можно использовать исходные таблицы.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-362">Note that similar explorations can be performed using the original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-the-sampled-table"></a><span data-ttu-id="a4ba2-363">Исследование: сообщение количества строк и столбцов в таблице выборки</span><span class="sxs-lookup"><span data-stu-id="a4ba2-363">Exploration: Report number of rows and columns in the sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="a4ba2-364">Исследование: распределение поездок с чаевыми и без чаевых</span><span class="sxs-lookup"><span data-stu-id="a4ba2-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="a4ba2-365">Изучение: распределение классов чаевых</span><span class="sxs-lookup"><span data-stu-id="a4ba2-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-the-tip-distribution-by-class"></a><span data-ttu-id="a4ba2-366">Исследование: построение диаграммы классового распределения чаевых</span><span class="sxs-lookup"><span data-stu-id="a4ba2-366">Exploration: Plot the tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![График № 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="a4ba2-368">Исследование: ежедневное распределение поездок</span><span class="sxs-lookup"><span data-stu-id="a4ba2-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="a4ba2-369">Исследование: распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="a4ba2-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="a4ba2-370">Изучение: распределение поездок по медальону и номеру лицензии водителя</span><span class="sxs-lookup"><span data-stu-id="a4ba2-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="a4ba2-371">Просмотр: распределение поездок по времени</span><span class="sxs-lookup"><span data-stu-id="a4ba2-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="a4ba2-372">Изучение: распределение поездок по расстоянию</span><span class="sxs-lookup"><span data-stu-id="a4ba2-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="a4ba2-373">Изучение: распределение поездок по типу оплаты</span><span class="sxs-lookup"><span data-stu-id="a4ba2-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="a4ba2-374">Проверка конечной формы таблицы с признаками</span><span class="sxs-lookup"><span data-stu-id="a4ba2-374">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="a4ba2-375"><a name="mlmodel"></a>Построение моделей в компоненте машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="a4ba2-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="a4ba2-376">Теперь мы готовы перейти к построению и развертыванию модели в [машинном обучении Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-376">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="a4ba2-377">Данные готовы для любой из задач прогнозирования, определенных ранее:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-377">The data is ready to be used in any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="a4ba2-378">**Двоичная классификация**: спрогнозировать, были ли выплачены чаевые за поездку.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-378">**Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="a4ba2-379">**Мультиклассовая классификация**: спрогнозировать диапазон выплаченных чаевых в соответствии с ранее определенными классами.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-379">**Multiclass classification**: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="a4ba2-380">**Задача регрессии**: спрогнозировать сумму чаевых, выплаченных за поездку.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-380">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

<span data-ttu-id="a4ba2-381">Чтобы начать упражнение по моделированию, войдите в рабочую область **Машинного обучения Azure**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-381">To begin the modeling exercise, log in to your **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="a4ba2-382">Если вы еще не создали рабочую область Машинного обучения, см. статью [Создание рабочей области Машинного обучения Azure и предоставление к ней общего доступа](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="a4ba2-383">Чтобы приступить к работе с машинным обучением Azure, см. статью [Что такое студия машинного обучения Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="a4ba2-383">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="a4ba2-384">Войдите в [Студию машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-384">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="a4ba2-385">На главной странице Студии содержится множество информации, видеороликов, учебников, ссылок на справочник модулей и другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-385">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="a4ba2-386">Дополнительные сведения о Машинном обучении Azure см. в [центре документации по машинному обучению Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-386">For more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="a4ba2-387">Типичный обучающий эксперимент предусматривает следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-387">A typical training experiment consists of the following steps:</span></span>

1. <span data-ttu-id="a4ba2-388">Создать **+НОВЫЙ** эксперимент.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="a4ba2-389">Получить данные в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-389">Get the data into Azure ML.</span></span>
3. <span data-ttu-id="a4ba2-390">Предварительно обработать, преобразовать данные и выполнить необходимые манипуляции с ними.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-390">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="a4ba2-391">Создать необходимые характеристики.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-391">Generate features as needed.</span></span>
5. <span data-ttu-id="a4ba2-392">Разбить данные на учебные/проверочные/тестовые наборы данных (или иметь отдельные наборы данных для каждой из этих целей).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-392">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="a4ba2-393">Выбрать один или несколько алгоритмов машинного обучения в зависимости от решаемой задачи обучения.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-393">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="a4ba2-394">Например, двоичная классификация, мультиклассовая классификация, регрессия.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="a4ba2-395">Обучить одну или несколько моделей с помощью учебного набора данных.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-395">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="a4ba2-396">Оценить проверочный набор данных с помощью обученных моделей.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-396">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="a4ba2-397">Вычислить модель (модели) для расчета соответствующих показателей для задачи по обучению.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-397">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="a4ba2-398">Провести тонкую настройку моделей и выбрать лучшую из них для развертывания.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-398">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="a4ba2-399">В этом упражнении мы уже изучили и спроектировали данные в хранилище данных SQL и определились с размером выборки для приема в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-399">In this exercise, we have already explored and engineered the data in SQL Data Warehouse, and decided on the sample size to ingest in Azure ML.</span></span> <span data-ttu-id="a4ba2-400">Вот процедура, позволяющая создать одну или несколько моделей прогнозирования:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-400">Here is the procedure to build one or more of the prediction models:</span></span>

1. <span data-ttu-id="a4ba2-401">Загрузите данные в Машинное обучение Azure, используя модуль [Импорт данных][import-data], доступный в разделе **Data Input and Output** (Ввод и вывод данных).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-401">Get the data into Azure ML using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="a4ba2-402">Дополнительные сведения см. на странице справки модуля [Import Data][import-data] (Импорт данных).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-402">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Модуль "Импорт данных" в Машинном обучении Azure][17]
2. <span data-ttu-id="a4ba2-404">На панели **Properties** (Свойства) в списке **Data source** (Источник данных) выберите **Azure SQL Database** (База данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-404">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="a4ba2-405">Введите DNS-имя базы данных в поле **Имя сервера базы данных** .</span><span class="sxs-lookup"><span data-stu-id="a4ba2-405">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="a4ba2-406">Формат: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="a4ba2-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="a4ba2-407">Введите **Имя базы данных** в соответствующее поле.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-407">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="a4ba2-408">Введите *имя пользователя SQL* в поле **Server user account name** (Имя учетной записи пользователя сервера) и *пароль* в поле **Server user account password** (Пароль учетной записи пользователя сервера).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-408">Enter the *SQL user name* in the **Server user account name**, and the *password* in the **Server user account password**.</span></span>
6. <span data-ttu-id="a4ba2-409">Установите флажок **Accept any server certificate** (Принимать любой сертификат сервера).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-409">Check the **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="a4ba2-410">В текстовой области **Запрос к базе данных** вставьте запрос, который извлекает необходимые поля базы данных (включая возможные вычисляемые поля, например метки) и уменьшает размер выборки данных до требуемого.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-410">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="a4ba2-411">На рисунке ниже показан пример эксперимента по двоичной классификации, в ходе которого происходит чтение данных прямо из базы данных хранилища данных SQL (не забудьте заменить имена таблиц nyctaxi_trip и nyctaxi_fare именами схемы и таблиц, использованными в пошаговом руководстве).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-411">An example of a binary classification experiment reading data directly from the SQL Data Warehouse database is in the figure below (remember to replace the table names nyctaxi_trip and nyctaxi_fare by the schema name and the table names you used in your walkthrough).</span></span> <span data-ttu-id="a4ba2-412">Подобные эксперименты можно сконструировать для задач мультиклассовой классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Чат Машинного обучения Azure][10]

> [!IMPORTANT]
> <span data-ttu-id="a4ba2-414">В примерах запросов на извлечение и выборку данных для моделирования, указанных в предыдущих разделах, **все метки для трех упражнений по моделированию включены в запрос**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-414">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="a4ba2-415">Важным (обязательным) шагом каждого из упражнений по моделированию является **исключение** ненужных меток для двух остальных задач, а также любых **целевых утечек**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-415">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="a4ba2-416">Например, при двоичной классификации используйте метку **tipped** и исключите поля **tip\_class**, **tip\_amount** и **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-416">For example, when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="a4ba2-417">Последние являются целевыми утечками, поскольку подразумевают, что чаевые выплачены.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-417">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="a4ba2-418">Чтобы исключить все ненужные столбцы или целевые утечки, можно воспользоваться модулем [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных) или [Edit Metadata][edit-metadata] (Изменение метаданных).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-418">To exclude any unnecessary columns or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="a4ba2-419">Дополнительные сведения см. на страницах справки модулей [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных) и [Edit Metadata][edit-metadata] (Изменение метаданных).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="a4ba2-420"><a name="mldeploy"></a>Развертывание моделей в службе Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="a4ba2-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="a4ba2-421">Когда модель готова, ее можно легко развернуть в виде веб-службы непосредственно из эксперимента.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-421">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="a4ba2-422">Дополнительные сведения о развертывании веб-служб Azure ML см. в статье [Развертывание веб-службы Машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="a4ba2-423">Чтобы развернуть новую веб-службу, необходимо выполнить такие действия.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-423">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="a4ba2-424">Создать эксперимент по количественной оценке.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="a4ba2-425">Развернуть веб-службу.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-425">Deploy the web service.</span></span>

<span data-ttu-id="a4ba2-426">Чтобы создать оценивающий эксперимент на основе учебного эксперимента со статусом **Завершено**, щелкните **Create scoring experiment** (Создать оценивающий эксперимент) на нижней панели действий.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-426">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Система оценок Azure][18]

<span data-ttu-id="a4ba2-428">Служба машинного обучения Azure попытается создать эксперимент по количественной оценке на основе компонентов учебного эксперимента.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-428">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="a4ba2-429">В частности, она:</span><span class="sxs-lookup"><span data-stu-id="a4ba2-429">In particular, it will:</span></span>

1. <span data-ttu-id="a4ba2-430">Сохранит обученную модель и удалит модули обучения модели.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-430">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="a4ba2-431">Идентифицирует логический **порт ввода** для представления ожидаемой схемы входных данных.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-431">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="a4ba2-432">Идентифицирует логический **порт вывода** для представления ожидаемой схемы вывода веб-службы.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-432">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="a4ba2-433">При создании оценочного эксперимента ознакомьтесь с ним и настройте его должным образом.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-433">When the scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="a4ba2-434">Типичной корректировкой является замена входного набора данных и/или запроса таким, который исключает поля меток, поскольку они не будут доступны при вызове службы.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-434">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="a4ba2-435">Также рекомендуется уменьшить размер входного набора данных и/или запроса до нескольких записей, которых достаточно для обозначения входной схемы.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-435">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="a4ba2-436">Для порта вывода зачастую исключаются все входные поля и в вывод включаются только **Scored Labels** (Оцененные метки) и **Scored Probabilities** (Оцененные вероятности) с помощью модуля [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных).</span><span class="sxs-lookup"><span data-stu-id="a4ba2-436">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="a4ba2-437">Пример оценивающего эксперимента показан на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-437">A sample scoring experiment is provided in the figure below.</span></span> <span data-ttu-id="a4ba2-438">Когда все будет готово к развертыванию, нажмите кнопку **ОПУБЛИКОВАТЬ ВЕБ-СЛУЖБУ** на нижней панели действий.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-438">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Публикация Машинного обучения Azure][11]

## <a name="summary"></a><span data-ttu-id="a4ba2-440">Сводка</span><span class="sxs-lookup"><span data-stu-id="a4ba2-440">Summary</span></span>
<span data-ttu-id="a4ba2-441">Итак, в этом пошаговом руководстве мы создали среду обработки и анализа данных, работали с большим общедоступным набором данных на протяжении всего процесса обработки и анализа данных группы от получения данных до обучения модели и развертывания веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-441">To recap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through the Team Data Science Process, all the way from data acquisition to model training, and then to the deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="a4ba2-442">Сведения о лицензии</span><span class="sxs-lookup"><span data-stu-id="a4ba2-442">License information</span></span>
<span data-ttu-id="a4ba2-443">Этот образец пошагового руководства и сопровождающие его сценарии и файлы IPython Notebook предоставлены корпорацией Майкрософт на условиях лицензии MIT.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="a4ba2-444">Дополнительные сведения см. в файле LICENSE.txt в каталоге примеров кода на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="a4ba2-444">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="a4ba2-445">Ссылки</span><span class="sxs-lookup"><span data-stu-id="a4ba2-445">References</span></span>
<span data-ttu-id="a4ba2-446">•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="a4ba2-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="a4ba2-447">•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="a4ba2-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="a4ba2-448">•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="a4ba2-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
