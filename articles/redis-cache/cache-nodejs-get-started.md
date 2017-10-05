---
title: "Использование кэша Redis для Azure с Node.js | Документация Майкрософт"
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
ms.openlocfilehash: 530191637b1aa91ee1d7fe5b5bb032c60983f7dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-nodejs"></a><span data-ttu-id="8183d-103">Использование кэша Redis для Azure с Node.js</span><span class="sxs-lookup"><span data-stu-id="8183d-103">How to use Azure Redis Cache with Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8183d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8183d-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="8183d-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8183d-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="8183d-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="8183d-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="8183d-107">Java</span><span class="sxs-lookup"><span data-stu-id="8183d-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="8183d-108">Python</span><span class="sxs-lookup"><span data-stu-id="8183d-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="8183d-109">Кэш Redis для Azure дает доступ к защищенному выделенному кэшу Redis, управляемому Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="8183d-109">Azure Redis Cache gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="8183d-110">Кэш доступен из любого приложения в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8183d-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="8183d-111">В этой статье показано, как приступить к работе с кэшем Redis для Azure, используя Node.js.</span><span class="sxs-lookup"><span data-stu-id="8183d-111">This topic shows you how to get started with Azure Redis Cache using Node.js.</span></span> <span data-ttu-id="8183d-112">Еще один пример использования кэша Redis для Azure с Node.js см. в статье [Создание приложения для разговоров на Node.js с использованием Socket.IO в службе приложений Azure](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span><span class="sxs-lookup"><span data-stu-id="8183d-112">For another example of using Azure Redis Cache with Node.js, see [Build a Node.js Chat Application with Socket.IO on an Azure Website](../app-service-web/web-sites-nodejs-chat-app-socketio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8183d-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8183d-113">Prerequisites</span></span>
<span data-ttu-id="8183d-114">Установите [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="8183d-114">Install [node_redis](https://github.com/mranney/node_redis):</span></span>

    npm install redis

<span data-ttu-id="8183d-115">В этом руководстве используется [node_redis](https://github.com/mranney/node_redis).</span><span class="sxs-lookup"><span data-stu-id="8183d-115">This tutorial uses [node_redis](https://github.com/mranney/node_redis).</span></span> <span data-ttu-id="8183d-116">Примеры использования других клиентов Node.js см. в отдельных документах по [клиентам Node.js для Redis](http://redis.io/clients#nodejs).</span><span class="sxs-lookup"><span data-stu-id="8183d-116">For examples of using other Node.js clients, see the individual documentation for the Node.js clients listed at [Node.js Redis clients](http://redis.io/clients#nodejs).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="8183d-117">Создание кэша Redis в Azure</span><span class="sxs-lookup"><span data-stu-id="8183d-117">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="8183d-118">Получение имени узла и ключей доступа</span><span class="sxs-lookup"><span data-stu-id="8183d-118">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="8183d-119">Безопасное подключение к кэшу с помощью SSL</span><span class="sxs-lookup"><span data-stu-id="8183d-119">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="8183d-120">Новейшие сборки [node_redis](https://github.com/mranney/node_redis) обеспечивают поддержку подключения к кэшу Redis для Azure по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="8183d-120">The latest builds of [node_redis](https://github.com/mranney/node_redis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="8183d-121">В приведенном ниже примере показано, как подключиться к кэшу Redis для Azure с помощью конечной точки SSL на порту 6380.</span><span class="sxs-lookup"><span data-stu-id="8183d-121">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="8183d-122">Подставьте вместо `<name>` имя своего кэша, а вместо `<key>` — первичный или вторичный ключ, как описано в предыдущем разделе [Получение имени узла и ключей доступа](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="8183d-122">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

> [!NOTE]
> <span data-ttu-id="8183d-123">Порт без SSL отключен для новых экземпляров кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="8183d-123">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="8183d-124">Если вы используете другой клиент, не поддерживающий SSL, см. сведения в разделе [Порты доступа](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="8183d-124">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="8183d-125">Добавление данных в кэш и их извлечение</span><span class="sxs-lookup"><span data-stu-id="8183d-125">Add something to the cache and retrieve it</span></span>
<span data-ttu-id="8183d-126">В следующем примере показано, как подключиться к экземпляру кэша Redis для Azure, а также как сохранить и извлечь элемент из кэша.</span><span class="sxs-lookup"><span data-stu-id="8183d-126">The following example shows you how to connect to an Azure Redis Cache instance, and store and retrieve an item from the cache.</span></span> <span data-ttu-id="8183d-127">Дополнительные примеры использования Redis с клиентом [node_redis](https://github.com/mranney/node_redis) см. на странице [http://redis.js.org/](http://redis.js.org/).</span><span class="sxs-lookup"><span data-stu-id="8183d-127">For more examples of using Redis with the [node_redis](https://github.com/mranney/node_redis) client, see [http://redis.js.org/](http://redis.js.org/).</span></span>

     var redis = require("redis");

      // Add your cache name and access key.
    var client = redis.createClient(6380,'<name>.redis.cache.windows.net', {auth_pass: '<key>', tls: {servername: '<name>.redis.cache.windows.net'}});

    client.set("key1", "value", function(err, reply) {
            console.log(reply);
        });

    client.get("key1",  function(err, reply) {
            console.log(reply);
        });

<span data-ttu-id="8183d-128">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8183d-128">Output:</span></span>

    OK
    value


## <a name="next-steps"></a><span data-ttu-id="8183d-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8183d-129">Next steps</span></span>
* <span data-ttu-id="8183d-130">[Включите диагностику кэша](cache-how-to-monitor.md#enable-cache-diagnostics), чтобы можно было [наблюдать](cache-how-to-monitor.md) за работоспособностью кэша.</span><span class="sxs-lookup"><span data-stu-id="8183d-130">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span>
* <span data-ttu-id="8183d-131">Прочитайте официальную [документацию Redis](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="8183d-131">Read the official [Redis documentation](http://redis.io/documentation).</span></span>

