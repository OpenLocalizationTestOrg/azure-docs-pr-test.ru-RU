---
title: "aaaProcess Azure данные большого двоичного объекта с углубленной аналитики | Документы Microsoft"
description: "Обработка данных в хранилище больших двоичных объектов Azure."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Обработка больших двоичных данных Azure с применением методов расширенного анализа
Этот документ содержит сведения о работе с данными в хранилище больших двоичных объектов Azure и создании характеристик на их основе. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Загрузка данных hello Pandas кадра данных.
В порядке tooexplore и управлять набора данных, его необходимо загрузить из hello BLOB-объект источника tooa локального файла, которое можно загрузить в кадре данных Pandas. Ниже приведены hello toofollow действия для выполнения данной процедуры.

1. Скачать hello данные из Azure BLOB-объекта с hello, следующий пример кода Python, с помощью службы BLOB-объектов. Замените переменную hello в коде hello ниже особые значения: 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. Чтение данных hello в Pandas-кадр данных из hello загрузили файл.
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Теперь вы готовы tooexplore hello данные и создавать признаки на этот набор данных.

## <a name="blob-dataexploration"></a>Просмотр данных
Ниже приведены некоторые примеры способов tooexplore данных с помощью Pandas.

1. Проверить количество строк и столбцов hello 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Сначала просмотреть hello или в последний раз несколько строк в наборе данных hello, как показано ниже:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Проверьте hello тип данных каждого столбца были импортированы как с помощью hello следующий образец кода
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Как проверить основные Статистика hello hello столбцов в наборе данных hello
   
        dataframe_blobdata.describe()
5. Рассмотрим hello число записей для каждого значения в столбце
   
        dataframe_blobdata['<column_name>'].value_counts()
6. Число отсутствующих значений и hello фактическое число записей в каждом столбце, используя следующий пример кода hello
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Если в данных hello нет значения для конкретного столбца, можно удалить их следующим образом:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   Другой способ tooreplace отсутствующих значений является режим функции hello.
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. Создать гистограмму диаграмму с помощью переменное число ячеек tooplot hello распространения переменной    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Посмотрите на взаимосвязи между переменными с помощью scatterplot или hello корреляции встроенные функции
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>Создание функций
Создавать функции с помощью Python вы можете приведенным ниже способом.

### <a name="blob-countfeature"></a>Создание функций на основе значений индикатора
Вот как можно создавать категориальные функции:

1. Проверьте распределение hello hello категориальных столбцов:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Создание значения индикатора для каждого значения в столбце hello
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Присоединение hello столбец индикатора с hello исходного кадра данных. 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Удалите саму переменную исходного hello:
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Создание характеристик путем группирования данных
Вот как можно создавать функции группирования:

1. Добавить последовательность столбцов toobin числового столбца
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Преобразовать последовательность сегментирования tooa логические переменные
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Наконец соединения hello фиктивный переменные обратно toohello исходного кадра данных.
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <a name="sql-featuregen"></a>Записи данных обратно tooAzure больших двоичных объектов и использование в машинном обучении Azure
После изучена hello данных и создать необходимые функции hello, можно передать данные hello (выборки или признак) tooan Azure BLOB-объектов и использовать его в машинном обучении Azure с помощью hello следующие шаги: Обратите внимание, что дополнительные компоненты могут создаваться в hello Студия машинного обучения также. 

1. Запись файла toolocal кадра данных hello
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Отправьте BLOB-объектов tooAzure hello данных следующим образом:
   
        from azure.storage.blob import BlobService
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
3. Теперь hello данные могут считываться из hello BLOB-объекта с помощью hello машинного обучения Azure [импорта данных] [ import-data] модуля, как показано на экране приветствия ниже:

![большой двоичный объект считывателя][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

