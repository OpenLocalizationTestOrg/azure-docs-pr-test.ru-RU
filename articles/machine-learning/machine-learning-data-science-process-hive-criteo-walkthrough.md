---
title: "Процесс обработки и анализа данных группы на практике: использование кластера Azure HDInsight Hadoop с набором данных объемом 1 ТБ | Документация Майкрософт"
description: "Применение процесса обработки и анализа данных группы в комплексном сценарии, включающем в себя использование кластера HDInsight Hadoop для создания и развертывания модели на основе общедоступного набора данных большого объема (1 ТБ)."
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
ms.openlocfilehash: 8e6143bca819c9a0484221f8b4feb319aaaa73f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="2702f-103">Процесс обработки и анализа данных группы на практике: использование кластера Azure HDInsight Hadoop с набором данных объемом 1 ТБ</span><span class="sxs-lookup"><span data-stu-id="2702f-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="2702f-104">В этом пошаговом руководстве показан комплексный сценарий использования процесса обработки и анализа данных группы на примере [кластера Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) для хранения, изучения, проектирование признаков и снижения частоты выборки данных в одном из общедоступных наборов данных [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="2702f-104">In this walkthrough, we demonstrate using the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="2702f-105">Мы построим модель двоичной классификации этих данных, используя машинное обучение Azure,</span><span class="sxs-lookup"><span data-stu-id="2702f-105">We use Azure Machine Learning to build a binary classification model on this data.</span></span> <span data-ttu-id="2702f-106">и покажем, как опубликовать одну из этих моделей в качестве веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2702f-106">We also show how to publish one of these models as a Web service.</span></span>

<span data-ttu-id="2702f-107">Для выполнения заданий, представленных в этом пошаговом руководстве, можно также использовать iPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="2702f-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span></span> <span data-ttu-id="2702f-108">Пользователям, которые хотят применить этот подход, следует просмотреть статью [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) (Пошаговое руководство Criteo по использованию подключения Hive ODBC).</span><span class="sxs-lookup"><span data-stu-id="2702f-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="2702f-109"><a name="dataset"></a>Описание набора данных Criteo</span><span class="sxs-lookup"><span data-stu-id="2702f-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="2702f-110">Данные Criteo представляют собой набор данных для прогнозирования переходов по рекламным объявлениям, который содержит приблизительно 370 ГБ TSV-файлов, сжатых с помощью служебной программы gzip (около 1,3 TБ без сжатия), что составляет 4,3 миллиарда записей.</span><span class="sxs-lookup"><span data-stu-id="2702f-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="2702f-111">Эти данные получены на основе данных о переходах по ссылкам за 24 дня, предоставленных [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="2702f-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="2702f-112">Для удобства специалистов по обработке и анализу данных мы разархивировали данные, доступные для экспериментирования.</span><span class="sxs-lookup"><span data-stu-id="2702f-112">For the convenience of data scientists, we have unzipped data available to us to experiment with.</span></span>

<span data-ttu-id="2702f-113">Каждая запись в этом наборе данных содержит 40 столбцов:</span><span class="sxs-lookup"><span data-stu-id="2702f-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="2702f-114">первый столбец — столбец с меткой, указывающий, щелкнул пользователь **рекламное объявление** (значение 1) или не щелкнул (значение 0);</span><span class="sxs-lookup"><span data-stu-id="2702f-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="2702f-115">следующие 13 столбцов являются числовыми;</span><span class="sxs-lookup"><span data-stu-id="2702f-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="2702f-116">последние 26 столбцов категориальные.</span><span class="sxs-lookup"><span data-stu-id="2702f-116">last 26 are categorical columns</span></span>

<span data-ttu-id="2702f-117">Столбцы являются анонимными, и в них используется ряд перечисляемых имен — от Col1 (столбец с меткой) до Col40 (последний категориальный столбец).</span><span class="sxs-lookup"><span data-stu-id="2702f-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span></span>            

<span data-ttu-id="2702f-118">Ниже приведен фрагмент первых 20 столбцов из двух наблюдений (строк) этого набора данных:</span><span class="sxs-lookup"><span data-stu-id="2702f-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="2702f-119">В этом наборе данных как в числовых столбцах, так и в категориальных столбцах есть недостающие значения.</span><span class="sxs-lookup"><span data-stu-id="2702f-119">There are missing values in both the numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="2702f-120">Ниже приведен простой способ обработки недостающих значений.</span><span class="sxs-lookup"><span data-stu-id="2702f-120">We describe a simple method for handling the missing values.</span></span> <span data-ttu-id="2702f-121">Дополнительные сведения о данных предоставляются на этапе их сохранения в таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="2702f-121">Additional details of the data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="2702f-122">**Определение.** *Коэффициент выбора рекламного объявления* — это процент выбора элементов путем щелчка в данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span></span> <span data-ttu-id="2702f-123">В этом наборе Criteo коэффициент составляет около 3,3 % или 0,033.</span><span class="sxs-lookup"><span data-stu-id="2702f-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="2702f-124"><a name="mltasks"></a>Примеры задач прогнозирования</span><span class="sxs-lookup"><span data-stu-id="2702f-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="2702f-125">В этом пошаговом руководстве рассмотрены два примера задач по прогнозированию:</span><span class="sxs-lookup"><span data-stu-id="2702f-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="2702f-126">**Двоичная классификация**— прогнозирует, щелкнет ли пользователь рекламное объявление:</span><span class="sxs-lookup"><span data-stu-id="2702f-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="2702f-127">класс 0 — не щелкнул;</span><span class="sxs-lookup"><span data-stu-id="2702f-127">Class 0: No Click</span></span>
   * <span data-ttu-id="2702f-128">класс 1 — щелкнул.</span><span class="sxs-lookup"><span data-stu-id="2702f-128">Class 1: Click</span></span>
2. <span data-ttu-id="2702f-129">**Регрессия**— прогнозирует вероятность щелчка рекламного объявления по признакам пользователя.</span><span class="sxs-lookup"><span data-stu-id="2702f-129">**Regression**: Predicts the probability of an ad click from user features.</span></span>

## <span data-ttu-id="2702f-130"><a name="setup"></a>Настройка кластера HDInsight Hadoop для обработки и анализа данных</span><span class="sxs-lookup"><span data-stu-id="2702f-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="2702f-131">**Примечание.** Эту задачу обычно выполняет **администратор**.</span><span class="sxs-lookup"><span data-stu-id="2702f-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="2702f-132">Настройте среду обработки и анализа данных Azure, чтобы создавать решения для прогнозной аналитики с помощью кластеров HDInsight, выполнив три шага:</span><span class="sxs-lookup"><span data-stu-id="2702f-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="2702f-133">[Создание учетной записи хранения.](../storage/common/storage-create-storage-account.md) Эта учетная запись хранения используется для хранения данных в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used to store data in Azure Blob Storage.</span></span> <span data-ttu-id="2702f-134">Здесь хранятся данные, используемые в кластерах HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2702f-134">The data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="2702f-135">[Настройка кластеров Azure HDInsight Hadoop для обработки и анализа данных.](machine-learning-data-science-customize-hadoop-cluster.md) На этом шаге создается кластер Azure HDInsight Hadoop и на всех узлах устанавливается 64-разрядный дистрибутив Anaconda Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="2702f-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="2702f-136">При настройке кластера HDInsight следует выполнить два важных шага (описанных в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="2702f-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span></span>
   
   * <span data-ttu-id="2702f-137">Во время создания кластера HDInsight необходимо связать учетную запись хранения, созданную на шаге 1, с этим кластером.</span><span class="sxs-lookup"><span data-stu-id="2702f-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="2702f-138">Эта учетная запись хранения используется для доступа к данным, которые можно обработать в пределах кластера.</span><span class="sxs-lookup"><span data-stu-id="2702f-138">This storage account is used for accessing data that can be processed within the cluster.</span></span>
   * <span data-ttu-id="2702f-139">После создания кластера необходимо включить удаленный доступ к головному узлу кластера.</span><span class="sxs-lookup"><span data-stu-id="2702f-139">You must enable Remote Access to the head node of the cluster after it is created.</span></span> <span data-ttu-id="2702f-140">Запомните указываемые здесь учетные данные для удаленного доступа (не те, которые были заданы при создании кластера), так как они потребуются для выполнения следующих действий.</span><span class="sxs-lookup"><span data-stu-id="2702f-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span></span>
3. <span data-ttu-id="2702f-141">[Создание рабочей области Машинного обучения Azure.](machine-learning-create-workspace.md) Эта рабочая область машинного обучения Azure используется для создания моделей машинного обучения после просмотра исходных данных и снижения частоты выборки в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2702f-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span></span>

## <span data-ttu-id="2702f-142"><a name="getdata"></a>Получение и использование данных из общедоступного источника</span><span class="sxs-lookup"><span data-stu-id="2702f-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="2702f-143">Доступ к набору данных [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) можно получить, щелкнув ссылку, приняв условия использования и указав имя.</span><span class="sxs-lookup"><span data-stu-id="2702f-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span></span> <span data-ttu-id="2702f-144">Ниже показан снимок того, как это выглядит.</span><span class="sxs-lookup"><span data-stu-id="2702f-144">A snapshot of what this looks like is shown here:</span></span>

![Принятие условий использования Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="2702f-146">Нажмите кнопку **Continue to Download** (Продолжить для скачивания), чтобы ознакомиться с дополнительными сведениями о наборе данных и его доступности.</span><span class="sxs-lookup"><span data-stu-id="2702f-146">Click **Continue to Download** to read more about the dataset and its availability.</span></span>

<span data-ttu-id="2702f-147">Данные находятся в расположении общедоступного [хранилище BLOB-объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md): wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="2702f-147">The data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="2702f-148">wasb относится к расположению хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-148">The "wasb" refers to Azure Blob Storage location.</span></span> 

1. <span data-ttu-id="2702f-149">Данные в этом общедоступном хранилище BLOB-объектов содержатся в трех вложенных папках с разархивированными данными.</span><span class="sxs-lookup"><span data-stu-id="2702f-149">The data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="2702f-150">Вложенная папка *raw/count/* содержит данные за первые 21 день — от day\_00 до day\_20.</span><span class="sxs-lookup"><span data-stu-id="2702f-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span></span>
   2. <span data-ttu-id="2702f-151">Вложенная папка *raw/train/* содержит данные за один день — day\_21.</span><span class="sxs-lookup"><span data-stu-id="2702f-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="2702f-152">Вложенная папка *raw/test/* содержит данные за два дня — day\_22 и day\_23.</span><span class="sxs-lookup"><span data-stu-id="2702f-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="2702f-153">Для тех, кому требуется начать с необработанных данных gzip, эти данные также доступны в главной папке *raw/* в виде day_NN.gz, где значение NN указано в диапазоне от 00 до 23.</span><span class="sxs-lookup"><span data-stu-id="2702f-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span></span>

<span data-ttu-id="2702f-154">Альтернативный способ получения доступа к этим данным, их просмотра и моделирования, который не требует скачивания локальных файлов, описан далее в этом пошаговом руководстве на этапе создания таблиц Hive.</span><span class="sxs-lookup"><span data-stu-id="2702f-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="2702f-155"><a name="login"></a>Вход в головной узел кластера</span><span class="sxs-lookup"><span data-stu-id="2702f-155"><a name="login"></a>Log in to the cluster headnode</span></span>
<span data-ttu-id="2702f-156">Чтобы войти в головной узел кластера, узнайте его расположение, используя [портал Azure](https://ms.portal.azure.com) .</span><span class="sxs-lookup"><span data-stu-id="2702f-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span></span> <span data-ttu-id="2702f-157">Щелкните значок HDInsight в виде слона в левой части портала, а затем дважды щелкните имя кластера.</span><span class="sxs-lookup"><span data-stu-id="2702f-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span></span> <span data-ttu-id="2702f-158">Перейдите на вкладку **Конфигурация** , дважды щелкните значок "Подключение" в нижней части страницы и при появлении запроса введите учетные данные для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="2702f-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="2702f-159">Таким образом вы перейдете к головному узлу кластера.</span><span class="sxs-lookup"><span data-stu-id="2702f-159">This takes you to the headnode of the cluster.</span></span>

<span data-ttu-id="2702f-160">Вот как выглядит экран при типичном первом входе в головной узел кластера:</span><span class="sxs-lookup"><span data-stu-id="2702f-160">Here is what a typical first log in to the cluster headnode looks like:</span></span>

![Вход в кластер](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="2702f-162">В левой части виден значок "Командная строка Hadoop". С помощью этой строки выполняется просмотр данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-162">On the left, we see the "Hadoop Command Line", which is our workhorse for the data exploration.</span></span> <span data-ttu-id="2702f-163">На экране также отображаются два полезных URL-адреса — «Состояние Hadoop Yarn» и «Узел имен Hadoop».</span><span class="sxs-lookup"><span data-stu-id="2702f-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="2702f-164">URL-адрес состояния Yarn показывает ход выполнения задания, а URL-адрес узла имен предоставляет дополнительную информацию о конфигурации кластера.</span><span class="sxs-lookup"><span data-stu-id="2702f-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span></span>

<span data-ttu-id="2702f-165">Теперь все готово для начала первой части пошагового руководства — просмотр данных с помощью Hive и подготовка данных для машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-165">Now we are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="2702f-166"><a name="hive-db-tables"></a> Создание базы данных и таблиц Hive</span><span class="sxs-lookup"><span data-stu-id="2702f-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="2702f-167">Чтобы создать таблицы Hive для нашего набора данных Criteo, откройте ***командную строку Hadoop*** на рабочем столе головного узла и введите имя каталога Hive с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="2702f-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="2702f-168">Выполняйте все команды Hive в этом пошаговом руководстве из командной строки каталога bin/ Hive.</span><span class="sxs-lookup"><span data-stu-id="2702f-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="2702f-169">Таким образом вы сможете автоматически избежать любых проблем с путем.</span><span class="sxs-lookup"><span data-stu-id="2702f-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="2702f-170">Термины "командная строка каталога Hive", "командная строка каталога bin/ Hive" и "командная строка Hadoop" будут использоваться на взаимозаменяемой основе.</span><span class="sxs-lookup"><span data-stu-id="2702f-170">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="2702f-171">Любой запрос Hive всегда можно выполнить с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="2702f-171">To execute any Hive query, one can always use the following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="2702f-172">После появления командной строки Hive REPL с символом hive > просто скопируйте и вставьте запрос, чтобы выполнить его.</span><span class="sxs-lookup"><span data-stu-id="2702f-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span></span>

<span data-ttu-id="2702f-173">Код ниже создает базу данных criteo, а затем — 4 таблицы:</span><span class="sxs-lookup"><span data-stu-id="2702f-173">The following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="2702f-174">*таблицу для создания счетчиков*, созданную для дней с day\_00 до day\_20;</span><span class="sxs-lookup"><span data-stu-id="2702f-174">a *table for generating counts* built on days day\_00 to day\_20,</span></span>
* <span data-ttu-id="2702f-175">*таблицу для использования в качестве набора данных*, созданную для дня day\_21;</span><span class="sxs-lookup"><span data-stu-id="2702f-175">a *table for use as the train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="2702f-176">две *таблицы для использования в качестве наборов данных теста*, созданные для дней day\_22 и day\_23 соответственно.</span><span class="sxs-lookup"><span data-stu-id="2702f-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="2702f-177">Тестовый набор данных был разделен на две разные таблицы, так как один из дней — праздник, и необходимо определить, может ли модель определить разницу между праздником и другим днем по коэффициенту выбора рекламного объявления.</span><span class="sxs-lookup"><span data-stu-id="2702f-177">We split our test dataset into two different tables because one of the days is a holiday, and we want to determine if the model can detect differences between a holiday and non-holiday from the clickthrough rate.</span></span>

<span data-ttu-id="2702f-178">Ниже для удобства приведен скрипт [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-178">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

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

<span data-ttu-id="2702f-179">Мы обратили внимание, что все эти таблицы являются внешними, так как были просто указаны расположения (wasb) хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-179">We note that all these tables are external as we simply point to Azure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="2702f-180">**ЛЮБОЙ запрос Hive, указанный ниже, можно выполнить двумя способами:**</span><span class="sxs-lookup"><span data-stu-id="2702f-180">**There are two ways to execute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="2702f-181">**Использование командной строки Hive REPL.** Первый способ — выполнить команду hive, а затем скопировать и вставить запрос в командную строку Hive REPL.</span><span class="sxs-lookup"><span data-stu-id="2702f-181">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span></span> <span data-ttu-id="2702f-182">Для этого введите следующее:</span><span class="sxs-lookup"><span data-stu-id="2702f-182">To do this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="2702f-183">Если скопировать и вставить запрос в командную строку REPL, он начнет выполняться.</span><span class="sxs-lookup"><span data-stu-id="2702f-183">Now at the REPL command-line, cutting and pasting the query executes it.</span></span>
2. <span data-ttu-id="2702f-184">**Сохранение запросов в файл и выполнение команды.** Второй способ — сохранить запросы в HQL-файл ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)), а затем выполнить следующую команду для отправки запроса:</span><span class="sxs-lookup"><span data-stu-id="2702f-184">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="2702f-185">Подтверждение создания базы данных и таблицы</span><span class="sxs-lookup"><span data-stu-id="2702f-185">Confirm database and table creation</span></span>
<span data-ttu-id="2702f-186">Далее мы подтвердим создание базы данных, выполнив команду ниже в командной строке каталога bin/ Hive.</span><span class="sxs-lookup"><span data-stu-id="2702f-186">Next, we confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="2702f-187">Результат выполнения команды:</span><span class="sxs-lookup"><span data-stu-id="2702f-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="2702f-188">Таким образом подтверждается создание новой базы данных criteo.</span><span class="sxs-lookup"><span data-stu-id="2702f-188">This confirms the creation of the new database, "criteo".</span></span>

<span data-ttu-id="2702f-189">Чтобы увидеть, какие таблицы были созданы, нужно просто выполнить команду в командной строке каталога bin/ Hive.</span><span class="sxs-lookup"><span data-stu-id="2702f-189">To see what tables we created, we simply issue the command here from the Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="2702f-190">Вы увидите следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="2702f-190">We then see the following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="2702f-191"><a name="exploration"></a> Просмотр данных в Hive</span><span class="sxs-lookup"><span data-stu-id="2702f-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="2702f-192">Теперь можно приступить к базовому просмотру данных в Hive.</span><span class="sxs-lookup"><span data-stu-id="2702f-192">Now we are ready to do some basic data exploration in Hive.</span></span> <span data-ttu-id="2702f-193">Мы начнем с подсчета примеров в таблицах данных для обучения и тестирования.</span><span class="sxs-lookup"><span data-stu-id="2702f-193">We begin by counting the number of examples in the train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="2702f-194">Количество примеров для обучения</span><span class="sxs-lookup"><span data-stu-id="2702f-194">Number of train examples</span></span>
<span data-ttu-id="2702f-195">Ниже показано содержимое скрипта [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-195">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="2702f-196">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="2702f-197">Кроме того, в командной строке каталога bin/ Hive можно выполнить следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2702f-197">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-the-two-test-datasets"></a><span data-ttu-id="2702f-198">Количество тестовых примеров в двух тестовых наборах данных</span><span class="sxs-lookup"><span data-stu-id="2702f-198">Number of test examples in the two test datasets</span></span>
<span data-ttu-id="2702f-199">Теперь нужно подсчитать количество примеров в двух тестовых наборах данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-199">We now count the number of examples in the two test datasets.</span></span> <span data-ttu-id="2702f-200">Ниже показано содержимое скрипта [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-200">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="2702f-201">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="2702f-202">Как правило, можно также вызвать скрипт в командной строке каталога bin/ Hive, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2702f-202">As usual, we may also call the script from the Hive bin/ directory prompt by issuing the command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="2702f-203">Наконец, мы просмотрим количество тестовых примеров в тестовом наборе данных на основе показателя day\_23.</span><span class="sxs-lookup"><span data-stu-id="2702f-203">Finally, we examine the number of test examples in the test dataset based on day\_23.</span></span>

<span data-ttu-id="2702f-204">Команда для выполнения этого действия похожа на команду выше (см. [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)).</span><span class="sxs-lookup"><span data-stu-id="2702f-204">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="2702f-205">Результат выполнения команды:</span><span class="sxs-lookup"><span data-stu-id="2702f-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-the-train-dataset"></a><span data-ttu-id="2702f-206">Распределение меток в наборе данных для обучения</span><span class="sxs-lookup"><span data-stu-id="2702f-206">Label distribution in the train dataset</span></span>
<span data-ttu-id="2702f-207">Необходимо определить распределение меток в наборе данных для обучения.</span><span class="sxs-lookup"><span data-stu-id="2702f-207">The label distribution in the train dataset is of interest.</span></span> <span data-ttu-id="2702f-208">Чтобы увидеть его, мы покажем содержимое скрипта [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-208">To see this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="2702f-209">Мы получаем такое распределение меток:</span><span class="sxs-lookup"><span data-stu-id="2702f-209">This yields the label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="2702f-210">Обратите внимание, что доля положительных меток составляет около 3,3 % (в соответствии с исходным набором данных).</span><span class="sxs-lookup"><span data-stu-id="2702f-210">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="2702f-211">Распределения гистограммы некоторых числовых переменных в наборе данных для обучения</span><span class="sxs-lookup"><span data-stu-id="2702f-211">Histogram distributions of some numeric variables in the train dataset</span></span>
<span data-ttu-id="2702f-212">Чтобы узнать, как выглядит распределение числовых переменных, можно использовать функцию Hive histogram\_numeric.</span><span class="sxs-lookup"><span data-stu-id="2702f-212">We can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span></span> <span data-ttu-id="2702f-213">Ниже представлено содержимое скрипта [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-213">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="2702f-214">Мы получаем следующий результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-214">This yields the following:</span></span>

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

<span data-ttu-id="2702f-215">Сочетание параметров LATERAL VIEW и explode в Hive служит для вывода выходных данных, подобных SQL, вместо обычного списка.</span><span class="sxs-lookup"><span data-stu-id="2702f-215">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span></span> <span data-ttu-id="2702f-216">Обратите внимание, что в этой таблице первый столбец соответствует центру каталога bin, а второй — его частоте.</span><span class="sxs-lookup"><span data-stu-id="2702f-216">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="2702f-217">Приблизительные процентили для некоторых числовых переменных в наборе данных для обучения</span><span class="sxs-lookup"><span data-stu-id="2702f-217">Approximate percentiles of some numeric variables in the train dataset</span></span>
<span data-ttu-id="2702f-218">Кроме того, нам необходимо вычислить приблизительные процентили для числовых переменных.</span><span class="sxs-lookup"><span data-stu-id="2702f-218">Also of interest with numeric variables is the computation of approximate percentiles.</span></span> <span data-ttu-id="2702f-219">Функция Hive percentile\_approx делает это автоматически.</span><span class="sxs-lookup"><span data-stu-id="2702f-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="2702f-220">Ниже представлено содержимое скрипта [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-220">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="2702f-221">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="2702f-222">Обратите внимание, что обычно распределение процентилей тесно связано с распределением гистограммы для любой числовой переменной.</span><span class="sxs-lookup"><span data-stu-id="2702f-222">We remark that the distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-the-train-dataset"></a><span data-ttu-id="2702f-223">Поиск количества уникальных значений для некоторых категориальных столбцов в наборе данных для обучения</span><span class="sxs-lookup"><span data-stu-id="2702f-223">Find number of unique values for some categorical columns in the train dataset</span></span>
<span data-ttu-id="2702f-224">Мы продолжаем просматривать данные, и теперь нам нужно найти количество уникальных значений, принимаемых некоторыми категориальными столбцами.</span><span class="sxs-lookup"><span data-stu-id="2702f-224">Continuing the data exploration, we now find, for some categorical columns, the number of unique values they take.</span></span> <span data-ttu-id="2702f-225">Для этого следует показать содержимое скрипта [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-225">To do this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="2702f-226">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="2702f-227">Обратите внимание, что в столбце Col15 найдено 19 млн. уникальных значений!</span><span class="sxs-lookup"><span data-stu-id="2702f-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="2702f-228">Невозможно кодировать такие многомерные категориальные переменные с помощью таких упрощенных методов, как «прямое кодирование».</span><span class="sxs-lookup"><span data-stu-id="2702f-228">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="2702f-229">Для эффективного решения этой проблемы объясняется и демонстрируется эффективный и надежный метод, называемый [обучение с использованием счетчиков](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx).</span><span class="sxs-lookup"><span data-stu-id="2702f-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="2702f-230">Этот подраздел завершается просмотром количества уникальных значений для других категориальных столбцов.</span><span class="sxs-lookup"><span data-stu-id="2702f-230">We end this sub-section by looking at the number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="2702f-231">Ниже приведено содержимое скрипта [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-231">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="2702f-232">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="2702f-233">И снова видно, что во всех столбцах, за исключением Col20, содержится много уникальных значений.</span><span class="sxs-lookup"><span data-stu-id="2702f-233">Again we see that except for Col20, all the other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-the-train-dataset"></a><span data-ttu-id="2702f-234">Подсчет совместного вхождения пар категориальных переменных в наборе данных для обучения</span><span class="sxs-lookup"><span data-stu-id="2702f-234">Co-occurrence counts of pairs of categorical variables in the train dataset</span></span>

<span data-ttu-id="2702f-235">Необходимо подсчитать совместное вхождение пар категориальных переменных.</span><span class="sxs-lookup"><span data-stu-id="2702f-235">The co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="2702f-236">Это можно определить с помощью кода в скрипте [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="2702f-236">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="2702f-237">В этом случае количество приведено в обратном порядке по порядку вхождения и рассмотрено 15 первых значений.</span><span class="sxs-lookup"><span data-stu-id="2702f-237">We reverse order the counts by their occurrence and look at the top 15 in this case.</span></span> <span data-ttu-id="2702f-238">Результат выполнения команды:</span><span class="sxs-lookup"><span data-stu-id="2702f-238">This gives us:</span></span>

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

## <span data-ttu-id="2702f-239"><a name="downsample"></a> Снижение частоты выборки в наборе данных для Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="2702f-239"><a name="downsample"></a> Down sample the datasets for Azure Machine Learning</span></span>
<span data-ttu-id="2702f-240">После просмотра наборов данных и демонстрации того, как можно выполнить этот тип просмотра для любых переменных (включая сочетания переменных), мы приступим к снижению частоты выборки в наборах данных для создания моделей в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-240">Having explored the datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample the data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="2702f-241">Помните, что рассматривается следующая задача: при заданном наборе примеров атрибутов (значений признаков от Col2 до Col40) нужно спрогнозировать, какое значение примет Col1 — 0 (без щелчка) или 1 (щелчок).</span><span class="sxs-lookup"><span data-stu-id="2702f-241">Recall that the problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="2702f-242">Чтобы снизить частоту выборки в наших наборах данных для обучения и тестовых наборах данных до 1 % от исходного размера, будет использована функция Hive RAND().</span><span class="sxs-lookup"><span data-stu-id="2702f-242">To down sample our train and test datasets to 1% of the original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="2702f-243">Следующий скрипт [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) выполняет это действие для набора данных для обучения:</span><span class="sxs-lookup"><span data-stu-id="2702f-243">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="2702f-244">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="2702f-245">Скрипт [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) выполняет это действие для тестовых данных за день day\_22:</span><span class="sxs-lookup"><span data-stu-id="2702f-245">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="2702f-246">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="2702f-247">Скрипт [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) выполняет это действие для тестовых данных за день day\_23:</span><span class="sxs-lookup"><span data-stu-id="2702f-247">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="2702f-248">Мы получаем такой результат:</span><span class="sxs-lookup"><span data-stu-id="2702f-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="2702f-249">Такой результат позволяет использовать наши наборы данных для обучения и тестовые наборы данных со сниженной частотой выборки для создания моделей в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-249">With this, we are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="2702f-250">Прежде чем мы перейдем к машинному обучению Azure, следует обсудить последний важный компонент, касающийся таблицы счетчиков.</span><span class="sxs-lookup"><span data-stu-id="2702f-250">There is a final important component before we move on to Azure Machine Learning, which is concerns the count table.</span></span> <span data-ttu-id="2702f-251">Он подробно описан в следующем подразделе.</span><span class="sxs-lookup"><span data-stu-id="2702f-251">In the next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="2702f-252"><a name="count"></a> Краткое описание таблицы счетчиков</span><span class="sxs-lookup"><span data-stu-id="2702f-252"><a name="count"></a> A brief discussion on the count table</span></span>
<span data-ttu-id="2702f-253">Как было видно, несколько категориальных переменных обладают очень высокой размерностью.</span><span class="sxs-lookup"><span data-stu-id="2702f-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="2702f-254">В нашем пошаговом руководстве представлен метод под названием [обучение с использованием счетчиков](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) для кодирования этих переменных эффективным и надежным способом.</span><span class="sxs-lookup"><span data-stu-id="2702f-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="2702f-255">Дополнительную информацию об этом методе можно получить, перейдя по указанной ссылке.</span><span class="sxs-lookup"><span data-stu-id="2702f-255">More information on this technique is in the link provided.</span></span>

[!NOTE]
><span data-ttu-id="2702f-256">В этом пошаговом руководстве рассматривается использование таблиц счетчиков для создания компактных представлений многомерных категориальных признаков.</span><span class="sxs-lookup"><span data-stu-id="2702f-256">In this walkthrough, we focus on using count tables to produce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="2702f-257">Это не единственный способ кодирования категориальных признаков. Дополнительные сведения о других методах заинтересованные пользователи могут найти в статьях по [прямому кодированию](http://en.wikipedia.org/wiki/One-hot) и [хэшированию признаков](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="2702f-257">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="2702f-258">Чтобы создать таблицы счетчиков на основе счетных данных, используются данные в папке raw/count.</span><span class="sxs-lookup"><span data-stu-id="2702f-258">To build count tables on the count data, we use the data in the folder raw/count.</span></span> <span data-ttu-id="2702f-259">В разделе о моделировании показано, как создавать эти таблицы счетчиков для категориальных признаков с нуля или использовать предварительно созданную таблицу счетчиков для работы с данными.</span><span class="sxs-lookup"><span data-stu-id="2702f-259">In the modeling section, we show users how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span></span> <span data-ttu-id="2702f-260">В следующих разделах термин «предварительно созданные таблицы счетчиков» употребляется в значении предоставляемых таблиц счетчиков.</span><span class="sxs-lookup"><span data-stu-id="2702f-260">In what follows, when we refer to "pre-built count tables", we mean using the count tables that we provide.</span></span> <span data-ttu-id="2702f-261">Подробные инструкции о том, как получить доступ к этим таблицам, приведены в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="2702f-261">Detailed instructions on how to access these tables are provided in the next section.</span></span>

## <span data-ttu-id="2702f-262"><a name="aml"></a> Создание моделей с помощью Машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="2702f-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="2702f-263">Процесс создания моделей в Машинном обучении Azure состоит из следующих шагов:</span><span class="sxs-lookup"><span data-stu-id="2702f-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="2702f-264">Получение данных из таблиц Hive и их добавление в Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="2702f-264">Get the data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="2702f-265">Создание эксперимента: очистка данных и создание признаков в таблицах счетчиков</span><span class="sxs-lookup"><span data-stu-id="2702f-265">Create the experiment: clean the data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="2702f-266">Создание, обучение и оценка модели</span><span class="sxs-lookup"><span data-stu-id="2702f-266">Build, train, and score the model</span></span>](#step3)
4. [<span data-ttu-id="2702f-267">Анализ модели</span><span class="sxs-lookup"><span data-stu-id="2702f-267">Evaluate the model</span></span>](#step4)
5. [<span data-ttu-id="2702f-268">Публикация модели в качестве веб-службы</span><span class="sxs-lookup"><span data-stu-id="2702f-268">Publish the model as a web-service</span></span>](#step5)

<span data-ttu-id="2702f-269">Теперь можно приступить к созданию моделей в Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-269">Now we are ready to build models in Azure Machine Learning studio.</span></span> <span data-ttu-id="2702f-270">Наши данные со сниженной частотой выборки сохраняются в кластере в виде таблиц Hive.</span><span class="sxs-lookup"><span data-stu-id="2702f-270">Our down sampled data is saved as Hive tables in the cluster.</span></span> <span data-ttu-id="2702f-271">Чтобы считать эти данные, мы используем модуль **Импорт данных** Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-271">We use the Azure Machine Learning **Import Data** module to read this data.</span></span> <span data-ttu-id="2702f-272">Учетные данные для доступа к учетной записи хранения этого кластера указаны далее.</span><span class="sxs-lookup"><span data-stu-id="2702f-272">The credentials to access the storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="2702f-273"><a name="step1"></a> Шаг 1. Извлечение данных из таблиц Hive в Машинное обучение Azure с помощью модуля "Импорт данных" и выбор этих данных для эксперимента машинного обучения</span><span class="sxs-lookup"><span data-stu-id="2702f-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="2702f-274">Для начала выберите **+Создать** -> **Эксперимент** -> **Пустой эксперимент**.</span><span class="sxs-lookup"><span data-stu-id="2702f-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="2702f-275">Затем в поле **Поиск** в верхнем левом углу экрана введите запрос "Импорт данных".</span><span class="sxs-lookup"><span data-stu-id="2702f-275">Then, from the **Search** box on the top left, search for "Import Data".</span></span> <span data-ttu-id="2702f-276">Перетащите модуль **Импорт данных** на холст эксперимента (в средней части экрана), чтобы использовать его для доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="2702f-276">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span></span>

<span data-ttu-id="2702f-277">Вот как выглядит модуль **Импорт данных** при получении данных из таблицы Hive:</span><span class="sxs-lookup"><span data-stu-id="2702f-277">This is what the **Import Data** looks like while getting data from the Hive table:</span></span>

![Модуль "Импорт данных" получает данные](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="2702f-279">Указанные выше параметры модуля **Импорт данных** представляют собой пример обязательных значений.</span><span class="sxs-lookup"><span data-stu-id="2702f-279">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span></span> <span data-ttu-id="2702f-280">Ниже представлены общие указания по заполнению набора параметров для модуля **Импорт данных** .</span><span class="sxs-lookup"><span data-stu-id="2702f-280">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span></span>

1. <span data-ttu-id="2702f-281">В поле **Источник данных**</span><span class="sxs-lookup"><span data-stu-id="2702f-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="2702f-282">В поле **Hive database query** (Запрос базы данных Hive) достаточно просто ввести SELECT * FROM <имя\_вашей\_базы_данных.имя\_вашей\_таблицы>.</span><span class="sxs-lookup"><span data-stu-id="2702f-282">In the **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="2702f-283">**URI сервера Hcatalog** — если используется кластер abc, введите адрес https://abc.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="2702f-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="2702f-284">**Имя учетной записи пользователя Hadoop** — имя пользователя, выбранное во время введения кластера в эксплуатацию.</span><span class="sxs-lookup"><span data-stu-id="2702f-284">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="2702f-285">(НЕ имя пользователя для удаленного доступа).</span><span class="sxs-lookup"><span data-stu-id="2702f-285">(NOT the Remote Access user name!)</span></span>
5. <span data-ttu-id="2702f-286">**Пароль учетной записи пользователя Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="2702f-286">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="2702f-287">Пароль для имени пользователя, выбранный во время введения кластера в эксплуатацию (НЕ пароль для удаленного доступа).</span><span class="sxs-lookup"><span data-stu-id="2702f-287">(NOT the Remote Access password!)</span></span>
6. <span data-ttu-id="2702f-288">**Расположение выходных данных**: выберите Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="2702f-289">**Имя учетной записи хранения Azure**: учетная запись хранения, связанная с кластером.</span><span class="sxs-lookup"><span data-stu-id="2702f-289">**Azure storage account name**: The storage account associated with the cluster</span></span>
8. <span data-ttu-id="2702f-290">**Ключ учетной записи хранения Azure**: ключ учетной записи хранения, связанной с кластером.</span><span class="sxs-lookup"><span data-stu-id="2702f-290">**Azure storage account key**: The key of the storage account associated with the cluster.</span></span>
9. <span data-ttu-id="2702f-291">**Имя контейнера Azure**: если используется имя кластера abc, нужно просто ввести abc.</span><span class="sxs-lookup"><span data-stu-id="2702f-291">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="2702f-292">После того как модуль **Импорт данных** завершит получение данных (возле модуля отобразится зеленая галочка), сохраните эти данные в качестве набора данных (с соответствующим именем).</span><span class="sxs-lookup"><span data-stu-id="2702f-292">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="2702f-293">Это выглядит так:</span><span class="sxs-lookup"><span data-stu-id="2702f-293">What this looks like:</span></span>

![Модуль "Импорт данных" сохраняет данные](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="2702f-295">Щелкните правой кнопкой мыши порт вывода модуля **Импорт данных** .</span><span class="sxs-lookup"><span data-stu-id="2702f-295">Right-click the output port of the **Import Data** module.</span></span> <span data-ttu-id="2702f-296">Отобразятся параметры **Сохранение набора данных** и **Визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="2702f-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="2702f-297">Если щелкнуть параметр **Визуализировать** , отобразится 100 строк с данными, а также правая панель, использующаяся для получения сводных статистических данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-297">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="2702f-298">Чтобы сохранить данные, выберите **Сохранение набора данных** и следуйте указаниям.</span><span class="sxs-lookup"><span data-stu-id="2702f-298">To save data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="2702f-299">Чтобы выбрать сохраненный набор данных, который будет использоваться в эксперименте машинного обучения, найдите его с помощью поля **Поиск** (на рисунке ниже).</span><span class="sxs-lookup"><span data-stu-id="2702f-299">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span></span> <span data-ttu-id="2702f-300">Затем введите часть имени набора данных, чтобы получить к нему доступ, и перетащите набор данных на главную панель.</span><span class="sxs-lookup"><span data-stu-id="2702f-300">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span></span> <span data-ttu-id="2702f-301">При этом набор данных автоматически выбирается для использования в моделировании машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="2702f-301">Dropping it onto the main panel selects it for use in machine learning modeling.</span></span>

![Перетаскивание набора данных на главную панель](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="2702f-303">Выполните эту процедуру для набора данных для обучения и тестового набора данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-303">Do this for both the train and the test datasets.</span></span> <span data-ttu-id="2702f-304">Кроме того, не забывайте использовать имя базы данных и имена таблиц, которые вы присвоили для этой цели.</span><span class="sxs-lookup"><span data-stu-id="2702f-304">Also, remember to use the database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="2702f-305">Показанные в примере значения приводятся только для справки.**</span><span class="sxs-lookup"><span data-stu-id="2702f-305">The values used in the figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="2702f-306"><a name="step2"></a> Шаг 2. Создание простого эксперимента в машинном обучении Azure для прогнозирования частоты выбора рекламного объявления</span><span class="sxs-lookup"><span data-stu-id="2702f-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span></span>
<span data-ttu-id="2702f-307">Наш эксперимент Машинного обучения Azure выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2702f-307">Our Azure ML experiment looks like this:</span></span>

![Эксперимент машинного обучения](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="2702f-309">Рассмотрим основные компоненты этого эксперимента.</span><span class="sxs-lookup"><span data-stu-id="2702f-309">We now examine the key components of this experiment.</span></span> <span data-ttu-id="2702f-310">Напоминаем, что для начала сохраненные наборы данных для обучения и тестовые наборы данных необходимо перетащить на холст эксперимента.</span><span class="sxs-lookup"><span data-stu-id="2702f-310">As a reminder, we need to drag our saved train and test datasets on to our experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="2702f-311">Очистка недостающих данных</span><span class="sxs-lookup"><span data-stu-id="2702f-311">Clean Missing Data</span></span>
<span data-ttu-id="2702f-312">Модуль **Clean Missing Data** (Очистка недостающих данных) выполняет одноименное действие, т. е. очищает недостающие данные, применяя для этого способ, указанный пользователем.</span><span class="sxs-lookup"><span data-stu-id="2702f-312">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="2702f-313">Если посмотреть на модуль, мы увидим следующее:</span><span class="sxs-lookup"><span data-stu-id="2702f-313">Looking into this module, we see this:</span></span>

![Очистка недостающих данных](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="2702f-315">Здесь мы выбрали заменить все недостающие значения на 0.</span><span class="sxs-lookup"><span data-stu-id="2702f-315">Here, we chose to replace all missing values with a 0.</span></span> <span data-ttu-id="2702f-316">Есть и другие варианты, которые можно увидеть, просмотрев раскрывающиеся списки в модуле.</span><span class="sxs-lookup"><span data-stu-id="2702f-316">There are other options as well, which can be seen by looking at the dropdowns in the module.</span></span>

#### <a name="feature-engineering-on-the-data"></a><span data-ttu-id="2702f-317">Проектирование компонентов на основе данных</span><span class="sxs-lookup"><span data-stu-id="2702f-317">Feature engineering on the data</span></span>
<span data-ttu-id="2702f-318">Некоторые категориальные функции крупных наборов данных могут иметь миллионы уникальных значений.</span><span class="sxs-lookup"><span data-stu-id="2702f-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="2702f-319">Использовать для представления таких многомерных функций упрощенные методы, например метод "прямого кодирования", нецелесообразно.</span><span class="sxs-lookup"><span data-stu-id="2702f-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="2702f-320">В этом пошаговом руководстве мы покажем, как с помощью встроенных модулей машинного обучения Azure применять функции счетчиков для создания компактных представлений многомерных категориальных переменных.</span><span class="sxs-lookup"><span data-stu-id="2702f-320">In this walkthrough, we demonstrate how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="2702f-321">Конечным результатом станет уменьшенный размер модели, более быстрое время обучения и параметры производительности, сопоставимые с результатами применения других методов.</span><span class="sxs-lookup"><span data-stu-id="2702f-321">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="2702f-322">Построение преобразований счетчиков</span><span class="sxs-lookup"><span data-stu-id="2702f-322">Building counting transforms</span></span>
<span data-ttu-id="2702f-323">Для создания функции счетчика используется модуль **Построение преобразования счетчика** , доступный в машинном обучении Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-323">To build count features, we use the **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="2702f-324">Модуль выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2702f-324">The module looks like this:</span></span>

<span data-ttu-id="2702f-325">![Модуль построения преобразования счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Модуль построения преобразования счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="2702f-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2702f-326">В поле **Count columns** (Столбцы счетчика) введены столбцы, в которых нужно применить счетчик.</span><span class="sxs-lookup"><span data-stu-id="2702f-326">In the **Count columns** box, we enter those columns that we wish to perform counts on.</span></span> <span data-ttu-id="2702f-327">Обычно это (как уже говорилось) — многомерные категориальные столбцы.</span><span class="sxs-lookup"><span data-stu-id="2702f-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="2702f-328">В начале статьи мы указали, что набор данных Criteo содержит 26 категориальных столбцов, от Col15 до Col40.</span><span class="sxs-lookup"><span data-stu-id="2702f-328">At the start, we mentioned that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span></span> <span data-ttu-id="2702f-329">Теперь вы применим счетчики ко всем этим столбцам и присвоим им индексы (от 15 до 40, разделенные запятыми).</span><span class="sxs-lookup"><span data-stu-id="2702f-329">Here, we count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="2702f-330">Для использования модуля в режиме MapReduce (подходит для больших наборов данных) требуется доступ к кластеру HDInsight Hadoop (можно использовать тот же кластер, который применялся для просмотра компонентов) и его учетные данные.</span><span class="sxs-lookup"><span data-stu-id="2702f-330">To use the module in the MapReduce mode (appropriate for large datasets), we need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="2702f-331">На предыдущих снимках экрана показано, как выглядят заполненные поля значений (замените их на значения, соответствующие вашему случаю).</span><span class="sxs-lookup"><span data-stu-id="2702f-331">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span></span>

![Параметры модуля](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="2702f-333">Приведенный выше снимок экрана показывает, как указать расположение большого двоичного объекта входных данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-333">In the figure above, we show how to enter the input blob location.</span></span> <span data-ttu-id="2702f-334">В этом расположении содержатся данные, зарезервированные под таблицы счетчиков.</span><span class="sxs-lookup"><span data-stu-id="2702f-334">This location has the data reserved for building count tables on.</span></span>

<span data-ttu-id="2702f-335">Когда выполнение этого модуля будет завершено, можно сохранить преобразование для последующего использования, щелкнув модуль правой кнопкой мыши и выбрав параметр **Save as Transform** (Сохранить как преобразование):</span><span class="sxs-lookup"><span data-stu-id="2702f-335">After this module finishes running, we can save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span></span>

![Параметр Save as Transform (Сохранить как преобразование)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="2702f-337">В представленной выше экспериментальной архитектуре сохраненному преобразованию счетчика точно соответствует набор данных ytransform2.</span><span class="sxs-lookup"><span data-stu-id="2702f-337">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span></span> <span data-ttu-id="2702f-338">Для остальной части эксперимента предположим, что читатель, применяет модуль **Построение преобразования счетчика** к некоторым данным для формирования счетчиков, а затем может использовать эти счетчики для создания функций счетчиков, применяемых к наборам данных для обучения и тестовым наборам данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-338">For the remainder of this experiment, we assume that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span></span>

##### <a name="choosing-what-count-features-to-include-as-part-of-the-train-and-test-datasets"></a><span data-ttu-id="2702f-339">Выбор функций счетчика для включения в наборы данных для обучения и тестовые наборы данных</span><span class="sxs-lookup"><span data-stu-id="2702f-339">Choosing what count features to include as part of the train and test datasets</span></span>
<span data-ttu-id="2702f-340">После преобразования счетчика можно выбрать функции для включения в наборы данных для обучения и тестовые наборы данных, используя для этого модуль **Изменение параметров таблицы счетчиков** .</span><span class="sxs-lookup"><span data-stu-id="2702f-340">Once we have a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="2702f-341">Этот модуль показан для полноты информации, но в целях упрощения в данном эксперименте он фактически не используется.</span><span class="sxs-lookup"><span data-stu-id="2702f-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Modify Count Table Parameters (Изменение параметров таблицы счетчиков)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="2702f-343">Как уже было показано, в данном случае мы решили использовать только логарифмы отношения вероятностей и игнорировать столбец задержки.</span><span class="sxs-lookup"><span data-stu-id="2702f-343">In this case, as can be seen, we have chosen to use just the log-odds and to ignore the back off column.</span></span> <span data-ttu-id="2702f-344">Также можно задать такие параметры, как пороговое значение ячейки сборки мусора, количество псевдослучайных предыдущих примеров для добавления с целью сглаживания и использование лапласовского шума.</span><span class="sxs-lookup"><span data-stu-id="2702f-344">We can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span></span> <span data-ttu-id="2702f-345">Все это — дополнительные возможности, и следует отметить, что пользователям, не знакомым с процессом создания функций подобного типа, рекомендуется начинать со значений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2702f-345">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-the-count-features"></a><span data-ttu-id="2702f-346">Преобразование данных перед созданием функций счетчика</span><span class="sxs-lookup"><span data-stu-id="2702f-346">Data transformation before generating the count features</span></span>
<span data-ttu-id="2702f-347">Теперь обратим внимание на такой важный момент, как преобразование данных для обучения и тестовых данных перед созданием функций счетчика.</span><span class="sxs-lookup"><span data-stu-id="2702f-347">Now we focus on an important point about transforming our train and test data prior to actually generating count features.</span></span> <span data-ttu-id="2702f-348">Обратите внимание, что перед применением преобразования счетчика к данным используются два модуля **Выполнение скрипта R** .</span><span class="sxs-lookup"><span data-stu-id="2702f-348">Note that there are two **Execute R Script** modules used before we apply the count transform to our data.</span></span>

![Модули "Выполнить сценарий R"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="2702f-350">Первый скрипт R выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2702f-350">Here is the first R script:</span></span>

![Первый сценарий R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="2702f-352">В этом скрипте R столбцы получают новые имена — от Col1 до Col40.</span><span class="sxs-lookup"><span data-stu-id="2702f-352">In this R script, we rename our columns to names "Col1" to "Col40".</span></span> <span data-ttu-id="2702f-353">Этот формат имен необходим для преобразования счетчика.</span><span class="sxs-lookup"><span data-stu-id="2702f-353">This is because the count transform expects names of this format.</span></span>

<span data-ttu-id="2702f-354">Во втором скрипте R балансируется распределение между положительными и отрицательными классами (классы 1 и 0 соответственно). Для этого используется понижающая дискретизация отрицательного класса.</span><span class="sxs-lookup"><span data-stu-id="2702f-354">In the second R script, we balance the distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling the negative class.</span></span> <span data-ttu-id="2702f-355">Приведенный ниже скрипт R показывает, как ее выполнить.</span><span class="sxs-lookup"><span data-stu-id="2702f-355">The R script here shows how to do this:</span></span>

![Второй сценарий R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="2702f-357">В этом простом скрипте R для установки интервала баланса между положительным и отрицательным классами используется выражение pos\_neg\_ratio.</span><span class="sxs-lookup"><span data-stu-id="2702f-357">In this simple R script, we use "pos\_neg\_ratio" to set the amount of balance between the positive and the negative classes.</span></span> <span data-ttu-id="2702f-358">Это действие важно, так как устранение дисбаланса между классами положительно влияет на скорость выполнения задач классификации со скошенным распределением классов (напомним, что в нашем случае на положительный класс приходится 3,3 %, а на отрицательный — 96,7 %).</span><span class="sxs-lookup"><span data-stu-id="2702f-358">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-the-count-transformation-on-our-data"></a><span data-ttu-id="2702f-359">Применение преобразования счетчика к данным</span><span class="sxs-lookup"><span data-stu-id="2702f-359">Applying the count transformation on our data</span></span>
<span data-ttu-id="2702f-360">Наконец, воспользуемся модулем **Применить преобразование** и применим преобразования счетчика к наборам данных для обучения и тестовым наборам данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-360">Finally, we can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span></span> <span data-ttu-id="2702f-361">Этот модуль воспринимает сохраненное преобразование счетчика как один набор входных данных, а наборы данных для обучения и тестовые наборы данных — как другой набор входных данных и возвращает данные с функциями счетчиков.</span><span class="sxs-lookup"><span data-stu-id="2702f-361">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span></span> <span data-ttu-id="2702f-362">Вот как это работает:</span><span class="sxs-lookup"><span data-stu-id="2702f-362">It is shown here:</span></span>

![Модуль применения преобразования](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-the-count-features-look-like"></a><span data-ttu-id="2702f-364">Фрагмент вида функций счетчика</span><span class="sxs-lookup"><span data-stu-id="2702f-364">An excerpt of what the count features look like</span></span>
<span data-ttu-id="2702f-365">Внешний вид функций счетчика в нашем случае очень информативен.</span><span class="sxs-lookup"><span data-stu-id="2702f-365">It is instructive to see what the count features look like in our case.</span></span> <span data-ttu-id="2702f-366">Вот его фрагмент:</span><span class="sxs-lookup"><span data-stu-id="2702f-366">Here we show an excerpt of this:</span></span>

![Функции счетчика](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="2702f-368">В этом фрагменте показано, что для столбцов, к которым применен счетчик, создаются как соответствующие задержки, так и счетчики и логарифмы отношения вероятностей.</span><span class="sxs-lookup"><span data-stu-id="2702f-368">In this excerpt, we show that for the columns that we counted on, we get the counts and log odds in addition to any relevant backoffs.</span></span>

<span data-ttu-id="2702f-369">Теперь, используя преобразованные наборы данных, можно построить модель машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-369">We are now ready to build an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="2702f-370">В следующем разделе показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="2702f-370">In the next section, we show how this can be done.</span></span>

### <span data-ttu-id="2702f-371"><a name="step3"></a> Шаг 3. Создание, обучение и оценка модели</span><span class="sxs-lookup"><span data-stu-id="2702f-371"><a name="step3"></a> Step 3: Build, train, and score the model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="2702f-372">Выбор ученика</span><span class="sxs-lookup"><span data-stu-id="2702f-372">Choice of learner</span></span>
<span data-ttu-id="2702f-373">В первую очередь необходимо выбрать ученика.</span><span class="sxs-lookup"><span data-stu-id="2702f-373">First, we need to choose a learner.</span></span> <span data-ttu-id="2702f-374">В качестве ученика будет выступать двухклассовое увеличивающееся дерево принятия решений.</span><span class="sxs-lookup"><span data-stu-id="2702f-374">We are going to use a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="2702f-375">По умолчанию для этого ученика используются следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="2702f-375">Here are the default options for this learner:</span></span>

![Параметры двухклассового увеличивающегося дерева принятия решений](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="2702f-377">Для данного эксперимента мы возьмем значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2702f-377">For our experiment, we are going to choose the default values.</span></span> <span data-ttu-id="2702f-378">Как правило, значения по умолчанию эффективны и позволяют быстро добиться нужной производительности.</span><span class="sxs-lookup"><span data-stu-id="2702f-378">We note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span></span> <span data-ttu-id="2702f-379">Построив базу, можно повысить производительность, скорректировав желаемые параметры.</span><span class="sxs-lookup"><span data-stu-id="2702f-379">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span></span>

#### <a name="train-the-model"></a><span data-ttu-id="2702f-380">Обучение модели</span><span class="sxs-lookup"><span data-stu-id="2702f-380">Train the model</span></span>
<span data-ttu-id="2702f-381">Для обучения мы просто вызовем модуль **Обучение модели** .</span><span class="sxs-lookup"><span data-stu-id="2702f-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="2702f-382">Он использует два набора входных данных — двухклассовое увеличивающееся дерево принятия решений (наш ученик) и набор данных для обучения.</span><span class="sxs-lookup"><span data-stu-id="2702f-382">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="2702f-383">Вот как это работает:</span><span class="sxs-lookup"><span data-stu-id="2702f-383">This is shown here:</span></span>

![Модуль "Обучение модели"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-the-model"></a><span data-ttu-id="2702f-385">Оценка модели</span><span class="sxs-lookup"><span data-stu-id="2702f-385">Score the model</span></span>
<span data-ttu-id="2702f-386">Обучив модель, можно оценить его производительность с помощью тестового набора данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-386">Once we have a trained model, we are ready to score on the test dataset and to evaluate its performance.</span></span> <span data-ttu-id="2702f-387">Для этого используется модуль **Score Model** (Оценка модели) на следующем рисунке вместе с модулем **Evaluate Model** (Анализ модели):</span><span class="sxs-lookup"><span data-stu-id="2702f-387">We do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span></span>

![Модуль "Оценка модели"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="2702f-389"><a name="step4"></a> Шаг 4. Анализ модели</span><span class="sxs-lookup"><span data-stu-id="2702f-389"><a name="step4"></a> Step 4: Evaluate the model</span></span>
<span data-ttu-id="2702f-390">Наконец, нам требуется оценить эффективность модели.</span><span class="sxs-lookup"><span data-stu-id="2702f-390">Finally, we would like to analyze model performance.</span></span> <span data-ttu-id="2702f-391">Как правило, для задач двухклассовой (двоичной) классификации хорошо подходит мера AUC.</span><span class="sxs-lookup"><span data-stu-id="2702f-391">Usually, for two class (binary) classification problems, a good measure is the AUC.</span></span> <span data-ttu-id="2702f-392">Чтобы визуализировать это, мы подключим модуль **Score Model** (Оценка модели) к модулю **Evaluate Model** (Анализ модели).</span><span class="sxs-lookup"><span data-stu-id="2702f-392">To visualize this, we hook up the **Score Model** module to an **Evaluate Model** module for this.</span></span> <span data-ttu-id="2702f-393">Если щелкнуть **Визуализировать** в модуле **Evaluate Model** (Анализ модели), отобразится подобная схема:</span><span class="sxs-lookup"><span data-stu-id="2702f-393">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span></span>

![Модуль «Анализ модели» и «Увеличивающееся дерево принятия решений»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="2702f-395">В задачах двоичной (или двухклассовой) классификации хорошо подходит такая мера прогнозирования точности, как AUC (площадь под кривой).</span><span class="sxs-lookup"><span data-stu-id="2702f-395">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span></span> <span data-ttu-id="2702f-396">Ниже будут показаны результаты использования этой модели на основе нашего тестового набора данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="2702f-397">Чтобы выполнить все должным образом, щелкните правой кнопкой мыши порт вывода модуля **Evaluate Model** (Анализ модели), а затем щелкните **Визуализировать**.</span><span class="sxs-lookup"><span data-stu-id="2702f-397">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span></span>

![Визуализация модуля «Анализ модели»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="2702f-399"><a name="step5"></a> Шаг 5. Публикация модели в качестве веб-службы</span><span class="sxs-lookup"><span data-stu-id="2702f-399"><a name="step5"></a> Step 5: Publish the model as a Web service</span></span>
<span data-ttu-id="2702f-400">Публикация модели машинного обучения Azure как веб-службы требует минимальных усилий и позволяет сделать ее доступной для других пользователей.</span><span class="sxs-lookup"><span data-stu-id="2702f-400">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="2702f-401">После публикации любой сможет вызвать веб-службу, передав ей исходные данные, по которым требуется прогноз, а веб-служба — выдать прогноз, используя эту модель.</span><span class="sxs-lookup"><span data-stu-id="2702f-401">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span></span>

<span data-ttu-id="2702f-402">Для этого сначала нужно сохранить обученную модель как объект «Обученная модель».</span><span class="sxs-lookup"><span data-stu-id="2702f-402">To do this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="2702f-403">Это можно сделать, щелкнув правой кнопкой мыши модуль **Обучение модели** и выбрав параметр **Save as Trained Model** (Сохранить как обученную модель).</span><span class="sxs-lookup"><span data-stu-id="2702f-403">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span></span>

<span data-ttu-id="2702f-404">Теперь нужно создать входные и выходные порты для веб-службы:</span><span class="sxs-lookup"><span data-stu-id="2702f-404">Next, we need to create input and output ports for our web service:</span></span>

* <span data-ttu-id="2702f-405">входной порт принимает данные в том же виде, что и данные, для которых требуется прогноз;</span><span class="sxs-lookup"><span data-stu-id="2702f-405">an input port takes data in the same form as the data that we need predictions for</span></span>
* <span data-ttu-id="2702f-406">выходной порт вывода выдает метки оценки и связанные с ними значения вероятности.</span><span class="sxs-lookup"><span data-stu-id="2702f-406">an output port returns the Scored Labels and the associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-the-input-port"></a><span data-ttu-id="2702f-407">Выбор нескольких строк данных для порта ввода</span><span class="sxs-lookup"><span data-stu-id="2702f-407">Select a few rows of data for the input port</span></span>
<span data-ttu-id="2702f-408">Чтобы выбрать всего 10 строк для использования в качестве данных порта ввода, можно воспользоваться модулем **Применение преобразования SQL** .</span><span class="sxs-lookup"><span data-stu-id="2702f-408">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span></span> <span data-ttu-id="2702f-409">Выберите для входного порта только эти строки данных с помощью показанного ниже SQL-запроса.</span><span class="sxs-lookup"><span data-stu-id="2702f-409">Select just these rows of data for our input port using the SQL query shown here:</span></span>

![Данные порта ввода](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="2702f-411">Веб-служба</span><span class="sxs-lookup"><span data-stu-id="2702f-411">Web service</span></span>
<span data-ttu-id="2702f-412">Теперь можно приступить к выполнению небольшого эксперимента, который можно использовать для публикации веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2702f-412">Now we are ready to run a small experiment that can be used to publish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="2702f-413">Создание входных данных для веб-службы</span><span class="sxs-lookup"><span data-stu-id="2702f-413">Generate input data for webservice</span></span>
<span data-ttu-id="2702f-414">Так как таблица счетчиков имеет большой размер, на начальном этапе мы возьмем несколько строк тестовых данных и создадим из них выходные данные с признаками счетчиков.</span><span class="sxs-lookup"><span data-stu-id="2702f-414">As a zeroth step, since the count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="2702f-415">Это послужит в качестве формата входных данных для наших веб-служб.</span><span class="sxs-lookup"><span data-stu-id="2702f-415">This can serve as the input data format for our webservice.</span></span> <span data-ttu-id="2702f-416">Вот как это работает:</span><span class="sxs-lookup"><span data-stu-id="2702f-416">This is shown here:</span></span>

![Создание входных данных модуля «Увеличивающееся дерево принятия решений»](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="2702f-418">В качестве формата входных данных теперь будут использоваться ВЫХОДНЫЕ ДАННЫЕ модуля **Характеризатор счетчиков** .</span><span class="sxs-lookup"><span data-stu-id="2702f-418">For the input data format, we now use the OUTPUT of the **Count Featurizer** module.</span></span> <span data-ttu-id="2702f-419">После завершения выполнения этого эксперимента сохраните выходные данные модуля **Характеризатор счетчиков** в качестве набора данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-419">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="2702f-420">Этот набор данных используется для входных данных в веб-службе.</span><span class="sxs-lookup"><span data-stu-id="2702f-420">This Dataset is used for the input data in the webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="2702f-421">Оценка эксперимента для публикации веб-службы</span><span class="sxs-lookup"><span data-stu-id="2702f-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="2702f-422">Сначала мы покажем, как это выглядит.</span><span class="sxs-lookup"><span data-stu-id="2702f-422">First, we show what this looks like.</span></span> <span data-ttu-id="2702f-423">Основная структура — модуль **Score Model** (Оценка модели), который принимает объект обученной модели, и несколько строк входных данных, созданных ранее с помощью модуля **Count Featurizer** (Характеризатор счетчиков).</span><span class="sxs-lookup"><span data-stu-id="2702f-423">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in the previous steps using the **Count Featurizer** module.</span></span> <span data-ttu-id="2702f-424">Мы используем модуль "Выбор столбцов в наборе данных", чтобы отобразить расчетные метки и значения вероятности оценки.</span><span class="sxs-lookup"><span data-stu-id="2702f-424">We use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span></span>

![Выбор столбцов в наборе данных](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="2702f-426">Обратите внимание, что модуль **Выбор столбцов в наборе данных** можно использовать для фильтрации данных из набора данных.</span><span class="sxs-lookup"><span data-stu-id="2702f-426">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="2702f-427">Содержимое модуля показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2702f-427">We show the contents here:</span></span>

![Фильтрация с помощью модуля "Выбор столбцов в наборе данных"](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="2702f-429">Чтобы порты ввода и вывода стали синими, просто щелкните значок **Подготовить веб-службу** в нижнем правом углу.</span><span class="sxs-lookup"><span data-stu-id="2702f-429">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span></span> <span data-ttu-id="2702f-430">Выполнение этого эксперимента также позволяет опубликовать веб-службу, щелкнув значок **Publish web service** (Опубликовать веб-службу) в нижнем правом углу, показанный ниже.</span><span class="sxs-lookup"><span data-stu-id="2702f-430">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span></span>

![Publish web service](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="2702f-432">После публикации веб-службы вы перейдете на страницу, которая выглядит таким образом:</span><span class="sxs-lookup"><span data-stu-id="2702f-432">Once the webservice is published, we get redirected to a page that looks thus:</span></span>

![Панель мониторинга веб-службы](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="2702f-434">Слева видно две ссылки для веб-служб:</span><span class="sxs-lookup"><span data-stu-id="2702f-434">We see two links for webservices on the left side:</span></span>

* <span data-ttu-id="2702f-435">Служба **Запрос — ответ** (или RRS), предназначенная для разовых прогнозов. Именно она будет использоваться на этом семинаре.</span><span class="sxs-lookup"><span data-stu-id="2702f-435">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="2702f-436">служба **ПАКЕТНОГО ВЫПОЛНЕНИЯ** (BES) используется для пакетных прогнозов и требует, чтобы входные данные, для которых нужно создать прогноз, находились в большом двоичном объекте Azure.</span><span class="sxs-lookup"><span data-stu-id="2702f-436">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="2702f-437">Если щелкнуть ссылку **Запрос — ответ**, вы перейдете на страницу, которая содержит код на C#, Python и R, поставляемый изготовителем. Этот код можно использовать для вызова веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2702f-437">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span></span> <span data-ttu-id="2702f-438">Обратите внимание, что ключ API на этой странице следует использовать для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="2702f-438">Note that the API key on this page needs to be used for authentication.</span></span>

<span data-ttu-id="2702f-439">Удобно скопировать этот код Рython и вставить его в новую ячейку в iPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="2702f-439">It is convenient to copy this python code over to a new cell in the IPython notebook.</span></span>

<span data-ttu-id="2702f-440">Ниже показан фрагмент кода Python с правильным ключом API.</span><span class="sxs-lookup"><span data-stu-id="2702f-440">Here we show a segment of python code with the correct API key.</span></span>

![Код Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="2702f-442">Обратите внимание, что мы заменили ключ API по умолчанию на ключ API для наших веб-служб.</span><span class="sxs-lookup"><span data-stu-id="2702f-442">Note that we replaced the default API key with our webservices's API key.</span></span> <span data-ttu-id="2702f-443">Щелкнув **Запуск** в данной ячейке в iPython Notebook, вы получите следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="2702f-443">Clicking **Run** on this cell in an IPython notebook yields the following response:</span></span>

![Ответ iPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="2702f-445">Мы видим, что ответы для двух запрошенных тестовых примеров (в структуре JSON сценария Python) получены в форме «расчетные метки, расчетные вероятности».</span><span class="sxs-lookup"><span data-stu-id="2702f-445">We see that for the two test examples we asked about (in the JSON framework of the python script), we get back answers in the form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="2702f-446">Обратите внимание, что в этом случае были выбраны значения по умолчанию кода, поставляемого изготовителем (значение 0 для всех числовых столбцов, строка «Значение» для всех категориальных столбцов).</span><span class="sxs-lookup"><span data-stu-id="2702f-446">Note that in this case, we chose the default values that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span></span>

<span data-ttu-id="2702f-447">На этом пошаговое руководство по обработке крупномасштабных наборов данных с помощью Машинного обучения Azure завершается.</span><span class="sxs-lookup"><span data-stu-id="2702f-447">This concludes our end-to-end walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="2702f-448">Мы начали работу с терабайтом данных, построили модель прогнозирования и развернули ее в облаке как веб-службу.</span><span class="sxs-lookup"><span data-stu-id="2702f-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in the cloud.</span></span>

