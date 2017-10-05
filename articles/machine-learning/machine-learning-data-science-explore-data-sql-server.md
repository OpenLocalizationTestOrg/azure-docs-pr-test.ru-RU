---
title: "Просмотр данных в виртуальной машине SQL Server на платформе Azure | Документация Майкрософт"
description: "Описание того, как просматривать данные, хранящиеся в виртуальной машине SQL Server на платформе Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: a2be21ef15b9209db1e97150e0297558fa69a7be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="1fe09-103">Просмотр данных в виртуальной машине SQL Server на платформе Azure</span><span class="sxs-lookup"><span data-stu-id="1fe09-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="1fe09-104">В этом документе описано, как просматривать данные, хранящиеся в виртуальной машине SQL Server на платформе Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe09-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="1fe09-105">Это можно сделать путем структурирования данных с помощью SQL или с использованием языка программирования, например Python.</span><span class="sxs-lookup"><span data-stu-id="1fe09-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="1fe09-106">Следующее **меню** содержит ссылки на статьи, описывающие использование средств для просмотра данных из различных сред хранения.</span><span class="sxs-lookup"><span data-stu-id="1fe09-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="1fe09-107">Эта задача является одним из этапов процесса аналитики Кортаны (CAP).</span><span class="sxs-lookup"><span data-stu-id="1fe09-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="1fe09-108">В образцах инструкций SQL, содержащихся в данном документе, предполагается, что данные находятся на сервере SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1fe09-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="1fe09-109">Если это не так, обратитесь к карте обработки облачных данных, чтобы узнать, как переместить данные в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1fe09-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="1fe09-110"><a name="sql-dataexploration"></a>Просмотр данных SQL с помощью сценариев SQL</span><span class="sxs-lookup"><span data-stu-id="1fe09-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="1fe09-111">Вот несколько примеров сценариев SQL, которые можно использовать для изучения хранилищ данных в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1fe09-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="1fe09-112">Получение количества наблюдений за день</span><span class="sxs-lookup"><span data-stu-id="1fe09-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="1fe09-113">Получение уровней в столбце категорий</span><span class="sxs-lookup"><span data-stu-id="1fe09-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="1fe09-114">Получение числа уровней в сочетании двух столбцов категорий</span><span class="sxs-lookup"><span data-stu-id="1fe09-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="1fe09-115">Получение распределения для числовых столбцов </span><span class="sxs-lookup"><span data-stu-id="1fe09-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="1fe09-116">Для практического примера можно использовать [набор данных о такси Нью-Йорка](http://www.andresmh.com/nyctaxitrips/) и статью IPNB под названием [Структурирование данных Нью-Йорка с помощью IPython Notebook и SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb), содержащую полное пошаговое руководство.</span><span class="sxs-lookup"><span data-stu-id="1fe09-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="1fe09-117"><a name="python"></a>Просмотр данных SQL с помощью Python</span><span class="sxs-lookup"><span data-stu-id="1fe09-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="1fe09-118">Использование языка Python для просмотра данных и создания характеристик, когда данные находятся в SQL Server, подобно обработке данных в большом двоичном объекте Azure с использованием Python, как описано в статье [Обработка больших двоичных данных Azure с применением методов расширенного анализа](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="1fe09-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="1fe09-119">Данные необходимо загрузить из базы данных в кадр данных Pandas для последующей обработки.</span><span class="sxs-lookup"><span data-stu-id="1fe09-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="1fe09-120">В этом разделе задокументирован процесс подключения к базе данных и загрузки данных в кадр данных.</span><span class="sxs-lookup"><span data-stu-id="1fe09-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="1fe09-121">Для подключения к базе данных SQL Server из языка Python с использованием pyodbc можно применить следующий формат строки подключения (замените servername, dbname, username и password соответствующими значениями имени сервера, имени БД, имени пользователя и пароля):</span><span class="sxs-lookup"><span data-stu-id="1fe09-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="1fe09-122">[Библиотека Pandas](http://pandas.pydata.org/) в языке Python предлагает большой выбор структур данных и средств анализа данных для манипуляций со значениями с помощью языке Python.</span><span class="sxs-lookup"><span data-stu-id="1fe09-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="1fe09-123">Следующий код считывает результаты, возвращенные из базы данных SQL Server, в кадр данных Pandas:</span><span class="sxs-lookup"><span data-stu-id="1fe09-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="1fe09-124">Теперь можно работать с кадром данных Pandas, как описано в статье [Обработка больших двоичных данных Azure с применением методов расширенного анализа](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="1fe09-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="1fe09-125">Практический пример применения процесса аналитики Кортаны</span><span class="sxs-lookup"><span data-stu-id="1fe09-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="1fe09-126">Полноценный пошаговый пример применения процесса Cortana Analytics с использованием общедоступного набора данных см. в статье [Процесс обработки и анализа данных группы на практике: использование SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="1fe09-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

