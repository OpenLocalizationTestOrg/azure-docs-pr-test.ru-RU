---
title: "хранилище больших двоичных объектов toouse aaaHow (объект хранилища) из C++ | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 0d7e7436a109ef54fc07cc238c03cfc7cf2caac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a>Как toouse хранилища BLOB-объектов из C++
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор
Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.

В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы хранилища больших двоичных объектов. Примеры Hello на языке C++ и использовать hello [клиентская библиотека хранилища Azure для C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello сценарии включают **передачи**, **вывод**, **Загрузка**, и **удаление** больших двоичных объектов.  

> [!NOTE]
> Это руководство по цели hello клиентская библиотека хранилища Azure для C++ версии 1.0.0 и более поздних версий. Hello рекомендуемое версии клиентской библиотеки хранилища 2.2.0, которая доступна через [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Создание приложения на C++
В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях C++.  

toodo таким образом, вам потребуется tooinstall hello клиентская библиотека хранилища Azure для C++ и создать учетную запись хранилища Azure в подписке Azure.   

hello tooinstall клиентская библиотека хранилища Azure для C++, можно использовать следующие методы hello:

* **Linux —** выполните hello инструкциями, приведенными в hello [клиентская библиотека хранилища Azure для C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) страницы.  
* **Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**. Команда hello введите следующее в hello [консоль диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу **ввод**.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-blob-storage"></a>Настройка вашего приложения tooaccess хранилища больших двоичных объектов
Добавьте следующие hello включать инструкции toohello вверху файла C++ hello место toouse hello Azure API-интерфейсы tooaccess BLOB-объектов хранилища:  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a>Настройка строки подключения к службе хранилища Azure
Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления. При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, с помощью hello имя учетной записи и hello хранилища ключи доступа к хранилищу для учетной записи хранения hello, перечисленные в hello [портала Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения. Сведения об учетных записях хранения и ключах доступа см. в статье[Об учетных записях хранения Azure](storage-create-storage-account.md). В этом примере показано, как объявить строки подключения hello toohold статического поля:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest приложения на локальном компьютере Windows, можно использовать hello Microsoft Azure [эмулятор хранилища](storage-use-emulator.md) , установленная с hello [пакета Azure SDK](https://azure.microsoft.com/downloads/). Эмулятор хранилища Hello — это программа, которая имитирует hello больших двоичных объектов, очередей и таблиц служб, доступных в Azure на локальном компьютере разработчика. Hello следующем примере показано, как объявить статическое поле toohold hello соединения строки tooyour эмулятора локального хранилища:

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

Эмулятор хранилища Azure hello toostart, выберите hello **запустить** или клавишу hello **Windows** ключа. Начните вводить **эмулятор хранилища Azure**и выберите **эмулятор хранилища Microsoft Azure** hello списке приложений.  

Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.  

## <a name="retrieve-your-connection-string"></a>Получить строку подключения
Можно использовать hello **cloud_storage_account** класса toorepresent сведений учетной записи хранилища. tooretrieve данные из строки подключения к хранилищу hello учетной записи хранилища, вы можете использовать hello **проанализировать** метод.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Затем следует получить tooa ссылку **cloud_blob_client** класса позволяет tooretrieve объектов, представляющих контейнеры и большие двоичные объекты, хранящиеся в hello службы хранилища больших двоичных объектов. Hello следующий код создает **cloud_blob_client** объекта с помощью объекта учетной записи хранилища hello, мы получить выше:  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a>Практическое руководство. Создание контейнера
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

В этом примере показано, как toocreate контейнера, если он еще не существует:  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

По умолчанию hello новый контейнер является закрытым и необходимо указать хранилища доступа ключа toodownload BLOB-объектов из этого контейнера. Следует toomake hello файлов больших двоичных объектов в пределах доступных tooeveryone hello контейнера можно задать toobe контейнера hello общим с помощью hello, следующий код:  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

Всем пользователям в Интернете hello можно увидеть в открытый контейнер BLOB-объектов, но можно изменить или удалить их только в том случае, если у вас есть ключ hello соответствующие права доступа.  

## <a name="how-to-upload-a-blob-into-a-container"></a>Практическое руководство. Отправка BLOB-объекта в контейнер
Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты. В большинстве случаев hello блочного BLOB-объекта — hello, рекомендуется toouse типа.  

большой двоичный объект блока файла tooa tooupload получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект блока. Получив ссылку на большой двоичный объект можно передать любой поток данных tooit с вызывающему Привет **upload_from_stream** метод. Эта операция создаст hello большого двоичного объекта, если он не существует, или ранее перезаписать его, если он существует. Следующий пример показывает как Hello tooupload большого двоичного объекта в контейнер и предполагается hello контейнера уже был создан.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

Кроме того, можно использовать hello **upload_from_file** tooupload метод файл tooa большого двоичного объекта.

## <a name="how-to-list-hello-blobs-in-a-container"></a>Как: hello двоичные объекты перечислены в контейнер
toolist hello BLOB-объектов в контейнере, сначала нужно получить ссылку на контейнер. Затем можно использовать контейнер hello **list_blobs** метод tooretrieve hello BLOB-объектов и/или каталогов в ней. широкий набор свойств и методов для возвращенной hello tooaccess **list_blob_item**, необходимо вызвать hello **list_blob_item.as_blob** tooget метод **cloud_blob** объекта, или hello **list_blob.as_directory** tooget метод объекта cloud_blob_directory. Hello следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в hello **мой пример контейнера** контейнера:

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

Дополнительные сведения об операциях перечисления см. в разделе [Перечисление ресурсов хранилища Azure в C++](storage-c-plus-plus-enumeration.md).

## <a name="how-to-download-blobs"></a>Практическое руководство. Загрузка BLOB-объектов
toodownload больших двоичных объектов, сначала получить ссылку на большой двоичный объект, а затем вызвать hello **download_to_stream** метод. Hello следующий пример использует hello **download_to_stream** метод tootransfer hello blob содержимое tooa объекта потока могут затем сохраняться tooa локального файла.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

Кроме того, можно использовать hello **download_to_file** метод toodownload hello содержимое файла tooa большого двоичного объекта.
Кроме того, можно также использовать hello **download_text** метод toodownload hello содержимое большого двоичного объекта в виде строки текста.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a>Практическое руководство. Удаление BLOB-объектов
toodelete большого двоичного объекта сначала получить ссылку на большой двоичный объект, а затем вызвать hello **delete_blob** метода.  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища больших двоичных объектов, выполните следующие дополнительные сведения о хранилище Azure toolearn ссылки.  

* [Как toouse хранилища очередей из C++](storage-c-plus-plus-how-to-use-queues.md)
* [Как toouse хранилище таблиц из C++](storage-c-plus-plus-how-to-use-tables.md)
* [Перечисление ресурсов хранилища Azure в C++](storage-c-plus-plus-enumeration.md)
* [Справочник по клиентской библиотеке хранилища для C++](http://azure.github.io/azure-storage-cpp)
* [Документация по хранилищу Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Перенесите данные с помощью командной строки программу AzCopy hello](storage-use-azcopy.md)

