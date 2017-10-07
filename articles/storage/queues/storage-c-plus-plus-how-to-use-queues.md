---
title: "хранилище очередей toouse aaaHow (C++) | Документы Microsoft"
description: "Узнайте, как toouse hello службы хранилища очередей в Azure. Примеры написаны на C++."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: b0cddf017878e9fab87f47d24b2906e40c9f4ad5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a>Как toouse хранилища очередей из C++
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Обзор
В этом руководстве будет показано, как с помощью распространенных сценариев tooperform hello службы хранилища очередей Azure. Примеры Hello на языке C++ и использовать hello [клиентская библиотека хранилища Azure для C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание и удаление очередей**.

> [!NOTE]
> Это руководство по цели hello клиентская библиотека хранилища Azure для C++ версии 1.0.0 и более поздних версий. Hello рекомендуемое версии клиентской библиотеки хранилища 2.2.0, которая доступна через [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Создание приложения на C++
В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях C++.

toodo таким образом, вам потребуется tooinstall hello клиентская библиотека хранилища Azure для C++ и создать учетную запись хранилища Azure в подписке Azure.

hello tooinstall клиентская библиотека хранилища Azure для C++, можно использовать следующие методы hello:

* **Linux —** выполните hello инструкциями, приведенными в hello [клиентская библиотека хранилища Azure для C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) страницы.
* **Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**. Команда hello введите следующее в hello [консоль диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу **ввод**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Настройка вашего приложения tooaccess хранилища очередей
Добавьте следующие hello включать инструкции toohello вверху файла C++ hello место toouse hello Azure API-интерфейсы tooaccess очереди хранилища:  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Настройка строки подключения к хранилищу Azure
Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления. При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, с помощью hello имя учетной записи и hello хранилища ключи доступа к хранилищу для учетной записи хранения hello, перечисленные в hello [портала Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения. Сведения об учетных записях хранения и ключах доступа см. в статье[Об учетных записях хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json). В этом примере показано, как объявить строки подключения hello toohold статического поля:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest приложения на локальном компьютере Windows, можно использовать hello Microsoft Azure [эмулятор хранилища](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) , установленная с hello [пакета Azure SDK](https://azure.microsoft.com/downloads/). Эмулятор хранилища Hello — это программа, которая имитирует hello больших двоичных объектов, очередей и таблиц служб, доступных в Azure на локальном компьютере разработчика. Hello следующем примере показано, как объявить статическое поле toohold hello соединения строки tooyour эмулятора локального хранилища:  

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

## <a name="how-to-create-a-queue"></a>Практическое руководство. Создание очереди
Объект **cloud_queue_client** позволяет получать ссылки на очереди. Hello следующий код создает **cloud_queue_client** объекта.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Используйте hello **cloud_queue_client** tooget требуется toouse очереди toohello ссылку объекта. Можно создать очередь hello, если он не существует.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Практическое руководство. Вставка сообщения в очередь
tooinsert сообщения в существующую очередь, сначала создайте **cloud_queue_message**. Затем вызовите hello **add_message** метод. Объект **cloud_queue_message** может быть создан из строки или массива **байтов**. Ниже приведен код (если он не существует), который создает очередь и вставок приветственное сообщение «Hello, World»:

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a>Как: Просмотр следующего сообщения hello
Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **peek_message** метод.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Способ: измените содержимое hello сообщение из очереди
Вы можете изменить содержимое сообщений на месте в очереди hello hello. Если сообщение hello представляет рабочей задачи, можно использовать этот компонент tooupdate hello состояние задачи рабочего hello. После кода Hello обновляется приветственное сообщение очереди новое содержимое и наборы hello tooextend время ожидания видимости другой 60 секунд. Сохраняет состояние работ, сопряженные с приветственное сообщение hello и предоставляет другой минуты toocontinue работа на приветственное сообщение клиента hello. Можно использовать этот рабочих процессов способ tootrack многоэтапной для очереди сообщений без необходимости toostart через от начала hello при неудачном завершении шага обработки из-за toohardware или ошибок программного обеспечения. Как правило будет хранить значение числа повторов и если приветственное сообщение повторяется более n раз, следует удалить его. Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a>Как: Отмена очередь следующего сообщения hello
Код удаляет сообщение из очереди в два этапа. При вызове **get_message**, вы получаете следующее сообщение hello в очереди. Сообщение, возвращенное из **get_message** становится невидимой tooany другой код, чтение сообщений из этой очереди. toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **delete_message**. Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку. Вызовы кода **delete_message** сразу после обработки сообщения hello.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Дополнительные параметры для удаления сообщений из очереди
Способ извлечения сообщения из очереди можно настроить двумя способами. Во-первых можно получить пакет сообщений (вверх too32). Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения. Hello следующий пример кода использует hello **get_messages** метод tooget 20 сообщений в одном вызове. Затем он обрабатывает каждое сообщение с помощью цикла **for** . Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения. Обратите внимание, что hello 5 минут запускается для всех сообщений в hello же время, поэтому после 5 минут с момента вызова hello слишком**get_messages**, все сообщения, которые не были удалены становятся видимыми.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a>Как: hello длина очереди получения
Можно получить оценку hello количество сообщений в очереди. Hello **download_attributes** метод запрашивает hello очереди службы tooretrieve атрибуты очереди hello, включая количество сообщений hello. Hello **approximate_message_count** метод возвращает hello приблизительное количество сообщений в очереди hello.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a>Практическое руководство. Удаление очереди
все сообщения hello и очереди, содержащиеся в нем, вызов hello toodelete **delete_queue_if_exists** метод hello объекта очереди.

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища очереди, выполните следующие дополнительные сведения о хранилище Azure toolearn ссылки.

* [Как toouse хранилища BLOB-объектов из C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Как toouse хранилище таблиц из C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Перечисление ресурсов хранилища Azure в C++](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Справочник по клиентской библиотеке хранилища для C++](http://azure.github.io/azure-storage-cpp)
* [Документация по хранилищу Azure](https://azure.microsoft.com/documentation/services/storage/)