---
title: "aaaMigrate tooRedis управляемой службы кэша приложений - Azure | Документы Microsoft"
description: "Узнайте, как toomigrate управляемой службы кэша и кэша в роли приложения tooAzure кэша Redis"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 041f077b-8c8e-4d7c-a3fc-89d334ed70d6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/30/2017
ms.author: sdanie
ms.openlocfilehash: bd81722820acf0d2637828fbb6100c723aafeba5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-managed-cache-service-tooazure-redis-cache"></a>Миграция из управляемой службы кэша tooAzure кэша Redis
Миграция приложений, использующих tooAzure управляемой службы кэша Azure Redis кэша может быть выполнено с минимальными изменениями tooyour приложения, в зависимости от используемых в приложении кэширования функций hello управляемой службы кэша. Hello API-интерфейсы, немного hello же они похожи и большая часть существующего кода, использующего управляемой службы кэша tooaccess кэша может быть использован с минимальными изменениями. В этом разделе показано, как toomake hello необходимой конфигурации и приложения изменяется toomigrate toouse приложений к управляемой службы кэша Azure Redis Cache и показано, как некоторые из функций hello кэша Redis для Azure можно используется tooimplement функции hello кэша управляемой службы кэша.

>[!NOTE]
>Использование управляемой службы кэша и кэша роли [прекращено](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/) 30 ноября 2016 г. При наличии нужных toomigrate tooAzure кэша Redis развертывания кэша в роли, можно выполнить действия hello в этой статье.

## <a name="migration-steps"></a>Этапы миграции
Привет, выполнив действия, необходимые toomigrate toouse приложения управляемой службы кэша Azure Redis Cache.

* Сопоставление функции управляемой службы кэша tooAzure кэша Redis
* Выбор уровня кэша.
* Создание кэша.
* Настройка клиентов кэша hello
  * Удаление конфигурации службы управляемого кэша hello
  * Настройка клиента кэша с помощью пакета NuGet StackExchange.Redis hello
* Перенос кода управляемой службы кэша.
  * Подключение с использованием класса ConnectionMultiplexer hello кэша toohello
  * Доступ примитивных типов данных в кэше hello
  * Работа с объектами .NET в кэше hello
* Перенос состояний сеансов ASP.NET и выводом tooAzure кэша Redis 

## <a name="map-managed-cache-service-features-tooazure-redis-cache"></a>Сопоставление функции управляемой службы кэша tooAzure кэша Redis
Управляемая служба кэша Azure и кэш Redis для Azure похожи, но некоторые их функции реализуются по-разному. В этом разделе описаны некоторые различия hello и приводятся рекомендации по реализации функции hello управляемой службы кэша в кэше Redis для Azure.

| Функция управляемой службы кэша | Поддержка управляемой службы кэша | Поддержка кэша Redis для Azure |
| --- | --- | --- |
| Именованные кэши |Настроить кэш по умолчанию, а в hello Standard и Premium предложения кэша, копирование toonine дополнительные именованные кэши могут быть настроены при желании. |Кэшах Azure Redis имеется определенное количество баз данных (по умолчанию 16), которые можно использовать tooimplement, который кэширует аналогичные toonamed функциональные возможности. Дополнительные сведения см. в разделах [What are Redis databases?](cache-configure.md#default-redis-server-configuration) (Что такое базы данных Redis) и [Конфигурация сервера Redis по умолчанию](cache-faq.md#what-are-redis-databases). |
| Высокая доступность |Обеспечивает высокую доступность для элементов в кэше hello в предложениях кэша Standard и Premium hello. Если элементы утрачиваются из-за сбоя tooa, резервные копии элементов hello в кэше hello по-прежнему доступны. Записывает toohello вторичный кэш выполняется синхронно. |Высокий уровень доступности предусмотрен в hello Standard и Premium предложения кэша, имеющих первичный/реплика конфигурации из двух узлов (каждый сегмент в кэше Premium имеет пару первичный и реплика). Реплика toohello операции записи выполняются асинхронно. Дополнительные сведения см. на странице [цены на кэш Redis для Azure](https://azure.microsoft.com/pricing/details/cache/). |
| Уведомления |Позволяет произойти клиентов tooreceive асинхронные уведомления при выполнении различных операций кэша в именованном кэше. |Клиентские приложения могут использовать Redis pub/sub или [уведомления Keyspace](cache-configure.md#keyspace-notifications-advanced-settings) tooachieve toonotifications аналогичные функциональные возможности. |
| Локальный кэш |Сохраняет копии кэшированных объектов локально на клиенте hello очень быстрый доступ. |Клиентские приложения, должны tooimplement этой функции с помощью словаря или аналогичной структуры данных. |
| Политика вытеснения |Нет или наиболее давно использовавшаяся. Политика по умолчанию Hello является LRU. |Кэш Azure Redis поддерживает следующие политики вытеснения hello: volatile-lru, allkeys-lru, срок жизни volatile случайных volatile, allkeys случайным образом, noeviction. Политика по умолчанию Hello является volatile-lru. Дополнительные сведения см. в разделе [Конфигурация сервера Redis по умолчанию](cache-configure.md#default-redis-server-configuration). |
| Политика срока действия |Политика срока по умолчанию Hello является абсолютным и срок действия по умолчанию hello составляет десять минут. Доступны также политики Sliding и Never. |По умолчанию элементы в кэше hello не истекает, но может быть настроен отдельно для каждой записи с помощью перегрузки набора кэша. Дополнительные сведения см. в разделе [Установка и получение объектов из кэша hello](cache-dotnet-how-to-use-azure-redis-cache.md#add-and-retrieve-objects-from-the-cache). |
| Регионы и добавление тегов |Регионы являются подгруппами для кэшированных элементов. Области также дополнительно поддерживают пометку hello кэшированных элементов описательными строками — тегами. Области поддерживают операции поиска tooperform hello возможности по элементам, помеченным тегами в этом регионе. Все элементы области находятся в одном узле кластера кэша hello. |Кэш Redis состоит из одного узла (если включена Redis кластера), hello понятие областей управляемой службы кэша не применяется. Redis поддерживает поиск и операции с маской при получении ключей, поэтому описательные теги может быть внедрен в имена ключей hello и используемые элементы hello tooretrieve позже. Пример добавления тегов с помощью Redis см. в статье [Добавление тегов с помощью Redis](http://stackify.com/implementing-cache-tagging-redis/). |
| Сериализация |Управляемый кэш поддерживает NetDataContractSerializer, BinaryFormatter и использование пользовательских сериализаторов hello. по умолчанию Hello используется NetDataContractSerializer. |Возлагается hello hello клиентских приложений tooserialize .NET объектов перед их размещением в кэш hello с выбором hello сериализатора hello вверх toohello разработчиком клиентского приложения. Дополнительные сведения и пример кода см. в разделе [работа с объектами .NET в кэше hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache). |
| Эмулятор кэша |Управляемый кэш предоставляет локальный эмулятор кэша. |Кэш Azure Redis имеет эмулятор, но вы можете [локально запуск сборки MSOpenTech hello redis server.exe](cache-faq.md#cache-emulator) tooprovide интерфейс эмулятора. |

## <a name="choose-a-cache-offering"></a>Выбор уровня кэша.
Кэш Microsoft Azure Redis доступна hello следующие уровни:

* **Basic** — один узел. Несколько размеров too53 Гбайт.
* **Стандартный** — два узла: основной и реплика. Несколько размеров too53 Гбайт. СОГЛАШЕНИЕ ОБ УРОВНЕ ОБСЛУЖИВАНИЯ 99,9 %.
* **Premium** — двумя узлами первичный/реплика с вверх too10 сегментов. Несколько размеров от 6 ГБ too530 ГБ. Все функции уровня "Стандартный", а также дополнительные функции, включая поддержку [кластера Redis](cache-how-to-premium-clustering.md), [сохраняемости Redis](cache-how-to-premium-persistence.md) и [виртуальной сети Azure](cache-how-to-premium-vnet.md). СОГЛАШЕНИЕ ОБ УРОВНЕ ОБСЛУЖИВАНИЯ 99,9 %.

Каждый уровень отличается доступными возможностями и ценой. Hello функций рассматриваются далее в этом руководстве, а также дополнительные сведения о ценах см. в разделе [сведения о ценах — кэш](https://azure.microsoft.com/pricing/details/cache/).

Отправная точка при миграции — размер toopick hello, соответствующей hello размеру предыдущего кэша управляемой службы кэша, а затем масштабирование вверх или вниз в зависимости от требований приложения hello. Дополнительные рекомендации по выбору hello подходящего предложения кэша Redis Azure см. в разделе [какие Redis размер кэша и использовать?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="create-a-cache"></a>Создание кэша.
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="configure-hello-cache-clients"></a>Настройка клиентов кэша hello
После создания и настройки кэша hello hello следующим шагом является управляемой службы кэша конфигурации tooremove hello и добавьте hello Добавление конфигурации кэша Redis для Azure hello и ссылки, чтобы клиенты кэша можно получить доступ к кэшу hello.

* Удаление конфигурации службы управляемого кэша hello
* Настройка клиента кэша с помощью пакета NuGet StackExchange.Redis hello

### <a name="remove-hello-managed-cache-service-configuration"></a>Удаление конфигурации службы управляемого кэша hello
Прежде чем hello клиентских приложений можно настроить для кэша Azure Redis, существующая конфигурация службы кэша hello и ссылки на сборку необходимо удалить, удалив hello управляемые службы пакета NuGet кэша.

hello toouninstall пакета управляемого кэша NuGet службы щелкните правой кнопкой мыши проект клиента hello в **обозревателе решений** и выберите **управление пакетами NuGet**. Выберите hello **установленных пакетов** узла и тип W**indowsAzure.Caching** в hello поиск установленных пакетов поле. Выберите **Windows** **кэш Azure** (или **Windows** **Azure Caching** в зависимости от версии пакета NuGet hello hello), нажмите кнопку  **Удалить**, а затем нажмите кнопку **закрыть**.

![Удаление пакета NuGet управляемой службы кэша Azure](./media/cache-migrate-to-redis/IC757666.jpg)

Удаление hello управляемые службы пакета NuGet кэша удаляет hello управляемой службы кэша сборки и записи управляемой службы кэша hello hello app.config или web.config клиентского приложения hello. Так как некоторые настраиваемые параметры не могут быть удалены при удалении пакета NuGet hello, откройте файл web.config или app.config и убедитесь, что hello, следующие элементы не будут окончательно удалены.

Убедитесь, что hello `dataCacheClients` запись удаляется из hello `configSections` элемента. Не удаляйте hello всего `configSections` элемент, просто удалите hello `dataCacheClients` записи, если он имеется.

```xml
<configSections>
  <!-- Existing sections omitted for clarity. -->
  <section name="dataCacheClients"type="Microsoft.ApplicationServer.Caching.DataCacheClientsSection, Microsoft.ApplicationServer.Caching.Core" allowLocation="true" allowDefinition="Everywhere"/>
</configSections>
```

Убедитесь, что hello `dataCacheClients` раздел удален. Hello `dataCacheClients` раздел будет примерно toohello следующий пример.

```xml
<dataCacheClients>
  <dataCacheClientname="default">
    <!--toouse hello in-role flavor of Azure Cache, set identifier toobe hello cache cluster role name -->
    <!--toouse hello Azure Managed Cache Service, set identifier toobe hello endpoint of hello cache cluster -->
    <autoDiscoverisEnabled="true"identifier="[Cache role name or Service Endpoint]"/>

    <!--<localCache isEnabled="true" sync="TimeoutBased" objectCount="100000" ttlValue="300" />-->
    <!--Use this section toospecify security settings for connecting tooyour cache. This section is not required if your cache is hosted on a role that is a part of your cloud service. -->
    <!--<securityProperties mode="Message" sslEnabled="true">
      <messageSecurity authorizationInfo="[Authentication Key]" />
    </securityProperties>-->
  </dataCacheClient>
</dataCacheClients>
```

После удаления конфигурации hello управляемой службы кэша можно настроить клиент кэша hello, как описано в следующем разделе hello.

### <a name="configure-a-cache-client-using-hello-stackexchangeredis-nuget-package"></a>Настройка клиента кэша с помощью пакета NuGet StackExchange.Redis hello
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

## <a name="migrate-managed-cache-service-code"></a>Перенос кода управляемой службы кэша.
Hello API для клиента кэша StackExchange.Redis hello — примерно toohello службы управляемого кэша. Этот раздел предоставляет обзор отличий hello.

### <a name="connect-toohello-cache-using-hello-connectionmultiplexer-class"></a>Подключение с использованием класса ConnectionMultiplexer hello кэша toohello
В управляемой службы кэша кэш подключений toohello обрабатывались hello `DataCacheFactory` и `DataCache` классы. Кэш Azure Redis, эти подключения управляются hello `ConnectionMultiplexer` класса.

Добавьте следующее hello с помощью инструкции toohello начало любого файла, из которого нужно tooaccess hello кэша.

```c#
using StackExchange.Redis
```

Если это пространство имен не разрешается, убедитесь, что добавили hello пакета StackExchange.Redis NuGet, как описано в [Настройка клиентов кэша hello](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).

> [!NOTE]
> Обратите внимание, что этот клиент StackExchange.Redis hello требуется платформа .NET Framework 4 или более поздней версии.
> 
> 

экземпляр кэша Redis для Azure tooan tooconnect, статический hello вызовов `ConnectionMultiplexer.Connect` метод и передайте его в конечную точку hello и ключ. Один из подходов toosharing `ConnectionMultiplexer` toohave статическое свойство, которое возвращает подключенный экземпляр, аналогичные toohello следующий пример является экземпляр приложения. Это обеспечивает tooinitialize потокобезопасным способом только одного подключенного `ConnectionMultiplexer` экземпляра. В этом примере `abortConnect` является набор toofalse, это означает, что hello вызов будет успешным, даже если кэш toohello подключение не установлено. Одна важная особенность `ConnectionMultiplexer` — что он будет автоматически восстанавливать подключение toohello кэша после hello проблемы в сети или по другим причинам не будут разрешены.

```c#
private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
{
    return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
});

public static ConnectionMultiplexer Connection
{
    get
    {
        return lazyConnection.Value;
    }
}
```

Hello конечную точку кэша, ключи и порты можно получить из hello **кэша Redis** колонку для экземпляра кэша. Дополнительные сведения см. в разделе [Свойства кэша Redis](cache-configure.md#properties).

После установления соединения hello вернуть базу данных кэша Redis ссылки toohello, вызывающему Привет `ConnectionMultiplexer.GetDatabase` метод. Hello объект, возвращенный hello `GetDatabase` метод является облегченным сквозным объектом и не обязательно toobe хранятся.

```c#
IDatabase cache = Connection.GetDatabase();

// Perform cache operations using hello cache object...
// Simple put of integral data types into hello cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from hello cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

Клиент StackExchange.Redis Hello использует hello `RedisKey` и `RedisValue` типов для доступа к элементам и сохранения в кэше hello. Эти типы сопоставляются с большинством несложных типов языков, например со строками, и часто не используются напрямую. Redis hello базовая разновидность значений Redis и строки может содержать несколько типов данных, включая сериализованные двоичные потоки, и пока не может непосредственно использовать тип hello, будет использовать методы, содержащие `String` в имени hello. Большинство примитивных типов данных хранения и получения элементов из кэша hello, с использованием hello `StringSet` и `StringGet` методов, если в кэше hello хранятся коллекции или другие типы данных Redis. 

`StringSet`и `StringGet` являются очень похожа toohello службы управляемого кэша `Put` и `Get` методов с одним важным отличием: перед установкой и получением объекта .NET в кэш hello вы сначала сериализовать его. 

При вызове `StringGet`, возвращается, если hello объект существует, и если нет, возвращается значение null. В этом случае можно получить значение hello из hello необходимый источник данных и сохранить его в кэше hello для последующего использования. Это известно как шаблон hello отдельно от кэша.

срок годности hello toospecify элемента в кэше hello, используйте hello `TimeSpan` параметр `StringSet`.

```c#
cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));
```

Кэш Redis для Azure может работать с объектами .NET, а также несложными типами данных, но прежде чем объект .NET можно будет кэшировать, он должен быть сериализован. Это hello отвечает разработчик приложения hello. Это обеспечивает гибкость hello разработчика по выбору hello hello сериализатор. Дополнительные сведения и пример кода см. в разделе [работа с объектами .NET в кэше hello](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

## <a name="migrate-aspnet-session-state-and-output-caching-tooazure-redis-cache"></a>Перенос состояний сеансов ASP.NET и выводом tooAzure кэша Redis
В кэше Redis для Azure есть поставщики состояния сеанса ASP.NET и кэширования вывода страниц. Удалите приложение, использующее версии управляемой службы кэша hello эти поставщики toomigrate hello существующие разделы из файла web.config, а затем настройте hello кэша Redis для Azure версии поставщиков hello. Инструкции по использованию hello поставщики ASP.NET кэша Redis Azure, см. в разделе [поставщика состояний сеансов ASP.NET для кэша Azure Redis](cache-aspnet-session-state-provider.md) и [поставщика кэша вывода ASP.NET для кэша Azure Redis](cache-aspnet-output-cache-provider.md).

## <a name="next-steps"></a>Дальнейшие действия
Просмотр hello [документации кэш Azure Redis](https://azure.microsoft.com/documentation/services/cache/) учебники, примеры, видео и других.

