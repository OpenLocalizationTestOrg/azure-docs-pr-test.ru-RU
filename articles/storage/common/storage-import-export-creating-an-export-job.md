---
title: "Создание задания экспорта для импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, как создать задание экспорта для службы импорта и экспорта Microsoft Azure."
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
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="49cda-103">Создание задания экспорта для службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="49cda-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="49cda-104">Создание задания экспорта для службы импорта и экспорта Microsoft Azure с помощью интерфейса REST API включает следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="49cda-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="49cda-105">выбор больших двоичных объектов для экспорта;</span><span class="sxs-lookup"><span data-stu-id="49cda-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="49cda-106">получение адреса для отправки;</span><span class="sxs-lookup"><span data-stu-id="49cda-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="49cda-107">создание задания экспорта;</span><span class="sxs-lookup"><span data-stu-id="49cda-107">Creating the export job.</span></span>

-   <span data-ttu-id="49cda-108">отправка пустых дисков в Майкрософт через поддерживаемого перевозчика;</span><span class="sxs-lookup"><span data-stu-id="49cda-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="49cda-109">обновление задания экспорта с использованием сведений о посылке;</span><span class="sxs-lookup"><span data-stu-id="49cda-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="49cda-110">получение дисков от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="49cda-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="49cda-111">Общие сведения о службе импорта и экспорта, а также руководство по использованию [портала Azure](https://portal.azure.com/) для создания заданий импорта и экспорта и управления ими см. в статье [Использование службы импорта и экспорта Azure для передачи данных в хранилище BLOB-объектов](storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="49cda-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="49cda-112">Выбор больших двоичных объектов для экспорта</span><span class="sxs-lookup"><span data-stu-id="49cda-112">Selecting blobs to export</span></span>
 <span data-ttu-id="49cda-113">Для создания задания экспорта следует указать список больших двоичных объектов, которые необходимо экспортировать из вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="49cda-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="49cda-114">Выбрать большие двоичные объекты для экспорта можно несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="49cda-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="49cda-115">использовать относительный путь к большому двоичному объекту, чтобы выбрать один BLOB-объект и все его моментальные снимки;</span><span class="sxs-lookup"><span data-stu-id="49cda-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="49cda-116">использовать относительный путь к большому двоичному объекту, чтобы выбрать один BLOB-объект без моментальных снимков;</span><span class="sxs-lookup"><span data-stu-id="49cda-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="49cda-117">использовать относительный путь к большому двоичному объекту и время создания моментального снимка, чтобы выбрать один моментальный снимок;</span><span class="sxs-lookup"><span data-stu-id="49cda-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="49cda-118">использовать префикс большого двоичного объекта, чтобы выбрать все BLOB-объекты и моментальные снимки с этим префиксом;</span><span class="sxs-lookup"><span data-stu-id="49cda-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="49cda-119">экспортировать все большие двоичные объекты и моментальные снимки в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="49cda-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="49cda-120">Дополнительные сведения об указании больших двоичных объектов для экспорта см. в разделе об операции [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="49cda-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="49cda-121">Получение расположения для отправки</span><span class="sxs-lookup"><span data-stu-id="49cda-121">Obtaining your shipping location</span></span>
<span data-ttu-id="49cda-122">Перед созданием задания экспорта необходимо получить название и адрес места для отправки, выполнив операцию [Get Location](https://portal.azure.com) или [List Locations](/rest/api/storageimportexport/listlocations).</span><span class="sxs-lookup"><span data-stu-id="49cda-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="49cda-123">Операция `List Locations` вернет список расположений и почтовых адресов.</span><span class="sxs-lookup"><span data-stu-id="49cda-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="49cda-124">В полученном списке выберите расположение и отправьте жесткие диски по соответствующему адресу.</span><span class="sxs-lookup"><span data-stu-id="49cda-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="49cda-125">Также можно использовать операцию `Get Location`, чтобы сразу получить адрес доставки для определенного расположения.</span><span class="sxs-lookup"><span data-stu-id="49cda-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="49cda-126">Выполните следующие действия, чтобы получить адрес доставки.</span><span class="sxs-lookup"><span data-stu-id="49cda-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="49cda-127">Определите имя расположения своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="49cda-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="49cda-128">Оно находится в поле **Расположение** на **панели мониторинга** учетной записи хранения на классическом портале. Это значение также можно получить, отправив запрос с помощью операции API управления службами [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties) (Получить свойства учетной записи хранения).</span><span class="sxs-lookup"><span data-stu-id="49cda-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="49cda-129">Получите расположение, доступное для обработки этой учетной записи хранения, путем вызова операции `Get Location`.</span><span class="sxs-lookup"><span data-stu-id="49cda-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="49cda-130">Расположение можно использовать, если его свойство `AlternateLocations` указывает на это же расположение.</span><span class="sxs-lookup"><span data-stu-id="49cda-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="49cda-131">В противном случае снова вызовите операцию `Get Location` для одного из альтернативных расположений.</span><span class="sxs-lookup"><span data-stu-id="49cda-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="49cda-132">Исходное расположение может быть временно закрыто для обслуживания.</span><span class="sxs-lookup"><span data-stu-id="49cda-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="49cda-133">Создание задания экспорта</span><span class="sxs-lookup"><span data-stu-id="49cda-133">Creating the export job</span></span>
 <span data-ttu-id="49cda-134">Чтобы создать задание экспорта, вызовите операцию [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="49cda-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="49cda-135">Необходимо будет указать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="49cda-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="49cda-136">имя задания;</span><span class="sxs-lookup"><span data-stu-id="49cda-136">A name for the job.</span></span>

-   <span data-ttu-id="49cda-137">имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="49cda-137">The storage account name.</span></span>

-   <span data-ttu-id="49cda-138">название расположения для отправки, полученное на предыдущем шаге;</span><span class="sxs-lookup"><span data-stu-id="49cda-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="49cda-139">тип задания (экспорт);</span><span class="sxs-lookup"><span data-stu-id="49cda-139">A job type (Export).</span></span>

-   <span data-ttu-id="49cda-140">обратный адрес, по которому следует вернуть диски после завершения задания экспорта;</span><span class="sxs-lookup"><span data-stu-id="49cda-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="49cda-141">список больших двоичных объектов (или их префиксов) для экспорта.</span><span class="sxs-lookup"><span data-stu-id="49cda-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="49cda-142">Отправка дисков</span><span class="sxs-lookup"><span data-stu-id="49cda-142">Shipping your drives</span></span>
 <span data-ttu-id="49cda-143">Используйте инструмент импорта и экспорта Azure для определения количества дисков, которые необходимо отправить, в зависимости от выбранных для экспорта больших двоичных объектов и размера диска.</span><span class="sxs-lookup"><span data-stu-id="49cda-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="49cda-144">Дополнительные сведения см. в статье [Использование средства импорта и экспорта Azure версии 1](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="49cda-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="49cda-145">Упакуйте диски в одну посылку и отправьте их по адресу, полученному на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="49cda-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="49cda-146">Запишите номер для отслеживания посылки для следующего шага.</span><span class="sxs-lookup"><span data-stu-id="49cda-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="49cda-147">Диски необходимо отправить через поддерживаемого перевозчика, который предоставит номер для отслеживания посылки.</span><span class="sxs-lookup"><span data-stu-id="49cda-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="49cda-148">Обновление задания экспорта с использованием сведений о посылке</span><span class="sxs-lookup"><span data-stu-id="49cda-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="49cda-149">После получения номера для отслеживания выполните операцию [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) (Обновление свойств задания), чтобы обновить имя перевозчика и номер для отслеживания в задании.</span><span class="sxs-lookup"><span data-stu-id="49cda-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="49cda-150">При необходимости можно также указать количество дисков, обратный адрес и дату отправки.</span><span class="sxs-lookup"><span data-stu-id="49cda-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="49cda-151">Получение посылки</span><span class="sxs-lookup"><span data-stu-id="49cda-151">Receiving the package</span></span>
 <span data-ttu-id="49cda-152">После обработки задания экспорта вы получите диски с зашифрованными данными.</span><span class="sxs-lookup"><span data-stu-id="49cda-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="49cda-153">Чтобы получить ключ BitLocker для каждого диска выполните операцию [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="49cda-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="49cda-154">Затем разблокируйте диск с помощью ключа.</span><span class="sxs-lookup"><span data-stu-id="49cda-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="49cda-155">Файл манифеста диска на каждом диске содержит список файлов на диске, а также исходный адрес большого двоичного объекта для каждого файла.</span><span class="sxs-lookup"><span data-stu-id="49cda-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49cda-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49cda-156">Next steps</span></span>

* [<span data-ttu-id="49cda-157">Использование REST API службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="49cda-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
