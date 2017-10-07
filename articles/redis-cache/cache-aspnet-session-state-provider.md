---
title: "aaaCache поставщика состояний сеансов ASP.NET | Документы Microsoft"
description: "Дополнительные сведения о том, как toostore состояний сеанса ASP.NET с помощью кэша Azure Redis"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Поставщик состояний сеансов ASP.NET для кэша Redis для Azure
Кэш Azure Redis предоставляет поставщик состояния сеанса можно использовать toostore состояние сеанса в кэше, а не в памяти или в SQL Server база данных. toouse hello поставщик кэширования состояний сеанса, сначала необходимо настроить кэш и затем настроить приложение ASP.NET для кэша с использованием пакета кэша NuGet состояний сеанса Redis hello.

Часто не имеет смысла в tooavoid реальных облачных приложений, хранить определенные виды состояния сеанса пользователя, но некоторые подходы влияют на производительность и масштабируемость сильнее, чем другие. При наличии toostore состояние hello наилучшим решением является tookeep hello объем состояния небольшой и в файлах cookie. Если это невозможно, следующее оптимальное решение hello — toouse состояние сеанса ASP.NET с поставщиком для распределенного кэша в памяти. Hello наихудшее решение с точки зрения производительности и масштабируемости — toouse поставщик состояния сеанса резервная копия базы данных. Здесь приведены рекомендации по использованию hello поставщика состояний сеансов ASP.NET для кэша Redis для Azure. Сведения о других параметрах состояний сеансов см. в разделе [Параметры состояний сеансов ASP.NET](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>Сохранение состояния сеанса ASP.NET в кэше hello
Щелкните tooconfigure клиентское приложение в Visual Studio с использованием пакета кэша NuGet состояний сеанса Redis hello, **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню.

Выполнения hello следующую команду из hello `Package Manager Console` окна.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Если вы используете hello кластеров из уровня "премиум" hello, необходимо использовать [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 или более поздней версии или исключение возникает исключение. Перемещение too2.0.1 или более поздней версии — это критическое изменение; Дополнительные сведения см. в разделе [v2.0.0 критические сведений об изменениях](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). Во время этого обновления статьи hello hello текущая версия этого пакета является 2.2.3.
> 
> 

пакет Redis NuGet поставщика состояний сеанса Hello имеет зависимость от пакета StackExchange.Redis.StrongName hello. Если отсутствует пакет StackExchange.Redis.StrongName hello в проекте, он устанавливается.

>[!NOTE]
>В дополнение toohello со строгими именами пакета StackExchange.Redis.StrongName имеется также hello StackExchange.Redis без строгого имени версии. Если проект использует hello без строгого имени версию StackExchange.Redis необходимо удалить ее, в противном случае можно получить конфликтов имен в проекте. Дополнительные сведения об этих пакетах см. в разделе [Настройка клиентов кэша .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello NuGet пакет загружает и добавляет hello требуется сборка ссылается на и добавляет следующий раздел в файл web.config hello. Этот раздел содержит hello требуемую конфигурацию приложения hello toouse кэш поставщика состояний сеанса Redis в ASP.NET.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

раздел содержит пример hello атрибутов и параметров для каждого атрибута в комментарий Hello.

Настройте атрибуты hello hello значениями из раздела кэша на портале Microsoft Azure hello и hello другие значения в случае необходимости. Инструкции по доступу к свойствам кэша см. в разделе [Настройка параметров кэша Redis](cache-configure.md#configure-redis-cache-settings).

* **host** — укажите конечную точку кэша.
* **порт** — использовать порт не SSL или порт SSL, в зависимости от параметров ssl hello.
* **accessKey** — использовать либо hello первичный или вторичный ключ кэша.
* **SSL** — значение true, если toosecure взаимодействий кэша/клиента с помощью ssl, в противном случае — значение false. Быть убедиться, что toospecify hello правильный порт.
  * Hello не SSL-порт отключен по умолчанию для нового кэша. Укажите значение true для этого параметра toouse hello порт SSL. Дополнительные сведения о включении порта без поддержки SSL hello см. в разделе hello [порты доступа](cache-configure.md#access-ports) раздела hello [настройте кэш](cache-configure.md) раздела.
* **throwOnError** — значение true, если требуется, чтобы toobe исключение, если сбой, или false, если операция toofail hello без вмешательства пользователя, создается исключение. Можно проверить наличие сбоя путем проверки статическое свойство Microsoft.Web.Redis.RedisSessionStateProvider.LastException hello. по умолчанию Hello имеет значение true.
* **retryTimeoutInMilliseconds** — в течение этого интервала (указывается в миллисекундах) для неудачных операций выполняются повторные попытки. Hello первый Повтор происходит через 20 секунд, а последующие повторы выполняются каждую секунду до истечения интервала retryTimeoutInMilliseconds hello. Сразу после этого интервала hello операция повторяется последний раз. Если по-прежнему происходит сбой операции hello, hello исключение обратно toohello вызывающего объекта, в зависимости от настройки throwOnError hello. значение по умолчанию Hello — 0, что означает нулевое количество попыток.
* **databaseId** — указывает, какие базы данных toouse для кэша вывода данных. Если не указан, используется значение по умолчанию hello 0.
* **applicationName** — ключи хранятся в кэше Redis как `{<Application Name>_<Session ID>}_Data`. Такая схема именования позволяет нескольким приложениям tooshare hello в одном экземпляре Redis. Этот параметр — необязательный, и, если для него не указано другое значение, используется значение по умолчанию.
* **connectionTimeoutInMilliseconds** — этот параметр позволяет connectTimeout hello toooverride параметр в клиенте StackExchange.Redis hello. Если не указан, используется hello connectTimeout по умолчанию 5000. Дополнительную информацию см. в статье [Модель конфигурации StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** — этот параметр позволяет syncTimeout hello toooverride параметр в клиенте StackExchange.Redis hello. Если не указан, используется hello syncTimeout по умолчанию 1000. Дополнительную информацию см. в статье [Модель конфигурации StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Дополнительные сведения об этих свойствах см. в разделе hello исходного объявлении в блоге [объявление поставщика состояний сеансов ASP.NET для Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

Не забывайте toocomment out hello Стандартная InProc раздел поставщика состояний сеанса в файл web.config.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

После выполнения этих действий, приложение будет hello настроенных toouse кэш поставщика состояний сеанса Redis. При использовании состояния сеанса в приложении состояние хранится в экземпляре кэша Redis для Azure.

> [!IMPORTANT]
> Данные, хранящиеся в кэше hello должны быть сериализуемыми, в отличие от hello данные, которые могут храниться в hello по умолчанию поставщика состояний сеансов ASP.NET в памяти. При использовании hello поставщика состояния сеанса для Redis, убедитесь, что hello типы данных, хранящихся в состоянии сеанса могут быть сериализованы.
> 
> 

## <a name="aspnet-session-state-options"></a>Параметры состояния сеанса ASP.NET
* В поставщик состояния сеансов в памяти — этот поставщик хранит состояние сеанса hello в памяти. с помощью этого поставщика Hello преимущество заключается в том, что это просто и быстро. Но если вы используете поставщик в памяти, вы не сможете масштабировать свои веб-приложения, так как поставщик не распределяется.
* Поставщик состояния сеанса SQL Server — этот поставщик хранит состояние сеанса hello в Sql Server. Используйте этого поставщика, если требуется состояние сеанса toostore hello в постоянное хранилище. Вы можете масштабировать свое веб-приложение, но использование SQL Server для сеанса может негативно повлиять на производительность веб-приложения.
* Распределенного в памяти поставщика состояний сеансов например кэш поставщика состояний сеанса Redis — это поставщик дает hello преимущества обоих миров. Веб-приложение может использовать простой, быстрый и масштабируемый поставщик состояний сеансов. Так как этот hello магазинов поставщика состояния сеанса в кэше, ваше приложение имеет tootake в расчет все hello характеристики, связанные с взаимодействием tooa распределенного кэша памяти, например временные неполадки сети. Рекомендации по использованию кэша см. в статье [Руководство по кэшированию](../best-practices-caching.md) из коллекции шаблонов и рекомендаций Майкрософт [Руководство по разработке и реализации облачного приложения Azure](https://github.com/mspnp/azure-guidance).

Дополнительные сведения о состоянии сеанса и другие рекомендации см. в статье [Рекомендации по веб-разработке (создание реальных облачных приложений с помощью Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Дальнейшие действия
Извлечение hello [поставщика кэша вывода ASP.NET для кэша Azure Redis](cache-aspnet-output-cache-provider.md).

