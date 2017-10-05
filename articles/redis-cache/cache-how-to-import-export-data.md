---
title: "Импорт и экспорт данных в кэше Redis для Azure | Документация Майкрософт"
description: "Вы можете узнать, как импортировать данные в хранилище BLOB-объектов и экспортировать их оттуда с использованием экземпляров кэша Redis для Azure категории \"Премиум\""
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: 5e6d731f0a1cecc1a191c74a45e37a9b94fd98ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="d4561-103">Импорт и экспорт данных в кэше Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="d4561-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="d4561-104">Импорта и экспорт являются операциями управления данными в кэше Redis для Azure, которые позволяют импортировать данные в кэш Redis для Azure или экспортировать их оттуда путем импорта и экспорта моментального снимка базы данных кэша Redis (RDB) из кэша уровня "Премиум" в большой двоичный объект в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="d4561-104">Import/Export is an Azure Redis Cache data management operation, which allows you to import data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="d4561-105">**Экспорт**. Моментальные снимки в формате RDB из кэша Redis для Azure можно экспортировать в страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="d4561-105">**Export** - you can export your Azure Redis Cache RDB snapshots to a Page Blob.</span></span>
- <span data-ttu-id="d4561-106">**Импорт**. Моментальные снимки в формате RDB можно импортировать в кэш Redis для Azure из страничного или блочного BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="d4561-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="d4561-107">Функция импорта/экспорта дает возможность переключаться между различными экземплярами кэша Redis для Azure или заполнять кэш данными перед использованием.</span><span class="sxs-lookup"><span data-stu-id="d4561-107">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="d4561-108">Эта статья содержит руководство по импорту и экспорту данных в кэше Redis для Azure, а также ответы на часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="d4561-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides the answers to commonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4561-109">Функция импорта/экспорта находится на этапе предварительной версии и доступна только для кэшей [категории "Премиум"](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="d4561-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="d4561-110">Импорт</span><span class="sxs-lookup"><span data-stu-id="d4561-110">Import</span></span>
<span data-ttu-id="d4561-111">Импорт можно использовать для переноса RDB-файлов, совместимых с Redis, с сервера Redis, запущенного в любом облаке или любой среде, включая Redis в Linux, Windows, или у любого поставщика облачных служб, такого как Amazon Web Services или другого.</span><span class="sxs-lookup"><span data-stu-id="d4561-111">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="d4561-112">Импорт данных позволяет легко создать кэш, предварительно заполненный данными.</span><span class="sxs-lookup"><span data-stu-id="d4561-112">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="d4561-113">Во время импорта кэш Redis для Azure загружает RDB-файлы из службы хранилища Azure в память, а затем вставляет в кэш ключи.</span><span class="sxs-lookup"><span data-stu-id="d4561-113">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory and then inserts the keys into the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="d4561-114">Перед началом операции импорта убедитесь, что RDB-файл или RDB-файлы базы данных Redis переданы в страничные или блочные BLOB-объекты в службе хранилища Azure, размещенные в том же регионе и подписке, что и ваш экземпляр кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="d4561-114">Before beginning the import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in the same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="d4561-115">Дополнительные сведения см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d4561-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="d4561-116">Если вы экспортировали RDB-файл с помощью функции [экспорта кэша Redis для Azure](#export), то этот файл уже находится в страничном BLOB-объекте и готов к импорту.</span><span class="sxs-lookup"><span data-stu-id="d4561-116">If you exported your RDB file using the [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="d4561-117">Чтобы импортировать один или несколько экспортированных больших двоичных объектов кэша, [перейдите к кэшу](cache-configure.md#configure-redis-cache-settings) на портале Azure и нажмите кнопку **Импорт данных** в **меню ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="d4561-117">To import one or more exported cache blobs, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Import data** from the **Resource menu**.</span></span>

    ![Импорт данных][cache-import-data]
2. <span data-ttu-id="d4561-119">Щелкните **Выберите BLOB-объекты** и выберите учетную запись хранения, содержащую данные для импорта.</span><span class="sxs-lookup"><span data-stu-id="d4561-119">Click **Choose Blob(s)** and select the storage account that contains the data to import.</span></span>

    ![Выбор учетной записи хранения][cache-import-choose-storage-account]
3. <span data-ttu-id="d4561-121">Щелкните контейнер, содержащий данные для импорта.</span><span class="sxs-lookup"><span data-stu-id="d4561-121">Click the container that contains the data to import.</span></span>

    ![Выберите контейнер][cache-import-choose-container]
4. <span data-ttu-id="d4561-123">Выберите один или несколько BLOB-объектов для импорта, щелкнув область слева от имени BLOB-объекта и выбрав пункт **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d4561-123">Select one or more blobs to import by clicking the area to the left of the blob name, and then click **Select**.</span></span>

    ![Выберите BLOB-объекты][cache-import-choose-blobs]
5. <span data-ttu-id="d4561-125">Щелкните **Импорт** для начала процесса импорта.</span><span class="sxs-lookup"><span data-stu-id="d4561-125">Click **Import** to begin the import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d4561-126">Во время процедуры импорта кэш недоступен для клиентов кэша, а все существующие в нем данные удаляются.</span><span class="sxs-lookup"><span data-stu-id="d4561-126">The cache is not accessible by cache clients during the import process, and any existing data in the cache is deleted.</span></span>
   >
   >

    ![Импорт][cache-import-blobs]

    <span data-ttu-id="d4561-128">Ход выполнения операции импорта можно отслеживать, выбирая уведомления на портале Azure или просматривая события в [журнале аудита](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="d4561-128">You can monitor the progress of the import operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Ход выполнения импорта][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="d4561-130">экспорт.</span><span class="sxs-lookup"><span data-stu-id="d4561-130">Export</span></span>
<span data-ttu-id="d4561-131">Экспорт позволяет экспортировать данные, хранящиеся в кэше Redis для Azure в RDB-файлы, совместимые с Redis.</span><span class="sxs-lookup"><span data-stu-id="d4561-131">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB file(s).</span></span> <span data-ttu-id="d4561-132">Эту функцию можно использовать для перемещения данных из одного экземпляра кэша Redis для Azure в другой или на другой сервер Redis.</span><span class="sxs-lookup"><span data-stu-id="d4561-132">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="d4561-133">Во время экспорта на виртуальной машине, где размещается экземпляр сервера кэша Redis для Azure, создается временный файл, который отправляется в заданную учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="d4561-133">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="d4561-134">После успешного или неудачного завершения операции экспорта этот временный файл удаляется.</span><span class="sxs-lookup"><span data-stu-id="d4561-134">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

1. <span data-ttu-id="d4561-135">Чтобы экспортировать текущее содержимое кэша в хранилище, [перейдите к кэшу](cache-configure.md#configure-redis-cache-settings) на портале Azure и нажмите кнопку **Экспорт данных** в **меню ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="d4561-135">To export the current contents of the cache to storage, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Export data** from the **Resource menu**.</span></span>

    ![Выберите контейнер хранилища][cache-export-data-choose-storage-container]
2. <span data-ttu-id="d4561-137">Щелкните **Выберите контейнер хранилища** и выберите требуемую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="d4561-137">Click **Choose Storage Container** and select the desired storage account.</span></span> <span data-ttu-id="d4561-138">Эта учетная запись хранения должна относиться к той же подписке и тому же региону, что ваш кэш.</span><span class="sxs-lookup"><span data-stu-id="d4561-138">The storage account must be in the same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d4561-139">Функция экспорта работает со страничными BLOB-объектами, которые поддерживаются как классическими учетными записями хранения, так и учетными записями хранения Resource Manager, но пока не поддерживаются [учетными записями хранения BLOB-объектов](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="d4561-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![Учетная запись хранения][cache-export-data-choose-account]
3. <span data-ttu-id="d4561-141">Выберите нужный контейнер BLOB-объектов и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d4561-141">Choose the desired blob container and click **Select**.</span></span> <span data-ttu-id="d4561-142">Чтобы использовать новый контейнер, щелкните **Добавить контейнер** и выберите его из списка.</span><span class="sxs-lookup"><span data-stu-id="d4561-142">To use new a container, click **Add Container** to add it first and then select it from the list.</span></span>

    ![Выберите контейнер хранилища][cache-export-data-container]
4. <span data-ttu-id="d4561-144">Введите значение **Префикс имени BLOB-объекта** и нажмите кнопку **Экспорт** для запуска процедуры экспорта.</span><span class="sxs-lookup"><span data-stu-id="d4561-144">Type a **Blob name prefix** and click **Export** to start the export process.</span></span> <span data-ttu-id="d4561-145">Префикс имени BLOB-объекта добавляется к именам файлов, создаваемых этой операцией экспорта.</span><span class="sxs-lookup"><span data-stu-id="d4561-145">The blob name prefix is used to prefix the names of files generated by this export operation.</span></span>

    ![экспорт.][cache-export-data]

    <span data-ttu-id="d4561-147">Ход выполнения операции экспорта можно отслеживать, выбирая уведомления на портале Azure или просматривая события в [журнале аудита](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="d4561-147">You can monitor the progress of the export operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Экспорт данных завершен][cache-export-data-export-complete]

    <span data-ttu-id="d4561-149">Во время экспорта кэши остаются доступными для использования.</span><span class="sxs-lookup"><span data-stu-id="d4561-149">Caches remain available for use during the export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="d4561-150">Часто задаваемые вопросы о функции импорта/экспорта</span><span class="sxs-lookup"><span data-stu-id="d4561-150">Import/Export FAQ</span></span>
<span data-ttu-id="d4561-151">Этот раздел содержит часто задаваемые вопросы о функции импорта/экспорта.</span><span class="sxs-lookup"><span data-stu-id="d4561-151">This section contains frequently asked questions about the Import/Export feature.</span></span>

* [<span data-ttu-id="d4561-152">В каких ценовых категориях можно функцию импорта/экспорта?</span><span class="sxs-lookup"><span data-stu-id="d4561-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="d4561-153">Можно ли импортировать данные с любого сервера Redis?</span><span class="sxs-lookup"><span data-stu-id="d4561-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="d4561-154">Какие версии RDB-файлов можно импортировать?</span><span class="sxs-lookup"><span data-stu-id="d4561-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="d4561-155">Доступен ли кэш во время операции импорта или экспорта?</span><span class="sxs-lookup"><span data-stu-id="d4561-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="d4561-156">Можно использовать функцию импорта/экспорта с кластером Redis?</span><span class="sxs-lookup"><span data-stu-id="d4561-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="d4561-157">Как работает импорт и экспорт в базах данных с пользовательскими настройками?</span><span class="sxs-lookup"><span data-stu-id="d4561-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="d4561-158">Чем отличается функция импорта/экспорта от сохраняемости Redis?</span><span class="sxs-lookup"><span data-stu-id="d4561-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="d4561-159">Можно ли автоматизировать функцию импорта/экспорта с помощью PowerShell, интерфейса командной строки или других клиентов управления?</span><span class="sxs-lookup"><span data-stu-id="d4561-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="d4561-160">Возникла ошибка времени ожидания во время операции импорта или экспорта. Что это означает?</span><span class="sxs-lookup"><span data-stu-id="d4561-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="d4561-161">При экспорте данных в хранилище BLOB-объектов Azure возникла ошибка. Что произошло?</span><span class="sxs-lookup"><span data-stu-id="d4561-161">I got an error when exporting my data to Azure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="d4561-162">В каких ценовых категориях можно функцию импорта/экспорта?</span><span class="sxs-lookup"><span data-stu-id="d4561-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="d4561-163">Функция импорта/экспорта доступна только в ценовой категории "Премиум".</span><span class="sxs-lookup"><span data-stu-id="d4561-163">Import/Export is available only in the premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="d4561-164">Можно ли импортировать данные с любого сервера Redis?</span><span class="sxs-lookup"><span data-stu-id="d4561-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="d4561-165">Да, в дополнение к импорту данных, экспортированных из экземпляров кэша Redis для Azure, можно импортировать RDB-файлы с любого сервера Redis, запущенного в любом облаке или любой среде, например в Linux, Windows или у поставщиков облачных решений, таких как Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="d4561-165">Yes, in addition to importing data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="d4561-166">Для этого передайте RDB-файл с нужного сервера Redis в страничный или блочный BLOB-объект в учетной записи хранения Azure, а затем импортируйте его в экземпляр кэша Redis для Azure уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="d4561-166">To do this, upload the RDB file from the desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="d4561-167">Например, вы можете экспортировать данные из рабочего кэша и импортировать их в кэш, используемый в составе промежуточной среды для тестирования или переноса.</span><span class="sxs-lookup"><span data-stu-id="d4561-167">For example, you may want to export the data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4561-168">Для успешного импорта данных, экспортированных с серверов Redis (не являющихся серверами кэша Redis для Azure), при использовании страничного BLOB-объекта его размер должен соответствовать границе в 512 байтов.</span><span class="sxs-lookup"><span data-stu-id="d4561-168">To successfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, the page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="d4561-169">Приме код для заполнения необходимых байтов приведен на странице [SamplePageBlobUpload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span><span class="sxs-lookup"><span data-stu-id="d4561-169">For sample code to perform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="d4561-170">Какие версии RDB-файлов можно импортировать?</span><span class="sxs-lookup"><span data-stu-id="d4561-170">What RDB versions can I import?</span></span>

<span data-ttu-id="d4561-171">Кэш Redis для Azure поддерживает импорт RDB-файлов вплоть до RDB версии 7.</span><span class="sxs-lookup"><span data-stu-id="d4561-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="d4561-172">Доступен ли кэш во время операции импорта или экспорта?</span><span class="sxs-lookup"><span data-stu-id="d4561-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="d4561-173">**Экспорт** — кэши остаются доступными, и во время операции экспорта можно продолжить работу с кэшем.</span><span class="sxs-lookup"><span data-stu-id="d4561-173">**Export** - Caches remain available and you can continue to use your cache during an export operation.</span></span>
* <span data-ttu-id="d4561-174">**Импорт** — кэши становятся недоступными при запуске операции импорта, а по ее завершении вновь становятся доступными для использования.</span><span class="sxs-lookup"><span data-stu-id="d4561-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when the import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="d4561-175">Можно использовать функцию импорта/экспорта с кластером Redis?</span><span class="sxs-lookup"><span data-stu-id="d4561-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="d4561-176">Да, и вы можете выполнять импорт/экспорт между кластеризованным и некластеризованный кэшами.</span><span class="sxs-lookup"><span data-stu-id="d4561-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="d4561-177">Так как кластер Redis [поддерживает только базу данных 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), данные в базах данных, отличных от 0, не импортируются.</span><span class="sxs-lookup"><span data-stu-id="d4561-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="d4561-178">При импорте данных кластеризованного кэша ключи перераспределяются между сегментами кластера.</span><span class="sxs-lookup"><span data-stu-id="d4561-178">When clustered cache data is imported, the keys are redistributed among the shards of the cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="d4561-179">Как работает импорт и экспорт в базах данных с пользовательскими настройками?</span><span class="sxs-lookup"><span data-stu-id="d4561-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="d4561-180">Некоторые ценовые категории имеют различные [ограничения для количества баз данных](cache-configure.md#databases), поэтому существуют определенные рекомендации по импорту, актуальные, если вы задали пользовательское значение для параметра `databases` во время создания кэша.</span><span class="sxs-lookup"><span data-stu-id="d4561-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="d4561-181">При импорте в ценовую категорию с более низким ограничением для параметра `databases` , чем у категории, из которой выполняется импорт:</span><span class="sxs-lookup"><span data-stu-id="d4561-181">When importing to a pricing tier with a lower `databases` limit than the tier from which you exported:</span></span>
  * <span data-ttu-id="d4561-182">Если вы используете заданное по умолчанию количество `databases` (16 для всех ценовых категорий), то данные не теряются.</span><span class="sxs-lookup"><span data-stu-id="d4561-182">If you are using the default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="d4561-183">Если вы используете настраиваемое количество `databases` , находящееся в пределах категории, в которую выполняется импорт, данные не теряются.</span><span class="sxs-lookup"><span data-stu-id="d4561-183">If you are using a custom number of `databases` that falls within the limits for the tier to which you are importing, no data is lost.</span></span>
  * <span data-ttu-id="d4561-184">Если экспортируемые данные включают в себя данные из баз данных, которые являются превышением ограничения для новой категории, данные из таких баз данных не импортируются.</span><span class="sxs-lookup"><span data-stu-id="d4561-184">If your exported data contained data in a database that exceeds the limits of the new tier, the data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="d4561-185">Чем отличается функция импорта/экспорта от сохраняемости Redis?</span><span class="sxs-lookup"><span data-stu-id="d4561-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="d4561-186">Сохраняемость кэша Redis для Azure обеспечивает целостность данных в кэше Redis посредством службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d4561-186">Azure Redis Cache persistence allows you to persist data stored in Redis to Azure Storage.</span></span> <span data-ttu-id="d4561-187">Если настроено постоянное хранение, кэш Redis для Azure будет сохранять моментальный снимок кэша Redis на диске в двоичном формате Redis в соответствии с настроенной частотой резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="d4561-187">When persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span></span> <span data-ttu-id="d4561-188">В случае аварии, при которой становятся недоступными как основной экземпляр кэша, так и реплика кэша, данные кэша восстанавливаются автоматически из последнего моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="d4561-188">If a catastrophic event occurs that disables both the primary and replica cache, the cache data is restored automatically using the most recent snapshot.</span></span> <span data-ttu-id="d4561-189">Дополнительные сведения см. в статье [Настройка постоянного хранения для кэша Redis для Azure уровня Премиум](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="d4561-189">For more information, see [How to configure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="d4561-190">Функция импорта/экспорта позволяет перенести данные в кэш Redis для Azure или экспортировать их оттуда.</span><span class="sxs-lookup"><span data-stu-id="d4561-190">Import/ Export allows you to bring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="d4561-191">Она не осуществляет настройку резервного копирования использует для восстановления механизм сохраняемости Redis.</span><span class="sxs-lookup"><span data-stu-id="d4561-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="d4561-192">Можно ли автоматизировать функцию импорта/экспорта с помощью PowerShell, интерфейса командной строки или других клиентов управления?</span><span class="sxs-lookup"><span data-stu-id="d4561-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="d4561-193">Да, инструкции по использованию PowerShell см. в разделах, посвященных [импорту](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) и [экспорту](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache) кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="d4561-193">Yes, for PowerShell instructions see [To import a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [To export a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="d4561-194">Во время операции импорта/экспорта возникла ошибка времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="d4561-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="d4561-195">Что это означает?</span><span class="sxs-lookup"><span data-stu-id="d4561-195">What does it mean?</span></span>
<span data-ttu-id="d4561-196">Если перед запуском операции вы находитесь в колонке **Импорт данных** или **Экспорт данных** дольше 15 минут, то появится сообщение об ошибке следующего вида:</span><span class="sxs-lookup"><span data-stu-id="d4561-196">If you remain on the **Import data** or **Export data** blade for longer than 15 minutes before initiating the operation, you receive an error with an error message similar to the following example:</span></span>

    The request to import data into cache 'contoso55' failed with status 'error' and error 'One of the SAS URIs provided could not be used for the following reason: The SAS token end time (se) must be at least 1 hour from now and the start time (st), if given, must be at least 15 minutes in the past.

<span data-ttu-id="d4561-197">Чтобы устранить эту проблему, запустите операцию импорта или экспорта до истечения 15 минут.</span><span class="sxs-lookup"><span data-stu-id="d4561-197">To resolve this, initiate the import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened"></a><span data-ttu-id="d4561-198">При экспорте данных в хранилище BLOB-объектов возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="d4561-198">I got an error when exporting my data to Azure Blob Storage.</span></span> <span data-ttu-id="d4561-199">Что произошло?</span><span class="sxs-lookup"><span data-stu-id="d4561-199">What happened?</span></span>
<span data-ttu-id="d4561-200">Функция экспорта работает только с RDB-файлами, сохраненными в виде страничных BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d4561-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="d4561-201">Другие типы больших двоичных объектов пока не поддерживаются, включая учетные записи хранилища BLOB-объектов с "горячим" и "холодным" уровнями.</span><span class="sxs-lookup"><span data-stu-id="d4561-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="d4561-202">Дополнительные сведения см. в разделе [Учетные записи хранения BLOB-объектов](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="d4561-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4561-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4561-203">Next steps</span></span>
<span data-ttu-id="d4561-204">Узнайте, как использовать расширенные функции кэша.</span><span class="sxs-lookup"><span data-stu-id="d4561-204">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="d4561-205">Знакомство с кэшем Redis для Azure уровня Премиум</span><span class="sxs-lookup"><span data-stu-id="d4561-205">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
