---
title: "Аналитика Озера данных Azure, с помощью интерфейса командной строки Azure aaaManage | Документы Microsoft"
description: "Узнайте об использовании заданий учетные записи аналитики Озера данных toomanage, источники данных и пользователей с помощью Azure CLI"
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
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="3ce14-103">Управление аналитикой озера данных Azure с помощью интерфейса командной строки (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="3ce14-104">Узнайте, как учетные записи toomanage аналитики Озера данных Azure, источники данных, пользователей и заданий с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3ce14-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, users, and jobs using hello Azure CLI.</span></span> <span data-ttu-id="3ce14-105">toosee статьи, посвященные управлению с помощью других средств, щелкните выше выберите вкладку hello.</span><span class="sxs-lookup"><span data-stu-id="3ce14-105">toosee management topics using other tools, click hello tab select above.</span></span>


<span data-ttu-id="3ce14-106">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="3ce14-106">**Prerequisites**</span></span>

<span data-ttu-id="3ce14-107">Прежде чем начать работу с учебником, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="3ce14-107">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="3ce14-108">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="3ce14-108">**An Azure subscription**.</span></span> <span data-ttu-id="3ce14-109">См. страницу [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ce14-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3ce14-110">**Интерфейс командной строки Azure**.</span><span class="sxs-lookup"><span data-stu-id="3ce14-110">**Azure CLI**.</span></span> <span data-ttu-id="3ce14-111">См. статью [Установка и настройка интерфейса командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3ce14-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="3ce14-112">Загрузите и установите hello **предварительного выпуска** [средства Azure CLI](https://github.com/MicrosoftBigData/AzureDataLake/releases) чтобы toocomplete этой демонстрации.</span><span class="sxs-lookup"><span data-stu-id="3ce14-112">Download and install hello **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order toocomplete this demo.</span></span>
* <span data-ttu-id="3ce14-113">**Проверка подлинности**, с использованием hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3ce14-113">**Authentication**, using hello following command:</span></span>
  
        azure login
    <span data-ttu-id="3ce14-114">Дополнительные сведения о проверке подлинности с помощью рабочей или учебной учетной записи см. в разделе [подключение tooan подписки Azure из hello Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="3ce14-114">For more information on authenticating using a work or school account, see [Connect tooan Azure subscription from hello Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="3ce14-115">**Переключите режим диспетчера ресурсов Azure toohello**, с использованием hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3ce14-115">**Switch toohello Azure Resource Manager mode**, using hello following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="3ce14-116">**toolist hello хранилища Озера данных и аналитики Озера данных команды:**</span><span class="sxs-lookup"><span data-stu-id="3ce14-116">**toolist hello Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="3ce14-117">Управление учетными записями</span><span class="sxs-lookup"><span data-stu-id="3ce14-117">Manage accounts</span></span>
<span data-ttu-id="3ce14-118">Перед выполнением любого задания аналитики озера данных необходимо иметь учетную запись аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="3ce14-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="3ce14-119">В отличие от Azure HDInsight учетная запись аналитики не оплачивается, если ни одно задание не выполняется.</span><span class="sxs-lookup"><span data-stu-id="3ce14-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="3ce14-120">Вы платите только за время hello, при выполнении задания.</span><span class="sxs-lookup"><span data-stu-id="3ce14-120">You only pay for hello time when it is running a job.</span></span>  <span data-ttu-id="3ce14-121">Дополнительные сведения см. в разделе [Обзор аналитики озера данных Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ce14-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="3ce14-122">Создание учетных записей</span><span class="sxs-lookup"><span data-stu-id="3ce14-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="3ce14-123">Обновление учетных записей</span><span class="sxs-lookup"><span data-stu-id="3ce14-123">Update accounts</span></span>
<span data-ttu-id="3ce14-124">Hello следующая команда обновляет свойства hello существующей учетной записи аналитики Озера данных</span><span class="sxs-lookup"><span data-stu-id="3ce14-124">hello following command updates hello properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="3ce14-125">Список учетных записей</span><span class="sxs-lookup"><span data-stu-id="3ce14-125">List accounts</span></span>
<span data-ttu-id="3ce14-126">Список учетных записей аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="3ce14-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="3ce14-127">Список учетных записей аналитики озера данных в конкретной группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="3ce14-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="3ce14-128">Получение сведений о конкретной учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="3ce14-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="3ce14-129">Удаление учетных записей аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="3ce14-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="3ce14-130">Управление источниками данных учетной записи</span><span class="sxs-lookup"><span data-stu-id="3ce14-130">Manage account data sources</span></span>
<span data-ttu-id="3ce14-131">Аналитика Озера данных в настоящее время поддерживает следующие источники данных hello:</span><span class="sxs-lookup"><span data-stu-id="3ce14-131">Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="3ce14-132">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="3ce14-133">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="3ce14-134">При создании учетной записи аналитики, необходимо назначить хранилища Озера данных Azure учетная запись toobe hello по умолчанию учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3ce14-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account toobe hello default storage account.</span></span> <span data-ttu-id="3ce14-135">Hello учетной записи хранения по умолчанию ADL используется toostore метаданные задания и задания журналы аудита.</span><span class="sxs-lookup"><span data-stu-id="3ce14-135">hello default ADL storage account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="3ce14-136">После создания учетной записи аналитики можно добавить дополнительные учетные записи хранения озера данных и учетные записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce14-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-hello-default-adl-storage-account"></a><span data-ttu-id="3ce14-137">Найти учетную запись хранения ADL по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="3ce14-137">Find hello default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="3ce14-138">значение Hello указана в списке свойств: datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="3ce14-138">hello value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="3ce14-139">Добавление дополнительных учетных записей хранения больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="3ce14-140">Поддерживаются только короткие имена хранилищ BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="3ce14-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="3ce14-141">Не следует использовать полное доменное имя, например "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="3ce14-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="3ce14-142">Добавление дополнительных учетных записей хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="3ce14-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="3ce14-143">[-d] — tooindicate необязательный ключ, является ли hello Озера данных добавляется учетная запись Озера данных по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="3ce14-143">[-d] is an optional switch tooindicate whether hello Data Lake being added is hello default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="3ce14-144">Обновление существующего источника данных</span><span class="sxs-lookup"><span data-stu-id="3ce14-144">Update existing data source</span></span>
<span data-ttu-id="3ce14-145">tooset существующего хранилища Озера данных учетной записи toobe hello значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="3ce14-145">tooset an existing Data Lake Store account toobe hello default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="3ce14-146">tooupdate существующего ключа учетной записи хранилища больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="3ce14-146">tooupdate an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="3ce14-147">Список источников данных</span><span class="sxs-lookup"><span data-stu-id="3ce14-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Источник данных списка аналитики озера данных](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="3ce14-149">Удаление источников данных</span><span class="sxs-lookup"><span data-stu-id="3ce14-149">Delete data sources:</span></span>
<span data-ttu-id="3ce14-150">toodelete учетной записи хранилища Озера данных:</span><span class="sxs-lookup"><span data-stu-id="3ce14-150">toodelete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="3ce14-151">toodelete учетной записи хранилища больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="3ce14-151">toodelete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="3ce14-152">Управление заданиями</span><span class="sxs-lookup"><span data-stu-id="3ce14-152">Manage jobs</span></span>
<span data-ttu-id="3ce14-153">Для создания любого задания требуется учетная запись аналитики озера данных.</span><span class="sxs-lookup"><span data-stu-id="3ce14-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="3ce14-154">Дополнительные сведения см. в разделе [Управление учетными записями Data Lake Analytics](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="3ce14-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="3ce14-155">Список заданий</span><span class="sxs-lookup"><span data-stu-id="3ce14-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Источник данных списка аналитики озера данных](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="3ce14-157">Получение сведений о задании</span><span class="sxs-lookup"><span data-stu-id="3ce14-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="3ce14-158">Отправка заданий</span><span class="sxs-lookup"><span data-stu-id="3ce14-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="3ce14-159">приоритет по умолчанию Hello задания равно 1000, а степень параллелизма для задания hello по умолчанию — 1.</span><span class="sxs-lookup"><span data-stu-id="3ce14-159">hello default priority of a job is 1000, and hello default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="3ce14-160">Отмена задания</span><span class="sxs-lookup"><span data-stu-id="3ce14-160">Cancel jobs</span></span>
<span data-ttu-id="3ce14-161">Использовать идентификатор задания hello toofind команда hello списка, а затем использовать задание hello toocancel "Отмена".</span><span class="sxs-lookup"><span data-stu-id="3ce14-161">Use hello list command toofind hello job id, and then use cancel toocancel hello job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="3ce14-162">Управление каталогом</span><span class="sxs-lookup"><span data-stu-id="3ce14-162">Manage catalog</span></span>
<span data-ttu-id="3ce14-163">каталог Hello U-SQL является toostructure используемых данных и кода, поэтому они могут совместно использоваться сценарии U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3ce14-163">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="3ce14-164">Hello каталога включает hello максимально возможную производительность с данными в Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce14-164">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="3ce14-165">Дополнительные сведения см. в разделе [Использование каталога U-SQL](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="3ce14-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="3ce14-166">Список элементов каталога</span><span class="sxs-lookup"><span data-stu-id="3ce14-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="3ce14-167">типы Hello включают базы данных, схемы, сборки, внешний источник данных, таблицы, возвращающей табличное значение функции или статистики таблицы.</span><span class="sxs-lookup"><span data-stu-id="3ce14-167">hello types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="3ce14-168">Использование групп ARM</span><span class="sxs-lookup"><span data-stu-id="3ce14-168">Use ARM groups</span></span>
<span data-ttu-id="3ce14-169">Обычно приложения состоят из множества компонентов, например веб-приложения, базы данных, сервера базы данных, хранилища и служб сторонних поставщиков.</span><span class="sxs-lookup"><span data-stu-id="3ce14-169">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="3ce14-170">Диспетчер ресурсов Azure (ARM) позволяет toowork с ресурсами hello в приложении как группы, который ссылается tooas группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce14-170">Azure Resource Manager (ARM) enables you toowork with hello resources in your application as a group, referred tooas an Azure Resource Group.</span></span> <span data-ttu-id="3ce14-171">Можно развернуть, обновления, отслеживания или удалить все ресурсы hello для вашего приложения, в один, согласованной операции.</span><span class="sxs-lookup"><span data-stu-id="3ce14-171">You can deploy, update, monitor or delete all of hello resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="3ce14-172">Вы можете уточнить счета для своей организации, просмотрев сведенные затраты для всей группы.</span><span class="sxs-lookup"><span data-stu-id="3ce14-172">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="3ce14-173">Можно уточнить выставления счетов для вашей организации, просмотрев hello сведенные затраты для всей группы hello.</span><span class="sxs-lookup"><span data-stu-id="3ce14-173">You can clarify billing for your organization by viewing hello rolled-up costs for hello entire group.</span></span> <span data-ttu-id="3ce14-174">в статье [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ce14-174">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="3ce14-175">Служба аналитики Озера данных могут включать hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="3ce14-175">A Data Lake Analytics service can include hello following components:</span></span>

* <span data-ttu-id="3ce14-176">Учетная запись аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-176">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="3ce14-177">Требуемая учетная запись хранения озера данных Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3ce14-177">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="3ce14-178">Дополнительные учетные записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-178">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="3ce14-179">Дополнительные учетные записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-179">Additional Azure Storage accounts</span></span>

<span data-ttu-id="3ce14-180">Можно создать все эти компоненты в группе один toomake группы ARM их проще toomanage.</span><span class="sxs-lookup"><span data-stu-id="3ce14-180">You can create all these components under one ARM group toomake them easier toomanage.</span></span>

![Аналитика озера данных Azure: учетная запись и хранилище](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="3ce14-182">Учетную запись аналитики Озера данных и учетных записей хранилища зависимых hello должны быть помещены в hello же центре обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce14-182">A Data Lake Analytics account and hello dependent storage accounts must be placed in hello same Azure data center.</span></span>
<span data-ttu-id="3ce14-183">Однако Hello ARM группы могут быть расположены в другом центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="3ce14-183">hello ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="3ce14-184">См. также</span><span class="sxs-lookup"><span data-stu-id="3ce14-184">See also</span></span>
* [<span data-ttu-id="3ce14-185">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-185">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="3ce14-186">Начало работы с аналитикой озера данных с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-186">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="3ce14-187">Управление аналитикой озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-187">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="3ce14-188">Мониторинг заданий аналитики озера данных Azure и устранение связанных с ними неполадок с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="3ce14-188">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

