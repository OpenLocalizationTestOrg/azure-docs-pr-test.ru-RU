---
title: "aaaHow toouse хранилища очередей из Node.js | Документы Microsoft"
description: "Узнайте, как toocreate службы очередей Azure hello toouse и очереди delete и insert, получение и удаление сообщений. Примеры кода написаны на Node.js."
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="02ff9-104">Как toouse хранилища очередей из Node.js</span><span class="sxs-lookup"><span data-stu-id="02ff9-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="02ff9-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="02ff9-105">Overview</span></span>
<span data-ttu-id="02ff9-106">В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы очередей Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="02ff9-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="02ff9-107">образцы Hello записываются с помощью Node.js API hello.</span><span class="sxs-lookup"><span data-stu-id="02ff9-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="02ff9-108">Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание и удаление очередей**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="02ff9-109">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="02ff9-109">Create a Node.js Application</span></span>
<span data-ttu-id="02ff9-110">Создайте пустое приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="02ff9-110">Create a blank Node.js application.</span></span> <span data-ttu-id="02ff9-111">Инструкции создания приложений Node.js см. в разделе [создать веб-приложение Node.js в службе приложений Azure](../../app-service-web/app-service-web-get-started-nodejs.md), [построения и развертывания tooan приложений Node.js облачной службы Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) с помощью Windows PowerShell или [ Построение и развертывание приложения tooAzure web Node.js, с помощью Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="02ff9-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="02ff9-112">Настройка приложения tooAccess хранилища</span><span class="sxs-lookup"><span data-stu-id="02ff9-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="02ff9-113">toouse хранилища Azure необходимо hello пакет SDK хранилища Azure для Node.js, включающий набор библиотек удобства, взаимодействующих со службами REST hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="02ff9-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="02ff9-114">С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета</span><span class="sxs-lookup"><span data-stu-id="02ff9-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="02ff9-115">Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Unix), перейдите в папку toohello, где создан пример приложения.</span><span class="sxs-lookup"><span data-stu-id="02ff9-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="02ff9-116">Тип **npm установить хранилища azure** в командном окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="02ff9-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="02ff9-117">Выходные данные команды hello — примерно toohello следующий пример.</span><span class="sxs-lookup"><span data-stu-id="02ff9-117">Output from hello command is similar toohello following example.</span></span>
 
    ```
    azure-storage@0.5.0 node_modules\azure-storage
    +-- extend@1.2.1
    +-- xmlbuilder@0.4.3
    +-- mime@1.2.11
    +-- node-uuid@1.4.3
    +-- validator@3.22.2
    +-- underscore@1.4.4
    +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
    +-- xml2js@0.2.7 (sax@0.5.2)
    +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    ```

3. <span data-ttu-id="02ff9-118">Вы можете вручную запустить hello **ls** tooverify команды, **узел\_модули** папка была создана.</span><span class="sxs-lookup"><span data-stu-id="02ff9-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="02ff9-119">В этой папке можно найти hello **хранилища azure** пакет, который содержит hello библиотеки, необходимые для доступа к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="02ff9-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="02ff9-120">Импорт пакета hello</span><span class="sxs-lookup"><span data-stu-id="02ff9-120">Import hello package</span></span>
<span data-ttu-id="02ff9-121">С помощью блокнота или другого текстового редактора, добавить hello следующие верхней toohello **server.js** файл приложения hello предполагаемой toouse хранилища:</span><span class="sxs-lookup"><span data-stu-id="02ff9-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="02ff9-122">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="02ff9-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="02ff9-123">модуль Hello azure будет считывать hello переменных среды AZURE\_ХРАНИЛИЩА\_учетной записи и AZURE\_ХРАНЕНИЯ\_доступа\_ключа или AZURE\_ХРАНЕНИЯ\_подключения \_Строка для tooyour tooconnect сведения, необходимые учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="02ff9-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="02ff9-124">Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello при вызове **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="02ff9-125">Например, задание переменных среды hello в hello [портала Azure](https://portal.azure.com) на веб-сайт Azure в разделе [Node.js веб-приложения с использованием службы таблиц Azure hello].</span><span class="sxs-lookup"><span data-stu-id="02ff9-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="02ff9-126">Практическое руководство. Создание очереди</span><span class="sxs-lookup"><span data-stu-id="02ff9-126">How To: Create a Queue</span></span>
<span data-ttu-id="02ff9-127">Hello следующий код создает **QueueService** объекта, который позволяет toowork с очередями.</span><span class="sxs-lookup"><span data-stu-id="02ff9-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="02ff9-128">Используйте hello **createQueueIfNotExists** метод, возвращающий hello указанной очереди, если он уже существует, или создает новую очередь с указанным именем hello, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="02ff9-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="02ff9-129">Если создается очередь hello `result.created` имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="02ff9-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="02ff9-130">Если существует очередь hello, `result.created` имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="02ff9-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="02ff9-131">Фильтры</span><span class="sxs-lookup"><span data-stu-id="02ff9-131">Filters</span></span>
<span data-ttu-id="02ff9-132">Необязательный операции фильтрации может быть применен toooperations, выполняемые с помощью **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="02ff9-133">К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:</span><span class="sxs-lookup"><span data-stu-id="02ff9-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="02ff9-134">После выполнения его предварительной обработки параметров запроса hello, метод hello должен toocall «Далее» передача обратный вызов с hello следующие подписи:</span><span class="sxs-lookup"><span data-stu-id="02ff9-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="02ff9-135">В этот обратный вызов, а после обработки returnObject hello (hello ответ от сервера toohello hello запроса), обратного вызова hello необходимы tooeither рядом вызова, если он существует toocontinue обработки других фильтров, или просто вызвав finalCallback tooend, в противном случае копирование hello вызов службы.</span><span class="sxs-lookup"><span data-stu-id="02ff9-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="02ff9-136">Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="02ff9-137">Hello следующий код создает **QueueService** объект, который использует hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="02ff9-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="02ff9-138">Практическое руководство. Вставка сообщения в очередь</span><span class="sxs-lookup"><span data-stu-id="02ff9-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="02ff9-139">сообщения в очереди, используйте hello tooinsert **createMessage** метод для создания нового сообщения и добавьте его toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="02ff9-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="02ff9-140">Практическое руководство: Просмотр следующего сообщения hello</span><span class="sxs-lookup"><span data-stu-id="02ff9-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="02ff9-141">Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **peekMessages** метод.</span><span class="sxs-lookup"><span data-stu-id="02ff9-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="02ff9-142">По умолчанию **peekMessages** просматривает одно сообщение.</span><span class="sxs-lookup"><span data-stu-id="02ff9-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="02ff9-143">Hello `result` содержит сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="02ff9-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="02ff9-144">С помощью **peekMessages** Если нет сообщений в очереди hello не будет возвращать ошибку, но сообщения не будут возвращены.</span><span class="sxs-lookup"><span data-stu-id="02ff9-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="02ff9-145">Практическое руководство: Следующее сообщение hello вывода из очереди</span><span class="sxs-lookup"><span data-stu-id="02ff9-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="02ff9-146">Обработка сообщения выполняется двухэтапным процессом:</span><span class="sxs-lookup"><span data-stu-id="02ff9-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="02ff9-147">Вывести из очереди сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="02ff9-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="02ff9-148">Удалите сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="02ff9-148">Delete hello message.</span></span>

<span data-ttu-id="02ff9-149">использовать toodequeue сообщение, **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="02ff9-150">Это делает сообщений hello невидимы в очереди hello, чтобы другие клиенты не мог обрабатывать их.</span><span class="sxs-lookup"><span data-stu-id="02ff9-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="02ff9-151">После обработки сообщения приложения вызовите **deleteMessage** toodelete его из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="02ff9-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="02ff9-152">Следующий пример Hello получает сообщение, а затем удаляет его.</span><span class="sxs-lookup"><span data-stu-id="02ff9-152">hello following example gets a message, then deletes it:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> <span data-ttu-id="02ff9-153">По умолчанию сообщение виден на 30 секунд, после которого он является видимым tooother клиентов.</span><span class="sxs-lookup"><span data-stu-id="02ff9-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="02ff9-154">Чтобы задать другое значение, укажите с методом **getMessages** параметр `options.visibilityTimeout`.</span><span class="sxs-lookup"><span data-stu-id="02ff9-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="02ff9-155">С помощью **getMessages** Если нет сообщений в очереди hello не будет возвращать ошибку, но сообщения не будут возвращены.</span><span class="sxs-lookup"><span data-stu-id="02ff9-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="02ff9-156">Практическое руководство: Изменение содержимого hello сообщения в очереди</span><span class="sxs-lookup"><span data-stu-id="02ff9-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="02ff9-157">Можно изменить содержимое сообщений на месте в очереди с помощью hello hello **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="02ff9-158">Следующий пример Hello обновляет hello текст сообщения:</span><span class="sxs-lookup"><span data-stu-id="02ff9-158">hello following example updates hello text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="02ff9-159">Практическое руководство. Использование дополнительных параметров для удаления сообщений из очереди</span><span class="sxs-lookup"><span data-stu-id="02ff9-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="02ff9-160">Существует два способа настройки извлечения сообщения из очереди:</span><span class="sxs-lookup"><span data-stu-id="02ff9-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="02ff9-161">`options.numOfMessages`— Получите пакет сообщений (вверх too32.)</span><span class="sxs-lookup"><span data-stu-id="02ff9-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="02ff9-162">`options.visibilityTimeout` — задает более длительное или короткое время ожидания невидимости.</span><span class="sxs-lookup"><span data-stu-id="02ff9-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="02ff9-163">Hello следующий пример использует hello **getMessages** метод tooget 15 сообщений в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="02ff9-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="02ff9-164">Затем он обрабатывает каждое сообщение с помощью цикла for.</span><span class="sxs-lookup"><span data-stu-id="02ff9-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="02ff9-165">Он также устанавливает минут toofive hello невидимости времени ожидания для всех сообщений, возвращаемый этим методом.</span><span class="sxs-lookup"><span data-stu-id="02ff9-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="02ff9-166">Практическое руководство: Получение hello длина очереди</span><span class="sxs-lookup"><span data-stu-id="02ff9-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="02ff9-167">Hello **getQueueMetadata** Возвращает метаданные очереди hello, включая hello приблизительное количество сообщений, ожидающих в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="02ff9-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="02ff9-168">Практическое руководство. Получение списка очередей</span><span class="sxs-lookup"><span data-stu-id="02ff9-168">How To: List Queues</span></span>
<span data-ttu-id="02ff9-169">Список очередей, используйте tooretrieve **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="02ff9-170">Список tooretrieve, отфильтрованный по определенным префиксом, используйте **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="02ff9-171">Если все очереди не может быть возвращен, `result.continuationToken` может использоваться как первый параметр hello **listQueuesSegmented** или hello второй параметр **listQueuesSegmentedWithPrefix** tooretrieve дополнительных результатов.</span><span class="sxs-lookup"><span data-stu-id="02ff9-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="02ff9-172">Практическое руководство. Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="02ff9-172">How To: Delete a Queue</span></span>
<span data-ttu-id="02ff9-173">toodelete все сообщения hello и очереди содержащиеся в нем, вызовите метод **deleteQueue** метод hello объекта очереди.</span><span class="sxs-lookup"><span data-stu-id="02ff9-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="02ff9-174">использовать все сообщения из очереди, не удаляя его, tooclear **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="02ff9-175">Практическое руководство. Работа с подписанными URL-адресами</span><span class="sxs-lookup"><span data-stu-id="02ff9-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="02ff9-176">Подписи общего доступа (SAS) являются tooqueues детального доступа tooprovide безопасным способом, без указания имени учетной записи хранения или ключи.</span><span class="sxs-lookup"><span data-stu-id="02ff9-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="02ff9-177">SAS чаще всего используется tooprovide ограниченный доступ tooyour очереди, например toosubmit сообщения мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="02ff9-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="02ff9-178">Доверенного приложения, такие как облачная служба создает подписанный URL-адрес с помощью hello **generateSharedAccessSignature** из hello **QueueService**и предоставляет его tooan приложения с частичным доверием или без доверия.</span><span class="sxs-lookup"><span data-stu-id="02ff9-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="02ff9-179">Например, мобильному приложению.</span><span class="sxs-lookup"><span data-stu-id="02ff9-179">For example, a mobile app.</span></span> <span data-ttu-id="02ff9-180">Hello SAS создается с помощью политики, которая описывает hello начала и окончания в какой hello действует SAS, а также hello владельца SAS уровня toohello предоставленный доступ.</span><span class="sxs-lookup"><span data-stu-id="02ff9-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="02ff9-181">Здравствуйте, следующий пример создает новую политику общего доступа, который позволит hello toohello SAS владельца tooadd сообщений в очереди и истечения срока действия 100 минут после hello время его создания.</span><span class="sxs-lookup"><span data-stu-id="02ff9-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

<span data-ttu-id="02ff9-182">Обратите внимание, что сведения об узле hello должен предоставляемых также, при необходимости при владельца SAS hello попытке tooaccess hello очереди.</span><span class="sxs-lookup"><span data-stu-id="02ff9-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="02ff9-183">Здравствуйте клиентское приложение, а затем использует hello SAS с **QueueServiceWithSAS** tooperform операций с очередью hello.</span><span class="sxs-lookup"><span data-stu-id="02ff9-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="02ff9-184">Следующий пример Hello подключается toohello очереди и создает сообщение.</span><span class="sxs-lookup"><span data-stu-id="02ff9-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="02ff9-185">Поскольку hello SAS был сформирован с использованием добавить доступ, если попытка не было внесено tooread, обновления или удаления сообщения, будет возвращена ошибка.</span><span class="sxs-lookup"><span data-stu-id="02ff9-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="02ff9-186">Доступ к спискам управления</span><span class="sxs-lookup"><span data-stu-id="02ff9-186">Access control lists</span></span>
<span data-ttu-id="02ff9-187">Также можно использовать политику доступа hello tooset список управления доступом (ACL) для SAS.</span><span class="sxs-lookup"><span data-stu-id="02ff9-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="02ff9-188">Это полезно в том случае, если хотите tooallow очереди hello tooaccess несколько клиентов, но добавлены политики различный уровень доступа для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="02ff9-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="02ff9-189">ACL реализуется с помощью массива политик доступа, каждая из которых связана со своим идентификатором.</span><span class="sxs-lookup"><span data-stu-id="02ff9-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="02ff9-190">Следующий пример Hello определяет две политики; один «user1» и «user2»:</span><span class="sxs-lookup"><span data-stu-id="02ff9-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="02ff9-191">Следующий пример возвращает Hello hello текущего списка управления Доступом для **myqueue**, затем добавляет hello новые политики с помощью **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="02ff9-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="02ff9-192">Такой подход допускает выполнение:</span><span class="sxs-lookup"><span data-stu-id="02ff9-192">This approach allows:</span></span>

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="02ff9-193">Один раз hello ACL было указано, можно создать на основе кода hello политики SAS.</span><span class="sxs-lookup"><span data-stu-id="02ff9-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="02ff9-194">Привет, следующий пример создает новый SAS для «user2»:</span><span class="sxs-lookup"><span data-stu-id="02ff9-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="02ff9-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02ff9-195">Next Steps</span></span>
<span data-ttu-id="02ff9-196">Теперь, когда вы узнали основы hello хранилища очередей, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="02ff9-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="02ff9-197">Посетите hello [блоге разработчиков хранилища Azure] [блоге разработчиков хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="02ff9-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="02ff9-198">Посетите hello [пакет SDK хранилища Azure для узла] [ Azure Storage SDK for Node] репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="02ff9-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="02ff9-199">
[Создание веб-приложений Node.js в Azure](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="02ff9-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="02ff9-200">[Веб-приложение node.js с помощью hello службы таблиц Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="02ff9-200">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="02ff9-201">[Построение и развертывание tooan приложений Node.js облачной службы Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="02ff9-201">[Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="02ff9-202">[Azure блог группы разработчиков хранилища]: http://blogs.msdn.com/b/windowsazurestorage/ [построение и развертывание приложения tooAzure web Node.js, с помощью Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="02ff9-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
