---
title: "состояние aaaSession с кэшем Azure Redis в службе приложений Azure"
description: "Узнайте, как toouse hello кэширования по состояния сеанса для службы кэша Azure toosupport ASP.NET."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>Состояние сеанса с кэшем Redis для Azure в службе приложений Azure
В этом разделе объясняется, как toouse hello служба кэша Redis Azure для хранения состояния сеанса.

Если веб-приложения ASP.NET использует состояние сеанса, необходимо будет tooconfigure поставщик состояния сеанса внешних (hello служба кэша Redis или поставщик состояния сеанса SQL Server). Если используются состояние сеанса, а не использовать внешнего поставщика, можно только tooone экземпляр веб-приложения. Hello служба кэша Redis является быстрым и простым tooenable hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>Создать hello кэша
Выполните [этим указаниям](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello кэша.

## <a id="configureproject"></a>Добавить hello RedisSessionStateProvider NuGet пакета tooyour веб-приложения
Установка hello NuGet `RedisSessionStateProvider` пакета.  Используйте hello следующая команда tooinstall из консоли диспетчера пакетов hello (**средства** > **диспетчера пакетов NuGet** > **консоль диспетчера пакетов**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

tooinstall из **средства** > **диспетчера пакетов NuGet** > **управление фрагментом пакетами для решения**, поиск `RedisSessionStateProvider`.

Дополнительные сведения см. hello [NuGet RedisSessionStateProvider страницы](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) и [Настройка клиента кэша hello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).

## <a id="configurewebconfig"></a>Изменение файла Web.Config hello
Кроме ссылается на сборку toomaking для кэша, hello пакет NuGet добавляет записи в заглушки hello *web.config* файла. 

1. Откройте hello *web.config* и найти hello hello **sessionState** элемента.
2. Введите значения hello для `host`, `accessKey`, `port` (hello SSL-порт должен быть 6380) и задайте `SSL` слишком`true`. Эти значения можно получить из hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715) колонку для экземпляра кэша. Дополнительные сведения см. в разделе [подключения кэша toohello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache). Обратите внимание, что порт не SSL hello отключен по умолчанию для нового кэша. Дополнительные сведения о включении порта без поддержки SSL hello см. в разделе hello [порты доступа](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) раздела hello [Настройка кэша в кэше Redis для Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) раздела. Hello следующую разметку показывает hello изменения toohello *web.config* файла, в частности hello изменения слишком*порт*, *узла*, accessKey * и *ssl*.
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <a id="usesessionobject"></a>Использование hello объекта сеанса в коде
последним шагом Hello является toobegin, используя объект сеанса hello в коде ASP.NET. Добавление состояния toosession объектов с помощью hello **Session.Add** метод. Этот метод использует элементы toostore пары "ключ значение" в кэш состояния сеанса hello.

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

Привет, следующий код получает это значение из состояния сеанса.

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

Можно также использовать объекты toocache кэша Redis hello в веб-приложения. Дополнительные сведения см. в статье о [приложении для обработки фильмов MVC с кэшем Redis для Azure за 15 минут](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).
Дополнительные сведения о том, как состояние сеанса ASP.NET toouse, в разделе [Общие сведения о состоянии сеанса ASP.NET][ASP.NET Session State Overview].

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *Автор: [Рик Андерсон (Rick Anderson)](https://twitter.com/RickAndMSFT)*

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

