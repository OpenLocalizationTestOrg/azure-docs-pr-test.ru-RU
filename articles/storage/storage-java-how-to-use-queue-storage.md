---
title: "aaaHow toouse хранилища очередей из Java | Документы Microsoft"
description: "Узнайте, как toocreate службы очередей Azure hello toouse и очереди delete и insert, получение и удаление сообщений. Примеры кода написаны на Java."
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
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="843a8-104">Как toouse хранилища очередей из Java</span><span class="sxs-lookup"><span data-stu-id="843a8-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="843a8-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="843a8-105">Overview</span></span>
<span data-ttu-id="843a8-106">В этом руководстве будет показано, как с помощью распространенных сценариев tooperform hello службы хранилища очередей Azure.</span><span class="sxs-lookup"><span data-stu-id="843a8-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="843a8-107">Hello примеры написаны на Java и использовать hello [пакет SDK хранилища Azure для Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="843a8-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="843a8-108">Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание** и **удаление** очереди.</span><span class="sxs-lookup"><span data-stu-id="843a8-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="843a8-109">Дополнительные сведения об очередях см. в разделе hello [дальнейшие действия](#Next-Steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="843a8-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="843a8-110">Примечание. Пакет SDK доступен для разработчиков, которые используют хранилище Azure на устройствах под управлением Android.</span><span class="sxs-lookup"><span data-stu-id="843a8-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="843a8-111">Дополнительные сведения см. в разделе hello [пакет SDK хранилища Azure для Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="843a8-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="843a8-112">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="843a8-112">Create a Java application</span></span>
<span data-ttu-id="843a8-113">В этом руководстве будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.</span><span class="sxs-lookup"><span data-stu-id="843a8-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="843a8-114">toodo таким образом, вам потребуется tooinstall hello Java Development Kit (JDK) и создать учетную запись хранилища Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="843a8-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="843a8-115">Как только вы делали, вам потребуется tooverify, разработки система удовлетворяет минимальным требованиям hello и зависимости, которые указаны в hello [пакет SDK хранилища Azure для Java] [ Azure Storage SDK for Java] репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="843a8-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="843a8-116">Если компьютер соответствует этим требованиям, можно выполнить hello инструкции по загрузке и установке hello библиотеки хранилища Azure для Java в вашей системе из этого репозитория.</span><span class="sxs-lookup"><span data-stu-id="843a8-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="843a8-117">После завершения этих задач можно будет toocreate приложения Java, использующего hello примеры в этой статье.</span><span class="sxs-lookup"><span data-stu-id="843a8-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="843a8-118">Настройка хранилища очереди tooaccess приложения</span><span class="sxs-lookup"><span data-stu-id="843a8-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="843a8-119">Добавьте следующие начало toohello инструкции импорта файла Java hello, место очереди tooaccess API-интерфейсов хранилища Azure toouse hello:</span><span class="sxs-lookup"><span data-stu-id="843a8-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="843a8-120">Настройка строки подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="843a8-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="843a8-121">Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления.</span><span class="sxs-lookup"><span data-stu-id="843a8-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="843a8-122">При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, используя hello имя учетной записи и hello первичный ключ доступа для учетной записи хранения hello, перечисленные в hello [портала Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения.</span><span class="sxs-lookup"><span data-stu-id="843a8-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="843a8-123">В этом примере показано, как объявить строки подключения hello toohold статического поля:</span><span class="sxs-lookup"><span data-stu-id="843a8-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="843a8-124">Эта строка в приложения, запущенного в рамках роли в Microsoft Azure, могут храниться в файле конфигурации службы hello, *ServiceConfiguration.cscfg*и можно осуществить с помощью toohello вызова  **RoleEnvironment.getConfigurationSettings** метод.</span><span class="sxs-lookup"><span data-stu-id="843a8-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="843a8-125">Ниже приведен пример получения строки подключения hello из **параметр** элемента с именем *StorageConnectionString* в файле конфигурации службы hello:</span><span class="sxs-lookup"><span data-stu-id="843a8-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="843a8-126">Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="843a8-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="843a8-127">Практическое руководство. Создание очереди</span><span class="sxs-lookup"><span data-stu-id="843a8-127">How to: Create a queue</span></span>
<span data-ttu-id="843a8-128">Объект **CloudQueueClient** позволяет ссылаться на объекты очередей.</span><span class="sxs-lookup"><span data-stu-id="843a8-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="843a8-129">Hello следующий код создает **CloudQueueClient** объекта.</span><span class="sxs-lookup"><span data-stu-id="843a8-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="843a8-130">(Примечание: существуют дополнительные способы toocreate **CloudStorageAccount** объектов; Дополнительные сведения см. в разделе **CloudStorageAccount** в hello [Azure SDK Справочник по клиентской хранилища].)</span><span class="sxs-lookup"><span data-stu-id="843a8-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="843a8-131">Используйте hello **CloudQueueClient** tooget требуется toouse очереди toohello ссылку объекта.</span><span class="sxs-lookup"><span data-stu-id="843a8-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="843a8-132">Можно создать очередь hello, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="843a8-132">You can create hello queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="843a8-133">Как: Добавление tooa очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="843a8-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="843a8-134">tooinsert сообщения в существующую очередь, сначала создайте **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="843a8-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="843a8-135">Затем вызовите hello **addMessage** метод.</span><span class="sxs-lookup"><span data-stu-id="843a8-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="843a8-136">Для создания объекта **CloudQueueMessage** можно использовать строку (в формате UTF-8) или массив байтов.</span><span class="sxs-lookup"><span data-stu-id="843a8-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="843a8-137">Ниже приведен код (если он не существует), который создает очередь и вставок приветственное сообщение «Hello, World».</span><span class="sxs-lookup"><span data-stu-id="843a8-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="843a8-138">Как: Просмотр следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="843a8-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="843a8-139">Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello путем вызова **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="843a8-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="843a8-140">Способ: измените содержимое hello сообщение из очереди</span><span class="sxs-lookup"><span data-stu-id="843a8-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="843a8-141">Вы можете изменить содержимое сообщений на месте в очереди hello hello.</span><span class="sxs-lookup"><span data-stu-id="843a8-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="843a8-142">Если сообщение hello представляет рабочей задачи, можно использовать этот компонент tooupdate hello состояние задачи рабочего hello.</span><span class="sxs-lookup"><span data-stu-id="843a8-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="843a8-143">После кода Hello обновляется приветственное сообщение очереди новое содержимое и наборы hello tooextend время ожидания видимости другой 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="843a8-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="843a8-144">Сохраняет состояние работ, сопряженные с приветственное сообщение hello и предоставляет другой минуты toocontinue работа на приветственное сообщение клиента hello.</span><span class="sxs-lookup"><span data-stu-id="843a8-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="843a8-145">Можно использовать этот рабочих процессов способ tootrack многоэтапной для очереди сообщений без необходимости toostart через от начала hello при неудачном завершении шага обработки из-за toohardware или ошибок программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="843a8-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="843a8-146">Как правило, будет хранить значение числа повторов, и если hello сообщение повторяется более  *n*  раз, следует удалить его.</span><span class="sxs-lookup"><span data-stu-id="843a8-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="843a8-147">Это обеспечивает защиту от сообщений, которые инициируют ошибку приложения при каждой попытке обработки.</span><span class="sxs-lookup"><span data-stu-id="843a8-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="843a8-148">следующие Hello кода выполняет образец hello очереди сообщений, находит первое сообщение hello, которое совпадает с «Hello, World» hello содержимое, а затем изменяет содержимое сообщения hello и завершает работу.</span><span class="sxs-lookup"><span data-stu-id="843a8-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="843a8-149">Кроме того hello следующий код обновляет только hello первой видимой сообщение hello очереди.</span><span class="sxs-lookup"><span data-stu-id="843a8-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="843a8-150">Как: hello длина очереди получения</span><span class="sxs-lookup"><span data-stu-id="843a8-150">How to: Get hello queue length</span></span>
<span data-ttu-id="843a8-151">Можно получить оценку hello количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="843a8-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="843a8-152">Hello **downloadAttributes** метод запрашивает у службы очередей hello несколько текущих значений, включая количество сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="843a8-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="843a8-153">число Hello приблизительное только в том случае, поскольку сообщения можно добавить или удалить после запроса tooyour отвечает hello службы очередей.</span><span class="sxs-lookup"><span data-stu-id="843a8-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="843a8-154">Hello **getApproximateMessageCount** метод возвращает последнее значение hello получить вызовом hello слишком**downloadAttributes**, без вызова службы очередей hello.</span><span class="sxs-lookup"><span data-stu-id="843a8-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="843a8-155">Как: Dequeue следующее сообщение hello</span><span class="sxs-lookup"><span data-stu-id="843a8-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="843a8-156">Код удаляет сообщение из очереди в два этапа.</span><span class="sxs-lookup"><span data-stu-id="843a8-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="843a8-157">При вызове **retrieveMessage**, вы получаете следующее сообщение hello в очереди.</span><span class="sxs-lookup"><span data-stu-id="843a8-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="843a8-158">Сообщение, возвращенное из **retrieveMessage** становится невидимой tooany другой код, чтение сообщений из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="843a8-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="843a8-159">По умолчанию это сообщение остается невидимым в течение 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="843a8-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="843a8-160">toofinish удаление приветственное сообщение из очереди hello, необходимо также вызвать **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="843a8-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="843a8-161">Это двухэтапный процесс удаления сообщения подтверждает, если tooprocess получит сообщение toohardware или ошибок программного обеспечения, другой экземпляр кода из-за сбоя программы hello одного сообщения и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="843a8-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="843a8-162">Вызовы кода **deleteMessage** сразу после обработки сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="843a8-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="843a8-163">Дополнительные варианты удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="843a8-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="843a8-164">Способ извлечения сообщения из очереди можно настроить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="843a8-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="843a8-165">Во-первых можно получить пакет сообщений (вверх too32).</span><span class="sxs-lookup"><span data-stu-id="843a8-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="843a8-166">Во-вторых можно задать более длинный или короткий невидимости тайм-аута, позволяя вашему коду больше или меньше toofully времени обработки каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="843a8-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="843a8-167">Hello следующий пример кода использует hello **retrieveMessages** метод tooget 20 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="843a8-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="843a8-168">Затем он обрабатывает каждое сообщение с помощью цикла **for** .</span><span class="sxs-lookup"><span data-stu-id="843a8-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="843a8-169">Он также устанавливает время ожидания toofive невидимости hello минут (300 секунд) для каждого сообщения.</span><span class="sxs-lookup"><span data-stu-id="843a8-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="843a8-170">Обратите внимание, что hello пяти минут запускается для всех сообщений в hello же времени, поэтому при пяти минут с момента вызова hello слишком**retrieveMessages**, все сообщения, которые не были удалены становятся видимыми.</span><span class="sxs-lookup"><span data-stu-id="843a8-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="843a8-171">Как: перечисление очередей hello</span><span class="sxs-lookup"><span data-stu-id="843a8-171">How to: List hello queues</span></span>
<span data-ttu-id="843a8-172">список текущей очереди hello, вызов hello tooobtain **CloudQueueClient.listQueues()** метод, который будет возвращать коллекцию **CloudQueue** объектов.</span><span class="sxs-lookup"><span data-stu-id="843a8-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="843a8-173">Практическое руководство. Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="843a8-173">How to: Delete a queue</span></span>
<span data-ttu-id="843a8-174">toodelete все сообщения hello и очереди содержащиеся в нем, вызов hello **deleteIfExists** метод hello **CloudQueue** объекта.</span><span class="sxs-lookup"><span data-stu-id="843a8-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="843a8-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="843a8-175">Next steps</span></span>
<span data-ttu-id="843a8-176">Теперь, когда вы узнали основы hello хранилища очередей, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="843a8-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="843a8-177">[Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="843a8-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="843a8-178">[Azure SDK Справочник по клиентской хранилища][Azure SDK Справочник по клиентской хранилища]</span><span class="sxs-lookup"><span data-stu-id="843a8-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="843a8-179">[REST API служб хранилища Azure][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="843a8-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="843a8-180">[Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="843a8-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure SDK Справочник по клиентской хранилища]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
