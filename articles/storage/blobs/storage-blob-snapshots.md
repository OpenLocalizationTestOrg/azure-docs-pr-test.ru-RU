---
title: "доступный только для чтения моментальный снимок большого двоичного объекта в хранилище Azure aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate моментальный снимок большого двоичного объекта tooback копии большого двоичного объекта в данный момент времени. Понять, как выставляются моментальные снимки и как toouse их toominimize емкости расходов."
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
ms.openlocfilehash: 57f2e76b8899b8a513688bf148dd13673141d5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-blob-snapshot"></a>Создание моментального снимка BLOB-объекта

Моментальный снимок — это версия BLOB-объекта только для чтения, сделанная в определенный момент времени. Моментальные снимки полезны для архивации BLOB-объектов. После создания моментального снимка его можно прочитать, скопировать или удалить, но вы не можете изменять его.

Моментальный снимок большого двоичного объекта — идентичные tooits базового большого двоичного объекта, за исключением hello большого двоичного объекта имеет URI **DateTime** значение добавлено toohello большой двоичный объект URI tooindicate hello времени в какой hello был сделан снимок. Например, если страничный большой двоичный объект URI — `http://storagesample.core.blob.windows.net/mydrives/myvhd`, моментальный снимок hello URI аналогичен слишком`http://storagesample.core.blob.windows.net/mydrives/myvhd?snapshot=2011-03-09T01:42:34.9360000Z`.

> [!NOTE]
> Все моментальные снимки имеют URI hello базового большого двоичного объекта. Здравствуйте только различие между hello базового BLOB-объектов и моментальных снимков hello hello добавляется **DateTime** значение.
>

Большой двоичный объект может иметь любое количество моментальных снимков. Моментальные снимки хранятся до тех пор, пока не будут явно удалены. При удалении исходного BLOB-объекта моментальный снимок будет также удален. Hello моментальных снимков, связанных с tootrack hello базового большого двоичного объекта, можно перечислить моментальные.

При создании моментального снимка большого двоичного объекта, hello системные свойства большого двоичного объекта, скопированного toohello моментальный снимок с hello одинаковые значения. Hello базового большого двоичного объекта метаданных также является скопированный toohello моментальных снимков, если не указать отдельные метаданные для hello моментального снимка при ее создании.

Связанные с hello базового BLOB-объекта аренды не влияют на hello моментального снимка. Вы не можете получить аренду в моментальном снимке.

Файл виртуального жесткого диска, используется toostore hello текущие данные и состояние диска виртуальной Машины. Можно отсоединить диск от внутри hello виртуальной Машины или завершить работу виртуальной Машины hello и затем создать моментальный снимок VHD-файл. Можно использовать этот файл моментального снимка более поздней версии tooretrieve hello VHD файлов на момент времени и повторно создайте hello виртуальной Машины.

Если для учетной записи хранилища hello включено шифрование службы хранилища (SSE) в какие hello находится больших двоичных объектов, а затем неактивные будут зашифрованы все моментальные снимки, что BLOB-объекта.

## <a name="create-a-snapshot"></a>Создание моментального снимка
Hello примере кода показано, как hello toocreate моментальный снимок с помощью [клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). В этом примере задает дополнительные метаданные для hello моментального снимка при его создании.

```csharp
private static async Task CreateBlockBlobSnapshot(CloudBlobContainer container)
{
    // Create a new block blob in hello container.
    CloudBlockBlob baseBlob = container.GetBlockBlobReference("sample-base-blob.txt");

    // Add blob metadata.
    baseBlob.Metadata.Add("ApproxBlobCreatedDate", DateTime.UtcNow.ToString());

    try
    {
        // Upload hello blob toocreate it, with its metadata.
        await baseBlob.UploadTextAsync(string.Format("Base blob: {0}", baseBlob.Uri.ToString()));

        // Sleep 5 seconds.
        System.Threading.Thread.Sleep(5000);

        // Create a snapshot of hello base blob.
        // Specify metadata at hello time that hello snapshot is created toospecify unique metadata for hello snapshot.
        // If no metadata is specified when hello snapshot is created, hello base blob's metadata is copied toohello snapshot.
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

## <a name="copy-snapshots"></a>Копирование моментальных снимков
Операции копирования больших двоичных объектов и моментальных снимков подчиняются следующим правилам.

* Можно скопировать моментальный снимок и заменить им исходный большой двоичный объект. Переместив положения toohello hello базового BLOB-объекта моментального снимка, можно восстановить более раннюю версию большого двоичного объекта. Здравствуйте, моментальный снимок остается, но hello базовый большой двоичный объект перезаписывается копией для записи моментальных снимков hello.
* Можно скопировать моментальный снимок tooa BLOB-объект назначения с другим именем. Hello полученный BLOB-объект назначения является доступным для записи большого двоичного объекта и моментальный снимок не.
* Когда копируется исходный большой двоичный объект, все снимки hello исходного большого двоичного объекта не копируются toohello назначения. Когда целевой большой двоичный объект перезаписывается копией, все моментальные снимки, связанные с hello исходный BLOB-объект назначения остаются без изменений.
* При создании моментального снимка большого двоичного объекта блока, список зафиксированных блокировок hello blob также является снимком скопированный toohello. Незафиксированные блоки не копируются.

## <a name="specify-an-access-condition"></a>Назначение условий доступа
При вызове [CreateSnapshotAsync][dotnet_CreateSnapshotAsync], можно указать условие доступа, чтобы hello моментальный снимок создается только в том случае, если условие выполняется. toospecify условие доступа, используйте hello [AccessCondition] [ dotnet_AccessCondition] параметра. Если условие не выполняется, hello моментальный снимок не создается и hello службы BLOB-объектов возвращает код состояния hello [HTTPStatusCode][dotnet_HTTPStatusCode]. PreconditionFailed.

## <a name="delete-snapshots"></a>Удаление моментальных снимков
Для удаления большого двоичного объекта с моментальными снимками hello моментальные снимки также будут удалены. Удаление моментального снимка по отдельности или удалить все снимки при удалении hello исходного большого двоичного объекта. При попытке toodelete большой двоичный объект, по-прежнему имеются моментальные снимки, результатом будет ошибка.

Здравствуйте, следуя примере кода показано, как toodelete большого двоичного объекта и его моментальные снимки в .NET, где `blockBlob` — это объект типа [CloudBlockBlob][dotnet_CloudBlockBlob]:

```csharp
await blockBlob.DeleteIfExistsAsync(DeleteSnapshotsOption.IncludeSnapshots, null, null, null);
```

## <a name="snapshots-with-azure-premium-storage"></a>Моментальные снимки и хранилище Azure Premium
При использовании хранилища Premium моментальных снимков, применяются hello следующие правила:

* Hello моментальных снимков для каждого большого двоичного объекта страницы в учетной записи хранения premium не более 100. Если этот предел превышен, hello операции моментальный снимок BLOB-объектов возвращает код ошибки 409 (`SnapshotCountExceeded`).
* При использовании учетной записи хранения класса Premium каждые десять минут можно создавать один моментальный снимок страничного BLOB-объекта. В случае превышения этого курса hello операции моментальный снимок BLOB-объектов возвращает код ошибки 409 (`SnapshotOperationRateExceeded`).
* tooread моментального снимка, можно использовать toocopy операции копирования BLOB-объекта hello моментального снимка tooanother страничный большой двоичный объект в учетной записи hello. Hello BLOB-объект назначения для операции копирования hello не должен содержать все существующие моментальные снимки. Если BLOB-объект назначения hello имеет моментальные снимки, то hello операции копирования BLOB-объектов возвращает код ошибки 409 (`SnapshotsPresent`).

## <a name="return-hello-absolute-uri-tooa-snapshot"></a>Возвращает моментальный снимок tooa hello абсолютный URI
Данный пример кода C# создается моментальный снимок и записывает hello абсолютный URI для hello первичного расположения.

```csharp
//Create hello blob service client object.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";

CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();

//Get a reference tooa blob.
CloudBlockBlob blob = container.GetBlockBlobReference("sampleblob.txt");
blob.UploadText("This is a blob.");

//Create a snapshot of hello blob and write out its primary URI.
CloudBlockBlob blobSnapshot = blob.CreateSnapshot();
Console.WriteLine(blobSnapshot.SnapshotQualifiedStorageUri.PrimaryUri);
```

## <a name="understand-how-snapshots-accrue-charges"></a>Общая информация о том, как моментальные снимки увеличивают плату
Создание моментального снимка, который является копией только для чтения большого двоичного объекта, может привести к учетной записи tooyour плата хранения дополнительных данных. При разработке приложения, это важно toobe учитывать как выставления счетов может провести, чтобы свести к минимуму затраты.

### <a name="important-billing-considerations"></a>Важные вопросы о выставлении счетов
После списка Hello включает tooconsider ключевые моменты при создании моментального снимка.

* Вашей учетной записи хранилища может привести к сборам за уникальные блокировки и страницы, являются ли они в большом двоичном объекте hello, или в снимке hello. Ваша учетная запись не создает дополнительных затрат на моментальные снимки, связанные с большой двоичный объект, пока вы не обновите hello больших двоичных объектов, на которых они основаны. После обновления базового hello большого двоичного объекта он расходится со своими моментальными снимками. В этом случае вы оплачивать уникальные блокировки hello и страницы в каждом большого двоичного объекта или моментального снимка.
* Когда вы заменяете блок в блочном большом двоичном объекте, за этот блок начинает взиматься плата как за уникальный. Это верно, даже если блока hello hello hello же и же идентификатор блока данных по мере имеет в снимке hello. После фиксации блока hello снова, он расходится со всеми своими двойниками во всех моментальных снимках, и вы будете оплачивать его данные. Здравствуйте, справедливо и для страницы в страничный большой двоичный объект, который обновляется с идентичными данными.
* Замена блочный BLOB-объект, вызывающий hello [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [UploadFromStream] [ dotnet_UploadFromStream], или [UploadFromByteArray] [ dotnet_UploadFromByteArray] метод заменяет все блоки в большом двоичном объекте hello. Если моментальный снимок, связанный с этим большим двоичным объектом, теперь разделить все блоки в hello базового BLOB-объектов и моментальных снимков и вы будете оплачивать все блоки hello в обоих больших двоичных объектов. Это верно, даже если данные hello в hello базового BLOB-объектов и моментальных снимков hello остаются идентичными.
* Hello службы больших двоичных объектов не имеет toodetermine означает ли два блока содержат идентичные данные. Каждая блокировка, которая была загружена и зафиксирована, обрабатывается как уникальная, даже если он имеет hello тем же данным и hello же блокирует идентификатор. Поскольку плата взимается за уникальные блокировки, это важно tooconsider, обновление большого двоичного объекта, имеющего моментальные снимки приводит к дополнительным уникальным блокировкам и дополнительным расходам.

### <a name="minimize-cost-with-snapshot-management"></a>Минимизация затрат с помощью управления моментальными снимками

Рекомендуется тщательно управления вашей моментальными снимками tooavoid дополнительная плата. Можно выполнить следующие рекомендации toohelp свести к минимуму затраты hello путем хранения hello вашей моментальных снимков.

* Удаление и повторное создание моментальных снимков, связанных с большой двоичный объект всякий раз при обновлении большого двоичного объекта hello, даже если вы обновляете с идентичными данными, если при разработке приложения требует сохранения моментальных снимков. Удаление и повторное создание моментальных снимков hello blob, позволяет обеспечить не расходятся hello больших двоичных объектов и моментальных снимков.
* Если необходимо хранить моментальные снимки для BLOB-объекта, старайтесь не вызывать [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], или [UploadFromByteArray] [ dotnet_UploadFromByteArray] tooupdate hello большого двоичного объекта. Эти методы заменяют все блоки hello в большом двоичном объекте hello, значительно приводит к вашей базового большого двоичного объекта и его toodiverge моментальные снимки. Вместо этого обновления hello наименьшее возможное количество блоков, с помощью hello [PutBlock] [ dotnet_PutBlock] и [PutBlockList] [ dotnet_PutBlockList] методы.

### <a name="snapshot-billing-scenarios"></a>Сценарии выставления счетов за моментальные снимки
Привет, следующие сценарии демонстрируют, как добавляется плата за большой двоичный объект блока и ее моментальные снимки.

**Сценарий 1**

В сценарии 1 базовый большой двоичный объект hello не обновлена после hello моментального снимка, поэтому плата начисляется только за уникальные блокировки 1, 2 и 3.

![Ресурсы хранилища Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-1.png)

**Сценарий 2**

В сценарии 2 hello базовый BLOB-объект был обновлен, но hello моментальный снимок нет. Блокировка 3 была обновлена и несмотря на то, что он содержит hello и тех же данных, и таким же Идентификатором hello, это не так же, как блокировки 3 в моментальном снимке hello hello. В результате учетной записи hello взимается плата за четыре блокировки.

![Ресурсы хранилища Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-2.png)

**Сценарий 3**

В сценарии 3 базовый hello BLOB-объект был обновлен, но hello моментальный снимок нет. Блокировка 3 была заменена блокировкой 4 в hello базового большого двоичного объекта, но hello моментальных снимков по-прежнему отражает блокировку 3. В результате учетной записи hello взимается плата за четыре блокировки.

![Ресурсы хранилища Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-3.png)

**Сценарий 4**

В сценарии 4 hello базовый BLOB-объект был обновлен полностью и не содержит ни одного первоначальных блокировок. В результате учетной записи hello взимается за все 8 уникальных блокировок. Такая ситуация возникает, если используется метод обновления, такие как [UploadFromFile][dotnet_UploadFromFile], [UploadText][dotnet_UploadText], [ UploadFromStream][dotnet_UploadFromStream], или [UploadFromByteArray][dotnet_UploadFromByteArray], так как эти методы заменяют все содержимое hello большого двоичного объекта.

![Ресурсы хранилища Azure](./media/storage-blob-snapshots/storage-blob-snapshots-billing-scenario-4.png)

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о работе с моментальными снимками диска виртуальной машины см. в статье [Архивация неуправляемых дисков виртуальной машины Azure с помощью добавочных моментальных снимков](../../virtual-machines/windows/incremental-snapshots.md).

* Дополнительные примеры кода, в которых используется хранилище BLOB-объектов, см. на странице с [примерами кода Azure](https://azure.microsoft.com/documentation/samples/?service=storage&term=blob). Можно загрузить пример приложения и запустите его или просмотр кода hello в GitHub.

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