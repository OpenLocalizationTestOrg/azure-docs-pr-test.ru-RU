---
title: "Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake | Документация Майкрософт"
description: "Как toouse Озера данных Azure toodo исследования и двоичной классификации данных задач для набора данных."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="1955c-103">Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1955c-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="1955c-104">В этом пошаговом руководстве показано, как просмотр данных toodo toouse Озера данных Azure и задачи двоичной классификации образца hello NYC такси маршрута и тариф авиакомпании toopredict набора данных независимо от того, имеется ли подсказка будет оплачиваться тариф авиакомпании.</span><span class="sxs-lookup"><span data-stu-id="1955c-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="1955c-105">Он поможет выполнить шаги hello hello [командного процесса обработки и анализа данных](http://aka.ms/datascienceprocess), узел узел, из данных приобретения toomodel обучения, а затем toohello развертывания веб-службы, которая публикует модели hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="1955c-106">Аналитика озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="1955c-107">Hello [Озера данных Microsoft Azure](https://azure.microsoft.com/solutions/data-lake/) имеет все необходимые toomake возможности hello легко toostore специалистами по анализу данных любого размера, формы и скорость и tooconduct обработки данных, advanced analytics и моделирования машины обучения с высокой масштабируемостью экономичным способом.</span><span class="sxs-lookup"><span data-stu-id="1955c-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="1955c-108">Плата взимается за задание, и только если данные обработаны фактически.</span><span class="sxs-lookup"><span data-stu-id="1955c-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="1955c-109">Azure аналитики Озера данных включает U-SQL, язык, что переходы hello декларативной природы SQL с hello выразительных возможностей C# tooprovide масштабируемой распределенного запроса возможностей.</span><span class="sxs-lookup"><span data-stu-id="1955c-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="1955c-110">Благодаря этому можно tooprocess неструктурированные данные, применив схему на чтение, вставка пользовательской логики и определяемые пользователем функции (UDF) и включает расширения tooenable нормально точный контроль над тем, как tooexecute в масштабе.</span><span class="sxs-lookup"><span data-stu-id="1955c-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="1955c-111">toolearn Дополнительные сведения о принципы разработки hello за U-SQL, в разделе [блоге Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="1955c-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="1955c-112">Аналитика озера данных — это также ключевая часть Cortana Analytics Suite. Она поддерживает работу с хранилищем данных SQL Azure, Power BI и фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="1955c-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="1955c-113">Это создает всеобъемлющую облачную платформу для работы с большими данными и углубленной аналитики.</span><span class="sxs-lookup"><span data-stu-id="1955c-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="1955c-114">В этом пошаговом руководстве начинается с описания hello необходимые компоненты и ресурсы, необходимые toocomplete hello задач с помощью аналитики Озера данных этой формы процесса обработки и анализа данных hello и каким образом tooinstall их.</span><span class="sxs-lookup"><span data-stu-id="1955c-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="1955c-115">Затем оно описано hello обработки данных с помощью U-SQL и завершается, показывая, как toouse Python и Hive с toobuild студии машинного обучения Azure и развернуть hello прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="1955c-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="1955c-116">U-SQL и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1955c-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="1955c-117">Рекомендуется использовать Visual Studio tooedit U-SQL скрипты tooprocess hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="1955c-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="1955c-118">сценарии Hello U-SQL описаны здесь и в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="1955c-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="1955c-119">процесс Hello включает обработки, просмотра и выборки данных hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="1955c-120">Здесь также показано, как toorun U-SQL в скрипт задание из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="1955c-121">Куст таблицы создаются для hello данных в связанных HDInsight кластера toofacilitate hello построение и развертывание модели двоичной классификации в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="1955c-122">Python</span><span class="sxs-lookup"><span data-stu-id="1955c-122">Python</span></span>
<span data-ttu-id="1955c-123">В этом пошаговом руководстве также содержит раздел, описывающий, каким образом toobuild и развертывание прогнозную модель с помощью Python с студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="1955c-124">Мы предоставляем записной книжке Jupyter hello Python скрипты для этих шагов в этом процессе.</span><span class="sxs-lookup"><span data-stu-id="1955c-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="1955c-125">ноутбук Hello включает код некоторые этапы проектирования дополнительных компонентов и построения моделей, например мультиклассовой классификации и регрессии, кроме моделирования toohello модель двоичной классификации, описанную.</span><span class="sxs-lookup"><span data-stu-id="1955c-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="1955c-126">Задача Hello регрессии — toopredict hello объем hello подсказки на основе других функций подсказки.</span><span class="sxs-lookup"><span data-stu-id="1955c-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="1955c-127">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-127">Azure Machine Learning</span></span>
<span data-ttu-id="1955c-128">Студия машинного обучения используется toobuild и разверните hello прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="1955c-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="1955c-129">Для этого используется два подхода: первый — с помощью сценариев Python, а второй — с использованием таблиц Hive на кластере HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="1955c-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="1955c-130">Сценарии</span><span class="sxs-lookup"><span data-stu-id="1955c-130">Scripts</span></span>
<span data-ttu-id="1955c-131">В этом пошаговом руководстве описаны только основные шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="1955c-132">Вы можете скачать полный hello **скрипт U-SQL** и **книжке Jupyter** из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="1955c-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1955c-133">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1955c-133">Prerequisites</span></span>
<span data-ttu-id="1955c-134">Прежде чем начать эти разделы, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="1955c-135">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-135">An Azure subscription.</span></span> <span data-ttu-id="1955c-136">Если у вас ее нет, см. статью [о получении бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1955c-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="1955c-137">[Рекомендуется] Visual Studio 2013 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1955c-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="1955c-138">Если вы еще не установили одну из этих версий, можно скачать бесплатную версию Community с сайта [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="1955c-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="1955c-139">Вместо Visual Studio также можно использовать запросы Озера данных Azure toosubmit портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="1955c-140">Корпорация Майкрософт предоставляет инструкции о том, как toodo так как с помощью Visual Studio, так и на портале hello в разделе "hello" под названием **обработки данных с помощью U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="1955c-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="1955c-141">Подготовка среды анализа данных для озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="1955c-142">среда обработки и анализа данных tooprepare hello в данном пошаговом руководстве создайте hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="1955c-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="1955c-143">хранилище озера данных Azure;</span><span class="sxs-lookup"><span data-stu-id="1955c-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="1955c-144">Аналитику озера данных Azure;</span><span class="sxs-lookup"><span data-stu-id="1955c-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="1955c-145">учетную запись хранения BLOB-объектов;</span><span class="sxs-lookup"><span data-stu-id="1955c-145">Azure Blob storage account</span></span>
* <span data-ttu-id="1955c-146">учетную запись Студии машинного обучения Azure;</span><span class="sxs-lookup"><span data-stu-id="1955c-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="1955c-147">средства озера данных Azure для Visual Studio (рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="1955c-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="1955c-148">Этот раздел содержит инструкции о том, как toocreate каждого из этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1955c-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="1955c-149">Если выбрать toouse Hive таблиц с помощью машинного обучения Azure, вместо Python, toobuild модели, необходимо также tooprovision кластер HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="1955c-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="1955c-150">Альтернативные процедура, описанная в описанной в соответствующем разделе hello ниже.</span><span class="sxs-lookup"><span data-stu-id="1955c-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="1955c-151">Hello **хранилища Озера данных Azure** могут создаваться либо отдельно, либо при создании hello **аналитики Озера данных Azure** хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="1955c-152">Для создания каждого из этих ресурсов отдельно ниже ссылаются инструкции, но hello учетной записи хранилища Озера данных не должны создаваться отдельно.</span><span class="sxs-lookup"><span data-stu-id="1955c-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="1955c-153">Создание хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="1955c-154">Создать из hello ADLS [портала Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1955c-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="1955c-155">Дополнительные сведения см. в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1955c-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="1955c-156">Быть убедиться, что tooset копирование hello удостоверение кластера AAD в hello **DataSource** колонке hello **необязательная конфигурация** колонке описано существует.</span><span class="sxs-lookup"><span data-stu-id="1955c-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="1955c-158">Создание учетной записи Аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="1955c-159">Создайте учетную запись ADLA из hello [портала Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1955c-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="1955c-160">Дополнительные сведения см. в статье [Руководство. Начало работы с Azure Data Lake Analytics с помощью портала Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1955c-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="1955c-162">Создание учетной записи хранения BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="1955c-163">Создать учетную запись службы хранилища больших двоичных объектов Azure из hello [портала Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1955c-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="1955c-164">Дополнительные сведения см. в разделе hello создать учетную запись хранилища раздела [учетных записей хранилища Azure о](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1955c-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="1955c-166">Настройка учетной записи Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="1955c-167">Войти в студию машинного обучения Azure из hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) страницы.</span><span class="sxs-lookup"><span data-stu-id="1955c-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="1955c-168">Щелкните hello **начните** кнопку и выберите «Бесплатную рабочую область» или «Стандартные рабочую область».</span><span class="sxs-lookup"><span data-stu-id="1955c-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="1955c-169">После этого можно будет toocreate экспериментов в Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="1955c-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="1955c-170">Установка инструментов озера данных Azure [рекомендуется]</span><span class="sxs-lookup"><span data-stu-id="1955c-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="1955c-171">Установите инструменты озера данных Azure в зависимости от своей версии Visual Studio со страницы [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)(Инструменты озера данных Azure для Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1955c-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="1955c-173">После успешного завершения установки hello, откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1955c-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="1955c-174">Вы увидите hello Озера данных вкладке hello меню вверху hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="1955c-175">Ресурсы Azure должны появиться в левой панели hello при входе в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="1955c-177">набор Hello NYC такси приема-передачи данных</span><span class="sxs-lookup"><span data-stu-id="1955c-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="1955c-178">Hello набора данных, мы использовали здесь является общедоступным набор данных — hello [NYC такси приема-передачи набора данных](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="1955c-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="1955c-179">Hello NYC такси обработки данных состоит из примерно 20 ГБ сжатые файлы CSV (~ 48 ГБ несжатого), запись более миллиона 173 отдельных приема-передачи и hello цен платная для каждого маршрута.</span><span class="sxs-lookup"><span data-stu-id="1955c-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="1955c-180">Каждая запись маршрута включает hello раскладки и истощение расположений и времени, анонимен hack номер лицензии (драйвер) и hello номер medallion (уникальный идентификатор элемента такси).</span><span class="sxs-lookup"><span data-stu-id="1955c-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="1955c-181">данные Hello охватывает все приема-передачи в 2013 году, hello и предоставляется в следующих двух наборов данных для каждого месяца hello:</span><span class="sxs-lookup"><span data-stu-id="1955c-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="1955c-182">Hello «trip_data» CSV содержит обработки таких сведений, как количество пассажиров, раскладки и dropoff точек, длительность обработки и длина пути.</span><span class="sxs-lookup"><span data-stu-id="1955c-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="1955c-183">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="1955c-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="1955c-184">Здравствуйте, trip_fare CSV содержит подробные сведения о тариф авиакомпании hello платная для каждого маршрута, например тип платежа, сумма тариф авиакомпании, излишнюю нагрузку налоги, советы и тарифы и hello общей оплаты.</span><span class="sxs-lookup"><span data-stu-id="1955c-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="1955c-185">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="1955c-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="1955c-186">Hello trip уникальных ключей toojoin\_данных и обработки\_тариф авиакомпании состоит из следующих трех полей hello: medallion hack\_лицензии и раскладки\_даты и времени.</span><span class="sxs-lookup"><span data-stu-id="1955c-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="1955c-187">Hello необработанные CSV-файлов может осуществляться из большой двоичный объект открытого хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="1955c-188">Здравствуйте скрипт U-SQL для этого соединения находятся в hello [соединения таблиц маршрута и тариф авиакомпании](#join) раздела.</span><span class="sxs-lookup"><span data-stu-id="1955c-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="1955c-189">Обработка данных с использованием U-SQL</span><span class="sxs-lookup"><span data-stu-id="1955c-189">Process data with U-SQL</span></span>
<span data-ttu-id="1955c-190">Hello задач обработки данных, приведенных в этом разделе включают передаче, проверка качества, исследование и выборки данных hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="1955c-191">Мы также показано, как toojoin маршрута и тариф авиакомпании таблицы.</span><span class="sxs-lookup"><span data-stu-id="1955c-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="1955c-192">Последний сегмент Hello показывает выполнения созданное задание U-SQL из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="1955c-193">Ниже приведены ссылки tooeach подраздела.</span><span class="sxs-lookup"><span data-stu-id="1955c-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="1955c-194">Прием данных: чтение из общедоступного большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="1955c-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="1955c-195">Проверка качества данных</span><span class="sxs-lookup"><span data-stu-id="1955c-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="1955c-196">Исследование данных</span><span class="sxs-lookup"><span data-stu-id="1955c-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="1955c-197">Объединение таблиц trip и fare</span><span class="sxs-lookup"><span data-stu-id="1955c-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="1955c-198">Выборка данных</span><span class="sxs-lookup"><span data-stu-id="1955c-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="1955c-199">Выполнение заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="1955c-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="1955c-200">сценарии Hello U-SQL описаны здесь и в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="1955c-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="1955c-201">Вы можете скачать полный hello **U-SQL скрипты** из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="1955c-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="1955c-202">tooexecute U-SQL, откройте Visual Studio, нажмите кнопку **файл--> Создать проект-->**, выберите **проекта U-SQL**, имя и сохранить его в папку tooa.</span><span class="sxs-lookup"><span data-stu-id="1955c-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="1955c-204">Это возможно toouse hello портала Azure tooexecute U-SQL вместо Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1955c-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="1955c-205">Можно переходить toohello ресурсов аналитики Озера данных Azure на портале hello и отправлять запросы напрямую, как показано в следующий рисунок hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="1955c-207"><a name="ingest"></a>Прием данных: чтение из общедоступного большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="1955c-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="1955c-208">Hello расположение данных hello в hello BLOB-объектов Azure есть ссылки как  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  и можно извлечь при помощи **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="1955c-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="1955c-209">Замените имя контейнера и имя учетной записи хранения в следующем сценарии для container_name@blob_storage_account_name в адресе wasb hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="1955c-210">Поскольку имена файлов hello в одном формате, можно использовать **trip\_data_ {\*\}.csv** tooread во всех файлах 12 маршрута.</span><span class="sxs-lookup"><span data-stu-id="1955c-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="1955c-211">Так как существуют заголовки в первой строке hello, мы должны tooremove hello заголовки и изменить типы столбцов в соответствующие столбцы.</span><span class="sxs-lookup"><span data-stu-id="1955c-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="1955c-212">Мы можем либо сохранить hello обработки данных tooAzure хранилища Озера данных с помощью **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ или tooAzure хранилища BLOB-объектов учетной записи с помощью  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="1955c-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="1955c-213">Аналогичным образом мы чтения в наборах данных тариф авиакомпании hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="1955c-214">Щелкните правой кнопкой мыши хранилища Озера данных Azure, вы можете toolook данные в **портала Azure--> обозреватель данных** или **проводнике** в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1955c-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="1955c-217"><a name="quality"></a>Проверка качества данных</span><span class="sxs-lookup"><span data-stu-id="1955c-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="1955c-218">После считывания маршрута и тариф авиакомпании таблиц в проверок качества данных может осуществляться в hello следующими способами.</span><span class="sxs-lookup"><span data-stu-id="1955c-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="1955c-219">Hello, возникающие в CSV-файлы могут быть хранилища больших двоичных объектов tooAzure выходных данных или хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="1955c-220">Найти число hello medallions и уникальный номер medallions:</span><span class="sxs-lookup"><span data-stu-id="1955c-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1955c-221">Определите медальоны, которые принадлежат такси, осуществившим более 100 поездок:</span><span class="sxs-lookup"><span data-stu-id="1955c-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1955c-222">Найдите записи, недопустимые в отношении pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="1955c-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1955c-223">Найдите отсутствующие значения некоторых переменных:</span><span class="sxs-lookup"><span data-stu-id="1955c-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="1955c-224"><a name="explore"></a>Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="1955c-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="1955c-225">Мы можем некоторые tooget исследования данных лучше понять hello данных.</span><span class="sxs-lookup"><span data-stu-id="1955c-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="1955c-226">Найти распространения hello скошенные и не чаевых оставил зависимости приема-передачи данных:</span><span class="sxs-lookup"><span data-stu-id="1955c-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1955c-227">Найти hello распределение суммы подсказка со значениями среза: 0,5,10 и 20 долларов.</span><span class="sxs-lookup"><span data-stu-id="1955c-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1955c-228">Получите базовые статистические данные о расстоянии поездок:</span><span class="sxs-lookup"><span data-stu-id="1955c-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="1955c-229">Найти процентилем hello trip расстояния:</span><span class="sxs-lookup"><span data-stu-id="1955c-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="1955c-230"><a name="join"></a>Объединение таблиц trip и fare</span><span class="sxs-lookup"><span data-stu-id="1955c-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="1955c-231">Таблицы trip и fare можно объединить по medallion, hack_license и pickup_time.</span><span class="sxs-lookup"><span data-stu-id="1955c-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="1955c-232">Для каждого уровня пассажира число рассчитайте hello количество записей, среднюю сумму чаевых, дисперсия суммы совет, процент скошенные приема-передачи данных.</span><span class="sxs-lookup"><span data-stu-id="1955c-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="1955c-233"><a name="sample"></a>Выборка данных</span><span class="sxs-lookup"><span data-stu-id="1955c-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="1955c-234">Сначала мы случайным образом выбрать 0,1% hello данных из hello соединяемую таблицу:</span><span class="sxs-lookup"><span data-stu-id="1955c-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="1955c-235">Затем мы выполним стратифицированную выборку по двоичной переменной tip_class:</span><span class="sxs-lookup"><span data-stu-id="1955c-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="1955c-236"><a name="run"></a>Выполнение заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="1955c-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="1955c-237">После завершения редактирования скриптов U-SQL, вы можете отправить их toohello сервера с помощью учетной записи аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="1955c-238">Выберите вкладку **Data Lake**, щелкните **Отправить задание**, а затем выберите свою учетную запись в поле **Analytics Account** (Учетная запись Аналитики), значение параметра **Параллелизм** и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1955c-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="1955c-240">Когда успешно проверьте соответствие задания hello hello состояние задания отображается в Visual Studio для наблюдения.</span><span class="sxs-lookup"><span data-stu-id="1955c-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="1955c-241">После завершения задания hello, вы можете даже воспроизведения hello задания процесс выполнения и узнать hello возникать узкие места действия tooimprove эффективность работы.</span><span class="sxs-lookup"><span data-stu-id="1955c-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="1955c-242">Вы можете перейти tooAzure портала toocheck hello состояния заданий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="1955c-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13.](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="1955c-245">Теперь можно проверить hello выходные файлы в хранилище больших двоичных объектов Azure или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="1955c-246">Мы используем данные образца hello стратифицированным для наших моделирования в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="1955c-249">Создание и развертывание моделей в Машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="1955c-250">Продемонстрированы два параметра, доступные для вас данных toopull в toobuild машинного обучения Azure и</span><span class="sxs-lookup"><span data-stu-id="1955c-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="1955c-251">В hello первый вариант — использовать hello выборки данных, написанных tooan больших двоичных объектов Azure (в hello **выборки данных** шага выше) и использовать Python toobuild и развертывания модели на основе машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="1955c-252">В случае второй hello запрос hello данных Озера данных Azure непосредственно с помощью запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="1955c-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="1955c-253">Этот параметр требует создания нового кластера HDInsight или использовать существующий кластер HDInsight, где hello Hive таблиц данных такси NY toohello точки в хранилище Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="1955c-254">Мы рассмотрим оба варианта ниже.</span><span class="sxs-lookup"><span data-stu-id="1955c-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="1955c-255">Вариант 1: Использование Python toobuild и развертывания моделей машинного обучения</span><span class="sxs-lookup"><span data-stu-id="1955c-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="1955c-256">toobuild и развертывания моделей машинного обучения с помощью Python, создайте записной книжке Jupyter на локальном компьютере или в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="1955c-257">Hello книжке Jupyter представленные на [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) содержит Здравствуйте tooexplore весь код, визуализация данных, конструируются, моделирования и развертывания.</span><span class="sxs-lookup"><span data-stu-id="1955c-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="1955c-258">В этой статье показано, просто hello моделирования и развертывания.</span><span class="sxs-lookup"><span data-stu-id="1955c-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="1955c-259">Импорт библиотек Python</span><span class="sxs-lookup"><span data-stu-id="1955c-259">Import Python libraries</span></span>
<span data-ttu-id="1955c-260">В порядке toorun hello образец книжке Jupyter или Здравствуйте файл сценария Python, hello Python требуются следующие пакеты.</span><span class="sxs-lookup"><span data-stu-id="1955c-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="1955c-261">При использовании hello записной книжки AzureML службы были установлены эти пакеты.</span><span class="sxs-lookup"><span data-stu-id="1955c-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="1955c-262">Чтение данных hello из большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="1955c-262">Read in hello data from blob</span></span>
* <span data-ttu-id="1955c-263">Строка подключения</span><span class="sxs-lookup"><span data-stu-id="1955c-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="1955c-264">Считайте данные в качестве текста:</span><span class="sxs-lookup"><span data-stu-id="1955c-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="1955c-266">Добавьте имена столбцов и отделите столбцы:</span><span class="sxs-lookup"><span data-stu-id="1955c-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="1955c-267">Изменить некоторые столбцы toonumeric</span><span class="sxs-lookup"><span data-stu-id="1955c-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="1955c-268">Создание моделей машинного обучения</span><span class="sxs-lookup"><span data-stu-id="1955c-268">Build machine learning models</span></span>
<span data-ttu-id="1955c-269">Здесь мы создаем модель двоичной классификации toopredict ли trip Подрезанный, или нет.</span><span class="sxs-lookup"><span data-stu-id="1955c-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="1955c-270">В записной книжке Jupyter hello можно найти другие две модели: мультиклассовой классификации и моделями регрессии.</span><span class="sxs-lookup"><span data-stu-id="1955c-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="1955c-271">Сначала мы должны toocreate фиктивный переменные, которые могут использоваться в scikit-узнать моделей</span><span class="sxs-lookup"><span data-stu-id="1955c-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="1955c-272">Создайте кадр данных для моделирования hello</span><span class="sxs-lookup"><span data-stu-id="1955c-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="1955c-273">Обучите и протестируйте разбиение на 60/40:</span><span class="sxs-lookup"><span data-stu-id="1955c-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="1955c-274">Получите логистическую регрессию в обучающем наборе:</span><span class="sxs-lookup"><span data-stu-id="1955c-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="1955c-275">Оцените тестируемый набор данных:</span><span class="sxs-lookup"><span data-stu-id="1955c-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="1955c-276">Выполните вычисление метрик оценки:</span><span class="sxs-lookup"><span data-stu-id="1955c-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="1955c-277">Создание API веб-службы и его использование в Python</span><span class="sxs-lookup"><span data-stu-id="1955c-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="1955c-278">Мы хотим toooperationalize hello модели машинного обучения после его построения.</span><span class="sxs-lookup"><span data-stu-id="1955c-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="1955c-279">Здесь в качестве примера мы используем двоичная модель логистической hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="1955c-280">Убедитесь, что scikit hello-сведения о версии в локальном компьютере 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="1955c-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="1955c-281">Не нужно tooworry об этом при использовании службы Azure ML studio.</span><span class="sxs-lookup"><span data-stu-id="1955c-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="1955c-282">Найдите учетные данные своей рабочей области в настройках Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="1955c-283">В Студии машинного обучения Azure выберите **Параметры** --> **Имя** --> **Authorization Tokens** (Маркеры авторизации).</span><span class="sxs-lookup"><span data-stu-id="1955c-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="1955c-285">Создайте веб-службу:</span><span class="sxs-lookup"><span data-stu-id="1955c-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="1955c-286">Получите учетные данные веб-службы:</span><span class="sxs-lookup"><span data-stu-id="1955c-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="1955c-287">Вызовите API веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1955c-287">Call Web service API.</span></span> <span data-ttu-id="1955c-288">У вас есть toowait 5-10 секунд после выполнения предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="1955c-289">Вариант 2. Создание и развертывание моделей прямо в Машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="1955c-290">Студия машинного обучения можно считывать данные непосредственно из хранилища Озера данных Azure и используется toocreate и развертывания моделей.</span><span class="sxs-lookup"><span data-stu-id="1955c-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="1955c-291">Этот подход использует таблицу Hive, которая указывает на hello хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="1955c-292">Для этого необходимо подготовить отдельный кластер Azure HDInsight, на какие hello Hive создается таблица.</span><span class="sxs-lookup"><span data-stu-id="1955c-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="1955c-293">Здравствуйте, следующие разделы Показать как toodo это.</span><span class="sxs-lookup"><span data-stu-id="1955c-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="1955c-294">Создание кластера HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="1955c-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="1955c-295">Создание кластера HDInsight (Linux) из hello [портала Azure](http://portal.azure.com). Дополнительные сведения см. в разделе hello **создать кластер HDInsight с tooAzure доступа хранилища Озера данных** статьи [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1955c-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="1955c-297">Создание таблицы Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="1955c-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="1955c-298">Теперь создадим toobe таблицы Hive используется в студии машинного обучения Azure в кластере HDInsight hello на hello данные, хранящиеся в хранилище Озера данных Azure hello предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="1955c-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="1955c-299">Go toohello только что созданный кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1955c-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="1955c-300">Нажмите кнопку **параметры** --> **свойства** --> **кластера удостоверений AAD** --> **доступом ADLS**, Убедитесь, что учетная запись хранилища Озера данных Azure добавляется в список hello чтение, запись и выполнение права.</span><span class="sxs-lookup"><span data-stu-id="1955c-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="1955c-302">Нажмите кнопку **мониторинга** Далее toohello **параметры** кнопка и окно появится всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="1955c-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="1955c-303">Нажмите кнопку **Hive представление** в hello в правом верхнем углу страницы приветствия и вы увидите hello **редактора запросов**.</span><span class="sxs-lookup"><span data-stu-id="1955c-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="1955c-306">Вставьте следующие toocreate скрипты Hive hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="1955c-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="1955c-307">Hello источник данных находится в хранилище Озера данных Azure ссылке таким образом: **adl://data_lake_store_name.azuredatalakestore.net:443/имя_папки/имя_файла**.</span><span class="sxs-lookup"><span data-stu-id="1955c-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="1955c-308">По завершении выполнения запроса hello вы увидите результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1955c-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="1955c-310">Создание и развертывание моделей в Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="1955c-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="1955c-311">Мы теперь готовы toobuild и развернуть модель, которая прогнозирует, оплачивается ли подсказка с машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="1955c-312">Hello стратифицированной выборки данных будет готова toobe, используемых в этой двоичной классификации (Совет или нет) проблему.</span><span class="sxs-lookup"><span data-stu-id="1955c-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="1955c-313">Здравствуйте, прогнозных моделей мультиклассовой классификации (tip_class) с помощью регрессии (tip_amount) можно также следует создавать и развертывать с студии машинного обучения Azure, а здесь только показано, как с помощью варианта toohandle hello hello модель двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="1955c-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="1955c-314">Получение данных hello в Azure ML с помощью hello **импорта данных** модуля, доступные в hello **ввод и вывод данных** раздела.</span><span class="sxs-lookup"><span data-stu-id="1955c-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="1955c-315">Дополнительные сведения см. в разделе hello [модуль импорта данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) справочной странице.</span><span class="sxs-lookup"><span data-stu-id="1955c-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="1955c-316">Выберите **запроса Hive** как hello **источника данных** в hello **свойства** панель.</span><span class="sxs-lookup"><span data-stu-id="1955c-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="1955c-317">Следующий скрипт Hive в hello hello вставить **запроса базы данных Hive** редактора</span><span class="sxs-lookup"><span data-stu-id="1955c-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="1955c-318">Введите hello URI HDInsight кластера (это можно найти на портале Azure), учетные данные Hadoop, расположение выходных данных и имя контейнера или ключа и имени учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="1955c-320">Пример эксперимента двоичной классификации, чтение данных из таблицы Hive показан в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="1955c-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="1955c-322">После создания эксперимента hello щелкните **настройки веб-службы** --> **прогнозной веб-службы**</span><span class="sxs-lookup"><span data-stu-id="1955c-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="1955c-324">Оценки экспериментов, по окончании нажмите кнопку выполнения hello автоматически создается **развертывание веб-службы**</span><span class="sxs-lookup"><span data-stu-id="1955c-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="1955c-326">скоро будет отображаться Hello мониторинга веб-службы:</span><span class="sxs-lookup"><span data-stu-id="1955c-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="1955c-328">Сводка</span><span class="sxs-lookup"><span data-stu-id="1955c-328">Summary</span></span>
<span data-ttu-id="1955c-329">После завершения этого пошагового руководства у вас будет создана среда анализа данных для создания всеобъемлющих масштабируемых решений озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1955c-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="1955c-330">Эта среда была используется tooanalyze большого открытого набора данных, сделав hello канонические шагов по hello процесса обработки и анализа данных, от получения данных через Обучение модели и развертывания toohello hello моделирование веб-службы.</span><span class="sxs-lookup"><span data-stu-id="1955c-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="1955c-331">U-SQL была используется tooprocess, исследовать и образец hello данных.</span><span class="sxs-lookup"><span data-stu-id="1955c-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="1955c-332">Python и Hive использовались в студии машинного обучения Azure toobuild и развернуть прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="1955c-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="1955c-333">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="1955c-333">What's next?</span></span>
<span data-ttu-id="1955c-334">Схема обучения для Hello [процесса обработки и анализа данных Team (TDSP)](http://aka.ms/datascienceprocess) предоставляет ссылки tootopics описание каждого шага в hello advanced analytics процесса.</span><span class="sxs-lookup"><span data-stu-id="1955c-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="1955c-335">Существует ряд пошаговых руководств, перечислено на hello [пошаговые руководства процесса обработки и анализа данных командного](data-science-process-walkthroughs.md) как страница этой демонстрации toouse ресурсов и служб в различных сценариях прогнозной аналитики:</span><span class="sxs-lookup"><span data-stu-id="1955c-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="1955c-336">Hello командного процесса обработки и анализа данных в действии: с помощью хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="1955c-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="1955c-337">Hello командного процесса обработки и анализа данных в действии: с использованием кластеров HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="1955c-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="1955c-338">Hello командного процесса обработки и анализа данных: с помощью SQL Server</span><span class="sxs-lookup"><span data-stu-id="1955c-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="1955c-339">Общие сведения об использовании процесса обработки и анализа данных hello усилить на Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1955c-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

