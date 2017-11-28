---
title: "Разработка для хранилища файлов Azure с помощью Python | Документация Майкрософт"
description: "Узнайте, как разрабатывать приложения и службы Python, использующие хранилище файлов Azure для хранения данных файлов."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: a1a37266908277b54e7b42d85b9b4873af77e622
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="f6e8c-103">Разработка для хранилища файлов Azure с помощью Python</span><span class="sxs-lookup"><span data-stu-id="f6e8c-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="f6e8c-104">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="f6e8c-104">About this tutorial</span></span>
<span data-ttu-id="f6e8c-105">В этом руководстве мы рассмотрим основы использования Python для разработки приложений и служб, использующих хранилище файлов Azure для хранения данных файлов.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-105">This tutorial will demonstrate the basics of using Python to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="f6e8c-106">В рамках этого руководства мы создадим простое консольное приложение, а также покажем, как выполнять базовые действия с Python и хранилищем файлов Azure:</span><span class="sxs-lookup"><span data-stu-id="f6e8c-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="f6e8c-107">создание файловых ресурсов Azure;</span><span class="sxs-lookup"><span data-stu-id="f6e8c-107">Create Azure File shares</span></span>
* <span data-ttu-id="f6e8c-108">создание каталогов;</span><span class="sxs-lookup"><span data-stu-id="f6e8c-108">Create directories</span></span>
* <span data-ttu-id="f6e8c-109">перечисление файлов и каталогов в файловом ресурсе Azure;</span><span class="sxs-lookup"><span data-stu-id="f6e8c-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="f6e8c-110">передача, загрузка и удаление файла.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="f6e8c-111">Так как доступ к хранилищу файлов Azure можно получить с помощью SMB, можно написать простые приложения, которые получают доступ к файловому ресурсу Azure, используя стандартные классы и функции Python для ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Python I/O classes and functions.</span></span> <span data-ttu-id="f6e8c-112">Из этой статьи вы узнаете, как создавать приложения, использующие пакет SDK Python для службы хранилища Azure, который использует [REST API хранилища файлов Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) для взаимодействия с этим хранилищем.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-112">This article will describe how to write applications that use the Azure Storage Python SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

### <a name="set-up-your-application-to-use-azure-file-storage"></a><span data-ttu-id="f6e8c-113">Настройка приложения для работы с хранилищем файлов Azure</span><span class="sxs-lookup"><span data-stu-id="f6e8c-113">Set up your application to use Azure File storage</span></span>
<span data-ttu-id="f6e8c-114">Добавьте следующий код в начало любого исходного файла Python, из которого планируется получать доступ к хранилищу Azure программным способом:</span><span class="sxs-lookup"><span data-stu-id="f6e8c-114">Add the following near the top of any Python source file in which you wish to programmatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a><span data-ttu-id="f6e8c-115">Настройка подключения к хранилищу файлов Azure</span><span class="sxs-lookup"><span data-stu-id="f6e8c-115">Set up a connection to Azure File storage</span></span> 
<span data-ttu-id="f6e8c-116">Объект `FileService` позволяет работать с общими ресурсами, каталогами и файлами.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-116">The `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="f6e8c-117">Следующий код создает объект `FileService`, используя имя и ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-117">The following code creates a `FileService` object using the storage account name and account key.</span></span> <span data-ttu-id="f6e8c-118">Замените `<myaccount>` и `<mykey>` именем учетной записи и ключом.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="f6e8c-119">Создание файлового ресурса Azure</span><span class="sxs-lookup"><span data-stu-id="f6e8c-119">Create an Azure File share</span></span>
<span data-ttu-id="f6e8c-120">В следующем примере кода для создания общего ресурса (если он не существует) можно использовать объект `FileService`.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-120">In the following code example, you can use a `FileService` object to create the share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="f6e8c-121">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="f6e8c-121">Create a directory</span></span>
<span data-ttu-id="f6e8c-122">Вы также можете организовать хранилище, помещая файлы в подкаталоги вместо их размещения в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-122">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="f6e8c-123">Хранилище файлов Azure позволяет создать столько каталогов, сколько может позволить ваша учетная запись.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-123">Azure File storage allows you to create as many directories as your account will allow.</span></span> <span data-ttu-id="f6e8c-124">В следующем примере кода в корневом каталоге создается вложенный каталог с именем **sampledir** .</span><span class="sxs-lookup"><span data-stu-id="f6e8c-124">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="f6e8c-125">Перечисление файлов и каталогов в файловом ресурсе Azure</span><span class="sxs-lookup"><span data-stu-id="f6e8c-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="f6e8c-126">Чтобы получить список файлов и каталогов в общем ресурсе, используйте метод **list\_directories\_and\_files**.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-126">To list the files and directories in a share, use the **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="f6e8c-127">Этот метод возвращает генератор.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-127">This method returns a generator.</span></span> <span data-ttu-id="f6e8c-128">Приведенный далее код выводит в консоль **имя** каждого файла и каталога в общем ресурсе.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-128">The following code outputs the **name** of each file and directory in a share to the console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="f6e8c-129">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-129">Upload a file</span></span> 
<span data-ttu-id="f6e8c-130">Файловый ресурс Azure содержит по крайней мере корневой каталог, где могут размещаться файлы.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-130">Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="f6e8c-131">В этом разделе вы узнаете, как отправить файл из локального хранилища в корневой каталог общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-131">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="f6e8c-132">Для создания файла и передачи данных используйте методы `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` или `create_file_from_text`.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-132">To create a file and upload data, use the `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="f6e8c-133">Это высокоуровневые методы, которые выполняют необходимое фрагментирование данных, если их размер превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-133">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="f6e8c-134">Метод `create_file_from_path` передает содержимое файла из указанного пути, а метод `create_file_from_stream` передает содержимое уже открытого файла или потока.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-134">`create_file_from_path` uploads the contents of a file from the specified path, and `create_file_from_stream` uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="f6e8c-135">Метод `create_file_from_bytes` передает массив байтов, а `create_file_from_text` — указанное текстовое значение с использованием указанной кодировки (по умолчанию UTF-8).</span><span class="sxs-lookup"><span data-stu-id="f6e8c-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="f6e8c-136">В примере далее содержимое файла **sunset.png** передается в файл **myfile**.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-136">The following example uploads the contents of the **sunset.png** file into the **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="f6e8c-137">Скачивание файла</span><span class="sxs-lookup"><span data-stu-id="f6e8c-137">Download a file</span></span>
<span data-ttu-id="f6e8c-138">Чтобы загрузить данные из файла, используйте методы `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes` или `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-138">To download data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="f6e8c-139">Это высокоуровневые методы, которые выполняют необходимое фрагментирование данных, если их размер превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-139">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="f6e8c-140">В следующем примере показано использование метода `get_file_to_path` для загрузки содержимого файла **myfile** и его сохранения в файл **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-140">The following example demonstrates using `get_file_to_path` to download the contents of the **myfile** file and store it to the **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="f6e8c-141">Удаление файла</span><span class="sxs-lookup"><span data-stu-id="f6e8c-141">Delete a file</span></span>
<span data-ttu-id="f6e8c-142">Наконец, чтобы удалить файл, вызовите метод `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-142">Finally, to delete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="f6e8c-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6e8c-143">Next steps</span></span>
<span data-ttu-id="f6e8c-144">Теперь, когда вы узнали о работе с хранилищем файлов Azure с помощью Python, воспользуйтесь следующими ссылками для изучения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="f6e8c-144">Now that you've learned how to manipulate Azure File storage with Python, follow these links to learn more.</span></span>

* [<span data-ttu-id="f6e8c-145">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="f6e8c-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="f6e8c-146">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="f6e8c-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="f6e8c-147">пакет SDK для службы хранилища Microsoft Azure для Python</span><span class="sxs-lookup"><span data-stu-id="f6e8c-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)