---
title: "aaaHow tooconfigure Redis кластеризации для кэша Redis Azure Premium | Документы Microsoft"
description: "Узнайте, как toocreate и управления ими кластеризации для повышенного уровня экземпляров кэша Redis для Azure Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 62208eec-52ae-4713-b077-62659fd844ab
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 44d520facb9d1af145b69f1b58f082aabb655d4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-redis-clustering-for-a-premium-azure-redis-cache"></a>Как tooconfigure Redis кластеризации для кэша Redis Azure Premium
Кэш Azure Redis имеет разные предложения кэша, которые обеспечивают гибкость при hello Выбор размера кэша и функций, включая возможности уровня Premium кластеризации, сохраняемости и поддержки виртуальной сети. В этой статье описывается, как tooconfigure кластеризации в расширенной Azure Redis кэш экземпляра.

Сведения о других функций кэша premium см. в разделе [уровня Premium кэша Redis Azure введение toohello](cache-premium-tier-intro.md).

## <a name="what-is-redis-cluster"></a>Что такое кластер Redis?
Кэш Redis для Azure предлагает кластер Redis в том виде, как это [реализовано в Redis](http://redis.io/topics/cluster-tutorial). С помощью Redis кластера можно получить следующие преимущества hello: 

* Hello tooautomatically возможность разделить набор данных между несколькими узлами. 
* Hello возможность toocontinue операций при подмножество узлов hello возникли сбои или являются не удается toocommunicate с остальной hello hello кластера. 
* Более высокая пропускная способность: пропускная способность линейно увеличивается по мере увеличения hello количество сегментов. 
* Дополнительные объем памяти: линейно возрастает по мере увеличения hello количество сегментов.  

Дополнительные сведения о размере, пропускной способности и полосе пропускания для кэшей уровня "Премиум" см. в разделе [Какое предложение и размер кэша Redis нужно использовать?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)

В Azure кластере Redis предлагается как первичный и реплика модели, где каждый сегмент имеет пару первичный/реплика с репликацией где репликации hello управляется службой кэша Azure Redis. 

## <a name="clustering"></a>Кластеризация
Hello включена кластеризация **новый кэш Redis** колонке во время создания кэша. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Кластеризация настраивается на hello **Redis кластера** колонку.

![Кластеризация][redis-cache-clustering]

Можно создать до too10 сегментов в кластере hello. Нажмите кнопку **включено** и передвиньте ползунок hello, или введите число от 1 до 10 для **количества сегментов** и нажмите кнопку **ОК**.

Каждый сегмент — это пара кэша первичный/реплика, управляет Azure и общий размер кэша hello hello вычисляется путем умножения на размер кэша hello, выбранного в ценовой категории hello hello количество сегментов. 

![Кластеризация][redis-cache-clustering-selected]

После создания кэша hello подключения tooit и используется только как кэш некластеризованных и Redis распределяет данные hello в сегменты кэша hello. Если Диагностика [включен](cache-how-to-monitor.md#enable-cache-diagnostics), метрики записываются отдельно для каждого сегмента и может быть [просмотреть](cache-how-to-monitor.md) в колонку кэша Redis hello. 

> [!NOTE]
> 
> Существует ряд незначительных отличий, необходимых в клиентском приложении для настройки кластеризации. Дополнительные сведения см. в разделе [необходимо toomake любые изменения toomy клиентского приложения toouse кластеризации?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 

Пример кода по работе с кластером с клиента StackExchange.Redis hello, в разделе hello [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) часть hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) образца.

<a name="cluster-size"></a>

## <a name="change-hello-cluster-size-on-a-running-premium-cache"></a>Изменение размера hello кластера, на котором установлена кэша premium
размер кластера hello toochange на выполнение расширенной кэш с кластеризации включено, щелкните **Redis размер кластера** из hello **ресурсов меню**.

> [!NOTE]
> Хотя hello Azure Redis кэша Premium уровня был выпущен tooGeneral доступности, hello Redis размер кластера компонент в настоящий момент в режиме предварительного просмотра.
> 
> 

![Размер кластера Redis][redis-cache-redis-cluster-size]

размер кластера toochange hello, используйте ползунок hello, или введите число от 1 до 10 в hello **количества сегментов** текстовое поле и нажмите кнопку **ОК** toosave.

> [!NOTE]
> Масштабирование на кластере выполняется hello [МИГРАЦИИ](https://redis.io/commands/migrate) команду, которая является ресурсоемким, поэтому для минимальное влияние рассмотрите возможность выполнения этой операции во время нерабочего времени. Во время процесса миграции hello будет отмечен пик в нагрузки сервера. Масштабирование кластера long запущен процесс и hello длительность зависит от числа hello ключей и размера hello значения, связанные с этими ключами.
> 
> 

## <a name="clustering-faq"></a>Часто задаваемые вопросы по кластеризации
Hello следующий список содержит toocommonly ответы, вопросы и ответы о кластеризации кэша Redis для Azure.

* [Зачем мне toomake любые изменения toomy клиентского приложения toouse кластеризации?](#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
* [Распределение ключей в кластере](#how-are-keys-distributed-in-a-cluster)
* [Что такое размер кэша наибольшее hello, которые я могу создать?](#what-is-the-largest-cache-size-i-can-create)
* [Все ли клиенты Redis поддерживают кластеризацию?](#do-all-redis-clients-support-clustering)
* [Как подключаться toomy кэша, если включена кластеризация?](#how-do-i-connect-to-my-cache-when-clustering-is-enabled)
* [Можно напрямую подключить отдельные сегменты toohello Мой кэша?](#can-i-directly-connect-to-the-individual-shards-of-my-cache)
* [Можно ли настроить кластеризацию для ранее созданного кэша?](#can-i-configure-clustering-for-a-previously-created-cache)
* [Можно ли настроить кластеризацию для кэша уровней Базовый и Стандартный?](#can-i-configure-clustering-for-a-basic-or-standard-cache)
* [Можно ли использовать кластеризации с поставщиками состояний сеансов ASP.NET Redis и кэширования вывода hello](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)
* [При использовании StackExchange.Redis и кластеризации порождаются исключения MOVE. Что делать?](#i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do)

### <a name="do-i-need-toomake-any-changes-toomy-client-application-toouse-clustering"></a>Зачем мне toomake любые изменения toomy клиентского приложения toouse кластеризации?
* Если кластеризация включена, доступна только база данных 0. Если клиентское приложение использует несколько баз данных, и она попытается tooread или записи базы данных tooa, отличное от 0, hello следующие исключения. `Unhandled Exception: StackExchange.Redis.RedisConnectionException: ProtocolFailure on GET --->` `StackExchange.Redis.RedisCommandException: Multiple databases are not supported on this server; cannot switch toodatabase: 6`
  
  Дополнительные сведения см. в разделе "Implemented subset" (Реализованное подмножество) статьи [Redis Cluster Specification](http://redis.io/topics/cluster-spec#implemented-subset) (Спецификация кластера Redis).
* Если вы используете клиент [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/), необходимо установить версию 1.0.481 или более позднюю. Подключение toohello кэша с помощью hello же [конечных точек, порты и ключи](cache-configure.md#properties) , используемый при соединении tooa кэша, у которого нет кластеризации включена. Hello единственное отличие заключается в том, что все операции чтения и записи должны выполняться toodatabase 0.
  
  * Требования других клиентов могут отличаться. Ознакомьтесь с разделом [Все ли клиенты Redis поддерживают кластеризацию?](#do-all-redis-clients-support-clustering)
* Если приложение использует несколько операций с ключом объединены в одну команду, все ключи должны находиться в hello же сегментов. ключи toolocate в hello же сегментов см. в разделе [ключи распределение в кластере?](#how-are-keys-distributed-in-a-cluster)
* Если вы используете поставщик состояний сеансов ASP.NET Redis, вам необходимо установить версию 2.0.1 или более позднюю версию. В разделе [используется кластеризация с поставщиками состояний сеансов ASP.NET Redis и кэширования вывода hello?](#can-i-use-clustering-with-the-redis-aspnet-session-state-and-output-caching-providers)

### <a name="how-are-keys-distributed-in-a-cluster"></a>Распределение ключей в кластере
На hello Redis [модели распространения ключей](http://redis.io/topics/cluster-spec#keys-distribution-model) документации: клавиша "пробел" hello разбивается на 16384 слотов. Каждый ключ является хэшируются и назначенный tooone эти слотов, которые распределены между узлами hello hello кластера. Настраивается хэшированных tooensure, которые находятся несколько ключей, в какие входит ключ hello hello же сегментов с помощью тегов хэш.

* Ключи с тегом хэш - Если заключен в любой части ключа hello `{` и `}`, только эту часть ключа hello хэшируется для целей hello определения hello слот хэш ключа. Например, следующие 3 ключи hello будут размещены в hello же сегментов: `{key}1`, `{key}2`, и `{key}3` с момента только hello `key` часть имени hello хэшируется. Полный список спецификаций для хэш-тегов ключей см. в разделе [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags) (Хэш-теги ключей).
* Ключи без тега хэш - hello весь раздел используется для хэширования. В результате статистически равномерное распределение по сегментам hello hello кэша.

Для оптимальной производительности и пропускной способности рекомендуется равномерно распределить hello ключей. При использовании ключей с тегом хэш это приложение hello ответственности tooensure hello ключи распределяются равномерно.

Дополнительные сведения см. в разделах [Keys distribution model](http://redis.io/topics/cluster-spec#keys-distribution-model) (Модель распределения ключей), [Redis Cluster data sharding](http://redis.io/topics/cluster-tutorial#redis-cluster-data-sharding) (Сегментирование данных в кластере Redis) и [Keys hash tags](http://redis.io/topics/cluster-spec#keys-hash-tags) (Хэш-теги ключей).

Пример кода по работе с кластеризацией и Поиск ключей в hello hello см же сегментировать данные с помощью клиента StackExchange.Redis hello, [clustering.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/Clustering.cs) часть hello [Hello World](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) образца.

### <a name="what-is-hello-largest-cache-size-i-can-create"></a>Что такое размер кэша наибольшее hello, которые я могу создать?
Hello наибольший размер кэша premium — 53 ГБ. Можно создать копию too10 сегментов, предоставляя максимальный размер 530 ГБ. Если требуется больший размер, вы можете [отправить запрос на получение дополнительного места](mailto:wapteams@microsoft.com?subject=Redis%20Cache%20quota%20increase). Подробные сведения см. на странице [Цены на кэш Redis для Azure](https://azure.microsoft.com/pricing/details/cache/).

### <a name="do-all-redis-clients-support-clustering"></a>Все ли клиенты Redis поддерживают кластеризацию?
В hello в настоящее время поддерживают не все клиенты Redis кластеризации. Например, ее не поддерживает StackExchange.Redis. Дополнительные сведения о других клиентов см. в разделе hello [воспроизведение с кластером hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) раздел hello [Redis кластера учебника](http://redis.io/topics/cluster-tutorial).

> [!NOTE]
> При использовании StackExchange.Redis в качестве клиента убедитесь в использовании hello последнюю версию [StackExchange.Redis](https://www.nuget.org/packages/StackExchange.Redis/) 1.0.481 или более поздней версии для кластеризации toowork правильно. При возникновении проблем с исключениями MOVE ознакомьтесь с дополнительными сведениями [здесь](#move-exceptions).
> 
> 

### <a name="how-do-i-connect-toomy-cache-when-clustering-is-enabled"></a>Как подключаться toomy кэша, если включена кластеризация?
Tooyour кэша можно подключиться с помощью hello же [конечные точки](cache-configure.md#properties), [порты](cache-configure.md#properties), и [ключей](cache-configure.md#access-keys) , используемый при соединении tooa кэша, у которого нет кластеризации включена. Redis управляет hello кластеризации hello серверную часть, поэтому не нужно toomanage его из клиента.

### <a name="can-i-directly-connect-toohello-individual-shards-of-my-cache"></a>Можно напрямую подключить отдельные сегменты toohello Мой кэша?
Официально это не поддерживается. Тем не менее каждый сегмент включает пару, которая включает основной кэш и его реплику и называется экземпляром кэша. Можно подключиться с помощью служебной программы redis cli hello в hello экземпляров кэша toothese [работает нестабильно](http://redis.io/download) ветви hello Redis репозитория в GitHub. Эта версия реализует базовую поддержку при работе с hello `-c` переключения. Дополнительные сведения см. [воспроизведение с кластером hello](http://redis.io/topics/cluster-tutorial#playing-with-the-cluster) на [http://redis.io](http://redis.io) в hello [Redis кластера учебника](http://redis.io/topics/cluster-tutorial).

Для не ssl используйте следующие команды hello.

    Redis-cli.exe –h <<cachename>> -p 13000 (tooconnect tooinstance 0)
    Redis-cli.exe –h <<cachename>> -p 13001 (tooconnect tooinstance 1)
    Redis-cli.exe –h <<cachename>> -p 13002 (tooconnect tooinstance 2)
    ...
    Redis-cli.exe –h <<cachename>> -p 1300N (tooconnect tooinstance N)

Для SSL замените `1300N` на `1500N`.

### <a name="can-i-configure-clustering-for-a-previously-created-cache"></a>Можно ли настроить кластеризацию для ранее созданного кэша?
В настоящее время включить кластеризацию можно только при создании кэша. Размер кластера hello можно изменить после создания кэша hello, но нельзя добавлять кластеризации кэша premium tooa или удалить кластер из кэша premium после создания кэша hello. Кэша premium с включенной кластеризацией и только одного сегмента отличается от кэша premium hello такого же размера, с без кластеризации.

### <a name="can-i-configure-clustering-for-a-basic-or-standard-cache"></a>Можно ли настроить кластеризацию для кэша уровней Базовый и Стандартный?
Кластеризация доступна только для кэша уровня Премиум.

### <a name="can-i-use-clustering-with-hello-redis-aspnet-session-state-and-output-caching-providers"></a>Можно ли использовать кластеризации с поставщиками состояний сеансов ASP.NET Redis и кэширования вывода hello
* **Поставщик кэша вывода Redis** — изменения не требуются.
* **Поставщик состояния сеанса redis** -toouse кластеризации, необходимо использовать [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 или более поздней версии или исключение возникает исключение. Это критическое изменение. Дополнительные сведения см. на странице [v2.0.0 Breaking Change Details](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details) (Подробные сведения о критических изменениях в версии 2.0.0).

<a name="move-exceptions"></a>

### <a name="i-am-getting-move-exceptions-when-using-stackexchangeredis-and-clustering-what-should-i-do"></a>При использовании StackExchange.Redis и кластеризации порождаются исключения MOVE. Что делать?
Если вы применяете StackExchange.Redis и получаете исключения `MOVE` при кластеризации, убедитесь, что вы используете [StackExchange.Redis 1.1.603](https://www.nuget.org/packages/StackExchange.Redis/) или более позднюю версию. Инструкции по настройке вашей toouse приложений .NET StackExchange.Redis см. в разделе [Настройка клиентов кэша hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

## <a name="next-steps"></a>Дальнейшие действия
Узнайте, как toouse более "премиум" кэша функции.

* [Уровень Premium кэша Redis Azure toohello введение](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-clustering]: ./media/cache-how-to-premium-clustering/redis-cache-clustering.png

[redis-cache-clustering-selected]: ./media/cache-how-to-premium-clustering/redis-cache-clustering-selected.png

[redis-cache-redis-cluster-size]: ./media/cache-how-to-premium-clustering/redis-cache-redis-cluster-size.png







