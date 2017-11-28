---
title: "Как использовать кэш Redis для Azure с Java | Документация Майкрософт"
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
ms.openlocfilehash: 3cfad3a7279b5f9bbff1e6cd9794c492e3544752
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-redis-cache-with-java"></a><span data-ttu-id="ac564-103">Использование кэша Redis для Azure с Java</span><span class="sxs-lookup"><span data-stu-id="ac564-103">How to use Azure Redis Cache with Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac564-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ac564-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="ac564-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ac564-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="ac564-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ac564-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="ac564-107">Java</span><span class="sxs-lookup"><span data-stu-id="ac564-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="ac564-108">Python</span><span class="sxs-lookup"><span data-stu-id="ac564-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="ac564-109">Кэш Redis для Azure дает доступ к выделенному кэшу Redis, управляемому Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ac564-109">Azure Redis Cache gives you access to a dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="ac564-110">Кэш доступен из любого приложения в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ac564-110">Your cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="ac564-111">В этом разделе показано, как приступить к работе с кэшем Redis для Azure, используя Java.</span><span class="sxs-lookup"><span data-stu-id="ac564-111">This topic shows you how to get started with Azure Redis Cache using Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac564-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ac564-112">Prerequisites</span></span>
<span data-ttu-id="ac564-113">[Jedis](https://github.com/xetorthio/jedis) — Java-клиент для Redis</span><span class="sxs-lookup"><span data-stu-id="ac564-113">[Jedis](https://github.com/xetorthio/jedis) - Java client for Redis</span></span>

<span data-ttu-id="ac564-114">В этом учебнике используется Jedis, но можно использовать любой клиент Java из перечисленных на сайте [http://redis.io/clients](http://redis.io/clients).</span><span class="sxs-lookup"><span data-stu-id="ac564-114">This tutorial uses Jedis, but you can use any Java client listed at [http://redis.io/clients](http://redis.io/clients).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="ac564-115">Создание кэша Redis в Azure</span><span class="sxs-lookup"><span data-stu-id="ac564-115">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="ac564-116">Получение имени узла и ключей доступа</span><span class="sxs-lookup"><span data-stu-id="ac564-116">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-to-the-cache-securely-using-ssl"></a><span data-ttu-id="ac564-117">Безопасное подключение к кэшу с помощью SSL</span><span class="sxs-lookup"><span data-stu-id="ac564-117">Connect to the cache securely using SSL</span></span>
<span data-ttu-id="ac564-118">Новейшие сборки [jedis](https://github.com/xetorthio/jedis) обеспечивают поддержку подключения к кэшу Redis для Azure по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="ac564-118">The latest builds of [jedis](https://github.com/xetorthio/jedis) provide support for connecting to Azure Redis Cache using SSL.</span></span> <span data-ttu-id="ac564-119">В приведенном ниже примере показано, как подключиться к кэшу Redis для Azure с помощью конечной точки SSL на порту 6380.</span><span class="sxs-lookup"><span data-stu-id="ac564-119">The following example shows how to connect to Azure Redis Cache using the SSL endpoint of 6380.</span></span> <span data-ttu-id="ac564-120">Подставьте вместо `<name>` имя своего кэша, а вместо `<key>` — первичный или вторичный ключ, как описано в предыдущем разделе [Получение имени узла и ключей доступа](#retrieve-the-host-name-and-access-keys).</span><span class="sxs-lookup"><span data-stu-id="ac564-120">Replace `<name>` with the name of your cache and `<key>` with either your primary or secondary key as described in the previous [Retrieve the host name and access keys](#retrieve-the-host-name-and-access-keys) section.</span></span>

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> <span data-ttu-id="ac564-121">Порт без SSL отключен для новых экземпляров кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="ac564-121">The non-SSL port is disabled for new Azure Redis Cache instances.</span></span> <span data-ttu-id="ac564-122">Если вы используете другой клиент, не поддерживающий SSL, см. сведения в разделе [Порты доступа](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="ac564-122">If you are using a different client that doesn't support SSL, see [How to enable the non-SSL port](cache-configure.md#access-ports).</span></span>
> 
> 

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="ac564-123">Добавление данных в кэш и их извлечение</span><span class="sxs-lookup"><span data-stu-id="ac564-123">Add something to the cache and retrieve it</span></span>
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


## <a name="next-steps"></a><span data-ttu-id="ac564-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac564-124">Next steps</span></span>
* <span data-ttu-id="ac564-125">[Включите диагностику кэша](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics), чтобы можно было [наблюдать](https://msdn.microsoft.com/library/azure/dn763945.aspx) за работоспособностью кэша.</span><span class="sxs-lookup"><span data-stu-id="ac564-125">[Enable cache diagnostics](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) so you can [monitor](https://msdn.microsoft.com/library/azure/dn763945.aspx) the health of your cache.</span></span>
* <span data-ttu-id="ac564-126">Прочитайте официальную [документацию Redis](http://redis.io/documentation).</span><span class="sxs-lookup"><span data-stu-id="ac564-126">Read the official [Redis documentation](http://redis.io/documentation).</span></span>
