---
title: "aaaDevelop для хранилища Azure File с Python | Документы Microsoft"
description: "Узнайте, как данные файлов toodevelop Python приложений и служб, использующих toostore хранилище файлов Azure."
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
ms.openlocfilehash: 2adc5aac2765b98a8022ab1f706c1fcdbca1b43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a><span data-ttu-id="a9d06-103">Разработка для хранилища файлов Azure с помощью Python</span><span class="sxs-lookup"><span data-stu-id="a9d06-103">Develop for Azure File storage with Python</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="a9d06-104">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="a9d06-104">About this tutorial</span></span>
<span data-ttu-id="a9d06-105">Этот учебник продемонстрируют hello основы работы с Python toodevelop приложений или служб, которые используют данные файла toostore хранилище файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d06-105">This tutorial will demonstrate hello basics of using Python toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="a9d06-106">В этом учебнике мы создайте простое консольное приложение и Показать как tooperform базовые действия с хранилищем, Python и файлов Azure:</span><span class="sxs-lookup"><span data-stu-id="a9d06-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Python and Azure File storage:</span></span>

* <span data-ttu-id="a9d06-107">создание файловых ресурсов Azure;</span><span class="sxs-lookup"><span data-stu-id="a9d06-107">Create Azure File shares</span></span>
* <span data-ttu-id="a9d06-108">создание каталогов;</span><span class="sxs-lookup"><span data-stu-id="a9d06-108">Create directories</span></span>
* <span data-ttu-id="a9d06-109">перечисление файлов и каталогов в файловом ресурсе Azure;</span><span class="sxs-lookup"><span data-stu-id="a9d06-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="a9d06-110">Передача, загрузка и удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="a9d06-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="a9d06-111">Поскольку хранилище файлов Azure может осуществляться по протоколу SMB, вполне возможно toowrite простых приложений, получающих доступ к папке файлов Azure hello, с помощью стандартных классов ввода-вывода Python hello и функции.</span><span class="sxs-lookup"><span data-stu-id="a9d06-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Python I/O classes and functions.</span></span> <span data-ttu-id="a9d06-112">В этой статье описывается, как toowrite приложения, использующие hello SDK Python хранилища Azure, которая использует hello [хранилища Azure File API-интерфейса REST](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure хранилища файлов.</span><span class="sxs-lookup"><span data-stu-id="a9d06-112">This article will describe how toowrite applications that use hello Azure Storage Python SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

### <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="a9d06-113">Настройка вашего приложения toouse хранилища Azure File</span><span class="sxs-lookup"><span data-stu-id="a9d06-113">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="a9d06-114">Добавьте следующее hello вверху hello любой Python исходный файл, в котором вы хотите tooprogrammatically доступа хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a9d06-114">Add hello following near hello top of any Python source file in which you wish tooprogrammatically access Azure Storage.</span></span>

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a><span data-ttu-id="a9d06-115">Настройка подключения tooAzure хранения файлов</span><span class="sxs-lookup"><span data-stu-id="a9d06-115">Set up a connection tooAzure File storage</span></span> 
<span data-ttu-id="a9d06-116">Hello `FileService` объекта позволяет работать с общие папки, каталоги и файлы.</span><span class="sxs-lookup"><span data-stu-id="a9d06-116">hello `FileService` object lets you work with shares, directories and files.</span></span> <span data-ttu-id="a9d06-117">Hello следующий код создает `FileService` объекта с помощью hello ключ учетной записи хранения имени и учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a9d06-117">hello following code creates a `FileService` object using hello storage account name and account key.</span></span> <span data-ttu-id="a9d06-118">Замените `<myaccount>` и `<mykey>` именем учетной записи и ключом.</span><span class="sxs-lookup"><span data-stu-id="a9d06-118">Replace `<myaccount>` and `<mykey>` with your account name and key.</span></span>

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a><span data-ttu-id="a9d06-119">Создание файлового ресурса Azure</span><span class="sxs-lookup"><span data-stu-id="a9d06-119">Create an Azure File share</span></span>
<span data-ttu-id="a9d06-120">В следующем примере кода hello, можно использовать `FileService` объекта toocreate hello папки, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="a9d06-120">In hello following code example, you can use a `FileService` object toocreate hello share if it doesn't exist.</span></span>

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a><span data-ttu-id="a9d06-121">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="a9d06-121">Create a directory</span></span>
<span data-ttu-id="a9d06-122">Кроме того, можно организовать хранилища путем помещения файлов в подкаталоги вместо их все в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="a9d06-122">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="a9d06-123">Хранилище файлов Azure позволяет toocreate как количество каталогов в вашей учетной записи будет разрешено.</span><span class="sxs-lookup"><span data-stu-id="a9d06-123">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="a9d06-124">Приведенный ниже код Hello будет создавать вложенный каталог с именем **sampledir** в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="a9d06-124">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="a9d06-125">Перечисление файлов и каталогов в файловом ресурсе Azure</span><span class="sxs-lookup"><span data-stu-id="a9d06-125">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="a9d06-126">toolist hello файлы и каталоги в общей папке, используйте hello **списка\_каталогов\_и\_файлы** метод.</span><span class="sxs-lookup"><span data-stu-id="a9d06-126">toolist hello files and directories in a share, use hello **list\_directories\_and\_files** method.</span></span> <span data-ttu-id="a9d06-127">Этот метод возвращает генератор.</span><span class="sxs-lookup"><span data-stu-id="a9d06-127">This method returns a generator.</span></span> <span data-ttu-id="a9d06-128">Hello следующий код выводит hello **имя** всех файлов и каталогов в консоли toohello общей папки.</span><span class="sxs-lookup"><span data-stu-id="a9d06-128">hello following code outputs hello **name** of each file and directory in a share toohello console.</span></span>

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a><span data-ttu-id="a9d06-129">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="a9d06-129">Upload a file</span></span> 
<span data-ttu-id="a9d06-130">Общая папка содержит очень бы в hello Azure файл, корневой каталог, где находятся файлы, можно.</span><span class="sxs-lookup"><span data-stu-id="a9d06-130">Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="a9d06-131">В этом разделе вы узнаете, как tooupload файла из локального хранилища на hello корневой каталог общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="a9d06-131">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="a9d06-132">файл toocreate и передачи данных, используйте hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` или `create_file_from_text` методы.</span><span class="sxs-lookup"><span data-stu-id="a9d06-132">toocreate a file and upload data, use hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` or `create_file_from_text` methods.</span></span> <span data-ttu-id="a9d06-133">Они являются высокого уровня методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="a9d06-133">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="a9d06-134">`create_file_from_path`передачи hello содержимое файла из указанного пути hello, и `create_file_from_stream` передачи hello содержимое из уже открытого файла или потока.</span><span class="sxs-lookup"><span data-stu-id="a9d06-134">`create_file_from_path` uploads hello contents of a file from hello specified path, and `create_file_from_stream` uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="a9d06-135">`create_file_from_bytes`передает массив байтов, и `create_file_from_text` передачи hello указан с помощью hello текстовое значение кодировки (по умолчанию tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="a9d06-135">`create_file_from_bytes` uploads an array of bytes, and `create_file_from_text` uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="a9d06-136">Hello следующий пример отправляет содержимое hello hello **sunset.png** файла в hello **myfile** файла.</span><span class="sxs-lookup"><span data-stu-id="a9d06-136">hello following example uploads hello contents of hello **sunset.png** file into hello **myfile** file.</span></span>

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a><span data-ttu-id="a9d06-137">Скачивание файла</span><span class="sxs-lookup"><span data-stu-id="a9d06-137">Download a file</span></span>
<span data-ttu-id="a9d06-138">toodownload данных из файла, используйте `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, или `get_file_to_text`.</span><span class="sxs-lookup"><span data-stu-id="a9d06-138">toodownload data from a file, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, or `get_file_to_text`.</span></span> <span data-ttu-id="a9d06-139">Они являются высокого уровня методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.</span><span class="sxs-lookup"><span data-stu-id="a9d06-139">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="a9d06-140">Hello следующий пример демонстрирует использование `get_file_to_path` toodownload содержимое hello hello **myfile** файл и сохранить его toohello **out sunset.png** файла.</span><span class="sxs-lookup"><span data-stu-id="a9d06-140">hello following example demonstrates using `get_file_to_path` toodownload hello contents of hello **myfile** file and store it toohello **out-sunset.png** file.</span></span>

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a><span data-ttu-id="a9d06-141">Удаление файла</span><span class="sxs-lookup"><span data-stu-id="a9d06-141">Delete a file</span></span>
<span data-ttu-id="a9d06-142">Наконец, вызовите toodelete файл `delete_file`.</span><span class="sxs-lookup"><span data-stu-id="a9d06-142">Finally, toodelete a file, call `delete_file`.</span></span>

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a><span data-ttu-id="a9d06-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a9d06-143">Next steps</span></span>
<span data-ttu-id="a9d06-144">Теперь, когда вы узнали, как toomanipulate хранилища Azure File с Python, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="a9d06-144">Now that you've learned how toomanipulate Azure File storage with Python, follow these links toolearn more.</span></span>

* [<span data-ttu-id="a9d06-145">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="a9d06-145">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="a9d06-146">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a9d06-146">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* [<span data-ttu-id="a9d06-147">пакет SDK для службы хранилища Microsoft Azure для Python</span><span class="sxs-lookup"><span data-stu-id="a9d06-147">Microsoft Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)