---
title: "aaaCache поставщика кэша вывода ASP.NET"
description: "Дополнительные сведения о том, как toocache вывода страницы ASP.NET с помощью кэша Azure Redis"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a>Поставщик кэша вывода ASP.NET для кэша Redis для Azure
Hello поставщика кэша вывода Redis представляет собой механизм хранения вне процесса для данных кэша вывода. Эти данные предназначены специально для полных HTTP-ответов (кэширование вывода страниц). Поставщик Hello подключается hello новой точке поставщика кэша вывода расширяемости, появившихся в ASP.NET 4.

Здравствуйте toouse поставщика кэша вывода Redis, сначала необходимо настроить кэш и затем настроить приложение ASP.NET с использованием пакета hello Redis NuGet поставщика кэша вывода. В этом разделе содержатся рекомендации по настройке вашего приложения toouse hello поставщика кэша вывода Redis. Дополнительные сведения о создании и настройке экземпляра кэша Redis для Azure см. в разделе [Создание кэша](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

## <a name="store-aspnet-page-output-in-hello-cache"></a>Сохранение вывода страниц ASP.NET в кэше hello
Щелкните tooconfigure клиентское приложение в Visual Studio с использованием пакета кэша NuGet состояний сеанса Redis hello, **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню.

Выполнения hello следующую команду из hello `Package Manager Console` окна.
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

пакет Redis NuGet поставщика кэша вывода Hello имеет зависимость от пакета StackExchange.Redis.StrongName hello. Если отсутствует пакет StackExchange.Redis.StrongName hello в проекте, он устанавливается. Дополнительные сведения о пакете hello Redis NuGet поставщика кэша вывода см. в разделе hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) страница NuGet.

>[!NOTE]
>В дополнение toohello со строгими именами пакета StackExchange.Redis.StrongName имеется также hello StackExchange.Redis без строгого имени версии. Если проект использует hello без строгого имени версию StackExchange.Redis необходимо удалить ее, в противном случае можно получить конфликтов имен в проекте. Дополнительные сведения об этих пакетах см. в разделе [Настройка клиентов кэша .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello NuGet пакет загружает и добавляет hello требуется сборка ссылается на и добавляет следующий раздел в файл web.config hello. Этот раздел содержит hello требуемую конфигурацию приложения hello toouse поставщика кэша вывода Redis в ASP.NET.

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

раздел содержит пример hello атрибутов и параметров для каждого атрибута в комментарий Hello.

Настройте атрибуты hello hello значениями из раздела кэша на портале Microsoft Azure hello и hello другие значения в случае необходимости. Инструкции по доступу к свойствам кэша см. в разделе [Настройка параметров кэша Redis](cache-configure.md#configure-redis-cache-settings).

* **host** — укажите конечную точку кэша.
* **порт** — использовать порт не SSL или порт SSL, в зависимости от параметров ssl hello.
* **accessKey** — использовать либо hello первичный или вторичный ключ кэша.
* **SSL** — значение true, если toosecure взаимодействий кэша/клиента с помощью ssl, в противном случае — значение false. Быть убедиться, что toospecify hello правильный порт.
  * Hello не SSL-порт отключен по умолчанию для нового кэша. Укажите значение true для этого параметра toouse hello порт SSL. Дополнительные сведения о включении порта без поддержки SSL hello см. в разделе hello [порты доступа](cache-configure.md#access-ports) раздела hello [настройте кэш](cache-configure.md) раздела.
* **databaseId** — Specified toouse какие базы данных для кэширования выходных данных. Если не указан, используется значение по умолчанию hello 0.
* **applicationName** — ключи хранятся в кэше Redis как `<AppName>_<SessionId>_Data`. Такая схема именования включает несколько приложений tooshare hello таким же ключом. Этот параметр — необязательный, и, если для него не указано другое значение, используется значение по умолчанию.
* **connectionTimeoutInMilliseconds** — этот параметр позволяет connectTimeout hello toooverride параметр в клиенте StackExchange.Redis hello. Если не указан, используется hello connectTimeout по умолчанию 5000. Дополнительную информацию см. в статье [Модель конфигурации StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** — этот параметр позволяет syncTimeout hello toooverride параметр в клиенте StackExchange.Redis hello. Если не указан, используется hello syncTimeout по умолчанию 1000. Дополнительную информацию см. в статье [Модель конфигурации StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Добавьте страницу OutputCache директив tooeach, для которого вы хотите toocache hello вывода.

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

В предыдущем примере hello hello страницы данных остается в кэше hello в кэше 60 секунд, а для каждой комбинации параметров кэшируются разные версии страницы приветствия. Дополнительные сведения о директиве OutputCache hello. в разделе [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).

После выполнения этих действий, приложение будет hello toouse настроенного поставщика кэша вывода Redis.

## <a name="next-steps"></a>Дальнейшие действия
Извлечение hello [поставщика состояний сеансов ASP.NET для кэша Azure Redis](cache-aspnet-session-state-provider.md).

