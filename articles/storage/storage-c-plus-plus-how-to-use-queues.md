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
ms.openlocfilehash: 755380824890ad83774e14d258975915e10cfede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="e01fe-104">Как toouse хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="e01fe-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="e01fe-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="e01fe-105">Overview</span></span>
<span data-ttu-id="e01fe-106">В этом руководстве будет показано, как с помощью распространенных сценариев tooperform hello службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="e01fe-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="e01fe-107">Примеры Hello на языке C++ и использовать hello [клиентская библиотека хранилища Azure для C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="e01fe-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="e01fe-108">Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание и удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="e01fe-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="e01fe-109">Это руководство по цели hello клиентская библиотека хранилища Azure для C++ версии 1.0.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="e01fe-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="e01fe-110">Hello рекомендуемое версии клиентской библиотеки хранилища 2.2.0, которая доступна через [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="e01fe-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="e01fe-111">Создание приложения на C++</span><span class="sxs-lookup"><span data-stu-id="e01fe-111">Create a C++ application</span></span>
<span data-ttu-id="e01fe-112">В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях C++.</span><span class="sxs-lookup"><span data-stu-id="e01fe-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="e01fe-113">toodo таким образом, вам потребуется tooinstall hello клиентская библиотека хранилища Azure для C++ и создать учетную запись хранилища Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="e01fe-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="e01fe-114">hello tooinstall клиентская библиотека хранилища Azure для C++, можно использовать следующие методы hello:</span><span class="sxs-lookup"><span data-stu-id="e01fe-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="e01fe-115">**Linux —** выполните hello инструкциями, приведенными в hello [клиентская библиотека хранилища Azure для C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) страницы.</span><span class="sxs-lookup"><span data-stu-id="e01fe-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="e01fe-116">**Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="e01fe-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="e01fe-117">Команда hello введите следующее в hello [консоль диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="e01fe-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="e01fe-118">Настройка вашего приложения tooaccess хранилища очередей</span><span class="sxs-lookup"><span data-stu-id="e01fe-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="e01fe-119">Добавьте следующие hello включать инструкции toohello вверху файла C++ hello место toouse hello Azure API-интерфейсы tooaccess очереди хранилища:</span><span class="sxs-lookup"><span data-stu-id="e01fe-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="e01fe-120">Настройка строки подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="e01fe-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="e01fe-121">Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления.</span><span class="sxs-lookup"><span data-stu-id="e01fe-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="e01fe-122">При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, с помощью hello имя учетной записи и hello хранилища ключи доступа к хранилищу для учетной записи хранения hello, перечисленные в hello [портала Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения.</span><span class="sxs-lookup"><span data-stu-id="e01fe-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="e01fe-123">Сведения об учетных записях хранения и ключах доступа см. в статье[Об учетных записях хранения Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e01fe-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="e01fe-124">В этом примере показано, как объявить строки подключения hello toohold статического поля:</span><span class="sxs-lookup"><span data-stu-id="e01fe-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="e01fe-125">tootest приложения на локальном компьютере Windows, можно использовать hello Microsoft Azure [эмулятор хранилища](storage-use-emulator.md) , установленная с hello [пакета Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e01fe-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="e01fe-126">Эмулятор хранилища Hello — это программа, которая имитирует hello больших двоичных объектов, очередей и таблиц служб, доступных в Azure на локальном компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="e01fe-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="e01fe-127">Hello следующем примере показано, как объявить статическое поле toohold hello соединения строки tooyour эмулятора локального хранилища:</span><span class="sxs-lookup"><span data-stu-id="e01fe-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="e01fe-128">Эмулятор хранилища Azure hello toostart, выберите hello **запустить** или клавишу hello **Windows** ключа.</span><span class="sxs-lookup"><span data-stu-id="e01fe-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="e01fe-129">Начните вводить **эмулятор хранилища Azure**и выберите **эмулятор хранилища Microsoft Azure** hello списке приложений.</span><span class="sxs-lookup"><span data-stu-id="e01fe-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="e01fe-130">Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="e01fe-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="e01fe-131">Получить строку подключения</span><span class="sxs-lookup"><span data-stu-id="e01fe-131">Retrieve your connection string</span></span>
<span data-ttu-id="e01fe-132">Можно использовать hello **cloud_storage_account** класса toorepresent сведений учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="e01fe-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="e01fe-133">tooretrieve данные из строки подключения к хранилищу hello учетной записи хранилища, вы можете использовать hello **проанализировать** метод.</span><span class="sxs-lookup"><span data-stu-id="e01fe-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="e01fe-134">Практическое руководство. Создание очереди</span><span class="sxs-lookup"><span data-stu-id="e01fe-134">How to: Create a queue</span></span>
<span data-ttu-id="e01fe-135">Объект **cloud_queue_client** позволяет получать ссылки на очереди.</span><span class="sxs-lookup"><span data-stu-id="e01fe-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="e01fe-136">Hello следующий код создает **cloud_queue_client** объекта.</span><span class="sxs-lookup"><span data-stu-id="e01fe-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="e01fe-137">Используйте hello **cloud_queue_client** tooget требуется toouse очереди toohello ссылку объекта.</span><span class="sxs-lookup"><span data-stu-id="e01fe-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="e01fe-138">Можно создать очередь hello, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="e01fe-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="e01fe-139">Практическое руководство. Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="e01fe-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="e01fe-140">tooinsert сообщения в существующую очередь, сначала создайте **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="e01fe-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="e01fe-141">Затем вызовите hello **add_message** метод.</span><span class="sxs-lookup"><span data-stu-id="e01fe-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="e01fe-142">Объект **cloud_queue_message** может быть создан из строки или массива **байтов**.</span><span class="sxs-lookup"><span data-stu-id="e01fe-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="e01fe-143">Ниже приведен код (если он не существует), который создает очередь и вставок приветственное сообщение «Hello, World»:</span><span class="sxs-lookup"><span data-stu-id="e01fe-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

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

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="e01fe-144">Как: Просмотр следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="e01fe-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="e01fe-145">Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **peek_message** метод.</span><span class="sxs-lookup"><span data-stu-id="e01fe-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="e01fe-146">Способ: измените содержимое hello сообщение из очереди</span><span class="sxs-lookup"><span data-stu-id="e01fe-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="e01fe-147">Вы можете изменить содержимое сообщений на месте в очереди hello hello.</span><span class="sxs-lookup"><span data-stu-id="e01fe-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="e01fe-148">Если сообщение hello представляет рабочей задачи, можно использовать этот компонент tooupdate hello состояние задачи рабочего hello.</span><span class="sxs-lookup"><span data-stu-id="e01fe-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="e01fe-149">После кода Hello обновляется приветственное сообщение очереди новое содержимое и наборы hello tooextend время ожидания видимости другой 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="e01fe-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="e01fe-150">Сохраняет состояние работ, сопряженные с приветственное сообщение hello и предоставляет другой минуты toocontinue работа на приветственное сообщение клиента hello.</span><span class="sxs-lookup"><span data-stu-id="e01fe-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="e01fe-151">Можно использовать этот рабочих процессов способ tootrack многоэтапной для очереди сообщений без необходимости toostart через от начала hello при неудачном завершении шага обработки из-за toohardware или ошибок программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="e01fe-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="e01fe-152">Как правило будет хранить значение числа повторов и если приветственное сообщение повторяется более n раз, следует удалить его.</span><span class="sxs-lookup"><span data-stu-id="e01fe-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="e01fe-153">Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.</span><span class="sxs-lookup"><span data-stu-id="e01fe-153">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="e01fe-154">Как: Отмена очередь следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="e01fe-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="e01fe-155">Код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="e01fe-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="e01fe-156">При вызове **get_message**, вы получаете следующее сообщение hello в очереди.</span><span class="sxs-lookup"><span data-stu-id="e01fe-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="e01fe-157">Сообщение, возвращенное из **get_message** становится невидимой tooany другой код, чтение сообщений из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="e01fe-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="e01fe-158">toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="e01fe-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="e01fe-159">Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="e01fe-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="e01fe-160">Вызовы кода **delete_message** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="e01fe-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="e01fe-161">Дополнительные параметры для удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="e01fe-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="e01fe-162">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="e01fe-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="e01fe-163">Во-первых можно получить пакет сообщений (вверх too32).</span><span class="sxs-lookup"><span data-stu-id="e01fe-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="e01fe-164">Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="e01fe-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="e01fe-165">Hello следующий пример кода использует hello **get_messages** метод tooget 20 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="e01fe-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="e01fe-166">Затем он обрабатывает каждое сообщение с помощью цикла **for** .</span><span class="sxs-lookup"><span data-stu-id="e01fe-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="e01fe-167">Он также устанавливает минут toofive hello невидимости время ожидания для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="e01fe-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="e01fe-168">Обратите внимание, что hello 5 минут запускается для всех сообщений в hello же время, поэтому после 5 минут с момента вызова hello слишком**get_messages**, все сообщения, которые не были удалены становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="e01fe-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="e01fe-169">Как: hello длина очереди получения</span><span class="sxs-lookup"><span data-stu-id="e01fe-169">How to: Get hello queue length</span></span>
<span data-ttu-id="e01fe-170">Можно получить оценку hello количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="e01fe-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="e01fe-171">Hello **download_attributes** метод запрашивает hello очереди службы tooretrieve атрибуты очереди hello, включая количество сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="e01fe-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="e01fe-172">Hello **approximate_message_count** метод возвращает hello приблизительное количество сообщений в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="e01fe-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

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

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="e01fe-173">Практическое руководство. Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="e01fe-173">How to: Delete a queue</span></span>
<span data-ttu-id="e01fe-174">все сообщения hello и очереди, содержащиеся в нем, вызов hello toodelete **delete_queue_if_exists** метод hello объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="e01fe-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e01fe-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e01fe-175">Next steps</span></span>
<span data-ttu-id="e01fe-176">Теперь, когда вы узнали основы hello хранилища очереди, выполните следующие дополнительные сведения о хранилище Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="e01fe-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="e01fe-177">Как toouse хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="e01fe-177">How toouse Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="e01fe-178">Как toouse хранилище таблиц из C++</span><span class="sxs-lookup"><span data-stu-id="e01fe-178">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="e01fe-179">Перечисление ресурсов хранилища Azure в C++</span><span class="sxs-lookup"><span data-stu-id="e01fe-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="e01fe-180">Справочник по клиентской библиотеке хранилища для C++</span><span class="sxs-lookup"><span data-stu-id="e01fe-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="e01fe-181">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="e01fe-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)