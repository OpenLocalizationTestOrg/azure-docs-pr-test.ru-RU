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
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>Просмотр данных в виртуальной машине SQL Server на платформе Azure
В этом документе рассматриваются как tooexplore данные, хранящиеся в виртуальной Машине SQL Server в Azure. Это можно сделать путем структурирования данных с помощью SQL или с использованием языка программирования, например Python.

следующие Hello **меню** связывает tootopics, описывающих, как toouse средств tooexplore данные из различных средах хранилища. Эта задача является этапом hello процесса Cortana аналитика (CAP).

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> Hello пример инструкции SQL в этом документе предполагается, что данные находятся в SQL Server. В противном случае обратитесь toohello облачных данных обработки и анализа процесса карты toolearn как toomove вашей tooSQL данные сервера.
> 
> 

## <a name="sql-dataexploration"></a>Просмотр данных SQL с помощью сценариев SQL
Вот несколько примеры сценариев SQL, которые можно использовать tooexplore хранилищ данных в SQL Server.

1. Получение числа hello наблюдения за день
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Получить уровней hello в категориальный столбец
   
    `select  distinct <column_name> from <databasename>`
3. Получить hello количество уровней в сочетании с двумя категориальные столбцы 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Получить hello распространения для числовых столбцов.
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> Практический пример, можно использовать hello [dataset такси NYC](http://www.andresmh.com/nyctaxitrips/) и toohello IPNB под названием [wrangling NYC данных с помощью ноутбук IPython и SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) руководство с начала до конца.
> 
> 

## <a name="python"></a>Просмотр данных SQL с помощью Python
С помощью Python tooexplore данных и создавать функции при hello данные хранятся в SQL Server схожие данные tooprocessing в BLOB-объектов Azure с помощью Python, как описано в документе [данные больших двоичных объектов Azure процесс в среде обработки и анализа данных](machine-learning-data-science-process-data-blob.md). Hello данных должен toobe загружаются из базы данных hello в pandas кадр данных и затем может быть дальнейшую обработку. Мы документа hello процесс соединения toohello базы данных и загрузку данных hello в hello кадр данных в этом разделе.

Hello следующий формат строки соединения может быть база данных SQL Server используется tooconnect tooa из Python, с помощью pyodbc (заменить имя сервера, dbname, имя пользователя и пароль особые значения):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [Pandas библиотеки](http://pandas.pydata.org/) в Python предоставляет широкий набор средств анализа данных и структур данных для работы с данными для программирования Python. Hello следующий код считывает hello результаты, возвращенные из базы данных SQL Server, в кадр данных Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Теперь можно работать с hello Pandas кадр данных, как описано в разделе hello [данные больших двоичных объектов Azure процесс в среде обработки и анализа данных](machine-learning-data-science-process-data-blob.md).

## <a name="cortana-analytics-process-in-action-example"></a>Практический пример применения процесса аналитики Кортаны
Пошаговое руководство с начала до конца пример hello Cortana Analytics процесс, используя открытый набор данных, в разделе [hello командного процесса обработки и анализа данных в действие: с помощью SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

