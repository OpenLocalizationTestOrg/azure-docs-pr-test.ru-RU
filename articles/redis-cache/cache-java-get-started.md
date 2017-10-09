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
# <a name="how-toouse-azure-redis-cache-with-java"></a>Как toouse Redis для Azure кэш с Java
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Azure предоставляет кэш Redis доступ tooa выделенный кэш, управляется Майкрософт Redis. Кэш доступен из любого приложения в Microsoft Azure.

В этом разделе рассказывается, как tooget работу с кэша Redis для Azure с помощью Java.

## <a name="prerequisites"></a>Предварительные требования
[Jedis](https://github.com/xetorthio/jedis) — Java-клиент для Redis

В этом учебнике используется Jedis, но можно использовать любой клиент Java из перечисленных на сайте [http://redis.io/clients](http://redis.io/clients).

## <a name="create-a-redis-cache-on-azure"></a>Создание кэша Redis в Azure
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-hello-host-name-and-access-keys"></a>Получить ключи hello узла имя и доступа
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="connect-toohello-cache-securely-using-ssl"></a>Подключение toohello кэша безопасным способом с помощью SSL
Hello последних построений [jedis](https://github.com/xetorthio/jedis) обеспечивают поддержку для подключения tooAzure кэша Redis с использованием SSL. Hello в следующем примере показано, как с помощью кэша Redis tooAzure tooconnect hello 6380 конечную точку SSL. Замените `<name>` с именем hello кэша и `<key>` либо первичный или вторичный ключ как описано в hello предыдущих [получить hello узла имя и ключами доступа](#retrieve-the-host-name-and-access-keys) раздела.

    boolean useSsl = true;
    /* In this line, replace <name> with your cache name: */
    JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */

> [!NOTE]
> Hello не SSL-порт отключен для новых экземпляров кэша Redis для Azure. Если вы используете другой клиент, который не поддерживает SSL, см. раздел [как tooenable hello не SSL-порт](cache-configure.md#access-ports).
> 
> 

## <a name="add-something-toohello-cache-and-retrieve-it"></a>Добавить что-нибудь toohello кэш и извлечь его
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


## <a name="next-steps"></a>Дальнейшие действия
* [Включить диагностику кэша](https://msdn.microsoft.com/library/azure/dn763945.aspx#EnableDiagnostics) так, чтобы [монитор](https://msdn.microsoft.com/library/azure/dn763945.aspx) hello работоспособности кэша.
* Официальные hello чтения [Redis документации](http://redis.io/documentation).
