---
title: "aaaUsing CDN Azure с CORS | Документы Microsoft"
description: "Узнайте, как toouse hello Azure доставки содержимого сети (CDN) toowith общий доступ к ресурсам независимо от источника (CORS)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>Использование Azure CDN с CORS
## <a name="what-is-cors"></a>Что такое CORS?
CORS (кросс-Origin доступ к ресурсам) является функцией HTTP, который позволяет веб-приложение в пределах одного домена tooaccess ресурсы в другом домене. В порядке tooreduce hello вероятность атак с использованием межсайтовых сценариев, все современных веб-браузеры имеют ограничение безопасности называется [политика одного источника](http://www.w3.org/Security/wiki/Same_Origin_Policy).  Это ограничение не позволяет веб-страницы вызывать интерфейсы API в другом домене.  CORS обеспечивают безопасный способ tooallow один источник (hello исходный домен) toocall API-интерфейсы в другой источник.

## <a name="how-it-works"></a>Принцип работы
Существует два типа запросов CORS, *простые запросы* и *сложные запросы*.

### <a name="for-simple-requests"></a>Простые запросы

1. Hello браузер отправляет запрос CORS hello с дополнительным **источника** заголовка HTTP-запроса. Hello значение этого заголовка — источник hello, обработавшего hello родительская страница, которая определяется как сочетание hello *протокола,* *домена,* и *порта.*  Если отображается страница https://www.contoso.com пытается tooaccess пользовательские данные в источник fabrikam.com hello, hello после заголовка запроса были бы отправлены toofabrikam.com:

   `Origin: https://www.contoso.com`

2. Hello сервер может ответить с любым из следующих hello:

   * Ответ с заголовком **Access-Control-Allow-Origin**, который указывает, какие исходные сайты разрешены. Например:

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * Ошибка HTTP код например 403, если сервер hello не допускает hello независимо от источника запроса после проверки заголовка Origin hello

   * Заголовок **Access-Control-Allow-Origin** с подстановочным знаком, который разрешает все источники:

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>Сложные запросы

Сложный запрос является запросом CORS, где требуется toosend браузера hello *Предварительный запрос* (т. е. предварительной выборки) перед отправкой самого запроса CORS hello. Hello Предварительный запрос запрашивает разрешение hello server Если hello первоначальный запрос CORS можно продолжить работу, а `OPTIONS` запроса toohello же URL-адрес.

> [!TIP]
> Дополнительные сведения о CORS потоков и типичные проблемы просмотрите hello [руководства по API REST tooCORS](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>Подстановочный знак или сценарии с одним источником
CORS в Azure CDN будет автоматически работать без дополнительной настройки, когда hello **Access-Control-Allow-Origin** задан заголовок toowildcard (*) или один источник.  Hello CDN кэширует первого ответа hello и последующие запросы будут использовать hello же заголовок.

Если запросы уже выполнены предыдущие tooCORS toohello CDN, задаваемого hello источника, необходимо будет toopurge содержимое на ваш конечная точка содержимого tooreload hello содержимого с hello **Access-Control-Allow-Origin** заголовок.

## <a name="multiple-origin-scenarios"></a>Сценарии с несколькими источниками
Если вам требуется tooallow определенного списка toobe источников, разрешенное для CORS, все еще немного усложняется. Hello проблема возникает, когда hello CDN кэширует hello **Access-Control-Allow-Origin** заголовок для hello первый источник CORS.  При последующих запрашивает другой источник CORS, hello CDN будет обслуживать hello в кэше **Access-Control-Allow-Origin** заголовок, который не будет совпадать.  Существует несколько способов toocorrect это.

### <a name="azure-cdn-premium-from-verizon"></a>Azure CDN уровня "Премиум" от Verizon
Здравствуйте, лучшим способом tooenable это toouse **Azure CDN Premium из Verizon**, которая предоставляет некоторые расширенные функции. 

Вам потребуется слишком[создать правило](cdn-rules-engine.md) toocheck hello **источника** заголовка запроса hello.  Если это допустимый источник вашей правило будет задавать hello **Access-Control-Allow-Origin** заголовок с hello источник, указанный в запросе hello.  Если указан источник hello в hello **источника** заголовок не допускается, правила следует пропустить hello **Access-Control-Allow-Origin** заголовок, что вызовет запроса hello tooreject обозревателя hello. 

Существует два способа toodo это с помощью модуля правил hello.  В обоих случаях hello **Access-Control-Allow-Origin** заголовок из файла hello исходного сервера не оказывает никакого влияния, обработчик правил hello CDN полностью управляет hello допускается источников CORS.

#### <a name="one-regular-expression-with-all-valid-origins"></a>Одно регулярное выражение со всеми допустимыми источниками
В этом случае вы создадите регулярное выражение, которое включает в себя все источники hello требуется tooallow: 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> В **Azure CDN от Verizon** в качестве основного механизма регулярных выражений используются [совместимые с Perl регулярные выражения](http://pcre.org/).  Можно использовать средства, подобного [регулярных выражений 101](https://regex101.com/) toovalidate регулярное выражение.  Обратите внимание, что символ hello «/» является допустимым в регулярных выражениях и не требует toobe escape-последовательность, однако экранирование этим символом считается лучшим способом и ожидаемых некоторые проверки регулярного выражения.
> 
> 

Если hello регулярное выражение сопоставляет, правила приведет к замене hello **Access-Control-Allow-Origin** заголовок (если таковые имеются), от начала координат hello с основанием hello, отправившего запрос hello.  Также можно добавить дополнительные заголовки CORS, например **Access-Control-Allow-Methods**.

![Пример правил с регулярным выражением](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>Правило заголовка запроса для каждого источника.
Вместо того чтобы регулярные выражения, вместо этого можно создать отдельные правила для каждого источника нужно с помощью hello tooallow **подстановочные заголовок запроса** [условию](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1). Как с помощью метода регулярного выражения hello hello система правил отдельно заголовки CORS hello наборов. 

![Пример правил без регулярного выражения](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> В приведенном выше примере hello, hello использование hello подстановочный знак * сообщает toomatch система правил hello HTTP и HTTPS.
> 
> 

### <a name="azure-cdn-standard"></a>Azure CDN уровня "Стандартный"
На Azure CDN стандартные профили hello только tooallow механизм для нескольких источников без использования hello происхождения hello подстановочный знак — toouse [запроса кэширование строки](cdn-query-string.md).  Требуется параметр строки запроса tooenable для конечной точки CDN hello и затем использовать строку запроса, уникальный для запросов в каждом домене разрешенных. Это приведет к hello кэша отдельный объект для каждой строки уникальных запросов CDN. Этот подход не является идеальным, тем не менее, как это приведет к несколько копий hello тот же файл в кэш hello CDN.  

