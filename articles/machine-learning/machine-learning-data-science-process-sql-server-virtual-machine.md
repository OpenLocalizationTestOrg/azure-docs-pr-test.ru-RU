---
title: "aaaExplore данных на виртуальной машине SQL Server в Azure | Документы Microsoft"
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
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="5a317-103"><a name="heading"></a>Обработка данных в виртуальной машине SQL Server на платформе Azure</span><span class="sxs-lookup"><span data-stu-id="5a317-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="5a317-104">В этом документе рассматриваются как tooexplore данные и создавать признаки для данных, хранящихся в виртуальной Машине SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="5a317-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="5a317-105">Это можно сделать путем структурирования данных с помощью SQL или с использованием языка программирования, например Python.</span><span class="sxs-lookup"><span data-stu-id="5a317-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="5a317-106">Hello пример инструкции SQL в этом документе предполагается, что данные находятся в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5a317-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="5a317-107">В противном случае обратитесь toohello облачных данных обработки и анализа процесса карты toolearn как toomove вашей tooSQL данные сервера.</span><span class="sxs-lookup"><span data-stu-id="5a317-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="5a317-108"><a name="SQL"></a>Использование SQL</span><span class="sxs-lookup"><span data-stu-id="5a317-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="5a317-109">Описание hello следующих данных wrangling задачи в этом разделе, с помощью SQL:</span><span class="sxs-lookup"><span data-stu-id="5a317-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="5a317-110">Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="5a317-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="5a317-111">Создание характеристик</span><span class="sxs-lookup"><span data-stu-id="5a317-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="5a317-112"><a name="sql-dataexploration"></a>Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="5a317-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="5a317-113">Вот несколько примеры сценариев SQL, которые можно использовать tooexplore хранилищ данных в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5a317-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="5a317-114">Практический пример, можно использовать hello [dataset такси NYC](http://www.andresmh.com/nyctaxitrips/) и toohello IPNB под названием [wrangling NYC данных с помощью ноутбук IPython и SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) руководство с начала до конца.</span><span class="sxs-lookup"><span data-stu-id="5a317-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="5a317-115">Получение числа hello наблюдения за день</span><span class="sxs-lookup"><span data-stu-id="5a317-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="5a317-116">Получить уровней hello в категориальный столбец</span><span class="sxs-lookup"><span data-stu-id="5a317-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="5a317-117">Получить hello количество уровней в сочетании с двумя категориальные столбцы</span><span class="sxs-lookup"><span data-stu-id="5a317-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="5a317-118">Получить hello распространения для числовых столбцов.</span><span class="sxs-lookup"><span data-stu-id="5a317-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="5a317-119"><a name="sql-featuregen"></a>Создание функций</span><span class="sxs-lookup"><span data-stu-id="5a317-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="5a317-120">В этом разделе мы опишем способы создания характеристик с помощью SQL:</span><span class="sxs-lookup"><span data-stu-id="5a317-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="5a317-121">Создание характеристик на основе количества</span><span class="sxs-lookup"><span data-stu-id="5a317-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="5a317-122">Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="5a317-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="5a317-123">Развертывание компонентов hello из одного столбца</span><span class="sxs-lookup"><span data-stu-id="5a317-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="5a317-124">После создания дополнительных компонентов можно добавлять их в виде столбцов toohello существующую таблицу или создать новую таблицу с дополнительные функции hello и первичный ключ, который можно объединить с исходной таблицей hello.</span><span class="sxs-lookup"><span data-stu-id="5a317-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="5a317-125"><a name="sql-countfeature"></a>Создание характеристик на основе количества</span><span class="sxs-lookup"><span data-stu-id="5a317-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="5a317-126">Hello следующих примерах показано два способа создания функции count.</span><span class="sxs-lookup"><span data-stu-id="5a317-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="5a317-127">Первый метод Hello использует суммирования и второй метод использует hello hello предложение «where».</span><span class="sxs-lookup"><span data-stu-id="5a317-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="5a317-128">Затем их можно объединить с hello исходной таблицы (с помощью первичных ключевых столбцов) toohave число функций вместе с исходными данными hello.</span><span class="sxs-lookup"><span data-stu-id="5a317-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="5a317-129"><a name="sql-binningfeature"></a>Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="5a317-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="5a317-130">Hello следующем примере показано, как toogenerate сегментации функции путем сегментирования (с помощью пять ячеек) столбца числовых значений, можно использовать как компонент:</span><span class="sxs-lookup"><span data-stu-id="5a317-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="5a317-131"><a name="sql-featurerollout"></a>Развертывание компонентов hello из одного столбца</span><span class="sxs-lookup"><span data-stu-id="5a317-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="5a317-132">В этом разделе показано как tooroll out одиночный столбец в таблице toogenerate дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="5a317-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="5a317-133">пример Hello предполагается наличие Широта и долгота столбец в таблице hello, из которого вы пытаетесь toogenerate функции.</span><span class="sxs-lookup"><span data-stu-id="5a317-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="5a317-134">Ниже приведен краткий учебник на данные о местоположении широты и долготы (ресурсов из stackoverflow [как toomeasure hello точность широты и долготы?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="5a317-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="5a317-135">Это полезно toounderstand перед featurizing hello поле «расположение»:</span><span class="sxs-lookup"><span data-stu-id="5a317-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="5a317-136">знак Hello указывает мы, являются ли вверх или вниз, Восточная или Западная по всему миру hello.</span><span class="sxs-lookup"><span data-stu-id="5a317-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="5a317-137">Ненулевая цифра сотен указывает, что используется долгота, а не широта!</span><span class="sxs-lookup"><span data-stu-id="5a317-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="5a317-138">цифра Hello десятков дает tooabout позиции 1 000 километров.</span><span class="sxs-lookup"><span data-stu-id="5a317-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="5a317-139">Она указывает, на каком континенте или в каком океане мы находимся.</span><span class="sxs-lookup"><span data-stu-id="5a317-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="5a317-140">Hello единиц (один десятичное) дает вверх километрах too111 (60 миля, около 69 миль).</span><span class="sxs-lookup"><span data-stu-id="5a317-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="5a317-141">Она может приблизительно сообщить нам, в каком крупном регионе или стране мы находимся.</span><span class="sxs-lookup"><span data-stu-id="5a317-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="5a317-142">первый десятичный разряд Hello стоит копирование км too11.1: она различает hello положение одного большого города из соседних большого города.</span><span class="sxs-lookup"><span data-stu-id="5a317-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="5a317-143">Hello двух знаков после запятой стоит вверх too1.1 км: его можно разделить один village из hello рядом.</span><span class="sxs-lookup"><span data-stu-id="5a317-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="5a317-144">Третий десятичный разряд Hello стоит копирование too110 m: можно указать, больших agricultural поля или учреждений университета.</span><span class="sxs-lookup"><span data-stu-id="5a317-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="5a317-145">Четвертый десятичный разряд Hello стоит копирование too11 m: можно указать, участка земли.</span><span class="sxs-lookup"><span data-stu-id="5a317-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="5a317-146">Это Типичная точность сопоставимых toohello Неисправленные GPS устройства с без помех.</span><span class="sxs-lookup"><span data-stu-id="5a317-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="5a317-147">Пятый десятичный разряд Hello стоит копирование too1.1 m: его по ширине позволяет отличить деревьев друг от друга.</span><span class="sxs-lookup"><span data-stu-id="5a317-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="5a317-148">Уровень точности toothis с коммерческих GPS-устройства могут быть осуществлены только с разностной исправления.</span><span class="sxs-lookup"><span data-stu-id="5a317-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="5a317-149">шестой десятичный разряд Hello стоит копирование m: too0.11, это можно использовать для размещения структуры проектирования ландшафтов, подробно построение дороги.</span><span class="sxs-lookup"><span data-stu-id="5a317-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="5a317-150">Этого уровня более чем достаточно для отслеживания движения ледников и рек.</span><span class="sxs-lookup"><span data-stu-id="5a317-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="5a317-151">Его можно достичь с помощью тщательного измерения с использованием GPS, например при дифференциальной коррекции GPS.</span><span class="sxs-lookup"><span data-stu-id="5a317-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="5a317-152">сведения о расположении Hello может быть Признак следующим образом отделить региону, расположение и сведения о городе.</span><span class="sxs-lookup"><span data-stu-id="5a317-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="5a317-153">Обратите внимание, что также можно вызывать конечную точку REST, такие как API службы Bing Maps см. в [найти расположение точкой](https://msdn.microsoft.com/library/ff701710.aspx) tooget сведения о регионе или районе hello.</span><span class="sxs-lookup"><span data-stu-id="5a317-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

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

<span data-ttu-id="5a317-154">Эти функции на основе расположения можно дополнительно используется toogenerate число дополнительных функций как описано выше.</span><span class="sxs-lookup"><span data-stu-id="5a317-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="5a317-155">Можно программным образом вставить записи hello, с помощью выбранного языка.</span><span class="sxs-lookup"><span data-stu-id="5a317-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="5a317-156">Может потребоваться tooinsert данных hello в блоки повышения эффективности записи tooimprove (пример того, как toodo этот использовании pyodbc см [tooaccess образец HelloWorld SQLServer с python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="5a317-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="5a317-157">Другой вариант — tooinsert данные в базе данных hello, с помощью hello [служебная программа BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a317-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="5a317-158"><a name="sql-aml"></a>Подключение tooAzure машинного обучения</span><span class="sxs-lookup"><span data-stu-id="5a317-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="5a317-159">Hello только что созданный компонент может добавляются как таблица tooan существующий столбец или хранится в новую таблицу и объединена с исходной таблицей hello для машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="5a317-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="5a317-160">Функции можно создать или получить доступ, уже созданы с помощью hello [импорта данных] [ import-data] в машинном обучении Azure как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="5a317-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![считыватели azureml][1] 

## <span data-ttu-id="5a317-162"><a name="python"></a>Использование языка программирования, например Python</span><span class="sxs-lookup"><span data-stu-id="5a317-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="5a317-163">С помощью Python tooexplore данных и создавать функции при схожие данные tooprocessing hello данные хранятся в SQL Server в BLOB-объектов Azure с помощью Python, как описано в документе [данные больших двоичных объектов Azure процесс в среде обработки и анализа данных](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="5a317-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="5a317-164">Hello данных должен toobe загружаются из базы данных hello в кадр данных pandas и затем обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="5a317-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="5a317-165">Мы документа hello процесс соединения toohello базы данных и загрузку данных hello в кадр данных hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5a317-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="5a317-166">Hello следующий формат строки соединения может быть база данных SQL Server используется tooconnect tooa из Python, с помощью pyodbc (заменить имя сервера, dbname, имя пользователя и пароль особые значения):</span><span class="sxs-lookup"><span data-stu-id="5a317-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="5a317-167">Hello [Pandas библиотеки](http://pandas.pydata.org/) в Python предоставляет широкий набор средств анализа данных и структур данных для работы с данными для программирования Python.</span><span class="sxs-lookup"><span data-stu-id="5a317-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="5a317-168">Приведенный ниже код Hello считывает hello результаты, возвращенные из базы данных SQL Server, в кадр данных Pandas:</span><span class="sxs-lookup"><span data-stu-id="5a317-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="5a317-169">Теперь можно работать с кадра данных Pandas hello, как описано в статье hello [данные больших двоичных объектов Azure процесс в среде обработки и анализа данных](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="5a317-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="5a317-170">Пример применения обработки данных в Azure на практике</span><span class="sxs-lookup"><span data-stu-id="5a317-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="5a317-171">Пошаговое руководство с начала до конца пример hello процесс обработки и анализа данных Azure, используя открытый набор данных, в разделе [Azure процесс обработки и анализа данных в действие](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5a317-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

