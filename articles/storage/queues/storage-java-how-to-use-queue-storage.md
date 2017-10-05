---
title: "Как использовать хранилище очередей из Java | Документация Майкрософт"
description: "Вы узнаете, как использовать службы очередей Azure для создания и удаления очередей, вставки, получения и удаления сообщений. Примеры кода написаны на Java."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: a56b345c5efb4ce9c8ee2da91b798d09d44e42be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="47da5-104">Использование хранилища очередей из Java</span><span class="sxs-lookup"><span data-stu-id="47da5-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="47da5-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="47da5-105">Overview</span></span>
<span data-ttu-id="47da5-106">В этом руководстве показано, как реализовать типичные сценарии с использованием службы хранения очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="47da5-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="47da5-107">Примеры написаны на Java и используют [пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="47da5-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="47da5-108">Здесь описаны такие сценарии, как **вставка**, **просмотр**, **получение** и **удаление** сообщений очереди, а также **создание** и **удаление** очередей.</span><span class="sxs-lookup"><span data-stu-id="47da5-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="47da5-109">Дополнительные сведения об очередях см. в разделе [Дальнейшие действия](#Next-Steps).</span><span class="sxs-lookup"><span data-stu-id="47da5-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="47da5-110">Примечание. Пакет SDK доступен для разработчиков, которые используют хранилище Azure на устройствах под управлением Android.</span><span class="sxs-lookup"><span data-stu-id="47da5-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="47da5-111">Дополнительные сведения см. в разделе [Microsoft Azure Storage SDK for Android][Azure Storage SDK for Android] (Пакет SDK хранилища Azure для Android).</span><span class="sxs-lookup"><span data-stu-id="47da5-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="47da5-112">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="47da5-112">Create a Java application</span></span>
<span data-ttu-id="47da5-113">В этом руководстве будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.</span><span class="sxs-lookup"><span data-stu-id="47da5-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="47da5-114">Для этого необходимо установить пакет SDK для Java (JDK) и создать учетную запись хранения Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="47da5-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="47da5-115">После того, как это будет сделано, необходимо убедиться, что ваша система разработки отвечает минимальным требованиям и зависимостям, указанным в репозитории [пакета SDK службы хранилища Azure для Java][Azure Storage SDK for Java] на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="47da5-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="47da5-116">Если ваша система отвечает указанным требованиям можно приступить к выполнению инструкций по загрузке библиотек хранилища Azure для Java из репозитория и их установке на своей системе.</span><span class="sxs-lookup"><span data-stu-id="47da5-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="47da5-117">После завершение этих задач вы сможете приступить к созданию приложения Java с использованием примеров из данной статьи.</span><span class="sxs-lookup"><span data-stu-id="47da5-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="47da5-118">Настройка приложения для доступа к хранилищу очередей</span><span class="sxs-lookup"><span data-stu-id="47da5-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="47da5-119">Если нужно использовать API-интерфейсы Azure для доступа к очередям, добавьте следующие инструкции импорта в верхнюю часть файла Java:</span><span class="sxs-lookup"><span data-stu-id="47da5-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="47da5-120">Настройка строки подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="47da5-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="47da5-121">Клиент хранилища Azure использует строку подключения с целью хранения конечных точек и учетных данных для доступа к службам управления данными.</span><span class="sxs-lookup"><span data-stu-id="47da5-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="47da5-122">При работе в клиентском приложении необходимо указать для хранилища строку подключения в следующем формате, используя имя своей учетной записи хранения и первичный ключ доступа для учетной записи хранения, указанные на [портале Azure](https://portal.azure.com) значениями *AccountName* и *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="47da5-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="47da5-123">В этом примере показано, как объявить статическое поле для размещения строки подключения:</span><span class="sxs-lookup"><span data-stu-id="47da5-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="47da5-124">Если приложение выполняется в роли на платформе Microsoft Azure, эта строка может храниться в файле конфигурации службы *ServiceConfiguration.cscfg*, для доступа к которой можно использовать вызов метода **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="47da5-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="47da5-125">Ниже приведен пример получения строки подключения из элемента **Setting** с именем *StorageConnectionString* в файле конфигурации службы:</span><span class="sxs-lookup"><span data-stu-id="47da5-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="47da5-126">В приведенных ниже примерах предполагается, что вы использовали одно из этих двух определений для получения строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="47da5-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="47da5-127">Практическое руководство. Создание очереди</span><span class="sxs-lookup"><span data-stu-id="47da5-127">How to: Create a queue</span></span>
<span data-ttu-id="47da5-128">Объект **CloudQueueClient** позволяет ссылаться на объекты очередей.</span><span class="sxs-lookup"><span data-stu-id="47da5-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="47da5-129">Следующий код создает объект **CloudQueueClient**.</span><span class="sxs-lookup"><span data-stu-id="47da5-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="47da5-130">(Примечание. Есть и другие способы создания объектов **CloudStorageAccount**. Дополнительные сведения см. в разделе **CloudStorageAccount** в [справочнике по пакету SDK для клиента службы хранилища Azure].)</span><span class="sxs-lookup"><span data-stu-id="47da5-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="47da5-131">С помощью объекта **CloudqueueClient** получите ссылку на очередь, которую необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="47da5-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="47da5-132">Очередь можно создать, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="47da5-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="47da5-133">Практическое руководство. Добавление сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="47da5-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="47da5-134">Чтобы вставить сообщение в существующую очередь, сначала создайте объект **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="47da5-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="47da5-135">Затем вызовите метод **AddMessage**.</span><span class="sxs-lookup"><span data-stu-id="47da5-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="47da5-136">Для создания объекта **CloudQueueMessage** можно использовать строку (в формате UTF-8) или массив байтов.</span><span class="sxs-lookup"><span data-stu-id="47da5-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="47da5-137">Ниже приведен код, который создает очередь (если она не существует) и вставляет сообщение "Привет, мир":</span><span class="sxs-lookup"><span data-stu-id="47da5-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="47da5-138">Практическое руководство. Просмотр следующего сообщения</span><span class="sxs-lookup"><span data-stu-id="47da5-138">How to: Peek at the next message</span></span>
<span data-ttu-id="47da5-139">Вы можете просмотреть сообщение в начале очереди, не удаляя его из очереди, вызвав метод **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="47da5-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="47da5-140">Практическое руководство. Изменение содержимого сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="47da5-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="47da5-141">Вы можете изменить содержимое сообщения непосредственно в очереди.</span><span class="sxs-lookup"><span data-stu-id="47da5-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="47da5-142">Если сообщение представляет собой рабочую задачу, можно использовать эту функцию для обновления состояния рабочей задачи.</span><span class="sxs-lookup"><span data-stu-id="47da5-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="47da5-143">Следующий код добавляет новое содержимое в очередь сообщений и продлевает время ожидания видимости еще на 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="47da5-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="47da5-144">Это сохраняет состояние работы, связанной с данным сообщением, и позволяет клиенту продолжить работу с сообщением на протяжении еще одной минуты.</span><span class="sxs-lookup"><span data-stu-id="47da5-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="47da5-145">Этот метод можно использовать для отслеживания многошаговых рабочих процессов по сообщениям в очереди без необходимости начинать с самого начала в случае сбоя шага обработки в связи с ошибкой аппаратного или программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="47da5-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="47da5-146">Обычно также сохраняется счетчик повторов. Если количество повторов сообщения превысит *n* раз, его нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="47da5-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="47da5-147">Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.</span><span class="sxs-lookup"><span data-stu-id="47da5-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="47da5-148">Приведенный ниже пример кода выполняет поиск в очереди сообщения, находит первое сообщение, которое содержит "Привет, мир", затем изменяет контент сообщения и выполняет выход.</span><span class="sxs-lookup"><span data-stu-id="47da5-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="47da5-149">В отличие от этого, следующий пример кода просто обновляет первое видимое сообщение в очереди.</span><span class="sxs-lookup"><span data-stu-id="47da5-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="47da5-150">Практическое руководство. Получение длины очереди</span><span class="sxs-lookup"><span data-stu-id="47da5-150">How to: Get the queue length</span></span>
<span data-ttu-id="47da5-151">Вы можете узнать приблизительное количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="47da5-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="47da5-152">Метод **downloadAttributes** запрашивает у службы очередей несколько текущих значений, включая количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="47da5-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="47da5-153">Счетчик указывает число лишь приблизительно, так как сообщения могут добавляться или удаляться после ответа службы очередей на ваш запрос.</span><span class="sxs-lookup"><span data-stu-id="47da5-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="47da5-154">Метод **getApproximateMessageCount** возвращает последнее значение, полученное при вызове **downloadAttributes** без обращения к службе очередей.</span><span class="sxs-lookup"><span data-stu-id="47da5-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="47da5-155">Практическое руководство. Удаление следующего сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="47da5-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="47da5-156">Код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="47da5-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="47da5-157">При вызове метода **retrieveMessage**вы получаете следующее сообщение в очереди.</span><span class="sxs-lookup"><span data-stu-id="47da5-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="47da5-158">Сообщение, возвращаемое методом **retrieveMessage** , становится невидимым для другого кода, считывающего сообщения из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="47da5-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="47da5-159">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="47da5-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="47da5-160">Чтобы завершить удаление сообщения из очереди, необходимо также вызвать метод **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="47da5-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="47da5-161">Этот двухэтапный процесс удаления сообщения позволяет удостовериться, что если коду не удастся обработать сообщение из-за сбоя оборудования или программного обеспечения, другой экземпляр кода сможет получить то же сообщение и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="47da5-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="47da5-162">Код вызывает метод **deleteMessage** сразу после обработки сообщения.</span><span class="sxs-lookup"><span data-stu-id="47da5-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="47da5-163">Дополнительные варианты удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="47da5-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="47da5-164">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="47da5-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="47da5-165">Во-первых, можно получить пакет сообщений (до 32 сообщений).</span><span class="sxs-lookup"><span data-stu-id="47da5-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="47da5-166">Во-вторых, можно задать более длительное или короткое время ожидания видимости, чтобы предоставить коду больше или меньше времени на полную обработку каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="47da5-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="47da5-167">В следующем примере кода метод **retrieveMessages** используется для получения 20 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="47da5-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="47da5-168">Затем он обрабатывает каждое сообщение с помощью цикла **for** .</span><span class="sxs-lookup"><span data-stu-id="47da5-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="47da5-169">Пример также задает время ожидания невидимости в размере пяти минут (300 секунд) для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="47da5-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="47da5-170">Обратите внимание, что пятиминутный период начинается для всех сообщений одновременно, поэтому по прошествии 5 минут с момента вызова **retreiveMessages**все сообщения, которые не были удалены, снова становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="47da5-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="47da5-171">Как перечислять очереди</span><span class="sxs-lookup"><span data-stu-id="47da5-171">How to: List the queues</span></span>
<span data-ttu-id="47da5-172">Чтобы получить список текущей очереди, вызовите метод **CloudQueueClient.listQueues()**, который возвращает коллекцию объектов **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="47da5-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="47da5-173">Практическое руководство. Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="47da5-173">How to: Delete a queue</span></span>
<span data-ttu-id="47da5-174">Для удаления очереди и всех сообщений в ней вызовите метод **deleteIfExists** в объекте **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="47da5-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="47da5-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47da5-175">Next steps</span></span>
<span data-ttu-id="47da5-176">Вы изучили основные сведения о хранилище очередей. Дополнительные сведения о более сложных задачах по использованию хранилища можно найти по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="47da5-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="47da5-177">[Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="47da5-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="47da5-178">[справочнике по пакету SDK для клиента службы хранилища Azure][справочнике по пакету SDK для клиента службы хранилища Azure]</span><span class="sxs-lookup"><span data-stu-id="47da5-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="47da5-179">[REST API служб хранилища Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="47da5-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="47da5-180">[Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="47da5-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[справочнике по пакету SDK для клиента службы хранилища Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
