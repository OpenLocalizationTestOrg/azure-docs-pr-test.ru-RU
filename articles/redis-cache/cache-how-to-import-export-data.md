---
title: "aaaImport и экспорт данных в кэше Redis для Azure | Документы Microsoft"
description: "Узнайте, как tooimport и экспорт данных tooand из хранилища больших двоичных объектов с экземплярами кэша Redis для Azure premium"
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
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="515ef-103">Импорт и экспорт данных в кэше Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="515ef-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="515ef-104">Импорт и экспорт является операцией управления данных кэша Redis для Azure, позволяющий tooimport данных в кэше Redis для Azure или экспорта данных из кэша Redis для Azure, Импорт и экспорт моментального снимка Redis кэша базы данных (RDB) из большого двоичного объекта tooa premium кэша в Azure Учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="515ef-104">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="515ef-105">**Экспорт** -можно экспортировать вашей tooa моментальные снимки RDB кэша Redis Azure страничного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="515ef-105">**Export** - you can export your Azure Redis Cache RDB snapshots tooa Page Blob.</span></span>
- <span data-ttu-id="515ef-106">**Импорт**. Моментальные снимки в формате RDB можно импортировать в кэш Redis для Azure из страничного или блочного BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="515ef-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="515ef-107">Импорт и экспорт позволяет toomigrate между различными экземплярами кэша Redis для Azure или заполнения кэша hello с данными, перед использованием.</span><span class="sxs-lookup"><span data-stu-id="515ef-107">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="515ef-108">В этой статье содержатся сведения для импорта и экспорта данных с помощью кэша Redis для Azure и предоставляет ответы на hello toocommonly вопросы и ответы.</span><span class="sxs-lookup"><span data-stu-id="515ef-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides hello answers toocommonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="515ef-109">Функция импорта/экспорта находится на этапе предварительной версии и доступна только для кэшей [категории "Премиум"](cache-premium-tier-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="515ef-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="515ef-110">Импорт</span><span class="sxs-lookup"><span data-stu-id="515ef-110">Import</span></span>
<span data-ttu-id="515ef-111">Импорт может быть используется toobring Redis совместимые RDB файлы с любого сервера Redis под управлением какой-либо облаке или в среде, включая Redis под управлением Linux, Windows или любого поставщика облачных служб, таких как Amazon Web Services и другие.</span><span class="sxs-lookup"><span data-stu-id="515ef-111">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="515ef-112">Импорт данных — простой способ toocreate кэша заполнены данными.</span><span class="sxs-lookup"><span data-stu-id="515ef-112">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="515ef-113">Во время процесса импорта hello кэша Redis для Azure hello RDB файлы загружаются из хранилища Azure в память и вставляет hello ключи в кэш hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-113">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory and then inserts hello keys into hello cache.</span></span>

> [!NOTE]
> <span data-ttu-id="515ef-114">Перед началом операции импорта hello, убедитесь, что файл базы данных Redis (RDB) или файлы загружаются в страницу или блочных BLOB-объектов в хранилище Azure, в hello же регионе и подписке, что экземпляр кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="515ef-114">Before beginning hello import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in hello same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="515ef-115">Дополнительные сведения см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="515ef-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="515ef-116">При экспорте файла с помощью hello RDB [Azure Redis кэша Export](#export) функция, файл RDB уже хранится в страничный большой двоичный объект и готов к импорту.</span><span class="sxs-lookup"><span data-stu-id="515ef-116">If you exported your RDB file using hello [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="515ef-117">tooimport один или несколько экспорта больших двоичных объектов кэша, [Обзор кэша tooyour](cache-configure.md#configure-redis-cache-settings) в hello портал Azure и нажмите кнопку **импорта данных** из hello **ресурсов меню**.</span><span class="sxs-lookup"><span data-stu-id="515ef-117">tooimport one or more exported cache blobs, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Import data** from hello **Resource menu**.</span></span>

    ![Импорт данных][cache-import-data]
2. <span data-ttu-id="515ef-119">Нажмите кнопку **выберите копий** и выберите учетную запись хранения hello, содержащий данные tooimport hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-119">Click **Choose Blob(s)** and select hello storage account that contains hello data tooimport.</span></span>

    ![Выбор учетной записи хранения][cache-import-choose-storage-account]
3. <span data-ttu-id="515ef-121">Щелкните контейнер hello, содержащий данные tooimport hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-121">Click hello container that contains hello data tooimport.</span></span>

    ![Выберите контейнер][cache-import-choose-container]
4. <span data-ttu-id="515ef-123">Выберите один или несколько tooimport большие двоичные объекты, нажав кнопку hello область toohello слева от имени большого двоичного объекта hello и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="515ef-123">Select one or more blobs tooimport by clicking hello area toohello left of hello blob name, and then click **Select**.</span></span>

    ![Выберите BLOB-объекты][cache-import-choose-blobs]
5. <span data-ttu-id="515ef-125">Нажмите кнопку **импорта** процесс импорта toobegin hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-125">Click **Import** toobegin hello import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="515ef-126">кэш Hello не доступны для клиентов кэша во время процесса импорта hello и удалить все существующие данные в кэше hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-126">hello cache is not accessible by cache clients during hello import process, and any existing data in hello cache is deleted.</span></span>
   >
   >

    ![Импорт][cache-import-blobs]

    <span data-ttu-id="515ef-128">Следующие уведомления hello из hello портал Azure, или просмотрев события hello в hello можно отслеживать ход выполнения операции импорта hello hello [журнал аудита](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="515ef-128">You can monitor hello progress of hello import operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Ход выполнения импорта][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="515ef-130">экспорт.</span><span class="sxs-lookup"><span data-stu-id="515ef-130">Export</span></span>
<span data-ttu-id="515ef-131">Экспорт позволяет tooexport hello данные, хранящиеся в кэш Azure Redis tooRedis совместимый RDB файлов.</span><span class="sxs-lookup"><span data-stu-id="515ef-131">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB file(s).</span></span> <span data-ttu-id="515ef-132">Можно использовать данные toomove этого компонента из одной tooanother экземпляр кэша Redis для Azure или tooanother сервера Redis.</span><span class="sxs-lookup"><span data-stu-id="515ef-132">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="515ef-133">Во время процесса экспорта hello временный файл создается на hello виртуальной Машины, что узлы hello экземпляр сервера кэша Redis для Azure, а hello файл отправленного toohello, назначенные учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="515ef-133">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="515ef-134">После завершения операции экспорта hello состояние успеха или сбоя hello временный файл удаляется.</span><span class="sxs-lookup"><span data-stu-id="515ef-134">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

1. <span data-ttu-id="515ef-135">tooexport hello текущее содержимое toostorage кэша hello, [Обзор кэша tooyour](cache-configure.md#configure-redis-cache-settings) в hello портал Azure и нажмите кнопку **экспортировать данные** из hello **ресурсов меню**.</span><span class="sxs-lookup"><span data-stu-id="515ef-135">tooexport hello current contents of hello cache toostorage, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Export data** from hello **Resource menu**.</span></span>

    ![Выберите контейнер хранилища][cache-export-data-choose-storage-container]
2. <span data-ttu-id="515ef-137">Нажмите кнопку **выберите контейнер хранилища** и выберите учетную запись хранения требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-137">Click **Choose Storage Container** and select hello desired storage account.</span></span> <span data-ttu-id="515ef-138">Учетная запись хранения Hello должна быть в hello одной подписке и регионе с кэшем.</span><span class="sxs-lookup"><span data-stu-id="515ef-138">hello storage account must be in hello same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="515ef-139">Функция экспорта работает со страничными BLOB-объектами, которые поддерживаются как классическими учетными записями хранения, так и учетными записями хранения Resource Manager, но пока не поддерживаются [учетными записями хранения BLOB-объектов](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="515ef-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![Учетная запись хранения][cache-export-data-choose-account]
3. <span data-ttu-id="515ef-141">Выберите требуемого hello контейнер больших двоичных объектов и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="515ef-141">Choose hello desired blob container and click **Select**.</span></span> <span data-ttu-id="515ef-142">Щелкните toouse новый контейнер **добавить контейнер** tooadd его первой, а затем выберите его из списка hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-142">toouse new a container, click **Add Container** tooadd it first and then select it from hello list.</span></span>

    ![Выберите контейнер хранилища][cache-export-data-container]
4. <span data-ttu-id="515ef-144">Введите значение **префикс имени большого двоичного объекта** и нажмите кнопку **Экспорт** toostart hello в процессе экспорта.</span><span class="sxs-lookup"><span data-stu-id="515ef-144">Type a **Blob name prefix** and click **Export** toostart hello export process.</span></span> <span data-ttu-id="515ef-145">префикс имени большого двоичного объекта Hello — используется tooprefix hello имена файлов, создаваемых этой операции экспорта.</span><span class="sxs-lookup"><span data-stu-id="515ef-145">hello blob name prefix is used tooprefix hello names of files generated by this export operation.</span></span>

    ![экспорт.][cache-export-data]

    <span data-ttu-id="515ef-147">Следующие уведомления hello из hello портал Azure, или просмотрев события hello в hello отследить ход выполнения hello операции экспорта hello [журнал аудита](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="515ef-147">You can monitor hello progress of hello export operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![Экспорт данных завершен][cache-export-data-export-complete]

    <span data-ttu-id="515ef-149">Кэши остаются доступными для использования в процессе экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-149">Caches remain available for use during hello export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="515ef-150">Часто задаваемые вопросы о функции импорта/экспорта</span><span class="sxs-lookup"><span data-stu-id="515ef-150">Import/Export FAQ</span></span>
<span data-ttu-id="515ef-151">В этом разделе приведены часто задаваемые вопросы о функции импорта и экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-151">This section contains frequently asked questions about hello Import/Export feature.</span></span>

* [<span data-ttu-id="515ef-152">В каких ценовых категориях можно функцию импорта/экспорта?</span><span class="sxs-lookup"><span data-stu-id="515ef-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="515ef-153">Можно ли импортировать данные с любого сервера Redis?</span><span class="sxs-lookup"><span data-stu-id="515ef-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="515ef-154">Какие версии RDB-файлов можно импортировать?</span><span class="sxs-lookup"><span data-stu-id="515ef-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="515ef-155">Доступен ли кэш во время операции импорта или экспорта?</span><span class="sxs-lookup"><span data-stu-id="515ef-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="515ef-156">Можно использовать функцию импорта/экспорта с кластером Redis?</span><span class="sxs-lookup"><span data-stu-id="515ef-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="515ef-157">Как работает импорт и экспорт в базах данных с пользовательскими настройками?</span><span class="sxs-lookup"><span data-stu-id="515ef-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="515ef-158">Чем отличается функция импорта/экспорта от сохраняемости Redis?</span><span class="sxs-lookup"><span data-stu-id="515ef-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="515ef-159">Можно ли автоматизировать функцию импорта/экспорта с помощью PowerShell, интерфейса командной строки или других клиентов управления?</span><span class="sxs-lookup"><span data-stu-id="515ef-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="515ef-160">Возникла ошибка времени ожидания во время операции импорта или экспорта. Что это означает?</span><span class="sxs-lookup"><span data-stu-id="515ef-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="515ef-161">Я получил ошибку при экспорте tooAzure Мои данные хранилища больших двоичных объектов. Что произошло?</span><span class="sxs-lookup"><span data-stu-id="515ef-161">I got an error when exporting my data tooAzure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="515ef-162">В каких ценовых категориях можно функцию импорта/экспорта?</span><span class="sxs-lookup"><span data-stu-id="515ef-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="515ef-163">Импорт и экспорт доступна только в ценовой категории premium hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-163">Import/Export is available only in hello premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="515ef-164">Можно ли импортировать данные с любого сервера Redis?</span><span class="sxs-lookup"><span data-stu-id="515ef-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="515ef-165">Да, кроме tooimporting данных, экспортированных из экземпляров кэша Redis для Azure, можно импортировать файлы RDB с любого сервера Redis под управлением какой-либо облака или среды, например поставщиков облачных служб, таких как Amazon Web Services, Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="515ef-165">Yes, in addition tooimporting data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="515ef-166">toodo это передачи hello RDB файла с сервера Redis требуемого hello в большой двоичный объект страницы или блок в учетной записи хранилища Azure, а затем импорт его в экземпляр кэша Redis для Azure premium.</span><span class="sxs-lookup"><span data-stu-id="515ef-166">toodo this, upload hello RDB file from hello desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="515ef-167">Например вы хотите tooexport hello данные из кэша рабочих и импортировать его в кэш, используемый как часть промежуточной среде для тестирования или миграции.</span><span class="sxs-lookup"><span data-stu-id="515ef-167">For example, you may want tooexport hello data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="515ef-168">toosuccessfully Импорт данных, экспортированных из Redis серверы, отличные от кэша Redis для Azure, когда с помощью страничного большого двоичного объекта, размер большого двоичного объекта страницы приветствия должна быть выровнена по границе 512 байт.</span><span class="sxs-lookup"><span data-stu-id="515ef-168">toosuccessfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, hello page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="515ef-169">Для образца кода tooperform требуемые байтов заполнения см. в разделе [пример страницы блога передачи](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span><span class="sxs-lookup"><span data-stu-id="515ef-169">For sample code tooperform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="515ef-170">Какие версии RDB-файлов можно импортировать?</span><span class="sxs-lookup"><span data-stu-id="515ef-170">What RDB versions can I import?</span></span>

<span data-ttu-id="515ef-171">Кэш Redis для Azure поддерживает импорт RDB-файлов вплоть до RDB версии 7.</span><span class="sxs-lookup"><span data-stu-id="515ef-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="515ef-172">Доступен ли кэш во время операции импорта или экспорта?</span><span class="sxs-lookup"><span data-stu-id="515ef-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="515ef-173">**Экспорт** - кэши остаются доступными и продолжайте toouse кэша во время операции экспорта.</span><span class="sxs-lookup"><span data-stu-id="515ef-173">**Export** - Caches remain available and you can continue toouse your cache during an export operation.</span></span>
* <span data-ttu-id="515ef-174">**Импортировать** - кэши становятся недоступными после запуска операции импорта и станут доступны для использования после завершения операции импорта hello.</span><span class="sxs-lookup"><span data-stu-id="515ef-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when hello import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="515ef-175">Можно использовать функцию импорта/экспорта с кластером Redis?</span><span class="sxs-lookup"><span data-stu-id="515ef-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="515ef-176">Да, и вы можете выполнять импорт/экспорт между кластеризованным и некластеризованный кэшами.</span><span class="sxs-lookup"><span data-stu-id="515ef-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="515ef-177">Так как кластер Redis [поддерживает только базу данных 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), данные в базах данных, отличных от 0, не импортируются.</span><span class="sxs-lookup"><span data-stu-id="515ef-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="515ef-178">При импорте данных кластеризованный кэша, ключи hello перераспределяются между сегментами hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="515ef-178">When clustered cache data is imported, hello keys are redistributed among hello shards of hello cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="515ef-179">Как работает импорт и экспорт в базах данных с пользовательскими настройками?</span><span class="sxs-lookup"><span data-stu-id="515ef-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="515ef-180">Некоторые ценовые категории имеют различные [баз данных ограничения](cache-configure.md#databases), поэтому существуют определенные рекомендации при импорте, если вы настроили пользовательское значение hello `databases` можно задать во время создания кэша.</span><span class="sxs-lookup"><span data-stu-id="515ef-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="515ef-181">При импорте tooa ценовой категории с более низким `databases` предел от уровня hello, из которого был экспортирован:</span><span class="sxs-lookup"><span data-stu-id="515ef-181">When importing tooa pricing tier with a lower `databases` limit than hello tier from which you exported:</span></span>
  * <span data-ttu-id="515ef-182">Если вы используете hello количество по умолчанию `databases`, которая 16 для всех ценовых категорий, данные не теряются.</span><span class="sxs-lookup"><span data-stu-id="515ef-182">If you are using hello default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="515ef-183">Если вы используете настраиваемое число `databases` , попадает в пределы hello для hello уровня toowhich при импорте, никакие данные не потеряны.</span><span class="sxs-lookup"><span data-stu-id="515ef-183">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are importing, no data is lost.</span></span>
  * <span data-ttu-id="515ef-184">Если экспортированных данных содержит данные в базе данных, размер которой превышает ограничения hello hello новый уровень, hello данные из указанных выше баз данных не импортируются.</span><span class="sxs-lookup"><span data-stu-id="515ef-184">If your exported data contained data in a database that exceeds hello limits of hello new tier, hello data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="515ef-185">Чем отличается функция импорта/экспорта от сохраняемости Redis?</span><span class="sxs-lookup"><span data-stu-id="515ef-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="515ef-186">Azure сохраняемости кэша Redis позволяет toopersist данные, хранящиеся в Redis tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="515ef-186">Azure Redis Cache persistence allows you toopersist data stored in Redis tooAzure Storage.</span></span> <span data-ttu-id="515ef-187">При настройке сохраняемости кэша Redis для Azure сохраняет моментальный снимок кэша Redis hello в Redis toodisk двоичный формат, в зависимости от можно настроить интервал резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="515ef-187">When persistence is configured, Azure Redis Cache persists a snapshot of hello Redis cache in a Redis binary format toodisk based on a configurable backup frequency.</span></span> <span data-ttu-id="515ef-188">В случае критического события, отключает hello первичный и реплика кэша hello кэширования данных восстанавливается автоматически с помощью hello самый последний моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="515ef-188">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache data is restored automatically using hello most recent snapshot.</span></span> <span data-ttu-id="515ef-189">Дополнительные сведения см. в разделе [как tooconfigure сохранения данных для кэша Redis Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="515ef-189">For more information, see [How tooconfigure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="515ef-190">Импорт / Экспорт позволяет toobring данных или экспорта из кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="515ef-190">Import/ Export allows you toobring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="515ef-191">Она не осуществляет настройку резервного копирования использует для восстановления механизм сохраняемости Redis.</span><span class="sxs-lookup"><span data-stu-id="515ef-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="515ef-192">Можно ли автоматизировать функцию импорта/экспорта с помощью PowerShell, интерфейса командной строки или других клиентов управления?</span><span class="sxs-lookup"><span data-stu-id="515ef-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="515ef-193">Да, PowerShell инструкции в разделе [tooimport кэш Redis](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) и [tooexport кэш Redis](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="515ef-193">Yes, for PowerShell instructions see [tooimport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [tooexport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="515ef-194">Во время операции импорта/экспорта возникла ошибка времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="515ef-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="515ef-195">Что это означает?</span><span class="sxs-lookup"><span data-stu-id="515ef-195">What does it mean?</span></span>
<span data-ttu-id="515ef-196">Если остались на hello **импорта данных** или **Экспорт данных** колонке более 15 минут перед запуском операции hello появляется сообщение об ошибке с ошибки сообщения аналогичные toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="515ef-196">If you remain on hello **Import data** or **Export data** blade for longer than 15 minutes before initiating hello operation, you receive an error with an error message similar toohello following example:</span></span>

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

<span data-ttu-id="515ef-197">tooresolve по этой операции экспорта или импорта hello инициировать до истечения 15 минут.</span><span class="sxs-lookup"><span data-stu-id="515ef-197">tooresolve this, initiate hello import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a><span data-ttu-id="515ef-198">Я получил ошибку при экспорте tooAzure Мои данные хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="515ef-198">I got an error when exporting my data tooAzure Blob Storage.</span></span> <span data-ttu-id="515ef-199">Что произошло?</span><span class="sxs-lookup"><span data-stu-id="515ef-199">What happened?</span></span>
<span data-ttu-id="515ef-200">Функция экспорта работает только с RDB-файлами, сохраненными в виде страничных BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="515ef-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="515ef-201">Другие типы больших двоичных объектов пока не поддерживаются, включая учетные записи хранилища BLOB-объектов с "горячим" и "холодным" уровнями.</span><span class="sxs-lookup"><span data-stu-id="515ef-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="515ef-202">Дополнительные сведения см. в разделе [Учетные записи хранения BLOB-объектов](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="515ef-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="515ef-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="515ef-203">Next steps</span></span>
<span data-ttu-id="515ef-204">Узнайте, как toouse более "премиум" кэша функции.</span><span class="sxs-lookup"><span data-stu-id="515ef-204">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="515ef-205">Уровень Premium кэша Redis Azure toohello введение</span><span class="sxs-lookup"><span data-stu-id="515ef-205">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

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
