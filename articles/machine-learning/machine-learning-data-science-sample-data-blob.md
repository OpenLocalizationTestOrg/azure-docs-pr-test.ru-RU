---
title: "Выборка данных в хранилище BLOB-объектов Azure | Документация Майкрософт"
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
ms.openlocfilehash: aa9ab454706429682a393c3d5758cebe20790e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="1d20c-103"><a name="heading"></a>Выборка данных в хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="1d20c-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="1d20c-104">Этот документ описывает выборку данных, содержащихся в хранилище BLOB-объектов Azure, путем их программной загрузки и последующей выборки с использованием процедур на языке Python.</span><span class="sxs-lookup"><span data-stu-id="1d20c-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="1d20c-105">**Меню** ниже содержит ссылки на разделы, в которых описана выборка данных из различных сред хранения.</span><span class="sxs-lookup"><span data-stu-id="1d20c-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="1d20c-106">**Для чего нужна выборка данных?**</span><span class="sxs-lookup"><span data-stu-id="1d20c-106">**Why sample your data?**</span></span>
<span data-ttu-id="1d20c-107">Если размер набора данных, который планируется проанализировать, слишком большой, обычно рекомендуется уменьшить выборку данных до размера, который останется репрезентативным и будет более управляемым.</span><span class="sxs-lookup"><span data-stu-id="1d20c-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="1d20c-108">Это способствует пониманию данных, их исследованию и проектированию характеристик.</span><span class="sxs-lookup"><span data-stu-id="1d20c-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="1d20c-109">Роль этой операции в процессе аналитики Кортаны заключается в том, чтобы сделать возможным быстрое прототипирование функций обработки данных и моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="1d20c-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="1d20c-110">Эта задача выборки является одним из этапов [процесса обработки и анализа данных группы (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="1d20c-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="1d20c-111">Скачать данные и уменьшить выборку данных</span><span class="sxs-lookup"><span data-stu-id="1d20c-111">Download and down-sample data</span></span>
1. <span data-ttu-id="1d20c-112">Загрузить данные из хранилища BLOB-объектов Azure с помощью службы BLOB-объектов и следующего образца кода на языке Python:</span><span class="sxs-lookup"><span data-stu-id="1d20c-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span></span> 
   
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
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))

2. <span data-ttu-id="1d20c-113">Считать данные во фрейм данных Pandas из файла, загруженного выше.</span><span class="sxs-lookup"><span data-stu-id="1d20c-113">Read data into a Pandas data-frame from the file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="1d20c-114">Уменьшить выборку данных с помощью `random.choice` `numpy`:</span><span class="sxs-lookup"><span data-stu-id="1d20c-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="1d20c-115">Теперь можно работать с указанным выше фреймом данных, содержащим 1-процентную выборку, для дальнейшего просмотра и создания характеристик.</span><span class="sxs-lookup"><span data-stu-id="1d20c-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="1d20c-116"><a name="heading"></a>Передача данных и их считывание в службу машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="1d20c-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="1d20c-117">С помощью следующего образца кода можно уменьшить выборку данных и использовать их непосредственно в Машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="1d20c-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="1d20c-118">Запись фрейма данных в локальный файл</span><span class="sxs-lookup"><span data-stu-id="1d20c-118">Write the data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="1d20c-119">Передача локального файла в BLOB-объект Azure с помощью следующего образца кода:</span><span class="sxs-lookup"><span data-stu-id="1d20c-119">Upload the local file to an Azure blob using the following sample code:</span></span>
   
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
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. <span data-ttu-id="1d20c-120">Считывание данных из большого двоичного объекта Azure с помощью модуля [Импорт данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) Машинного обучения Azure, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="1d20c-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span></span>

![большой двоичный объект считывателя](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

