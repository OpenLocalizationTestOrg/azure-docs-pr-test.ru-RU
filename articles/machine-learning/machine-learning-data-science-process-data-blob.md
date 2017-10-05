---
title: "Обработка больших двоичных данных Azure с применением методов расширенного анализа | Документация Майкрософт"
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
ms.openlocfilehash: 36d950fd81029af82d9f2f652b2f01dba5fc8cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="ae65a-103"><a name="heading"></a>Обработка больших двоичных данных Azure с применением методов расширенного анализа</span><span class="sxs-lookup"><span data-stu-id="ae65a-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="ae65a-104">Этот документ содержит сведения о работе с данными в хранилище больших двоичных объектов Azure и создании характеристик на их основе.</span><span class="sxs-lookup"><span data-stu-id="ae65a-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="ae65a-105">Загрузка данных во фрейм данных Pandas</span><span class="sxs-lookup"><span data-stu-id="ae65a-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="ae65a-106">Для просмотра набора данных и управления им набор необходимо скачать из источника больших двоичных объектов в локальный файл, который затем можно загрузить в кадр данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="ae65a-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="ae65a-107">Ниже приведен порядок выполнения данной процедуры.</span><span class="sxs-lookup"><span data-stu-id="ae65a-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="ae65a-108">Скачайте данные из большого двоичного объекта Azure с помощью службы BLOB-объектов. Для этого воспользуйтесь приведенным ниже примером кода Python.</span><span class="sxs-lookup"><span data-stu-id="ae65a-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="ae65a-109">Замените переменные этого кода своими значениями.</span><span class="sxs-lookup"><span data-stu-id="ae65a-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="ae65a-110">Прочитайте данные, которые содержит скачанный файл, в блоке данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="ae65a-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="ae65a-111">Теперь вы готовы просматривать эти данные и создавать функции на основе этого набора данных.</span><span class="sxs-lookup"><span data-stu-id="ae65a-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="ae65a-112"><a name="blob-dataexploration"></a>Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="ae65a-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="ae65a-113">Вот несколько примеров того, как можно просматривать данные с помощью Pandas:</span><span class="sxs-lookup"><span data-stu-id="ae65a-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="ae65a-114">Проверьте количество строк и столбцов.</span><span class="sxs-lookup"><span data-stu-id="ae65a-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="ae65a-115">Проверьте первые или последние несколько строк в наборе данных так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ae65a-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="ae65a-116">Проверьте тип данных, импортированный в каждый столбец, с помощью приведенного ниже образца кода.</span><span class="sxs-lookup"><span data-stu-id="ae65a-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="ae65a-117">Проверьте основную статистику, относящуюся к столбцам набора данных, так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ae65a-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="ae65a-118">Проверьте количество записей в каждом столбце так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ae65a-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="ae65a-119">Проверьте соотношение числа отсутствующих значений к фактическому количеству записей в каждом столбце. Воспользуйтесь приведенным ниже образцом кода.</span><span class="sxs-lookup"><span data-stu-id="ae65a-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="ae65a-120">Если в том или ином столбце данных отсутствуют значения, вы можете заменить их так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ae65a-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="ae65a-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="ae65a-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="ae65a-122">Другой способ заменить отсутствующие значения — воспользоваться функцией режима.</span><span class="sxs-lookup"><span data-stu-id="ae65a-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="ae65a-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="ae65a-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="ae65a-124">Создайте гистограмму, используя переменное количество ячеек, чтобы построить распределение переменной.</span><span class="sxs-lookup"><span data-stu-id="ae65a-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="ae65a-125">Проверьте корреляции между переменными, используя диаграмму рассеяния или встроенную функцию корреляции.</span><span class="sxs-lookup"><span data-stu-id="ae65a-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="ae65a-126"><a name="blob-featuregen"></a>Создание характеристик</span><span class="sxs-lookup"><span data-stu-id="ae65a-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="ae65a-127">Создавать функции с помощью Python вы можете приведенным ниже способом.</span><span class="sxs-lookup"><span data-stu-id="ae65a-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="ae65a-128"><a name="blob-countfeature"></a>Создание функций на основе значений индикатора</span><span class="sxs-lookup"><span data-stu-id="ae65a-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="ae65a-129">Вот как можно создавать категориальные функции:</span><span class="sxs-lookup"><span data-stu-id="ae65a-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="ae65a-130">Проверьте распределение категориального столбца.</span><span class="sxs-lookup"><span data-stu-id="ae65a-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="ae65a-131">Создайте значения индикатора для каждого значения столбца.</span><span class="sxs-lookup"><span data-stu-id="ae65a-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="ae65a-132">Объедините столбец индикатора с исходным блоком данных.</span><span class="sxs-lookup"><span data-stu-id="ae65a-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="ae65a-133">Удалите исходную переменную.</span><span class="sxs-lookup"><span data-stu-id="ae65a-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="ae65a-134"><a name="blob-binningfeature"></a>Создание характеристик путем группирования данных</span><span class="sxs-lookup"><span data-stu-id="ae65a-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="ae65a-135">Вот как можно создавать функции группирования:</span><span class="sxs-lookup"><span data-stu-id="ae65a-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="ae65a-136">Добавьте последовательность столбцов, чтобы создать числовой столбец.</span><span class="sxs-lookup"><span data-stu-id="ae65a-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="ae65a-137">Преобразуйте группирование в последовательность логических переменных.</span><span class="sxs-lookup"><span data-stu-id="ae65a-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="ae65a-138">Наконец, объедините фиктивные переменные с исходным блоком данных.</span><span class="sxs-lookup"><span data-stu-id="ae65a-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="ae65a-139"><a name="sql-featuregen"></a>Запись данных обратно в большой двоичный объект Azure и их использование в Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="ae65a-139"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="ae65a-140">После просмотра данных и создания необходимых вам признаков вы можете отправить данные (в выборке или в признаке) в большой двоичный объект Azure и использовать их в Студии машинного обучения Azure. Вы можете это сделать описанным ниже способом. Обратите внимание на то, что дополнительные характеристики можно создавать и в Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ae65a-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="ae65a-141">Запишите блок данных в локальный файл.</span><span class="sxs-lookup"><span data-stu-id="ae65a-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="ae65a-142">Отправьте данные в большой двоичный объект Azure так, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="ae65a-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="ae65a-143">Теперь данные можно считывать из большого двоичного объекта с помощью модуля [Импорт данных][import-data] машинного обучения Azure (см. рисунок ниже).</span><span class="sxs-lookup"><span data-stu-id="ae65a-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![большой двоичный объект считывателя][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

