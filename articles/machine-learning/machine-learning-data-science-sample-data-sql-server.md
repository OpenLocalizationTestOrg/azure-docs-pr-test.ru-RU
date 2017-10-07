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
# <a name="heading"></a>Выборка данных на сервере SQL Server в Azure
В этом документе показано, как сохранить toosample данных в SQL Server в Azure с помощью SQL или языка программирования Python hello. Здесь также показано, как toomove выборке данных в машинном обучении Azure путем его сохранения файла tooa, поместив его tooan BLOB-объектов Azure и их считывания в студию машинного обучения Azure.

Выборка Python Hello использует hello [pyodbc](https://code.google.com/p/pyodbc/) tooSQL tooconnect ODBC библиотеки Server в Azure и hello [Pandas](http://pandas.pydata.org/) библиотеки toodo hello выборки.

> [!NOTE]
> Hello пример кода SQL в этом документе предполагается, что hello данных находится в SQL Server в Azure. Если это не так, можно найти слишком[перемещение данных tooSQL Server в Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) инструкции о том, как toomove вашей tooSQL данных сервера в Azure.
> 
> 

следующие Hello **меню** связывает tootopics, описывающие как toosample данные из различных средах хранилища. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Для чего нужна выборка данных?**
При планировании tooanalyze dataset hello имеет большой размер, это обычно tooreduce данных рекомендуется toodown образец hello его tooa размер меньший, но репрезентативный и управляемость. Это способствует пониманию данных, их исследованию и проектированию характеристик. Ее роль в hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) — tooenable быстрого создания прототипов функций обработки данных hello и машинного обучения моделей.

Эта задача выборка является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>Использование SQL
В этом разделе описываются способы, с помощью SQL tooperform простую случайную выборку данных hello базы данных hello. Выберите нужный метод в зависимости от размера ваших данных и их распределения.

Hello две следующие пункты показывают, как toouse newid в SQL Server tooperform hello выборки. Hello выбранного метода в зависимости от способа случайных toobe образец hello (pk_id в следующем образце кода hello предполагается toobe автоматического создания первичного ключа).

1. Менее строгая случайная выборка
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Более случайная выборка 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

Для выборки можно также использовать предложение TABLESAMPLE, как показано ниже. Это может быть лучшим вариантом, если размер данных велик (предполагается, что данные на разных страницах не сопоставляются) и toocomplete hello запроса слишком много времени.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> Можно просматривать данные этой выборки и создавать характеристики, сохранив ее в новой таблице
> 
> 

### <a name="sql-aml"></a>Подключение tooAzure машинного обучения
Вы можете напрямую использовать примеры запросов hello выше hello машинного обучения Azure [импорта данных] [ import-data] данные toodown образец hello модуля на hello полет и переведите его в эксперимент машинного обучения Azure. Ниже приведен снимок экрана с помощью hello чтения модуля tooread hello выборки данных:

![считыватель sql][1]

## <a name="python"></a>С помощью языка программирования Python hello
В этом разделе демонстрируется использование hello [pyodbc библиотеки](https://code.google.com/p/pyodbc/) tooestablish ODBC подключения tooa базы данных SQL server в Python. строку подключения базы данных Hello таков: (Замените servername, dbname, имя пользователя и пароль конфигурацию):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [Pandas](http://pandas.pydata.org/) библиотеки в Python предоставляет широкий набор средств анализа данных и структур данных для работы с данными для программирования Python. Приведенный ниже код Hello считывает 0,1% образец hello данных из таблицы в базе данных Azure SQL в данных Pandas:

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

Теперь можно работать с данными выборки hello в кадре данных Pandas hello. 

### <a name="python-aml"></a>Подключение tooAzure машинного обучения
Можно использовать следующие образец кода toosave hello данных уменьшается tooa файл hello и отправьте его tooan BLOB-объектов Azure. Hello данные в большом двоичном объекте hello непосредственно считываются в эксперимента обучения машины Azure с помощью hello [импорта данных] [ import-data] модуля. Ниже приведены шаги Hello. 

1. Запись hello pandas данных кадра tooa локального файла
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Отправка больших двоичных объектов tooAzure локального файла
   
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
3. Чтение данных из больших двоичных объектов Azure с помощью машинного обучения Azure [импорта данных] [ import-data] модуля, как показано ниже захвата экрана приветствия:

![большой двоичный объект считывателя][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Hello командного процесса обработки и анализа данных в примере действие
Пример Пошаговое руководство с начала до конца hello командного процесса обработки и анализа данных с помощью набора общих см [командного процесса обработки и анализа данных в действии: с помощью SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
