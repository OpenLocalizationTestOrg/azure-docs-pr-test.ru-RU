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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="28d85-103">Создание характеристик для данных хранилища больших двоичных объектов Azure с помощью Panda</span><span class="sxs-lookup"><span data-stu-id="28d85-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="28d85-104">В этом документе показано, как toocreate функции для данных, хранящихся в контейнере BLOB-объектов Azure, с помощью hello [Pandas](http://pandas.pydata.org/) пакета Python.</span><span class="sxs-lookup"><span data-stu-id="28d85-104">This document shows how toocreate features for data that is stored in Azure blob container using hello [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="28d85-105">После структуризации как tooload hello в кадр данных Panda, он отображается как toogenerate категориальных признаков с помощью сценариев Python значения индикатора и группирование компонентов.</span><span class="sxs-lookup"><span data-stu-id="28d85-105">After outlining how tooload hello data into a Panda data frame, it shows how toogenerate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="28d85-106">Это **меню** связывает tootopics, описано, как toocreate функции для данных в различных средах.</span><span class="sxs-lookup"><span data-stu-id="28d85-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="28d85-107">Эта задача является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="28d85-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28d85-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="28d85-108">Prerequisites</span></span>
<span data-ttu-id="28d85-109">В этой статье предполагается, что вы уже создали учетную запись хранилища BLOB-объектов Azure и сохранили в ней свои данные.</span><span class="sxs-lookup"><span data-stu-id="28d85-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="28d85-110">Получить инструкции tooset учетную запись [создать учетную запись хранилища Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="28d85-110">If you need instructions tooset up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="28d85-111">Загрузка данных hello Pandas кадра данных.</span><span class="sxs-lookup"><span data-stu-id="28d85-111">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="28d85-112">В порядке toodo просматривать и управлять набора данных, его необходимо загрузить из hello BLOB-объект источника tooa локального файла, которое можно загрузить в кадре данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="28d85-112">In order toodo explore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="28d85-113">Ниже приведены hello toofollow действия для выполнения данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="28d85-113">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="28d85-114">Скачать hello данные из Azure BLOB-объекта с hello, следующий пример кода Python, с помощью службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="28d85-114">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="28d85-115">Замените переменную hello в коде hello ниже особые значения:</span><span class="sxs-lookup"><span data-stu-id="28d85-115">Replace hello variable in hello code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="28d85-116">Чтение данных hello в Pandas-кадр данных из hello загрузили файл.</span><span class="sxs-lookup"><span data-stu-id="28d85-116">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="28d85-117">Теперь вы готовы tooexplore hello данные и создавать признаки на этот набор данных.</span><span class="sxs-lookup"><span data-stu-id="28d85-117">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="28d85-118"><a name="blob-featuregen"></a>Создание функций</span><span class="sxs-lookup"><span data-stu-id="28d85-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="28d85-119">Hello следующих двух разделах показано, как toogenerate категориальных признаков с значения индикатора и сегментирования функции с помощью сценариев Python.</span><span class="sxs-lookup"><span data-stu-id="28d85-119">hello next two sections show how toogenerate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="28d85-120"><a name="blob-countfeature"></a>Создание функций на основе значений индикатора</span><span class="sxs-lookup"><span data-stu-id="28d85-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="28d85-121">Вот как можно создавать категориальные функции:</span><span class="sxs-lookup"><span data-stu-id="28d85-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="28d85-122">Проверьте распределение hello hello категориальных столбцов:</span><span class="sxs-lookup"><span data-stu-id="28d85-122">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="28d85-123">Создание значения индикатора для каждого значения в столбце hello</span><span class="sxs-lookup"><span data-stu-id="28d85-123">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="28d85-124">Присоединение hello столбец индикатора с hello исходного кадра данных.</span><span class="sxs-lookup"><span data-stu-id="28d85-124">Join hello indicator column with hello original data frame</span></span>
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="28d85-125">Удалите саму переменную исходного hello:</span><span class="sxs-lookup"><span data-stu-id="28d85-125">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="28d85-126"><a name="blob-binningfeature"></a>Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="28d85-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="28d85-127">Вот как можно создавать функции группирования:</span><span class="sxs-lookup"><span data-stu-id="28d85-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="28d85-128">Добавить последовательность столбцов toobin числового столбца</span><span class="sxs-lookup"><span data-stu-id="28d85-128">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="28d85-129">Преобразовать последовательность сегментирования tooa логические переменные</span><span class="sxs-lookup"><span data-stu-id="28d85-129">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="28d85-130">Наконец соединения hello фиктивный переменные обратно toohello исходного кадра данных.</span><span class="sxs-lookup"><span data-stu-id="28d85-130">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="28d85-131"><a name="sql-featuregen"></a>Записи данных обратно tooAzure больших двоичных объектов и использование в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="28d85-131"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="28d85-132">После изучена hello данных и создать необходимые функции hello, можно передать данные hello (выборки или признак) tooan Azure BLOB-объектов и использовать его в машинном обучении Azure с помощью hello следующие шаги: Обратите внимание, что дополнительные компоненты могут создаваться в hello Студия машинного обучения также.</span><span class="sxs-lookup"><span data-stu-id="28d85-132">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="28d85-133">Запись файла toolocal кадра данных hello</span><span class="sxs-lookup"><span data-stu-id="28d85-133">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="28d85-134">Отправьте BLOB-объектов tooAzure hello данных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="28d85-134">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="28d85-135">Теперь hello данные могут считываться из hello BLOB-объекта с помощью hello машинного обучения Azure [импорта данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) модуля, как показано на экране приветствия ниже:</span><span class="sxs-lookup"><span data-stu-id="28d85-135">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in hello screen below:</span></span>

![большой двоичный объект считывателя](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

