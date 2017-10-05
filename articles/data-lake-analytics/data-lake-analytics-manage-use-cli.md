---
title: "Управление Azure Data Lake Analytics с помощью интерфейса командной строки Azure | Документация Майкрософт"
description: "Узнайте, как управлять учетными записями, источниками данных, пользователями и заданиями аналитики озера данных Azure с помощью интерфейса командной строки Azure."
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f90bada3572c0ed40b07d76ec02c1b499bbd1428
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="109aa-103">Управление аналитикой озера данных Azure с помощью интерфейса командной строки (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="109aa-104">Узнайте, как управлять учетными записями, источниками данных, пользователями и заданиями Azure Data Lake Analytics с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="109aa-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="109aa-105">Для просмотра статей, посвященных управлению с помощью других инструментов, щелкните селектор вкладок выше.</span><span class="sxs-lookup"><span data-stu-id="109aa-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="109aa-106">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="109aa-106">**Prerequisites**</span></span>

<span data-ttu-id="109aa-107">Перед началом работы с этим учебником необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="109aa-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="109aa-108">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="109aa-108">**An Azure subscription**.</span></span> <span data-ttu-id="109aa-109">См. страницу [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="109aa-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="109aa-110">**Интерфейс командной строки Azure**.</span><span class="sxs-lookup"><span data-stu-id="109aa-110">**Azure CLI**.</span></span> <span data-ttu-id="109aa-111">См. статью [Установка и настройка интерфейса командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="109aa-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="109aa-112">Для выполнения этой демонстрации загрузите и установите **предварительный выпуск** [программ CLI Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) .</span><span class="sxs-lookup"><span data-stu-id="109aa-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="109aa-113">**Пройдите проверку подлинности**с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="109aa-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="109aa-114">Дополнительные сведения об аутентификации с помощью рабочей или учебной учетной записи см. в статье [Подключение к среде Azure с использованием интерфейса командной строки Azure (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="109aa-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="109aa-115">**Переключитесь в режим диспетчера ресурсов Azure**с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="109aa-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="109aa-116">**Получение списка команд хранилища озера данных и аналитики озера данных**</span><span class="sxs-lookup"><span data-stu-id="109aa-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="109aa-117">Управление учетными записями</span><span class="sxs-lookup"><span data-stu-id="109aa-117">Manage accounts</span></span>
<span data-ttu-id="109aa-118">Перед выполнением любого задания аналитики озера данных необходимо иметь учетную запись аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="109aa-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="109aa-119">В отличие от Azure HDInsight учетная запись аналитики не оплачивается, если ни одно задание не выполняется.</span><span class="sxs-lookup"><span data-stu-id="109aa-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="109aa-120">Вы платите только за время, когда выполняется задание.</span><span class="sxs-lookup"><span data-stu-id="109aa-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="109aa-121">Дополнительные сведения см. в разделе [Обзор аналитики озера данных Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="109aa-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="109aa-122">Создание учетных записей</span><span class="sxs-lookup"><span data-stu-id="109aa-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="109aa-123">Обновление учетных записей</span><span class="sxs-lookup"><span data-stu-id="109aa-123">Update accounts</span></span>
<span data-ttu-id="109aa-124">Следующая команда используется для обновления свойств существующей учетной записи данных озера аналитики.</span><span class="sxs-lookup"><span data-stu-id="109aa-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="109aa-125">Список учетных записей</span><span class="sxs-lookup"><span data-stu-id="109aa-125">List accounts</span></span>
<span data-ttu-id="109aa-126">Список учетных записей аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="109aa-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="109aa-127">Список учетных записей аналитики озера данных в конкретной группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="109aa-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="109aa-128">Получение сведений о конкретной учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="109aa-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="109aa-129">Удаление учетных записей аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="109aa-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="109aa-130">Управление источниками данных учетной записи</span><span class="sxs-lookup"><span data-stu-id="109aa-130">Manage account data sources</span></span>
<span data-ttu-id="109aa-131">Аналитика озера данных в настоящее время поддерживает следующие источники данных:</span><span class="sxs-lookup"><span data-stu-id="109aa-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="109aa-132">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="109aa-133">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="109aa-134">При создании учетной записи аналитики необходимо указать учетную запись хранения озера данных Azure в качестве учетной записи хранения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="109aa-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="109aa-135">Учетная запись хранения озера данных по умолчанию используется для хранения метаданных задания и журналов аудита задания.</span><span class="sxs-lookup"><span data-stu-id="109aa-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="109aa-136">После создания учетной записи аналитики можно добавить дополнительные учетные записи хранения озера данных и учетные записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="109aa-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="109aa-137">Поиск учетной записи хранения озера данных по умолчанию</span><span class="sxs-lookup"><span data-stu-id="109aa-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="109aa-138">Значение находится в списке свойств: datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="109aa-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="109aa-139">Добавление дополнительных учетных записей хранения больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="109aa-140">Поддерживаются только короткие имена хранилищ BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="109aa-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="109aa-141">Не следует использовать полное доменное имя, например "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="109aa-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="109aa-142">Добавление дополнительных учетных записей хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="109aa-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="109aa-143">[-d] — это необязательный параметр, указывающий, является ли добавляемое озеро данных учетной записью озера данных по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="109aa-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="109aa-144">Обновление существующего источника данных</span><span class="sxs-lookup"><span data-stu-id="109aa-144">Update existing data source</span></span>
<span data-ttu-id="109aa-145">Задание существующей учетной записи хранилища озера данных в качестве учетной записи по умолчанию</span><span class="sxs-lookup"><span data-stu-id="109aa-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="109aa-146">Обновление существующего ключа учетной записи хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="109aa-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="109aa-147">Список источников данных</span><span class="sxs-lookup"><span data-stu-id="109aa-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Источник данных списка аналитики озера данных](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="109aa-149">Удаление источников данных</span><span class="sxs-lookup"><span data-stu-id="109aa-149">Delete data sources:</span></span>
<span data-ttu-id="109aa-150">Удаление учетной записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="109aa-151">Удаление учетной записи хранения BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="109aa-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="109aa-152">Управление заданиями</span><span class="sxs-lookup"><span data-stu-id="109aa-152">Manage jobs</span></span>
<span data-ttu-id="109aa-153">Для создания любого задания требуется учетная запись аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="109aa-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="109aa-154">Дополнительные сведения см. в разделе [Управление учетными записями Data Lake Analytics](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="109aa-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="109aa-155">Список заданий</span><span class="sxs-lookup"><span data-stu-id="109aa-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Источник данных списка аналитики озера данных](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="109aa-157">Получение сведений о задании</span><span class="sxs-lookup"><span data-stu-id="109aa-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="109aa-158">Отправка заданий</span><span class="sxs-lookup"><span data-stu-id="109aa-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="109aa-159">Приоритет задания по умолчанию — 1000, а степень параллелизма по умолчанию для задания — 1.</span><span class="sxs-lookup"><span data-stu-id="109aa-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="109aa-160">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="109aa-160">Cancel jobs</span></span>
<span data-ttu-id="109aa-161">Используйте команду list, чтобы найти идентификатор задания, а затем используйте команду cancel для отмены задания.</span><span class="sxs-lookup"><span data-stu-id="109aa-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="109aa-162">Управление каталогом</span><span class="sxs-lookup"><span data-stu-id="109aa-162">Manage catalog</span></span>
<span data-ttu-id="109aa-163">Каталог U-SQL используется для структурирования данных и кода, чтобы их могли совместно использовать сценарии U-SQL.</span><span class="sxs-lookup"><span data-stu-id="109aa-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="109aa-164">Каталог обеспечивает максимальную производительность, возможную с данными в озере данных Azure.</span><span class="sxs-lookup"><span data-stu-id="109aa-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="109aa-165">Дополнительные сведения см. в разделе [Использование каталога U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="109aa-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="109aa-166">Список элементов каталога</span><span class="sxs-lookup"><span data-stu-id="109aa-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="109aa-167">К типа относятся база данных, схема, сборка, внешний источник данных, таблица, функция с табличным значением или статистика таблицы.</span><span class="sxs-lookup"><span data-stu-id="109aa-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="109aa-168">Использование групп ARM</span><span class="sxs-lookup"><span data-stu-id="109aa-168">Use ARM groups</span></span>
<span data-ttu-id="109aa-169">Обычно приложения состоят из множества компонентов, например веб-приложения, базы данных, сервера базы данных, хранилища и служб сторонних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="109aa-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="109aa-170">Вы можете развертывать, обновлять, отслеживать или удалять все ресурсы для приложения в рамках одной скоординированной операции.</span><span class="sxs-lookup"><span data-stu-id="109aa-170">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="109aa-171">Для развертывания вы используете шаблон, который можно использовать для разных сред, в том числе для тестовой, промежуточной и рабочей.</span><span class="sxs-lookup"><span data-stu-id="109aa-171">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="109aa-172">Вы можете уточнить счета для своей организации, просмотрев сведенные затраты для всей группы.</span><span class="sxs-lookup"><span data-stu-id="109aa-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="109aa-173">Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="109aa-173">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="109aa-174">в статье [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="109aa-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="109aa-175">Служба аналитики озера данных может включать следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="109aa-175">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="109aa-176">Учетная запись аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="109aa-177">Требуемая учетная запись хранения озера данных Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="109aa-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="109aa-178">Дополнительные учетные записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="109aa-179">Дополнительные учетные записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="109aa-180">Можно создать все эти компоненты в одной группе ARM, чтобы ими было проще управлять.</span><span class="sxs-lookup"><span data-stu-id="109aa-180">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Аналитика озера данных Azure: учетная запись и хранилище](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="109aa-182">Учетная запись аналитики озера данных и зависимые учетные записи хранения должны находиться в одном центре обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="109aa-182">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="109aa-183">Однако группа ARM может находиться в другом центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="109aa-183">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="109aa-184">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="109aa-184">See also</span></span>
* [<span data-ttu-id="109aa-185">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="109aa-186">Начало работы с аналитикой озера данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="109aa-187">Управление аналитикой озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="109aa-188">Мониторинг заданий аналитики озера данных Azure и устранение связанных с ними неполадок с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="109aa-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

