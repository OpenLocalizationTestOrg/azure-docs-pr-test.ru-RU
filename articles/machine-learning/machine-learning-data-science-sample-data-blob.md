---
title: "хранилище больших двоичных объектов aaaSample данные в Azure | Документы Microsoft"
description: "Выборка данных в хранилище больших двоичных объектов Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Выборка данных в хранилище больших двоичных объектов Azure
Этот документ описывает выборку данных, содержащихся в хранилище BLOB-объектов Azure, путем их программной загрузки и последующей выборки с использованием процедур на языке Python.

следующие Hello **меню** связывает tootopics, описывающие как toosample данные из различных средах хранилища. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Для чего нужна выборка данных?**
При планировании tooanalyze dataset hello имеет большой размер, это обычно tooreduce данных рекомендуется toodown образец hello его tooa размер меньший, но репрезентативный и управляемость. Это способствует пониманию данных, их исследованию и проектированию характеристик. Его роль в hello процесса Cortana Analytics — tooenable быстрого создания прототипов функций обработки данных hello и машинного обучения моделей.

Эта задача выборка является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="download-and-down-sample-data"></a>Скачать данные и уменьшить выборку данных
1. Загрузите hello данных из хранилища BLOB-объектов Azure, с помощью службы BLOB-объектов hello из следующий пример кода Python hello: 
   
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

2. Чтение данных в Pandas-кадр данных из файла hello загруженного ранее.
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. Вниз образец hello данных с помощью hello `numpy` `random.choice` следующим образом:
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

Теперь можно работать с hello выше кадра данных с 1-процентной выборки hello для дальнейшего исследования и создания компонентов.

## <a name="heading"></a>Передача данных и их считывание в службу машинного обучения Azure
Можно использовать следующий образец кода toodown образец hello данных hello и использовать его непосредственно в машинном обучении Azure:

1. Запись локального файла кадра данных tooa hello
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. Отправка tooan локальный файл hello Azure BLOB-объекта с помощью hello следующий образец кода:
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. Чтение данных hello из BLOB-объектов Azure с помощью машинного обучения Azure hello [импорта данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) как показано в приведенном ниже рисунке hello:

![большой двоичный объект считывателя](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

