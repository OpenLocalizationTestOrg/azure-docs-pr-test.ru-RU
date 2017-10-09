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
# <a name="how-toouse-azure-redis-cache-with-nodejs"></a><span data-ttu-id="8005e-103">Как toouse Redis для Azure кэш с Node.js</span><span class="sxs-lookup"><span data-stu-id="8005e-103">How toouse Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8005e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8005e-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="8005e-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8005e-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="8005e-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="8005e-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="8005e-107">Java</span><span class="sxs-lookup"><span data-stu-id="8005e-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="8005e-108">Python</span><span class="sxs-lookup"><span data-stu-id="8005e-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="8005e-109">Azure кэша Redis предоставляет доступ к tooa безопасного выделенному кэшу Redis, управляемый корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="8005e-109">Azure Redis Cache gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="8005e-110">Кэш доступен из любого приложения в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8005e-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="8005e-111">В этом разделе рассказывается, как tooget работу с кэша Redis для Azure с помощью Node.js.</span><span class="sxs-lookup"><span data-stu-id="8005e-111">This topic shows you how tooget started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="8005e-112">Еще один пример использования кэша Redis для Azure с Node.js см. в статье [Создание приложения для разговоров на Node.js с использованием Socket.IO в службе приложений Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="8005e-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8005e-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8005e-113">Prerequisites</span></span>
<span data-ttu-id="8005e-114">Установите [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="8005e-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="8005e-115">В этом руководстве используется [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="8005e-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="8005e-116">Примеры использования других клиентов Node.js документации hello отдельных клиентов Node.js hello, перечисленных в [клиентов Node.js Redis](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="8005e-116">For examples of using other Node.js clients, see hello individual documentation for hello Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="8005e-117">Создание кэша Redis в Azure</span><span class="sxs-lookup"><span data-stu-id="8005e-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="8005e-118">Получить ключи hello узла имя и доступа</span><span class="sxs-lookup"><span data-stu-id="8005e-118">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="8005e-119">Подключение toohello кэша безопасным способом с помощью SSL</span><span class="sxs-lookup"><span data-stu-id="8005e-119">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="8005e-120">Hello последних построений [node_redis](https://github.com/mranney/node_redis) обеспечивают поддержку для подключения tooAzure кэша Redis с использованием SSL.</span><span class="sxs-lookup"><span data-stu-id="8005e-120">hello latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="8005e-121">Hello в следующем примере показано, как с помощью кэша Redis tooAzure tooconnect hello 6380 конечную точку SSL.</span><span class="sxs-lookup"><span data-stu-id="8005e-121">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="8005e-122">Замените `<name>` с именем hello кэша и `<key>` либо первичный или вторичный ключ как описано в hello предыдущих [получить hello узла имя и ключами доступа](#retrieve-the-host-name-and-access-keys) раздела.</span><span class="sxs-lookup"><span data-stu-id="8005e-122">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="8005e-123">Hello не SSL-порт отключен для новых экземпляров кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="8005e-123">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="8005e-124">Если вы используете другой клиент, который не поддерживает SSL, см. раздел [как tooenable hello не SSL-порт](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="8005e-124">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="8005e-125">Добавить что-нибудь toohello кэш и извлечь его</span><span class="sxs-lookup"><span data-stu-id="8005e-125">Add something toohello cache and retrieve it</span></span>
<span data-ttu-id="8005e-126">Следующий пример показывает, как tooconnect tooan redis для Azure — кэш экземпляра, хранения и получить элемент из кэша hello Hello.</span><span class="sxs-lookup"><span data-stu-id="8005e-126">hello following example shows you how tooconnect tooan Azure Redis Cache instance, and store and retrieve an item from hello cache.</span></span> <span data-ttu-id="8005e-127">Дополнительные примеры использования Redis с hello [node_redis](https://github.com/mranney/node_redis) клиента, в разделе [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="8005e-127">For more examples of using Redis with hello [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="8005e-128">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8005e-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="8005e-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8005e-129">Next steps</span></span>
* <span data-ttu-id="8005e-130">[Включить диагностику кэша](cache-how-to-monitor.md#enable-cache-diagnostics) так, чтобы [монитор](cache-how-to-monitor.md) hello работоспособности кэша.</span><span class="sxs-lookup"><span data-stu-id="8005e-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span>
* <span data-ttu-id="8005e-131">Официальные hello чтения [Redis документации](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="8005e-131">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>

