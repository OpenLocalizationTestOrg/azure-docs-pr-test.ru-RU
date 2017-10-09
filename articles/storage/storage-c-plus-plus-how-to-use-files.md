---
title: "aaaDevelop для хранилища Azure File с C++ | Документы Microsoft"
description: "Узнайте, как данные файлов toodevelop C++ приложений и служб, использующих toostore хранилище файлов Azure."
services: storage
documentationcenter: .net
author: renashahmsft
manager: aungoo
editor: tysonn
ms.assetid: a1e8c99e-47a6-43a9-9541-c9262eb00b38
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: renashahmsft
ms.openlocfilehash: 40c3aac94214a91121913e2ded315031aeed1c30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a><span data-ttu-id="581a8-103">Разработка для хранилища файлов Azure на языке C++</span><span class="sxs-lookup"><span data-stu-id="581a8-103">Develop for Azure File storage with C++</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="581a8-104">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="581a8-104">About this tutorial</span></span>

<span data-ttu-id="581a8-105">В этом учебнике вы узнаете, как tooperform основные операции в хранилище файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="581a8-105">In this tutorial, you'll learn how tooperform basic operations on Azure File storage.</span></span> <span data-ttu-id="581a8-106">Через примеры на языке C++, вы узнаете, как toocreate общие папки и каталоги, передача, список и удалять файлы.</span><span class="sxs-lookup"><span data-stu-id="581a8-106">Through samples written in C++, you'll learn how toocreate shares and directories, upload, list, and delete files.</span></span> <span data-ttu-id="581a8-107">Если используется новое хранилище файла tooAzure через понятия hello в последующих разделах hello пригодятся для понимания образцы hello.</span><span class="sxs-lookup"><span data-stu-id="581a8-107">If you are new tooAzure File storage , going through hello concepts in hello sections that follow will be helpful in understanding hello samples.</span></span>


* <span data-ttu-id="581a8-108">Создание и удаление общих папок Azure.</span><span class="sxs-lookup"><span data-stu-id="581a8-108">Create and delete Azure File shares</span></span>
* <span data-ttu-id="581a8-109">Создание и удаление каталогов.</span><span class="sxs-lookup"><span data-stu-id="581a8-109">Create and delete directories</span></span>
* <span data-ttu-id="581a8-110">Перечисление файлов и каталогов в файловом ресурсе Azure.</span><span class="sxs-lookup"><span data-stu-id="581a8-110">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="581a8-111">Передача, загрузка и удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="581a8-111">Upload, download, and delete a file</span></span>
* <span data-ttu-id="581a8-112">Задание квоты hello (максимальный размер) для Azure общей папки</span><span class="sxs-lookup"><span data-stu-id="581a8-112">Set hello quota (maximum size) for an Azure File share</span></span>
* <span data-ttu-id="581a8-113">Создание подписанного URL-адреса (ключ SAS) для файла, который использует политику общего доступа, определенные в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="581a8-113">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>

> [!Note]  
> <span data-ttu-id="581a8-114">Поскольку хранилище файлов Azure может осуществляться по протоколу SMB, это возможно toowrite простые приложения, которые доступ к общему ресурсу hello файлов Azure, с помощью стандартных классов ввода-вывода C++ hello и функций.</span><span class="sxs-lookup"><span data-stu-id="581a8-114">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard C++ I/O classes and functions.</span></span> <span data-ttu-id="581a8-115">В этой статье описывается, как toowrite приложения, использующие hello SDK C++ хранилища Azure, которая использует hello [хранилища Azure File API-интерфейса REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure хранилища файлов.</span><span class="sxs-lookup"><span data-stu-id="581a8-115">This article will describe how toowrite applications that use hello Azure Storage C++ SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-c-application"></a><span data-ttu-id="581a8-116">Создание приложения на C++</span><span class="sxs-lookup"><span data-stu-id="581a8-116">Create a C++ application</span></span>
<span data-ttu-id="581a8-117">образцы toobuild hello, необходимо будет hello tooinstall 2.4.0 клиентская библиотека хранилища Azure для C++.</span><span class="sxs-lookup"><span data-stu-id="581a8-117">toobuild hello samples, you will need tooinstall hello Azure Storage Client Library 2.4.0 for C++.</span></span> <span data-ttu-id="581a8-118">Вам также необходимо создать учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="581a8-118">You should also have created an Azure storage account.</span></span>

<span data-ttu-id="581a8-119">tooinstall hello Azure Storage Client 2.4.0 для C++, можно использовать один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="581a8-119">tooinstall hello Azure Storage Client 2.4.0 for C++, you can use one of hello following methods:</span></span>

* <span data-ttu-id="581a8-120">**Linux —** выполните hello инструкциями, приведенными в hello [клиентская библиотека хранилища Azure для C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) страницы.</span><span class="sxs-lookup"><span data-stu-id="581a8-120">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="581a8-121">**Windows.** В Visual Studio щелкните **Инструменты &gt; Диспетчер пакетов NuGet** Консоль диспетчера пакетов&gt;.</span><span class="sxs-lookup"><span data-stu-id="581a8-121">**Windows:** In Visual Studio, click **Tools &gt; NuGet Package Manager &gt; Package Manager Console**.</span></span> <span data-ttu-id="581a8-122">Команда hello введите следующее в hello [консоль диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="581a8-122">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a><span data-ttu-id="581a8-123">Настройка вашего приложения toouse хранилища Azure File</span><span class="sxs-lookup"><span data-stu-id="581a8-123">Set up your application toouse Azure File storage</span></span>
<span data-ttu-id="581a8-124">Добавьте следующие hello включать вверху исходный файл C++ hello место хранилища Azure File toomanipulate toohello инструкции:</span><span class="sxs-lookup"><span data-stu-id="581a8-124">Add hello following include statements toohello top of hello C++ source file where you want toomanipulate Azure File storage:</span></span>

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="581a8-125">Настройка строки подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="581a8-125">Set up an Azure storage connection string</span></span>
<span data-ttu-id="581a8-126">toouse хранения файлов необходима учетная запись хранилища Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="581a8-126">toouse File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="581a8-127">Hello первым шагом будет tooconfigure строку подключения, которая будет использоваться учетная запись хранения tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="581a8-127">hello first step would be tooconfigure a connection string, which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="581a8-128">Определим статических переменных toodo.</span><span class="sxs-lookup"><span data-stu-id="581a8-128">Let's define a static variable toodo that.</span></span>

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="581a8-129">Учетной записи хранилища Azure tooan подключения</span><span class="sxs-lookup"><span data-stu-id="581a8-129">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="581a8-130">Можно использовать hello **cloud_storage_account** класса toorepresent сведений учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="581a8-130">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="581a8-131">tooretrieve данные из строки подключения к хранилищу hello учетной записи хранилища, вы можете использовать hello **проанализировать** метод.</span><span class="sxs-lookup"><span data-stu-id="581a8-131">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a><span data-ttu-id="581a8-132">Создание файлового ресурса Azure</span><span class="sxs-lookup"><span data-stu-id="581a8-132">Create an Azure File share</span></span>
<span data-ttu-id="581a8-133">Все файлы и каталоги в хранилище файлов Azure размещаются в контейнере, который называется общей папкой (**Share**).</span><span class="sxs-lookup"><span data-stu-id="581a8-133">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="581a8-134">Учетная запись хранения может иметь столько общих папок, насколько позволяет емкость вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="581a8-134">Your storage account can have as many shares as your account capacity allows.</span></span> <span data-ttu-id="581a8-135">tooobtain доступа tooa общей папки и ее содержимое, необходимо toouse клиент хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="581a8-135">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

<span data-ttu-id="581a8-136">С помощью клиента хранилища Azure файл hello, это позволяет получить общую папку tooa ссылки.</span><span class="sxs-lookup"><span data-stu-id="581a8-136">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

<span data-ttu-id="581a8-137">hello toocreate общей папки, используйте hello **create_if_not_exists** метод hello **cloud_file_share** объекта.</span><span class="sxs-lookup"><span data-stu-id="581a8-137">toocreate hello share, use hello **create_if_not_exists** method of hello **cloud_file_share** object.</span></span>

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

<span data-ttu-id="581a8-138">На этом этапе **совместное использование** содержит общую папку tooa ссылку с именем **Мои папки образца**.</span><span class="sxs-lookup"><span data-stu-id="581a8-138">At this point, **share** holds a reference tooa share named **my-sample-share**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="581a8-139">Удаление общей папки Azure</span><span class="sxs-lookup"><span data-stu-id="581a8-139">Delete an Azure File share</span></span>
<span data-ttu-id="581a8-140">Удаление общей папки выполняется путем вызова hello **delete_if_exists** метод на объекте cloud_file_share.</span><span class="sxs-lookup"><span data-stu-id="581a8-140">Deleting a share is done by calling hello **delete_if_exists** method on a cloud_file_share object.</span></span> <span data-ttu-id="581a8-141">Ниже приведен пример кода, который выполняет это действие.</span><span class="sxs-lookup"><span data-stu-id="581a8-141">Here's sample code that does that.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a><span data-ttu-id="581a8-142">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="581a8-142">Create a directory</span></span>
<span data-ttu-id="581a8-143">Хранилище можно упорядочить путем помещения файлов в подкаталогах вместо их все в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="581a8-143">You can organize storage by putting files inside subdirectories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="581a8-144">Хранилище файлов Azure позволяет toocreate как количество каталогов в вашей учетной записи будет разрешено.</span><span class="sxs-lookup"><span data-stu-id="581a8-144">Azure File storage allows you toocreate as many directories as your account will allow.</span></span> <span data-ttu-id="581a8-145">Приведенный ниже код Hello создаст каталог с именем **мой каталог образцов** в корневом каталоге hello, а также подкаталог **Мой образец подкаталог**.</span><span class="sxs-lookup"><span data-stu-id="581a8-145">hello code below will create a directory named **my-sample-directory** under hello root directory as well as a subdirectory named **my-sample-subdirectory**.</span></span>

```cpp
// Retrieve a reference tooa directory
azure::storage::cloud_file_directory directory = share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Return value is true if hello share did not exist and was successfully created.
directory.create_if_not_exists();

// Create a subdirectory.
azure::storage::cloud_file_directory subdirectory = 
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));
subdirectory.create_if_not_exists();
```

## <a name="delete-a-directory"></a><span data-ttu-id="581a8-146">Удаление каталога</span><span class="sxs-lookup"><span data-stu-id="581a8-146">Delete a directory</span></span>
<span data-ttu-id="581a8-147">Удаление каталога является простой задачей, однако следует отметить, что нельзя удалить каталог, по-прежнему содержащий файлы или другие каталоги.</span><span class="sxs-lookup"><span data-stu-id="581a8-147">Deleting a directory is a simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// Get a reference toohello directory.
azure::storage::cloud_file_directory directory = 
  share.get_directory_reference(_XPLATSTR("my-sample-directory"));

// Get a reference toohello subdirectory you want toodelete.
azure::storage::cloud_file_directory sub_directory =
  directory.get_subdirectory_reference(_XPLATSTR("my-sample-subdirectory"));

// Delete hello subdirectory and hello sample directory.
sub_directory.delete_directory_if_exists();

directory.delete_directory_if_exists();
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="581a8-148">Перечисление файлов и каталогов в файловом ресурсе Azure</span><span class="sxs-lookup"><span data-stu-id="581a8-148">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="581a8-149">Получить список файлов и каталогов в общей папке довольно просто, вызвав метод **list_files_and_directorie** по ссылке **cloud_file_directory**.</span><span class="sxs-lookup"><span data-stu-id="581a8-149">Obtaining a list of files and directories within a share is easily done by calling **list_files_and_directories** on a **cloud_file_directory** reference.</span></span> <span data-ttu-id="581a8-150">широкий набор свойств и методов для возвращенной hello tooaccess **list_file_and_directory_item**, необходимо вызвать hello **list_file_and_directory_item.as_file** tooget метод **cloud_ файл** объекта или hello **list_file_and_directory_item.as_directory** tooget метод **cloud_file_directory** объекта.</span><span class="sxs-lookup"><span data-stu-id="581a8-150">tooaccess hello rich set of properties and methods for a returned **list_file_and_directory_item**, you must call hello **list_file_and_directory_item.as_file** method tooget a **cloud_file** object, or hello **list_file_and_directory_item.as_directory** method tooget a **cloud_file_directory** object.</span></span>

<span data-ttu-id="581a8-151">Hello, следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в корневом каталоге hello hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="581a8-151">hello following code demonstrates how tooretrieve and output hello URI of each item in hello root directory of hello share.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

// Output URI of each item.
azure::storage::list_file_and_diretory_result_iterator end_of_results;

for (auto it = directory.list_files_and_directories(); it != end_of_results; ++it)
{
    if(it->is_directory())
    {
        ucout << "Directory: " << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
    else if (it->is_file())
    {
        ucout << "File: " << it->as_file().uri().primary_uri().to_string() << std::endl;
    }        
}
```

## <a name="upload-a-file"></a><span data-ttu-id="581a8-152">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="581a8-152">Upload a file</span></span>
<span data-ttu-id="581a8-153">В очень hello бы, Azure файловый ресурс содержит корневой каталог, где находятся файлы, можно.</span><span class="sxs-lookup"><span data-stu-id="581a8-153">At hello very least, an Azure File share contains a root directory where files can reside.</span></span> <span data-ttu-id="581a8-154">В этом разделе вы узнаете, как tooupload файла из локального хранилища на hello корневой каталог общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="581a8-154">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="581a8-155">Первым шагом Hello в передаче файла является tooobtain каталог toohello ссылок, где он находится.</span><span class="sxs-lookup"><span data-stu-id="581a8-155">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="581a8-156">Это делается путем вызова hello **get_root_directory_reference** метод hello объекта общей папки.</span><span class="sxs-lookup"><span data-stu-id="581a8-156">You do this by calling hello **get_root_directory_reference** method of hello share object.</span></span>

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

<span data-ttu-id="581a8-157">Теперь, когда имеется ссылка toohello корневой каталог общего ресурса hello, можно отправить файл на него.</span><span class="sxs-lookup"><span data-stu-id="581a8-157">Now that you have a reference toohello root directory of hello share, you can upload a file onto it.</span></span> <span data-ttu-id="581a8-158">В этом примере выполняется отправка из файла, текста и потока.</span><span class="sxs-lookup"><span data-stu-id="581a8-158">This example uploads from a file, from text, and from a stream.</span></span>

```cpp
// Upload a file from a stream.
concurrency::streams::istream input_stream = 
  concurrency::streams::file_stream<uint8_t>::open_istream(_XPLATSTR("DataFile.txt")).get();

azure::storage::cloud_file file1 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));
file1.upload_from_stream(input_stream);

// Upload some files from text.
azure::storage::cloud_file file2 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
file2.upload_text(_XPLATSTR("more text"));

// Upload a file from a file.
azure::storage::cloud_file file4 = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));
file4.upload_from_file(_XPLATSTR("DataFile.txt"));    
```

## <a name="download-a-file"></a><span data-ttu-id="581a8-159">Скачивание файла</span><span class="sxs-lookup"><span data-stu-id="581a8-159">Download a file</span></span>
<span data-ttu-id="581a8-160">файлы toodownload сначала получить ссылку на файл, а затем вызвать hello **download_to_stream** метод tootransfer hello файл содержимое tooa поток объекта, которые могут затем сохраняться tooa локального файла.</span><span class="sxs-lookup"><span data-stu-id="581a8-160">toodownload files, first retrieve a file reference and then call hello **download_to_stream** method tootransfer hello file contents tooa stream object, which you can then persist tooa local file.</span></span> <span data-ttu-id="581a8-161">Кроме того, можно использовать hello **download_to_file** метод toodownload hello содержимое локального файла tooa файла.</span><span class="sxs-lookup"><span data-stu-id="581a8-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a file tooa local file.</span></span> <span data-ttu-id="581a8-162">Можно использовать hello **download_text** метод toodownload hello содержимое файла в виде текстовой строки.</span><span class="sxs-lookup"><span data-stu-id="581a8-162">You can use hello **download_text** method toodownload hello contents of a file as a text string.</span></span>

<span data-ttu-id="581a8-163">Hello следующий пример использует hello **download_to_stream** и **download_text** toodemonstrate методы загрузки hello файлы, которые были созданы в предыдущих разделах.</span><span class="sxs-lookup"><span data-stu-id="581a8-163">hello following example uses hello **download_to_stream** and **download_text** methods toodemonstrate downloading hello files, which were created in previous sections.</span></span>

```cpp
// Download as text
azure::storage::cloud_file text_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-2"));
utility::string_t text = text_file.download_text();
ucout << "File Text: " << text << std::endl;

// Download as a stream.
azure::storage::cloud_file stream_file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
stream_file.download_to_stream(output_stream);
std::ofstream outfile("DownloadFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();
outfile.write((char *)&data[0], buffer.size());
outfile.close();
```

## <a name="delete-a-file"></a><span data-ttu-id="581a8-164">Удаление файла</span><span class="sxs-lookup"><span data-stu-id="581a8-164">Delete a file</span></span>
<span data-ttu-id="581a8-165">Следующая распространенная операция в хранилище файлов Azure — это удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="581a8-165">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="581a8-166">Hello следующий код удаляет файл с именем my пример файл-3 хранятся в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="581a8-166">hello following code deletes a file named my-sample-file-3 stored under hello root directory.</span></span>

```cpp
// Get a reference toohello root directory for hello share.    
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

azure::storage::cloud_file_directory root_dir = 
  share.get_root_directory_reference();

azure::storage::cloud_file file = 
  root_dir.get_file_reference(_XPLATSTR("my-sample-file-3"));

file.delete_file_if_exists();
```

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a><span data-ttu-id="581a8-167">Задание квоты hello (максимальный размер) для Azure общей папки</span><span class="sxs-lookup"><span data-stu-id="581a8-167">Set hello quota (maximum size) for an Azure File share</span></span>
<span data-ttu-id="581a8-168">Можно установить квоты hello (или максимальный размер) для общей папки, в гигабайтах.</span><span class="sxs-lookup"><span data-stu-id="581a8-168">You can set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="581a8-169">Можно также проверить, какой объем данных в настоящее время хранится в папке hello toosee.</span><span class="sxs-lookup"><span data-stu-id="581a8-169">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="581a8-170">В параметр квоты hello для общей папки можно ограничить общий размер hello hello файлы, хранящиеся в папке hello.</span><span class="sxs-lookup"><span data-stu-id="581a8-170">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="581a8-171">Если общий размер файлов в общей папке hello hello превышает квоту hello задать для общей папки hello, а затем клиентов будет невозможно tooincrease hello размера существующих файлов или создания новых файлов, если эти файлы являются пустыми.</span><span class="sxs-lookup"><span data-stu-id="581a8-171">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="581a8-172">Hello приведенном ниже примере показано, как toocheck hello текущего использования для общей папки и как tooset hello квоты для общей папки hello.</span><span class="sxs-lookup"><span data-stu-id="581a8-172">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
if (share.exists())
{
    std::cout << "Current share usage: " << share.download_share_usage() << "/" << share.properties().quota();

    //This line sets hello quota too2560GB
    share.resize(2560);

    std::cout << "Quota increased: " << share.download_share_usage() << "/" << share.properties().quota();

}
```

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="581a8-173">Создание подписи общего доступа для файла или файлового ресурса</span><span class="sxs-lookup"><span data-stu-id="581a8-173">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="581a8-174">Для файлового ресурса или отдельного файла можно создать подписанный URL-адрес (SAS).</span><span class="sxs-lookup"><span data-stu-id="581a8-174">You can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="581a8-175">Можно также создать политики общего доступа на общих toomanage общий доступ к файлам подписи.</span><span class="sxs-lookup"><span data-stu-id="581a8-175">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="581a8-176">Создание политики общего доступа рекомендуется, так как она предоставляет средства отзыва hello SAS, если он должен быть скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="581a8-176">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="581a8-177">Следующий пример Hello создает политику общего доступа в общей папке, а затем использует ограничения hello tooprovide политика для SAS для файла в hello совместного использования.</span><span class="sxs-lookup"><span data-stu-id="581a8-177">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```cpp
// Parse hello connection string for hello storage account.
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello file client and get a reference toohello share
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();

azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

if (share.exists())
{
    // Create and assign a policy
    utility::string_t policy_name = _XPLATSTR("sampleSharePolicy");

    azure::storage::file_shared_access_policy sharedPolicy = 
      azure::storage::file_shared_access_policy();

    //set permissions tooexpire in 90 minutes
    sharedPolicy.set_expiry(utility::datetime::utc_now() + 
       utility::datetime::from_minutes(90));

    //give read and write permissions
    sharedPolicy.set_permissions(azure::storage::file_shared_access_policy::permissions::write | azure::storage::file_shared_access_policy::permissions::read);

    //set permissions for hello share
    azure::storage::file_share_permissions permissions;    

    //retrieve hello current list of shared access policies
    azure::storage::shared_access_policies<azure::storage::file_shared_access_policy> policies;

    //add hello new shared policy
    policies.insert(std::make_pair(policy_name, sharedPolicy));

    //save hello updated policy list
    permissions.set_policies(policies);
    share.upload_permissions(permissions);

    //Retrieve hello root directory and file references
    azure::storage::cloud_file_directory root_dir = 
        share.get_root_directory_reference();
    azure::storage::cloud_file file = 
      root_dir.get_file_reference(_XPLATSTR("my-sample-file-1"));

    // Generate a SAS for a file in hello share 
    //  and associate this access policy with it.        
    utility::string_t sas_token = file.get_shared_access_signature(sharedPolicy);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.        
    azure::storage::cloud_file file_with_sas(azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()));
    utility::string_t text = _XPLATSTR("My sample content");        
    file_with_sas.upload_text(text);        

    //Download and print URL with SAS.
    utility::string_t downloaded_text = file_with_sas.download_text();        
    ucout << downloaded_text << std::endl;        
    ucout << azure::storage::storage_credentials(sas_token).transform_uri(file.uri().primary_uri()).to_string() << std::endl;

}
```
## <a name="next-steps"></a><span data-ttu-id="581a8-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="581a8-178">Next steps</span></span>
<span data-ttu-id="581a8-179">toolearn Дополнительные сведения о хранилище Azure, изучение этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="581a8-179">toolearn more about Azure Storage, explore these resources:</span></span>

* [<span data-ttu-id="581a8-180">Клиентская библиотека хранилища для C++</span><span class="sxs-lookup"><span data-stu-id="581a8-180">Storage Client Library for C++</span></span>](https://github.com/Azure/azure-storage-cpp)
* <span data-ttu-id="581a8-181">[Примеры для службы хранилища файлов Azure на языке C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span><span class="sxs-lookup"><span data-stu-id="581a8-181">[Azure Storage File Service Samples in C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)</span></span>
* [<span data-ttu-id="581a8-182">Azure Storage Explorer;</span><span class="sxs-lookup"><span data-stu-id="581a8-182">Azure Storage Explorer</span></span>](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [<span data-ttu-id="581a8-183">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="581a8-183">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)