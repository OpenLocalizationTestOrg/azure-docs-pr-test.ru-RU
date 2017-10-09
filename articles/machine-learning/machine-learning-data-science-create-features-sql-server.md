---
title: "функции aaaCreate для данных в SQL Server с помощью SQL и Python | Документы Microsoft"
description: "Обработка данных из SQL Azure"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="bf1fa-103">Создание характеристик для данных в SQL Server с помощью SQL и Python</span><span class="sxs-lookup"><span data-stu-id="bf1fa-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="bf1fa-104">В этом документе показано, как функции toogenerate для данных, хранящихся в виртуальной Машине SQL Server в Azure, чтобы алгоритмы более эффективно узнать из данных hello.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-104">This document shows how toogenerate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from hello data.</span></span> <span data-ttu-id="bf1fa-105">Это можно сделать с помощью SQL или с использованием языка программирования, например Python. Здесь показаны оба варианта.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="bf1fa-106">Это **меню** связывает tootopics, описано, как toocreate функции для данных в различных средах.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="bf1fa-107">Эта задача является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="bf1fa-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="bf1fa-108">Практический пример, можно найти hello [dataset такси NYC](http://www.andresmh.com/nyctaxitrips/) и toohello IPNB под названием [wrangling NYC данных с помощью ноутбук IPython и SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) руководство с начала до конца.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-108">For a practical example, you can consult hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bf1fa-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bf1fa-109">Prerequisites</span></span>
<span data-ttu-id="bf1fa-110">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="bf1fa-110">This article assumes that you have:</span></span>

* <span data-ttu-id="bf1fa-111">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-111">Created an Azure storage account.</span></span> <span data-ttu-id="bf1fa-112">Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="bf1fa-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="bf1fa-113">Сохранили данные в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="bf1fa-114">Если нет, см. раздел [перемещение данных tooan базы данных SQL Azure для машинного обучения Azure](machine-learning-data-science-move-sql-azure.md) инструкции как toomove hello данных существует.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-114">If you have not, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how toomove hello data there.</span></span>

## <span data-ttu-id="bf1fa-115"><a name="sql-featuregen"></a>Создание характеристик с помощью SQL</span><span class="sxs-lookup"><span data-stu-id="bf1fa-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="bf1fa-116">В этом разделе мы опишем способы создания характеристик с помощью SQL:</span><span class="sxs-lookup"><span data-stu-id="bf1fa-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="bf1fa-117">Создание характеристик на основе количества</span><span class="sxs-lookup"><span data-stu-id="bf1fa-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="bf1fa-118">Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="bf1fa-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="bf1fa-119">Развертывание компонентов hello из одного столбца</span><span class="sxs-lookup"><span data-stu-id="bf1fa-119">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="bf1fa-120">После создания дополнительных компонентов можно добавлять их в виде столбцов toohello существующую таблицу или создать новую таблицу с дополнительные функции hello и первичный ключ, который можно объединить с исходной таблицей hello.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-120">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span>
> 
> 

### <span data-ttu-id="bf1fa-121"><a name="sql-countfeature"></a>Создание характеристик на основе количества</span><span class="sxs-lookup"><span data-stu-id="bf1fa-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="bf1fa-122">В этом документе показаны два способа создания количественных характеристик.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="bf1fa-123">Первый метод Hello использует суммирования и второй метод использует hello hello предложение «where».</span><span class="sxs-lookup"><span data-stu-id="bf1fa-123">hello first method uses conditional sum and hello second method uses hello 'where\` clause.</span></span> <span data-ttu-id="bf1fa-124">Затем их можно объединить с hello исходной таблицы (с помощью первичных ключевых столбцов) toohave число функций вместе с исходными данными hello.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-124">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="bf1fa-125"><a name="sql-binningfeature"></a>Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="bf1fa-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="bf1fa-126">Hello следующем примере показано, как toogenerate сегментации функции путем сегментирования (с использованием 5 ячеек) столбца числовых значений, можно использовать как компонент:</span><span class="sxs-lookup"><span data-stu-id="bf1fa-126">hello following example shows how toogenerate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="bf1fa-127"><a name="sql-featurerollout"></a>Развертывание компонентов hello из одного столбца</span><span class="sxs-lookup"><span data-stu-id="bf1fa-127"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="bf1fa-128">В этом разделе показано горизонтального tooroll один столбец в таблице toogenerate дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-128">In this section, we demonstrate how tooroll-out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="bf1fa-129">пример Hello предполагается наличие Широта и долгота столбец в таблице hello, из которого вы пытаетесь toogenerate функции.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-129">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="bf1fa-130">Вот краткое руководство по данным широты/долготы расположения (на основе ресурса stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span><span class="sxs-lookup"><span data-stu-id="bf1fa-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="bf1fa-131">Это полезно toounderstand перед featurizing hello поле «расположение»:</span><span class="sxs-lookup"><span data-stu-id="bf1fa-131">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="bf1fa-132">знак Hello указывает мы, являются ли вверх или вниз, Восточная или Западная по всему миру hello.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-132">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="bf1fa-133">Ненулевая цифра сотен указывает, что используется долгота, а не широта!</span><span class="sxs-lookup"><span data-stu-id="bf1fa-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="bf1fa-134">цифра Hello десятков дает tooabout позиции 1 000 километров.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-134">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="bf1fa-135">Она указывает, на каком континенте или в каком океане мы находимся.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="bf1fa-136">Hello единиц (один десятичное) дает вверх километрах too111 (60 миля, около 69 миль).</span><span class="sxs-lookup"><span data-stu-id="bf1fa-136">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="bf1fa-137">Она может приблизительно сообщить нам, в каком крупном регионе или стране мы находимся.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="bf1fa-138">первый десятичный разряд Hello стоит копирование км too11.1: она различает hello положение одного большого города из соседних большого города.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-138">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="bf1fa-139">Hello двух знаков после запятой стоит вверх too1.1 км: его можно разделить один village из hello рядом.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-139">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="bf1fa-140">Третий десятичный разряд Hello стоит копирование too110 m: можно указать, больших agricultural поля или учреждений университета.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-140">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="bf1fa-141">Четвертый десятичный разряд Hello стоит копирование too11 m: можно указать, участка земли.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-141">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="bf1fa-142">Это Типичная точность сопоставимых toohello Неисправленные GPS устройства с без помех.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-142">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="bf1fa-143">Hello пятый десятичный разряд стоит копирование too1.1 m: его отличить друг от друга деревьев.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-143">hello fifth decimal place is worth up too1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="bf1fa-144">Уровень точности toothis с коммерческих GPS-устройства могут быть осуществлены только с разностной исправления.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-144">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="bf1fa-145">шестой десятичный разряд Hello стоит копирование m: too0.11, это можно использовать для размещения структуры проектирования ландшафтов, подробно построение дороги.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-145">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="bf1fa-146">Этого уровня более чем достаточно для отслеживания движения ледников и рек.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="bf1fa-147">Его можно достичь с помощью тщательного измерения с использованием GPS, например при дифференциальной коррекции GPS.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="bf1fa-148">сведения о расположении Hello можно может быть Признак следующим образом отделить региону, расположение и сведения о городе.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-148">hello location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="bf1fa-149">Обратите внимание, что один раз, можно также вызвать конечную точку REST, например в API службы Bing Maps `https://msdn.microsoft.com/library/ff701710.aspx` tooget сведения о регионе или районе hello.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/district information.</span></span>

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

<span data-ttu-id="bf1fa-150">Hello над местом на основе возможностей можно дополнительно использовать toogenerate число дополнительных функций, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-150">hello above location based features can be further used toogenerate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="bf1fa-151">Можно программным образом вставить записи hello, с помощью выбранного языка.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-151">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="bf1fa-152">Может потребоваться tooinsert данных hello в блоки повышения эффективности записи tooimprove [см. пример hello toodo этого с помощью pyodbc здесь](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="bf1fa-152">You may need tooinsert hello data in chunks tooimprove write efficiency [Check out hello example of how toodo this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="bf1fa-153">Другой вариант — tooinsert данные в базу данных при помощи hello [служебная программа BCP](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="bf1fa-153">Another alternative is tooinsert data in hello database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="bf1fa-154"><a name="sql-aml"></a>Подключение tooAzure машинного обучения</span><span class="sxs-lookup"><span data-stu-id="bf1fa-154"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="bf1fa-155">Hello только что созданный компонент может добавляются как таблица tooan существующий столбец или хранится в новую таблицу и объединена с исходной таблицей hello для машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-155">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="bf1fa-156">Функции можно создать или получить доступ, уже созданы с помощью hello [импорта данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) модуля в Azure ML, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="bf1fa-156">Features can be generated or accessed if already created, using hello [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![считыватели azureml](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="bf1fa-158"><a name="python"></a>Использование языка программирования, например Python</span><span class="sxs-lookup"><span data-stu-id="bf1fa-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="bf1fa-159">С помощью функции toogenerate Python, когда hello данных в SQL Server — подобные данные tooprocessing в BLOB-объектов Azure с помощью Python, как описано в документе [данных Azure Blob процесса среды вы данных обработки и анализа](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="bf1fa-159">Using Python toogenerate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="bf1fa-160">Hello данных должен toobe загружаются из базы данных hello в кадр данных pandas и затем обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-160">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="bf1fa-161">Мы документа hello процесс соединения toohello базы данных и загрузку данных hello в кадр данных hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-161">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="bf1fa-162">Hello следующий формат строки соединения может быть база данных SQL Server используется tooconnect tooa из Python, с помощью pyodbc (заменить имя сервера, dbname, имя пользователя и пароль особые значения):</span><span class="sxs-lookup"><span data-stu-id="bf1fa-162">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="bf1fa-163">Hello [Pandas библиотеки](http://pandas.pydata.org/) в Python предоставляет широкий набор средств анализа данных и структур данных для работы с данными для программирования Python.</span><span class="sxs-lookup"><span data-stu-id="bf1fa-163">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="bf1fa-164">Приведенный ниже код Hello считывает hello результаты, возвращенные из базы данных SQL Server, в кадр данных Pandas:</span><span class="sxs-lookup"><span data-stu-id="bf1fa-164">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="bf1fa-165">Теперь можно работать с кадра данных Pandas hello, как описано в разделах [создают функции для хранения данных больших двоичных объектов Azure, с помощью Panda](machine-learning-data-science-create-features-blob.md).</span><span class="sxs-lookup"><span data-stu-id="bf1fa-165">Now you can work with hello Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

