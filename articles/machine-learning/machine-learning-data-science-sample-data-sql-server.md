---
title: "Выборка данных на сервере SQL Server в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 1bdcc7175dac325de1144d805e977264524b3fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="292ba-103"><a name="heading"></a>Выборка данных на сервере SQL Server в Azure</span><span class="sxs-lookup"><span data-stu-id="292ba-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="292ba-104">В этом документе описывается процесс выборки данных, хранящихся на сервере SQL Server в Azure, с помощью SQL или языка программирования Python.</span><span class="sxs-lookup"><span data-stu-id="292ba-104">This document shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span></span> <span data-ttu-id="292ba-105">В нем также показано, как переместить данные выборки в службу машинного обучения Azure, сохранив их в файл, передав его в BLOB-объект Azure, а затем считав в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="292ba-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="292ba-106">Процедура выборки Python использует библиотеку [pyodbc](https://code.google.com/p/pyodbc/) ODBC для подключения к SQL Server в Azure и библиотеку [Pandas](http://pandas.pydata.org/) для выполнения выборки.</span><span class="sxs-lookup"><span data-stu-id="292ba-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="292ba-107">Образец кода SQL в этом документе предполагает, что данные содержатся на сервере SQL Server на платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="292ba-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span></span> <span data-ttu-id="292ba-108">Если это не так, воспользуйтесь инструкциями по переносу данных в SQL Server в среде Azure, изложенными в разделе [Перемещение данных в SQL Server в Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) .</span><span class="sxs-lookup"><span data-stu-id="292ba-108">If it is not, please refer to [Move data to SQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how to move your data to SQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="292ba-109">**Меню** ниже содержит ссылки на разделы, в которых описана выборка данных из различных сред хранения.</span><span class="sxs-lookup"><span data-stu-id="292ba-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="292ba-110">**Для чего нужна выборка данных?**</span><span class="sxs-lookup"><span data-stu-id="292ba-110">**Why sample your data?**</span></span>
<span data-ttu-id="292ba-111">Если размер набора данных, который планируется проанализировать, слишком большой, обычно рекомендуется уменьшить выборку данных до размера, который останется репрезентативным и будет более управляемым.</span><span class="sxs-lookup"><span data-stu-id="292ba-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="292ba-112">Это способствует пониманию данных, их исследованию и проектированию характеристик.</span><span class="sxs-lookup"><span data-stu-id="292ba-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="292ba-113">Роль этой операции в [процессе обработки и анализа данных группы (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) состоит в том, чтобы сделать возможным быстрое прототипирование функций обработки данных и моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="292ba-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="292ba-114">Эта задача выборки является одним из этапов [процесса обработки и анализа данных группы (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="292ba-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="292ba-115"><a name="SQL"></a>Использование SQL</span><span class="sxs-lookup"><span data-stu-id="292ba-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="292ba-116">В этом разделе описываются несколько методов использования SQL для выполнения простой случайной выборки из данных, содержащихся в базе данных.</span><span class="sxs-lookup"><span data-stu-id="292ba-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span></span> <span data-ttu-id="292ba-117">Выберите нужный метод в зависимости от размера ваших данных и их распределения.</span><span class="sxs-lookup"><span data-stu-id="292ba-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="292ba-118">Два элемента ниже показывают, как использовать newid в SQL Server для выполнения выборки.</span><span class="sxs-lookup"><span data-stu-id="292ba-118">The two items below show how to use newid in SQL Server to perform the sampling.</span></span> <span data-ttu-id="292ba-119">Выбор метода зависит от того, насколько случайной требуется сделать выборку (pk_id в образце кода ниже предполагается автоматически генерируемым первичным ключом).</span><span class="sxs-lookup"><span data-stu-id="292ba-119">The method you choose depends on how random you want the sample to be (pk_id in the sample code below is assumed to be an auto-generated primary key).</span></span>

1. <span data-ttu-id="292ba-120">Менее строгая случайная выборка</span><span class="sxs-lookup"><span data-stu-id="292ba-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="292ba-121">Более случайная выборка</span><span class="sxs-lookup"><span data-stu-id="292ba-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="292ba-122">Для выборки можно также использовать предложение TABLESAMPLE, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="292ba-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="292ba-123">Этот подход рекомендуется использовать для работы с данными большого размера (предполагается, что данные на разных страницах не коррелируют между собой) и для выполнения запроса в разумные сроки.</span><span class="sxs-lookup"><span data-stu-id="292ba-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="292ba-124">Можно просматривать данные этой выборки и создавать характеристики, сохранив ее в новой таблице</span><span class="sxs-lookup"><span data-stu-id="292ba-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="292ba-125"><a name="sql-aml"></a>Подключение к службе машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="292ba-125"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="292ba-126">Приведенные выше примеры запросов можно использовать непосредственно в модуле [Импорт данных][import-data] Машинного обучения Azure для оперативного сокращения выборки данных и их передачи в эксперимент машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="292ba-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="292ba-127">Ниже показан снимок экрана при использовании модуля Reader для считывания данных выборки:</span><span class="sxs-lookup"><span data-stu-id="292ba-127">A screen shot of using the reader module to read the sampled data is shown below:</span></span>

![считыватель sql][1]

## <span data-ttu-id="292ba-129"><a name="python"></a>Использование языка программирования Python</span><span class="sxs-lookup"><span data-stu-id="292ba-129"><a name="python"></a>Using the Python programming language</span></span>
<span data-ttu-id="292ba-130">В этом разделе демонстрируется использование [библиотеки pyodbc](https://code.google.com/p/pyodbc/) для установки подключения ODBC к Базе данных SQL Server на языке Python.</span><span class="sxs-lookup"><span data-stu-id="292ba-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span></span> <span data-ttu-id="292ba-131">Строка подключения к базе данных выглядит следующим образом (замените servername, dbname, username и password соответственно именем сервера, именем базы данных, именем пользователя и паролем из вашей конфигурации):</span><span class="sxs-lookup"><span data-stu-id="292ba-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="292ba-132">Библиотека [Pandas](http://pandas.pydata.org/) в языке Python предоставляет широкий набор структур данных и средств анализа данных для манипуляций с данными при программировании на языке Python.</span><span class="sxs-lookup"><span data-stu-id="292ba-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="292ba-133">Приведенный ниже код считывает 0,1%-ную выборку данных из таблицы базы данных Azure SQL в данные Pandas:</span><span class="sxs-lookup"><span data-stu-id="292ba-133">The code below reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="292ba-134">Теперь можно работать с данными выборки во фрейме данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="292ba-134">You can now work with the sampled data in the Pandas data frame.</span></span> 

### <span data-ttu-id="292ba-135"><a name="python-aml"></a>Подключение к службе машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="292ba-135"><a name="python-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="292ba-136">С помощью следующего образца кода можно сохранить данные уменьшенной выборки в файл и передать его в BLOB-объект Azure.</span><span class="sxs-lookup"><span data-stu-id="292ba-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span></span> <span data-ttu-id="292ba-137">Данные из большого двоичного объекта можно считать непосредственно в эксперимент машинного обучения Azure с помощью модуля [Импорт данных][import-data].</span><span class="sxs-lookup"><span data-stu-id="292ba-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span></span> <span data-ttu-id="292ba-138">Для этого необходимо выполнить следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="292ba-138">The steps are as follows:</span></span> 

1. <span data-ttu-id="292ba-139">Запись фрейма данных pandas в локальный файл</span><span class="sxs-lookup"><span data-stu-id="292ba-139">Write the pandas data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="292ba-140">Передача локального файла в BLOB-объект Azure</span><span class="sxs-lookup"><span data-stu-id="292ba-140">Upload local file to Azure blob</span></span>
   
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
3. <span data-ttu-id="292ba-141">Считывание данных из большого двоичного объекта Azure с помощью модуля [Импорт данных][import-data] Машинного обучения Azure, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="292ba-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the screen grab below:</span></span>

![большой двоичный объект считывателя][2]

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="292ba-143">Пример применения процесса обработки и анализа данных группы на практике</span><span class="sxs-lookup"><span data-stu-id="292ba-143">The Team Data Science Process in Action example</span></span>
<span data-ttu-id="292ba-144">Полноценный пошаговый пример применения процесса обработки и анализа данных группы с использованием общедоступного набора данных см. в статье [Процесс обработки и анализа данных группы на практике: использование SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="292ba-144">For an end-to-end walkthrough example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
