---
title: "Изучение данных на виртуальной машине SQL Server в Azure | Документация Майкрософт"
description: "Изучение данных и создание характеристик на виртуальной машине SQL Server в Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 16fabb29bdc8ec770efd843e18e9016e338a8f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="8bff8-103"><a name="heading"></a>Обработка данных в виртуальной машине SQL Server на платформе Azure</span><span class="sxs-lookup"><span data-stu-id="8bff8-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="8bff8-104">В этом документе описывается изучение данных и создание характеристик для данных, хранящихся в виртуальной машине SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="8bff8-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="8bff8-105">Это можно сделать путем структурирования данных с помощью SQL или с использованием языка программирования, например Python.</span><span class="sxs-lookup"><span data-stu-id="8bff8-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="8bff8-106">В образцах инструкций SQL, содержащихся в данном документе, предполагается, что данные находятся на сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8bff8-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="8bff8-107">Если это не так, обратитесь к карте обработки облачных данных, чтобы узнать, как переместить данные в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8bff8-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="8bff8-108"><a name="SQL"></a>Использование SQL</span><span class="sxs-lookup"><span data-stu-id="8bff8-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="8bff8-109">В данном разделе с помощью SQL описываются следующие задачи по структурированию данных:</span><span class="sxs-lookup"><span data-stu-id="8bff8-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="8bff8-110">Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="8bff8-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="8bff8-111">Создание характеристик</span><span class="sxs-lookup"><span data-stu-id="8bff8-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="8bff8-112"><a name="sql-dataexploration"></a>Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="8bff8-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="8bff8-113">Вот несколько примеров сценариев SQL, которые можно использовать для изучения хранилищ данных в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8bff8-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="8bff8-114">Для практического примера можно использовать [набор данных о такси Нью-Йорка](http://www.andresmh.com/nyctaxitrips/) и статью IPNB под названием [Структурирование данных Нью-Йорка с помощью IPython Notebook и SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb), содержащую полное пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="8bff8-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="8bff8-115">Получение количества наблюдений за день</span><span class="sxs-lookup"><span data-stu-id="8bff8-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="8bff8-116">Получение уровней в столбце категорий</span><span class="sxs-lookup"><span data-stu-id="8bff8-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="8bff8-117">Получение числа уровней в сочетании двух столбцов категорий</span><span class="sxs-lookup"><span data-stu-id="8bff8-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="8bff8-118">Получение распределения для числовых столбцов</span><span class="sxs-lookup"><span data-stu-id="8bff8-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="8bff8-119"><a name="sql-featuregen"></a>Создание характеристик</span><span class="sxs-lookup"><span data-stu-id="8bff8-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="8bff8-120">В этом разделе мы опишем способы создания характеристик с помощью SQL:</span><span class="sxs-lookup"><span data-stu-id="8bff8-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="8bff8-121">Создание характеристик на основе количества</span><span class="sxs-lookup"><span data-stu-id="8bff8-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="8bff8-122">Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="8bff8-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="8bff8-123">Развертывание характеристик из одного столбца</span><span class="sxs-lookup"><span data-stu-id="8bff8-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="8bff8-124">После создания дополнительных компонентов можно либо добавить их в виде столбцов в существующую таблицу, либо создать новую таблицу с дополнительными компонентами и первичным ключом, которую можно будет объединить с исходной таблицей.</span><span class="sxs-lookup"><span data-stu-id="8bff8-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <span data-ttu-id="8bff8-125"><a name="sql-countfeature"></a>Создание характеристик на основе количества</span><span class="sxs-lookup"><span data-stu-id="8bff8-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="8bff8-126">В следующих примерах показаны два способа создания количественных характеристик.</span><span class="sxs-lookup"><span data-stu-id="8bff8-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="8bff8-127">В первом способе используется условная сумма, а во втором — предложение where.</span><span class="sxs-lookup"><span data-stu-id="8bff8-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="8bff8-128">Затем их можно объединить с исходной таблицей (с помощью столбцов первичных ключей), чтобы включить количественные характеристики вместе с исходными данными.</span><span class="sxs-lookup"><span data-stu-id="8bff8-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="8bff8-129"><a name="sql-binningfeature"></a>Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="8bff8-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="8bff8-130">В следующем примере показано, как создать группированные характеристики, сгруппировав (с использованием пяти ячеек) числовой столбец, который взамен можно использовать как характеристику:</span><span class="sxs-lookup"><span data-stu-id="8bff8-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="8bff8-131"><a name="sql-featurerollout"></a>Развертывание характеристик из одного столбца</span><span class="sxs-lookup"><span data-stu-id="8bff8-131"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="8bff8-132">В этом разделе мы покажем, как развернуть одиночный столбец в таблице для создания дополнительных характеристик.</span><span class="sxs-lookup"><span data-stu-id="8bff8-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="8bff8-133">В примере предполагается, что в таблице, из которой вы намерены создать характеристики, содержится столбец широты или долготы.</span><span class="sxs-lookup"><span data-stu-id="8bff8-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="8bff8-134">Вот краткое руководство по данным широты/долготы расположения (на основе ресурса stackoverflow): [Как измерить точность широты и долготы](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude).</span><span class="sxs-lookup"><span data-stu-id="8bff8-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="8bff8-135">Перед присвоением характеристики полю расположения полезно понять следующее:</span><span class="sxs-lookup"><span data-stu-id="8bff8-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="8bff8-136">Знак сообщает, в каком полушарии мы находимся: северном или южном, восточном или западном.</span><span class="sxs-lookup"><span data-stu-id="8bff8-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="8bff8-137">Ненулевая цифра сотен указывает, что используется долгота, а не широта!</span><span class="sxs-lookup"><span data-stu-id="8bff8-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="8bff8-138">Цифра десятков сообщает положение с точностью примерно 1000 километров.</span><span class="sxs-lookup"><span data-stu-id="8bff8-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="8bff8-139">Она указывает, на каком континенте или в каком океане мы находимся.</span><span class="sxs-lookup"><span data-stu-id="8bff8-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="8bff8-140">Цифра единиц (один десятичный градус) дает положение с точностью до 111 километров (60 морских миль, или около 69 миль).</span><span class="sxs-lookup"><span data-stu-id="8bff8-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="8bff8-141">Она может приблизительно сообщить нам, в каком крупном регионе или стране мы находимся.</span><span class="sxs-lookup"><span data-stu-id="8bff8-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="8bff8-142">Первый десятичный разряд соответствует точности до 11,1 км: он позволяет различать положение одного крупного города относительно соседнего крупного города.</span><span class="sxs-lookup"><span data-stu-id="8bff8-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="8bff8-143">Второй десятичный разряд соответствует точности до 1,1 км: он позволяет различать мелкие населенные пункты.</span><span class="sxs-lookup"><span data-stu-id="8bff8-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="8bff8-144">Третий десятичный разряд соответствует точности до 110 м: он позволяет идентифицировать крупное сельскохозяйственное поле или кампус учреждения.</span><span class="sxs-lookup"><span data-stu-id="8bff8-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="8bff8-145">Четвертый десятичный разряд соответствует точности до 11 м: он позволяет идентифицировать участок земли.</span><span class="sxs-lookup"><span data-stu-id="8bff8-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="8bff8-146">Это сравнимо с типичной точностью устройства GPS без коррекции при отсутствии помех.</span><span class="sxs-lookup"><span data-stu-id="8bff8-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="8bff8-147">Пятый десятичный разряд соответствует точности до 1,1 м: он позволяет отличать деревья друг от друга.</span><span class="sxs-lookup"><span data-stu-id="8bff8-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="8bff8-148">Точность этого уровня с помощью коммерческих GPS-устройств может быть достигнута только при использовании дифференциальной коррекции.</span><span class="sxs-lookup"><span data-stu-id="8bff8-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="8bff8-149">Шестой десятичный разряд соответствует точности до 0,11 м: это значение можно использовать для подробной детализации сооружений, для проектирования ландшафтов, строительства дорог.</span><span class="sxs-lookup"><span data-stu-id="8bff8-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="8bff8-150">Этого уровня более чем достаточно для отслеживания движения ледников и рек.</span><span class="sxs-lookup"><span data-stu-id="8bff8-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="8bff8-151">Его можно достичь с помощью тщательного измерения с использованием GPS, например при дифференциальной коррекции GPS.</span><span class="sxs-lookup"><span data-stu-id="8bff8-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="8bff8-152">Сведения о местоположении можно характеризовать следующим образом, выделяя информацию о регионе, местоположении и городе.</span><span class="sxs-lookup"><span data-stu-id="8bff8-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="8bff8-153">Обратите внимание на то, что для получения сведений об области или регионе можно также вызвать конечную точку REST, например интерфейс Bing Maps API, доступный в разделе [Поиск расположения по точке](https://msdn.microsoft.com/library/ff701710.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8bff8-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="8bff8-154">Характеристики на основе расположения можно в дальнейшем использовать для создания дополнительных количественных характеристик, как было описано ранее.</span><span class="sxs-lookup"><span data-stu-id="8bff8-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="8bff8-155">Можно программным путем вставлять записи с использованием выбранного языка.</span><span class="sxs-lookup"><span data-stu-id="8bff8-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="8bff8-156">Для повышения эффективности записи данные можно вставлять блоками — пример такого решения с использованием pyodbc см. в статье [Пример HelloWorld с обращением к SQL Server с помощью Python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="8bff8-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="8bff8-157">Другой вариант — вставить данные в базу данных с использованием [служебной программы BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="8bff8-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="8bff8-158"><a name="sql-aml"></a>Подключение к службе машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="8bff8-158"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="8bff8-159">Новую созданную характеристику можно добавить в виде столбца в существующую таблицу или сохранить в новой таблице и объединить с существующей таблицей для машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="8bff8-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="8bff8-160">Вы можете создать характеристики и открыть доступ к ним, если они уже созданы, с помощью модуля [Импорт данных][import-data] в Машинном обучении Azure, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8bff8-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![считыватели azureml][1] 

## <span data-ttu-id="8bff8-162"><a name="python"></a>Использование языка программирования, например Python</span><span class="sxs-lookup"><span data-stu-id="8bff8-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="8bff8-163">Использование языка Python для просмотра данных и создания характеристик, когда данные находятся в SQL Server, подобно обработке данных в большом двоичном объекте Azure с использованием Python, как описано в статье [Обработка больших двоичных данных Azure с применением методов расширенного анализа](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="8bff8-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="8bff8-164">Данные необходимо загрузить из базы данных во фрейм данных pandas для последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="8bff8-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="8bff8-165">В этом разделе документирован процесс подключения к базе данных и загрузки данных во фрейм данных.</span><span class="sxs-lookup"><span data-stu-id="8bff8-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="8bff8-166">Для подключения к базе данных SQL Server из языка Python с использованием pyodbc можно применить следующий формат строки подключения (замените servername, dbname, username и password соответствующими значениями имени сервера, имени БД, имени пользователя и пароля):</span><span class="sxs-lookup"><span data-stu-id="8bff8-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="8bff8-167">[Библиотека Pandas](http://pandas.pydata.org/) в языке Python предлагает большой выбор структур данных и средств анализа данных для манипуляций со значениями с помощью языке Python.</span><span class="sxs-lookup"><span data-stu-id="8bff8-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="8bff8-168">Приведенный ниже код считывает результаты, возвращенные из базы данных SQL Server, во фрейм данных Pandas:</span><span class="sxs-lookup"><span data-stu-id="8bff8-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="8bff8-169">Теперь можно работать с фреймом данных Pandas, как описано в статье [Обработка больших двоичных данных Azure с применением методов расширенного анализа](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="8bff8-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="8bff8-170">Пример применения обработки данных в Azure на практике</span><span class="sxs-lookup"><span data-stu-id="8bff8-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="8bff8-171">Пример комплексного пошагового руководства по обработке и анализу данных в Azure с использованием общедоступного набора данных см. в статье [Процесс обработки и анализа данных группы на практике: использование SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8bff8-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

