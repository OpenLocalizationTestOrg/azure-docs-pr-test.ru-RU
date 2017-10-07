---
title: "функции aaaCreate для Azure BLOB-объектов хранилища данных, с помощью Panda | Документы Microsoft"
description: "Как toocreate функции для данных, хранящихся в контейнере BLOB-объектов Azure с пакетом Panda Python hello."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Создание характеристик для данных хранилища больших двоичных объектов Azure с помощью Panda
В этом документе показано, как toocreate функции для данных, хранящихся в контейнере BLOB-объектов Azure, с помощью hello [Pandas](http://pandas.pydata.org/) пакета Python. После структуризации как tooload hello в кадр данных Panda, он отображается как toogenerate категориальных признаков с помощью сценариев Python значения индикатора и группирование компонентов.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Это **меню** связывает tootopics, описано, как toocreate функции для данных в различных средах. Эта задача является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже создали учетную запись хранилища BLOB-объектов Azure и сохранили в ней свои данные. Получить инструкции tooset учетную запись [создать учетную запись хранилища Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Загрузка данных hello Pandas кадра данных.
В порядке toodo просматривать и управлять набора данных, его необходимо загрузить из hello BLOB-объект источника tooa локального файла, которое можно загрузить в кадре данных Pandas. Ниже приведены hello toofollow действия для выполнения данной процедуры.

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

## <a name="blob-featuregen"></a>Создание функций
Hello следующих двух разделах показано, как toogenerate категориальных признаков с значения индикатора и сегментирования функции с помощью сценариев Python.

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
3. Теперь hello данные могут считываться из hello BLOB-объекта с помощью hello машинного обучения Azure [импорта данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) модуля, как показано на экране приветствия ниже:

![большой двоичный объект считывателя](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

