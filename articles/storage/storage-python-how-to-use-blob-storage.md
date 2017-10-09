---
title: "aaaHow toouse хранилища больших двоичных объектов Azure (объект хранилища) из Python | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="c8c0a-103">Как toouse хранилища больших двоичных объектов Azure с Python</span><span class="sxs-lookup"><span data-stu-id="c8c0a-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="c8c0a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c8c0a-104">Overview</span></span>
<span data-ttu-id="c8c0a-105">Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="c8c0a-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="c8c0a-107">Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="c8c0a-108">В этой статье будет показано, как tooperform распространенные сценарии использования хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="c8c0a-109">Hello примеры написаны на Python и использовать hello [пакет SDK хранилища Microsoft Azure для Python].</span><span class="sxs-lookup"><span data-stu-id="c8c0a-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="c8c0a-110">Hello сценарии включают отправки, список, загрузка и удаление больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="c8c0a-111">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="c8c0a-111">Create a container</span></span>
<span data-ttu-id="c8c0a-112">Исходя из большого двоичного объекта типа hello хотелось бы toouse, создайте **BlockBlobService**, **AppendBlobService**, или **PageBlobService** объекта.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="c8c0a-113">Hello следующий код использует **BlockBlobService** объекта.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="c8c0a-114">Добавьте следующее hello верхней hello любого файла Python, в котором вы хотите tooprogrammatically доступа Azure блочное хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="c8c0a-115">Hello следующий код создает **BlockBlobService** объекта с помощью hello ключ учетной записи хранения имени и учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="c8c0a-116">Замените myaccount и mykey фактическими значениями имени и ключа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="c8c0a-117">В следующем примере кода hello, можно использовать **BlockBlobService** hello контейнера объекта toocreate, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="c8c0a-118">По умолчанию hello новый контейнер является закрытым, поэтому необходимо указать ключи доступа к хранилищу (как это было сделано ранее) toodownload большие двоичные объекты из этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="c8c0a-119">Следует toomake hello BLOB-объектов в доступных tooeveryone hello контейнера можно создать контейнер hello и передать hello уровень общего доступа, с помощью hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="c8c0a-120">Кроме того можно изменить контейнер после создания его с помощью hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="c8c0a-121">После этого изменения всем пользователям в Интернете hello можно увидеть в открытый контейнер BLOB-объектов, но только можно изменить или удалить их.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="c8c0a-122">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="c8c0a-122">Upload a blob into a container</span></span>
<span data-ttu-id="c8c0a-123">toocreate большого двоичного объекта и передачи данных, используйте hello **создания\_большого двоичного объекта\_из\_путь**, **создать\_большого двоичного объекта\_из\_поток**, **создания\_большого двоичного объекта\_из\_байт** или **создания\_большого двоичного объекта\_из\_текста** методы.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="c8c0a-124">Они являются высокого уровня методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="c8c0a-125">**Создание\_большого двоичного объекта\_из\_путь** передач hello содержимое файла из указанного пути hello, и **создать\_больших двоичных объектов\_из\_поток** передачи hello содержимое из уже открытого файла или потока.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="c8c0a-126">**Создание\_большого двоичного объекта\_из\_байт** передает массив байтов, и **создания\_большого двоичного объекта\_из\_текст** передает указанный hello текстовое значение, с помощью hello указан кодирования (по умолчанию tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="c8c0a-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="c8c0a-127">Hello следующий пример отправляет содержимое hello hello **sunset.png** файла в hello **«myblob»** больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="c8c0a-128">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="c8c0a-128">List hello blobs in a container</span></span>
<span data-ttu-id="c8c0a-129">toolist hello BLOB-объектов в контейнере, используйте hello **списка\_большие двоичные объекты** метод.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="c8c0a-130">Этот метод возвращает генератор.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-130">This method returns a generator.</span></span> <span data-ttu-id="c8c0a-131">Hello следующий код выводит hello **имя** каждого BLOB-объекта в контейнер toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="c8c0a-132">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="c8c0a-132">Download blobs</span></span>
<span data-ttu-id="c8c0a-133">toodownload данные из большого двоичного объекта используйте **получить\_большого двоичного объекта\_для\_путь**, **получить\_большого двоичного объекта\_для\_поток**, **получить\_большого двоичного объекта\_для\_байт**, или **получить\_большого двоичного объекта\_для\_текст**.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="c8c0a-134">Они являются высокого уровня методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="c8c0a-135">Hello следующий пример демонстрирует использование **получить\_большого двоичного объекта\_для\_путь** toodownload содержимое hello hello **«myblob»** больших двоичных объектов и их сохранения toohello **out sunset.png** файла.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="c8c0a-136">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="c8c0a-136">Delete a blob</span></span>
<span data-ttu-id="c8c0a-137">Наконец, вызовите toodelete большой двоичный объект **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="c8c0a-138">Написание tooan append больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="c8c0a-138">Writing tooan append blob</span></span>
<span data-ttu-id="c8c0a-139">Добавочный большой двоичный объект оптимизирован для операций добавления, например ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="c8c0a-140">Как большой двоичный объект блока добавочный BLOB-объект состоит из блоков, но при добавлении нового большого двоичного объекта tooan append блок, это всегда присоединенных toohello конец hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="c8c0a-141">Вы не можете обновить или удалить существующий блок в добавочном большом двоичном объекте.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="c8c0a-142">Идентификаторы блокировок Hello для добавочный большой двоичный объект не отображаются, как и для большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="c8c0a-143">Каждый блок в добавочный большой двоичный объект может быть разный размер копии tooa более 4 Мбайт и добавочный большой двоичный объект может содержать не более 50 000 блоков.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="c8c0a-144">Максимальный размер Hello добавочный большой двоичный объект таким образом — немного более 195 ГБ (4 МБ X 50 000 блоков).</span><span class="sxs-lookup"><span data-stu-id="c8c0a-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="c8c0a-145">Hello приведенном ниже примере создается новый добавочный большой двоичный объект и добавляет tooit некоторых данных, имитируя операция простого ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="c8c0a-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8c0a-146">Next steps</span></span>
<span data-ttu-id="c8c0a-147">Теперь, когда вы узнали основы hello хранилища больших двоичных объектов, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="c8c0a-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="c8c0a-148">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="c8c0a-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="c8c0a-149">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c8c0a-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="c8c0a-150">[Блог рабочей группы службы хранилища Azure]</span><span class="sxs-lookup"><span data-stu-id="c8c0a-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="c8c0a-151">[пакет SDK хранилища Microsoft Azure для Python]</span><span class="sxs-lookup"><span data-stu-id="c8c0a-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Блог рабочей группы службы хранилища Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[пакет SDK хранилища Microsoft Azure для Python]: https://github.com/Azure/azure-storage-python
