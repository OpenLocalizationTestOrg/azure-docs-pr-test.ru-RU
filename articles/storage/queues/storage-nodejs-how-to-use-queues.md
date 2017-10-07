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
# <a name="how-toouse-queue-storage-from-nodejs"></a>Как toouse хранилища очередей из Node.js
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы очередей Microsoft Azure. образцы Hello записываются с помощью Node.js API hello. Hello сценарии включают **Вставка**, **Просмотр**, **начало**, и **удаление** очередь сообщений, а также  **Создание и удаление очередей**.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Создание приложения Node.js
Создайте пустое приложение Node.js. Инструкции создания приложений Node.js см. в разделе [создать веб-приложение Node.js в службе приложений Azure](../../app-service-web/app-service-web-get-started-nodejs.md), [построения и развертывания tooan приложений Node.js облачной службы Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) с помощью Windows PowerShell или [ Построение и развертывание приложения tooAzure web Node.js, с помощью Web Matrix](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Настройка приложения tooAccess хранилища
toouse хранилища Azure необходимо hello пакет SDK хранилища Azure для Node.js, включающий набор библиотек удобства, взаимодействующих со службами REST hello хранилища.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета
1. Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Unix), перейдите в папку toohello, где создан пример приложения.
2. Тип **npm установить хранилища azure** в командном окне приветствия. Выходные данные команды hello — примерно toohello следующий пример.
 
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

3. Вы можете вручную запустить hello **ls** tooverify команды, **узел\_модули** папка была создана. В этой папке можно найти hello **хранилища azure** пакет, который содержит hello библиотеки, необходимые для доступа к хранилищу.

### <a name="import-hello-package"></a>Импорт пакета hello
С помощью блокнота или другого текстового редактора, добавить hello следующие верхней toohello **server.js** файл приложения hello предполагаемой toouse хранилища:

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
модуль Hello azure будет считывать hello переменных среды AZURE\_ХРАНИЛИЩА\_учетной записи и AZURE\_ХРАНЕНИЯ\_доступа\_ключа или AZURE\_ХРАНЕНИЯ\_подключения \_Строка для tooyour tooconnect сведения, необходимые учетной записи хранилища Azure. Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello при вызове **createQueueService**.

Например, задание переменных среды hello в hello [портала Azure](https://portal.azure.com) на веб-сайт Azure в разделе [Node.js веб-приложения с использованием службы таблиц Azure hello].

## <a name="how-to-create-a-queue"></a>Практическое руководство. Создание очереди
Hello следующий код создает **QueueService** объекта, который позволяет toowork с очередями.

```
var queueSvc = azure.createQueueService();
```

Используйте hello **createQueueIfNotExists** метод, возвращающий hello указанной очереди, если он уже существует, или создает новую очередь с указанным именем hello, если он еще не существует.

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

Если создается очередь hello `result.created` имеет значение true. Если существует очередь hello, `result.created` имеет значение false.

### <a name="filters"></a>Фильтры
Необязательный операции фильтрации может быть применен toooperations, выполняемые с помощью **QueueService**. К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:

```
function handle (requestOptions, next)
```

После выполнения его предварительной обработки параметров запроса hello, метод hello должен toocall «Далее» передача обратный вызов с hello следующие подписи:

```
function (returnObject, finalCallback, next)
```

В этот обратный вызов, а после обработки returnObject hello (hello ответ от сервера toohello hello запроса), обратного вызова hello необходимы tooeither рядом вызова, если он существует toocontinue обработки других фильтров, или просто вызвав finalCallback tooend, в противном случае копирование hello вызов службы.

Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**. Hello следующий код создает **QueueService** объект, который использует hello **ExponentialRetryPolicyFilter**:

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Практическое руководство. Вставка сообщения в очередь
сообщения в очереди, используйте hello tooinsert **createMessage** метод для создания нового сообщения и добавьте его toohello очереди.

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a>Практическое руководство: Просмотр следующего сообщения hello
Можно считывать сообщения hello в hello передней части очереди, не удаляя его из очереди hello, вызывающему Привет **peekMessages** метод. По умолчанию **peekMessages** просматривает одно сообщение.

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

Hello `result` содержит сообщение hello.

> [!NOTE]
> С помощью **peekMessages** Если нет сообщений в очереди hello не будет возвращать ошибку, но сообщения не будут возвращены.
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a>Практическое руководство: Следующее сообщение hello вывода из очереди
Обработка сообщения выполняется двухэтапным процессом:

1. Вывести из очереди сообщение hello.
2. Удалите сообщение hello.

использовать toodequeue сообщение, **getMessages**. Это делает сообщений hello невидимы в очереди hello, чтобы другие клиенты не мог обрабатывать их. После обработки сообщения приложения вызовите **deleteMessage** toodelete его из очереди hello. Следующий пример Hello получает сообщение, а затем удаляет его.

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
> По умолчанию сообщение виден на 30 секунд, после которого он является видимым tooother клиентов. Чтобы задать другое значение, укажите с методом **getMessages** параметр `options.visibilityTimeout`.
> 
> [!NOTE]
> С помощью **getMessages** Если нет сообщений в очереди hello не будет возвращать ошибку, но сообщения не будут возвращены.
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Практическое руководство: Изменение содержимого hello сообщения в очереди
Можно изменить содержимое сообщений на месте в очереди с помощью hello hello **updateMessage**. Следующий пример Hello обновляет hello текст сообщения:

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

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Практическое руководство. Использование дополнительных параметров для удаления сообщений из очереди
Существует два способа настройки извлечения сообщения из очереди:

* `options.numOfMessages`— Получите пакет сообщений (вверх too32.)
* `options.visibilityTimeout` — задает более длительное или короткое время ожидания невидимости.

Hello следующий пример использует hello **getMessages** метод tooget 15 сообщений в одном вызове. Затем он обрабатывает каждое сообщение с помощью цикла for. Он также устанавливает минут toofive hello невидимости времени ожидания для всех сообщений, возвращаемый этим методом.

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

## <a name="how-to-get-hello-queue-length"></a>Практическое руководство: Получение hello длина очереди
Hello **getQueueMetadata** Возвращает метаданные очереди hello, включая hello приблизительное количество сообщений, ожидающих в очереди hello.

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a>Практическое руководство. Получение списка очередей
Список очередей, используйте tooretrieve **listQueuesSegmented**. Список tooretrieve, отфильтрованный по определенным префиксом, используйте **listQueuesSegmentedWithPrefix**.

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

Если все очереди не может быть возвращен, `result.continuationToken` может использоваться как первый параметр hello **listQueuesSegmented** или hello второй параметр **listQueuesSegmentedWithPrefix** tooretrieve дополнительных результатов.

## <a name="how-to-delete-a-queue"></a>Практическое руководство. Удаление очереди
toodelete все сообщения hello и очереди содержащиеся в нем, вызовите метод **deleteQueue** метод hello объекта очереди.

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

использовать все сообщения из очереди, не удаляя его, tooclear **clearMessages**.

## <a name="how-to-work-with-shared-access-signatures"></a>Практическое руководство. Работа с подписанными URL-адресами
Подписи общего доступа (SAS) являются tooqueues детального доступа tooprovide безопасным способом, без указания имени учетной записи хранения или ключи. SAS чаще всего используется tooprovide ограниченный доступ tooyour очереди, например toosubmit сообщения мобильного приложения.

Доверенного приложения, такие как облачная служба создает подписанный URL-адрес с помощью hello **generateSharedAccessSignature** из hello **QueueService**и предоставляет его tooan приложения с частичным доверием или без доверия. Например, мобильному приложению. Hello SAS создается с помощью политики, которая описывает hello начала и окончания в какой hello действует SAS, а также hello владельца SAS уровня toohello предоставленный доступ.

Здравствуйте, следующий пример создает новую политику общего доступа, который позволит hello toohello SAS владельца tooadd сообщений в очереди и истечения срока действия 100 минут после hello время его создания.

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

Обратите внимание, что сведения об узле hello должен предоставляемых также, при необходимости при владельца SAS hello попытке tooaccess hello очереди.

Здравствуйте клиентское приложение, а затем использует hello SAS с **QueueServiceWithSAS** tooperform операций с очередью hello. Следующий пример Hello подключается toohello очереди и создает сообщение.

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

Поскольку hello SAS был сформирован с использованием добавить доступ, если попытка не было внесено tooread, обновления или удаления сообщения, будет возвращена ошибка.

### <a name="access-control-lists"></a>Доступ к спискам управления
Также можно использовать политику доступа hello tooset список управления доступом (ACL) для SAS. Это полезно в том случае, если хотите tooallow очереди hello tooaccess несколько клиентов, но добавлены политики различный уровень доступа для каждого клиента.

ACL реализуется с помощью массива политик доступа, каждая из которых связана со своим идентификатором. Следующий пример Hello определяет две политики; один «user1» и «user2»:

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

Следующий пример возвращает Hello hello текущего списка управления Доступом для **myqueue**, затем добавляет hello новые политики с помощью **setQueueAcl**. Такой подход допускает выполнение:

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

Один раз hello ACL было указано, можно создать на основе кода hello политики SAS. Привет, следующий пример создает новый SAS для «user2»:

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища очередей, выполните эти ссылки toolearn о более сложных задач хранилища.

* Посетите hello [блоге разработчиков хранилища Azure] [блоге разработчиков хранилища Azure].
* Посетите hello [пакет SDK хранилища Azure для узла] [ Azure Storage SDK for Node] репозитория в GitHub.

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
[Создание веб-приложений Node.js в Azure](../../app-service-web/app-service-web-get-started-nodejs.md)   
[Веб-приложение node.js с помощью hello службы таблиц Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
  


[Построение и развертывание tooan приложений Node.js облачной службы Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md)   
[Azure блог группы разработчиков хранилища]: http://blogs.msdn.com/b/windowsazurestorage/ [построение и развертывание приложения tooAzure web Node.js, с помощью Web Matrix]: https://www.microsoft.com/web/webmatrix/   
