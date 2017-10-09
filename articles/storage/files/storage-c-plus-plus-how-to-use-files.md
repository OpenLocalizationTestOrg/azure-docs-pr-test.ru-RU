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
ms.openlocfilehash: 48f668cf9359f88baeaaa08ee0d44e70bd0f5f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-c"></a>Разработка для хранилища файлов Azure на языке C++
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>О данном учебнике

В этом учебнике вы узнаете, как tooperform основные операции в хранилище файлов Azure. Через примеры на языке C++, вы узнаете, как toocreate общие папки и каталоги, передача, список и удалять файлы. Если используется новое хранилище файла tooAzure через понятия hello в последующих разделах hello пригодятся для понимания образцы hello.


* Создание и удаление общих папок Azure.
* Создание и удаление каталогов.
* Перечисление файлов и каталогов в файловом ресурсе Azure.
* Передача, загрузка и удаление файлов.
* Задание квоты hello (максимальный размер) для Azure общей папки
* Создание подписанного URL-адреса (ключ SAS) для файла, который использует политику общего доступа, определенные в общей папке hello.

> [!Note]  
> Поскольку хранилище файлов Azure может осуществляться по протоколу SMB, это возможно toowrite простые приложения, которые доступ к общему ресурсу hello файлов Azure, с помощью стандартных классов ввода-вывода C++ hello и функций. В этой статье описывается, как toowrite приложения, использующие hello SDK C++ хранилища Azure, которая использует hello [хранилища Azure File API-интерфейса REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure хранилища файлов.

## <a name="create-a-c-application"></a>Создание приложения на C++
образцы toobuild hello, необходимо будет hello tooinstall 2.4.0 клиентская библиотека хранилища Azure для C++. Вам также необходимо создать учетную запись хранилища Azure.

tooinstall hello Azure Storage Client 2.4.0 для C++, можно использовать один из следующих методов hello:

* **Linux —** выполните hello инструкциями, приведенными в hello [клиентская библиотека хранилища Azure для C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) страницы.
* **Windows.** В Visual Studio щелкните **Инструменты &gt; Диспетчер пакетов NuGet** Консоль диспетчера пакетов&gt;. Команда hello введите следующее в hello [консоль диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу **ввод**.
  
```
Install-Package wastorage
```

## <a name="set-up-your-application-toouse-azure-file-storage"></a>Настройка вашего приложения toouse хранилища Azure File
Добавьте следующие hello включать вверху исходный файл C++ hello место хранилища Azure File toomanipulate toohello инструкции:

```cpp
#include <was/storage_account.h>
#include <was/file.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Настройка строки подключения к хранилищу Azure
toouse хранения файлов необходима учетная запись хранилища Azure tooyour tooconnect. Hello первым шагом будет tooconfigure строку подключения, которая будет использоваться учетная запись хранения tooyour tooconnect. Определим статических переменных toodo.

```cpp
// Define hello connection-string with your values.
const utility::string_t 
storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

## <a name="connecting-tooan-azure-storage-account"></a>Учетной записи хранилища Azure tooan подключения
Можно использовать hello **cloud_storage_account** класса toorepresent сведений учетной записи хранилища. tooretrieve данные из строки подключения к хранилищу hello учетной записи хранилища, вы можете использовать hello **проанализировать** метод.

```cpp
// Retrieve storage account from connection string.    
azure::storage::cloud_storage_account storage_account = 
  azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="create-an-azure-file-share"></a>Создание файлового ресурса Azure
Все файлы и каталоги в хранилище файлов Azure размещаются в контейнере, который называется общей папкой (**Share**). Учетная запись хранения может иметь столько общих папок, насколько позволяет емкость вашей учетной записи. tooobtain доступа tooa общей папки и ее содержимое, необходимо toouse клиент хранилища файлов Azure.

```cpp
// Create hello Azure File storage client.
azure::storage::cloud_file_client file_client = 
  storage_account.create_cloud_file_client();
```

С помощью клиента хранилища Azure файл hello, это позволяет получить общую папку tooa ссылки.

```cpp
// Get a reference toohello file share
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));
```

hello toocreate общей папки, используйте hello **create_if_not_exists** метод hello **cloud_file_share** объекта.

```cpp
if (share.create_if_not_exists()) {    
    std::wcout << U("New share created") << std::endl;    
}
```

На этом этапе **совместное использование** содержит общую папку tooa ссылку с именем **Мои папки образца**.

## <a name="delete-an-azure-file-share"></a>Удаление общей папки Azure
Удаление общей папки выполняется путем вызова hello **delete_if_exists** метод на объекте cloud_file_share. Ниже приведен пример кода, который выполняет это действие.

```cpp
// Get a reference toohello share.
azure::storage::cloud_file_share share = 
  file_client.get_share_reference(_XPLATSTR("my-sample-share"));

// delete hello share if exists
share.delete_share_if_exists();
```

## <a name="create-a-directory"></a>Создайте каталог
Хранилище можно упорядочить путем помещения файлов в подкаталогах вместо их все в корневом каталоге hello. Хранилище файлов Azure позволяет toocreate как количество каталогов в вашей учетной записи будет разрешено. Приведенный ниже код Hello создаст каталог с именем **мой каталог образцов** в корневом каталоге hello, а также подкаталог **Мой образец подкаталог**.

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

## <a name="delete-a-directory"></a>Удаление каталога
Удаление каталога является простой задачей, однако следует отметить, что нельзя удалить каталог, по-прежнему содержащий файлы или другие каталоги.

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Перечисление файлов и каталогов в файловом ресурсе Azure
Получить список файлов и каталогов в общей папке довольно просто, вызвав метод **list_files_and_directorie** по ссылке **cloud_file_directory**. широкий набор свойств и методов для возвращенной hello tooaccess **list_file_and_directory_item**, необходимо вызвать hello **list_file_and_directory_item.as_file** tooget метод **cloud_ файл** объекта или hello **list_file_and_directory_item.as_directory** tooget метод **cloud_file_directory** объекта.

Hello, следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в корневом каталоге hello hello общей папки.

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

## <a name="upload-a-file"></a>Отправить файл.
В очень hello бы, Azure файловый ресурс содержит корневой каталог, где находятся файлы, можно. В этом разделе вы узнаете, как tooupload файла из локального хранилища на hello корневой каталог общего ресурса.

Первым шагом Hello в передаче файла является tooobtain каталог toohello ссылок, где он находится. Это делается путем вызова hello **get_root_directory_reference** метод hello объекта общей папки.

```cpp
//Get a reference toohello root directory for hello share.
azure::storage::cloud_file_directory root_dir = share.get_root_directory_reference();
```

Теперь, когда имеется ссылка toohello корневой каталог общего ресурса hello, можно отправить файл на него. В этом примере выполняется отправка из файла, текста и потока.

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

## <a name="download-a-file"></a>Скачивание файла
файлы toodownload сначала получить ссылку на файл, а затем вызвать hello **download_to_stream** метод tootransfer hello файл содержимое tooa поток объекта, которые могут затем сохраняться tooa локального файла. Кроме того, можно использовать hello **download_to_file** метод toodownload hello содержимое локального файла tooa файла. Можно использовать hello **download_text** метод toodownload hello содержимое файла в виде текстовой строки.

Hello следующий пример использует hello **download_to_stream** и **download_text** toodemonstrate методы загрузки hello файлы, которые были созданы в предыдущих разделах.

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

## <a name="delete-a-file"></a>Удаление файла
Следующая распространенная операция в хранилище файлов Azure — это удаление файлов. Hello следующий код удаляет файл с именем my пример файл-3 хранятся в корневом каталоге hello.

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

## <a name="set-hello-quota-maximum-size-for-an-azure-file-share"></a>Задание квоты hello (максимальный размер) для Azure общей папки
Можно установить квоты hello (или максимальный размер) для общей папки, в гигабайтах. Можно также проверить, какой объем данных в настоящее время хранится в папке hello toosee.

В параметр квоты hello для общей папки можно ограничить общий размер hello hello файлы, хранящиеся в папке hello. Если общий размер файлов в общей папке hello hello превышает квоту hello задать для общей папки hello, а затем клиентов будет невозможно tooincrease hello размера существующих файлов или создания новых файлов, если эти файлы являются пустыми.

Hello приведенном ниже примере показано, как toocheck hello текущего использования для общей папки и как tooset hello квоты для общей папки hello.

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

## <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Создание подписи общего доступа для файла или файлового ресурса
Для файлового ресурса или отдельного файла можно создать подписанный URL-адрес (SAS). Можно также создать политики общего доступа на общих toomanage общий доступ к файлам подписи. Создание политики общего доступа рекомендуется, так как она предоставляет средства отзыва hello SAS, если он должен быть скомпрометирован.

Следующий пример Hello создает политику общего доступа в общей папке, а затем использует ограничения hello tooprovide политика для SAS для файла в hello совместного использования.

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
## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о хранилище Azure, изучение этих ресурсов.

* [Клиентская библиотека хранилища для C++](https://github.com/Azure/azure-storage-cpp)
* [Примеры для службы хранилища файлов Azure на языке C++] (https://github.com/Azure-Samples/storage-file-cpp-getting-started)
* [Azure Storage Explorer;](http://go.microsoft.com/fwlink/?LinkID=822673&clcid=0x409)
* [Документация по хранилищу Azure](https://azure.microsoft.com/documentation/services/storage/)