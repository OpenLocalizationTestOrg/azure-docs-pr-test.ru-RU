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
# <span data-ttu-id="833e0-103"><a name="heading"></a>Обработка больших двоичных данных Azure с применением методов расширенного анализа</span><span class="sxs-lookup"><span data-stu-id="833e0-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="833e0-104">Этот документ содержит сведения о работе с данными в хранилище больших двоичных объектов Azure и создании характеристик на их основе.</span><span class="sxs-lookup"><span data-stu-id="833e0-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="833e0-105">Загрузка данных hello Pandas кадра данных.</span><span class="sxs-lookup"><span data-stu-id="833e0-105">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="833e0-106">В порядке tooexplore и управлять набора данных, его необходимо загрузить из hello BLOB-объект источника tooa локального файла, которое можно загрузить в кадре данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="833e0-106">In order tooexplore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="833e0-107">Ниже приведены hello toofollow действия для выполнения данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="833e0-107">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="833e0-108">Скачать hello данные из Azure BLOB-объекта с hello, следующий пример кода Python, с помощью службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="833e0-108">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="833e0-109">Замените переменную hello в коде hello ниже особые значения:</span><span class="sxs-lookup"><span data-stu-id="833e0-109">Replace hello variable in hello code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="833e0-110">Чтение данных hello в Pandas-кадр данных из hello загрузили файл.</span><span class="sxs-lookup"><span data-stu-id="833e0-110">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="833e0-111">Теперь вы готовы tooexplore hello данные и создавать признаки на этот набор данных.</span><span class="sxs-lookup"><span data-stu-id="833e0-111">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="833e0-112"><a name="blob-dataexploration"></a>Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="833e0-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="833e0-113">Ниже приведены некоторые примеры способов tooexplore данных с помощью Pandas.</span><span class="sxs-lookup"><span data-stu-id="833e0-113">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="833e0-114">Проверить количество строк и столбцов hello</span><span class="sxs-lookup"><span data-stu-id="833e0-114">Inspect hello number of rows and columns</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="833e0-115">Сначала просмотреть hello или в последний раз несколько строк в наборе данных hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="833e0-115">Inspect hello first or last few rows in hello dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="833e0-116">Проверьте hello тип данных каждого столбца были импортированы как с помощью hello следующий образец кода</span><span class="sxs-lookup"><span data-stu-id="833e0-116">Check hello data type each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="833e0-117">Как проверить основные Статистика hello hello столбцов в наборе данных hello</span><span class="sxs-lookup"><span data-stu-id="833e0-117">Check hello basic stats for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="833e0-118">Рассмотрим hello число записей для каждого значения в столбце</span><span class="sxs-lookup"><span data-stu-id="833e0-118">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="833e0-119">Число отсутствующих значений и hello фактическое число записей в каждом столбце, используя следующий пример кода hello</span><span class="sxs-lookup"><span data-stu-id="833e0-119">Count missing values versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="833e0-120">Если в данных hello нет значения для конкретного столбца, можно удалить их следующим образом:</span><span class="sxs-lookup"><span data-stu-id="833e0-120">If you have missing values for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="833e0-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="833e0-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="833e0-122">Другой способ tooreplace отсутствующих значений является режим функции hello.</span><span class="sxs-lookup"><span data-stu-id="833e0-122">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="833e0-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="833e0-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="833e0-124">Создать гистограмму диаграмму с помощью переменное число ячеек tooplot hello распространения переменной</span><span class="sxs-lookup"><span data-stu-id="833e0-124">Create a histogram plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="833e0-125">Посмотрите на взаимосвязи между переменными с помощью scatterplot или hello корреляции встроенные функции</span><span class="sxs-lookup"><span data-stu-id="833e0-125">Look at correlations between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="833e0-126"><a name="blob-featuregen"></a>Создание функций</span><span class="sxs-lookup"><span data-stu-id="833e0-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="833e0-127">Создавать функции с помощью Python вы можете приведенным ниже способом.</span><span class="sxs-lookup"><span data-stu-id="833e0-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="833e0-128"><a name="blob-countfeature"></a>Создание функций на основе значений индикатора</span><span class="sxs-lookup"><span data-stu-id="833e0-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="833e0-129">Вот как можно создавать категориальные функции:</span><span class="sxs-lookup"><span data-stu-id="833e0-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="833e0-130">Проверьте распределение hello hello категориальных столбцов:</span><span class="sxs-lookup"><span data-stu-id="833e0-130">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="833e0-131">Создание значения индикатора для каждого значения в столбце hello</span><span class="sxs-lookup"><span data-stu-id="833e0-131">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="833e0-132">Присоединение hello столбец индикатора с hello исходного кадра данных.</span><span class="sxs-lookup"><span data-stu-id="833e0-132">Join hello indicator column with hello original data frame</span></span> 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="833e0-133">Удалите саму переменную исходного hello:</span><span class="sxs-lookup"><span data-stu-id="833e0-133">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="833e0-134"><a name="blob-binningfeature"></a>Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="833e0-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="833e0-135">Вот как можно создавать функции группирования:</span><span class="sxs-lookup"><span data-stu-id="833e0-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="833e0-136">Добавить последовательность столбцов toobin числового столбца</span><span class="sxs-lookup"><span data-stu-id="833e0-136">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="833e0-137">Преобразовать последовательность сегментирования tooa логические переменные</span><span class="sxs-lookup"><span data-stu-id="833e0-137">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="833e0-138">Наконец соединения hello фиктивный переменные обратно toohello исходного кадра данных.</span><span class="sxs-lookup"><span data-stu-id="833e0-138">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="833e0-139"><a name="sql-featuregen"></a>Записи данных обратно tooAzure больших двоичных объектов и использование в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="833e0-139"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="833e0-140">После изучена hello данных и создать необходимые функции hello, можно передать данные hello (выборки или признак) tooan Azure BLOB-объектов и использовать его в машинном обучении Azure с помощью hello следующие шаги: Обратите внимание, что дополнительные компоненты могут создаваться в hello Студия машинного обучения также.</span><span class="sxs-lookup"><span data-stu-id="833e0-140">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="833e0-141">Запись файла toolocal кадра данных hello</span><span class="sxs-lookup"><span data-stu-id="833e0-141">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="833e0-142">Отправьте BLOB-объектов tooAzure hello данных следующим образом:</span><span class="sxs-lookup"><span data-stu-id="833e0-142">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="833e0-143">Теперь hello данные могут считываться из hello BLOB-объекта с помощью hello машинного обучения Azure [импорта данных] [ import-data] модуля, как показано на экране приветствия ниже:</span><span class="sxs-lookup"><span data-stu-id="833e0-143">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data][import-data] module as shown in hello screen below:</span></span>

![большой двоичный объект считывателя][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

