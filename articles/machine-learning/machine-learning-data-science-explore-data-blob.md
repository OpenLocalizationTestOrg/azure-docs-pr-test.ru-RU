---
title: "Просмотр данных в хранилище BLOB-объектов Azure с помощью Pandas | Документация Майкрософт"
description: "Описание просмотра данных, которые хранятся в контейнере больших двоичных объектов Azure, с помощью Pandas."
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
ms.openlocfilehash: e1b33b17270122a38228484a56c8324c5b4505a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="3e088-103">Просмотр данных в хранилище больших двоичных объектов Azure с помощью Pandas</span><span class="sxs-lookup"><span data-stu-id="3e088-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="3e088-104">В этом документе описывается просмотр данных, которые хранятся в контейнере больших двоичных объектов Azure, с помощью пакета Python [Pandas](http://pandas.pydata.org/) .</span><span class="sxs-lookup"><span data-stu-id="3e088-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="3e088-105">Следующее **меню** содержит ссылки на статьи, описывающие использование средств для просмотра данных из различных сред хранения.</span><span class="sxs-lookup"><span data-stu-id="3e088-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="3e088-106">Эта задача является одним из этапов [процесса обработки и анализа данных]().</span><span class="sxs-lookup"><span data-stu-id="3e088-106">This task is a step in the [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="3e088-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3e088-107">Prerequisites</span></span>
<span data-ttu-id="3e088-108">В этой статье предполагается, что вы:</span><span class="sxs-lookup"><span data-stu-id="3e088-108">This article assumes that you have:</span></span>

* <span data-ttu-id="3e088-109">Создали учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="3e088-109">Created an Azure storage account.</span></span> <span data-ttu-id="3e088-110">Инструкции см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3e088-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="3e088-111">Сохранили данные в учетной записи хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="3e088-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="3e088-112">Инструкции можно найти в статье [Перемещение данных в службу хранилища Azure и обратно](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="3e088-112">If you need instructions, see [Moving data to and from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-the-data-into-a-pandas-dataframe"></a><span data-ttu-id="3e088-113">Загрузка данных в кадр данных Pandas</span><span class="sxs-lookup"><span data-stu-id="3e088-113">Load the data into a Pandas DataFrame</span></span>
<span data-ttu-id="3e088-114">Для просмотра набора данных и управления им набор необходимо сначала скачать из источника больших двоичных объектов в локальный файл, который в последствии можно загрузить в кадр данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="3e088-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="3e088-115">Ниже приведен порядок выполнения данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="3e088-115">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="3e088-116">Скачайте данные из большого двоичного объекта Azure с помощью службы BLOB-объектов. Для этого воспользуйтесь приведенным ниже примером кода Python.</span><span class="sxs-lookup"><span data-stu-id="3e088-116">Download the data from Azure blob with the following Python code sample using blob service.</span></span> <span data-ttu-id="3e088-117">Замените переменные в этом коде своими значениями.</span><span class="sxs-lookup"><span data-stu-id="3e088-117">Replace the variable in the following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="3e088-118">Прочитайте данные, которые содержит скачанный файл, в блоке данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="3e088-118">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="3e088-119">Теперь вы готовы просматривать эти данные и создавать функции на основе этого набора данных.</span><span class="sxs-lookup"><span data-stu-id="3e088-119">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="3e088-120"><a name="blob-dataexploration"></a>Примеры просмотра данных с помощью Pandas</span><span class="sxs-lookup"><span data-stu-id="3e088-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="3e088-121">Вот несколько примеров того, как можно просматривать данные с помощью Pandas:</span><span class="sxs-lookup"><span data-stu-id="3e088-121">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="3e088-122">Проверьте **количество строк и столбцов**</span><span class="sxs-lookup"><span data-stu-id="3e088-122">Inspect the **number of rows and columns**</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="3e088-123">**Проверьте** первые или последние несколько **строк** в следующем наборе данных:</span><span class="sxs-lookup"><span data-stu-id="3e088-123">**Inspect** the first or last few **rows** in the following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="3e088-124">Проверьте **тип данных** , импортированный в каждый столбец, с помощью приведенного ниже примера кода.</span><span class="sxs-lookup"><span data-stu-id="3e088-124">Check the **data type** each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="3e088-125">Проверьте **основную статистику** , относящуюся к столбцам набора данных, так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3e088-125">Check the **basic stats** for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="3e088-126">Проверьте количество записей в каждом столбце так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3e088-126">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="3e088-127">**Проверьте соотношение числа отсутствующих значений** к фактическому количеству записей в каждом столбце. Воспользуйтесь приведенным ниже примером кода.</span><span class="sxs-lookup"><span data-stu-id="3e088-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="3e088-128">Если в том или ином столбце данных **отсутствуют значения** , вы можете заменить их так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3e088-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="3e088-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="3e088-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="3e088-130">Другой способ заменить отсутствующие значения — воспользоваться функцией режима.</span><span class="sxs-lookup"><span data-stu-id="3e088-130">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="3e088-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<имя_столбца>':dataframe_blobdata['<имя_столбца>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="3e088-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="3e088-132">Создайте **гистограмму** , используя переменное количество ячеек, чтобы построить распределение переменной.</span><span class="sxs-lookup"><span data-stu-id="3e088-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="3e088-133">Проверьте **корреляции** между переменными, используя диаграмму рассеяния или встроенную функцию корреляции.</span><span class="sxs-lookup"><span data-stu-id="3e088-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

