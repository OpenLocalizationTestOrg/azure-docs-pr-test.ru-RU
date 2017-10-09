---
title: "aaaHow toouse кэша Redis с Node.js | Документы Microsoft"
description: "Начните работу с кэшем Redis для Azure с использованием Node.js и node_redis."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: 06fddc95-8029-4a8d-83f5-ebd5016891d9
ms.service: cache
ms.devlang: nodejs
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: dc8732041d2c4e5793e684e0c80b87a1c9d17f34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a>Как toouse Redis для Azure кэш с Node.js
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure кэша Redis предоставляет доступ к tooa безопасного выделенному кэшу Redis, управляемый корпорацией Майкрософт. Кэш доступен из любого приложения в Microsoft Azure.

В этом разделе рассказывается, как tooget работу с кэша Redis для Azure с помощью Node.js. Еще один пример использования кэша Redis для Azure с Node.js см. в статье [Создание приложения для разговоров на Node.js с использованием Socket.IO в службе приложений Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).

## <a name="prerequisites"></a>Предварительные требования
Установите [node_redis](https://github.com/mranney/node_redis).

    npm install redis

В этом руководстве используется [node_redis](https://github.com/mranney/node_redis). Примеры использования других клиентов Node.js документации hello отдельных клиентов Node.js hello, перечисленных в [клиентов Node.js Redis](http://redis.io/clients#nodejs).

## <a name="create-a-redis-cache-on-azure"></a>Создание кэша Redis в Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Получить ключи hello узла имя и доступа
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Подключение toohello кэша безопасным способом с помощью SSL
Hello последних построений [node_redis](https://github.com/mranney/node_redis) обеспечивают поддержку для подключения tooAzure кэша Redis с использованием SSL. Hello в следующем примере показано, как с помощью кэша Redis tooAzure tooconnect hello 6380 конечную точку SSL. Замените `<name>` с именем hello кэша и `<key>` либо первичный или вторичный ключ как описано в hello предыдущих [получить hello узла имя и ключами доступа](#retrieve-the-host-name-and-access-keys) раздела.

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> Hello не SSL-порт отключен для новых экземпляров кэша Redis для Azure. Если вы используете другой клиент, который не поддерживает SSL, см. раздел [как tooenable hello не SSL-порт](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Добавить что-нибудь toohello кэш и извлечь его
Следующий пример показывает, как tooconnect tooan redis для Azure — кэш экземпляра, хранения и получить элемент из кэша hello Hello. Дополнительные примеры использования Redis с hello [node_redis](https://github.com/mranney/node_redis) клиента, в разделе [http://redis.js.org/](http://redis.js.org/).

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

Выходные данные:

    OK
    value


## <a name="next-steps"></a>Дальнейшие действия
* [Включить диагностику кэша](cache-how-to-monitor.md#enable-cache-diagnostics) так, чтобы [монитор](cache-how-to-monitor.md) hello работоспособности кэша.
* Официальные hello чтения [Redis документации](http://redis.io/documentation).

