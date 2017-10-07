---
title: "aaaExplore данные в Azure хранилище больших двоичных объектов с Pandas | Документы Microsoft"
description: "Как tooexplore данных, хранящихся в Azure BLOB-объектов с помощью Pandas контейнера."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Просмотр данных в хранилище больших двоичных объектов Azure с помощью Pandas
В этом документе рассматриваются как tooexplore данных, хранящихся в Azure BLOB-объектов контейнера с помощью [Pandas](http://pandas.pydata.org/) пакета Python.

следующие Hello **меню** связывает tootopics, описывающих, как toouse средств tooexplore данные из различных средах хранилища. Эта задача является этапом hello [процесса обработки и анализа данных]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы:

* Создали учетную запись хранения Azure. Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Сохранили данные в учетной записи хранилища больших двоичных объектов Azure. При необходимости инструкции в разделе [tooand перемещение данных из хранилища Azure](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Загрузка данных hello в кадр данных под Pandas
tooexplore и управлять набора данных, его необходимо сначала загрузить из hello BLOB-объект источника tooa локального файла, который можно загрузить в кадр данных под Pandas. Ниже приведены hello toofollow действия для выполнения данной процедуры.

1. Скачать hello данные из Azure BLOB-объекта с hello следующий образец кода Python, с помощью службы BLOB-объектов. Замените переменной hello в hello после кода особые значения: 
   
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

## <a name="blob-dataexploration"></a>Примеры просмотра данных с помощью Pandas
Ниже приведены некоторые примеры способов tooexplore данных с помощью Pandas.

1. Проверять hello **номеров строк и столбцов** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **Проверить** hello первой или последней несколько **строки** в hello после набора данных:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Проверьте hello **тип данных** каждый столбец был импортирован с помощью hello следующий образец кода
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Проверьте hello **основные stats** для столбцов hello в hello набора данных следующим образом
   
        dataframe_blobdata.describe()
5. Рассмотрим hello число записей для каждого значения в столбце
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Число отсутствующих значений** и hello фактическое число записей в каждом столбце, используя следующий пример кода hello
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Если у вас есть **недостающие значения** для определенного столбца данных hello, можно удалить их следующим образом:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   Другой способ tooreplace отсутствующих значений является режим функции hello.
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. Создание **гистограммы** построения с помощью переменное число ячеек tooplot hello распространения переменной    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Посмотрите на **корреляции** между переменными с помощью scatterplot или hello корреляции встроенные функции
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

