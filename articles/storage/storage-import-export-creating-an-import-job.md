---
title: "aaaCreate задание импорта для импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как toocreate импортировать hello службы импорта и экспорта Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="b723a-103">Создание задания импорта для hello службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="b723a-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="b723a-104">Создание задания импорта службы импорта и экспорта Microsoft Azure hello, с использованием hello REST API включает hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="b723a-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="b723a-105">Подготовка дисков с hello средство импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="b723a-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="b723a-106">Получение hello расположение toowhich tooship hello диска.</span><span class="sxs-lookup"><span data-stu-id="b723a-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="b723a-107">Создание задания импорта hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-107">Creating hello import job.</span></span>

-   <span data-ttu-id="b723a-108">Доставка hello дисков tooMicrosoft через перевозчика.</span><span class="sxs-lookup"><span data-stu-id="b723a-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="b723a-109">Обновление задания импорта hello с hello доставки сведений.</span><span class="sxs-lookup"><span data-stu-id="b723a-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="b723a-110">В разделе [tooBlob hello импорта и экспорта Microsoft Azure службы tooTransfer данные хранилища с помощью](storage-import-export-service.md) Обзор службы импорта и экспорта hello и учебник, в котором показано, как toouse hello [портал Azure](https://portal.azure.com/) toocreate и управления импортом и экспортом заданий.</span><span class="sxs-lookup"><span data-stu-id="b723a-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="b723a-111">Подготовка дисков с hello средство импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="b723a-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="b723a-112">Hello действия tooprepare дисков для задания импорта hello же того, необходимо создать портал hello jobvia hello или через hello REST API.</span><span class="sxs-lookup"><span data-stu-id="b723a-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="b723a-113">Ниже вкратце описана процедура подготовки диска.</span><span class="sxs-lookup"><span data-stu-id="b723a-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="b723a-114">См. toohello [Справочник ExportTool импорта Azure](storage-import-export-tool-how-to-v1.md) Полные инструкции по установке.</span><span class="sxs-lookup"><span data-stu-id="b723a-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="b723a-115">Вы можете загрузить средство импорта и экспорта Azure hello [здесь](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="b723a-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="b723a-116">Подготовка дисков включает следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b723a-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="b723a-117">Идентификационные данные toobe hello импортированы.</span><span class="sxs-lookup"><span data-stu-id="b723a-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="b723a-118">Определение hello целевых больших двоичных объектов в хранилище Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="b723a-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="b723a-119">С помощью средства импорта и экспорта Azure toocopy hello вашей tooone данных или несколько жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="b723a-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="b723a-120">Hello средство импорта и экспорта Azure также создаст файл манифеста для каждого из устройств hello при его подготовке.</span><span class="sxs-lookup"><span data-stu-id="b723a-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="b723a-121">Этот файл манифеста содержит:</span><span class="sxs-lookup"><span data-stu-id="b723a-121">A manifest file contains:</span></span>

-   <span data-ttu-id="b723a-122">Перечисление всех hello файлы, предназначенные для отправки и сопоставления hello tooblobs эти файлы.</span><span class="sxs-lookup"><span data-stu-id="b723a-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="b723a-123">Контрольные суммы сегментов каждого файла hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="b723a-124">Сведения о hello метаданных и свойств tooassociate каждого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="b723a-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="b723a-125">Список tootake действие hello если большой двоичный объект, передаваемая имеет hello одинаковые имена, как существующий большой двоичный объект в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="b723a-126">Возможные параметры: a) перезапись большого двоичного объекта hello с файлом hello, б) сохранение hello существующий большой двоичный объект и пропустить при передаче файла hello, c), добавьте имя toohello суффикса не конфликтует с другими файлами.</span><span class="sxs-lookup"><span data-stu-id="b723a-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="b723a-127">Получение расположения для отправки</span><span class="sxs-lookup"><span data-stu-id="b723a-127">Obtaining your shipping location</span></span>

<span data-ttu-id="b723a-128">Перед созданием задания импорта, необходимо tooobtain название организации и адрес, вызывающий hello [перечисление расположений](/rest/api/storageimportexport/listlocations) операции.</span><span class="sxs-lookup"><span data-stu-id="b723a-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="b723a-129">Операция `List Locations` вернет список расположений и почтовых адресов.</span><span class="sxs-lookup"><span data-stu-id="b723a-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="b723a-130">Можно выбрать расположение из hello вернул список и отправить свой адрес toothat жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="b723a-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="b723a-131">Можно также использовать hello `Get Location` адрес в определенное место доставки непосредственно hello tooobtain операции.</span><span class="sxs-lookup"><span data-stu-id="b723a-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="b723a-132">Выполните действия hello ниже расположение доставки tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="b723a-133">Определите имя hello hello расположение учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="b723a-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="b723a-134">Это значение можно найти в разделе hello **расположение** на учетную запись хранения hello **мониторинга** в hello портал Azure или запросить с помощью hello службы управления API-операции [получения хранилища Свойства учетной записи](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="b723a-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="b723a-135">Получить расположение hello, доступных tooprocess этой учетной записи хранения, вызывающему Привет `Get Location` операции.</span><span class="sxs-lookup"><span data-stu-id="b723a-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="b723a-136">Если hello `AlternateLocations` свойство расположения hello содержит зоной hello, то это хорошо toouse это расположение.</span><span class="sxs-lookup"><span data-stu-id="b723a-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="b723a-137">В противном случае вызов hello `Get Location` операцию, указав одно из альтернативных расположений hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="b723a-138">исходное расположение Hello временно закрыт для обслуживания.</span><span class="sxs-lookup"><span data-stu-id="b723a-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="b723a-139">Создание задания импорта hello</span><span class="sxs-lookup"><span data-stu-id="b723a-139">Creating hello import job</span></span>
<span data-ttu-id="b723a-140">Задание импорта hello toocreate, вызов hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операции.</span><span class="sxs-lookup"><span data-stu-id="b723a-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="b723a-141">Вам потребуется hello tooprovide следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="b723a-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="b723a-142">Имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-142">A name for hello job.</span></span>

-   <span data-ttu-id="b723a-143">Имя учетной записи хранения Hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-143">hello storage account name.</span></span>

-   <span data-ttu-id="b723a-144">Здравствуйте, название организации, полученное из предыдущего шага hello доставки.</span><span class="sxs-lookup"><span data-stu-id="b723a-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="b723a-145">тип задания (импорт);</span><span class="sxs-lookup"><span data-stu-id="b723a-145">A job type (Import).</span></span>

-   <span data-ttu-id="b723a-146">Hello обратный адрес, где hello диски будут отправлены после завершения задания импорта hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="b723a-147">Список дисков в задании hello Hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-147">hello list of drives in hello job.</span></span> <span data-ttu-id="b723a-148">Для каждого диска необходимо включить следующую информацию, что был получен во время подготовки диска hello hello:</span><span class="sxs-lookup"><span data-stu-id="b723a-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="b723a-149">Идентификатор диска Hello</span><span class="sxs-lookup"><span data-stu-id="b723a-149">hello drive Id</span></span>

    -   <span data-ttu-id="b723a-150">ключ BitLocker Hello</span><span class="sxs-lookup"><span data-stu-id="b723a-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="b723a-151">относительный путь файла манифеста Hello на жестком диске hello</span><span class="sxs-lookup"><span data-stu-id="b723a-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="b723a-152">Хэш MD5 файла манифеста в кодировке Base16 Hello</span><span class="sxs-lookup"><span data-stu-id="b723a-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="b723a-153">Отправка дисков</span><span class="sxs-lookup"><span data-stu-id="b723a-153">Shipping your drives</span></span>
<span data-ttu-id="b723a-154">Необходимо отправить свой адрес toohello дисков, полученное из предыдущего шага hello, и вы должны предоставить hello службы импорта и экспорта с hello отслеживания номер пакета hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="b723a-155">Диски необходимо отправить через поддерживаемого перевозчика, который предоставит номер для отслеживания посылки.</span><span class="sxs-lookup"><span data-stu-id="b723a-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="b723a-156">Обновление задания импорта hello с данных о доставке</span><span class="sxs-lookup"><span data-stu-id="b723a-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="b723a-157">После того как вы номер для отслеживания, вызовите hello [обновления свойств задания](/api/storageimportexport/jobs#Jobs_Update) имя оператора, hello идентификационный номер задания hello и hello номер счета перевозчика для возврата доставки доставки hello tooupdate операции.</span><span class="sxs-lookup"><span data-stu-id="b723a-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="b723a-158">Кроме того, можно дополнительно указать номер hello дисков, а также дата отгрузки hello.</span><span class="sxs-lookup"><span data-stu-id="b723a-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b723a-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b723a-159">Next steps</span></span>

* [<span data-ttu-id="b723a-160">С помощью REST API службы импорта и экспорта hello</span><span class="sxs-lookup"><span data-stu-id="b723a-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
