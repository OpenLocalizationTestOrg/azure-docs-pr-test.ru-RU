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
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="5a9ce-103">Просмотр данных в хранилище больших двоичных объектов Azure с помощью Pandas</span><span class="sxs-lookup"><span data-stu-id="5a9ce-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="5a9ce-104">В этом документе рассматриваются как tooexplore данных, хранящихся в Azure BLOB-объектов контейнера с помощью [Pandas](http://pandas.pydata.org/) пакета Python.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="5a9ce-105">следующие Hello **меню** связывает tootopics, описывающих, как toouse средств tooexplore данные из различных средах хранилища.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="5a9ce-106">Эта задача является этапом hello [процесса обработки и анализа данных]().</span><span class="sxs-lookup"><span data-stu-id="5a9ce-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="5a9ce-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5a9ce-107">Prerequisites</span></span>
<span data-ttu-id="5a9ce-108">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="5a9ce-108">This article assumes that you have:</span></span>

* <span data-ttu-id="5a9ce-109">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-109">Created an Azure storage account.</span></span> <span data-ttu-id="5a9ce-110">Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5a9ce-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="5a9ce-111">Сохранили данные в учетной записи хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="5a9ce-112">При необходимости инструкции в разделе [tooand перемещение данных из хранилища Azure](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="5a9ce-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="5a9ce-113">Загрузка данных hello в кадр данных под Pandas</span><span class="sxs-lookup"><span data-stu-id="5a9ce-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="5a9ce-114">tooexplore и управлять набора данных, его необходимо сначала загрузить из hello BLOB-объект источника tooa локального файла, который можно загрузить в кадр данных под Pandas.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="5a9ce-115">Ниже приведены hello toofollow действия для выполнения данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="5a9ce-116">Скачать hello данные из Azure BLOB-объекта с hello следующий образец кода Python, с помощью службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="5a9ce-117">Замените переменной hello в hello после кода особые значения:</span><span class="sxs-lookup"><span data-stu-id="5a9ce-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="5a9ce-118">Чтение данных hello в Pandas-кадр данных из hello загрузили файл.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="5a9ce-119">Теперь вы готовы tooexplore hello данные и создавать признаки на этот набор данных.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="5a9ce-120"><a name="blob-dataexploration"></a>Примеры просмотра данных с помощью Pandas</span><span class="sxs-lookup"><span data-stu-id="5a9ce-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="5a9ce-121">Ниже приведены некоторые примеры способов tooexplore данных с помощью Pandas.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="5a9ce-122">Проверять hello **номеров строк и столбцов**</span><span class="sxs-lookup"><span data-stu-id="5a9ce-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="5a9ce-123">**Проверить** hello первой или последней несколько **строки** в hello после набора данных:</span><span class="sxs-lookup"><span data-stu-id="5a9ce-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="5a9ce-124">Проверьте hello **тип данных** каждый столбец был импортирован с помощью hello следующий образец кода</span><span class="sxs-lookup"><span data-stu-id="5a9ce-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="5a9ce-125">Проверьте hello **основные stats** для столбцов hello в hello набора данных следующим образом</span><span class="sxs-lookup"><span data-stu-id="5a9ce-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="5a9ce-126">Рассмотрим hello число записей для каждого значения в столбце</span><span class="sxs-lookup"><span data-stu-id="5a9ce-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="5a9ce-127">**Число отсутствующих значений** и hello фактическое число записей в каждом столбце, используя следующий пример кода hello</span><span class="sxs-lookup"><span data-stu-id="5a9ce-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="5a9ce-128">Если у вас есть **недостающие значения** для определенного столбца данных hello, можно удалить их следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5a9ce-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="5a9ce-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="5a9ce-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="5a9ce-130">Другой способ tooreplace отсутствующих значений является режим функции hello.</span><span class="sxs-lookup"><span data-stu-id="5a9ce-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="5a9ce-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="5a9ce-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="5a9ce-132">Создание **гистограммы** построения с помощью переменное число ячеек tooplot hello распространения переменной</span><span class="sxs-lookup"><span data-stu-id="5a9ce-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="5a9ce-133">Посмотрите на **корреляции** между переменными с помощью scatterplot или hello корреляции встроенные функции</span><span class="sxs-lookup"><span data-stu-id="5a9ce-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

