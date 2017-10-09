---
title: "aaaHow toouse кэша Redis для Azure с Java | Документы Microsoft"
description: "Приступая к работе с кэшем Redis для Azure с использованием Java"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 29275a5e-2e39-4ef2-804f-7ecc5161eab9
ms.service: cache
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 04/13/2017
ms.author: sdanie
ms.openlocfilehash: 7768e879d71f61585b59cf4bd6634ba3f12e001d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache-with-java"></a><span data-ttu-id="0bdf6-103">Как toouse Redis для Azure кэш с Java</span><span class="sxs-lookup"><span data-stu-id="0bdf6-103">How toouse Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0bdf6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0bdf6-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="0bdf6-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0bdf6-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="0bdf6-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="0bdf6-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="0bdf6-107">Java</span><span class="sxs-lookup"><span data-stu-id="0bdf6-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="0bdf6-108">Python</span><span class="sxs-lookup"><span data-stu-id="0bdf6-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="0bdf6-109">Azure предоставляет кэш Redis доступ tooa выделенный кэш, управляется Майкрософт Redis.</span><span class="sxs-lookup"><span data-stu-id="0bdf6-109">Azure Redis Cache gives you access tooa dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="0bdf6-110">Кэш доступен из любого приложения в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0bdf6-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="0bdf6-111">В этом разделе рассказывается, как tooget работу с кэша Redis для Azure с помощью Java.</span><span class="sxs-lookup"><span data-stu-id="0bdf6-111">This topic shows you how tooget started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bdf6-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0bdf6-112">Prerequisites</span></span>
<span data-ttu-id="0bdf6-113">[Jedis](https://github.com/xetorthio/jedis) — Java-клиент для Redis</span><span class="sxs-lookup"><span data-stu-id="0bdf6-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="0bdf6-114">В этом учебнике используется Jedis, но можно использовать любой клиент Java из перечисленных на сайте [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="0bdf6-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="0bdf6-115">Создание кэша Redis в Azure</span><span class="sxs-lookup"><span data-stu-id="0bdf6-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a><span data-ttu-id="0bdf6-116">Получить ключи hello узла имя и доступа</span><span class="sxs-lookup"><span data-stu-id="0bdf6-116">Retrieve hello host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a><span data-ttu-id="0bdf6-117">Подключение toohello кэша безопасным способом с помощью SSL</span><span class="sxs-lookup"><span data-stu-id="0bdf6-117">Connect toohello cache securely using SSL</span></span>
<span data-ttu-id="0bdf6-118">Hello последних построений [jedis](https://github.com/xetorthio/jedis) обеспечивают поддержку для подключения tooAzure кэша Redis с использованием SSL.</span><span class="sxs-lookup"><span data-stu-id="0bdf6-118">hello latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting tooAzure Redis Cache using SSL.</span></span> <span data-ttu-id="0bdf6-119">Hello в следующем примере показано, как с помощью кэша Redis tooAzure tooconnect hello 6380 конечную точку SSL.</span><span class="sxs-lookup"><span data-stu-id="0bdf6-119">hello following example shows how tooconnect tooAzure Redis Cache using hello SSL endpoint of 6380.</span></span> <span data-ttu-id="0bdf6-120">Замените `<name>` с именем hello кэша и `<key>` либо первичный или вторичный ключ как описано в hello предыдущих [получить hello узла имя и ключами доступа](#retrieve-the-host-name-and-access-keys) раздела.</span><span class="sxs-lookup"><span data-stu-id="0bdf6-120">Replace `<name>` with hello name of your cache and `<key>` with either your primary or secondary key as described in hello previous [Retrieve hello host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="0bdf6-121">Hello не SSL-порт отключен для новых экземпляров кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="0bdf6-121">hello non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="0bdf6-122">Если вы используете другой клиент, который не поддерживает SSL, см. раздел [как tooenable hello не SSL-порт](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="0bdf6-122">If you are using a different client that doesn't support SSL, see [How tooenable hello non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a><span data-ttu-id="0bdf6-123">Добавить что-нибудь toohello кэш и извлечь его</span><span class="sxs-lookup"><span data-stu-id="0bdf6-123">Add something toohello cache and retrieve it</span></span>
    package com.mycompany.app;
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisShardInfo;

    public class App
    {
      public static void main( String[] args )
      {
        boolean useSsl = true;
        /* In this line, replace <name> with your cache name: */
        JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
        shardInfo.setPassword("<key>"); /* Use your access key. */
        Jedis jedis = new Jedis(shardInfo);
        jedis.set("foo", "bar");
        String value = jedis.get("foo");
      }
    }


## <a name="next-steps"></a><span data-ttu-id="0bdf6-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bdf6-124">Next steps</span></span>
* <span data-ttu-id="0bdf6-125">[Включить диагностику кэша](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) так, чтобы [монитор](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello работоспособности кэша.</span><span class="sxs-lookup"><span data-stu-id="0bdf6-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello health of your cache.</span></span>
* <span data-ttu-id="0bdf6-126">Официальные hello чтения [Redis документации](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="0bdf6-126">Read hello official [Redis documentation](http://redis.io/documentation).</span></span>
