---
title: "запрос aaaAdvanced регулирования со службой управления API Azure"
description: "Узнайте, как toocreate применение гибкую квоту и политики управления API Azure ограничение частоты."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Расширенное регулирование запросов с помощью API Management
Может toothrottle входящие запросы, — это ключевой роль управления API Azure. Позволяет либо управляющий hello скорости запросов или общее количество запросов в hello данных перемещаются, API управления API поставщиков tooprotect их интерфейсов API из о нарушении и создания значения для различных уровней API продукта.

## <a name="product-based-throttling"></a>Регулирование запросов на основе продукта
toodate скорость hello возможности регулирования были определенной подписки ограниченный toobeing области tooa (фактически ключ), определенные на hello портал издателя управления API. Это полезно для hello API поставщика tooapply ограничения на hello разработчики, которые зарегистрировались toouse их API, однако он не помогает, например, регулирования отдельным конечным пользователям hello API. Это возможно, что для одного пользователя tooconsume hello разработчик приложения hello всей квоты и затем предотвращают другим клиентам hello разработчик может toouse приложения hello. Кроме того несколько клиентов, которые может создавать большое количество запросов может ограничить доступ toooccasional пользователей.

## <a name="custom-key-based-throttling"></a>Регулирование запросов на основе настраиваемых ключей
новый Hello [скорость ограничение по ключ](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [ключ квоты](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) политики предоставляют значительно более гибкий элемент управления tootraffic решения. Эти новые политики позволяют toodefine выражений tooidentify hello ключи, которые будут используется tootrack использования трафика. Привет, как это работает простых проиллюстрирован с примерами. 

## <a name="ip-address-throttling"></a>Регулирование запросов по IP-адресам
Hello следующие политики ограничения один tooonly адрес IP клиента 10 вызывает каждую минуту с общим 1 000 000 вызовов и 10 000 килобайт пропускной способности для каждого месяца. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Если все клиенты в Интернете hello уникальный IP-адрес, это может быть эффективным способом ограничения использования пользователем. Тем не менее вполне вероятно, что несколько пользователей будут один общий IP-адрес из-за доступ к hello toothem Интернета через устройство NAT для управления доступом. Несмотря на это, для интерфейсов API, позволяющих доступ без проверки подлинности hello `IpAddress` может быть лучшим вариантом hello.

## <a name="user-identity-throttling"></a>Регулирование запросов по удостоверениям пользователя
Если пользователь прошел проверку подлинности, на основе данных, уникально идентифицирующих этого пользователя, генерируется ключ регулирования.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

В этом примере мы извлечь hello заголовок Authorization, преобразуйте его слишком`JWT` объекта и использовать субъекта hello hello маркера tooidentify hello пользователя и использовать его как ограничение ключа частоты hello. Если удостоверение пользователя hello хранится в hello `JWT` как один из других hello утверждений затем значение может использоваться вместо него.

## <a name="combined-policies"></a>Объединенные политики
Несмотря на то, что новые политики регулирования hello обеспечивают больший контроль, чем hello существующую политику регулирования, по-прежнему значение объединение обе возможности. Регулирование по ключу продукта подписки ([ограничение частоты вызовов по подписке](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) и [набор квоты на использование по подписке](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) является отличным способом tooenable monetizing API-интерфейса путем однократного списания на основе использования уровней. Hello более точный контроль того, что может toothrottle пользователем дополняет и предотвращает ухудшения качества hello другого поведение одного пользователя. 

## <a name="client-driven-throttling"></a>Регулирование со стороны клиента
Если hello регулирования ключ определен с помощью [выражение политики](https://msdn.microsoft.com/library/azure/dn910913.aspx), то hello API поставщика, который выбирает действует как регулирование hello. Однако разработчик может потребоваться toocontrol, как они интенсивность ограничить своих клиентов. Это может включить hello API поставщика путем введения разработчика tooallow пользовательский заголовок hello клиентского приложения toocommunicate hello ключа toohello API.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

Это позволяет toochoose приложения hello разработчик клиента способ ограничение ключа частоты toocreate hello. С помощью немного ingenuity разработчик клиента создать свои собственные уровни норм путем выделения наборов ключей toousers и поворот hello использования ключа.

## <a name="summary"></a>Сводка
Управления API Azure предоставляет скорость и квоты, регулирование tooboth защиты и добавить значение tooyour API-службы. новые политики настраиваемые правила выбора области регулирования Hello разрешающее вы точно Контролируемая контроль над tooenable этих политик приложений еще лучше toobuild клиентов. Hello в этой статье примерах hello использовать эти новые политики, ограничение ключи с IP-адресов клиентов, удостоверения пользователя и клиента, созданного значения частоты производства. Тем не менее существует много других частей сообщения hello, который может быть использован как агент пользователя, фрагментов пути URL-адрес, размер сообщения.

## <a name="next-steps"></a>Дальнейшие действия
Отправьте нам ваши отзывы в потоке hello Disqus для этого раздела. Было бы отлично toohear о других возможных значений ключа, были логичным выбором в ваших сценариях.

## <a name="watch-a-video-overview-of-these-policies"></a>Посмотрите видеообзор этих политик.
Дополнительные сведения о hello [скорость ограничение по ключ](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) и [ключ квоты](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) политики, описанные в данной статье, обратите внимание на следующие видео hello.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

