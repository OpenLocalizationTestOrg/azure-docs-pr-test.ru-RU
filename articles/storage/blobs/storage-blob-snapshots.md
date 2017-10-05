---
title: "Создание моментального снимка большого двоичного объекта только для чтения в службе хранилища Azure | Документация Майкрософт"
description: "Узнайте, как создать моментальный снимок большого двоичного объекта для резервного копирования данных BLOB-объектов в конкретный момент времени. Узнайте, как выставляются счета за моментальные снимки и как их можно использовать для сокращения расходов емкости."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 3710705d-e127-4b01-8d0f-29853fb06d0d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: marsma
ms.openlocfilehash: b1d87cd66457b08bba594bfc7de1e9e4e2dff1e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-blob-snapshot"></a><span data-ttu-id="69f8f-104">Создание моментального снимка BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="69f8f-104">Create a blob snapshot</span></span>

<span data-ttu-id="69f8f-105">Моментальный снимок — это версия BLOB-объекта только для чтения, сделанная в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="69f8f-105">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="69f8f-106">Моментальные снимки полезны для архивации BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="69f8f-106">Snapshots are useful for backing up blobs.</span></span> <span data-ttu-id="69f8f-107">После создания моментального снимка его можно прочитать, скопировать или удалить, но вы не можете изменять его.</span><span class="sxs-lookup"><span data-stu-id="69f8f-107">After you create a snapshot, you can read, copy, or delete it, but you cannot modify it.</span></span>

<span data-ttu-id="69f8f-108">Моментальный снимок большого двоичного объекта идентичен объекту, на основе которого он создан. Единственное исключение: к URI большого двоичного объекта добавляется значение **DateTime**, которое указывает время создания снимка.</span><span class="sxs-lookup"><span data-stu-id="69f8f-108">A snapshot of a blob is identical to its base blob, except that the blob URI has a **DateTime** value appended to the blob URI to indicate the time at which the snapshot was taken.</span></span> <span data-ttu-id="69f8f-109">Например, если страничный BLOB-объект имеет URI `http://storagesample.core.blob.windows.net/mydrives/myvhd`, то URI снимка будет иметь такой вид: `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span><span class="sxs-lookup"><span data-stu-id="69f8f-109">For example, if a page blob URI is `http://storagesample.core.blob.windows.net/mydrives/myvhd`, the snapshot URI is similar to `http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.</span></span>

> [!NOTE]
> <span data-ttu-id="69f8f-110">Все моментальные снимки имеют одинаковый URI базового большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="69f8f-110">All snapshots share the base blob's URI.</span></span> <span data-ttu-id="69f8f-111">Большой двоичный объект и его моментальный снимок отличаются только добавлением значения **DateTime** .</span><span class="sxs-lookup"><span data-stu-id="69f8f-111">The only distinction between the base blob and the snapshot is the appended **DateTime** value.</span></span>
>

<span data-ttu-id="69f8f-112">Большой двоичный объект может иметь любое количество моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-112">A blob can have any number of snapshots.</span></span> <span data-ttu-id="69f8f-113">Моментальные снимки хранятся до тех пор, пока не будут явно удалены.</span><span class="sxs-lookup"><span data-stu-id="69f8f-113">Snapshots persist until they are explicitly deleted.</span></span> <span data-ttu-id="69f8f-114">При удалении исходного BLOB-объекта моментальный снимок будет также удален.</span><span class="sxs-lookup"><span data-stu-id="69f8f-114">A snapshot cannot outlive its base blob.</span></span> <span data-ttu-id="69f8f-115">Чтобы было удобнее контролировать моментальные снимки большого двоичного объекта, их можно пронумеровать.</span><span class="sxs-lookup"><span data-stu-id="69f8f-115">You can enumerate the snapshots associated with the base blob to track your current snapshots.</span></span>

<span data-ttu-id="69f8f-116">При создании моментального снимка BLOB-объекта его системные свойства и их значения копируются в снимок.</span><span class="sxs-lookup"><span data-stu-id="69f8f-116">When you create a snapshot of a blob, the blob's system properties are copied to the snapshot with the same values.</span></span> <span data-ttu-id="69f8f-117">Метаданные базового большого двоичного объекта также копируются в моментальный снимок, если при его создании не были указаны отдельные метаданные для снимка.</span><span class="sxs-lookup"><span data-stu-id="69f8f-117">The base blob's metadata is also copied to the snapshot, unless you specify separate metadata for the snapshot when you create it.</span></span>

<span data-ttu-id="69f8f-118">Свойства аренды, связанные с базовым BLOB-объектом, не влияют на моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="69f8f-118">Any leases associated with the base blob do not affect the snapshot.</span></span> <span data-ttu-id="69f8f-119">Вы не можете получить аренду в моментальном снимке.</span><span class="sxs-lookup"><span data-stu-id="69f8f-119">You cannot acquire a lease on a snapshot.</span></span>

<span data-ttu-id="69f8f-120">VHD-файл используется для хранения текущей информации о диске виртуальной машины и его состояния.</span><span class="sxs-lookup"><span data-stu-id="69f8f-120">A VHD file is used to store the current information and status for a VM disk.</span></span> <span data-ttu-id="69f8f-121">Можно отключить диск в виртуальной машине или завершить ее работу, после чего создать моментальный снимок его VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="69f8f-121">You can detach a disk from within the VM or shut down the VM, and then take a snapshot of its VHD file.</span></span> <span data-ttu-id="69f8f-122">Этот файл моментального снимка можно будет использовать позже, чтобы получить VHD-файл на этот момент времени и повторно создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="69f8f-122">You can use that snapshot file later to retrieve the VHD file at that point in time and recreate the VM.</span></span>

<span data-ttu-id="69f8f-123">Если для учетной записи хранения, в которой хранится большой двоичный объект, включено шифрование службы хранилища (SSE), то все неактивные моментальные снимки этого большого двоичного объекта также будут шифроваться.</span><span class="sxs-lookup"><span data-stu-id="69f8f-123">If Storage Service Encryption (SSE) is enabled for the storage account in which the blob resides, then any snapshots taken of that blob will be encrypted at rest.</span></span>

## <a name="create-a-snapshot"></a><span data-ttu-id="69f8f-124">Создание моментального снимка</span><span class="sxs-lookup"><span data-stu-id="69f8f-124">Create a snapshot</span></span>
<span data-ttu-id="69f8f-125">В следующем примере кода показано, как создать моментальный снимок с помощью [клиентской библиотеки хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="69f8f-125">The following code example shows how to create a snapshot by using the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="69f8f-126">В этом примере мы указываем дополнительные метаданные для моментального снимка при его создании.</span><span class="sxs-lookup"><span data-stu-id="69f8f-126">This example specifies additional metadata for the snapshot when it is created.</span></span>

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in the container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload the blob to create it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of the base blob.
        // Specify metadata at the time that the snapshot is created to specify unique metadata for the snapshot.
        // If no metadata is specified when the snapshot is created, the base blob's metadata is copied to the snapshot.
        Dictionary<string, string> metadata = new Dictionary<string, string>();
        metadata.Add("ApproxSnapshotCreatedDate", DateTime.UtcNow.ToString());
        await baseBlob.CreateSnapshotAsync(metadata, null, null, null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="copy-snapshots"></a><span data-ttu-id="69f8f-127">Копирование моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="69f8f-127">Copy snapshots</span></span>
<span data-ttu-id="69f8f-128">Операции копирования больших двоичных объектов и моментальных снимков подчиняются следующим правилам.</span><span class="sxs-lookup"><span data-stu-id="69f8f-128">Copy operations involving blobs and snapshots follow these rules:</span></span>

* <span data-ttu-id="69f8f-129">Можно скопировать моментальный снимок и заменить им исходный большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="69f8f-129">You can copy a snapshot over its base blob.</span></span> <span data-ttu-id="69f8f-130">Повысив уровень моментального снимка до базового большого двоичного объекта, можно восстановить более раннюю версию большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="69f8f-130">By promoting a snapshot to the position of the base blob, you can restore an earlier version of a blob.</span></span> <span data-ttu-id="69f8f-131">Моментальный снимок остается, но базовый BLOB-объект перезаписывается с помощью копии моментального снимка, допускающей запись.</span><span class="sxs-lookup"><span data-stu-id="69f8f-131">The snapshot remains, but the base blob is overwritten with a writable copy of the snapshot.</span></span>
* <span data-ttu-id="69f8f-132">Можно скопировать моментальный снимок в целевой большой двоичный объект с другим именем.</span><span class="sxs-lookup"><span data-stu-id="69f8f-132">You can copy a snapshot to a destination blob with a different name.</span></span> <span data-ttu-id="69f8f-133">Полученный целевой BLOB-объект не станет моментальным снимком, а будет BLOB-объектом, доступным для записи.</span><span class="sxs-lookup"><span data-stu-id="69f8f-133">The resulting destination blob is a writable blob and not a snapshot.</span></span>
* <span data-ttu-id="69f8f-134">Если копируется исходный большой двоичный объект, его моментальные снимки не копируются.</span><span class="sxs-lookup"><span data-stu-id="69f8f-134">When a source blob is copied, any snapshots of the source blob are not copied to the destination.</span></span> <span data-ttu-id="69f8f-135">Если большой двоичный объект восстанавливается из его копии, это не влияет на связанные с ним моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="69f8f-135">When a destination blob is overwritten with a copy, any snapshots associated with the original destination blob remain intact.</span></span>
* <span data-ttu-id="69f8f-136">При создании моментального снимка блочного BLOB-объекта в снимок также копируется его список зафиксированных блоков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-136">When you create a snapshot of a block blob, the blob's committed block list is also copied to the snapshot.</span></span> <span data-ttu-id="69f8f-137">Незафиксированные блоки не копируются.</span><span class="sxs-lookup"><span data-stu-id="69f8f-137">Any uncommitted blocks are not copied.</span></span>

## <a name="specify-an-access-condition"></a><span data-ttu-id="69f8f-138">Назначение условий доступа</span><span class="sxs-lookup"><span data-stu-id="69f8f-138">Specify an access condition</span></span>
<span data-ttu-id="69f8f-139">При вызове [CreateSnapshotAsync][dotnet_CreateSnapshotAsync] можно указать условие доступа, чтобы моментальный снимок создавался только в том случае, если данное условие выполняется.</span><span class="sxs-lookup"><span data-stu-id="69f8f-139">When you call [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], you can specify an access condition so that the snapshot is created only if a condition is met.</span></span> <span data-ttu-id="69f8f-140">Для этого воспользуйтесь параметром [AccessCondition][dotnet_AccessCondition].</span><span class="sxs-lookup"><span data-stu-id="69f8f-140">To specify an access condition, use the [AccessCondition][dotnet_AccessCondition] parameter.</span></span> <span data-ttu-id="69f8f-141">При невыполнении указанного условия моментальный снимок не будет создан, а служба BLOB-объектов вернет код состояния [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span><span class="sxs-lookup"><span data-stu-id="69f8f-141">If the specified condition is not met, the snapshot is not created, and the Blob service returns status code [HTTPStatusCode][dotnet_HTTPStatusCode].PreconditionFailed.</span></span>

## <a name="delete-snapshots"></a><span data-ttu-id="69f8f-142">Удаление моментальных снимков</span><span class="sxs-lookup"><span data-stu-id="69f8f-142">Delete snapshots</span></span>
<span data-ttu-id="69f8f-143">Большой двоичный объект с моментальными снимками невозможно удалить, пока не будут удалены все его снимки.</span><span class="sxs-lookup"><span data-stu-id="69f8f-143">You can't delete a blob with snapshots unless the snapshots are also deleted.</span></span> <span data-ttu-id="69f8f-144">Можно удалить моментальный снимок отдельно или указать, чтобы при удалении исходного большого двоичного объекта были удалены и все его моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="69f8f-144">You can delete a snapshot individually, or specify that all snapshots be deleted when the source blob is deleted.</span></span> <span data-ttu-id="69f8f-145">Попытка удалить большой двоичный объект, у которого еще есть моментальные снимки, завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="69f8f-145">If you attempt to delete a blob that still has snapshots, an error results.</span></span>

<span data-ttu-id="69f8f-146">В следующем коде показан пример удаления большого двоичного объекта и его моментальных снимков в .NET, где `blockBlob` является объектом типа [CloudBlockBlob][dotnet_CloudBlockBlob]:</span><span class="sxs-lookup"><span data-stu-id="69f8f-146">The following code example shows how to delete a blob and its snapshots in .NET, where `blockBlob` is an object of type [CloudBlockBlob][dotnet_CloudBlockBlob]:</span></span>

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a><span data-ttu-id="69f8f-147">Моментальные снимки и хранилище Azure Premium</span><span class="sxs-lookup"><span data-stu-id="69f8f-147">Snapshots with Azure Premium Storage</span></span>
<span data-ttu-id="69f8f-148">При использовании моментальных снимков с хранилищем класса "Премиум" применяются такие правила:</span><span class="sxs-lookup"><span data-stu-id="69f8f-148">When using snapshots with Premium Storage, the following rules apply:</span></span>

* <span data-ttu-id="69f8f-149">Учетная запись хранения класса Premium поддерживает до 100 моментальных снимков на каждый страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="69f8f-149">The maximum number of snapshots per page blob in a premium storage account is 100.</span></span> <span data-ttu-id="69f8f-150">При превышении этого предела операция Snapshot Blob возвращает код ошибки 409 (`SnapshotCountExceeded`).</span><span class="sxs-lookup"><span data-stu-id="69f8f-150">If that limit is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotCountExceeded`).</span></span>
* <span data-ttu-id="69f8f-151">При использовании учетной записи хранения класса Premium каждые десять минут можно создавать один моментальный снимок страничного BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="69f8f-151">You can take a snapshot of a page blob in a premium storage account once every 10 minutes.</span></span> <span data-ttu-id="69f8f-152">При превышении этого значения операция Snapshot Blob возвращает код ошибки 409 (`SnapshotOperationRateExceeded`).</span><span class="sxs-lookup"><span data-stu-id="69f8f-152">If that rate is exceeded, the Snapshot Blob operation returns error code 409 (`SnapshotOperationRateExceeded`).</span></span>
* <span data-ttu-id="69f8f-153">Для чтения моментального снимка вы можете воспользоваться операцией Copy Blob, чтобы скопировать его в другой страничный BLOB-объект в пределах учетной записи.</span><span class="sxs-lookup"><span data-stu-id="69f8f-153">To read a snapshot, you can use the Copy Blob operation to copy a snapshot to another page blob in the account.</span></span> <span data-ttu-id="69f8f-154">При этом в целевом большом двоичном объекте, выбранном для копирования, не должно быть других моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-154">The destination blob for the copy operation must not have any existing snapshots.</span></span> <span data-ttu-id="69f8f-155">Если у целевого большого двоичного объекта есть моментальные снимки, операция Copy Blob возвращает код ошибки 409 (`SnapshotsPresent`).</span><span class="sxs-lookup"><span data-stu-id="69f8f-155">If the destination blob does have snapshots, then the Copy Blob operation returns error code 409 (`SnapshotsPresent`).</span></span>

## <a name="return-the-absolute-uri-to-a-snapshot"></a><span data-ttu-id="69f8f-156">Возврат абсолютного URI для моментального снимка</span><span class="sxs-lookup"><span data-stu-id="69f8f-156">Return the absolute URI to a snapshot</span></span>
<span data-ttu-id="69f8f-157">Этот пример кода C# создает новый моментальный снимок и записывает абсолютный URI для первичного расположения.</span><span class="sxs-lookup"><span data-stu-id="69f8f-157">This C# code example creates a snapshot and writes out the absolute URI for the primary location.</span></span>

```csharp
//Create the blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference to a blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of the blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a><span data-ttu-id="69f8f-158">Общая информация о том, как моментальные снимки увеличивают плату</span><span class="sxs-lookup"><span data-stu-id="69f8f-158">Understand how snapshots accrue charges</span></span>
<span data-ttu-id="69f8f-159">Создание моментальных снимков, представляющих собой копии больших двоичных объектов с доступом только для чтения, может привести к дополнительной плате за хранение данных в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="69f8f-159">Creating a snapshot, which is a read-only copy of a blob, can result in additional data storage charges to your account.</span></span> <span data-ttu-id="69f8f-160">При проектировании приложения важно учитывать, как эта плата может накапливаться, чтобы минимизировать затраты.</span><span class="sxs-lookup"><span data-stu-id="69f8f-160">When designing your application, it is important to be aware of how these charges might accrue so that you can minimize costs.</span></span>

### <a name="important-billing-considerations"></a><span data-ttu-id="69f8f-161">Важные вопросы о выставлении счетов</span><span class="sxs-lookup"><span data-stu-id="69f8f-161">Important billing considerations</span></span>
<span data-ttu-id="69f8f-162">Следующий список включает ключевые пункты, которые следует рассмотреть при создании моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="69f8f-162">The following list includes key points to consider when creating a snapshot.</span></span>

* <span data-ttu-id="69f8f-163">Плата взимается за уникальные блоки и страницы независимо от того, где они находятся: в большом двоичном объекте или моментальном снимке.</span><span class="sxs-lookup"><span data-stu-id="69f8f-163">Your storage account incurs charges for unique blocks or pages, whether they are in the blob or in the snapshot.</span></span> <span data-ttu-id="69f8f-164">Ваша учетная запись не влечет за собой дополнительных затрат на моментальные снимки, связанные с большим двоичным объектом, пока большой двоичный объект, на котором они основаны, не будет обновлен.</span><span class="sxs-lookup"><span data-stu-id="69f8f-164">Your account does not incur additional charges for snapshots associated with a blob until you update the blob on which they are based.</span></span> <span data-ttu-id="69f8f-165">После изменения базового большого двоичного объекта он начнет отличаться от своих моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-165">After you update the base blob, it diverges from its snapshots.</span></span> <span data-ttu-id="69f8f-166">Теперь вы будете оплачивать все уникальные блоки и страницы в каждом большом двоичном объекте или моментальном снимке.</span><span class="sxs-lookup"><span data-stu-id="69f8f-166">When this happens, you are charged for the unique blocks or pages in each blob or snapshot.</span></span>
* <span data-ttu-id="69f8f-167">Когда вы заменяете блок в блочном большом двоичном объекте, за этот блок начинает взиматься плата как за уникальный.</span><span class="sxs-lookup"><span data-stu-id="69f8f-167">When you replace a block within a block blob, that block is subsequently charged as a unique block.</span></span> <span data-ttu-id="69f8f-168">Это произойдет, даже если у блока тот же идентификатор блока и те же данные, что и в моментальном снимке.</span><span class="sxs-lookup"><span data-stu-id="69f8f-168">This is true even if the block has the same block ID and the same data as it has in the snapshot.</span></span> <span data-ttu-id="69f8f-169">Как только блок фиксируется заново, он расходится со всеми своими дубликатами во всех моментальных снимках и вы будете оплачивать его данные.</span><span class="sxs-lookup"><span data-stu-id="69f8f-169">After the block is committed again, it diverges from its counterpart in any snapshot, and you will be charged for its data.</span></span> <span data-ttu-id="69f8f-170">Это же происходит и для страницы в страничном BLOB-объекте, обновляемом идентичными данными.</span><span class="sxs-lookup"><span data-stu-id="69f8f-170">The same holds true for a page in a page blob that's updated with identical data.</span></span>
* <span data-ttu-id="69f8f-171">При замещении блочного BLOB-объекта путем вызова метода [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] или [UploadFromByteArray][dotnet_UploadFromByteArray] заменяются все блоки в этом большом двоичном объекте.</span><span class="sxs-lookup"><span data-stu-id="69f8f-171">Replacing a block blob by calling the [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] method replaces all blocks in the blob.</span></span> <span data-ttu-id="69f8f-172">Если с этим большим двоичным объектом связан моментальный снимок, то все блоки в базовом большом двоичном объекте перестанут совпадать с блоками в моментальном снимке, и вы будете оплачивать хранение всех блоков в обоих больших двоичных объектах.</span><span class="sxs-lookup"><span data-stu-id="69f8f-172">If you have a snapshot associated with that blob, all blocks in the base blob and snapshot now diverge, and you will be charged for all the blocks in both blobs.</span></span> <span data-ttu-id="69f8f-173">Это произойдет, даже если данные базового большого двоичного объекта и моментального снимка останутся идентичными.</span><span class="sxs-lookup"><span data-stu-id="69f8f-173">This is true even if the data in the base blob and the snapshot remain identical.</span></span>
* <span data-ttu-id="69f8f-174">В службе BLOB-объектов Azure нет средств, позволяющих определить, содержат ли два блока идентичные данные.</span><span class="sxs-lookup"><span data-stu-id="69f8f-174">The Azure Blob service does not have a means to determine whether two blocks contain identical data.</span></span> <span data-ttu-id="69f8f-175">Каждый блок, который был загружен и зафиксирован, обрабатывается как уникальный, даже если он содержит те же данные и имеет тот же идентификатор блока.</span><span class="sxs-lookup"><span data-stu-id="69f8f-175">Each block that is uploaded and committed is treated as unique, even if it has the same data and the same block ID.</span></span> <span data-ttu-id="69f8f-176">Так как плата добавляется за уникальные блоки, важно иметь в виду, что обновление большого двоичного объекта, содержащего моментальный снимок, приведет к появлению дополнительных уникальных блоков и дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="69f8f-176">Because charges accrue for unique blocks, it's important to consider that updating a blob that has a snapshot results in additional unique blocks and additional charges.</span></span>

### <a name="minimize-cost-with-snapshot-management"></a><span data-ttu-id="69f8f-177">Минимизация затрат с помощью управления моментальными снимками</span><span class="sxs-lookup"><span data-stu-id="69f8f-177">Minimize cost with snapshot management</span></span>

<span data-ttu-id="69f8f-178">Рекомендуется управлять моментальными снимками осторожно, чтобы избежать наценок.</span><span class="sxs-lookup"><span data-stu-id="69f8f-178">We recommend managing your snapshots carefully to avoid extra charges.</span></span> <span data-ttu-id="69f8f-179">Выполните приведенные ниже рекомендации, чтобы свести к минимуму затраты на хранение моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-179">You can follow these best practices to help minimize the costs incurred by the storage of your snapshots:</span></span>

* <span data-ttu-id="69f8f-180">Удаляйте и повторно создавайте моментальные снимки, связанные с большим двоичным объектом, при обновлении этого объекта, даже если вы обновляете его идентичными данными, если только структура вашего приложения не требует сохранения моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-180">Delete and re-create snapshots associated with a blob whenever you update the blob, even if you are updating with identical data, unless your application design requires that you maintain snapshots.</span></span> <span data-ttu-id="69f8f-181">За счет удаления и повторного создания моментальных снимков больших двоичных объектов можно исключить расхождение большого двоичного объекта с моментальными снимками.</span><span class="sxs-lookup"><span data-stu-id="69f8f-181">By deleting and re-creating the blob's snapshots, you can ensure that the blob and snapshots do not diverge.</span></span>
* <span data-ttu-id="69f8f-182">Если необходимо хранить моментальные снимки для больших двоичных объектов, то не вызывайте для их обновления методы [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] и [UploadFromByteArray][dotnet_UploadFromByteArray].</span><span class="sxs-lookup"><span data-stu-id="69f8f-182">If you are maintaining snapshots for a blob, avoid calling [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray] to update the blob.</span></span> <span data-ttu-id="69f8f-183">Эти методы заменяют все блоки в большом двоичном объекте, и после этого базовый большой двоичный объект начинает значительно отличаться от своих моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-183">These methods replace all of the blocks in the blob, causing your base blob and its snapshots to diverge significantly.</span></span> <span data-ttu-id="69f8f-184">Вместо этого обновляйте наименьшее возможное количество блоков с помощью методов [PutBlock][dotnet_PutBlock] и [PutBlockList][dotnet_PutBlockList].</span><span class="sxs-lookup"><span data-stu-id="69f8f-184">Instead, update the fewest possible number of blocks by using the [PutBlock][dotnet_PutBlock] and [PutBlockList][dotnet_PutBlockList] methods.</span></span>

### <a name="snapshot-billing-scenarios"></a><span data-ttu-id="69f8f-185">Сценарии выставления счетов за моментальные снимки</span><span class="sxs-lookup"><span data-stu-id="69f8f-185">Snapshot billing scenarios</span></span>
<span data-ttu-id="69f8f-186">В следующих сценариях показано, как добавляется плата за большой двоичный объект и его моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="69f8f-186">The following scenarios demonstrate how charges accrue for a block blob and its snapshots.</span></span>

<span data-ttu-id="69f8f-187">**Сценарий 1**</span><span class="sxs-lookup"><span data-stu-id="69f8f-187">**Scenario 1**</span></span>

<span data-ttu-id="69f8f-188">В сценарии 1 базовый большой двоичный объект создания моментального снимка не обновлялся, поэтому плата начисляется только за уникальные блоки 1, 2 и 3.</span><span class="sxs-lookup"><span data-stu-id="69f8f-188">In scenario 1, the base blob has not been updated after the snapshot was taken, so charges are incurred only for unique blocks 1, 2, and 3.</span></span>

![Ресурсы хранилища Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

<span data-ttu-id="69f8f-190">**Сценарий 2**</span><span class="sxs-lookup"><span data-stu-id="69f8f-190">**Scenario 2**</span></span>

<span data-ttu-id="69f8f-191">В сценарии 2 базовый большой двоичный объект изменился, а моментальный снимок — нет.</span><span class="sxs-lookup"><span data-stu-id="69f8f-191">In scenario 2, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="69f8f-192">Блок 3 был обновлен, и, хотя он содержит такие же данные и тот же идентификатор, он отличается от блока 3 в моментальном снимке.</span><span class="sxs-lookup"><span data-stu-id="69f8f-192">Block 3 was updated, and even though it contains the same data and the same ID, it is not the same as block 3 in the snapshot.</span></span> <span data-ttu-id="69f8f-193">В результате плата в учетной записи взимается за четыре блока.</span><span class="sxs-lookup"><span data-stu-id="69f8f-193">As a result, the account is charged for four blocks.</span></span>

![Ресурсы хранилища Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

<span data-ttu-id="69f8f-195">**Сценарий 3**</span><span class="sxs-lookup"><span data-stu-id="69f8f-195">**Scenario 3**</span></span>

<span data-ttu-id="69f8f-196">В сценарии 3 базовый большой двоичный объект изменился, а моментальный снимок — нет.</span><span class="sxs-lookup"><span data-stu-id="69f8f-196">In scenario 3, the base blob has been updated, but the snapshot has not.</span></span> <span data-ttu-id="69f8f-197">Блок 3 был заменен блоком 4 в базовом большом двоичном объекте, но моментальный снимок по-прежнему отражает блок 3.</span><span class="sxs-lookup"><span data-stu-id="69f8f-197">Block 3 was replaced with block 4 in the base blob, but the snapshot still reflects block 3.</span></span> <span data-ttu-id="69f8f-198">В результате плата в учетной записи взимается за четыре блока.</span><span class="sxs-lookup"><span data-stu-id="69f8f-198">As a result, the account is charged for four blocks.</span></span>

![Ресурсы хранилища Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

<span data-ttu-id="69f8f-200">**Сценарий 4**</span><span class="sxs-lookup"><span data-stu-id="69f8f-200">**Scenario 4**</span></span>

<span data-ttu-id="69f8f-201">В сценарии 4 базовый большой двоичный объект был полностью обновлен и не содержит никаких первоначальных блоков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-201">In scenario 4, the base blob has been completely updated and contains none of its original blocks.</span></span> <span data-ttu-id="69f8f-202">В результате плата в учетной записи взимается за все восемь уникальных блоков.</span><span class="sxs-lookup"><span data-stu-id="69f8f-202">As a result, the account is charged for all eight unique blocks.</span></span> <span data-ttu-id="69f8f-203">Этот сценарий может произойти при использовании таких методов обновления, как [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream] и [UploadFromByteArray][dotnet_UploadFromByteArray], так как эти методы заменяют все содержимое больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="69f8f-203">This scenario can occur if you are using an update method such as [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream][dotnet_UploadFromStream], or [UploadFromByteArray][dotnet_UploadFromByteArray], because these methods replace all of the contents of a blob.</span></span>

![Ресурсы хранилища Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a><span data-ttu-id="69f8f-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69f8f-205">Next steps</span></span>

* <span data-ttu-id="69f8f-206">Дополнительные сведения о работе с моментальными снимками диска виртуальной машины см. в статье [Архивация неуправляемых дисков виртуальной машины Azure с помощью добавочных моментальных снимков](../../virtual-machines/windows/incremental-snapshots.md).</span><span class="sxs-lookup"><span data-stu-id="69f8f-206">You can find more information about working with virtual machine (VM) disk snapshots in [Back up Azure unmanaged VM disks with incremental snapshots](../../virtual-machines/windows/incremental-snapshots.md)</span></span>

* <span data-ttu-id="69f8f-207">Дополнительные примеры кода, в которых используется хранилище BLOB-объектов, см. на странице с [примерами кода Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span><span class="sxs-lookup"><span data-stu-id="69f8f-207">For additional code examples using Blob storage, see [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob).</span></span> <span data-ttu-id="69f8f-208">Вы можете скачать пример приложения и запустить его или просмотреть код на GitHub.</span><span class="sxs-lookup"><span data-stu-id="69f8f-208">You can download a sample application and run it, or browse the code on GitHub.</span></span>

[dotnet_AccessCondition]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.accesscondition.aspx
[dotnet_CloudBlockBlob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.aspx
[dotnet_CreateSnapshotAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.createsnapshotasync.aspx
[dotnet_HTTPStatusCode]: https://msdn.microsoft.com/library/system.net.httpstatuscode(v=vs.110).aspx
[dotnet_PutBlockList]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblocklist.aspx
[dotnet_PutBlock]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.putblock.aspx
[dotnet_UploadFromByteArray]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfrombytearray.aspx
[dotnet_UploadFromFile]: https://msdn.microsoft.com/library/azure/mt705654.aspx
[dotnet_UploadFromStream]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadfromstream.aspx
[dotnet_UploadText]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblockblob.uploadtext.aspx