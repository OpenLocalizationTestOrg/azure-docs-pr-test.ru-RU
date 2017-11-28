---
title: "aaaSample данных в SQL Server в Azure | Документы Microsoft"
description: "Выборка данных на сервере SQL Server в Azure"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="a1932-103"><a name="heading"></a>Выборка данных на сервере SQL Server в Azure</span><span class="sxs-lookup"><span data-stu-id="a1932-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="a1932-104">В этом документе показано, как сохранить toosample данных в SQL Server в Azure с помощью SQL или языка программирования Python hello.</span><span class="sxs-lookup"><span data-stu-id="a1932-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="a1932-105">Здесь также показано, как toomove выборке данных в машинном обучении Azure путем его сохранения файла tooa, поместив его tooan BLOB-объектов Azure и их считывания в студию машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a1932-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="a1932-106">Выборка Python Hello использует hello [pyodbc](https://code.google.com/p/pyodbc/) tooSQL tooconnect ODBC библиотеки Server в Azure и hello [Pandas](http://pandas.pydata.org/) библиотеки toodo hello выборки.</span><span class="sxs-lookup"><span data-stu-id="a1932-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="a1932-107">Hello пример кода SQL в этом документе предполагается, что hello данных находится в SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="a1932-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="a1932-108">Если это не так, можно найти слишком[перемещение данных tooSQL Server в Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) инструкции о том, как toomove вашей tooSQL данных сервера в Azure.</span><span class="sxs-lookup"><span data-stu-id="a1932-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="a1932-109">следующие Hello **меню** связывает tootopics, описывающие как toosample данные из различных средах хранилища.</span><span class="sxs-lookup"><span data-stu-id="a1932-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="a1932-110">**Для чего нужна выборка данных?**</span><span class="sxs-lookup"><span data-stu-id="a1932-110">**Why sample your data?**</span></span>
<span data-ttu-id="a1932-111">При планировании tooanalyze dataset hello имеет большой размер, это обычно tooreduce данных рекомендуется toodown образец hello его tooa размер меньший, но репрезентативный и управляемость.</span><span class="sxs-lookup"><span data-stu-id="a1932-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="a1932-112">Это способствует пониманию данных, их исследованию и проектированию характеристик.</span><span class="sxs-lookup"><span data-stu-id="a1932-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="a1932-113">Ее роль в hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) — tooenable быстрого создания прототипов функций обработки данных hello и машинного обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="a1932-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="a1932-114">Эта задача выборка является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="a1932-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="a1932-115"><a name="SQL"></a>Использование SQL</span><span class="sxs-lookup"><span data-stu-id="a1932-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="a1932-116">В этом разделе описываются способы, с помощью SQL tooperform простую случайную выборку данных hello базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="a1932-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="a1932-117">Выберите нужный метод в зависимости от размера ваших данных и их распределения.</span><span class="sxs-lookup"><span data-stu-id="a1932-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="a1932-118">Hello две следующие пункты показывают, как toouse newid в SQL Server tooperform hello выборки.</span><span class="sxs-lookup"><span data-stu-id="a1932-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="a1932-119">Hello выбранного метода в зависимости от способа случайных toobe образец hello (pk_id в следующем образце кода hello предполагается toobe автоматического создания первичного ключа).</span><span class="sxs-lookup"><span data-stu-id="a1932-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="a1932-120">Менее строгая случайная выборка</span><span class="sxs-lookup"><span data-stu-id="a1932-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="a1932-121">Более случайная выборка</span><span class="sxs-lookup"><span data-stu-id="a1932-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="a1932-122">Для выборки можно также использовать предложение TABLESAMPLE, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a1932-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="a1932-123">Это может быть лучшим вариантом, если размер данных велик (предполагается, что данные на разных страницах не сопоставляются) и toocomplete hello запроса слишком много времени.</span><span class="sxs-lookup"><span data-stu-id="a1932-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="a1932-124">Можно просматривать данные этой выборки и создавать характеристики, сохранив ее в новой таблице</span><span class="sxs-lookup"><span data-stu-id="a1932-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="a1932-125"><a name="sql-aml"></a>Подключение tooAzure машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a1932-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="a1932-126">Вы можете напрямую использовать примеры запросов hello выше hello машинного обучения Azure [импорта данных] [ import-data] данные toodown образец hello модуля на hello полет и переведите его в эксперимент машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="a1932-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="a1932-127">Ниже приведен снимок экрана с помощью hello чтения модуля tooread hello выборки данных:</span><span class="sxs-lookup"><span data-stu-id="a1932-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![считыватель sql][1]

## <span data-ttu-id="a1932-129"><a name="python"></a>С помощью языка программирования Python hello</span><span class="sxs-lookup"><span data-stu-id="a1932-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="a1932-130">В этом разделе демонстрируется использование hello [pyodbc библиотеки](https://code.google.com/p/pyodbc/) tooestablish ODBC подключения tooa базы данных SQL server в Python.</span><span class="sxs-lookup"><span data-stu-id="a1932-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="a1932-131">строку подключения базы данных Hello таков: (Замените servername, dbname, имя пользователя и пароль конфигурацию):</span><span class="sxs-lookup"><span data-stu-id="a1932-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="a1932-132">Hello [Pandas](http://pandas.pydata.org/) библиотеки в Python предоставляет широкий набор средств анализа данных и структур данных для работы с данными для программирования Python.</span><span class="sxs-lookup"><span data-stu-id="a1932-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="a1932-133">Приведенный ниже код Hello считывает 0,1% образец hello данных из таблицы в базе данных Azure SQL в данных Pandas:</span><span class="sxs-lookup"><span data-stu-id="a1932-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="a1932-134">Теперь можно работать с данными выборки hello в кадре данных Pandas hello.</span><span class="sxs-lookup"><span data-stu-id="a1932-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="a1932-135"><a name="python-aml"></a>Подключение tooAzure машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a1932-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="a1932-136">Можно использовать следующие образец кода toosave hello данных уменьшается tooa файл hello и отправьте его tooan BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="a1932-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="a1932-137">Hello данные в большом двоичном объекте hello непосредственно считываются в эксперимента обучения машины Azure с помощью hello [импорта данных] [ import-data] модуля.</span><span class="sxs-lookup"><span data-stu-id="a1932-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="a1932-138">Ниже приведены шаги Hello.</span><span class="sxs-lookup"><span data-stu-id="a1932-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="a1932-139">Запись hello pandas данных кадра tooa локального файла</span><span class="sxs-lookup"><span data-stu-id="a1932-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="a1932-140">Отправка больших двоичных объектов tooAzure локального файла</span><span class="sxs-lookup"><span data-stu-id="a1932-140">Upload local file tooAzure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="a1932-141">Чтение данных из больших двоичных объектов Azure с помощью машинного обучения Azure [импорта данных] [ import-data] модуля, как показано ниже захвата экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="a1932-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![большой двоичный объект считывателя][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="a1932-143">Hello командного процесса обработки и анализа данных в примере действие</span><span class="sxs-lookup"><span data-stu-id="a1932-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="a1932-144">Пример Пошаговое руководство с начала до конца hello командного процесса обработки и анализа данных с помощью набора общих см [командного процесса обработки и анализа данных в действии: с помощью SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a1932-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
