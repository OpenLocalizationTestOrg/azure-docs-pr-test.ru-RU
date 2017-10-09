---
title: "Hello командного процесса обработки и анализа данных в действие — с помощью кластера Azure HDInsight Hadoop для набора данных 1 ТБ | Документы Microsoft"
description: "С помощью hello процесс обработки и анализа данных для команды сценария конца в конец данных, построенных на HDInsight Hadoop кластера toobuild и развертывания модели с помощью большого набора данных общедоступным (1 ТБ)"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="2fdf2-103">Hello командного процесса обработки и анализа данных в действие — с помощью кластера Azure HDInsight Hadoop для набора данных 1 ТБ</span><span class="sxs-lookup"><span data-stu-id="2fdf2-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="2fdf2-104">В этом пошаговом руководстве показано использование hello командного процесса обработки и анализа данных в сценарии с начала до конца [кластера Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, изучение, инженер компонентов и публично вниз образец данных из одного hello Доступные [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) наборов данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="2fdf2-105">Мы используем машинного обучения Azure toobuild модель двоичной классификации на основе этих данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="2fdf2-106">Также мы покажем, как toopublish одну из этих моделей как веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="2fdf2-107">Это также возможно toouse задачи hello tooaccomplish ноутбук IPython, представленных в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="2fdf2-108">Пользователей, которые бы как tootry, такой подход следует обратиться к hello [Criteo Пошаговое руководство по использованию соединений Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) раздела.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="2fdf2-109"><a name="dataset"></a>Описание набора данных Criteo</span><span class="sxs-lookup"><span data-stu-id="2fdf2-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="2fdf2-110">Hello Criteo данных является прогноз щелкните набор данных, составляет приблизительно 370 gzip сжатых файлов TSV (~1.3TB несжатых данных), составляющие 4.3 миллиард записей.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="2fdf2-111">Эти данные получены на основе данных о переходах по ссылкам за 24 дня, предоставленных [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="2fdf2-112">Для удобства hello специалистами по анализу данных мы распаковал tooexperiment toous доступных данных с.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="2fdf2-113">Каждая запись в этом наборе данных содержит 40 столбцов:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="2fdf2-114">Hello первый столбец является столбцом метки, указывающее, является ли пользователь щелкает **добавить** (значение 1) или не см (значение 0)</span><span class="sxs-lookup"><span data-stu-id="2fdf2-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="2fdf2-115">следующие 13 столбцов являются числовыми;</span><span class="sxs-lookup"><span data-stu-id="2fdf2-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="2fdf2-116">последние 26 столбцов категориальные.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-116">last 26 are categorical columns</span></span>

<span data-ttu-id="2fdf2-117">Hello столбцы являются анонимны и использовать ряд перечисленные имена: «Col1» (для столбца меток hello) слишком "Col40» (для последнего столбца категорий hello).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="2fdf2-118">Ниже приведен фрагмент hello сначала 20 столбцы двух наблюдения (строк) из этого набора данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="2fdf2-119">Отсутствуют некоторые значения в обоих столбцах числовых и категориальные hello в этом наборе данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="2fdf2-120">Чтобы описать простой метод для обработки недостающих значений hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="2fdf2-121">Дополнительные сведения о данных hello изучаются при их хранения в таблицах Hive.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="2fdf2-122">**Определение:** *скорость с дополнительной информацией (CTR):* это процент hello щелчков мыши hello данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="2fdf2-123">В этом наборе Criteo данных hello CTR — около % 3.3 или 0.033.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="2fdf2-124"><a name="mltasks"></a>Примеры задач прогнозирования</span><span class="sxs-lookup"><span data-stu-id="2fdf2-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="2fdf2-125">В этом пошаговом руководстве рассмотрены два примера задач по прогнозированию:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="2fdf2-126">**Двоичная классификация**— прогнозирует, щелкнет ли пользователь рекламное объявление:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="2fdf2-127">класс 0 — не щелкнул;</span><span class="sxs-lookup"><span data-stu-id="2fdf2-127">Class 0: No Click</span></span>
   * <span data-ttu-id="2fdf2-128">класс 1 — щелкнул.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-128">Class 1: Click</span></span>
2. <span data-ttu-id="2fdf2-129">**Регрессия**: прогнозирует вероятность hello и нажмите кнопку ad из признаки пользователя.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="2fdf2-130"><a name="setup"></a>Настройка кластера HDInsight Hadoop для обработки и анализа данных</span><span class="sxs-lookup"><span data-stu-id="2fdf2-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="2fdf2-131">**Примечание.** Эту задачу обычно выполняет **администратор**.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="2fdf2-132">Настройте среду обработки и анализа данных Azure, чтобы создавать решения для прогнозной аналитики с помощью кластеров HDInsight, выполнив три шага:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="2fdf2-133">[Создать учетную запись хранилища](../storage/common/storage-create-storage-account.md): этой учетной записи хранения — используется toostore данные в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="2fdf2-134">Здесь хранятся данные Hello, используемые в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="2fdf2-135">[Настройка кластеров Azure HDInsight Hadoop для обработки и анализа данных.](machine-learning-data-science-customize-hadoop-cluster.md) На этом шаге создается кластер Azure HDInsight Hadoop и на всех узлах устанавливается 64-разрядный дистрибутив Anaconda Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="2fdf2-136">При настройке кластера HDInsight hello существуют два toocomplete важные действия (как описано в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="2fdf2-137">Необходимо связать учетную запись хранения hello, созданной на шаге 1 с кластером HDInsight, при его создании.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="2fdf2-138">Эта учетная запись используется для доступа к данным, которое может быть обработано в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="2fdf2-139">Необходимо включить удаленный доступ toohello головного узла кластера hello после его создания.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="2fdf2-140">Запоминать учетные данные удаленного доступа hello, указанные здесь (отличающиеся от параметров, указанных для hello кластера при его создании): при необходимости toocomplete hello следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="2fdf2-141">[Создайте рабочую область машинного Обучения Azure](machine-learning-create-workspace.md): рабочая область машинного обучения этот Azure используется для построения моделей машинного обучения, после просмотра исходных данных, а также работу выборки в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="2fdf2-142"><a name="getdata"></a>Получение и использование данных из общедоступного источника</span><span class="sxs-lookup"><span data-stu-id="2fdf2-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="2fdf2-143">Hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) набор данных может осуществляться, щелкнув ссылку hello, принимая hello условия использования и предоставления имени.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="2fdf2-144">Ниже показан снимок того, как это выглядит.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-144">A snapshot of what this looks like is shown here:</span></span>

![Принятие условий использования Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="2fdf2-146">Нажмите кнопку **tooDownload Продолжить** tooread Дополнительные сведения о hello набора данных и его доступности.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="2fdf2-147">Hello данные находятся в открытом [хранилище больших двоичных объектов](../storage/blobs/storage-dotnet-how-to-use-blobs.md) расположение: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="2fdf2-148">Hello «wasb» ссылается tooAzure место хранения большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="2fdf2-149">Hello данные в это хранилище BLOB-объект открытого состоит из трех во вложенных данных в распакованную.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="2fdf2-150">Здравствуйте, вложенная папка *необработанные и числа объектов/* содержит hello первый 21 день данных — от дня\_00 tooday\_20</span><span class="sxs-lookup"><span data-stu-id="2fdf2-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="2fdf2-151">Здравствуйте, вложенная папка *raw/Обучение/* состоит из одного дня данных, день\_21</span><span class="sxs-lookup"><span data-stu-id="2fdf2-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="2fdf2-152">Здравствуйте, вложенная папка *необработанные и тестирования или* состоит из двух дней данных, день\_22 и день\_23</span><span class="sxs-lookup"><span data-stu-id="2fdf2-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="2fdf2-153">Для теми, кто toostart с hello gzip необработанных данных, они также доступны в главную папку hello *raw /* как day_NN.gz, где NN находятся значения от 00 too23.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="2fdf2-154">Альтернативный подход tooaccess, просматривайте и модели данных, которые не требуются все локальные файлы для загрузки описан далее в этом пошаговом руководстве при создании таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="2fdf2-155"><a name="login"></a>Войдите в головному узлу кластера toohello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="2fdf2-156">toolog в toohello головному узлу кластера hello, используйте hello [портал Azure](https://ms.portal.azure.com) toolocate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="2fdf2-157">Щелкните значок elephant HDInsight hello hello слева, а затем дважды щелкните имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="2fdf2-158">Перейдите toohello **конфигурации** вкладку, дважды щелкните значок CONNECT hello hello нижней части страницы hello и введите свои учетные данные удаленного доступа при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="2fdf2-159">Это занимает toohello головному узлу кластера hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="2fdf2-160">Ниже приведен типичный первый вход головному узлу кластера toohello выглядит как:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![Войдите в toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="2fdf2-162">В левой части экрана приветствия мы видим hello «Hadoop Command Line», которая является нашей workhorse для просмотра данных hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="2fdf2-163">На экране также отображаются два полезных URL-адреса — «Состояние Hadoop Yarn» и «Узел имен Hadoop».</span><span class="sxs-lookup"><span data-stu-id="2fdf2-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="2fdf2-164">URL-адрес состояния yarn Hello показывает ход выполнения задания и URL-адрес узла hello имя подробные сведения о конфигурации кластера hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="2fdf2-165">Теперь мы настроены и готовы toobegin первой части пошагового руководства hello: Просмотр данных с помощью Hive и Подготовка данных для машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="2fdf2-166"><a name="hive-db-tables"></a> Создание базы данных и таблиц Hive</span><span class="sxs-lookup"><span data-stu-id="2fdf2-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="2fdf2-167">таблицы toocreate Hive для наших Criteo dataset, откройте hello ***командной строки Hadoop*** hello desktop hello головного узла, а также введите hello Hive каталог, введя команду hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="2fdf2-168">Выполнить все команды Hive в этом пошаговом руководстве из ячейки Hive hello / directory строки.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="2fdf2-169">Таким образом вы сможете автоматически избежать любых проблем с путем.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="2fdf2-170">Мы используем условия hello «Hive каталога prompt», «Hive bin / подсказки директории» и «командной строки Hadoop» попеременно.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="2fdf2-171">tooexecute любого запроса Hive можно всегда использовать hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="2fdf2-172">После hello Hive REPL отображается с «hive > "войти, просто Вырезать и вставить запрос tooexecute hello его.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="2fdf2-173">Hello следующий код создает базу данных «criteo» и затем создает 4 таблиц:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="2fdf2-174">*таблицы для создания счетчиков* лежит дней день\_00 tooday\_20,</span><span class="sxs-lookup"><span data-stu-id="2fdf2-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="2fdf2-175">*как hello обучающего набора данных на таблицу для использования* лежит день\_21, и</span><span class="sxs-lookup"><span data-stu-id="2fdf2-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="2fdf2-176">два *таблицы для использования в качестве hello проверочных наборов данных* лежит день\_22 и день\_23 соответственно.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="2fdf2-177">Мы разбить нашей проверочный набор данных двух различных таблиц, так как один из дней hello является выходным днем, и мы стремимся toodetermine Если hello модели можно определить различия между праздников и не праздничных от частоты hello с дополнительной информацией.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="2fdf2-178">Здравствуйте, сценарий [образец &#95; hive &#95; Создание &#95; criteo &#95; базы данных &#95; и &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) будет отображена здесь для удобства:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="2fdf2-179">Мы Обратите внимание, что эти таблицы внешнего как мы просто tooAzure точка расположения хранилища больших двоичных объектов (wasb).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="2fdf2-180">**Существует два способа tooexecute ANY Hive запрос, который теперь упоминается.**</span><span class="sxs-lookup"><span data-stu-id="2fdf2-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="2fdf2-181">**С помощью Hive REPL командной строки "hello"**: hello сначала является tooissue команда «hive» и скопируйте и вставьте запрос в hello Hive REPL командной строки.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="2fdf2-182">toodo этой, выполните:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="2fdf2-183">Теперь в hello REPL командной строки, вырезание и вставка запроса hello выполняет его.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="2fdf2-184">**Сохранение запросов tooa файла и выполнении команды hello**: hello, второй — toosave hello запросы tooa .hql файла ([образец &#95; hive &#95; Создание &#95; criteo &#95; базы данных &#95; и &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) и затем проблема hello следующая команда tooexecute hello запроса:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="2fdf2-185">Подтверждение создания базы данных и таблицы</span><span class="sxs-lookup"><span data-stu-id="2fdf2-185">Confirm database and table creation</span></span>
<span data-ttu-id="2fdf2-186">Далее мы подтвердить создание hello hello базы данных с hello следующую команду из ячейки Hive hello / directory строки:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="2fdf2-187">Результат выполнения команды:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="2fdf2-188">Это подтверждает Создание hello hello новую базу данных, «criteo».</span><span class="sxs-lookup"><span data-stu-id="2fdf2-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="2fdf2-189">toosee какие таблицы мы создали, мы просто выполните команду hello здесь из ячейки Hive hello / directory строки:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="2fdf2-190">Затем мы видим hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="2fdf2-191"><a name="exploration"></a> Просмотр данных в Hive</span><span class="sxs-lookup"><span data-stu-id="2fdf2-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="2fdf2-192">Теперь мы готовы toodo просмотра некоторых основных данных в кусте.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="2fdf2-193">Мы начните с инвентаризации hello количество примеров в hello обучение и таблицы данных теста.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="2fdf2-194">Количество примеров для обучения</span><span class="sxs-lookup"><span data-stu-id="2fdf2-194">Number of train examples</span></span>
<span data-ttu-id="2fdf2-195">Здравствуйте, содержимое [образец &#95; hive &#95; число &#95; обучение &#95; таблицы &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) показано ниже:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="2fdf2-196">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="2fdf2-197">Кроме того, один также может выдать следующую команду из ячейки Hive hello hello / directory строки:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="2fdf2-198">Количество примеров теста в наборах данных hello два теста</span><span class="sxs-lookup"><span data-stu-id="2fdf2-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="2fdf2-199">Теперь мы счетчик hello количество примеров в hello двух наборов данных теста.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="2fdf2-200">Здравствуйте, содержимое [образец & #95 hive & #95 счетчик &#95; criteo &#95; тестовые &#95; & #95 день; 22 &#95; #95;examples.hql & таблицы](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) рассматриваются следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="2fdf2-201">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="2fdf2-202">Как обычно, мы также может выполнять вызов сценария hello из ячейки Hive hello / directory приглашения, выполнив команду hello:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="2fdf2-203">Наконец, мы изучаем hello количество примеров теста в проверочном наборе данных hello, в зависимости от дня\_23.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="2fdf2-204">Hello команда toodo это аналогичный toohello просто показанной (см. слишком[образец &#95; hive &#95; число &#95; criteo &#95; тестовые &#95; день &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="2fdf2-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="2fdf2-205">Результат выполнения команды:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="2fdf2-206">Метка распространения в наборе данных обучение hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="2fdf2-207">Hello распространения метки в наборе данных обучение hello представляет интерес.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="2fdf2-208">toosee это, мы Показать содержимое [образец &#95; hive &#95; criteo &#95; метка &#95; распространения &#95; обучение &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="2fdf2-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="2fdf2-209">Это дает hello метки распространения:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="2fdf2-210">Обратите внимание, что процент hello положительное метки около 3.3% (согласуется с hello исходный набор данных).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="2fdf2-211">Набор данных обучения Гистограмма распределения некоторых числовых переменных в hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="2fdf2-212">Можно использовать собственный куста «гистограммы\_числовых» функции toofind out какие hello распределение числовых переменных hello выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="2fdf2-213">Вот содержимое hello [образец &#95; hive &#95; criteo &#95; гистограммы &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="2fdf2-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="2fdf2-214">Это дает ниже hello:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-214">This yields hello following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="2fdf2-215">ПРЕДСТАВЛЕНИЕ — БОКОВОЕ Hello разрезать сочетание в куст служит tooproduce SQL-подобного выходные данные вместо обычного списка hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="2fdf2-216">Обратите внимание, что в hello этой таблицы, первый столбец hello соответствует toohello bin center и hello второй toohello bin частоты.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="2fdf2-217">Приблизительное процентилем некоторых числовых переменных в hello обучения набора данных</span><span class="sxs-lookup"><span data-stu-id="2fdf2-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="2fdf2-218">Также интереса с числовых переменных, вычисление приблизительное процентилем hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="2fdf2-219">Функция Hive percentile\_approx делает это автоматически.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="2fdf2-220">Здравствуйте, содержимое [образец &#95; hive &#95; criteo &#95; приблизительное &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) являются:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="2fdf2-221">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="2fdf2-222">Мы оператор комментария hello распределение процентилем обычно является тесно связанных toohello гистограммы распространения любой числовой переменной.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="2fdf2-223">Найти количество уникальных значений для некоторых категориальных столбцов в наборе данных обучение hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="2fdf2-224">Продолжить просмотр данных hello, мы теперь доступны, для некоторых категориальных столбцов hello количество уникальных значений, которые они принимают.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="2fdf2-225">toodo это, мы Показать содержимое [образец &#95; hive &#95; criteo &#95; уникальный &#95; значения &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="2fdf2-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="2fdf2-226">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="2fdf2-227">Обратите внимание, что в столбце Col15 найдено 19 млн. уникальных значений!</span><span class="sxs-lookup"><span data-stu-id="2fdf2-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="2fdf2-228">С помощью упрощенного такие методы, как «горячая один кодировка» tooencode таких многомерными категориальных переменных невозможна.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="2fdf2-229">Для эффективного решения этой проблемы объясняется и демонстрируется эффективный и надежный метод, называемый [обучение с использованием счетчиков](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="2fdf2-230">Этот подраздел мы последний, просмотрев hello количество уникальных значений для некоторых других категориальных столбцов также.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="2fdf2-231">Здравствуйте, содержимое [образец &#95; hive &#95; criteo &#95; уникальный &#95; значения &#95; несколько &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) являются:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="2fdf2-232">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="2fdf2-233">Опять же мы видим, за исключением Col20, все hello другие столбцы имеют много уникальных значений.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="2fdf2-234">Количество вхождений сопутствующего пар категориальных переменных в наборе данных обучение hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="2fdf2-235">количество вхождений сопутствующего Hello пары категориальные переменные также представляет интерес.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="2fdf2-236">Это может быть определено с помощью кода hello в [образец &#95; hive &#95; criteo &#95; парной &#95; категориальные &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="2fdf2-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="2fdf2-237">Мы обратном hello числа заказов по их вхождения и в этом случае просмотрите hello top 15.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="2fdf2-238">Результат выполнения команды:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="2fdf2-239"><a name="downsample"></a>Вниз hello образцы наборов данных для машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="2fdf2-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="2fdf2-240">При необходимости изучать hello наборы данных и показано, как может сделать этот тип для просмотра всех переменных (включая комбинаций), мы теперь вниз образцы наборов данных hello, что мы можно создавать модели в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="2fdf2-241">Помните, мы сосредоточим внимание на проблему hello является: при заданном наборе образцы атрибутов (значения компонента из Col2 - Col40), мы прогнозировать, является ли Col1 0 (нет щелкните) или 1 (щелкните).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="2fdf2-242">toodown образца нашей обучения и тестирования, наборов данных too1% от исходного размера hello, мы используем куста собственной функции RAND().</span><span class="sxs-lookup"><span data-stu-id="2fdf2-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="2fdf2-243">Здравствуйте следующему сценарию [образец &#95; hive &#95; criteo &#95; понижение разрешения &#95; обучение &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) делает это для набора данных для обучения hello:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="2fdf2-244">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="2fdf2-245">Здравствуйте, сценарий [образец &#95; hive &#95; criteo &#95; понижение разрешения &#95; тестовые &#95; & #95 день; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) делает это для проверочных данных, день\_22:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="2fdf2-246">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="2fdf2-247">Наконец, hello скрипт [образец &#95; hive &#95; criteo &#95; понижение разрешения &#95; тестовые &#95; & #95 день; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) делает это для проверочных данных, день\_23:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="2fdf2-248">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="2fdf2-249">Таким образом, мы будут готовы toouse наш список выборки обучения и проверочных наборов данных для построения моделей в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="2fdf2-250">Прежде чем мы перейдем tooAzure машинного обучения, являющийся таблицы счетчиков hello проблемы нет окончательного важным компонентом.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="2fdf2-251">В следующем разделе вложенных hello мы обсудим это некоторые сведения.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="2fdf2-252"><a name="count"></a>Краткое описание для таблицы счетчиков hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="2fdf2-253">Как было видно, несколько категориальных переменных обладают очень высокой размерностью.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="2fdf2-254">В нашем пошаговом руководстве рассматриваются мощный метод, называемый [обучения с подсчитывает](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode эти переменные эффективным и надежным способом.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="2fdf2-255">Дополнительные сведения об этом приеме — hello ссылке.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="2fdf2-256">В этом пошаговом руководстве мы связана с использованием число таблиц tooproduce compact представления многомерными категориальных признаков.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="2fdf2-257">Это не hello единственным способом tooencode категориальных признаков; Дополнительные сведения о других возможностях интерес пользователи могут извлекать [один горячей encoding](http://en.wikipedia.org/wiki/One-hot) и [хэширование признаков](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="2fdf2-258">таблицы счетчиков toobuild hello количество данных, мы используем данные hello в hello raw или число папок.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="2fdf2-259">В hello моделирования разделе, демонстрируется пользователей как toobuild они подсчитывают таблицы для категориальных признаков с нуля, или в качестве альтернативы toouse таблицу готовые счетчиков для их изучения.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="2fdf2-260">В том, что следующим образом, когда мы ссылаемся слишком «готовые таблицы счетчиков», имеется в виду с помощью таблиц счетчиков hello, мы предоставляем.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="2fdf2-261">Подробные инструкции по как tooaccess эти таблицы приведены в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="2fdf2-262"><a name="aml"></a> Создание моделей с помощью Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="2fdf2-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="2fdf2-263">Процесс создания моделей в Машинном обучении Azure состоит из следующих шагов:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="2fdf2-264">Получать данные hello из таблицы Hive в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="2fdf2-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="2fdf2-265">Создайте эксперимент hello: очистка данных hello и создания признаков с помощью таблиц счетчиков</span><span class="sxs-lookup"><span data-stu-id="2fdf2-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="2fdf2-266">Сборки, обучение и hello оценка модели</span><span class="sxs-lookup"><span data-stu-id="2fdf2-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="2fdf2-267">Hello модель оценки</span><span class="sxs-lookup"><span data-stu-id="2fdf2-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="2fdf2-268">Опубликовать как веб служба модели hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="2fdf2-269">Теперь мы все готово toobuild моделей в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="2fdf2-270">Наши вниз выборки данных сохраняется как таблицы Hive в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="2fdf2-271">Мы используем hello машинного обучения Azure **импорта данных** модуль tooread эти данные.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="2fdf2-272">Учетная запись хранения Hello учетные данные с tooaccess hello этого кластера приведены в какие следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="2fdf2-273"><a name="step1"></a>Шаг 1: Получение данных из таблицы Hive в машинном обучении Azure с помощью модуля hello импорта данных и выбрать его для эксперимента машинного обучения</span><span class="sxs-lookup"><span data-stu-id="2fdf2-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="2fdf2-274">Для начала выберите **+Создать** -> **Эксперимент** -> **Пустой эксперимент**.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="2fdf2-275">Затем из hello **поиска** поле на hello вверху слева, поиск «Импорт данных».</span><span class="sxs-lookup"><span data-stu-id="2fdf2-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="2fdf2-276">Перетаскивание hello **импорта данных** модуль toohello эксперимента canvas (hello средней части экрана приветствия) toouse hello модуля для доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="2fdf2-277">Это связано с какой hello **импорта данных** выглядит как при получении данных из таблицы Hive hello:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![Модуль "Импорт данных" получает данные](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="2fdf2-279">Для hello **импорта данных** tooprovide требуется модуль hello значения параметров "hello", предоставляемые в hello график — это только примеры hello сортировку значений.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="2fdf2-280">Ниже приведены некоторые общие рекомендации по установке toofill hello параметр out для hello **импорта данных** модуля.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="2fdf2-281">В поле **Источник данных**</span><span class="sxs-lookup"><span data-stu-id="2fdf2-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="2fdf2-282">В hello **запроса базы данных Hive** поле простой запрос SELECT * FROM < ваш\_базы данных\_name.your\_таблицы\_имя >-достаточно.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="2fdf2-283">**URI сервера Hcatalog** — если используется кластер abc, введите адрес https://abc.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="2fdf2-284">**Имя учетной записи пользователя Hadoop**: hello имени пользователя, выбранного во время hello commissioning hello кластера.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="2fdf2-285">(Не hello именем пользователя удаленного доступа!)</span><span class="sxs-lookup"><span data-stu-id="2fdf2-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="2fdf2-286">**Пароль учетной записи пользователя Hadoop**: hello пароль для имени пользователя hello, выбранного во время hello commissioning hello кластера.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="2fdf2-287">(Не hello пароля для удаленного доступа!)</span><span class="sxs-lookup"><span data-stu-id="2fdf2-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="2fdf2-288">**Расположение выходных данных**: выберите Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="2fdf2-289">**Имя учетной записи хранилища Azure**: hello учетной записи хранилища, связанного с кластером hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="2fdf2-290">**Ключ учетной записи хранилища Azure**: hello ключ учетной записи хранилища hello, связанной с кластером hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="2fdf2-291">**Имя контейнера Azure**: Если имя кластера hello «abc», то обычно это просто «abc»,.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="2fdf2-292">Здравствуйте, один раз **импорта данных** окончания получения данных (отображается зеленый hello делений на hello модуля), сохранить эти данные как набор данных (с именем по своему усмотрению).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="2fdf2-293">Это выглядит так:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-293">What this looks like:</span></span>

![Модуль "Импорт данных" сохраняет данные](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="2fdf2-295">Щелкните правой кнопкой мыши hello выходной порт hello **импорта данных** модуля.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="2fdf2-296">Отобразятся параметры **Сохранение набора данных** и **Визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="2fdf2-297">Hello **визуализировать** параметр, если выбран вариант, отображает 100 строк данных hello, вместе с правой панели, который удобен для некоторых сводные статистические данные.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="2fdf2-298">toosave данных, просто выберите **Сохранить как набор данных** и следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="2fdf2-299">dataset tooselect hello сохранен для использования в образовательных эксперименте машины, найдите hello наборов данных при помощи hello **поиска** поле показано hello следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="2fdf2-300">Затем просто ввести имя hello Вы дали hello dataset частично tooaccess его и перетащите hello набора данных в hello главной панели.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="2fdf2-301">На место hello главной панели выбирает для использования в моделировании машины обучения.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Набор данных сводной на главной панели hello](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="2fdf2-303">Сделайте это для обучения hello и наборы данных теста hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="2fdf2-304">Кроме того помните, имя базы данных toouse hello и имена таблиц, которые вы присвоили для этой цели.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="2fdf2-305">Hello значения, используемые на рисунке hello предназначены исключительно для иллюстрации purposes.* *</span><span class="sxs-lookup"><span data-stu-id="2fdf2-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="2fdf2-306"><a name="step2"></a>Шаг 2: Создание простого эксперимента машинного обучения Azure движениями toopredict и не щелкает</span><span class="sxs-lookup"><span data-stu-id="2fdf2-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="2fdf2-307">Наш эксперимент Машинного обучения Azure выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-307">Our Azure ML experiment looks like this:</span></span>

![Эксперимент машинного обучения](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="2fdf2-309">Рассматриваются основные компоненты этого эксперимента hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="2fdf2-310">Напоминаем нам нужна toodrag наши сохраненные обучения и проверочных наборов данных на холст эксперимента tooour сначала.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="2fdf2-311">Очистка недостающих данных</span><span class="sxs-lookup"><span data-stu-id="2fdf2-311">Clean Missing Data</span></span>
<span data-ttu-id="2fdf2-312">Hello **Очистка недостающих данных** модуль делает его названия: он удаляет отсутствующие данные таким образом, может задаваться пользователем.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="2fdf2-313">Если посмотреть на модуль, мы увидим следующее:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-313">Looking into this module, we see this:</span></span>

![Очистка недостающих данных](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="2fdf2-315">Здесь мы выбрали tooreplace все отсутствующие значения с 0.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="2fdf2-316">Существуют другие параметры, в том, которые можно увидеть, просмотрев hello раскрывающихся списков в модуле hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="2fdf2-317">Конструируются hello данных</span><span class="sxs-lookup"><span data-stu-id="2fdf2-317">Feature engineering on hello data</span></span>
<span data-ttu-id="2fdf2-318">Некоторые категориальные функции крупных наборов данных могут иметь миллионы уникальных значений.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="2fdf2-319">Использовать для представления таких многомерных функций упрощенные методы, например метод "прямого кодирования", нецелесообразно.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="2fdf2-320">В этом пошаговом руководстве показано, как toouse число компонентов, с помощью встроенных toogenerate модули машинного обучения Azure compact представления этих многомерными категориальные переменные.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="2fdf2-321">Hello конечным результатом является меньший размер модели, сократить время обучения и метрики производительности, которые довольно сопоставимых toousing других методов.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="2fdf2-322">Построение преобразований счетчиков</span><span class="sxs-lookup"><span data-stu-id="2fdf2-322">Building counting transforms</span></span>
<span data-ttu-id="2fdf2-323">toobuild число функций, мы используем hello **построения подсчета преобразования** модуль, который доступен в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="2fdf2-324">модуль Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-324">hello module looks like this:</span></span>

<span data-ttu-id="2fdf2-325">![Модуль построения преобразования счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Модуль построения преобразования счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="2fdf2-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2fdf2-326">В hello **число столбцов** , мы введите в поле желаем tooperform учитывается на столбцы.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="2fdf2-327">Обычно это (как уже говорилось) — многомерные категориальные столбцы.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="2fdf2-328">Во время запуска hello, мы уже упоминали Criteo hello набор данных имеет 26 категориальных столбцов: из Col15 tooCol40.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="2fdf2-329">Здесь мы подсчета на всех из них и предоставлять их индексы (из 15 too40, разделенных запятыми, как показано).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="2fdf2-330">модуль toouse hello в Здравствуйте MapReduce режиме (подходит для больших наборов данных), мы должны получить доступ к кластера HDInsight Hadoop tooan (одно для исследования компонент может быть повторно использован для этой цели также приветствия) и его учетные данные.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="2fdf2-331">Hello предыдущих рисунках показаны hello заполняться значениями выглядеть следующим образом (Замените hello значений, заданных для сочетается с другими, соответствующими для собственных варианта использования).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![Параметры модуля](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="2fdf2-333">В hello выше рисунке показано, как tooenter hello входного BLOB-объект расположения.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="2fdf2-334">Это расположение содержит данные hello, выделенная для создания таблиц счетчиков.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="2fdf2-335">После завершения этого модуля, мы сможем Сохранить преобразование hello для более поздней версии, щелкните правой кнопкой мыши модуль hello и выбрав hello **сохранение преобразования** параметр:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

![Параметр Save as Transform (Сохранить как преобразование)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="2fdf2-337">В нашей архитектуры эксперимента, показанном выше hello dataset «ytransform2» соответствует точно tooa Сохранить преобразование count.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="2fdf2-338">Hello оставшейся части этого эксперимента, предполагается, что используемое чтения hello **построения подсчета преобразования** модуля на некоторые счетчики toogenerate данных и затем может использовать эти функции count toogenerate счетчиков hello обучения и проверочных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="2fdf2-339">Выбор, что подсчет tooinclude функции как часть обучения hello и проверочных наборов данных</span><span class="sxs-lookup"><span data-stu-id="2fdf2-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="2fdf2-340">После получения счетчик преобразования готовности hello пользователь может выбрать какие функции tooinclude в их поезда и проверочных наборов данных с помощью hello **изменить параметры таблицы счетчик** модуля.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="2fdf2-341">Этот модуль показан для полноты информации, но в целях упрощения в данном эксперименте он фактически не используется.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Modify Count Table Parameters (Изменение параметров таблицы счетчиков)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="2fdf2-343">Таким образом как можно увидеть, мы выбрали toouse вероятность журнала просто hello и tooignore hello пассивный режим столбца.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="2fdf2-344">Мы также можно настроить параметры, например пороговое значение контейнера для сборки мусора hello, сколько tooadd псевдослучайных предыдущие примеры для сглаживания, и ли toouse любой Лапласа помех или нет.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="2fdf2-345">Все эти — это дополнительные возможности и что toobe целый значения по умолчанию hello хорошей отправной точкой для пользователей, имеющих возможность создания нового типа toothis.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="2fdf2-346">Преобразование данных перед созданием функции count hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="2fdf2-347">Теперь мы сосредоточить внимание на важное правило о преобразовании нашей обучение и проверить данные предыдущих tooactually создания функции count.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="2fdf2-348">Обратите внимание, что два **выполнение скрипта R** модули, используемые, прежде чем мы применить преобразование tooour hello количество данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![Модули "Выполнить сценарий R"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="2fdf2-350">Вот первый сценарий R hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-350">Here is hello first R script:</span></span>

![Первый сценарий R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="2fdf2-352">В этом сценарии R переименуем нашей toonames столбцы «Col1» слишком «Col40».</span><span class="sxs-lookup"><span data-stu-id="2fdf2-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="2fdf2-353">Это так, как преобразование числа hello ожидает имена этого формата.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="2fdf2-354">В hello второй скрипт R, мы распределить hello распространения между классами положительные и отрицательные (классы 1 и 0 соответственно) с отрицательным класса понижение hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="2fdf2-355">Hello R сценарии здесь показано, как toodo это:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-355">hello R script here shows how toodo this:</span></span>

![Второй сценарий R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="2fdf2-357">В этой простой сценарий R, мы используем «pos\_neg\_отношение» tooset hello объем баланс между hello положительные и отрицательные классы hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="2fdf2-358">Это важно, что toodo, поскольку улучшение дисбаланс класс обычно дает преимущества в производительности для проблем классификации, где распространения класс hello синхронизована (Напомним, что в нашем случае у нас есть положительные и отрицательные класса 96.7% 3.3%).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="2fdf2-359">Применение преобразования числа hello с нашими данными</span><span class="sxs-lookup"><span data-stu-id="2fdf2-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="2fdf2-360">Наконец, мы используем hello **применение преобразования** tooapply модуль hello число преобразований на нашем обучения и проверочных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="2fdf2-361">Этот модуль принимает преобразования числа hello сохранен как один вход и hello обучения или тестирования наборы данных, как hello другие входные данные и возвращает данные с помощью функции count.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="2fdf2-362">Вот как это работает:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-362">It is shown here:</span></span>

![Модуль применения преобразования](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="2fdf2-364">Фрагмент кода как выглядеть функции count hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="2fdf2-365">Бывает полезным toosee, какие функции count hello выглядеть в нашем случае.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="2fdf2-366">Вот его фрагмент:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-366">Here we show an excerpt of this:</span></span>

![Функции счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="2fdf2-368">В данном отрывке Далее показано, что для hello столбцов, которые мы подсчитаны, мы получить количество hello вход шансов соответствующие backoffs tooany сложения.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="2fdf2-369">Мы стали готовы toobuild модель машинного обучения Azure, используя эти преобразованный наборы данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="2fdf2-370">В следующем разделе hello показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="2fdf2-371"><a name="step3"></a>Шаг 3: Построение, обучения и оценка модели hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="2fdf2-372">Выбор ученика</span><span class="sxs-lookup"><span data-stu-id="2fdf2-372">Choice of learner</span></span>
<span data-ttu-id="2fdf2-373">Во-первых мы должны toochoose ученика.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="2fdf2-374">Как наш ученик не будет toouse два класса повышенного дерева принятия решений.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="2fdf2-375">Ниже приведены параметры по умолчанию hello для этого ученика.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-375">Here are hello default options for this learner:</span></span>

![Параметры двухклассового увеличивающегося дерева принятия решений](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="2fdf2-377">В нашем эксперименте не значения по умолчанию hello toochoose постоянной.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="2fdf2-378">Мы Обратите внимание, что значения по умолчанию, hello, являются обычно значимые и удобным способом tooget быстрого базовых показателей производительности.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="2fdf2-379">На производительность можно повысить, широкими параметры при выборе tooonce вами базового плана.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="2fdf2-380">Обучение модели hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-380">Train hello model</span></span>
<span data-ttu-id="2fdf2-381">Для обучения мы просто вызовем модуль **Обучение модели** .</span><span class="sxs-lookup"><span data-stu-id="2fdf2-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="2fdf2-382">два входных данных tooit Hello: hello ученик Двухклассового повышенного дерева принятия решений и наши обучающего набора данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="2fdf2-383">Вот как это работает:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-383">This is shown here:</span></span>

![Модуль "Обучение модели"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="2fdf2-385">Модель оценки hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-385">Score hello model</span></span>
<span data-ttu-id="2fdf2-386">После обучения модели, мы готовы tooscore на hello проверки набора данных и tooevaluate его производительности.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="2fdf2-387">Это делается с помощью hello **модель оценки** показано hello следующий рисунок, вместе с модулем **модель оценки** модуля:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![Модуль "Оценка модели"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="2fdf2-389"><a name="step4"></a>Шаг 4: Оценка модели hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="2fdf2-390">Наконец мы хотели бы tooanalyze модели производительности.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="2fdf2-391">Как правило для проблем классификации (двоичный) двух классов, хорошей мерой — hello AUC.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="2fdf2-392">toovisualize это, мы подключить hello **модель оценки** tooan модуль **модель оценки** модуля для этого.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="2fdf2-393">Щелкнув **визуализировать** на hello **модель оценки** модуль создает график как hello, выполнив одно:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Модуль «Анализ модели» и «Увеличивающееся дерево принятия решений»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="2fdf2-395">В двоичный файл (или два класса) проблем классификации, хорошо степень точности прогнозов является hello области под кривой (AUC).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="2fdf2-396">Ниже будут показаны результаты использования этой модели на основе нашего тестового набора данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="2fdf2-397">tooget это, щелкните правой кнопкой мыши порт вывода hello hello **модель оценки** модуля и затем **визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Визуализация модуля «Анализ модели»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="2fdf2-399"><a name="step5"></a>Шаг 5: Публикация hello модели веб-службы</span><span class="sxs-lookup"><span data-stu-id="2fdf2-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="2fdf2-400">возможность Hello toopublish модель машинного обучения Azure как веб-службы с минимальными усилиями ценные функция для создания широко доступны.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="2fdf2-401">После этого, любой пользователь может создать вызовы toohello веб-службы с входными данными, они должны прогнозы для, что hello веб-служба использует модель tooreturn hello этих прогнозов.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="2fdf2-402">toodo это, мы сначала сохраните нашей обученной модели в виде обученной модели объекта.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="2fdf2-403">Это можно сделать, щелкнув правой кнопкой мыши hello **Обучение модели** модуль и с помощью hello **Сохранить как Обученную модель** параметр.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="2fdf2-404">Теперь нам нужны toocreate ввод и вывод портов для веб-узле службы:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="2fdf2-405">порта ввода принимает данные в hello же форму как hello данные, необходимые для прогнозы</span><span class="sxs-lookup"><span data-stu-id="2fdf2-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="2fdf2-406">порт вывода возвращает связанные hello вероятности и метки оцененных hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="2fdf2-407">Выберите несколько строк данных для входного порта hello</span><span class="sxs-lookup"><span data-stu-id="2fdf2-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="2fdf2-408">Это удобный toouse **применение преобразования SQL** tooserve модуль tooselect только 10 строк, как hello входные данные порт.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="2fdf2-409">Выберите только этих строк данных для наших входного порта с помощью запроса SQL hello, показано ниже:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![Данные порта ввода](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="2fdf2-411">Веб-служба</span><span class="sxs-lookup"><span data-stu-id="2fdf2-411">Web service</span></span>
<span data-ttu-id="2fdf2-412">Теперь мы готовы toorun небольшой эксперимент, который можно использовать toopublish веб-узле службы.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="2fdf2-413">Создание входных данных для веб-службы</span><span class="sxs-lookup"><span data-stu-id="2fdf2-413">Generate input data for webservice</span></span>
<span data-ttu-id="2fdf2-414">В качестве шага нулевого поскольку таблицы счетчиков hello велик, мы занять всего несколько строк данных теста и создавать выходные данные из них с помощью функции count.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="2fdf2-415">Это может служить форматом hello входные данные для наших веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="2fdf2-416">Вот как это работает:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-416">This is shown here:</span></span>

![Создание входных данных модуля «Увеличивающееся дерево принятия решений»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="2fdf2-418">Формат входных данных hello, теперь мы используем hello выходные данные hello **Характеризатора** модуля.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="2fdf2-419">После завершения это поэкспериментировать, сохранить выходные данные hello из hello **Характеризатора** модуль в качестве набора данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="2fdf2-420">Этот набор данных будет использоваться для hello входных данных в hello webservice.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="2fdf2-421">Оценка эксперимента для публикации веб-службы</span><span class="sxs-lookup"><span data-stu-id="2fdf2-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="2fdf2-422">Сначала мы покажем, как это выглядит.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-422">First, we show what this looks like.</span></span> <span data-ttu-id="2fdf2-423">Структура essential Hello **модель оценки** модуля, который принимает объект нашей обученной модели и несколько строк входных данных, мы создали на предыдущих шагах hello, с помощью hello **Характеризатора** модуля.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="2fdf2-424">Мы используем tooproject «Выберите столбцы в наборе данных» hello Оцененный метки и Оценка вероятности hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![Выбор столбцов в наборе данных](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="2fdf2-426">Обратите внимание, каким образом hello **Выбор столбцов в наборе данных** модуль можно использовать для «фильтрации» данные из набора данных.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="2fdf2-427">Мы Показать содержимое hello здесь:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-427">We show hello contents here:</span></span>

![Фильтрация с помощью hello Выбор столбцов в модуле набора данных](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="2fdf2-429">порты tooget hello синий входных и выходных данных, нужно просто щелкнуть **Подготовка веб-службы** внизу hello справа.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="2fdf2-430">Запуск этого эксперимента также позволяет нам toopublish hello веб-службы: щелкните hello **публикации веб-службы** значок hello нижней правой, показанный здесь:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![Publish web service](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="2fdf2-432">После публикации веб-службы hello мы получаем перенаправленный tooa страницу, которая выглядит таким образом:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Панель мониторинга веб-службы](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="2fdf2-434">В левой части hello видно две ссылки для веб-службы:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="2fdf2-435">Hello **запрос-ОТВЕТ** службы (или записи Ресурсов) предназначена для единичные прогнозы и будет использовать в этом цеху.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="2fdf2-436">Hello **ПАКЕТНОЕ выполнение** службы (BES) используется для пакетных прогнозов и требует наличия, прогнозы toomake hello входные данные находились в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="2fdf2-437">Щелкнув ссылку hello **запрос-ОТВЕТ** отсылает tooa страницы, которая дает нам предустановленных кода на C#, python и R. Этот код можно использовать для создания веб-службы toohello вызовы удобным образом.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="2fdf2-438">Обратите внимание, что hello ключ API на этой странице требуется toobe, используемый для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="2fdf2-439">Это удобный toocopy этот python code через tooa новую ячейку в записной книжке IPython hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="2fdf2-440">Здесь показано сегмент кода python, с hello правильный ключ API.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-440">Here we show a segment of python code with hello correct API key.</span></span>

![Код Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="2fdf2-442">Обратите внимание, что мы заменены ключ API по умолчанию hello ключ API наш веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="2fdf2-443">Щелкнув **запуска** в данную ячейку в IPython записной книжки дает hello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="2fdf2-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![Ответ iPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="2fdf2-445">Мы видим, что для hello двух тестовых примеры, которые мы спросили (в framework JSON hello hello сценария python), мы получаем ответы в форме hello «Оцененный метки, Оцененный вероятности».</span><span class="sxs-lookup"><span data-stu-id="2fdf2-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="2fdf2-446">Обратите внимание, что в этом случае мы выбрали значения по умолчанию hello предустановленных кода hello предоставляет (0 для всех числовых столбцов и строку hello «значение» для всех категориальных столбцов).</span><span class="sxs-lookup"><span data-stu-id="2fdf2-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="2fdf2-447">Это заключительный шаг нашей отображение Пошаговое руководство с начала до конца как toohandle крупномасштабных набора данных, с помощью машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="2fdf2-448">Мы начали с терабайт данных, создается модель прогнозирования и развернуть его как веб-службы в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="2fdf2-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

