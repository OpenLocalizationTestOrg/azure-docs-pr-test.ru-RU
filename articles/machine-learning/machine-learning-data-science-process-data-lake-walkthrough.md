---
title: "Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake | Документация Майкрософт"
description: "В этой статье описано, как выполнять задания по исследованию и двоичной классификации данных на основе набора данных озера данных Azure."
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
ms.openlocfilehash: 34fbe99572b4a6cee73de6ae5412a0ec09dd1ccc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="d3ee7-103">Полное пошаговое руководство по масштабируемому анализу данных с помощью Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d3ee7-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="d3ee7-104">В этом пошаговом руководстве на примере набора данных о поездках и тарифах такси в Нью-Йорке показано, как использовать озеро данных Azure для выполнения задач по исследованию и двоичной классификации данных, чтобы спрогнозировать вероятность получения чаевых за поездку.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-104">This walkthrough shows how to use Azure Data Lake to do data exploration and binary classification tasks on a sample of the NYC taxi trip and fare dataset to predict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="d3ee7-105">Здесь подробно описаны шаги [процесса обработки и анализа данных группы](http://aka.ms/datascienceprocess)— от получения данных для обучения модели и до развертывания веб-службы, которая публикует модель.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-105">It walks you through the steps of the [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition to model training, and then to the deployment of a web service that publishes the model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="d3ee7-106">Аналитика озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="d3ee7-107">[Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) предусматривает все необходимые возможности для аналитиков, упрощающие хранение данных любого размера, формата и скорости обработки и обеспечивающие высокую гибкость и экономичность обработки данных, углубленной аналитики и создания моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-107">The [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all the capabilities required to make it easy for data scientists to store data of any size, shape and speed, and to conduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="d3ee7-108">Плата взимается за задание, и только если данные обработаны фактически.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="d3ee7-109">Аналитика озера данных Azure предполагает использование U-SQL, языка, который объединяет декларативную природу SQL с выразительностью C#, чтобы позволить создавать масштабируемые распределенные запросы.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-109">Azure Data Lake Analytics includes U-SQL, a language that blends the declarative nature of SQL with the expressive power of C# to provide scalable distributed query capability.</span></span> <span data-ttu-id="d3ee7-110">Она позволяет обрабатывать неструктурированные данные, применяя схему для чтения, вставки пользовательской логики и определяемых пользователем функций (UDF), и предполагает возможности расширения, обеспечивающие точный контроль над выполнением в масштабе.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-110">It enables you to process unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility to enable fine grained control over how to execute at scale.</span></span> <span data-ttu-id="d3ee7-111">Дополнительные сведения о принципах разработки U-SQL см. в [записи блога о Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-111">To learn more about the design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="d3ee7-112">Аналитика озера данных — это также ключевая часть Cortana Analytics Suite. Она поддерживает работу с хранилищем данных SQL Azure, Power BI и фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="d3ee7-113">Это создает всеобъемлющую облачную платформу для работы с большими данными и углубленной аналитики.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="d3ee7-114">Пошаговое руководство начинается с описания необходимых компонентов, а также ресурсов, которые требуются для выполнения задач с использованием Аналитики озера данных, лежащих в основе анализа данных.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-114">This walkthrough begins by describing the prerequisites and resources that are needed to complete the tasks with Data Lake Analytics that form the data science process and how to install them.</span></span> <span data-ttu-id="d3ee7-115">Затем здесь описаны шаги по обработке данных, выполняемые с использованием U-SQL. В конце статьи показано, как использовать Python и Hive со студией машинного обучения Azure для создания и развертывания прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-115">Then it outlines the data processing steps using U-SQL and concludes by showing how to use Python and Hive with Azure Machine Learning Studio to build and deploy the predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="d3ee7-116">U-SQL и Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3ee7-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="d3ee7-117">В этом пошаговом руководстве рекомендуется использовать Visual Studio, чтобы изменять сценарии U-SQL для обработки набора данных.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-117">This walkthrough recommends using Visual Studio to edit U-SQL scripts to process the dataset.</span></span> <span data-ttu-id="d3ee7-118">Сценарии U-SQL, описанные в документе, приводятся в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-118">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="d3ee7-119">Процесс включает в себя прием, исследование и выборку данных.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-119">The process includes ingesting, exploring, and sampling the data.</span></span> <span data-ttu-id="d3ee7-120">Также здесь показывается, как выполнить задание со сценарием U-SQL на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-120">It also shows how to run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="d3ee7-121">Для данных в связанном кластере HDInsight создаются таблицы Hive, которые упрощают сборку и развертывание модели двоичной классификации в Студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-121">Hive tables are created for the data in an associated HDInsight cluster to facilitate the building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="d3ee7-122">Python</span><span class="sxs-lookup"><span data-stu-id="d3ee7-122">Python</span></span>
<span data-ttu-id="d3ee7-123">В этом пошаговом руководстве также содержится раздел, в котором показано, как создавать и развертывать прогнозную модель с помощью Python и студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-123">This walkthrough also contains a section that shows how to build and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="d3ee7-124">Мы предоставили записную книжку Jupyter со сценариями Python для шагов в этом процессе.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-124">We provide a Jupyter notebook with the Python scripts for these steps in this process.</span></span> <span data-ttu-id="d3ee7-125">Этот Notebook включает в себя код для некоторых дополнительных шагов проектирования признаков и создания моделей, например многоклассовой классификации и регрессии, в дополнение к модели двоичной классификации, описанной здесь.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-125">The notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition to the binary classification model outlined here.</span></span> <span data-ttu-id="d3ee7-126">Задача регрессии: спрогнозировать сумму чаевых в зависимости от других признаков.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-126">The regression task is to predict the amount of the tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="d3ee7-127">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-127">Azure Machine Learning</span></span>
<span data-ttu-id="d3ee7-128">Студия машинного обучения Azure используется для создания и развертывания прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-128">Azure Machine Learning Studio is used to build and deploy the predictive models.</span></span> <span data-ttu-id="d3ee7-129">Для этого используется два подхода: первый — с помощью сценариев Python, а второй — с использованием таблиц Hive на кластере HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="d3ee7-130">Сценарии</span><span class="sxs-lookup"><span data-stu-id="d3ee7-130">Scripts</span></span>
<span data-ttu-id="d3ee7-131">В этом пошаговом руководстве описаны только основные шаги.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-131">Only the principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="d3ee7-132">Вы можете скачать полный **скрипт U-SQL**, а также **записную книжку Jupyter** из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-132">You can download the full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3ee7-133">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3ee7-133">Prerequisites</span></span>
<span data-ttu-id="d3ee7-134">Прежде чем начать работу по этим разделам, необходимо обеспечить наличие следующего:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-134">Before you begin these topics, you must have the following:</span></span>

* <span data-ttu-id="d3ee7-135">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-135">An Azure subscription.</span></span> <span data-ttu-id="d3ee7-136">Если у вас ее нет, см. статью [о получении бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d3ee7-137">[Рекомендуется] Visual Studio 2013 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="d3ee7-138">Если вы еще не установили одну из этих версий, можно скачать бесплатную версию Community с сайта [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="d3ee7-139">Чтобы отправлять запросы озера данных Azure, вместо Visual Studio можно также использовать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-139">Instead of Visual Studio, you can also use the Azure Portal to submit Azure Data Lake queries.</span></span> <span data-ttu-id="d3ee7-140">Инструкции о том, как сделать это с помощью Visual Studio и на портале, см. в разделе **Обработка данных с использованием U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-140">We will provide instructions on how to do so both with Visual Studio and on the portal in the section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="d3ee7-141">Подготовка среды анализа данных для озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="d3ee7-142">Чтобы подготовить среду анализа данных для этого пошагового руководства, создайте следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-142">To prepare the data science environment for this walkthrough, create the following resources:</span></span>

* <span data-ttu-id="d3ee7-143">хранилище озера данных Azure;</span><span class="sxs-lookup"><span data-stu-id="d3ee7-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="d3ee7-144">Аналитику озера данных Azure;</span><span class="sxs-lookup"><span data-stu-id="d3ee7-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="d3ee7-145">учетную запись хранения BLOB-объектов;</span><span class="sxs-lookup"><span data-stu-id="d3ee7-145">Azure Blob storage account</span></span>
* <span data-ttu-id="d3ee7-146">учетную запись Студии машинного обучения Azure;</span><span class="sxs-lookup"><span data-stu-id="d3ee7-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="d3ee7-147">средства озера данных Azure для Visual Studio (рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="d3ee7-148">Этот раздел содержит указания о том, как создать каждый из этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-148">This section provides instructions on how to create each of these resources.</span></span> <span data-ttu-id="d3ee7-149">Если для создания модели вы решили вместо Python использовать таблицы Hive с Машинным обучением Azure, то необходимо также подготовить кластер HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-149">If you choose to use Hive tables with Azure Machine Learning, instead of Python, to build a model,you will also need to provision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="d3ee7-150">Этот альтернативный способ описан в соответствующем разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-150">This alternative procedure in described in the appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="d3ee7-151">**Azure Data Lake Store** можно создать отдельно или вместе с **Azure Data Lake Analytics** в качестве хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-151">The **Azure Data Lake Store** can be created either separately or when you create the **Azure Data Lake Analytics** as the default storage.</span></span> <span data-ttu-id="d3ee7-152">Указания по созданию каждого из этих ресурсов приведены по отдельности ниже, но учетную запись хранения Data Lake не требуется создавать отдельно.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-152">Instructions are referenced for creating each of these resources separately below, but the Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="d3ee7-153">Создание хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="d3ee7-154">Создайте ADLS на [портале Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-154">Create an ADLS from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="d3ee7-155">Дополнительные сведения см. в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="d3ee7-156">Обязательно настройте удостоверение кластера AAD в колонке **Источник данных** колонки **Необязательная конфигурация**, показанной здесь.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-156">Be sure to set up the Cluster AAD Identity in the **DataSource** blade of the **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="d3ee7-158">Создание учетной записи Аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="d3ee7-159">Создайте учетную запись ADLA на [портале Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-159">Create an ADLA account from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="d3ee7-160">Дополнительные сведения см. в статье [Руководство. Начало работы с Azure Data Lake Analytics с помощью портала Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="d3ee7-162">Создание учетной записи хранения BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="d3ee7-163">Создайте учетную запись хранилища BLOB-объектов Azure на [портале Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-163">Create an Azure Blob storage account from the [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="d3ee7-164">Дополнительные сведения см. в разделе "Создайте учетную запись хранения" в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-164">For details, see the Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="d3ee7-166">Настройка учетной записи Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="d3ee7-167">Войдите в студию машинного обучения со страницы [Машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) .</span><span class="sxs-lookup"><span data-stu-id="d3ee7-167">Sign up/into Azure Machine Learning Studio from the [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="d3ee7-168">Нажмите кнопку **Начните прямо сейчас** и выберите Free Workspace ("Бесплатная рабочая область") или Standard Workspace ("Стандартная рабочая область").</span><span class="sxs-lookup"><span data-stu-id="d3ee7-168">Click on the **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="d3ee7-169">После этого в Студии машинного обучения Azure можно будет создавать эксперименты.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-169">After this you will be able to create experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="d3ee7-170">Установка инструментов озера данных Azure [рекомендуется]</span><span class="sxs-lookup"><span data-stu-id="d3ee7-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="d3ee7-171">Установите инструменты озера данных Azure в зависимости от своей версии Visual Studio со страницы [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)(Инструменты озера данных Azure для Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="d3ee7-173">После успешного завершения установки откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-173">After the installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="d3ee7-174">Вы должны увидеть вкладку Data Lake ("Озеро данных") в меню вверху.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-174">You should see the Data Lake tab the menu at the top.</span></span> <span data-ttu-id="d3ee7-175">Ресурсы Azure должны отобразиться на левой панели при входе в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-175">Your Azure resources should appear in the left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="the-nyc-taxi-trips-dataset"></a><span data-ttu-id="d3ee7-177">Набор данных "Поездки такси Нью-Йорка"</span><span class="sxs-lookup"><span data-stu-id="d3ee7-177">The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="d3ee7-178">Здесь мы использовали общедоступный набор данных [Поездки такси Нью-Йорка](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-178">The data set we used here is a publicly available dataset -- the [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="d3ee7-179">Данные о поездках такси Нью-Йорка содержатся в сжатых CSV-файлах размером около 20 ГБ (примерно 48 ГБ в несжатом виде), которые включают в себя сведения о более 173 млн отдельных поездок и платежах за каждую поездку.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-179">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="d3ee7-180">В каждой записи о поездке содержатся данные о расположении пунктов посадки и высадки, а также времени, анонимизированный номер лицензии водителя и номер медальона (уникальный идентификатор такси).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-180">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="d3ee7-181">Данные включают в себя все поездки за 2013 год и предоставляются в виде следующих двух наборов данных за каждый месяц:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-181">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

* <span data-ttu-id="d3ee7-182">CSV-файл trip_data содержит подробную информацию о поездке, например число пассажиров, пункты отправления и назначения, продолжительность поездки и ее расстояние.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-182">The 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="d3ee7-183">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="d3ee7-184">CSV-файл trip_fare содержит подробную информацию об оплате каждой поездки, такие как тип оплаты, сумма тарифа, надбавка и налоги, чаевые и пошлины, а также общая выплаченная сумма.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-184">The 'trip_fare' CSV contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="d3ee7-185">Вот несколько примеров записей:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="d3ee7-186">Уникальный ключ для объединения trip\_data и trip\_fare состоит из следующих трех полей: medallion, hack\_license и pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-186">The unique key to join trip\_data and trip\_fare is composed of the following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="d3ee7-187">Необработанные файлы в формате CSV можно получать из общедоступных больших двоичных объектов хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-187">The raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="d3ee7-188">Сценарий U-SQL для этого объединения находится в разделе [Объединение таблиц trip и fare](#join) .</span><span class="sxs-lookup"><span data-stu-id="d3ee7-188">The U-SQL script for this join is in the [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="d3ee7-189">Обработка данных с использованием U-SQL</span><span class="sxs-lookup"><span data-stu-id="d3ee7-189">Process data with U-SQL</span></span>
<span data-ttu-id="d3ee7-190">Задачи обработки данных в этом разделе предусматривают прием, проверку качества, исследование и выборку данных.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-190">The data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling the data.</span></span> <span data-ttu-id="d3ee7-191">Здесь также показано, как объединить таблицы trip и fare.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-191">We also show how to join trip and fare tables.</span></span> <span data-ttu-id="d3ee7-192">В последнем разделе показано, как выполнить задание со сценарием U-SQL на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-192">The final section shows run a U-SQL scripted job from the Azure portal.</span></span> <span data-ttu-id="d3ee7-193">Ниже приведены ссылки на каждый подраздел.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-193">Here are links to each subsection:</span></span>

* [<span data-ttu-id="d3ee7-194">Прием данных: чтение из общедоступного большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="d3ee7-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="d3ee7-195">Проверка качества данных</span><span class="sxs-lookup"><span data-stu-id="d3ee7-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="d3ee7-196">Исследование данных</span><span class="sxs-lookup"><span data-stu-id="d3ee7-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="d3ee7-197">Объединение таблиц trip и fare</span><span class="sxs-lookup"><span data-stu-id="d3ee7-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="d3ee7-198">Выборка данных</span><span class="sxs-lookup"><span data-stu-id="d3ee7-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="d3ee7-199">Выполнение заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="d3ee7-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="d3ee7-200">Сценарии U-SQL, описанные в документе, приводятся в отдельном файле.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-200">The U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="d3ee7-201">Можно скачать полные **сценарии U-SQL** из [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-201">You can download the full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="d3ee7-202">Чтобы выполнить сценарий U-SQL, откройте Visual Studio, выберите **Файл --> Создать --> Проект**, щелкните **U-SQL Project** (Проект U-SQL), укажите имя и сохраните проект в папке.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-202">To execute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it to a folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="d3ee7-204">Для выполнения сценариев U-SQL вместо Visual Studio можно использовать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-204">It is possible to use the Azure Portal to execute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="d3ee7-205">Можно перейти к ресурсу "Аналитика озера данных Azure" на портале и отправить запросы напрямую, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-205">You can navigate to the Azure Data Lake Analytics resource on the portal and submit queries directly as illustrated in the following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="d3ee7-207"><a name="ingest"></a>Прием данных: чтение из общедоступного большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="d3ee7-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="d3ee7-208">Данные большого двоичного объекта Azure расположены по адресу **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**, и их можно извлечь, используя **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-208">The location of the data in the Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="d3ee7-209">В следующих скриптах подставьте имена своих контейнера и учетной записи хранения для container_name@blob_storage_account_name в адресе wasb.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in the wasb address.</span></span> <span data-ttu-id="d3ee7-210">Так как у имен файлов одинаковый формат, чтобы выполнить чтение всех 12 файлов поездок, можно использовать **trip\_data_{\*\}}.csv**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-210">Since the file names are in same format, we can use **trip\_data_{\*\}.csv** to read in all 12 trip files.</span></span> 

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

<span data-ttu-id="d3ee7-211">В первой строке есть заголовки, поэтому их необходимо удалить и изменить типы столбцов на соответствующие.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-211">Since there are headers in the first row, we need to remove the headers and change column types into appropriate ones.</span></span> <span data-ttu-id="d3ee7-212">Обработанные данные можно сохранить в хранилище Azure Data Lake с помощью **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/имя_папки/имя_файла**_ или в учетной записи хранилища BLOB-объектов Azure с помощью **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-212">We can either save the processed data to Azure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or to Azure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

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

    ////output data to ADL
    OUTPUT @trip   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data to blob
    OUTPUT @trip   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="d3ee7-213">Аналогичным образом можно выполнить чтение наборов данных о тарифах.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-213">Similarly we can read in the fare data sets.</span></span> <span data-ttu-id="d3ee7-214">Щелкните Azure Data Lake Store правой кнопкой мыши и выберите **Портал Azure --> Обозреватель данных** или в среде Visual Studio используйте **проводник**, чтобы просмотреть данные.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-214">Right click Azure Data Lake Store, you can choose to look at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="d3ee7-217"><a name="quality"></a>Проверка качества данных</span><span class="sxs-lookup"><span data-stu-id="d3ee7-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="d3ee7-218">После считывания таблиц trip и fare можно проверить качество данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-218">After trip and fare tables have been read in, data quality checks can be done in the following way.</span></span> <span data-ttu-id="d3ee7-219">Полученные файлы в формате CSV можно поместить в хранилище BLOB-объектов Azure или хранилище озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-219">The resulting CSV files can be output to Azure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="d3ee7-220">Узнайте количество медальонов и их уникальные номера:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-220">Find the number of medallions and unique number of medallions:</span></span>

    ///check the number of medallions and unique number of medallions
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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d3ee7-221">Определите медальоны, которые принадлежат такси, осуществившим более 100 поездок:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d3ee7-222">Найдите записи, недопустимые в отношении pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d3ee7-223">Найдите отсутствующие значения некоторых переменных:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-223">Find missing values for some variables:</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="d3ee7-224"><a name="explore"></a>Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="d3ee7-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="d3ee7-225">Чтобы лучше узнать все аспекты данных, можно провести некоторые исследования.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-225">We can do some data exploration to get a better understanding of the data.</span></span>

<span data-ttu-id="d3ee7-226">Получите распределение поездок с чаевыми и без них:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-226">Find the distribution of tipped and non-tipped trips:</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d3ee7-227">Получите распределение сумм чаевых с пороговыми значениями: 0, 5, 10 и 20 долларов.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-227">Find the distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d3ee7-228">Получите базовые статистические данные о расстоянии поездок:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-228">Find basic statistics of trip distance:</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="d3ee7-229">Узнайте процентили расстояния поездок.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-229">Find the percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="d3ee7-230"><a name="join"></a>Объединение таблиц trip и fare</span><span class="sxs-lookup"><span data-stu-id="d3ee7-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="d3ee7-231">Таблицы trip и fare можно объединить по medallion, hack_license и pickup_time.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output to blob
    OUTPUT @model_data_full   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data to ADL
    OUTPUT @model_data_full   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="d3ee7-232">Вычислите количество записей, среднюю сумму чаевых, дисперсию суммы чаевых и процент поездок, за которые выплатили чаевые, для каждого уровня количества пассажиров.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-232">For each level of passenger count, calculate the number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="d3ee7-233"><a name="sample"></a>Выборка данных</span><span class="sxs-lookup"><span data-stu-id="d3ee7-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="d3ee7-234">Сначала мы случайным образом выберем 0,1 % данных из объединенной таблицы:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-234">First we randomly select 0.1% of the data from the joined table:</span></span>

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
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="d3ee7-235">Затем мы выполним стратифицированную выборку по двоичной переменной tip_class:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output to blob
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data to ADL
    OUTPUT @model_data_stratified_sample_1_1000   
    TO "swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="d3ee7-236"><a name="run"></a>Выполнение заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="d3ee7-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="d3ee7-237">Завершив редактировать сценарии U-SQL, вы можете отправить их на сервер, используя учетную запись Аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-237">When you finish editing U-SQL scripts, you can submit them to the server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="d3ee7-238">Выберите вкладку **Data Lake**, щелкните **Отправить задание**, а затем выберите свою учетную запись в поле **Analytics Account** (Учетная запись Аналитики), значение параметра **Параллелизм** и нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="d3ee7-240">Если задание будет выполнено успешно, его состояние отобразится в Visual Studio для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-240">When the job is complied successfully, the status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="d3ee7-241">После завершения задания можно даже воспроизвести его выполнение и определить, на каких шагах возникают узкие места, чтобы повысить эффективность работы.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-241">After the job finishes running, you can even replay the job execution process and find out the bottleneck steps to improve your job efficiency.</span></span> <span data-ttu-id="d3ee7-242">Вы также можете перейти на портал Azure, чтобы проверить состояние заданий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-242">You can also go to Azure Portal to check the status of your U-SQL jobs.</span></span>

 ![13.](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="d3ee7-245">Теперь можно проверить выходные файлы в хранилище BLOB-объектов или на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-245">Now you can check the output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="d3ee7-246">Данные стратифицированной выборки будут использоваться для моделирования на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-246">We will use the stratified sample data for our modeling in the next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="d3ee7-249">Создание и развертывание моделей в Машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="d3ee7-250">Мы продемонстрируем два доступных варианта извлечения данных в машинное обучение Azure для создания и развертывания моделей.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-250">We demonstrate two options available for you to pull data into Azure Machine Learning to build and</span></span> 

* <span data-ttu-id="d3ee7-251">Первый вариант предусматривает использование данных выборки, записанных в большой двоичный объект Azure (на шаге **Выборка данных** выше), и Python, чтобы создать и развернуть модели из Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-251">In the first option, you use the sampled data that has been written to an Azure Blob (in the **Data sampling** step above) and use Python to build and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="d3ee7-252">Второй вариант предполагает, что вы запрашиваете данные озера данных Azure напрямую с помощью запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-252">In the second option, you query the data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="d3ee7-253">При выборе такого варианта необходимо создать новый кластер HDInsight или использовать кластер HDInsight, который уже есть. Таблицы Hive кластера должны указывать на данные о такси Нью-Йорка в хранилище озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where the Hive tables point to the NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="d3ee7-254">Мы рассмотрим оба варианта ниже.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-to-build-and-deploy-machine-learning-models"></a><span data-ttu-id="d3ee7-255">Вариант 1. Использование Python для создания и развертывания моделей машинного обучения</span><span class="sxs-lookup"><span data-stu-id="d3ee7-255">Option 1: Use Python to build and deploy machine learning models</span></span>
<span data-ttu-id="d3ee7-256">Для создания и развертывания моделей машинного обучения, используя Python, создайте записную книжки Jupyter на локальном компьютере или в студии машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-256">To build and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="d3ee7-257">Записная книжка Jupyter, которая доступна на сайте [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough), содержит полный код для исследования и визуализации данных, проектирования признаков, моделирования и развертывания.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-257">The Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains the full code to explore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="d3ee7-258">В этой статье показываются шаги только по моделированию и развертыванию.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-258">In this article, we show just the modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="d3ee7-259">Импорт библиотек Python</span><span class="sxs-lookup"><span data-stu-id="d3ee7-259">Import Python libraries</span></span>
<span data-ttu-id="d3ee7-260">Чтобы запустить пример Jupyter Notebook или файл сценария Python, необходимо установить следующие пакеты Python.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-260">In order to run the sample Jupyter Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="d3ee7-261">Если вы используете службу Notebook Машинного обучения Azure, эти пакеты уже установлены.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-261">If you are using the AzureML Notebook service, these packages have been pre-installed.</span></span>

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


### <a name="read-in-the-data-from-blob"></a><span data-ttu-id="d3ee7-262">Считывание данных из большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="d3ee7-262">Read in the data from blob</span></span>
* <span data-ttu-id="d3ee7-263">Строка подключения</span><span class="sxs-lookup"><span data-stu-id="d3ee7-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="d3ee7-264">Считайте данные в качестве текста:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds to read in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="d3ee7-266">Добавьте имена столбцов и отделите столбцы:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="d3ee7-267">Измените значения в некоторых столбцах на числовые:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-267">Change some columns to numeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="d3ee7-268">Создание моделей машинного обучения</span><span class="sxs-lookup"><span data-stu-id="d3ee7-268">Build machine learning models</span></span>
<span data-ttu-id="d3ee7-269">В этом разделе мы создадим модель двоичной классификации, чтобы спрогнозировать вероятность получения чаевых за поездку.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-269">Here we build a binary classification model to predict whether a trip is tipped or not.</span></span> <span data-ttu-id="d3ee7-270">В Jupyter Notebook можно найти две другие модели: многоклассовой классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-270">In the Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="d3ee7-271">Сначала необходимо создать фиктивные переменные, которые можно использовать в моделях scikit-learn:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-271">First we need to create dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="d3ee7-272">Создайте кадр данных для моделирования:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-272">Create data frame for the modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="d3ee7-273">Обучите и протестируйте разбиение на 60/40:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="d3ee7-274">Получите логистическую регрессию в обучающем наборе:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="d3ee7-275">Оцените тестируемый набор данных:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="d3ee7-276">Выполните вычисление метрик оценки:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-276">Calculate Evaluation metrics</span></span>
  
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

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="d3ee7-277">Создание API веб-службы и его использование в Python</span><span class="sxs-lookup"><span data-stu-id="d3ee7-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="d3ee7-278">После создания модель машинного обучения необходимо ввести в эксплуатацию.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-278">We want to operationalize the machine learning model after it has been built.</span></span> <span data-ttu-id="d3ee7-279">Здесь в качестве примера мы используем двоичную логистическую модель.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-279">Here we use the binary logistic model as an example.</span></span> <span data-ttu-id="d3ee7-280">Убедитесь, что на локальном компьютере установлена версия scikit-learn 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-280">Make sure the scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="d3ee7-281">Если вы используете службу Студии машинного обучения Microsoft Azure, этого делать не нужно.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-281">You don't have to worry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="d3ee7-282">Найдите учетные данные своей рабочей области в настройках Студии машинного обучения Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="d3ee7-283">В Студии машинного обучения Azure выберите **Параметры** --> **Имя** --> **Authorization Tokens** (Маркеры авторизации).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="d3ee7-285">Создайте веб-службу:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="d3ee7-286">Получите учетные данные веб-службы:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="d3ee7-287">Вызовите API веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-287">Call Web service API.</span></span> <span data-ttu-id="d3ee7-288">После выполнения предыдущего шага нужно будет подождать 5–10 секунд.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-288">You have to wait 5-10 seconds after the previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="d3ee7-289">Вариант 2. Создание и развертывание моделей прямо в Машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="d3ee7-290">Студия машинного обучения Azure может считывать данные прямо из хранилища озера данных Azure, а затем использоваться для создания и развертывания моделей.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used to create and deploy models.</span></span> <span data-ttu-id="d3ee7-291">Этот подход использует таблицу Hive, которая указывает на хранилище озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-291">This approach uses a Hive table that points at the Azure Data Lake Store.</span></span> <span data-ttu-id="d3ee7-292">Для этого необходимо подготовить отдельный кластер Azure HDInsight, а в нем создать таблицу Hive.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-292">This requires that a separate Azure HDInsight cluster be provisioned, on which the Hive table is created.</span></span> <span data-ttu-id="d3ee7-293">В следующих разделах показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-293">The following sections show how to do this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="d3ee7-294">Создание кластера HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="d3ee7-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="d3ee7-295">Создайте кластер HDInsight (на платформе Linux) на [портале Azure](http://portal.azure.com). Дополнительные сведения см. в разделе **Создание кластера Azure HDInsight с доступом к Azure Data Lake Store** в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-295">Create an HDInsight Cluster (Linux) from the [Azure Portal](http://portal.azure.com).For details, see the **Create an HDInsight cluster with access to Azure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="d3ee7-297">Создание таблицы Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="d3ee7-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="d3ee7-298">Теперь мы создадим таблицы Hive, необходимые для студии машинного обучения Azure в кластере HDInsight, используя данные из хранилища озера данных Azure, сохраненные на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-298">Now we create Hive tables to be used in Azure Machine Learning Studio in the HDInsight cluster using the data stored in Azure Data Lake Store in the previous step.</span></span> <span data-ttu-id="d3ee7-299">Перейдите на только что созданный кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-299">Go to the HDInsight cluster just created.</span></span> <span data-ttu-id="d3ee7-300">Выберите **Параметры** --> **Свойства** --> **Удостоверение кластера AAD** --> **ADLS Access** (Доступ ADLS), убедитесь, что учетная запись Azure Data Lake Store добавлена в список и есть права на чтение, запись и выполнение.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in the list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="d3ee7-302">Щелкните **Панель мониторинга** рядом с кнопкой **Параметры**, и откроется новое окно.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-302">Then click **Dashboard** next to the **Settings** button and a window will pop up.</span></span> <span data-ttu-id="d3ee7-303">Щелкните **Представление Hive** в правом верхнем углу страницы, и вы увидите **Редактор запросов**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-303">Click **Hive View** in the upper right corner of the page and you will see the **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="d3ee7-306">Вставьте следующие сценарии Hive, чтобы создать таблицу.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-306">Paste in the following Hive scripts to create a table.</span></span> <span data-ttu-id="d3ee7-307">Источник данных находится в ссылке на Azure Data Lake Store в таком формате: **adl://data_lake_store_name.azuredatalakestore.net:443/имя_папки/имя_файла**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-307">The location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

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


<span data-ttu-id="d3ee7-308">После выполнения запроса отобразятся аналогичные результаты:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-308">When the query finishes running, you will see the results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="d3ee7-310">Создание и развертывание моделей в Студии машинного обучения Azure</span><span class="sxs-lookup"><span data-stu-id="d3ee7-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="d3ee7-311">Теперь все готово для создания и развертывания модели, с помощью которой можно спрогнозировать, будут ли выплачены чаевые за поездку, используя машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-311">We are now ready to build and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="d3ee7-312">Данные стратифицированной выборки готовы к использованию в этой задаче двоичной классификации (поездка с чаевыми или без чаевых).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-312">The stratified sample data is ready to be used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="d3ee7-313">Прогнозные модели, использующие многоклассовую классификацию (tip_class) и регрессию (tip_amount), также можно создавать и развертывать с помощью студии машинного обучения Azure, но здесь мы показываем только случай с использованием модели двоичной классификации.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-313">The predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how to handle the case using the binary classification model.</span></span>

1. <span data-ttu-id="d3ee7-314">Загрузите данные в Машинное обучение Azure, используя модуль **Импорт данных**, доступный в разделе **Ввод и вывод данных**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-314">Get the data into Azure ML using the **Import Data** module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="d3ee7-315">Дополнительные сведения см. на странице справки [Импорт данных](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-315">For more information, see the [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="d3ee7-316">Выберите значение **Hive Query** (Запрос Hive) для параметра **Источник данных** на панели **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-316">Select **Hive Query** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="d3ee7-317">Вставьте следующий сценарий Hive в редактор **Hive database query** (Запрос к базе данных Hive):</span><span class="sxs-lookup"><span data-stu-id="d3ee7-317">Paste the following Hive script in the **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="d3ee7-318">Введите универсальный код ресурса (URI) кластера HDInsight (его можно найти на портале Azure), учетные данные Hadoop, расположение выходных данных и имя контейнера, ключа или учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-318">Enter the URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="d3ee7-320">На рисунке ниже показан пример эксперимента по двоичной классификации, который связан с чтением данных из таблицы Hive.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-320">An example of a binary classification experiment reading data from Hive table is shown in the figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="d3ee7-322">После создания эксперимента выберите **Set Up Web Service** -->  (Настройка веб-службы) **Predictive Web Service** (Прогнозная веб-служба).</span><span class="sxs-lookup"><span data-stu-id="d3ee7-322">After the experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="d3ee7-324">Запустите автоматически созданный оценивающий эксперимент, а по его завершении нажмите кнопку **Deploy Web Service**</span><span class="sxs-lookup"><span data-stu-id="d3ee7-324">Run the automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="d3ee7-326">Вскоре отобразится панель мониторинга веб-службы:</span><span class="sxs-lookup"><span data-stu-id="d3ee7-326">The web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="d3ee7-328">Сводка</span><span class="sxs-lookup"><span data-stu-id="d3ee7-328">Summary</span></span>
<span data-ttu-id="d3ee7-329">После завершения этого пошагового руководства у вас будет создана среда анализа данных для создания всеобъемлющих масштабируемых решений озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="d3ee7-330">Эта среда использовалась для анализа большого набора данных, в отношении которого выполнены ключевые шаги по обработке данных — от получения данных и обучения модели до развертывания модели в качестве веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-330">This environment was used to analyze a large public dataset, taking it through the canonical steps of the Data Science Process, from data acquisition through model training, and then to the deployment of the model as a web service.</span></span> <span data-ttu-id="d3ee7-331">Язык U-SQL использовался для обработки, просмотра и выборки данных.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-331">U-SQL was used to process, explore and sample the data.</span></span> <span data-ttu-id="d3ee7-332">Python и Hive использовались со студией машинного обучения Azure для создания и развертывания прогнозных моделей.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-332">Python and Hive were used with Azure Machine Learning Studio to build and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="d3ee7-333">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="d3ee7-333">What's next?</span></span>
<span data-ttu-id="d3ee7-334">Схема обучения для [процесса обработки и анализа данных группы (TDSP)](http://aka.ms/datascienceprocess) содержит ссылки на разделы, описывающие каждый шаг в процессе расширенной аналитики.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-334">The learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links to topics describing each step in the advanced analytics process.</span></span> <span data-ttu-id="d3ee7-335">Существует ряд пошаговых руководств, упорядоченных на странице [Пошаговые руководства по процессу обработки и анализа данных](data-science-process-walkthroughs.md) , которые демонстрируют, как использовать ресурсы и службы в различных сценариях прогнозной аналитики.</span><span class="sxs-lookup"><span data-stu-id="d3ee7-335">There are a series of walkthroughs itemized on the [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how to use resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="d3ee7-336">Процесс обработки и анализа данных группы на практике: использование хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="d3ee7-336">The Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="d3ee7-337">Процесс обработки и анализа данных группы на практике: использование кластеров HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="d3ee7-337">The Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="d3ee7-338">Процесс обработки и анализа данных группы на практике: использование SQL Server</span><span class="sxs-lookup"><span data-stu-id="d3ee7-338">The Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="d3ee7-339">Общие сведения об обработке и анализе данных с помощью платформы Spark в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d3ee7-339">Overview of the Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

