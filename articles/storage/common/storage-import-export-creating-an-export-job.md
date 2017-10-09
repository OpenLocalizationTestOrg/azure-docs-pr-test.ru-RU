---
title: "aaaCreate Экспорт заданий импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как toocreate Экспорт задания для hello службы импорта и экспорта Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="3dc73-103">Создание задания экспорта для hello службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="3dc73-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="3dc73-104">Создание задания экспорта службы импорта и экспорта Microsoft Azure hello, с использованием hello REST API включает hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="3dc73-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="3dc73-105">При выборе hello tooexport больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="3dc73-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="3dc73-106">получение адреса для отправки;</span><span class="sxs-lookup"><span data-stu-id="3dc73-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="3dc73-107">Создание задания экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-107">Creating hello export job.</span></span>

-   <span data-ttu-id="3dc73-108">Доставка вашей tooMicrosoft пустые диски через перевозчика.</span><span class="sxs-lookup"><span data-stu-id="3dc73-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="3dc73-109">Обновление задания экспорта hello с hello данных пакета.</span><span class="sxs-lookup"><span data-stu-id="3dc73-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="3dc73-110">Получение hello дисков от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3dc73-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="3dc73-111">В разделе [tooBlob hello импорта и экспорта Windows Azure службы tooTransfer данные хранилища с помощью](storage-import-export-service.md) Обзор службы импорта и экспорта hello и учебник, в котором показано, как toouse hello [портал Azure](https://portal.azure.com/) toocreate и управления импортом и экспортом заданий.</span><span class="sxs-lookup"><span data-stu-id="3dc73-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="3dc73-112">При выборе tooexport больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="3dc73-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="3dc73-113">toocreate задание экспорта, необходимо будет tooprovide список больших двоичных объектов, что нужно tooexport из вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="3dc73-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="3dc73-114">Существует несколько способов tooselect toobe экспортировать большие двоичные объекты:</span><span class="sxs-lookup"><span data-stu-id="3dc73-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="3dc73-115">Tooselect относительного пути можно использовать один большой двоичный объект и все ее моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="3dc73-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="3dc73-116">Можно использовать один BLOB-объект без его мгновенных снимков tooselect относительного пути.</span><span class="sxs-lookup"><span data-stu-id="3dc73-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="3dc73-117">Можно использовать путь относительный больших двоичных объектов и tooselect времени моментальных снимков одного моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="3dc73-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="3dc73-118">Все большие двоичные объекты и моментальные снимки можно использовать tooselect префикс BLOB-объекта с префиксом hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="3dc73-119">Можно экспортировать все большие двоичные объекты и моментальные снимки в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="3dc73-120">Дополнительные сведения об указании больших двоичных объектов tooexport, см. в разделе hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операции.</span><span class="sxs-lookup"><span data-stu-id="3dc73-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="3dc73-121">Получение расположения для отправки</span><span class="sxs-lookup"><span data-stu-id="3dc73-121">Obtaining your shipping location</span></span>
<span data-ttu-id="3dc73-122">Перед созданием задания экспорта, необходимо tooobtain название организации и адрес, вызывающий hello [получить расположение](https://portal.azure.com) или [перечисление расположений](/rest/api/storageimportexport/listlocations) операции.</span><span class="sxs-lookup"><span data-stu-id="3dc73-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="3dc73-123">Операция `List Locations` вернет список расположений и почтовых адресов.</span><span class="sxs-lookup"><span data-stu-id="3dc73-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="3dc73-124">Можно выбрать расположение из hello вернул список и отправить свой адрес toothat жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="3dc73-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="3dc73-125">Можно также использовать hello `Get Location` адрес в определенное место доставки непосредственно hello tooobtain операции.</span><span class="sxs-lookup"><span data-stu-id="3dc73-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="3dc73-126">Выполните действия hello ниже расположение доставки tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="3dc73-127">Определите имя hello hello расположение учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="3dc73-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="3dc73-128">Это значение можно найти в разделе hello **расположение** на учетную запись хранения hello **мониторинга** в классическом hello портала или запросить с помощью hello службы управления API-операции [получить Свойства учетной записи хранения](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="3dc73-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="3dc73-129">Получить расположение hello, которые доступны tooprocess этой учетной записи хранения, вызывающему Привет `Get Location` операции.</span><span class="sxs-lookup"><span data-stu-id="3dc73-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="3dc73-130">Если hello `AlternateLocations` свойство расположения hello содержит зоной hello, то это хорошо toouse это расположение.</span><span class="sxs-lookup"><span data-stu-id="3dc73-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="3dc73-131">В противном случае вызов hello `Get Location` операцию, указав одно из альтернативных расположений hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="3dc73-132">исходное расположение Hello временно закрыт для обслуживания.</span><span class="sxs-lookup"><span data-stu-id="3dc73-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="3dc73-133">Создание задания экспорта hello</span><span class="sxs-lookup"><span data-stu-id="3dc73-133">Creating hello export job</span></span>
 <span data-ttu-id="3dc73-134">задания экспорта toocreate hello hello вызовов [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операции.</span><span class="sxs-lookup"><span data-stu-id="3dc73-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="3dc73-135">Вам потребуется hello tooprovide следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="3dc73-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="3dc73-136">Имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-136">A name for hello job.</span></span>

-   <span data-ttu-id="3dc73-137">Имя учетной записи хранения Hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-137">hello storage account name.</span></span>

-   <span data-ttu-id="3dc73-138">Здравствуйте, название организации, полученное на предыдущем шаге hello доставки.</span><span class="sxs-lookup"><span data-stu-id="3dc73-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="3dc73-139">тип задания (экспорт);</span><span class="sxs-lookup"><span data-stu-id="3dc73-139">A job type (Export).</span></span>

-   <span data-ttu-id="3dc73-140">Hello обратный адрес, где hello диски будут отправлены после завершения задания экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="3dc73-141">экспортировать список больших двоичных объектов (или префиксов больших двоичных объектов) toobe Hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="3dc73-142">Отправка дисков</span><span class="sxs-lookup"><span data-stu-id="3dc73-142">Shipping your drives</span></span>
 <span data-ttu-id="3dc73-143">Далее используйте hello средство импорта и экспорта Azure toodetermine hello количество дисков требуется toosend, в зависимости от hello больших двоичных объектов, выбранных toobe экспортированы и hello размер диска.</span><span class="sxs-lookup"><span data-stu-id="3dc73-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="3dc73-144">В разделе hello [Справочник средство импорта и экспорта Azure](storage-import-export-tool-how-to-v1.md) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="3dc73-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="3dc73-145">Пакет hello диски в один пакет и их отправке toohello адресу, полученному hello выше шаг.</span><span class="sxs-lookup"><span data-stu-id="3dc73-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="3dc73-146">Обратите внимание, номер пакета для следующего шага hello отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="3dc73-147">Диски необходимо отправить через поддерживаемого перевозчика, который предоставит номер для отслеживания посылки.</span><span class="sxs-lookup"><span data-stu-id="3dc73-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="3dc73-148">Обновление задания экспорта hello с указанием данных пакета</span><span class="sxs-lookup"><span data-stu-id="3dc73-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="3dc73-149">После того как вы номер для отслеживания, вызовите hello [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) tooupdated hello перевозчика имя операции и номер для hello задания отслеживания.</span><span class="sxs-lookup"><span data-stu-id="3dc73-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="3dc73-150">При необходимости можно указать количество дисков, обратный адрес hello и дата отгрузки hello также hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="3dc73-151">Получение пакета hello</span><span class="sxs-lookup"><span data-stu-id="3dc73-151">Receiving hello package</span></span>
 <span data-ttu-id="3dc73-152">После обработки задания экспорта ваши диски будут возвращены tooyou с вашими зашифрованными данными.</span><span class="sxs-lookup"><span data-stu-id="3dc73-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="3dc73-153">Можно извлечь ключ BitLocker hello для каждого из устройств hello, вызывающему Привет [получения задания](/rest/api/storageimportexport/jobs#Jobs_Get) операции.</span><span class="sxs-lookup"><span data-stu-id="3dc73-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="3dc73-154">Затем можно разблокировать диск hello, с помощью ключа hello.</span><span class="sxs-lookup"><span data-stu-id="3dc73-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="3dc73-155">файл манифеста диска Hello на каждом диске содержит hello список файлов на диске hello, а также исходный адрес большого двоичного объекта hello для каждого файла.</span><span class="sxs-lookup"><span data-stu-id="3dc73-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dc73-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3dc73-156">Next steps</span></span>

* [<span data-ttu-id="3dc73-157">С помощью REST API службы импорта и экспорта hello</span><span class="sxs-lookup"><span data-stu-id="3dc73-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
