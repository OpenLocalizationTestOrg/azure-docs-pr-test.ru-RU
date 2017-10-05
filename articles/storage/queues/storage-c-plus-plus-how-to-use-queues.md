---
title: "Использование хранилища очередей (C++) | Документация Майкрософт"
description: "Узнайте, как использовать службу хранилища очередей в Azure. Примеры написаны на C++."
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
ms.openlocfilehash: 5e81d5e0af9871099b7f921f355cf94249e4d30c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="1ac77-104">Использование хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="1ac77-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="1ac77-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="1ac77-105">Overview</span></span>
<span data-ttu-id="1ac77-106">В этом руководстве показано, как реализовать типичные сценарии с использованием службы хранения очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="1ac77-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="1ac77-107">Примеры написаны на C++ и используют [клиентскую библиотеку хранилища Azure для C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="1ac77-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="1ac77-108">Здесь описаны такие сценарии, как **вставка**, **просмотр**, **получение** и **удаление** сообщений очереди, а также **создание и удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="1ac77-109">Данное руководство предназначено для клиентской библиотеки хранилища Azure для С++ версии 1.0.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="1ac77-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="1ac77-110">Рекомендуемая версия клиентской библиотеки хранилища — 2.2.0. Она доступна на сайте [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="1ac77-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="1ac77-111">Создание приложения на C++</span><span class="sxs-lookup"><span data-stu-id="1ac77-111">Create a C++ application</span></span>
<span data-ttu-id="1ac77-112">В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях C++.</span><span class="sxs-lookup"><span data-stu-id="1ac77-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="1ac77-113">Для этого необходимо установить клиентскую библиотеку хранилища Azure для C++ и создать учетную запись хранения Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="1ac77-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="1ac77-114">Чтобы установить клиентскую библиотеку хранилища для C++, можно использовать следующие методы.</span><span class="sxs-lookup"><span data-stu-id="1ac77-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="1ac77-115">**Linux:** следуйте инструкциям, указанным в файле README [клиентской библиотеки хранилища Azure для C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="1ac77-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="1ac77-116">**Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="1ac77-117">Введите следующую команду в [консоли диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="1ac77-118">Настройка приложения для доступа к хранилищу очередей</span><span class="sxs-lookup"><span data-stu-id="1ac77-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="1ac77-119">Если нужно использовать API-интерфейсы Azure для доступа к очередям, добавьте следующие инструкции импорта в верхнюю часть файла C++.</span><span class="sxs-lookup"><span data-stu-id="1ac77-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="1ac77-120">Настройка строки подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="1ac77-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="1ac77-121">Клиент хранилища Azure использует строку подключения с целью хранения конечных точек и учетных данных для доступа к службам управления данными.</span><span class="sxs-lookup"><span data-stu-id="1ac77-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="1ac77-122">При запуске в клиентском приложении необходимо указать строку подключения для хранилища в следующем формате (в качестве параметров *AccountName* и *AccountKey* укажите имя и ключ доступа своей учетной записи хранения, их можно получить на [портале Azure](https://portal.azure.com)).</span><span class="sxs-lookup"><span data-stu-id="1ac77-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="1ac77-123">Сведения об учетных записях хранения и ключах доступа см. в статье[Об учетных записях хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1ac77-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="1ac77-124">В этом примере показано, как объявить статическое поле для размещения строки подключения:</span><span class="sxs-lookup"><span data-stu-id="1ac77-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="1ac77-125">Чтобы протестировать приложение на локальном компьютере Windows, можно использовать [эмулятор хранения](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) Microsoft Azure, установленный вместе с [пакетом SDK Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1ac77-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="1ac77-126">Эмулятор хранения — это программа, моделирующая службы больших двоичных объектов, очередей и таблиц, доступных в Azure на локальном компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="1ac77-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="1ac77-127">В следующем примере показано, как объявить статическое поле для размещения строки подключения для эмулятора локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="1ac77-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="1ac77-128">Чтобы запустить эмулятор хранения Azure, нажмите кнопку **Пуск** или клавишу **Windows**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="1ac77-129">Начните набирать **эмулятор хранения Azure** и выберите **эмулятор хранения Microsoft Azure** из списка приложений.</span><span class="sxs-lookup"><span data-stu-id="1ac77-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="1ac77-130">В приведенных ниже примерах предполагается, что вы использовали одно из этих двух определений для получения строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="1ac77-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="1ac77-131">Получить строку подключения</span><span class="sxs-lookup"><span data-stu-id="1ac77-131">Retrieve your connection string</span></span>
<span data-ttu-id="1ac77-132">Информацию о своей учетной записи хранения можно представить с помощью класса **cloud_storage_account**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="1ac77-133">Чтобы получить данные учетной записи хранения из строки подключения хранилища, можно использовать метод **синтаксического анализа** .</span><span class="sxs-lookup"><span data-stu-id="1ac77-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="1ac77-134">Практическое руководство. Создание очереди</span><span class="sxs-lookup"><span data-stu-id="1ac77-134">How to: Create a queue</span></span>
<span data-ttu-id="1ac77-135">Объект **cloud_queue_client** позволяет получать ссылки на очереди.</span><span class="sxs-lookup"><span data-stu-id="1ac77-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="1ac77-136">Следующий код создает объект **cloud_queue_client**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="1ac77-137">С помощью объекта **cloud_queue_client** получите ссылку на очередь, которую необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="1ac77-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="1ac77-138">Очередь можно создать, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="1ac77-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="1ac77-139">Практическое руководство. Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="1ac77-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="1ac77-140">Чтобы вставить сообщение в существующую очередь, сначала создайте новый объект **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="1ac77-141">Затем вызовите метод **add_message**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="1ac77-142">Объект **cloud_queue_message** может быть создан из строки или массива **байтов**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="1ac77-143">Ниже приведен код, который создает очередь (если она отсутствует) и вставляет сообщение "Hello World".</span><span class="sxs-lookup"><span data-stu-id="1ac77-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="1ac77-144">Практическое руководство. Просмотр следующего сообщения</span><span class="sxs-lookup"><span data-stu-id="1ac77-144">How to: Peek at the next message</span></span>
<span data-ttu-id="1ac77-145">Вы можете просмотреть сообщение в начале очереди, не удаляя его из очереди, вызвав метод **peek_message**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="1ac77-146">Практическое руководство. Изменение содержимого сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="1ac77-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="1ac77-147">Вы можете изменить содержимое сообщения непосредственно в очереди.</span><span class="sxs-lookup"><span data-stu-id="1ac77-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="1ac77-148">Если сообщение представляет собой рабочую задачу, можно использовать эту функцию для обновления состояния рабочей задачи.</span><span class="sxs-lookup"><span data-stu-id="1ac77-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="1ac77-149">Следующий код добавляет новое содержимое в очередь сообщений и продлевает время ожидания видимости еще на 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="1ac77-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="1ac77-150">Это сохраняет состояние работы, связанной с данным сообщением, и позволяет клиенту продолжить работу с сообщением на протяжении еще одной минуты.</span><span class="sxs-lookup"><span data-stu-id="1ac77-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="1ac77-151">Этот метод можно использовать для отслеживания многошаговых рабочих процессов по сообщениям в очереди без необходимости начинать с самого начала в случае сбоя шага обработки в связи с ошибкой аппаратного или программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="1ac77-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="1ac77-152">Обычно также сохраняется счетчик повторов; если количество повторов сообщения превысит n раз, его нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="1ac77-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="1ac77-153">Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.</span><span class="sxs-lookup"><span data-stu-id="1ac77-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="1ac77-154">Практическое руководство. Удаление следующего сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="1ac77-154">How to: De-queue the next message</span></span>
<span data-ttu-id="1ac77-155">Код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="1ac77-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="1ac77-156">При вызове **get_message** вы получаете следующее сообщение в очереди.</span><span class="sxs-lookup"><span data-stu-id="1ac77-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="1ac77-157">Сообщение, возвращаемое методом **get_message**, становится невидимым для другого кода, считывающего сообщения из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="1ac77-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="1ac77-158">Чтобы завершить удаление сообщения из очереди, необходимо также вызвать метод **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="1ac77-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="1ac77-159">Этот двухэтапный процесс удаления сообщения позволяет удостовериться, что если коду не удастся обработать сообщение из-за сбоя оборудования или программного обеспечения, другой экземпляр кода сможет получить то же сообщение и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="1ac77-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="1ac77-160">Код вызывает метод **delete_message** сразу после обработки сообщения.</span><span class="sxs-lookup"><span data-stu-id="1ac77-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="1ac77-161">Дополнительные параметры для удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="1ac77-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="1ac77-162">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="1ac77-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="1ac77-163">Во-первых, можно получить пакет сообщений (до 32 сообщений).</span><span class="sxs-lookup"><span data-stu-id="1ac77-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="1ac77-164">Во-вторых, можно задать более длительное или короткое время ожидания видимости, чтобы предоставить коду больше или меньше времени на полную обработку каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="1ac77-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="1ac77-165">В следующем примере кода метод **get_messages** используется для получения 20 сообщений за один вызов.</span><span class="sxs-lookup"><span data-stu-id="1ac77-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="1ac77-166">Затем он обрабатывает каждое сообщение с помощью цикла **for** .</span><span class="sxs-lookup"><span data-stu-id="1ac77-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="1ac77-167">Он также задает время ожидания невидимости 5 минут для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="1ac77-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="1ac77-168">Обратите внимание, что пятиминутный период начинается для всех сообщений одновременно, поэтому по прошествии 5 минут с момента вызова **get_messages** все сообщения, которые не были удалены, снова становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="1ac77-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="1ac77-169">Практическое руководство. Получение длины очереди</span><span class="sxs-lookup"><span data-stu-id="1ac77-169">How to: Get the queue length</span></span>
<span data-ttu-id="1ac77-170">Вы можете узнать приблизительное количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="1ac77-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="1ac77-171">Метод **download_attributes** отправляет в службу очередей запрос на извлечение атрибутов очереди, включая количество сообщений.</span><span class="sxs-lookup"><span data-stu-id="1ac77-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="1ac77-172">Метод **Approximate_message_count** возвращает приблизительное количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="1ac77-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="1ac77-173">Практическое руководство. Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="1ac77-173">How to: Delete a queue</span></span>
<span data-ttu-id="1ac77-174">Для удаления очереди и всех сообщений в ней вызовите метод **delete_queue_if_exists** для объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="1ac77-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="1ac77-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ac77-175">Next steps</span></span>
<span data-ttu-id="1ac77-176">Теперь, когда вы ознакомились с основными сведениями о хранилище очередей, используйте следующие ссылки для получения дополнительных сведений о хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="1ac77-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="1ac77-177">Использование хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="1ac77-177">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="1ac77-178">Использование табличного хранилища из C++</span><span class="sxs-lookup"><span data-stu-id="1ac77-178">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="1ac77-179">Перечисление ресурсов хранилища Azure в C++</span><span class="sxs-lookup"><span data-stu-id="1ac77-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="1ac77-180">Справочник по клиентской библиотеке хранилища для C++</span><span class="sxs-lookup"><span data-stu-id="1ac77-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="1ac77-181">Документация по хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="1ac77-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)