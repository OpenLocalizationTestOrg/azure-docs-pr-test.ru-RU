---
title: "Hello командного процесса обработки и анализа данных в действии: хранилище данных SQL с помощью | Документы Microsoft"
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
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="48a86-103">Hello командного процесса обработки и анализа данных в действии: с помощью хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="48a86-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="48a86-104">В этом учебнике мы пошаговыми руководствами по сборке и развертывании хранилища данных SQL (хранилища данных SQL) с помощью модели машинного обучения для набора данных общедоступным--hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="48a86-105">Hello модели двоичной классификации, созданной прогнозирует ли совет оплачивается для обработки и для предсказания hello распространения для Оплаченные суммы совет hello также описаны моделей мультиклассовой классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="48a86-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="48a86-106">Привет, ниже представлена процедура Hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="48a86-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="48a86-107">Далее показано, как toosetup среды обработки и анализа данных, как tooload hello данных в хранилища данных SQL, а также использование хранилища данных SQL или ноутбук IPython tooexplore hello данных и инженерам функции toomodel.</span><span class="sxs-lookup"><span data-stu-id="48a86-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="48a86-108">Затем показывается как toobuild и развертывания модели с машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="48a86-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="48a86-109"><a name="dataset"></a>набор Hello NYC такси приема-передачи данных</span><span class="sxs-lookup"><span data-stu-id="48a86-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="48a86-110">Hello NYC такси обработки данных состоит из примерно 20 ГБ сжатые файлы CSV (~ 48 ГБ несжатого), запись более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута.</span><span class="sxs-lookup"><span data-stu-id="48a86-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="48a86-111">Каждая запись маршрута включает hello раскладки и истощение расположений и времени, анонимен hack номер лицензии (драйвер) и hello номер medallion (уникальный идентификатор элемента такси).</span><span class="sxs-lookup"><span data-stu-id="48a86-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="48a86-112">данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:</span><span class="sxs-lookup"><span data-stu-id="48a86-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="48a86-113">Hello **trip_data.csv** файл содержит сведения о обработки, например количество пассажиров, отправки и dropoff точек, длительность обработки и длина маршрута.</span><span class="sxs-lookup"><span data-stu-id="48a86-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="48a86-114">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="48a86-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="48a86-115">Hello **trip_fare.csv** файл содержит подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты.</span><span class="sxs-lookup"><span data-stu-id="48a86-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="48a86-116">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="48a86-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="48a86-117">Hello **уникальный ключ** используется toojoin trip\_данных и обработки\_тариф авиакомпании состоит из следующих трех полей hello:</span><span class="sxs-lookup"><span data-stu-id="48a86-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="48a86-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="48a86-118">medallion,</span></span>
* <span data-ttu-id="48a86-119">hack\_license и</span><span class="sxs-lookup"><span data-stu-id="48a86-119">hack\_license and</span></span>
* <span data-ttu-id="48a86-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="48a86-120">pickup\_datetime.</span></span>

## <span data-ttu-id="48a86-121"><a name="mltasks"></a>Определение трех типов задач прогнозирования</span><span class="sxs-lookup"><span data-stu-id="48a86-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="48a86-122">Мы сформулировать три прогноза проблемы с учетом hello *совет\_сумма* задачи моделирования tooillustrate трех типов:</span><span class="sxs-lookup"><span data-stu-id="48a86-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="48a86-123">**Двоичной классификации**: toopredict ли совет уплаченной поездки, т. е. *совет\_сумма* , которое больше, чем $0 — положительные пример, тогда как *совет\_сумма* $ 0 представляет собой отрицательное пример.</span><span class="sxs-lookup"><span data-stu-id="48a86-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="48a86-124">**Мультиклассовая классификация**: диапазон hello toopredict подсказки оплаты hello trip.</span><span class="sxs-lookup"><span data-stu-id="48a86-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="48a86-125">Разделен hello *совет\_сумма* в пять ячеек или классы:</span><span class="sxs-lookup"><span data-stu-id="48a86-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="48a86-126">**Задача регрессии**: оплачена сумма hello toopredict подсказки для маршрута.</span><span class="sxs-lookup"><span data-stu-id="48a86-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="48a86-127"><a name="setup"></a>Настройка среды обработки и анализа данных Azure hello для расширенной аналитики</span><span class="sxs-lookup"><span data-stu-id="48a86-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="48a86-128">tooset настройку среды обработки и анализа данных Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="48a86-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="48a86-129">**Создайте собственную учетную запись хранилища BLOB-объектов Azure**</span><span class="sxs-lookup"><span data-stu-id="48a86-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="48a86-130">При подготовке хранилища BLOB-объектов Azure, выберите географическое расположение для хранилища BLOB-объектов Azure в или как можно ближе слишком**центральных штатах юга США**, который здесь хранятся hello такси NYC данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="48a86-131">с помощью AzCopy из контейнера tooa контейнер хранилища BLOB-объект открытого hello в учетной записи будут копироваться данные Hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="48a86-132">Hello ближе к хранилищу больших двоичных объектов tooSouth центральной части США, hello быстрее этой задачи (шаг 4) будет завершено.</span><span class="sxs-lookup"><span data-stu-id="48a86-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="48a86-133">toocreate собственные учетной записи хранилища Azure, hello выполните шаги, описанные в [учетных записей хранилища Azure о](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="48a86-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="48a86-134">Быть убедиться, что примечания toomake hello значения для следующих учетных данных учетной записи хранилища, как они потребуется позже в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="48a86-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="48a86-135">**Имя учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="48a86-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="48a86-136">**Ключ учетной записи хранения**</span><span class="sxs-lookup"><span data-stu-id="48a86-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="48a86-137">**Имя контейнера** (который вы хотите toobe hello данные, хранящиеся в hello хранилище больших двоичных объектов)</span><span class="sxs-lookup"><span data-stu-id="48a86-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="48a86-138">**Подготовьте экземпляр хранилища данных SQL Azure.**</span><span class="sxs-lookup"><span data-stu-id="48a86-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="48a86-139">Выполните hello документации на [создать хранилище данных SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision экземпляр хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="48a86-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="48a86-140">Убедитесь, что вносимые нотации на hello следующие учетные данные хранилища данных SQL, которые будут использоваться на последующих этапах.</span><span class="sxs-lookup"><span data-stu-id="48a86-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="48a86-141">**Имя сервера**: <server Name>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="48a86-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="48a86-142">**имя (базы данных) хранилища данных SQL;**</span><span class="sxs-lookup"><span data-stu-id="48a86-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="48a86-143">**Имя пользователя**</span><span class="sxs-lookup"><span data-stu-id="48a86-143">**Username**</span></span>
* <span data-ttu-id="48a86-144">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="48a86-144">**Password**</span></span>

<span data-ttu-id="48a86-145">**Установите Visual Studio и SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="48a86-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="48a86-146">Инструкции можно найти в статье [Установка Visual Studio 2015 и SSDT для хранилища данных SQL](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="48a86-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="48a86-147">**Подключение tooyour хранилища данных SQL Azure с помощью Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="48a86-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="48a86-148">Инструкции см. шаги 1 и 2 в [подключения tooAzure хранилище данных SQL с помощью Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48a86-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="48a86-149">Выполнения hello следующий запрос SQL в базе данных hello, созданных в хранилище данных SQL (вместо hello запрос, приведенный в шаге 3 hello подключиться разделе) слишком**создайте главный ключ**.</span><span class="sxs-lookup"><span data-stu-id="48a86-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="48a86-150">**Создайте рабочую область Машинного обучения Azure, используя подписку Azure.**</span><span class="sxs-lookup"><span data-stu-id="48a86-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="48a86-151">Инструкции можно найти в статье [Создание рабочей области машинного обучения Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="48a86-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="48a86-152"><a name="getdata"></a>Hello данные загружаются в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="48a86-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="48a86-153">Откройте командную консоль Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48a86-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="48a86-154">Hello следующей команды PowerShell toodownload hello примере файлы скрипта SQL, мы поделиться с вами в локальный каталог tooa GitHub, который указывается с помощью параметра hello *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="48a86-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="48a86-155">Можно изменить значение параметра hello *- DestDir* tooany локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="48a86-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="48a86-156">Если *- DestDir* не существует, он будет создан hello сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48a86-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="48a86-157">Может потребоваться слишком**Запуск от имени администратора** при выполнении следующего сценария PowerShell if Здравствуй вашей *DestDir* каталог должен tooit toocreate или toowrite прав администратора.</span><span class="sxs-lookup"><span data-stu-id="48a86-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="48a86-158">После успешного выполнения изменяет текущий рабочий каталог слишком*- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="48a86-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="48a86-159">Можно toosee экран, подобный ниже:</span><span class="sxs-lookup"><span data-stu-id="48a86-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="48a86-160">В вашей *- DestDir*, выполните следующий сценарий PowerShell с правами администратора hello:</span><span class="sxs-lookup"><span data-stu-id="48a86-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="48a86-161">Hello сценария PowerShell для hello первый раз, запускаемый запрашивается tooinput hello сведения из вашего хранилища данных SQL Azure и вашей учетной записи хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="48a86-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="48a86-162">По завершении этого скрипта PowerShell под управлением для hello впервые, учетные данные hello входных данных можно будет были записаны файл конфигурации tooa SQLDW.conf в hello имеется рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="48a86-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="48a86-163">Hello будущих выполнения этот файл сценария PowerShell имеет параметр tooread hello всех необходимых параметров из файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="48a86-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="48a86-164">Если вам требуется toochange некоторые параметры, вы можете tooinput hello параметров на экране приветствия после строки, удаление этого файла конфигурации и ввод значений параметров hello в ответ на приглашение или значений параметров hello toochange путем редактирования файла SQLDW.conf hello в вашей *- DestDir* каталога.</span><span class="sxs-lookup"><span data-stu-id="48a86-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="48a86-165">В порядке tooavoid схемы имя конфликтует с уже существующих в вашей хранилища данных SQL Azure при чтении параметров непосредственно из файла SQLDW.conf hello случайное число из 3 цифр добавляется имя схемы toohello из файла SQLDW.conf hello как имя схемы по умолчанию hello для Каждое выполнение.</span><span class="sxs-lookup"><span data-stu-id="48a86-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="48a86-166">Hello сценарий PowerShell может запросить имя схемы: hello имя может быть указан по своему усмотрению пользователя.</span><span class="sxs-lookup"><span data-stu-id="48a86-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="48a86-167">Это **сценарий PowerShell** файл завершения hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="48a86-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="48a86-168">**Скачивание и установка AzCopy**, если она еще не установлена.</span><span class="sxs-lookup"><span data-stu-id="48a86-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
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
* <span data-ttu-id="48a86-169">**Копирование учетной записи хранилища данных tooyour закрытый большой двоичный объект** из hello общедоступный BLOB-объект с помощью AzCopy</span><span class="sxs-lookup"><span data-stu-id="48a86-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="48a86-170">**Загружает данные с помощью Polybase (путем выполнения LoadDataToSQLDW.sql) tooyour хранилища данных SQL Azure** из вашей учетной записи хранилища закрытый большой двоичный объект с hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="48a86-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="48a86-171">Создание схемы</span><span class="sxs-lookup"><span data-stu-id="48a86-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="48a86-172">Создание учетных данных для определенной базы данных</span><span class="sxs-lookup"><span data-stu-id="48a86-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="48a86-173">Создание внешнего источника данных для BLOB-объекта хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="48a86-173">Create an external data source for an Azure storage blob</span></span>
    
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
  * <span data-ttu-id="48a86-174">Создание формата внешнего файла для CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="48a86-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="48a86-175">Без сжатия данных и поля разделены символом вертикальной черты hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
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
  * <span data-ttu-id="48a86-176">Создание внешних таблиц (trip и fare) для хранения набора данных такси Нью-Йорка в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="48a86-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
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

    - <span data-ttu-id="48a86-177">Загрузка данных из внешних таблиц в хранилище BLOB-объектов Azure tooSQL хранилища данных</span><span class="sxs-lookup"><span data-stu-id="48a86-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

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

    - <span data-ttu-id="48a86-178">Создать образец таблицы данных (NYCTaxi_Sample) и вставки данных tooit от выбора SQL-запросы таблиц маршрута и тариф авиакомпании hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="48a86-179">(Некоторые шаги в этом пошаговом руководстве должен toouse этот образец таблицы.)</span><span class="sxs-lookup"><span data-stu-id="48a86-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

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

<span data-ttu-id="48a86-180">географическое расположение Hello учетные записи хранения влияет на время загрузки.</span><span class="sxs-lookup"><span data-stu-id="48a86-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="48a86-181">В зависимости от географического расположения hello вашей учетной записи хранилища закрытый большой двоичный объект, hello процесс копирования данных из большой двоичный объект открытого tooyour личной учетной записи хранения может занять около 15 минут или даже больше и hello обработать загрузки данных из вашей учетной записи хранения tooyour хранилища данных SQL Azure может занять до 20 минут или больше.</span><span class="sxs-lookup"><span data-stu-id="48a86-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="48a86-182">Что делать, если у вас есть дублирования источника и назначения файлов будет иметь toodecide.</span><span class="sxs-lookup"><span data-stu-id="48a86-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="48a86-183">Если toobe файлы CSV-файл hello, скопированные из учетной записи хранилища закрытый большой двоичный объект tooyour в хранилище BLOB-объект открытого hello уже существуют в вашей учетной записи хранилища закрытый большой двоичный объект, AzCopy запрашивает, следует ли вы toooverwrite их.</span><span class="sxs-lookup"><span data-stu-id="48a86-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="48a86-184">Если вы не хотите toooverwrite их, входные  **n**  при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="48a86-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="48a86-185">Если требуется, чтобы toooverwrite **все** из них, ввода **** при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="48a86-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="48a86-186">Также можно ввести **y** toooverwrite .csv файлы по отдельности.</span><span class="sxs-lookup"><span data-stu-id="48a86-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![График № 21][21]

<span data-ttu-id="48a86-188">Можно использовать собственные данные.</span><span class="sxs-lookup"><span data-stu-id="48a86-188">You can use your own data.</span></span> <span data-ttu-id="48a86-189">Если данные хранятся в локальном компьютере, в реальной жизни приложения, по-прежнему можно использовать закрытый большой двоичный объект Azure AzCopy tooupload локальных данных tooyour хранилища.</span><span class="sxs-lookup"><span data-stu-id="48a86-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="48a86-190">Требуется только toochange hello **источника** расположение, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, в hello команды AzCopy hello PowerShell скрипт файл toohello локальный каталог, содержащий данные.</span><span class="sxs-lookup"><span data-stu-id="48a86-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="48a86-191">Если данные уже находится в хранилище BLOB-объектов Azure закрытый в реальной жизни приложения, можно пропустить hello AzCopy hello сценарий PowerShell и тем самым непосредственно передать tooAzure hello данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="48a86-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="48a86-192">Потребуются дополнительные редактирует из сценария tootailor hello его toohello формат данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="48a86-193">Этот сценарий Powershell также подключает hello сведения хранилища данных SQL Azure в hello исследования примере файлы данных SQLDW_Explorations.sql, SQLDW_Explorations.ipynb и SQLDW_Explorations_Scripts.py, чтобы эти три файла будут готовы toobe испытан мгновенно После завершения hello сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48a86-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="48a86-194">После успешного выполнения вы увидите экран, аналогичный этому:</span><span class="sxs-lookup"><span data-stu-id="48a86-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="48a86-195"><a name="dbexplore"></a>Изучение данных и проектирование признаков в хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="48a86-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="48a86-196">В этом разделе мы исследуем данные и создадим признаки, используя SQL-запросы для хранилища данных SQL Azure с помощью **средств работы с данными Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="48a86-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="48a86-197">Все запросы SQL, используемые в этом разделе можно найти в hello пример сценария с именем *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="48a86-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="48a86-198">Этот файл уже загруженные tooyour локальный каталог для скрипта PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="48a86-199">Кроме того, его также можно получить на сайте [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="48a86-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="48a86-200">Но в GitHub в файл hello отсутствуют сведения hello хранилища данных SQL Azure, попадет в систему.</span><span class="sxs-lookup"><span data-stu-id="48a86-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="48a86-201">Подключение tooyour хранилища данных SQL Azure с помощью Visual Studio с именем входа hello хранилища данных SQL и пароля и откройте hello **обозреватель объектов SQL** базу данных tooconfirm hello и таблицы были импортированы.</span><span class="sxs-lookup"><span data-stu-id="48a86-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="48a86-202">Получить hello *SQLDW_Explorations.sql* файла.</span><span class="sxs-lookup"><span data-stu-id="48a86-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="48a86-203">tooopen редактор запросов хранилища параллельных данных (PDW), использовать hello **новый запрос** команду в это время ваш PDW выбран hello **обозреватель объектов SQL**.</span><span class="sxs-lookup"><span data-stu-id="48a86-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="48a86-204">PDW Hello стандартный редактор SQL-запросов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="48a86-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="48a86-205">Ниже приведены hello тип данных, возможности просмотра и создания задачи, выполняемые в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="48a86-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="48a86-206">Просмотрим распределение данных по нескольким полям в различных временных окнах.</span><span class="sxs-lookup"><span data-stu-id="48a86-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="48a86-207">Проверка качества данных полей hello широты и долготы.</span><span class="sxs-lookup"><span data-stu-id="48a86-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="48a86-208">Создание двоичного и мультиклассовой классификации меток, основываясь на hello **совет\_сумма**.</span><span class="sxs-lookup"><span data-stu-id="48a86-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="48a86-209">Создадим характеристики и вычислим/сравним расстояния поездок.</span><span class="sxs-lookup"><span data-stu-id="48a86-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="48a86-210">Объединение hello двух таблиц и извлеките случайную выборку, который будет использоваться toobuild моделей.</span><span class="sxs-lookup"><span data-stu-id="48a86-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="48a86-211">Проверка импорта данных</span><span class="sxs-lookup"><span data-stu-id="48a86-211">Data import verification</span></span>
<span data-ttu-id="48a86-212">Эти запросы обеспечивают быстрой проверки количества строк и столбцов в таблицах, заполнять ранее с помощью Polybase параллельный массовый импорт, приветствия hello</span><span class="sxs-lookup"><span data-stu-id="48a86-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="48a86-213">**Выходные данные.** Вы должны получить 173 179 759 строк и 14 столбцов.</span><span class="sxs-lookup"><span data-stu-id="48a86-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="48a86-214">Просмотр: Распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="48a86-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="48a86-215">Следующий пример запроса определяет medallions hello (номера такси) завершенных более 100 приема-передачи данных в течение указанного периода времени.</span><span class="sxs-lookup"><span data-stu-id="48a86-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="48a86-216">запрос Hello получают преимущества от доступа hello секционированные таблицы с момента обусловлено схему секционирования hello **раскладки\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="48a86-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="48a86-217">Запрос hello полного набора данных следует использовать hello секционированные таблицы и/или сканирование индекса.</span><span class="sxs-lookup"><span data-stu-id="48a86-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="48a86-218">**Вывод:** hello запросов должны возвращать таблицу со строками, указав hello 13,369 medallions (такси) и hello количество выполненных их в 2013 trip.</span><span class="sxs-lookup"><span data-stu-id="48a86-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="48a86-219">последний столбец Hello содержит hello число hello приема-передачи завершена.</span><span class="sxs-lookup"><span data-stu-id="48a86-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="48a86-220">Просмотр: распределение поездок по параметрам medallion и hack_license</span><span class="sxs-lookup"><span data-stu-id="48a86-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="48a86-221">Этот пример определяет medallions hello (номера такси) и hack_license цифры (драйверы) выполнения больше, чем 100 приема-передачи данных в течение указанного периода времени.</span><span class="sxs-lookup"><span data-stu-id="48a86-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="48a86-222">**Вывод:** hello запрос должен возвращать таблицу со строками 13,369, указав идентификаторы выполненными более, 100 приема-передачи в 2013 драйвер или автомобиль hello 13,369.</span><span class="sxs-lookup"><span data-stu-id="48a86-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="48a86-223">последний столбец Hello содержит hello число hello приема-передачи завершена.</span><span class="sxs-lookup"><span data-stu-id="48a86-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="48a86-224">Оценка качества данных: проверка записей с неправильными значениями долготы и/или широты</span><span class="sxs-lookup"><span data-stu-id="48a86-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="48a86-225">В этом примере анализируется, если любая из поля долготы и широты hello либо содержит недопустимое значение (градусов в радианах должно быть от -90 до 90), или иметь (0, 0) координаты.</span><span class="sxs-lookup"><span data-stu-id="48a86-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="48a86-226">**Вывод:** hello запрос возвращает 837,467 приема-передачи, которые имеют недопустимые поля долготы и широты.</span><span class="sxs-lookup"><span data-stu-id="48a86-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="48a86-227">Изучение: распределение поездок с чаевыми и без чаевых</span><span class="sxs-lookup"><span data-stu-id="48a86-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="48a86-228">Этот пример возвращает числовой hello приема-передачи, были чаевых оставил зависимости и номер hello, не были Подрезанный за указанный период времени (или hello полного набора данных Если охватывающие hello полный год, которая будет настроена здесь).</span><span class="sxs-lookup"><span data-stu-id="48a86-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="48a86-229">Это распределение отражает hello двоичных метки распространения toobe впоследствии использовать для моделирования двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="48a86-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="48a86-230">**Вывод:** hello запроса следует следующие возвращаемого hello совет частот hello годом 2013: 90,447,622 чаевых оставил зависимости и 82,264,709 чаевых оставил зависимости не.</span><span class="sxs-lookup"><span data-stu-id="48a86-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="48a86-231">Изучение: распределение классов и диапазонов чаевых</span><span class="sxs-lookup"><span data-stu-id="48a86-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="48a86-232">Этот пример вычисляет распределение hello диапазоны подсказки в определенный момент времени периода (или hello полного набора данных Если охватывающие hello полный год).</span><span class="sxs-lookup"><span data-stu-id="48a86-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="48a86-233">Это распределение hello hello метки классы, которые будут использоваться позже для моделирования мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="48a86-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

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

<span data-ttu-id="48a86-234">**Выходные данные:**</span><span class="sxs-lookup"><span data-stu-id="48a86-234">**Output:**</span></span>

| <span data-ttu-id="48a86-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="48a86-235">tip_class</span></span> | <span data-ttu-id="48a86-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="48a86-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="48a86-237">1</span><span class="sxs-lookup"><span data-stu-id="48a86-237">1</span></span> |<span data-ttu-id="48a86-238">82230915</span><span class="sxs-lookup"><span data-stu-id="48a86-238">82230915</span></span> |
| <span data-ttu-id="48a86-239">2</span><span class="sxs-lookup"><span data-stu-id="48a86-239">2</span></span> |<span data-ttu-id="48a86-240">6198803</span><span class="sxs-lookup"><span data-stu-id="48a86-240">6198803</span></span> |
| <span data-ttu-id="48a86-241">3</span><span class="sxs-lookup"><span data-stu-id="48a86-241">3</span></span> |<span data-ttu-id="48a86-242">1932223</span><span class="sxs-lookup"><span data-stu-id="48a86-242">1932223</span></span> |
| <span data-ttu-id="48a86-243">0</span><span class="sxs-lookup"><span data-stu-id="48a86-243">0</span></span> |<span data-ttu-id="48a86-244">82264625</span><span class="sxs-lookup"><span data-stu-id="48a86-244">82264625</span></span> |
| <span data-ttu-id="48a86-245">4</span><span class="sxs-lookup"><span data-stu-id="48a86-245">4</span></span> |<span data-ttu-id="48a86-246">85765</span><span class="sxs-lookup"><span data-stu-id="48a86-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="48a86-247">Изучение: вычисление и сравнение расстояния поездок</span><span class="sxs-lookup"><span data-stu-id="48a86-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="48a86-248">Этот пример преобразует hello раскладки и истощение долготы и широты tooSQL geography указывает, вычисляет расстояние trip hello, с помощью точек различие SQL geography и возвращает случайную выборку hello результатов для сравнения.</span><span class="sxs-lookup"><span data-stu-id="48a86-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="48a86-249">пример Hello ограничивает результаты hello, координирует toovalid только с помощью hello качества данных оценки запроса, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="48a86-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
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

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="48a86-250">Проектирование признаков с помощью функций SQL</span><span class="sxs-lookup"><span data-stu-id="48a86-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="48a86-251">Иногда функции SQL могут быть полезны при проектировании признаков.</span><span class="sxs-lookup"><span data-stu-id="48a86-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="48a86-252">В этом пошаговом руководстве мы определили SQL функция toocalculate hello прямой расстояние между расположениями отправки и dropoff hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="48a86-253">Можно выполнить следующие сценарии SQL в hello **данных средств Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="48a86-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="48a86-254">Вот hello скрипт SQL, который определяет функции hello расстояние.</span><span class="sxs-lookup"><span data-stu-id="48a86-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="48a86-255">Ниже приведен пример toocall функции toogenerate этой функции в SQL-запросе:</span><span class="sxs-lookup"><span data-stu-id="48a86-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="48a86-256">**Вывод:** этот запрос создает таблицу (с 2,803,538 строк) с раскладки и dropoff latitudes и долгот и соответствующий hello направлять расстояние в милях.</span><span class="sxs-lookup"><span data-stu-id="48a86-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="48a86-257">Ниже приведены результаты hello первыми тремя строками.</span><span class="sxs-lookup"><span data-stu-id="48a86-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="48a86-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="48a86-258">pickup_latitude</span></span> | <span data-ttu-id="48a86-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="48a86-259">pickup_longitude</span></span> | <span data-ttu-id="48a86-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="48a86-260">dropoff_latitude</span></span> | <span data-ttu-id="48a86-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="48a86-261">dropoff_longitude</span></span> | <span data-ttu-id="48a86-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="48a86-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="48a86-263">1</span><span class="sxs-lookup"><span data-stu-id="48a86-263">1</span></span> |<span data-ttu-id="48a86-264">40,731804</span><span class="sxs-lookup"><span data-stu-id="48a86-264">40.731804</span></span> |<span data-ttu-id="48a86-265">–74,001083</span><span class="sxs-lookup"><span data-stu-id="48a86-265">-74.001083</span></span> |<span data-ttu-id="48a86-266">40,736622</span><span class="sxs-lookup"><span data-stu-id="48a86-266">40.736622</span></span> |<span data-ttu-id="48a86-267">–73,988953</span><span class="sxs-lookup"><span data-stu-id="48a86-267">-73.988953</span></span> |<span data-ttu-id="48a86-268">0,7169601222</span><span class="sxs-lookup"><span data-stu-id="48a86-268">.7169601222</span></span> |
| <span data-ttu-id="48a86-269">2</span><span class="sxs-lookup"><span data-stu-id="48a86-269">2</span></span> |<span data-ttu-id="48a86-270">40,715794</span><span class="sxs-lookup"><span data-stu-id="48a86-270">40.715794</span></span> |<span data-ttu-id="48a86-271">–74,010635</span><span class="sxs-lookup"><span data-stu-id="48a86-271">-74,010635</span></span> |<span data-ttu-id="48a86-272">40,725338</span><span class="sxs-lookup"><span data-stu-id="48a86-272">40.725338</span></span> |<span data-ttu-id="48a86-273">–74,00399</span><span class="sxs-lookup"><span data-stu-id="48a86-273">-74.00399</span></span> |<span data-ttu-id="48a86-274">0,7448343721</span><span class="sxs-lookup"><span data-stu-id="48a86-274">.7448343721</span></span> |
| <span data-ttu-id="48a86-275">3</span><span class="sxs-lookup"><span data-stu-id="48a86-275">3</span></span> |<span data-ttu-id="48a86-276">40,761456</span><span class="sxs-lookup"><span data-stu-id="48a86-276">40.761456</span></span> |<span data-ttu-id="48a86-277">–73,999886</span><span class="sxs-lookup"><span data-stu-id="48a86-277">-73.999886</span></span> |<span data-ttu-id="48a86-278">40,766544</span><span class="sxs-lookup"><span data-stu-id="48a86-278">40.766544</span></span> |<span data-ttu-id="48a86-279">–73,988228</span><span class="sxs-lookup"><span data-stu-id="48a86-279">-73.988228</span></span> |<span data-ttu-id="48a86-280">0,7037227967</span><span class="sxs-lookup"><span data-stu-id="48a86-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="48a86-281">Подготовка данных для построения модели</span><span class="sxs-lookup"><span data-stu-id="48a86-281">Prepare data for model building</span></span>
<span data-ttu-id="48a86-282">Hello следующий запрос соединения hello **nyctaxi\_trip** и **nyctaxi\_тариф авиакомпании** таблицы, приводит к возникновению ошибки двоичной классификации метки **чаевых оставил зависимости**, Метка многоклассовый классификатор **совет\_класса**и извлекает образец из hello полный объединенном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="48a86-283">Hello выборка выполняется путем извлечения подмножества hello приема-передачи данных на основе времени раскладки.</span><span class="sxs-lookup"><span data-stu-id="48a86-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="48a86-284">Этот запрос можно скопировать, затем вставить непосредственно в hello [студии машинного обучения Azure](https://studio.azureml.net) [импорта данных] [ import-data] модуль для приема прямой данных из экземпляра базы данных SQL hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="48a86-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="48a86-285">запрос Hello исключает записи с неверным (0, 0) координаты.</span><span class="sxs-lookup"><span data-stu-id="48a86-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

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

<span data-ttu-id="48a86-286">Когда вы будете готовы tooproceed tooAzure машинного обучения, можно либо:</span><span class="sxs-lookup"><span data-stu-id="48a86-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="48a86-287">Сохранить hello окончательного SQL запроса tooextract и образец hello данных и копирования и вставки hello запрос непосредственно в [импорта данных] [ import-data] в машинном обучении Azure, или</span><span class="sxs-lookup"><span data-stu-id="48a86-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="48a86-288">Сохранять hello выборки и социотехники данных планируется toouse для построения в новые хранилища данных SQL модели и использовать новую таблицу hello в hello [импорта данных] [ import-data] модуль в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="48a86-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="48a86-289">Hello сценария PowerShell в предыдущем шаге это сделано автоматически.</span><span class="sxs-lookup"><span data-stu-id="48a86-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="48a86-290">Можно считывать данные непосредственно из этой таблицы в модуле hello импорта данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="48a86-291"><a name="ipnb"></a>Просмотр данных и проектирование характеристик в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="48a86-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="48a86-292">В этом разделе мы выполним создание функции, с помощью обоих Python и просмотра данных и запросов SQL к hello хранилища данных SQL создана ранее.</span><span class="sxs-lookup"><span data-stu-id="48a86-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="48a86-293">Образец ноутбук IPython с именем **SQLDW_Explorations.ipynb** и файл сценария Python **SQLDW_Explorations_Scripts.py** были загруженный tooyour локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="48a86-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="48a86-294">Они также доступны на веб-сайте [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="48a86-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="48a86-295">В сценариях Python эти два файла идентичны.</span><span class="sxs-lookup"><span data-stu-id="48a86-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="48a86-296">файл сценария Python Hello предоставляется tooyou, если у вас на сервер ноутбук IPython.</span><span class="sxs-lookup"><span data-stu-id="48a86-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="48a86-297">Эти два примера файлов Python предназначены для использования с **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="48a86-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="48a86-298">Здравствуйте, необходимой информации хранилища данных SQL Azure в образце hello ноутбук IPython и hello сценария файл загруженный tooyour локального компьютера было подключено сценарием PowerShell hello ранее Python.</span><span class="sxs-lookup"><span data-stu-id="48a86-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="48a86-299">Они выполняются без изменений.</span><span class="sxs-lookup"><span data-stu-id="48a86-299">They are executable without any modification.</span></span>

<span data-ttu-id="48a86-300">Если заранее настроенных рабочую область машинного обучения Azure, можно непосредственно загрузить пример hello ноутбук IPython toohello ноутбук IPython AzureML службы и начать его выполнение.</span><span class="sxs-lookup"><span data-stu-id="48a86-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="48a86-301">Ниже приведены hello действия tooupload tooAzureML ноутбук IPython службы.</span><span class="sxs-lookup"><span data-stu-id="48a86-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="48a86-302">Войдите в рабочей области машинного обучения Azure tooyour, нажмите кнопку «Studio» в верхнем hello и нажмите кнопку «НОУТБУКИ» hello левой части веб-страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="48a86-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![График № 22][22]
2. <span data-ttu-id="48a86-304">Щелкните «Создать» hello левый нижний угол hello веб-страницы и выберите пункт «Python 2».</span><span class="sxs-lookup"><span data-stu-id="48a86-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="48a86-305">Затем предоставьте записной книжке toohello имя и щелкните hello флажок toocreate hello нового пустым ноутбук IPython.</span><span class="sxs-lookup"><span data-stu-id="48a86-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![График № 23][23]
3. <span data-ttu-id="48a86-307">Щелкните символ «Jupyter» hello в левом верхнем углу hello hello новый ноутбук IPython.</span><span class="sxs-lookup"><span data-stu-id="48a86-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![График № 24][24]
4. <span data-ttu-id="48a86-309">Перетаскивание toohello ноутбук IPython образец hello **дерева** ноутбук IPython AzureML службы и нажмите кнопку **отправить**.</span><span class="sxs-lookup"><span data-stu-id="48a86-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="48a86-310">Затем образец hello ноутбук IPython будет отправленного toohello ноутбук IPython AzureML службы.</span><span class="sxs-lookup"><span data-stu-id="48a86-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![График № 25][25]

<span data-ttu-id="48a86-312">В порядке toorun hello образец ноутбук IPython или Здравствуйте файл сценария Python, hello Python требуются следующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="48a86-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="48a86-313">При использовании службы AzureML ноутбук IPython hello эти пакеты были предварительно установлены.</span><span class="sxs-lookup"><span data-stu-id="48a86-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="48a86-314">pandas</span><span class="sxs-lookup"><span data-stu-id="48a86-314">pandas</span></span>
    - <span data-ttu-id="48a86-315">numpy</span><span class="sxs-lookup"><span data-stu-id="48a86-315">numpy</span></span>
    - <span data-ttu-id="48a86-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="48a86-316">matplotlib</span></span>
    - <span data-ttu-id="48a86-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="48a86-317">pyodbc</span></span>
    - <span data-ttu-id="48a86-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="48a86-318">PyTables</span></span>

<span data-ttu-id="48a86-319">При создании дополнительных аналитических решений на AzureML с большим объемом данных, рекомендуется использовать последовательность Hello необходимо hello в следующем:</span><span class="sxs-lookup"><span data-stu-id="48a86-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="48a86-320">Чтение в небольшую выборку данных hello в кадр данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="48a86-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="48a86-321">Выполните некоторые визуализации и исследования с помощью hello выборки данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="48a86-322">Поэкспериментируйте с помощью hello конструируются выборке данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="48a86-323">Для просмотра большего размера данных, обработки данных и конструируются используйте Python tooissue SQL-запросы непосредственно к hello хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="48a86-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="48a86-324">Определите, подходит для построения модели машинного обучения Azure toobe размер образца hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="48a86-325">Hello Далее приведены несколько исследования данных, визуализация данных и примеры технических возможностей.</span><span class="sxs-lookup"><span data-stu-id="48a86-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="48a86-326">Дополнительные исследования данных можно найти в образце hello ноутбук IPython и файл сценария Python образец hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="48a86-327">Инициализация учетных данных базы данных</span><span class="sxs-lookup"><span data-stu-id="48a86-327">Initialize database credentials</span></span>
<span data-ttu-id="48a86-328">Инициализируйте параметры подключения к базе данных в hello следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="48a86-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="48a86-329">Создание подключения к базе данных</span><span class="sxs-lookup"><span data-stu-id="48a86-329">Create database connection</span></span>
<span data-ttu-id="48a86-330">Вот hello строку подключения, которая создает базу данных toohello подключения hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="48a86-331">Сообщение числа строк и столбцов в таблице <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="48a86-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
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

* <span data-ttu-id="48a86-332">Общее число строк = 173179759</span><span class="sxs-lookup"><span data-stu-id="48a86-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="48a86-333">Общее число столбцов = 14</span><span class="sxs-lookup"><span data-stu-id="48a86-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="48a86-334">Сообщение числа строк и столбцов в таблице <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="48a86-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
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

* <span data-ttu-id="48a86-335">Общее число строк = 173179759</span><span class="sxs-lookup"><span data-stu-id="48a86-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="48a86-336">Общее количество столбцов — 11.</span><span class="sxs-lookup"><span data-stu-id="48a86-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="48a86-337">Чтение в образец небольшой данных из базы данных хранилища данных SQL hello</span><span class="sxs-lookup"><span data-stu-id="48a86-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
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
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="48a86-338">Время tooread hello образец таблицы — 14.096495 секунд.</span><span class="sxs-lookup"><span data-stu-id="48a86-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="48a86-339">Количество полученных строк и столбцов — 1000 и 21.</span><span class="sxs-lookup"><span data-stu-id="48a86-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="48a86-340">Описательная статистика</span><span class="sxs-lookup"><span data-stu-id="48a86-340">Descriptive statistics</span></span>
<span data-ttu-id="48a86-341">Теперь все готово tooexplore hello выборки данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="48a86-342">Мы начнем с рассмотрения некоторых описательных статистических показателей для hello **trip\_расстояние** (или другие поля нажмите toospecify).</span><span class="sxs-lookup"><span data-stu-id="48a86-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="48a86-343">Визуализация: пример блочной диаграммы</span><span class="sxs-lookup"><span data-stu-id="48a86-343">Visualization: Box plot example</span></span>
<span data-ttu-id="48a86-344">Теперь рассмотрим hello Блочная для hello trip расстояние toovisualize hello квантилей.</span><span class="sxs-lookup"><span data-stu-id="48a86-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![График #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="48a86-346">Визуализация: пример графика распределения</span><span class="sxs-lookup"><span data-stu-id="48a86-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="48a86-347">Графики, отображающие распределение hello и гистограммы для hello выборки trip расстояния.</span><span class="sxs-lookup"><span data-stu-id="48a86-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![График #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="48a86-349">Визуализация: гистограммы и линейные графики</span><span class="sxs-lookup"><span data-stu-id="48a86-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="48a86-350">В этом примере мы bin расстояние trip hello в пять ячеек и визуализировать hello группирование результатов.</span><span class="sxs-lookup"><span data-stu-id="48a86-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="48a86-351">Можно построить hello выше распространения ячейки в строке или строки построения с:</span><span class="sxs-lookup"><span data-stu-id="48a86-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![График #3][3]

<span data-ttu-id="48a86-353">и</span><span class="sxs-lookup"><span data-stu-id="48a86-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![График #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="48a86-355">Визуализация: примеры точечных диаграмм</span><span class="sxs-lookup"><span data-stu-id="48a86-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="48a86-356">Мы покажем точечной диаграммы между **trip\_время\_в\_сек** и **trip\_расстояние** toosee при наличии корреляции</span><span class="sxs-lookup"><span data-stu-id="48a86-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![График #6][6]

<span data-ttu-id="48a86-358">Аналогичным образом можно проверить hello связь между **скорость\_кода** и **trip\_расстояние**.</span><span class="sxs-lookup"><span data-stu-id="48a86-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![График #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="48a86-360">Изучение выборки данных с помощью SQL-запросов в IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="48a86-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="48a86-361">В этом разделе мы исследуем распределения данных с помощью hello выборки данных, который сохраняется в новой таблице hello, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="48a86-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="48a86-362">Обратите внимание, что аналогичные просмотров может осуществляться с помощью hello исходных таблиц.</span><span class="sxs-lookup"><span data-stu-id="48a86-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="48a86-363">Просмотр: Количество отчетов строк и столбцов в hello выбранных таблицы</span><span class="sxs-lookup"><span data-stu-id="48a86-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="48a86-364">Исследование: распределение поездок с чаевыми и без чаевых</span><span class="sxs-lookup"><span data-stu-id="48a86-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="48a86-365">Изучение: распределение классов чаевых</span><span class="sxs-lookup"><span data-stu-id="48a86-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="48a86-366">Просмотр: Построения распространения совет hello классом</span><span class="sxs-lookup"><span data-stu-id="48a86-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![График № 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="48a86-368">Исследование: ежедневное распределение поездок</span><span class="sxs-lookup"><span data-stu-id="48a86-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="48a86-369">Исследование: распределение поездок по параметру medallion</span><span class="sxs-lookup"><span data-stu-id="48a86-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="48a86-370">Изучение: распределение поездок по медальону и номеру лицензии водителя</span><span class="sxs-lookup"><span data-stu-id="48a86-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="48a86-371">Просмотр: распределение поездок по времени</span><span class="sxs-lookup"><span data-stu-id="48a86-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="48a86-372">Изучение: распределение поездок по расстоянию</span><span class="sxs-lookup"><span data-stu-id="48a86-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="48a86-373">Изучение: распределение поездок по типу оплаты</span><span class="sxs-lookup"><span data-stu-id="48a86-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="48a86-374">Проверьте hello конечная форма hello признак таблицы</span><span class="sxs-lookup"><span data-stu-id="48a86-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="48a86-375"><a name="mlmodel"></a>Построение моделей в компоненте машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="48a86-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="48a86-376">Мы стали готовы tooproceed toomodel построение и развертывание модели в [машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="48a86-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="48a86-377">Hello данных — Готово toobe используется ни в одном hello прогноза проблем, описанных выше, а именно:</span><span class="sxs-lookup"><span data-stu-id="48a86-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="48a86-378">**Двоичная классификация**: toopredict ли уплаченной Совет для маршрута.</span><span class="sxs-lookup"><span data-stu-id="48a86-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="48a86-379">**Мультиклассовая классификация**: диапазон hello toopredict совета оплачен, в соответствии с toohello ранее определенных классов.</span><span class="sxs-lookup"><span data-stu-id="48a86-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="48a86-380">**Задача регрессии**: оплачена сумма hello toopredict подсказки для маршрута.</span><span class="sxs-lookup"><span data-stu-id="48a86-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="48a86-381">toobegin hello моделированию, войдите в tooyour **машинного обучения Azure** рабочей области.</span><span class="sxs-lookup"><span data-stu-id="48a86-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="48a86-382">Если вы еще не создали рабочую область Машинного обучения, см. статью [Создание рабочей области Машинного обучения Azure и предоставление к ней общего доступа](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="48a86-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="48a86-383">tooget к выполнению машинного обучения Azure в разделе [возможности студии машинного обучения Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="48a86-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="48a86-384">Войдите в слишком[студии машинного обучения Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="48a86-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="48a86-385">Hello Studio домашней странице предоставляет широкий набор сведений, видео, учебники, ссылки toohello Справочник по модулям и другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="48a86-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="48a86-386">Дополнительные сведения о машинном обучении Azure можно найти hello [центр документации машинного обучения Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="48a86-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="48a86-387">Эксперимента обучения обычно состоит из hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="48a86-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="48a86-388">Создать **+НОВЫЙ** эксперимент.</span><span class="sxs-lookup"><span data-stu-id="48a86-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="48a86-389">Получите данные hello в Azure ML.</span><span class="sxs-lookup"><span data-stu-id="48a86-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="48a86-390">Предварительно обработать, преобразование данных и управления ими hello при необходимости.</span><span class="sxs-lookup"><span data-stu-id="48a86-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="48a86-391">Создать необходимые характеристики.</span><span class="sxs-lookup"><span data-stu-id="48a86-391">Generate features as needed.</span></span>
5. <span data-ttu-id="48a86-392">Разбиение данных hello в набор данных, обучения и проверки и тестирования (или иметь отдельный набор данных для каждого).</span><span class="sxs-lookup"><span data-stu-id="48a86-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="48a86-393">Выберите один или несколько алгоритмов машинного обучения в зависимости от hello обучения toosolve проблему.</span><span class="sxs-lookup"><span data-stu-id="48a86-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="48a86-394">Например, двоичная классификация, мультиклассовая классификация, регрессия.</span><span class="sxs-lookup"><span data-stu-id="48a86-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="48a86-395">Обучение одной или нескольких моделей с помощью hello обучающий набор данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="48a86-396">Оценка hello проверочного набора данных с помощью обученной модели hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="48a86-397">Оцените hello модели toocompute hello соответствующие метрики для изучения проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="48a86-398">Настройка модели hello и выберите hello наиболее toodeploy модели.</span><span class="sxs-lookup"><span data-stu-id="48a86-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="48a86-399">В этом упражнении мы уже изучена разработан hello данные в хранилище данных SQL и решили tooingest размер образца hello в Azure ML.</span><span class="sxs-lookup"><span data-stu-id="48a86-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="48a86-400">Вот toobuild процедуры hello один или несколько моделей прогнозирования hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="48a86-401">Получение данных hello в Azure ML с помощью hello [импорта данных] [ import-data] модуля, доступные в hello **ввод и вывод данных** раздела.</span><span class="sxs-lookup"><span data-stu-id="48a86-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="48a86-402">Дополнительные сведения см. в разделе hello [импорта данных] [ import-data] справочной странице модуля.</span><span class="sxs-lookup"><span data-stu-id="48a86-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Модуль "Импорт данных" в Машинном обучении Azure][17]
2. <span data-ttu-id="48a86-404">Выберите **базы данных SQL Azure** как hello **источника данных** в hello **свойства** панель.</span><span class="sxs-lookup"><span data-stu-id="48a86-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="48a86-405">Введите имя DNS hello базы данных в hello **имя сервера базы данных** поля.</span><span class="sxs-lookup"><span data-stu-id="48a86-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="48a86-406">Формат: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="48a86-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="48a86-407">Введите hello **имя базы данных** в соответствующее поле hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="48a86-408">Введите hello *имя пользователя SQL* в hello **имя учетной записи пользователя сервера**и hello *пароль* в hello **пароль учетной записи пользователя сервера**.</span><span class="sxs-lookup"><span data-stu-id="48a86-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="48a86-409">Проверьте hello **принимать любой сертификат сервера** параметр.</span><span class="sxs-lookup"><span data-stu-id="48a86-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="48a86-410">В hello **запроса базы данных** Измените текстовое поле, вставьте запрос hello какие извлекает hello необходимые поля (включая все вычисляемые поля, такие как метки hello) базы данных и вниз образцы размер выборки toohello требуемого hello данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="48a86-411">Пример эксперимента двоичной классификации, чтение данных непосредственно из базы данных хранилища данных SQL hello: hello рисунке (Помните tooreplace hello имена таблиц nyctaxi_trip и nyctaxi_fare схемой hello имя и hello имена таблиц, который использовался в вашей Пошаговое руководство).</span><span class="sxs-lookup"><span data-stu-id="48a86-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="48a86-412">Подобные эксперименты можно сконструировать для задач мультиклассовой классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="48a86-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Чат Машинного обучения Azure][10]

> [!IMPORTANT]
> <span data-ttu-id="48a86-414">В hello моделирования данных по извлечению и выборки запроса примеры, приведенные в предыдущих разделах **все метки для моделирования упражнений hello трех включаются в запрос hello**.</span><span class="sxs-lookup"><span data-stu-id="48a86-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="48a86-415">(Обязательный) в каждом hello моделирования упражнения важно слишком**исключить** hello ненужные метки для hello другие две проблемы и любые другие **целевой утечки**.</span><span class="sxs-lookup"><span data-stu-id="48a86-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="48a86-416">Например, при использовании двоичной классификации, используйте метки hello **чаевых оставил зависимости** и исключить hello поля **совет\_класса**, **совет\_сумма**, и **общее\_сумма**.</span><span class="sxs-lookup"><span data-stu-id="48a86-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="48a86-417">последний Hello оплачиваются утечки целевой, так как они предполагают совет hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="48a86-418">tooexclude утечек целевой, или ненужных столбцов могут использовать hello [Выбор столбцов в наборе данных] [ select-columns] модуля или hello [редактирование метаданных] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="48a86-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="48a86-419">Дополнительные сведения см. на страницах справки модулей [Select Columns in Dataset][select-columns] (Выбор столбцов в наборе данных) и [Edit Metadata][edit-metadata] (Изменение метаданных).</span><span class="sxs-lookup"><span data-stu-id="48a86-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="48a86-420"><a name="mldeploy"></a>Развертывание моделей в службе Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="48a86-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="48a86-421">Когда модель готова, можно легко развернуть его веб-службы непосредственно из эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="48a86-422">Дополнительные сведения о развертывании веб-служб Azure ML см. в статье [Развертывание веб-службы Машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="48a86-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="48a86-423">toodeploy веб-службу, необходимо:</span><span class="sxs-lookup"><span data-stu-id="48a86-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="48a86-424">Создать эксперимент по количественной оценке.</span><span class="sxs-lookup"><span data-stu-id="48a86-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="48a86-425">Развертывание веб-службы hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-425">Deploy hello web service.</span></span>

<span data-ttu-id="48a86-426">оценки поэкспериментировать с toocreate **завершен** обучения, эксперимента, нажмите кнопку **создать ЭКСПЕРИМЕНТ ОЦЕНКИ** hello нижней панели действий.</span><span class="sxs-lookup"><span data-stu-id="48a86-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Система оценок Azure][18]

<span data-ttu-id="48a86-428">Машинное обучение Azure попытается toocreate эксперимент оценки на основе компонентов hello эксперимента обучения hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="48a86-429">В частности, она:</span><span class="sxs-lookup"><span data-stu-id="48a86-429">In particular, it will:</span></span>

1. <span data-ttu-id="48a86-430">Сохранить обученную модель hello и удалите hello модели обучающих модулей.</span><span class="sxs-lookup"><span data-stu-id="48a86-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="48a86-431">Определение логических **входному порту** toorepresent hello требуется схема входных данных.</span><span class="sxs-lookup"><span data-stu-id="48a86-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="48a86-432">Определение логических **выходного порта** toorepresent hello ожидаемый web службы выходные данные схемы.</span><span class="sxs-lookup"><span data-stu-id="48a86-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="48a86-433">При создании оценки экспериментов hello, проверьте его и сделать при необходимости измените.</span><span class="sxs-lookup"><span data-stu-id="48a86-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="48a86-434">Типичные корректировки — входного набора данных hello tooreplace или запроса с одним, что исключает поля меток, их будет недоступен при вызове службы hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="48a86-435">Это также размером хорошей практикой tooreduce hello hello входной набор данных или запроса tooa несколько записей, достаточно tooindicate hello входной схемы.</span><span class="sxs-lookup"><span data-stu-id="48a86-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="48a86-436">Для порта вывода hello, он общие tooexclude всех полей ввода и включать только hello **меток оцененных значений** и **оцененных вероятностей** в выходных данных с помощью hello hello [Выбор столбцов в наборе данных ] [ select-columns] модуля.</span><span class="sxs-lookup"><span data-stu-id="48a86-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="48a86-437">В приведенном ниже рисунке hello предоставляется образец эксперимент оценки.</span><span class="sxs-lookup"><span data-stu-id="48a86-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="48a86-438">Окончании toodeploy, нажмите кнопку hello **публикации веб-службы** кнопку hello нижней панели действий.</span><span class="sxs-lookup"><span data-stu-id="48a86-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Публикация Машинного обучения Azure][11]

## <a name="summary"></a><span data-ttu-id="48a86-440">Сводка</span><span class="sxs-lookup"><span data-stu-id="48a86-440">Summary</span></span>
<span data-ttu-id="48a86-441">toorecap то было выполнено в этом учебнике Пошаговое руководство, вы создали среде обработки и анализа данных Azure, работали с большой открытый набор данных переводить его через hello процесс обработки и анализа данных для группы, все возможности hello со обучение toomodel получения данных, а затем toohello развертывание веб-службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="48a86-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="48a86-442">Сведения о лицензии</span><span class="sxs-lookup"><span data-stu-id="48a86-442">License information</span></span>
<span data-ttu-id="48a86-443">Это пошаговое руководство по примеру и соответствующую ему коллекцию скриптов и IPython notebook(s) совместно корпорацией Майкрософт в рамках лицензии MIT hello.</span><span class="sxs-lookup"><span data-stu-id="48a86-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="48a86-444">Проверьте файл LICENSE.txt hello в каталоге hello hello образца кода на GitHub для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="48a86-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="48a86-445">Ссылки</span><span class="sxs-lookup"><span data-stu-id="48a86-445">References</span></span>
<span data-ttu-id="48a86-446">•    [Страница загрузки данных о поездках такси Нью-Йорка (Andrés Monroy)](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="48a86-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="48a86-447">•    [Получение данных о поездках такси Нью-Йорка на основании FOIL (Chris Whong)](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="48a86-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="48a86-448">•    [Статистические данные о комиссионных сборах за аренду такси и лимузинов Нью-Йорка](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="48a86-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
