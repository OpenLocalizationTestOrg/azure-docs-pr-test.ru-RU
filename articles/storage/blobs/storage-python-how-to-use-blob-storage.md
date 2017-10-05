---
title: "Как использовать хранилище BLOB-объектов Azure (хранилище объектов) из Python | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
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
ms.openlocfilehash: 1cab8407be6fc8932b68e50d0c301e8ea37ea3ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="6b31b-103">Использование хранилища больших двоичных объектов Azure из Python</span><span class="sxs-lookup"><span data-stu-id="6b31b-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="6b31b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6b31b-104">Overview</span></span>
<span data-ttu-id="6b31b-105">Хранилище BLOB-объектов Azure — это служба, которая хранит неструктурированные данные в облаке в качестве объектов или больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="6b31b-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="6b31b-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="6b31b-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="6b31b-107">Хранилище BLOB-объектов иногда также называют хранилищем объектов.</span><span class="sxs-lookup"><span data-stu-id="6b31b-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="6b31b-108">В этой статье описано, как реализовать типичные сценарии с использованием хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="6b31b-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="6b31b-109">Примеры написаны на Python, и в них используется [пакет SDK для службы хранилища Microsoft Azure для Python].</span><span class="sxs-lookup"><span data-stu-id="6b31b-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="6b31b-110">Здесь описаны такие сценарии, как отправка, перечисление, скачивание и удаление больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="6b31b-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="6b31b-111">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="6b31b-111">Create a container</span></span>
<span data-ttu-id="6b31b-112">В зависимости от требуемого типа BLOB-объекта создайте объект **BlockBlobService**, **AppendBlobService** или **PageBlobService**.</span><span class="sxs-lookup"><span data-stu-id="6b31b-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="6b31b-113">В следующем коде используется объект **BlockBlobService** .</span><span class="sxs-lookup"><span data-stu-id="6b31b-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="6b31b-114">Добавьте следующий код в начало любого файла Python, из которого планируется получать программный доступ к хранилищу блочных BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6b31b-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="6b31b-115">Следующий код создает объект **BlockBlobService** , используя имя и ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6b31b-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="6b31b-116">Замените myaccount и mykey фактическими значениями имени и ключа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6b31b-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="6b31b-117">В следующем примере кода для создания контейнера (если он не существует) можно использовать объект **BlockBlobService** .</span><span class="sxs-lookup"><span data-stu-id="6b31b-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="6b31b-118">По умолчанию новый контейнер является закрытым, поэтому необходимо указать ключ доступа к хранилищу (как делалось раньше), чтобы скачать большие двоичные объекты из этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="6b31b-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="6b31b-119">Чтобы сделать большие двоичные объекты в этом контейнере доступными для всех пользователей, вы можете создать контейнер и предоставить открытый доступ, используя следующий код.</span><span class="sxs-lookup"><span data-stu-id="6b31b-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="6b31b-120">Либо можно изменить контейнер после его создания, используя следующий код.</span><span class="sxs-lookup"><span data-stu-id="6b31b-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="6b31b-121">После этого изменения любой пользователь в Интернете сможет видеть большие двоичные объекты в общедоступном контейнере, но изменить или удалить их сможете только вы.</span><span class="sxs-lookup"><span data-stu-id="6b31b-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6b31b-122">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="6b31b-122">Upload a blob into a container</span></span>
<span data-ttu-id="6b31b-123">Чтобы создать блочный BLOB-объект и передать данные, используйте метод **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** или **create\_blob\_from\_text**.</span><span class="sxs-lookup"><span data-stu-id="6b31b-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="6b31b-124">Это высокоуровневые методы, которые выполняют необходимое фрагментирование данных, если их размер превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="6b31b-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="6b31b-125">Метод **create\_blob\_from\_path** передает содержимое файла из указанного расположения, а метод **create\_blob\_from\_stream** передает содержимое уже открытого файла или потока.</span><span class="sxs-lookup"><span data-stu-id="6b31b-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="6b31b-126">Метод **create\_blob\_from\_bytes** передает массив байтов, а метод **create\_blob\_from\_text** передает заданное текстовое значение, используя указанную кодировку (по умолчанию — UTF-8).</span><span class="sxs-lookup"><span data-stu-id="6b31b-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="6b31b-127">В следующем примере содержимое файла **sunset.png** передается в BLOB-объект **myblob**.</span><span class="sxs-lookup"><span data-stu-id="6b31b-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="6b31b-128">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="6b31b-128">List the blobs in a container</span></span>
<span data-ttu-id="6b31b-129">Чтобы перечислить BLOB-объекты в контейнере, используйте метод **list\_blobs**.</span><span class="sxs-lookup"><span data-stu-id="6b31b-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="6b31b-130">Этот метод возвращает генератор.</span><span class="sxs-lookup"><span data-stu-id="6b31b-130">This method returns a generator.</span></span> <span data-ttu-id="6b31b-131">Следующий код выводит на консоль **имя** каждого большого двоичного объекта в контейнере.</span><span class="sxs-lookup"><span data-stu-id="6b31b-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="6b31b-132">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="6b31b-132">Download blobs</span></span>
<span data-ttu-id="6b31b-133">Чтобы скачать данные из BLOB-объекта, используйте **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes** или **get\_blob\_to\_text**.</span><span class="sxs-lookup"><span data-stu-id="6b31b-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="6b31b-134">Это высокоуровневые методы, которые выполняют необходимое фрагментирование данных, если их размер превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="6b31b-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="6b31b-135">В примере ниже показано использование метода **get\_blob\_to\_path** для скачивания содержимого большого двоичного объекта **myblob** и его сохранения в файл **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="6b31b-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="6b31b-136">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="6b31b-136">Delete a blob</span></span>
<span data-ttu-id="6b31b-137">Наконец, чтобы удалить BLOB-объект, вызовите **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="6b31b-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="6b31b-138">Запись в расширенный большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="6b31b-138">Writing to an append blob</span></span>
<span data-ttu-id="6b31b-139">Добавочный большой двоичный объект оптимизирован для операций добавления, например ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="6b31b-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="6b31b-140">Как и блочный BLOB-объект, добавочный большой двоичный объект состоит из блоков, но при добавлении нового блока в добавочный большой двоичный объект он всегда добавляется в конец этого объекта.</span><span class="sxs-lookup"><span data-stu-id="6b31b-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="6b31b-141">Вы не можете обновить или удалить существующий блок в добавочном большом двоичном объекте.</span><span class="sxs-lookup"><span data-stu-id="6b31b-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="6b31b-142">Идентификаторы блоков в добавочном большом двоичном объекте не отображаются, как в блочном BLOB-объекте.</span><span class="sxs-lookup"><span data-stu-id="6b31b-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="6b31b-143">Каждый блок в добавочном большом двоичном объекте может иметь разный размер (не более 4 МБ), кроме того, добавочный большой двоичный объект может содержать не более 50 000 блоков.</span><span class="sxs-lookup"><span data-stu-id="6b31b-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="6b31b-144">Таким образом, максимальный размер добавочного большого двоичного объекта немного превышает 195 ГБ (4 МБ X 50 000 блоков).</span><span class="sxs-lookup"><span data-stu-id="6b31b-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="6b31b-145">Приведенный ниже пример создает новый добавочный большой двоичный объект и добавляет в него некоторые данные, имитируя простые операции ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="6b31b-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="6b31b-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6b31b-146">Next steps</span></span>
<span data-ttu-id="6b31b-147">Вы ознакомились с базовыми понятиями о хранилище BLOB-объектов. Дополнительные сведения см. по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="6b31b-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="6b31b-148">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="6b31b-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="6b31b-149">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="6b31b-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="6b31b-150">[Блог рабочей группы службы хранилища Azure]</span><span class="sxs-lookup"><span data-stu-id="6b31b-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="6b31b-151">[пакет SDK для службы хранилища Microsoft Azure для Python]</span><span class="sxs-lookup"><span data-stu-id="6b31b-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Блог рабочей группы службы хранилища Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[пакет SDK для службы хранилища Microsoft Azure для Python]: https://github.com/Azure/azure-storage-python
