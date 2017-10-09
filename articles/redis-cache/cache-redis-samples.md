---
title: "Примеры кэша Redis aaaAzure | Документы Microsoft"
description: "Узнайте, как toouse Redis для Azure кэша"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1f8d210c-ee09-4fe2-b63f-1e69246a27d8
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 5cf9287b577758b5d880d1ca3928c1bee643a8ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-samples"></a>Примеры кэша Redis для Azure
Здесь представлен список образцов кэша Redis для Azure, охватывающие сценариев, таких как подключение tooa кэша, чтения и записи данных tooand из кэша и использование поставщиков кэша Redis ASP.NET hello. Некоторые примеры hello, загружаемые проекты, а некоторые содержат пошаговые инструкции и содержащих фрагменты кода, но не создавать связь tooa загружаемый проект.

## <a name="hello-world-samples"></a>Примеры Hello World
Hello образцы в этом разделе показывают основные принципы hello подключение tooan экземпляр кэша Redis для Azure, чтение и запись кэша toohello данных с помощью различных языков и клиентов Redis.

Hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) образце показано, как tooperform различные операции, используя hello кэша [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) клиент .NET.

В этом примере показано, как:

* использовать различные параметры подключения;
* Чтение и запись объектов tooand из кэша hello, с использованием синхронные и асинхронные операции
* Использует Redis ЧТО/MSET команды tooreturn значения указанных ключей
* выполнять операции транзакций Redis;
* работать со списками и отсортированными наборами Redis;
* хранить объекты .NET с помощью сериализаторов JsonConvert;
* Используйте Redis задает tooimplement тегов
* Работа с кластером Redis

Дополнительные сведения см. в разделе hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) hello в разделе документации на github, а также для нескольких сценариев использования [StackExchange.Redis.Tests](https://github.com/StackExchange/StackExchange.Redis/tree/master/StackExchange.Redis.Tests) модульных тестов.

[Как toouse Redis для Azure кэш с Python](cache-python-get-started.md) показано, как tooget работу с кэша Redis для Azure с помощью Python и hello [redis py](https://github.com/andymccurdy/redis-py) клиента.

[Работа с объектами .NET в кэше hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) показан один из способов tooserialize .NET объекты можно создать их tooand считывает их из экземпляра кэша Redis для Azure. 

## <a name="use-redis-cache-as-a-scale-out-backplane-for-aspnet-signalr"></a>Использование кэша Redis в качестве масштабируемой объединительной панели для ASP.NET SignalR
Hello [использовать кэш Redis масштабируемой объединительной платы для ASP.NET SignalR](https://github.com/rustd/RedisSamples/tree/master/RedisAsSignalRBackplane) образец демонстрирует использование кэша Azure Redis как в объединительной панели SignalR. Дополнительные сведения об объединительной панели см. в разделе [Масштабирование SignalR с помощью Redis](http://www.asp.net/signalr/overview/performance/scaleout-with-redis).

## <a name="redis-cache-customer-query-sample"></a>Пример запроса клиента кэша Redis
Этот пример сравнивает производительность при доступе к данным из кэша и при доступе к данным из хранилища сохраняемости. Этот пример содержит два проекта.

* [Демонстрация повышения производительности путем кэширования данных с помощью кэша Redis](https://github.com/rustd/RedisSamples/tree/master/RedisCacheCustomerQuerySample)
* [Начальное значение hello базы данных и кэш для демонстрации hello](https://github.com/rustd/RedisSamples/tree/master/SeedCacheForCustomerQuerySample)

## <a name="aspnet-session-state-and-output-caching"></a>Состояние сеанса ASP.NET и кэширование вывода
Hello [toostore использование кэша Azure Redis ASP.NET SessionState и OutputCache](https://github.com/rustd/RedisSamples/tree/master/SessionState_OutputCaching) образце показано, как вы toouse кэш Azure Redis toostore сеанс ASP.NET и кэша вывода с помощью hello SessionState и OutputCache поставщиков для Redis.

## <a name="manage-azure-redis-cache-with-maml"></a>Управление кэшем Redis для Azure с помощью MAML
Hello [управления кэша Redis для Azure с помощью библиотеки управления Azure](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) образце показано, как использовать библиотеки управления Azure toomanage - (Создание или обновление или удаление) вашего кэша. 

## <a name="custom-monitoring-sample"></a>Пример настраиваемого мониторинга
Hello [доступа слежения за кэшем Redis данных](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) образце показано, как мониторинга данные доступны для кэша Redis Azure за пределами hello портала Azure.

## <a name="a-twitter-style-clone-written-using-php-and-redis"></a>Приложение в стиле Twitter, написанное с помощью PHP и Redis
Hello [Retwis](https://github.com/SyntaxC4-MSFT/retwis) образец является hello Redis Hello World. Это минимальный клон социальных сетей стиле Twitter написано с помощью Redis и PHP, с помощью hello [Predis](https://github.com/nrk/predis) клиента. Hello исходный код находится спроектированный toobe очень простой и на hello одновременную tooshow различных структур данных Redis.

## <a name="bandwidth-monitor"></a>Монитор пропускной способности
Hello [пропускной способности монитора](https://github.com/JonCole/SampleCode/tree/master/BandWidthMonitor) образец позволяет toomonitor пропускной способности hello используется на клиенте hello. toomeasure hello пропускной способности, запустить образец hello на клиентском компьютере hello кэша, сделать вызовы toohello кэша и наблюдать за пропускной способности hello, сообщаемые монитор образец hello пропускной способности.

