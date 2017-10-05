---
title: "Создание признаков для данных хранилища BLOB-объектов Azure с помощью Panda | Документация Майкрософт"
description: "Описание создания характеристик для данных, которые хранятся в контейнере больших двоичных объектов Azure, с помощью пакета Python Pandas."
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
ms.openlocfilehash: 2ef2acfea2372ac7fd52d099a2b4203ee2242d81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="d279d-103">Создание характеристик для данных хранилища больших двоичных объектов Azure с помощью Panda</span><span class="sxs-lookup"><span data-stu-id="d279d-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="d279d-104">В этом документе демонстрируется создание характеристик для данных, которые хранятся в контейнере больших двоичных объектов Azure, с помощью пакета Python [Pandas](http://pandas.pydata.org/) .</span><span class="sxs-lookup"><span data-stu-id="d279d-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="d279d-105">После описания загрузки данных в кадр данных Panda в нем показано создание категориальных характеристик с использованием сценариев Pyrhon со значениями индикатора и характеристиками группирования.</span><span class="sxs-lookup"><span data-stu-id="d279d-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="d279d-106">Это **меню** содержит ссылки на статьи, описывающие создание характеристик для данных в различных средах.</span><span class="sxs-lookup"><span data-stu-id="d279d-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="d279d-107">Эта задача является одним из этапов [процесса обработки и анализа данных группы (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="d279d-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d279d-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d279d-108">Prerequisites</span></span>
<span data-ttu-id="d279d-109">В этой статье предполагается, что вы уже создали учетную запись хранилища BLOB-объектов Azure и сохранили в ней свои данные.</span><span class="sxs-lookup"><span data-stu-id="d279d-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="d279d-110">Инструкции по настройке учетной записи в Azure см. в разделе [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d279d-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="d279d-111">Загрузка данных во фрейм данных Pandas</span><span class="sxs-lookup"><span data-stu-id="d279d-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="d279d-112">Для просмотра набора данных и управления им набор необходимо скачать из источника больших двоичных объектов в локальный файл, который в последствии можно загрузить во фрейм данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="d279d-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="d279d-113">Ниже приведен порядок выполнения данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="d279d-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="d279d-114">Скачайте данные из большого двоичного объекта Azure с помощью службы BLOB-объектов. Для этого воспользуйтесь приведенным ниже примером кода Python.</span><span class="sxs-lookup"><span data-stu-id="d279d-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="d279d-115">Замените переменные этого кода своими значениями.</span><span class="sxs-lookup"><span data-stu-id="d279d-115">Replace the variable in the code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="d279d-116">Прочитайте данные, которые содержит скачанный файл, в блоке данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="d279d-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="d279d-117">Теперь вы готовы просматривать эти данные и создавать функции на основе этого набора данных.</span><span class="sxs-lookup"><span data-stu-id="d279d-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="d279d-118"><a name="blob-featuregen"></a>Создание функций</span><span class="sxs-lookup"><span data-stu-id="d279d-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="d279d-119">В двух следующих разделах показано, как создать категориальные характеристики со значениями индикатора и характеристики группирования с помощью сценариев Python.</span><span class="sxs-lookup"><span data-stu-id="d279d-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="d279d-120"><a name="blob-countfeature"></a>Создание функций на основе значений индикатора</span><span class="sxs-lookup"><span data-stu-id="d279d-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="d279d-121">Вот как можно создавать категориальные функции:</span><span class="sxs-lookup"><span data-stu-id="d279d-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="d279d-122">Проверьте распределение категориального столбца.</span><span class="sxs-lookup"><span data-stu-id="d279d-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="d279d-123">Создайте значения индикатора для каждого значения столбца.</span><span class="sxs-lookup"><span data-stu-id="d279d-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="d279d-124">Объедините столбец индикатора с исходным блоком данных.</span><span class="sxs-lookup"><span data-stu-id="d279d-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="d279d-125">Удалите исходную переменную.</span><span class="sxs-lookup"><span data-stu-id="d279d-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="d279d-126"><a name="blob-binningfeature"></a>Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="d279d-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="d279d-127">Вот как можно создавать функции группирования:</span><span class="sxs-lookup"><span data-stu-id="d279d-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="d279d-128">Добавьте последовательность столбцов, чтобы создать числовой столбец.</span><span class="sxs-lookup"><span data-stu-id="d279d-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="d279d-129">Преобразуйте группирование в последовательность логических переменных.</span><span class="sxs-lookup"><span data-stu-id="d279d-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="d279d-130">Наконец, объедините фиктивные переменные с исходным блоком данных.</span><span class="sxs-lookup"><span data-stu-id="d279d-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="d279d-131"><a name="sql-featuregen"></a>Запись данных обратно в большой двоичный объект Azure и их использование в Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="d279d-131"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="d279d-132">После просмотра данных и создания необходимых вам признаков вы можете отправить данные (в выборке или в признаке) в большой двоичный объект Azure и использовать их в Студии машинного обучения Azure. Вы можете это сделать описанным ниже способом. Обратите внимание на то, что дополнительные характеристики можно создавать и в Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d279d-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="d279d-133">Запишите блок данных в локальный файл.</span><span class="sxs-lookup"><span data-stu-id="d279d-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="d279d-134">Отправьте данные в большой двоичный объект Azure так, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="d279d-134">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="d279d-135">Теперь данные можно считывать из большого двоичного объекта с помощью модуля [Импорт данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) машинного обучения Azure (см. рисунок ниже).</span><span class="sxs-lookup"><span data-stu-id="d279d-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![большой двоичный объект считывателя](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

