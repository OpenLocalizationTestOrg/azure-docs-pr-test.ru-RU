---
title: "истечение срока действия aaaManage веб-содержимого в сети доставки Содержимого Azure | Документы Microsoft"
description: "Узнайте, как toomanage истечения срока действия содержимого веб-приложений и облачные службы Azure, ASP.NET или IIS в Azure CDN."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Управление сроком действия содержимого веб-приложений и облачных служб Azure, ASP.NET или IIS в Azure CDN
> [!div class="op_single_selector"]
> * [Веб-приложения и облачные службы Azure, ASP.NET или IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Служба BLOB-объектов в службе хранилища Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

Файлы из любого общедоступного исходного веб-сервера могут кэшироваться в Azure CDN до истечения его срока жизни.  Hello TTL определяется hello [ *Cache-Control* заголовок](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) в ответ hello HTTP hello исходного сервера.  В этой статье описывается как tooset `Cache-Control` заголовки для веб-приложения Azure, облачных служб Azure, приложений ASP.NET и узлы служб IIS, все из которых настраиваются точно так же.

> [!TIP]
> Вы можете tooset не TTL в файле.  Тогда Azure CDN по умолчанию применит срок жизни длительностью семь дней.
> 
> Дополнительные сведения о работе toospeed toofiles доступ и другие ресурсы в сети доставки Содержимого Azure см. в разделе hello [Общие сведения о Azure CDN](cdn-overview.md).
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>Настройка заголовков Cache-Control в конфигурации
Для статического содержимого, такие как изображения и таблицы стилей, можно управлять частотой обновления hello, изменяя hello **applicationHost.config** или **web.config** файлы для веб-приложения.  Hello **system.webServer\staticContent\clientCache** элемент в файле конфигурации hello установит hello `Cache-Control` заголовок для содержимого. Для **web.config**, параметры конфигурации hello повлияют на все содержимое в hello и все вложенные папки, если не переопределено на уровне вложенную Привет.  Например можно задать значение по умолчанию срока жизни в toohave корневой hello все статическое содержимое в кэше в течение трех дней, но иметь вложенную папку с более переменной содержимого с кэширования составляет 6 часов.  Для **applicationHost.config**, все приложения на сайте hello будут затронуты, но могут быть переопределены в **web.config** файлы в приложениях hello.

Hello следующий XML-КОДЕ показан пример установки **clientCache** toospecify a максимальный срок хранения, равным 3 дням:  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

Указание **UseMaxAge** добавляет `Cache-Control: max-age=<nnn>` toohello ответ заголовок на основании hello значение, указанное в hello **CacheControlMaxAge** атрибута. имеет формат Hello hello timespan для hello **cacheControlMaxAge** атрибут <days>.<hours>:<min>:<sec>. Дополнительные сведения о hello **clientCache** узел, в разделе [кэш клиента <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).  

## <a name="setting-cache-control-headers-in-code"></a>Настройка заголовков Cache-Control в коде
Для приложений ASP.NET, можно задать поведение кэширования CDN hello программно, параметр hello **HttpResponse.Cache** свойство. Дополнительные сведения о hello **HttpResponse.Cache** свойство, в разделе [свойство HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) и [класс HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

Если вы хотите tooprogrammatically кэшировать содержимое приложения в ASP.NET, убедитесь, что помечены как кэшируемые содержимое hello, присвоив свойству HttpCacheability слишком*открытый*. Кроме того, убедитесь, что задан проверяющий элемент управления кэша. проверяющий элемент управления кэша Hello может быть последнее изменение отметки времени, заданная при вызове SetLastModified, или значение etag, установленное при вызове SetETag. При необходимости можно также указать срок хранения кэша, вызвав SetExpires, или можно положиться на эвристический метод кэширования по умолчанию hello описано ранее в этом документе.  

Например toocache содержимое за один час, добавьте hello следующее:  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>Дальнейшие действия
* [Ознакомления с подробными сведениями о hello **clientCache** элемент](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Ознакомьтесь с документацией hello для hello **HttpResponse.Cache** свойство](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Ознакомьтесь с документацией hello для hello **класс HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

