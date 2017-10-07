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
# <span data-ttu-id="8f22b-103"><a name="heading"></a>Выборка данных в хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="8f22b-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="8f22b-104">Этот документ описывает выборку данных, содержащихся в хранилище BLOB-объектов Azure, путем их программной загрузки и последующей выборки с использованием процедур на языке Python.</span><span class="sxs-lookup"><span data-stu-id="8f22b-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="8f22b-105">следующие Hello **меню** связывает tootopics, описывающие как toosample данные из различных средах хранилища.</span><span class="sxs-lookup"><span data-stu-id="8f22b-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="8f22b-106">**Для чего нужна выборка данных?**</span><span class="sxs-lookup"><span data-stu-id="8f22b-106">**Why sample your data?**</span></span>
<span data-ttu-id="8f22b-107">При планировании tooanalyze dataset hello имеет большой размер, это обычно tooreduce данных рекомендуется toodown образец hello его tooa размер меньший, но репрезентативный и управляемость.</span><span class="sxs-lookup"><span data-stu-id="8f22b-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="8f22b-108">Это способствует пониманию данных, их исследованию и проектированию характеристик.</span><span class="sxs-lookup"><span data-stu-id="8f22b-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="8f22b-109">Его роль в hello процесса Cortana Analytics — tooenable быстрого создания прототипов функций обработки данных hello и машинного обучения моделей.</span><span class="sxs-lookup"><span data-stu-id="8f22b-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="8f22b-110">Эта задача выборка является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="8f22b-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="8f22b-111">Скачать данные и уменьшить выборку данных</span><span class="sxs-lookup"><span data-stu-id="8f22b-111">Download and down-sample data</span></span>
1. <span data-ttu-id="8f22b-112">Загрузите hello данных из хранилища BLOB-объектов Azure, с помощью службы BLOB-объектов hello из следующий пример кода Python hello:</span><span class="sxs-lookup"><span data-stu-id="8f22b-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="8f22b-113">Чтение данных в Pandas-кадр данных из файла hello загруженного ранее.</span><span class="sxs-lookup"><span data-stu-id="8f22b-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="8f22b-114">Вниз образец hello данных с помощью hello `numpy` `random.choice` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8f22b-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="8f22b-115">Теперь можно работать с hello выше кадра данных с 1-процентной выборки hello для дальнейшего исследования и создания компонентов.</span><span class="sxs-lookup"><span data-stu-id="8f22b-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="8f22b-116"><a name="heading"></a>Передача данных и их считывание в службу машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="8f22b-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="8f22b-117">Можно использовать следующий образец кода toodown образец hello данных hello и использовать его непосредственно в машинном обучении Azure:</span><span class="sxs-lookup"><span data-stu-id="8f22b-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="8f22b-118">Запись локального файла кадра данных tooa hello</span><span class="sxs-lookup"><span data-stu-id="8f22b-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="8f22b-119">Отправка tooan локальный файл hello Azure BLOB-объекта с помощью hello следующий образец кода:</span><span class="sxs-lookup"><span data-stu-id="8f22b-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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

3. <span data-ttu-id="8f22b-120">Чтение данных hello из BLOB-объектов Azure с помощью машинного обучения Azure hello [импорта данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) как показано в приведенном ниже рисунке hello:</span><span class="sxs-lookup"><span data-stu-id="8f22b-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![большой двоичный объект считывателя](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

