---
title: "aaaExplore данных в SQL Server виртуальной машины в Azure | Документы Microsoft"
description: "Как tooexplore данные, хранящиеся в виртуальной Машине SQL Server в Azure."
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
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="61a0d-103">Просмотр данных в виртуальной машине SQL Server на платформе Azure</span><span class="sxs-lookup"><span data-stu-id="61a0d-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="61a0d-104">В этом документе рассматриваются как tooexplore данные, хранящиеся в виртуальной Машине SQL Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="61a0d-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="61a0d-105">Это можно сделать путем структурирования данных с помощью SQL или с использованием языка программирования, например Python.</span><span class="sxs-lookup"><span data-stu-id="61a0d-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="61a0d-106">следующие Hello **меню** связывает tootopics, описывающих, как toouse средств tooexplore данные из различных средах хранилища.</span><span class="sxs-lookup"><span data-stu-id="61a0d-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="61a0d-107">Эта задача является этапом hello процесса Cortana аналитика (CAP).</span><span class="sxs-lookup"><span data-stu-id="61a0d-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="61a0d-108">Hello пример инструкции SQL в этом документе предполагается, что данные находятся в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="61a0d-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="61a0d-109">В противном случае обратитесь toohello облачных данных обработки и анализа процесса карты toolearn как toomove вашей tooSQL данные сервера.</span><span class="sxs-lookup"><span data-stu-id="61a0d-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="61a0d-110"><a name="sql-dataexploration"></a>Просмотр данных SQL с помощью сценариев SQL</span><span class="sxs-lookup"><span data-stu-id="61a0d-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="61a0d-111">Вот несколько примеры сценариев SQL, которые можно использовать tooexplore хранилищ данных в SQL Server.</span><span class="sxs-lookup"><span data-stu-id="61a0d-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="61a0d-112">Получение числа hello наблюдения за день</span><span class="sxs-lookup"><span data-stu-id="61a0d-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="61a0d-113">Получить уровней hello в категориальный столбец</span><span class="sxs-lookup"><span data-stu-id="61a0d-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="61a0d-114">Получить hello количество уровней в сочетании с двумя категориальные столбцы</span><span class="sxs-lookup"><span data-stu-id="61a0d-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="61a0d-115">Получить hello распространения для числовых столбцов.</span><span class="sxs-lookup"><span data-stu-id="61a0d-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="61a0d-116">Практический пример, можно использовать hello [dataset такси NYC](http://www.andresmh.com/nyctaxitrips/) и toohello IPNB под названием [wrangling NYC данных с помощью ноутбук IPython и SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) руководство с начала до конца.</span><span class="sxs-lookup"><span data-stu-id="61a0d-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="61a0d-117"><a name="python"></a>Просмотр данных SQL с помощью Python</span><span class="sxs-lookup"><span data-stu-id="61a0d-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="61a0d-118">С помощью Python tooexplore данных и создавать функции при hello данные хранятся в SQL Server схожие данные tooprocessing в BLOB-объектов Azure с помощью Python, как описано в документе [данные больших двоичных объектов Azure процесс в среде обработки и анализа данных](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="61a0d-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="61a0d-119">Hello данных должен toobe загружаются из базы данных hello в pandas кадр данных и затем может быть дальнейшую обработку.</span><span class="sxs-lookup"><span data-stu-id="61a0d-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="61a0d-120">Мы документа hello процесс соединения toohello базы данных и загрузку данных hello в hello кадр данных в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="61a0d-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="61a0d-121">Hello следующий формат строки соединения может быть база данных SQL Server используется tooconnect tooa из Python, с помощью pyodbc (заменить имя сервера, dbname, имя пользователя и пароль особые значения):</span><span class="sxs-lookup"><span data-stu-id="61a0d-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="61a0d-122">Hello [Pandas библиотеки](http://pandas.pydata.org/) в Python предоставляет широкий набор средств анализа данных и структур данных для работы с данными для программирования Python.</span><span class="sxs-lookup"><span data-stu-id="61a0d-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="61a0d-123">Hello следующий код считывает hello результаты, возвращенные из базы данных SQL Server, в кадр данных Pandas:</span><span class="sxs-lookup"><span data-stu-id="61a0d-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="61a0d-124">Теперь можно работать с hello Pandas кадр данных, как описано в разделе hello [данные больших двоичных объектов Azure процесс в среде обработки и анализа данных](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="61a0d-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="61a0d-125">Практический пример применения процесса аналитики Кортаны</span><span class="sxs-lookup"><span data-stu-id="61a0d-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="61a0d-126">Пошаговое руководство с начала до конца пример hello Cortana Analytics процесс, используя открытый набор данных, в разделе [hello командного процесса обработки и анализа данных в действие: с помощью SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="61a0d-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

