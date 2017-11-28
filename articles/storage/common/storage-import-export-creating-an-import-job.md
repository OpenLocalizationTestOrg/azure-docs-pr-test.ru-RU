---
title: "Создание задания импорта для импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, как создать задание импорта для службы импорта и экспорта Microsoft Azure."
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
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="85022-103">Создание задания импорта для службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="85022-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="85022-104">Создание задания импорта для службы импорта и экспорта Microsoft Azure с помощью интерфейса REST API включает следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="85022-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="85022-105">подготовка дисков с помощью инструмента импорта и экспорта Azure;</span><span class="sxs-lookup"><span data-stu-id="85022-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="85022-106">получение адреса для отправки диска;</span><span class="sxs-lookup"><span data-stu-id="85022-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="85022-107">создание задания импорта;</span><span class="sxs-lookup"><span data-stu-id="85022-107">Creating the import job.</span></span>

-   <span data-ttu-id="85022-108">отправка дисков в Майкрософт через поддерживаемого перевозчика;</span><span class="sxs-lookup"><span data-stu-id="85022-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="85022-109">внесение сведений о доставке в задание импорта.</span><span class="sxs-lookup"><span data-stu-id="85022-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="85022-110">Общие сведения о службе импорта и экспорта, а также руководство по использованию [портала Azure](https://portal.azure.com/) для создания заданий импорта и экспорта и управления ими см. в статье [Использование службы импорта и экспорта Azure для передачи данных в хранилище BLOB-объектов](storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="85022-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="85022-111">Подготовка дисков с помощью средства импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="85022-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="85022-112">Действия по подготовке дисков для задания импорта одинаковы независимо от способа создания задания: с помощью портала или REST API.</span><span class="sxs-lookup"><span data-stu-id="85022-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="85022-113">Ниже вкратце описана процедура подготовки диска.</span><span class="sxs-lookup"><span data-stu-id="85022-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="85022-114">Подробные инструкции см. в [справочном руководстве по средству импорта и экспорта Azure](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="85022-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="85022-115">Инструмент импорта и экспорта Azure можно скачать [отсюда](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="85022-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="85022-116">Подготовка дисков включает следующие действия:</span><span class="sxs-lookup"><span data-stu-id="85022-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="85022-117">определение данных, подлежащих импорту;</span><span class="sxs-lookup"><span data-stu-id="85022-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="85022-118">определение целевых больших двоичных объектов в службе хранилища Azure;</span><span class="sxs-lookup"><span data-stu-id="85022-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="85022-119">копирование данных на один или несколько жестких дисков с помощью инструмента импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="85022-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="85022-120">Кроме того, инструмент импорта и экспорта Azure при подготовке дисков создает файл манифеста для каждого диска.</span><span class="sxs-lookup"><span data-stu-id="85022-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="85022-121">Этот файл манифеста содержит:</span><span class="sxs-lookup"><span data-stu-id="85022-121">A manifest file contains:</span></span>

-   <span data-ttu-id="85022-122">перечисление всех файлов, предназначенных для передачи, и сопоставление этих файлов с большими двоичными объектами;</span><span class="sxs-lookup"><span data-stu-id="85022-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="85022-123">контрольные суммы сегментов каждого файла;</span><span class="sxs-lookup"><span data-stu-id="85022-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="85022-124">сведения о метаданных и свойствах для каждого большого двоичного объекта;</span><span class="sxs-lookup"><span data-stu-id="85022-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="85022-125">список действий, которые нужно выполнить при совпадении имен передаваемого большого двоичного объекта и уже существующего в целевом контейнере.</span><span class="sxs-lookup"><span data-stu-id="85022-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="85022-126">Возможные варианты действий: a) перезаписать большой двоичный объект новым файлом; б) сохранить существующий большой двоичный объект и пропустить передачу файла; в) добавить к имени файла суффикс, позволяющий избежать конфликта с другими файлами.</span><span class="sxs-lookup"><span data-stu-id="85022-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="85022-127">Получение расположения для отправки</span><span class="sxs-lookup"><span data-stu-id="85022-127">Obtaining your shipping location</span></span>

<span data-ttu-id="85022-128">Перед созданием задания импорта необходимо получить название и адрес места для отправки, выполнив операцию [вывода списка расположений](/rest/api/storageimportexport/listlocations).</span><span class="sxs-lookup"><span data-stu-id="85022-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="85022-129">Операция `List Locations` вернет список расположений и почтовых адресов.</span><span class="sxs-lookup"><span data-stu-id="85022-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="85022-130">В полученном списке выберите расположение и отправьте жесткие диски по соответствующему адресу.</span><span class="sxs-lookup"><span data-stu-id="85022-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="85022-131">Также можно использовать операцию `Get Location`, чтобы сразу получить адрес доставки для определенного расположения.</span><span class="sxs-lookup"><span data-stu-id="85022-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="85022-132">Выполните следующие действия, чтобы получить адрес доставки.</span><span class="sxs-lookup"><span data-stu-id="85022-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="85022-133">Определите имя расположения своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="85022-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="85022-134">Оно находится в поле **Расположение** на **панели мониторинга** учетной записи хранения на портале Azure. Это значение также можно получить, отправив запрос с помощью операции API управления службами [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties) (Получить свойства учетной записи хранения).</span><span class="sxs-lookup"><span data-stu-id="85022-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="85022-135">Вызовите операцию `Get Location`, чтобы узнать расположение для обработки информации по этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="85022-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="85022-136">Расположение можно использовать, если его свойство `AlternateLocations` указывает на это же расположение.</span><span class="sxs-lookup"><span data-stu-id="85022-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="85022-137">В противном случае снова вызовите операцию `Get Location` для одного из альтернативных расположений.</span><span class="sxs-lookup"><span data-stu-id="85022-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="85022-138">Исходное расположение может быть временно закрыто для обслуживания.</span><span class="sxs-lookup"><span data-stu-id="85022-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="85022-139">Создание задания импорта</span><span class="sxs-lookup"><span data-stu-id="85022-139">Creating the import job</span></span>
<span data-ttu-id="85022-140">Чтобы создать задание импорта, вызовите операцию [создания задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="85022-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="85022-141">Необходимо будет указать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="85022-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="85022-142">имя задания;</span><span class="sxs-lookup"><span data-stu-id="85022-142">A name for the job.</span></span>

-   <span data-ttu-id="85022-143">имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="85022-143">The storage account name.</span></span>

-   <span data-ttu-id="85022-144">название расположения для отправки, полученное на предыдущем шаге;</span><span class="sxs-lookup"><span data-stu-id="85022-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="85022-145">тип задания (импорт);</span><span class="sxs-lookup"><span data-stu-id="85022-145">A job type (Import).</span></span>

-   <span data-ttu-id="85022-146">обратный адрес, на который следует вернуть диски после завершения задания импорта;</span><span class="sxs-lookup"><span data-stu-id="85022-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="85022-147">список дисков в задании.</span><span class="sxs-lookup"><span data-stu-id="85022-147">The list of drives in the job.</span></span> <span data-ttu-id="85022-148">Для каждого диска укажите следующие сведения, полученные во время подготовки диска:</span><span class="sxs-lookup"><span data-stu-id="85022-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="85022-149">идентификатор диска;</span><span class="sxs-lookup"><span data-stu-id="85022-149">The drive Id</span></span>

    -   <span data-ttu-id="85022-150">ключ BitLocker;</span><span class="sxs-lookup"><span data-stu-id="85022-150">The BitLocker key</span></span>

    -   <span data-ttu-id="85022-151">относительный путь к файлу манифеста на жестком диске;</span><span class="sxs-lookup"><span data-stu-id="85022-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="85022-152">хэш MD5 для файла манифеста в кодировке Base16.</span><span class="sxs-lookup"><span data-stu-id="85022-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="85022-153">Отправка дисков</span><span class="sxs-lookup"><span data-stu-id="85022-153">Shipping your drives</span></span>
<span data-ttu-id="85022-154">Отправьте диски по адресу, полученному на предыдущем этапе, а также передайте в службу импорта и экспорта номер отслеживания посылки.</span><span class="sxs-lookup"><span data-stu-id="85022-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="85022-155">Диски необходимо отправить через поддерживаемого перевозчика, который предоставит номер для отслеживания посылки.</span><span class="sxs-lookup"><span data-stu-id="85022-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="85022-156">Внесение сведений о доставке в задание импорта</span><span class="sxs-lookup"><span data-stu-id="85022-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="85022-157">Когда вы получите номер для отслеживания посылки, вызовите операцию [обновления свойств задания](/api/storageimportexport/jobs#Jobs_Update) и предоставьте название компании перевозчика, номер для отслеживания по этому заданию и номер счета перевозчика для возврата дисков.</span><span class="sxs-lookup"><span data-stu-id="85022-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="85022-158">Можно также указать количество дисков и дату отправки.</span><span class="sxs-lookup"><span data-stu-id="85022-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85022-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="85022-159">Next steps</span></span>

* [<span data-ttu-id="85022-160">Использование REST API службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="85022-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
