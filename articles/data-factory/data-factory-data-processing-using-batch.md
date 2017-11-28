---
title: "Обработка больших наборов данных с использованием фабрики данных и пакетной службы | Документация Майкрософт"
description: "Содержит описание процесса обработки больших объемов данных в конвейере фабрики данных Azure с использованием возможности параллельной обработки пакетной службы Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 9defbf7a6a515740fa3b3cb1c67a2f5f9d9baa01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="3912a-103">Обработка больших наборов данных с помощью фабрики данных и пакетной службы</span><span class="sxs-lookup"><span data-stu-id="3912a-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="3912a-104">В этой статье описывается архитектура простого решения, которое автоматически и по расписанию перемещает и обрабатывает большие наборы данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="3912a-105">Здесь также предоставлено полное пошаговое руководство по реализации решения с помощью фабрики данных Azure и пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="3912a-106">Эта статья длиннее обычной статьи, так как в ней содержится пошаговое руководство для всего примера решения.</span><span class="sxs-lookup"><span data-stu-id="3912a-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="3912a-107">Если вы впервые используете пакетную службу и фабрику данных, здесь вы можете узнать об этих службах и их совместном использовании.</span><span class="sxs-lookup"><span data-stu-id="3912a-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="3912a-108">Если вы немного знакомы с этими службами и проектируете решение, то можете сосредоточиться только на [разделе об архитектуре](#architecture-of-sample-solution). Если вы разрабатываете прототип или решение, то можете попытаться выполнить пошаговые инструкции из приведенного [руководства](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="3912a-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="3912a-109">Мы приветствуем ваши комментарии об этой статье и использовании ее содержимого.</span><span class="sxs-lookup"><span data-stu-id="3912a-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="3912a-110">Сначала давайте рассмотрим, как фабрика данных и пакетная служба могут быть полезны для обработки больших наборов данных в облаке.</span><span class="sxs-lookup"><span data-stu-id="3912a-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="3912a-111">Сведения о пакетной службе Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-111">Why Azure Batch?</span></span>
<span data-ttu-id="3912a-112">Пакетная служба Azure позволяет эффективно запускать приложения, выполняющие крупномасштабные параллельные вычислительные задания с высокой производительностью, в облаке.</span><span class="sxs-lookup"><span data-stu-id="3912a-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="3912a-113">Это служба платформы, которая планирует запуск ресурсоемких вычислительных задач в управляемой коллекции виртуальных машин и автоматически масштабирует вычислительные ресурсы в соответствии с требованиями задания.</span><span class="sxs-lookup"><span data-stu-id="3912a-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="3912a-114">С помощью пакетной службы вы можете определять вычислительные ресурсы Azure, необходимые для выполнения приложений в параллельном режиме и в нужном масштабе.</span><span class="sxs-lookup"><span data-stu-id="3912a-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="3912a-115">Вы можете выполнять задания по запросу или по расписанию. При этом вам не нужно вручную создавать и настраивать кластер высокопроизводительных вычислений (HPC), отдельные виртуальные машины, виртуальные сети или сложную инфраструктуру планировщика задач и заданий, а также управлять всеми этими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="3912a-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="3912a-116">Если вы не знакомы с пакетной службой Azure, изучите приведенные ниже статьи. Это поможет вам понять архитектуру и схему реализации решения, описанного в этой статье.</span><span class="sxs-lookup"><span data-stu-id="3912a-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>   

* [<span data-ttu-id="3912a-117">Основные сведения о пакетной службе Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="3912a-118">Обзор функций пакетной службы</span><span class="sxs-lookup"><span data-stu-id="3912a-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="3912a-119">Чтобы получить дополнительные сведения о пакетной службе Azure, ознакомьтесь со [схемой обучения по пакетной службе Azure](https://azure.microsoft.com/documentation/learning-paths/batch/) (необязательно).</span><span class="sxs-lookup"><span data-stu-id="3912a-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="3912a-120">Сведения о фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="3912a-121">Фабрика данных представляет собой облачную службу интеграции информации, которая организует и автоматизирует перемещение и преобразование данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="3912a-122">Фабрика данных позволяет создавать управляемые конвейеры данных, которые перемещают данные из локальных и облачных хранилищ данных в централизованное хранилище (например, в хранилище BLOB-объектов Azure), а также обрабатывают и преобразовывают данные с помощью служб, таких как Azure HDInsight и Машинное обучение Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="3912a-123">Вы можете планировать запуск конвейеров данных по расписанию (ежечасно, ежедневно, еженедельно и т. д.), отслеживать их состояние и управлять ими, чтобы обнаруживать проблемы и принимать меры.</span><span class="sxs-lookup"><span data-stu-id="3912a-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span></span>

<span data-ttu-id="3912a-124">Если вы не знакомы с фабрикой данных Azure, просмотрите приведенные ниже статьи. Это поможет понять архитектуру и реализацию решения, описанного в этой статье.</span><span class="sxs-lookup"><span data-stu-id="3912a-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>  

* [<span data-ttu-id="3912a-125">Общие сведения о службе фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="3912a-126">Построение конвейера данных</span><span class="sxs-lookup"><span data-stu-id="3912a-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="3912a-127">Чтобы получить дополнительные сведения о фабрике данных Azure, ознакомьтесь со [схемой обучения по фабрике данных Azure](https://azure.microsoft.com/documentation/learning-paths/data-factory/) (необязательно).</span><span class="sxs-lookup"><span data-stu-id="3912a-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="3912a-128">Совместное использование фабрики данных и пакетной службы</span><span class="sxs-lookup"><span data-stu-id="3912a-128">Data Factory and Batch together</span></span>
<span data-ttu-id="3912a-129">Фабрика данных включает в себя встроенные действия, например действие копирования, позволяющее копировать или перемещать данные из исходного хранилища данных в целевое, и действие HIVE, позволяющее обрабатывать данные с использованием кластеров Hadoop (HDInsight) в Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="3912a-130">Список поддерживаемых действий преобразования см. в [этой статье](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3912a-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="3912a-131">Благодаря этой службе вы можете также создавать настраиваемые действия .NET для перемещения или обработки данных с помощью собственной логики, а также выполнять эти действия в кластере Azure HDInsight или в пуле виртуальных машин пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="3912a-132">При использовании пакетной службы Azure можно настроить автоматическое масштабирование пула (добавление или удаление виртуальных машин в зависимости от рабочей нагрузки) по предоставленной формуле.</span><span class="sxs-lookup"><span data-stu-id="3912a-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="3912a-133">Архитектура примера решения</span><span class="sxs-lookup"><span data-stu-id="3912a-133">Architecture of sample solution</span></span>
<span data-ttu-id="3912a-134">Несмотря на то, что архитектура, описанная в этой статье, предназначена для простого решения, она подходит для таких сложных сценариев, как моделирование рисков по финансовым услугам, обработка и отрисовка изображений и геномный анализ.</span><span class="sxs-lookup"><span data-stu-id="3912a-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="3912a-135">На схеме показано, как фабрика данных управляет перемещением и обработкой данных и как пакетная служба Azure параллельно обрабатывает данные.</span><span class="sxs-lookup"><span data-stu-id="3912a-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="3912a-136">Скачайте и распечатайте схему для удобства (в формате 297 x 420 мм</span><span class="sxs-lookup"><span data-stu-id="3912a-136">Download and print the diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="3912a-137">или А3): [Управление данными и высокопроизводительными вычислениями с помощью пакетной службы и фабрики данных Azure](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="3912a-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="3912a-138">[![Схема обработки данных большого объема](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="3912a-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="3912a-139">Ниже приведен список основных этапов процесса.</span><span class="sxs-lookup"><span data-stu-id="3912a-139">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="3912a-140">Решение содержит код и указания по созданию комплексного решения.</span><span class="sxs-lookup"><span data-stu-id="3912a-140">The solution includes code and explanations to build the end-to-end solution.</span></span>

1. <span data-ttu-id="3912a-141">**Настройка пула вычислительных узлов (виртуальные машины) для пакетной службы Azure**.</span><span class="sxs-lookup"><span data-stu-id="3912a-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="3912a-142">Можно указать количество узлов и размер каждого из них.</span><span class="sxs-lookup"><span data-stu-id="3912a-142">You can specify the number of nodes and size of each node.</span></span>
2. <span data-ttu-id="3912a-143">**Создание экземпляра фабрики данных Azure** , для которого настраиваются сущности, представляющие хранилище BLOB-объектов, службу вычислений пакетной службы Azure, входные и выходные данные, а также рабочий процесс и конвейер с действиями, позволяющими перемещать и преобразовывать данные.</span><span class="sxs-lookup"><span data-stu-id="3912a-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="3912a-144">**Создание настраиваемого действия .NET в конвейере фабрики данных**.</span><span class="sxs-lookup"><span data-stu-id="3912a-144">**Create a custom .NET activity in the Data Factory pipeline**.</span></span> <span data-ttu-id="3912a-145">Действие является пользовательским кодом, который выполняется в пуле пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-145">The activity is your user code that runs on the Azure Batch pool.</span></span>
4. <span data-ttu-id="3912a-146">**Сохранение больших объемов входных данных в виде больших двоичных объектов в службе хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="3912a-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="3912a-147">Данные при этом разделяются на логические срезы (обычно по времени).</span><span class="sxs-lookup"><span data-stu-id="3912a-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="3912a-148">**Фабрика данных копирует данные, которые параллельно обрабатываются** и передаются в дополнительное расположение.</span><span class="sxs-lookup"><span data-stu-id="3912a-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>
6. <span data-ttu-id="3912a-149">**Фабрика данных запускает настраиваемое действие с помощью пула, выделенного пакетной службой**.</span><span class="sxs-lookup"><span data-stu-id="3912a-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span></span> <span data-ttu-id="3912a-150">Действия в фабрике данных могут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="3912a-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="3912a-151">В каждом действии обрабатывается один срез данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="3912a-152">Результаты сохраняются в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-152">The results are stored in Azure storage.</span></span>
7. <span data-ttu-id="3912a-153">**Фабрика данных перемещает окончательные результаты в третье расположение**для распространения с помощью приложения или дальнейшей обработки с помощью других инструментов.</span><span class="sxs-lookup"><span data-stu-id="3912a-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="3912a-154">Реализация примера решения</span><span class="sxs-lookup"><span data-stu-id="3912a-154">Implementation of sample solution</span></span>
<span data-ttu-id="3912a-155">Пример решения намеренно простой, чтобы продемонстрировать совместное использование фабрики данных и пакетной службы для обработки наборов данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="3912a-156">Решение просто вычисляет количество вхождений условия поиска (Microsoft) во входных файлах, упорядоченных по временным рядам.</span><span class="sxs-lookup"><span data-stu-id="3912a-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="3912a-157">Количество выводится в выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="3912a-157">It outputs the count to output files.</span></span>

<span data-ttu-id="3912a-158">**Время**. Если вы знакомы с основами использования Azure, фабрики данных и пакетной службы, а также выполнили предварительные требования, перечисленные ниже, создание решения должно занять 1–2 часа.</span><span class="sxs-lookup"><span data-stu-id="3912a-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3912a-159">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3912a-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="3912a-160">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-160">Azure subscription</span></span>
<span data-ttu-id="3912a-161">Если у вас нет подписки Azure, то всего за несколько минут можно создать бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="3912a-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3912a-162">Узнайте больше о [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3912a-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="3912a-163">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-163">Azure storage account</span></span>
<span data-ttu-id="3912a-164">Учетная запись хранения Azure используется в этом учебнике для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-164">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="3912a-165">Если у вас нет учетной записи хранения Azure, ознакомьтесь с разделом [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3912a-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="3912a-166">В примере решения используется хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="3912a-166">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="3912a-167">Учетная запись пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-167">Azure Batch account</span></span>
<span data-ttu-id="3912a-168">Создание учетной записи пакетной службы Azure на [портале Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="3912a-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="3912a-169">Ознакомьтесь со статьей [Создание учетной записи пакетной службы Azure и управление ею](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3912a-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="3912a-170">Запишите ключ и имя учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-170">Note the Azure Batch account name and account key.</span></span> <span data-ttu-id="3912a-171">Для создания учетной записи пакетной службы Azure можно также воспользоваться командлетом [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx).</span><span class="sxs-lookup"><span data-stu-id="3912a-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span></span> <span data-ttu-id="3912a-172">Подробные инструкции по использованию этого командлета см. в статье [Приступая к работе с командлетами PowerShell пакетной службы Azure](../batch/batch-powershell-cmdlets-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3912a-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="3912a-173">В примере решения используется пакетная служба Azure (косвенно, через конвейер фабрики данных Azure) для параллельной обработки данных в пуле вычислительных узлов (управляемой коллекции виртуальных машин).</span><span class="sxs-lookup"><span data-stu-id="3912a-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="3912a-174">Пул виртуальных машин пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="3912a-175">Создайте **пул пакетной службы Azure** с как минимум 2 вычислительными узлами.</span><span class="sxs-lookup"><span data-stu-id="3912a-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="3912a-176">На [портале Azure](https://portal.azure.com) щелкните **Обзор** в меню слева и выберите **Уч. записи пакетной службы**.</span><span class="sxs-lookup"><span data-stu-id="3912a-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="3912a-177">Выберите свою учетную запись пакетной службы Azure, чтобы открыть колонку **Учетная запись пакетной службы** .</span><span class="sxs-lookup"><span data-stu-id="3912a-177">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
3. <span data-ttu-id="3912a-178">Щелкните элемент **Пулы** .</span><span class="sxs-lookup"><span data-stu-id="3912a-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="3912a-179">В колонке **Пулы** нажмите кнопку "Добавить" на панели инструментов, чтобы добавить пул.</span><span class="sxs-lookup"><span data-stu-id="3912a-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
   1. <span data-ttu-id="3912a-180">Введите идентификатор для пула (**идентификатор пула**).</span><span class="sxs-lookup"><span data-stu-id="3912a-180">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="3912a-181">Сохраните **идентификатор пула**. Он понадобится при создании решения фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
   2. <span data-ttu-id="3912a-182">В качестве параметра семейства операционных систем укажите **Windows Server 2012 R2** .</span><span class="sxs-lookup"><span data-stu-id="3912a-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
   3. <span data-ttu-id="3912a-183">Выберите **Ценовая категория для узлов**.</span><span class="sxs-lookup"><span data-stu-id="3912a-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="3912a-184">Для параметра **Выделенный целевой объект** укажите значение **2**.</span><span class="sxs-lookup"><span data-stu-id="3912a-184">Enter **2** as value for the **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="3912a-185">Для параметра **Максимальное число заданий на узел** укажите значение **2**.</span><span class="sxs-lookup"><span data-stu-id="3912a-185">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="3912a-186">Нажмите кнопку **ОК** , чтобы создать пул.</span><span class="sxs-lookup"><span data-stu-id="3912a-186">Click **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="3912a-187">Обозреватель хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-187">Azure Storage Explorer</span></span>
<span data-ttu-id="3912a-188">[Azure Storage Explorer 6 (инструмент)](https://azurestorageexplorer.codeplex.com/) или [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (от ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="3912a-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="3912a-189">Эти инструменты предназначены для проверки и изменения данных в проектах службы хранилища Azure, включая журналы облачных приложений.</span><span class="sxs-lookup"><span data-stu-id="3912a-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="3912a-190">Создайте контейнер **mycontainer** с закрытым доступом (без анонимного доступа).</span><span class="sxs-lookup"><span data-stu-id="3912a-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="3912a-191">При использовании **CloudXplorer**создавайте папки и подпапки со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="3912a-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="3912a-192">`Inputfolder`и `outputfolder` — это папки верхнего уровня в `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="3912a-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="3912a-193">`inputfolder` содержит вложенные папки с метками даты и времени (ГГГГ-ММ-ДД-ЧЧ).</span><span class="sxs-lookup"><span data-stu-id="3912a-193">The `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="3912a-194">При использовании **Azure Storage Explorer** на следующем шаге необходимо передать файлы с именами `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` и т. д.</span><span class="sxs-lookup"><span data-stu-id="3912a-194">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="3912a-195">На этом шаге автоматически будут созданы папки.</span><span class="sxs-lookup"><span data-stu-id="3912a-195">This step automatically creates the folders.</span></span>
3. <span data-ttu-id="3912a-196">Создайте на компьютере текстовый файл **file.txt** с содержимым, в котором есть ключевое слово **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="3912a-196">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="3912a-197">Например, test custom activity Microsoft test custom activity Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3912a-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="3912a-198">Отправьте файл в следующие входные папки хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-198">Upload the file to the following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="3912a-199">При использовании **Azure Storage Explorer** передайте файл **file.txt** в контейнер **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="3912a-199">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span></span> <span data-ttu-id="3912a-200">На панели инструментов щелкните **Копировать**, чтобы создать копию большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="3912a-200">Click **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="3912a-201">В диалоговом окне **Копирование большого двоичного объекта** измените **имя целевого большого двоичного объекта** на `inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="3912a-201">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="3912a-202">Повторите этот шаг, чтобы создать `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` и т. д.</span><span class="sxs-lookup"><span data-stu-id="3912a-202">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="3912a-203">Это действие автоматически создает данные папки.</span><span class="sxs-lookup"><span data-stu-id="3912a-203">This action automatically creates the folders.</span></span>
5. <span data-ttu-id="3912a-204">Создайте другой контейнер с именем: `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="3912a-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="3912a-205">В этот контейнер передается ZIP-файл настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="3912a-205">You upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="3912a-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3912a-206">Visual Studio</span></span>
<span data-ttu-id="3912a-207">Установите Microsoft Visual Studio 2012 или более поздней версии, чтобы создать настраиваемое действие пакетной службы, которое будет использоваться в решении фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-207">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="3912a-208">Пошаговое создание решения</span><span class="sxs-lookup"><span data-stu-id="3912a-208">High-level steps to create the solution</span></span>
1. <span data-ttu-id="3912a-209">Создайте настраиваемое действие, содержащее логику обработки данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-209">Create a custom activity that contains the data processing logic.</span></span>
2. <span data-ttu-id="3912a-210">Создайте фабрику данных Azure, которая использует настраиваемое действие:</span><span class="sxs-lookup"><span data-stu-id="3912a-210">Create an Azure data factory that uses the custom activity:</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="3912a-211">Создание пользовательского действия</span><span class="sxs-lookup"><span data-stu-id="3912a-211">Create the custom activity</span></span>
<span data-ttu-id="3912a-212">Настраиваемое действие фабрики данных составляет основу этого примера решения.</span><span class="sxs-lookup"><span data-stu-id="3912a-212">The Data Factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="3912a-213">Для выполнения этого действия в решении используется пакетная служба Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-213">The sample solution uses Azure Batch to run the custom activity.</span></span> <span data-ttu-id="3912a-214">Общие сведения о разработке настраиваемых действий и их использовании в конвейере фабрики данных Azure см. в статье [Использование настраиваемых действий в конвейере фабрики данных Azure](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="3912a-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="3912a-215">Чтобы создать настраиваемое действие .NET, которое можно использовать в конвейере фабрики данных Azure, необходимо создать проект **библиотеки классов .NET** с классом, который реализует интерфейс **IDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="3912a-215">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="3912a-216">У этого интерфейса только один метод — **Execute**.</span><span class="sxs-lookup"><span data-stu-id="3912a-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="3912a-217">Подпись метода выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3912a-217">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="3912a-218">У этого метода есть несколько ключевых компонентов, с которыми нужно разобраться.</span><span class="sxs-lookup"><span data-stu-id="3912a-218">The method has a few key components that you need to understand.</span></span>

* <span data-ttu-id="3912a-219">Метод принимает четыре параметра:</span><span class="sxs-lookup"><span data-stu-id="3912a-219">The method takes four parameters:</span></span>

  1. <span data-ttu-id="3912a-220">**linkedServices** —</span><span class="sxs-lookup"><span data-stu-id="3912a-220">**linkedServices**.</span></span> <span data-ttu-id="3912a-221">это перечисляемый список связанных служб, которые связывают источники входных и выходных данных (например, хранилище BLOB-объектов Azure) с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span></span> <span data-ttu-id="3912a-222">В этом примере присутствует только одна связанная служба (служба хранилища Azure), которая используется для входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="3912a-223">**наборы данных**.</span><span class="sxs-lookup"><span data-stu-id="3912a-223">**datasets**.</span></span> <span data-ttu-id="3912a-224">это перечисляемый список наборов данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="3912a-225">Этот параметр можно использовать для получения расположений и схем, которые определяются входными и выходными наборами данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-225">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="3912a-226">**activity** —</span><span class="sxs-lookup"><span data-stu-id="3912a-226">**activity**.</span></span> <span data-ttu-id="3912a-227">этот параметр представляет текущую вычислительную сущность (в этом примере — пакетную службу Azure).</span><span class="sxs-lookup"><span data-stu-id="3912a-227">This parameter represents the current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="3912a-228">**logger** —</span><span class="sxs-lookup"><span data-stu-id="3912a-228">**logger**.</span></span> <span data-ttu-id="3912a-229">средство ведения журнала позволяет записывать комментарии отладки, которые отображаются в виде пользовательского журнала для конвейера.</span><span class="sxs-lookup"><span data-stu-id="3912a-229">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span></span>
* <span data-ttu-id="3912a-230">Этот метод возвращает словарь, который можно будет использовать для создания цепочки из настраиваемых действий в будущем.</span><span class="sxs-lookup"><span data-stu-id="3912a-230">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="3912a-231">Эта функция еще не реализована, поэтому из метода просто возвращается пустой словарь.</span><span class="sxs-lookup"><span data-stu-id="3912a-231">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="3912a-232">Процедура. Создание настраиваемого действия</span><span class="sxs-lookup"><span data-stu-id="3912a-232">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="3912a-233">Создайте проект библиотеки классов .NET в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="3912a-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="3912a-234">Запустите **Visual Studio 2012,** /**Visual Studio 2013 или Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="3912a-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="3912a-235">Щелкните **Файл**, наведите указатель мыши на пункт **Создать** и щелкните **Проект**.</span><span class="sxs-lookup"><span data-stu-id="3912a-235">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="3912a-236">Разверните раздел **Шаблоны** и выберите **Visual C#\#**.</span><span class="sxs-lookup"><span data-stu-id="3912a-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="3912a-237">В этом руководстве используется язык C\#, но для создания настраиваемого действия вы можете использовать любой язык .NET.</span><span class="sxs-lookup"><span data-stu-id="3912a-237">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>
   4. <span data-ttu-id="3912a-238">Выберите тип **Библиотека классов** из списка типов проектов справа.</span><span class="sxs-lookup"><span data-stu-id="3912a-238">Select **Class Library** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="3912a-239">В поле **Имя** введите **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="3912a-239">Enter **MyDotNetActivity** for the **Name**.</span></span>
   6. <span data-ttu-id="3912a-240">В поле **Расположение\\ выберите** C:**ADF**.</span><span class="sxs-lookup"><span data-stu-id="3912a-240">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="3912a-241">Создайте папку **ADF** , если она не существует.</span><span class="sxs-lookup"><span data-stu-id="3912a-241">Create the folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="3912a-242">Нажмите кнопку **ОК** , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="3912a-242">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="3912a-243">Щелкните **Инструменты**, наведите указатель мыши на **Диспетчер пакетов NuGet** и щелкните **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="3912a-243">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="3912a-244">В **консоли диспетчера пакетов** выполните следующую команду, чтобы импортировать пакет **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="3912a-244">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="3912a-245">Импортируйте пакет NuGet для **службы хранилища Azure** в проект.</span><span class="sxs-lookup"><span data-stu-id="3912a-245">Import the **Azure Storage** NuGet package in to the project.</span></span> <span data-ttu-id="3912a-246">Он нужен, так как в данном примере используется API хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="3912a-246">You need this package because you use the Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="3912a-247">Добавьте следующие директивы с **using** в исходный файл в проекте.</span><span class="sxs-lookup"><span data-stu-id="3912a-247">Add the following **using** directives to the source file in the project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="3912a-248">Измените имя **пространства имен** на **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="3912a-248">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="3912a-249">Измените имя класса на **MyDotNetActivity** и извлеките класс из интерфейса **IDotNetActivity**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="3912a-249">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="3912a-250">Реализуйте (добавьте) метод **Execute** интерфейса **IDotNetActivity** для класса **MyDotNetActivity** и скопируйте следующий пример кода в этот метод.</span><span class="sxs-lookup"><span data-stu-id="3912a-250">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span> <span data-ttu-id="3912a-251">Объяснение логики, используемой в этом методе, см. в разделе [Метод Execute](#execute-method).</span><span class="sxs-lookup"><span data-stu-id="3912a-251">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize the continuation token before using it in the do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get the list of input blobs from the input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns the number of occurrences of
           // the search term (“Microsoft”) in each blob associated
           // with the data slice.
           //
           // definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="3912a-252">Добавьте в класс следующие вспомогательные методы.</span><span class="sxs-lookup"><span data-stu-id="3912a-252">Add the following helper methods to the class.</span></span> <span data-ttu-id="3912a-253">Их вызывает метод **Execute** .</span><span class="sxs-lookup"><span data-stu-id="3912a-253">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="3912a-254">Самое главное, метод **Calculate** изолирует код, который выполняет итерацию каждого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="3912a-254">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="3912a-255">Метод **GetFolderPath** возвращает путь к папке, на которую указывает набор данных, а метод **GetFileName** — имя большого двоичного объекта или файла, на который указывает набор данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-255">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="3912a-256">Метод **Calculate** вычисляет количество экземпляров ключевого слова **Microsoft** во входных файлах (в больших двоичных объектах в папке).</span><span class="sxs-lookup"><span data-stu-id="3912a-256">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span></span> <span data-ttu-id="3912a-257">Условие поиска (Microsoft) жестко задано в коде.</span><span class="sxs-lookup"><span data-stu-id="3912a-257">The search term (“Microsoft”) is hard-coded in the code.</span></span>

1. <span data-ttu-id="3912a-258">Скомпилируйте проект.</span><span class="sxs-lookup"><span data-stu-id="3912a-258">Compile the project.</span></span> <span data-ttu-id="3912a-259">В меню щелкните **Построить** и **Построить решение**.</span><span class="sxs-lookup"><span data-stu-id="3912a-259">Click **Build** from the menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="3912a-260">Запустите **проводник Windows** и перейдите к папке **bin\\debug** или **bin\\release** в зависимости от типа сборки.</span><span class="sxs-lookup"><span data-stu-id="3912a-260">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span></span>
3. <span data-ttu-id="3912a-261">Создайте ZIP-файл **MyDotNetActivity.zip**, который содержит все двоичные файлы из папки **\\bin\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="3912a-261">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="3912a-262">Можно также добавить файл MyDotNetActivity.**pdb**, чтобы в случае сбоя получить дополнительные сведения, например номер строки в исходном коде, вызвавшей ошибку.</span><span class="sxs-lookup"><span data-stu-id="3912a-262">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="3912a-263">Передайте архив **MyDotNetActivity.zip** в качестве большого двоичного объекта в контейнер больших двоичных объектов `customactivitycontainer` в хранилище BLOB-объектов Azure (используется связанной службой **StorageLinkedService** в **ADFTutorialDataFactor**).</span><span class="sxs-lookup"><span data-stu-id="3912a-263">Upload **MyDotNetActivity.zip** as a blob to the blob container: `customactivitycontainer` in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="3912a-264">Если контейнер `customactivitycontainer` еще не существует, создайте его.</span><span class="sxs-lookup"><span data-stu-id="3912a-264">Create the blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="3912a-265">Метод Execute</span><span class="sxs-lookup"><span data-stu-id="3912a-265">Execute method</span></span>
<span data-ttu-id="3912a-266">В этом разделе содержатся дополнительные сведения и примечания о коде в методе Execute.</span><span class="sxs-lookup"><span data-stu-id="3912a-266">This section provides more details and notes about the code in the Execute method.</span></span>

1. <span data-ttu-id="3912a-267">Элементы для выполнения итерации входной коллекции находятся в пространстве имен [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="3912a-267">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="3912a-268">Для итерации коллекции больших двоичных объектов необходимо использовать класс **BlobContinuationToken**.</span><span class="sxs-lookup"><span data-stu-id="3912a-268">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span></span> <span data-ttu-id="3912a-269">В сущности, необходимо использовать цикл do-while и маркер в качестве механизма для выхода из цикла.</span><span class="sxs-lookup"><span data-stu-id="3912a-269">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="3912a-270">Дополнительные сведения см. в статье [Использование хранилища BLOB-объектов из .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="3912a-270">For more information, see [How to use Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="3912a-271">Базовый цикл выглядит так:</span><span class="sxs-lookup"><span data-stu-id="3912a-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize the continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get the list of input blobs from the input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="3912a-272">Дополнительные сведения см. в документации по методу [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx).</span><span class="sxs-lookup"><span data-stu-id="3912a-272">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="3912a-273">Код для работы с набором больших двоичных объектов логически находится в цикле do-while.</span><span class="sxs-lookup"><span data-stu-id="3912a-273">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="3912a-274">В методе **Execute** цикл do-while передает список больших двоичных объектов в метод **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="3912a-274">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="3912a-275">Этот метод возвращает строковую переменную с именем **output** , которая является результатом итерации всех больших двоичных объектов в сегменте.</span><span class="sxs-lookup"><span data-stu-id="3912a-275">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="3912a-276">Он возвращает число вхождений условия поиска (**Microsoft**) в большом двоичном объекте, переданном в метод **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="3912a-276">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="3912a-277">После завершения работы метода **Calculate** его результаты записываются в новый большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="3912a-277">Once the **Calculate** method has done the work, it must be written to a new blob.</span></span> <span data-ttu-id="3912a-278">Следовательно, для каждого обработанного набора больших двоичных объектов можно записать новый большой двоичный объект с результатами.</span><span class="sxs-lookup"><span data-stu-id="3912a-278">So for every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="3912a-279">Чтобы записать новый большой двоичный объект, сначала найдите выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-279">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="3912a-280">Код также вызывает вспомогательный метод **GetFolderPath** , чтобы получить путь к папке (имя контейнера хранилища).</span><span class="sxs-lookup"><span data-stu-id="3912a-280">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="3912a-281">Метод **GetFolderPath** приводит объект DataSet к AzureBlobDataSet со свойством FolderPath.</span><span class="sxs-lookup"><span data-stu-id="3912a-281">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="3912a-282">Код вызывает метод **GetFileName** , чтобы получить имя файла (имя большого двоичного объекта).</span><span class="sxs-lookup"><span data-stu-id="3912a-282">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="3912a-283">Используемый код аналогичен приведенному выше коду, используемому для получения пути к папке.</span><span class="sxs-lookup"><span data-stu-id="3912a-283">The code is similar to the above code to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="3912a-284">Чтобы записать имя файла, создается объект универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="3912a-284">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="3912a-285">Для возврата имени контейнера в конструкторе URI используется свойство **BlobEndpoint** .</span><span class="sxs-lookup"><span data-stu-id="3912a-285">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="3912a-286">Для создания URI выходного большого двоичного объекта сочетаются путь к папке и имя файла.</span><span class="sxs-lookup"><span data-stu-id="3912a-286">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="3912a-287">Имя файла записано, и теперь можно записать выводимую строку из метода **Calculate** в новый большой двоичный объект:</span><span class="sxs-lookup"><span data-stu-id="3912a-287">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="3912a-288">Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="3912a-288">Create the data factory</span></span>
<span data-ttu-id="3912a-289">В разделе [Создание настраиваемого действия](#create-the-custom-activity) вы создали настраиваемое действие и отправили ZIP-файл с двоичными файлами и PDB-файлом в контейнер больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-289">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span></span> <span data-ttu-id="3912a-290">В этом разделе вы создадите **фабрику данных** Azure с **конвейером**, использующим **настраиваемое действие**.</span><span class="sxs-lookup"><span data-stu-id="3912a-290">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span></span>

<span data-ttu-id="3912a-291">Входной набор данных для пользовательского действия представляет собой большие двоичные объекты (файлы) во входной папке (`mycontainer\\inputfolder`) в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="3912a-291">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="3912a-292">Выходной набор данных для пользовательского действия представляет собой выходные большие двоичные объекты в папке выходных данных (`mycontainer\\outputfolder`) в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="3912a-292">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="3912a-293">Перенесите в папки входных данных один или несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="3912a-293">Drop one or more files in the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="3912a-294">Например, перенесите один файл (file.txt) со следующим содержимым в каждую папку.</span><span class="sxs-lookup"><span data-stu-id="3912a-294">For example, drop one file (file.txt) with the following content into each of the folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="3912a-295">Каждая входная папка соответствует одному срезу в фабрике данных Azure, даже если она содержит 2 файла или более.</span><span class="sxs-lookup"><span data-stu-id="3912a-295">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span></span> <span data-ttu-id="3912a-296">При обработке каждого среза конвейером пользовательское действие выполняет итерацию всех больших двоичных объектов во входной папке для этого среза.</span><span class="sxs-lookup"><span data-stu-id="3912a-296">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="3912a-297">Отображаются пять выходных файлов с одинаковым содержимым.</span><span class="sxs-lookup"><span data-stu-id="3912a-297">You see five output files with the same content.</span></span> <span data-ttu-id="3912a-298">Например, выходной файл, полученный в ходе обработки файла в папке 2015-11-16-00, включает в себя следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="3912a-298">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="3912a-299">Если в папку входных данных перенести несколько файлов (file.txt, file2.txt, file3.txt) с одинаковым содержимым, то в выходном файле будет следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="3912a-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="3912a-300">В этом примере каждая папка (2015-11-16-00 и т. д.) соответствует одному срезу, несмотря на то, что она содержит несколько входных файлов.</span><span class="sxs-lookup"><span data-stu-id="3912a-300">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="3912a-301">Теперь во входном файле появилось три строки, по одной на каждый входной файл (большой двоичный объект) в папке, связанный со срезом (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="3912a-301">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="3912a-302">Такая задача создается для каждого запуска действия.</span><span class="sxs-lookup"><span data-stu-id="3912a-302">A task is created for each activity run.</span></span> <span data-ttu-id="3912a-303">В этом примере в конвейере есть только одно действие.</span><span class="sxs-lookup"><span data-stu-id="3912a-303">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="3912a-304">При обработке среза конвейером в пакетной службе Azure выполняется настраиваемое действие для обработки среза.</span><span class="sxs-lookup"><span data-stu-id="3912a-304">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span></span> <span data-ttu-id="3912a-305">Так как имеется 5 срезов (каждому срезу может соответствовать несколько больших двоичных объектов или файлов), в пакетной службе Azure создано 5 задач.</span><span class="sxs-lookup"><span data-stu-id="3912a-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="3912a-306">При запуске задачи в пакетной службе фактически выполняется настраиваемое действие.</span><span class="sxs-lookup"><span data-stu-id="3912a-306">When a task runs on Batch, it is actually the custom activity that is running.</span></span>

<span data-ttu-id="3912a-307">В следующем пошаговом руководстве содержатся дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="3912a-307">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="3912a-308">Шаг 1. Создание фабрики данных</span><span class="sxs-lookup"><span data-stu-id="3912a-308">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="3912a-309">Войдите на [портал Azure](https://portal.azure.com/) и сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="3912a-309">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>

   1. <span data-ttu-id="3912a-310">В меню слева нажмите кнопку **Создать** .</span><span class="sxs-lookup"><span data-stu-id="3912a-310">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="3912a-311">В колонке **Создание** щелкните **Данные и аналитика**.</span><span class="sxs-lookup"><span data-stu-id="3912a-311">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="3912a-312">Щелкните **Фабрика данных** в колонке **Аналитика данных**.</span><span class="sxs-lookup"><span data-stu-id="3912a-312">Click **Data Factory** on the **Data analytics** blade.</span></span>
2. <span data-ttu-id="3912a-313">В колонке **Создание фабрики данных** в поле "Имя" введите **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="3912a-313">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="3912a-314">Имя фабрики данных Azure должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="3912a-314">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="3912a-315">Если возникнет ошибка **Имя фабрики данных CustomActivityFactory недоступно**, измените имя этой фабрики данных (например, на **ваше_имяCustomActivityFactory**) и попробуйте создать ее снова.</span><span class="sxs-lookup"><span data-stu-id="3912a-315">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="3912a-316">Щелкните **Имя группы ресурсов**, чтобы выбрать имеющуюся группу ресурсов, или создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3912a-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="3912a-317">Убедитесь, что используется именно та подписка и регион, в которых необходимо создать фабрику данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-317">Verify that you are using the correct subscription and region where you want the data factory to be created.</span></span>
5. <span data-ttu-id="3912a-318">В колонке **Создание фабрики данных** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3912a-318">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="3912a-319">Созданная фабрика данных появится на **панели мониторинга** портала Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-319">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="3912a-320">Ее содержимое отобразится на соответствующей странице.</span><span class="sxs-lookup"><span data-stu-id="3912a-320">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="3912a-321">Шаг 2. Создание связанных служб</span><span class="sxs-lookup"><span data-stu-id="3912a-321">Step 2: Create linked services</span></span>
<span data-ttu-id="3912a-322">Связанные службы связывают хранилища данных или службы вычислений с фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-322">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="3912a-323">На этом этапе учетная запись **хранения Azure** и учетная запись **пакетной службы Azure** будут связаны с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-323">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="3912a-324">Создание связанной службы хранения Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="3912a-325">В колонке **Фабрика данных** для **CustomActivityFactory** щелкните элемент **Создание и развертывание**.</span><span class="sxs-lookup"><span data-stu-id="3912a-325">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="3912a-326">Отобразится редактор фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-326">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="3912a-327">На панели команд щелкните **Создание хранилища данных** и выберите **Служба хранилища Azure**.</span><span class="sxs-lookup"><span data-stu-id="3912a-327">Click **New data store** on the command bar and choose **Azure storage.**</span></span> <span data-ttu-id="3912a-328">В редакторе отобразится сценарий JSON для создания связанной службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-328">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="3912a-329">Замените **account name** именем своей учетной записи хранения Azure, а **account key** — ключом доступа к ней.</span><span class="sxs-lookup"><span data-stu-id="3912a-329">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="3912a-330">Сведения о получении ключа доступа к хранилищу см. в разделах о [просмотре, копировании и повторном создании ключей доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="3912a-330">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="3912a-331">Чтобы развернуть эту службу, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="3912a-331">Click **Deploy** on the command bar to deploy the linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="3912a-332">Создание связанной пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="3912a-333">На этом шаге вы создаете связанную службу для учетной записи **пакетной службы Azure**, в которой будет выполняться настраиваемое действие фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-333">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span></span>

1. <span data-ttu-id="3912a-334">Щелкните **Новое вычисление** в командной строке и выберите **Пакетная служба Azure**.</span><span class="sxs-lookup"><span data-stu-id="3912a-334">Click **New compute** on the command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="3912a-335">В редакторе отобразится сценарий JSON для создания связанной пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-335">You should see the JSON script for creating an Azure Batch linked service in the editor.</span></span>
2. <span data-ttu-id="3912a-336">В сценарии JSON выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="3912a-336">In the JSON script:</span></span>

   1. <span data-ttu-id="3912a-337">Замените **account name** именем учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-337">Replace **account name** with the name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="3912a-338">Замените **access key** ключом доступа к учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-338">Replace **access key** with the access key of the Azure Batch account.</span></span>
   3. <span data-ttu-id="3912a-339">Введите идентификатор пула для свойства **poolName** **.**</span><span class="sxs-lookup"><span data-stu-id="3912a-339">Enter the ID of the pool for the **poolName** property**.**</span></span> <span data-ttu-id="3912a-340">Для этого свойства можно задать имя пула или идентификатор пула.</span><span class="sxs-lookup"><span data-stu-id="3912a-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="3912a-341">Введите URI пакета для свойства JSON **batchUri** .</span><span class="sxs-lookup"><span data-stu-id="3912a-341">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="3912a-342">**URL-адрес** из **колонки учетной записи пакетной службы Azure** имеет следующий формат: \<имя_учетной_записи\>.\<регион\>.batch.azure.com. В свойстве **batchUri** в JSON требуется **удалить заполнитель accountname**</span><span class="sxs-lookup"><span data-stu-id="3912a-342">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com. For the **batchUri** property in the JSON, you need to **remove "accountname."**</span></span> <span data-ttu-id="3912a-343">в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="3912a-343">from the URL.</span></span> <span data-ttu-id="3912a-344">Пример: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="3912a-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="3912a-345">Для свойства **poolName** можно также указать идентификатор пула вместо его имени.</span><span class="sxs-lookup"><span data-stu-id="3912a-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="3912a-346">Служба фабрики данных не поддерживает параметр по требованию для пакетной службы Azure, как для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3912a-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="3912a-347">Пул пакетной службы Azure можно использовать только в фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="3912a-348">В качестве параметра семейства операционных систем укажите **StorageLinkedService** for the **linkedServiceName** .</span><span class="sxs-lookup"><span data-stu-id="3912a-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="3912a-349">Эта связанная служба была создана на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="3912a-349">You created this linked service in the previous step.</span></span> <span data-ttu-id="3912a-350">Это хранилище используется в качестве промежуточной области для файлов и журналов.</span><span class="sxs-lookup"><span data-stu-id="3912a-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="3912a-351">Чтобы развернуть эту службу, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="3912a-351">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="3912a-352">Шаг 3. Создание наборов данных</span><span class="sxs-lookup"><span data-stu-id="3912a-352">Step 3: Create datasets</span></span>
<span data-ttu-id="3912a-353">На этом шаге вы создадите наборы данных, которые представляют входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="3912a-353">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="3912a-354">Создание входного набора данных</span><span class="sxs-lookup"><span data-stu-id="3912a-354">Create input dataset</span></span>
1. <span data-ttu-id="3912a-355">В **редакторе** фабрики данных нажмите на панели инструментов кнопку **Новый набор данных** и выберите в раскрывающемся меню пункт **Хранилище BLOB-объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="3912a-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="3912a-356">Замените код JSON в правой области на следующий фрагмент кода JSON:</span><span class="sxs-lookup"><span data-stu-id="3912a-356">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="3912a-357">Позже в этом пошаговом руководстве вы создадите конвейер со временем начала 2015-11-16T00:00:00Z и временем окончания 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="3912a-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="3912a-358">Данные будут создаваться **почасово**, поэтому мы получим 5 входных и выходных срезов (между **00**:00:00 -\> **05**:00:00).</span><span class="sxs-lookup"><span data-stu-id="3912a-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="3912a-359">Для параметров **frequency** и **interval** входного набора данных установлены значения **Hour** и **1**. Это означает, что входной срез данных будет создаваться каждый час.</span><span class="sxs-lookup"><span data-stu-id="3912a-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="3912a-360">Это значения времени начала для каждого среза, представленные системной переменной **SliceStart** в приведенном выше фрагменте кода JSON.</span><span class="sxs-lookup"><span data-stu-id="3912a-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span></span>

    | <span data-ttu-id="3912a-361">**Срез**</span><span class="sxs-lookup"><span data-stu-id="3912a-361">**Slice**</span></span> | <span data-ttu-id="3912a-362">**Время начала**</span><span class="sxs-lookup"><span data-stu-id="3912a-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="3912a-363">1</span><span class="sxs-lookup"><span data-stu-id="3912a-363">1</span></span>         | <span data-ttu-id="3912a-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="3912a-365">2</span><span class="sxs-lookup"><span data-stu-id="3912a-365">2</span></span>         | <span data-ttu-id="3912a-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="3912a-367">3</span><span class="sxs-lookup"><span data-stu-id="3912a-367">3</span></span>         | <span data-ttu-id="3912a-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="3912a-369">4.</span><span class="sxs-lookup"><span data-stu-id="3912a-369">4</span></span>         | <span data-ttu-id="3912a-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="3912a-371">5</span><span class="sxs-lookup"><span data-stu-id="3912a-371">5</span></span>         | <span data-ttu-id="3912a-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="3912a-373">Значение параметра **folderPath** вычисляется с использованием года, месяца, дня и часа значения времени начала среза (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="3912a-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="3912a-374">Именно так входная папка сопоставляется со срезом.</span><span class="sxs-lookup"><span data-stu-id="3912a-374">Therefore, here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="3912a-375">**Срез**</span><span class="sxs-lookup"><span data-stu-id="3912a-375">**Slice**</span></span> | <span data-ttu-id="3912a-376">**Время начала**</span><span class="sxs-lookup"><span data-stu-id="3912a-376">**Start time**</span></span>          | <span data-ttu-id="3912a-377">**Входная папка**</span><span class="sxs-lookup"><span data-stu-id="3912a-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="3912a-378">1</span><span class="sxs-lookup"><span data-stu-id="3912a-378">1</span></span>         | <span data-ttu-id="3912a-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="3912a-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="3912a-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="3912a-381">2</span><span class="sxs-lookup"><span data-stu-id="3912a-381">2</span></span>         | <span data-ttu-id="3912a-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="3912a-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="3912a-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="3912a-384">3</span><span class="sxs-lookup"><span data-stu-id="3912a-384">3</span></span>         | <span data-ttu-id="3912a-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="3912a-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="3912a-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="3912a-387">4.</span><span class="sxs-lookup"><span data-stu-id="3912a-387">4</span></span>         | <span data-ttu-id="3912a-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="3912a-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="3912a-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="3912a-390">5</span><span class="sxs-lookup"><span data-stu-id="3912a-390">5</span></span>         | <span data-ttu-id="3912a-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="3912a-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="3912a-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="3912a-393">На панели инструментов щелкните **Развернуть**, чтобы создать и развернуть таблицу **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="3912a-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="3912a-394">Создание выходного набора данных</span><span class="sxs-lookup"><span data-stu-id="3912a-394">Create output dataset</span></span>
<span data-ttu-id="3912a-395">На этом шаге создается еще один набор данных типа AzureBlob для представления выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="3912a-396">В **редакторе** фабрики данных нажмите на панели инструментов кнопку **Новый набор данных** и выберите в раскрывающемся меню пункт **Хранилище BLOB-объектов Azure**.</span><span class="sxs-lookup"><span data-stu-id="3912a-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="3912a-397">Замените код JSON в правой области на следующий фрагмент кода JSON:</span><span class="sxs-lookup"><span data-stu-id="3912a-397">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    <span data-ttu-id="3912a-398">Для каждого входного среза данных создается выходной большой двоичный объект или файл.</span><span class="sxs-lookup"><span data-stu-id="3912a-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="3912a-399">Ниже в таблице приведены имена, которые даются выходным файлам для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="3912a-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="3912a-400">Все выходные файлы создаются в одной папке выходных данных: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="3912a-400">All the output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="3912a-401">**Срез**</span><span class="sxs-lookup"><span data-stu-id="3912a-401">**Slice**</span></span> | <span data-ttu-id="3912a-402">**Время начала**</span><span class="sxs-lookup"><span data-stu-id="3912a-402">**Start time**</span></span>          | <span data-ttu-id="3912a-403">**Выходной файл**</span><span class="sxs-lookup"><span data-stu-id="3912a-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="3912a-404">1</span><span class="sxs-lookup"><span data-stu-id="3912a-404">1</span></span>         | <span data-ttu-id="3912a-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="3912a-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="3912a-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="3912a-407">2</span><span class="sxs-lookup"><span data-stu-id="3912a-407">2</span></span>         | <span data-ttu-id="3912a-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="3912a-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="3912a-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="3912a-410">3</span><span class="sxs-lookup"><span data-stu-id="3912a-410">3</span></span>         | <span data-ttu-id="3912a-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="3912a-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="3912a-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="3912a-413">4.</span><span class="sxs-lookup"><span data-stu-id="3912a-413">4</span></span>         | <span data-ttu-id="3912a-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="3912a-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="3912a-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="3912a-416">5</span><span class="sxs-lookup"><span data-stu-id="3912a-416">5</span></span>         | <span data-ttu-id="3912a-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="3912a-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="3912a-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="3912a-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="3912a-419">Помните, что все файлы во входной папке (например, 2015-11-16-00) являются частью среза со значениями времени начала (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="3912a-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span></span> <span data-ttu-id="3912a-420">Во время обработки этого среза пользовательское действие сканирует каждый файл и создает строку в выходном файле с количеством вхождений условия поиска (Microsoft).</span><span class="sxs-lookup"><span data-stu-id="3912a-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="3912a-421">Если в папке 2015-11-16-00 есть три файла, то в выходном файле 2015-11-16-00.txt будет три строки.</span><span class="sxs-lookup"><span data-stu-id="3912a-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="3912a-422">На панели инструментов щелкните **Развернуть**, чтобы создать и развернуть **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="3912a-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-custom-activity"></a><span data-ttu-id="3912a-423">Шаг 4. Создание и запуск конвейера с настраиваемым действием</span><span class="sxs-lookup"><span data-stu-id="3912a-423">Step 4: Create and run the pipeline with custom activity</span></span>
<span data-ttu-id="3912a-424">На этом шаге создается конвейер с одним настраиваемым действием, созданным ранее.</span><span class="sxs-lookup"><span data-stu-id="3912a-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3912a-425">Если файл **file.txt** не отправлен в папки входных данных в контейнере больших двоичных объектов, сделайте это, прежде чем создавать конвейер.</span><span class="sxs-lookup"><span data-stu-id="3912a-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span></span> <span data-ttu-id="3912a-426">В JSON конвейера для свойства **IsPaused** задано значение false, поэтому конвейер запустится сразу по прошествии даты, указанной в параметре **start**.</span><span class="sxs-lookup"><span data-stu-id="3912a-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="3912a-427">В редакторе фабрики данных, нажмите кнопку **Создать конвейер** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="3912a-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span></span> <span data-ttu-id="3912a-428">Если команда не отображается, нажмите кнопку **... (многоточие)**, чтобы отобразить ее.</span><span class="sxs-lookup"><span data-stu-id="3912a-428">If you do not see the command, click **... (Ellipsis)** to see it.</span></span>
2. <span data-ttu-id="3912a-429">Замените сценарий JSON в правой области приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="3912a-429">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="3912a-430">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="3912a-430">Note the following points:</span></span>

   * <span data-ttu-id="3912a-431">В конвейере содержится одно действие типа **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="3912a-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="3912a-432">В **AssemblyName** задано имя библиотеки DLL **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="3912a-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="3912a-433">В **EntryPoint** — **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="3912a-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="3912a-434">По сути, это фрагмент кода \<пространство_имен\>.\<имя_класса\>.</span><span class="sxs-lookup"><span data-stu-id="3912a-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="3912a-435">Для параметра **PackageLinkedService** задано значение **StorageLinkedService**, которое указывает на хранилище BLOB-объектов, содержащее ZIP-файл настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="3912a-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="3912a-436">Если для входных и выходных файлов и ZIP-файла настраиваемого действия используются разные учетные записи хранения Azure, то необходимо создать другую связанную службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span></span> <span data-ttu-id="3912a-437">В этой статье предполагается использование одной и той же учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-437">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="3912a-438">Для **PackageFile** установлено значение **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="3912a-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="3912a-439">Используется формат \<контейнер_для_zip-файла\>/\<имя_zip-файла.zip\>.</span><span class="sxs-lookup"><span data-stu-id="3912a-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="3912a-440">Настраиваемое действие принимает **InputDataset** в качестве входных данных и **OutputDataset** — в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="3912a-441">Свойство **linkedServiceName** настраиваемого действия указывает на **AzureBatchLinkedService**, которое сообщает фабрике данных Azure, что необходимо запустить настраиваемое действие в пакетной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span></span>
   * <span data-ttu-id="3912a-442">Обратите внимание на параметр **concurrency**.</span><span class="sxs-lookup"><span data-stu-id="3912a-442">The **concurrency** setting is important.</span></span> <span data-ttu-id="3912a-443">Если используется значение по умолчанию, т. е. 1, то даже если в пуле пакетной службы Azure есть 2 или несколько вычислительных узлов, срезы обрабатываются по очереди.</span><span class="sxs-lookup"><span data-stu-id="3912a-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="3912a-444">Таким образом игнорируется возможность параллельной обработки пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="3912a-445">Если задать для параметра **concurrency** большее значение, например 2, это означает, что одновременно могут обрабатываться два среза (соответствующие двум задачам в пакетной службе Azure). В этом случае используются обе виртуальные машины в пуле пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span></span> <span data-ttu-id="3912a-446">Исходя из этого, укажите соответствующее значение для свойства concurrency.</span><span class="sxs-lookup"><span data-stu-id="3912a-446">Therefore, set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="3912a-447">По умолчанию на виртуальной машине в любой момент времени будет выполняться только одна задача (один срез).</span><span class="sxs-lookup"><span data-stu-id="3912a-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="3912a-448">Так происходит, потому что по умолчанию для параметра **Maximum tasks per VM** (Максимальное количество задач на виртуальную машину) задано значение 1 для пула пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span></span> <span data-ttu-id="3912a-449">В ходе выполнения необходимых требований создан пул и для этого свойства задано значение 2. Поэтому на виртуальной машине могут выполняться два среза фабрики данных одновременно.</span><span class="sxs-lookup"><span data-stu-id="3912a-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span></span>

    -   <span data-ttu-id="3912a-450">Для свойства **isPaused** по умолчанию установлено значение false.</span><span class="sxs-lookup"><span data-stu-id="3912a-450">**isPaused** property is set to false by default.</span></span> <span data-ttu-id="3912a-451">В этом примере конвейер запускается незамедлительно, потому что срезы приходятся на прошлое.</span><span class="sxs-lookup"><span data-stu-id="3912a-451">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="3912a-452">Для этого свойства можно задать значение true, чтобы приостановить работу конвейера. Чтобы перезапустить его, нужно снова установить значение false.</span><span class="sxs-lookup"><span data-stu-id="3912a-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>

    -   <span data-ttu-id="3912a-453">Разница между временем **начала** и временем **окончания** составляет пять часов, а срезы создаются каждый час. Таким образом конвейер создает пять срезов.</span><span class="sxs-lookup"><span data-stu-id="3912a-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="3912a-454">Чтобы развернуть конвейер, нажмите кнопку **Развернуть** на панели команд.</span><span class="sxs-lookup"><span data-stu-id="3912a-454">Click **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="3912a-455">Шаг 5. Тестирование конвейера</span><span class="sxs-lookup"><span data-stu-id="3912a-455">Step 5: Test the pipeline</span></span>
<span data-ttu-id="3912a-456">На этом шаге вы протестируете конвейер. Для этого файлы будут перенесены в папки входных данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-456">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="3912a-457">Сначала перенесем один файл в одну входную папку.</span><span class="sxs-lookup"><span data-stu-id="3912a-457">Let’s start with testing the pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="3912a-458">На портале Azure в колонке "Фабрика данных" щелкните **Схема**.</span><span class="sxs-lookup"><span data-stu-id="3912a-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="3912a-459">В представлении схемы дважды щелкните входной набор данных **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="3912a-459">In the diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="3912a-460">Должна появиться колонка **InputDataset** со всеми пятью срезами.</span><span class="sxs-lookup"><span data-stu-id="3912a-460">You should see the **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="3912a-461">Обратите внимание на значения в столбцах **Время начала среза** и **Время окончания среза** для каждого среза.</span><span class="sxs-lookup"><span data-stu-id="3912a-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="3912a-462">Теперь в **представлении схемы** щелкните **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="3912a-462">In the **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="3912a-463">Если срезы уже созданы, вы увидите пять выходных срезов данных в состоянии готовности.</span><span class="sxs-lookup"><span data-stu-id="3912a-463">You should see that the five output slices are in the Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="3912a-464">На портале Azure просмотрите **задачи**, связанные со **срезами**, а также сведения о том, на какой виртуальной машине выполнялся каждый срез.</span><span class="sxs-lookup"><span data-stu-id="3912a-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="3912a-465">Дополнительные сведения см. в разделе [Интеграция фабрики данных и пакетной службы](#data-factory-and-batch-integration).</span><span class="sxs-lookup"><span data-stu-id="3912a-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="3912a-466">Выходные файлы должны появиться в папке `outputfolder` контейнера `mycontainer` в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-466">You should see the output files in the `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="3912a-467">Должно появиться пять выходных файлов, по одному на каждый входной срез.</span><span class="sxs-lookup"><span data-stu-id="3912a-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="3912a-468">В каждом из выходных файлов должно быть содержимое, аналогичное приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="3912a-468">Each of the output file should have content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="3912a-469">На следующей схеме показано сопоставление срезов данных фабрики и задач в пакетной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span></span> <span data-ttu-id="3912a-470">В этом примере срез запускался всего один раз.</span><span class="sxs-lookup"><span data-stu-id="3912a-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="3912a-471">Теперь давайте попробуем использовать несколько файлов в папке.</span><span class="sxs-lookup"><span data-stu-id="3912a-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="3912a-472">Создайте файлы **file2.txt**, **file3.txt**, **file4.txt** и **file5.txt** с тем же содержимым, что и в файле file.txt в папке **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="3912a-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="3912a-473">В папке выходных данных **удалите** выходной файл **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="3912a-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="3912a-474">Теперь в колонке **OutputDataset** щелкните правой кнопкой мыши срез, для которого в столбце **Время начала среза** задано значение **11/16/2015 01:00:00 AM**, и выберите пункт **Запустить** для повторного выполнения и обработки среза.</span><span class="sxs-lookup"><span data-stu-id="3912a-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span></span> <span data-ttu-id="3912a-475">Теперь в срезе пять файлов вместо одного.</span><span class="sxs-lookup"><span data-stu-id="3912a-475">Now, the slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="3912a-476">Когда после запуска среза его состояние изменится на **Готов**, проверьте содержимое в выходном файле для этого среза (**2015-11-16-01.txt**) в папке `outputfolder` контейнера `mycontainer` в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="3912a-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="3912a-477">В выходном файле каждому файлу среза должна соответствовать одна строка.</span><span class="sxs-lookup"><span data-stu-id="3912a-477">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="3912a-478">Если не удалить выходной файл 2015-11-16-01.txt перед использованием пяти входных файлов, появится одна строка из предыдущего запуска среза и пять строк из текущего.</span><span class="sxs-lookup"><span data-stu-id="3912a-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="3912a-479">По умолчанию содержимое добавляется в выходной файл, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="3912a-479">By default, the content is appended to output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="3912a-480">Интеграция фабрики данных и пакетной службы</span><span class="sxs-lookup"><span data-stu-id="3912a-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="3912a-481">Служба фабрики данных создает в пакетной службе Azure задание с именем `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="3912a-481">The Data Factory service creates a job in Azure Batch with the name: `adf-poolname:job-xxx`.</span></span>

![Фабрика данных Azure — задания пакетной службы](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="3912a-483">Для каждого запуска действия среза в задании создается задача.</span><span class="sxs-lookup"><span data-stu-id="3912a-483">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="3912a-484">При наличии 10 срезов, готовых к обработке, в рамках этого задания создаются 10 задач.</span><span class="sxs-lookup"><span data-stu-id="3912a-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="3912a-485">Если в пуле доступны несколько вычислительных узлов, можно обрабатывать параллельно сразу несколько срезов.</span><span class="sxs-lookup"><span data-stu-id="3912a-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="3912a-486">Если для максимального количества задач на вычислительный узел установлено значение > 1, можно также выполнять сразу несколько срезов в одном цикле вычислений.</span><span class="sxs-lookup"><span data-stu-id="3912a-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span></span>

<span data-ttu-id="3912a-487">В этом примере имеется пять срезов, что соответствует пяти задачам в пакетной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="3912a-488">Так как для свойства **concurrency** задано значение **5** в JSON конвейера в фабрике данных Azure, а для параметра **Maximum tasks per VM** (Максимальное число задач на виртуальную машину) — **2** в пуле пакетной службы Azure с **2** виртуальными машинами, задачи будут выполняться очень быстро (просмотрите время начала и завершения задач).</span><span class="sxs-lookup"><span data-stu-id="3912a-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="3912a-489">На портале просмотрите задание пакетной службы и его задачи, связанные со **срезами** , а также сведения о том, на какой виртуальной машине выполнялся каждый срез.</span><span class="sxs-lookup"><span data-stu-id="3912a-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span></span>

![Фабрика данных Azure — задачи задания пакетной службы](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="3912a-491">Выполнение отладки конвейера</span><span class="sxs-lookup"><span data-stu-id="3912a-491">Debug the pipeline</span></span>
<span data-ttu-id="3912a-492">Отладка состоит из нескольких базовых методов:</span><span class="sxs-lookup"><span data-stu-id="3912a-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="3912a-493">Если для входного среза данных не установлено значение **Готово**, убедитесь, что структура входной папки правильная и что в ней существует файл file.txt.</span><span class="sxs-lookup"><span data-stu-id="3912a-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="3912a-494">В методе **Execute** настраиваемого действия используйте объект **IActivityLogger**, чтобы записывать в журнал сведения, которые помогут устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="3912a-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="3912a-495">Сообщения, записанные в журнал, сохраняются в файле user\_0.log.</span><span class="sxs-lookup"><span data-stu-id="3912a-495">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="3912a-496">В колонке **OutputDataset** щелкните срез, чтобы открыть для него колонку **Срез данных**.</span><span class="sxs-lookup"><span data-stu-id="3912a-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="3912a-497">Для этого среза будет указано значение **Запуски операции** .</span><span class="sxs-lookup"><span data-stu-id="3912a-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="3912a-498">Должно выполняться лишь одно действие.</span><span class="sxs-lookup"><span data-stu-id="3912a-498">You should see one activity run for the slice.</span></span> <span data-ttu-id="3912a-499">Если в командной строке щелкнуть **Запуск** , можно запустить другое действие для этого среза.</span><span class="sxs-lookup"><span data-stu-id="3912a-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="3912a-500">Если щелкнуть выполняемое действие, появится колонка **Подробности о выполнении операции** со списком файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="3912a-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="3912a-501">Записанные в журнал сообщения можно просмотреть в файле **user\_0.log**.</span><span class="sxs-lookup"><span data-stu-id="3912a-501">You see logged messages in the **user\_0.log** file.</span></span> <span data-ttu-id="3912a-502">Если возникнет ошибка, действие будет выполнено три раза, так как для количества повторных попыток в JSON-файле конвейера или действия задано значение 3.</span><span class="sxs-lookup"><span data-stu-id="3912a-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="3912a-503">Если щелкнуть выполняемое действие, отобразятся файлы журнала, которые можно использовать для устранения ошибки.</span><span class="sxs-lookup"><span data-stu-id="3912a-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="3912a-504">В списке файлов журнала щелкните **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="3912a-504">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="3912a-505">На панели справа отображаются результаты использования метода **IActivityLogger.Write** .</span><span class="sxs-lookup"><span data-stu-id="3912a-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="3912a-506">Проверьте файл system-0.log на наличие любых системных сообщений об ошибках или исключений.</span><span class="sxs-lookup"><span data-stu-id="3912a-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="3912a-507">Добавьте **PDB-файл** в ZIP-файл, чтобы в случае возникновения ошибки сведения об ошибке содержали, например, информацию о **стеке вызовов**.</span><span class="sxs-lookup"><span data-stu-id="3912a-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="3912a-508">Все файлы в ZIP-файле для пользовательского действия должны находиться на **верхнем уровне** без вложенных папок.</span><span class="sxs-lookup"><span data-stu-id="3912a-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="3912a-509">Убедитесь, что для параметров **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip) и **packageLinkedService** (должен указывать на хранилище BLOB-объектов Azure, содержащее ZIP-файл) установлены правильные значения.</span><span class="sxs-lookup"><span data-stu-id="3912a-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span></span>
6. <span data-ttu-id="3912a-510">Если ошибки устранены и необходимо повторно обработать срез, в колонке **OutputDataset** щелкните срез правой кнопкой мыши и выберите пункт **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="3912a-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="3912a-511">В хранилище BLOB-объектов Azure появится **контейнер** с именем `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="3912a-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="3912a-512">Этот контейнер не удаляется автоматически, но его можно безопасно удалить после завершения тестирования решения.</span><span class="sxs-lookup"><span data-stu-id="3912a-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span></span> <span data-ttu-id="3912a-513">Аналогичным образом решение фабрики данных создает **задание** пакетной службы Azure с именем `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="3912a-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="3912a-514">При необходимости после выполнения тестирования решения это задание можно удалить.</span><span class="sxs-lookup"><span data-stu-id="3912a-514">You can delete this job after you test the solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="3912a-515">Настраиваемое действие не использует файл **app.config** из пакета.</span><span class="sxs-lookup"><span data-stu-id="3912a-515">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="3912a-516">Поэтому, если код считывает какие-либо строки подключения из файла конфигурации, это не сработает во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="3912a-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="3912a-517">При использовании пакетной службы Azure рекомендуется хранить все секреты в **хранилище ключей Azure**. Кроме того, следует использовать субъект-службу на основе сертификата для защиты хранилища ключей и переместить сертификат в пул пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="3912a-518">В этом случае пользовательское действие .NET в среде выполнения сможет использовать секреты из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="3912a-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="3912a-519">Это универсальное решение, которое можно использовать для любых типов секрета, а не только строк подключения.</span><span class="sxs-lookup"><span data-stu-id="3912a-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span></span>

    <span data-ttu-id="3912a-520">Существует и более простое (но не самое лучшее) решение: можно создать **связанную службу SQL Azure** с параметрами строки подключения, набор данных, использующий связанную службу, и привязать его как фиктивный набор входных данных к настраиваемому действию .NET.</span><span class="sxs-lookup"><span data-stu-id="3912a-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="3912a-521">После этого вы сможете получить доступ к строке подключения связанной службы из кода пользовательского действия — в среде выполнения она должна работать нормально.</span><span class="sxs-lookup"><span data-stu-id="3912a-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="3912a-522">Расширение примера</span><span class="sxs-lookup"><span data-stu-id="3912a-522">Extend the sample</span></span>
<span data-ttu-id="3912a-523">Для получения дополнительных сведений о функциях фабрики данных Azure и пакетной службы Azure этот пример можно расширить.</span><span class="sxs-lookup"><span data-stu-id="3912a-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="3912a-524">Например, чтобы обрабатывать срезы с использованием другого диапазона времени, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="3912a-524">For example, to process slices in a different time range, do the following steps:</span></span>

1. <span data-ttu-id="3912a-525">Добавьте в папку `inputfolder` подпапки 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 и поместите в них входные файлы.</span><span class="sxs-lookup"><span data-stu-id="3912a-525">Add the following subfolders in the `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="3912a-526">Измените время окончания для конвейера с `2015-11-16T05:00:00Z` на `2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="3912a-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="3912a-527">В **представлении схемы** дважды щелкните **InputDataset** и убедитесь, что для входных срезов отображается состояние "Готово".</span><span class="sxs-lookup"><span data-stu-id="3912a-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span></span> <span data-ttu-id="3912a-528">Дважды щелкните **OuptutDataset** , чтобы просмотреть состояние выходных срезов.</span><span class="sxs-lookup"><span data-stu-id="3912a-528">Double-click **OuptutDataset** to see the state of output slices.</span></span> <span data-ttu-id="3912a-529">Если отображается состояние "Готово", проверьте выходные файлы в выходной папке.</span><span class="sxs-lookup"><span data-stu-id="3912a-529">If they are in Ready state, check the output folder for the output files.</span></span>
2. <span data-ttu-id="3912a-530">Укажите для параметра **concurrency** большее или меньшее значение, чтобы понять, как это влияет на производительность решения, особенно на обработку в пакетной службе Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span></span> <span data-ttu-id="3912a-531">(Дополнительные сведения о параметре **concurrency** см. в разделе "Шаг 4. Создание и запуск конвейера".)</span><span class="sxs-lookup"><span data-stu-id="3912a-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span></span>
3. <span data-ttu-id="3912a-532">Создайте пул с большим или меньшим значением для параметра **Maximum tasks per VM** (Максимальное число задач на виртуальную машину).</span><span class="sxs-lookup"><span data-stu-id="3912a-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="3912a-533">Чтобы воспользоваться созданным пулом, обновите связанную службу пакетной службы Azure в решении фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span></span> <span data-ttu-id="3912a-534">(Дополнительные сведения о параметре **Maximum tasks per VM** (Максимальное число задач на виртуальную машину) см. в разделе "Шаг 4. Создание и запуск конвейера".)</span><span class="sxs-lookup"><span data-stu-id="3912a-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="3912a-535">Создайте пул пакетной службы Azure с использованием функции **автомасштабирования** .</span><span class="sxs-lookup"><span data-stu-id="3912a-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="3912a-536">Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure представляет собой динамическую настройку вычислительной мощности, используемой вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="3912a-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="3912a-537">Приведенный пример формулы обеспечивает следующее поведение: при создании пул изначально содержит одну виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="3912a-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="3912a-538">Метрика $PendingTasks определяет количество задач в состоянии выполнения и активном состоянии (в очереди).</span><span class="sxs-lookup"><span data-stu-id="3912a-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="3912a-539">Формула находит среднее число ожидающих выполнения задач за последние 180 секунд и соответствующим образом задает значение TargetDedicated.</span><span class="sxs-lookup"><span data-stu-id="3912a-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="3912a-540">Благодаря этому значение TargetDedicated никогда не превысит 25 виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="3912a-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="3912a-541">Таким образом, по мере поступления новых задач пул автоматически увеличивается, а по мере их завершения виртуальные машины высвобождаются по одной, и функция автоматического масштабирования уменьшает пул.</span><span class="sxs-lookup"><span data-stu-id="3912a-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="3912a-542">Значения startingNumberOfVMs и maxNumberofVMs можно настроить в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="3912a-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>
 
    <span data-ttu-id="3912a-543">Формула автоматического масштабирования:</span><span class="sxs-lookup"><span data-stu-id="3912a-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="3912a-544">Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](../batch/batch-automatic-scaling.md).</span><span class="sxs-lookup"><span data-stu-id="3912a-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="3912a-545">Если в пуле используется [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)(значение по умолчанию), пакетной службе может потребоваться 15–30 минут на подготовку виртуальной машины перед выполнением настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="3912a-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="3912a-546">Если пул использует другое значение autoScaleEvaluationInterval, пакетная служба может затрачивать autoScaleEvaluationInterval плюс 10 минут.</span><span class="sxs-lookup"><span data-stu-id="3912a-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="3912a-547">В примере решения метод **Execute** вызывает метод **Calculate**, который обрабатывает входной срез данных для создания выходного среза данных.</span><span class="sxs-lookup"><span data-stu-id="3912a-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="3912a-548">Можно написать собственный метод для обработки входных данных и заменить вызов метода Calculate в методе Execute его вызовом.</span><span class="sxs-lookup"><span data-stu-id="3912a-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="3912a-549">Дальнейшие действия. Использование данных</span><span class="sxs-lookup"><span data-stu-id="3912a-549">Next steps: Consume the data</span></span>
<span data-ttu-id="3912a-550">После обработки данных их можно использовать в интерактивных инструментах, например в **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="3912a-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="3912a-551">Ниже приведены ссылки на статьи, в которых представлены общие сведения о Power BI и информация о том, как использовать это средство в Azure.</span><span class="sxs-lookup"><span data-stu-id="3912a-551">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="3912a-552">Изучение набора данных в Power BI</span><span class="sxs-lookup"><span data-stu-id="3912a-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="3912a-553">Начало работы с Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3912a-553">Getting started with the Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="3912a-554">Обновление данных в Power BI</span><span class="sxs-lookup"><span data-stu-id="3912a-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="3912a-555">Общая информация об Azure и Power BI</span><span class="sxs-lookup"><span data-stu-id="3912a-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="3912a-556">Ссылки</span><span class="sxs-lookup"><span data-stu-id="3912a-556">References</span></span>
* [<span data-ttu-id="3912a-557">Фабрика данных Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="3912a-558">Введение в службу фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-558">Introduction to Azure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="3912a-559">Начало работы с фабрикой данных Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="3912a-560">Использование настраиваемых действий в конвейере фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="3912a-561">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="3912a-562">Основные сведения о пакетной службе Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="3912a-563">Обзор функций пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="3912a-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="3912a-564">Создание учетной записи пакетной службы Azure на портале Azure и управление ею</span><span class="sxs-lookup"><span data-stu-id="3912a-564">Create and manage Azure Batch account in the Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="3912a-565">Начало работы с библиотекой Пакетной службы Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="3912a-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
