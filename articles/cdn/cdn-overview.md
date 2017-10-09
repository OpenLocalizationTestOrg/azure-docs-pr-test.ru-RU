---
title: "Общие сведения о CDN aaaAzure | Документы Microsoft"
description: "Узнайте, какие hello Azure сеть доставки содержимого (CDN) — и как toouse его содержимое toodeliver высокой пропускной способностью путем кэширования BLOB-объекты и статическое содержимое."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Общие сведения о hello Azure доставки содержимого сети (CDN)
> [!NOTE]
> Этот документ описывает какие hello Azure доставки содержимого сети (CDN) —, как он работает и функции hello каждого продукта Azure CDN.  Если хотите tooskip эти сведения и перейдите прямой tooa учебник о том, как toocreate конечной точкой CDN, в разделе [использование Azure CDN](cdn-create-new-endpoint.md).  Если требуется toosee список текущих расположениях узлов CDN см [расположения POP в CDN Azure](cdn-pop-locations.md).
> 
> 

Hello Azure сеть доставки содержимого (CDN) кэширует статического веб-содержимого в стратегически расположенных пунктах tooprovide максимальную пропускную способность для доставки содержимого toousers.  Hello CDN предлагает разработчикам глобальное решение по доставке контента с высокой пропускной способностью путем кэширования контента hello на физических узлах по Здравствуй, мир. 

с помощью средств веб-сайт toocache CDN hello Hello преимущества:

* Лучшая производительность и взаимодействие с конечными пользователями, особенно в том случае, если с помощью приложений, в которых несколько циклов приема-передачи необходимого tooload содержимого.
* Большие масштабирования toobetter обработки кратковременной высокой нагрузки, как и в начале hello продукта запустите событий.
* Распределение пользовательских запросов и обслуживает содержимое из пограничных серверов, меньше трафик отправляется toohello источника.

## <a name="how-it-works"></a>Принцип работы
![Обзор сети доставки содержимого](./media/cdn-overview/cdn-overview.png)

1. Пользователь (Alice) запрашивает файл (ресурс), обращаясь к нему по URL-адресу со специальным доменным именем, например `<endpointname>.azureedge.net`.  DNS направляет hello запроса toohello лучше всего выполняется расположение, точки присутствия (POP).  Обычно это hello POP, географически ближайший toohello пользователя.
2. Если пограничные серверы hello в hello POP hello файл отсутствует в кэше, hello пограничный сервер запрашивает hello файл из исходной hello.  Hello источник может быть веб-приложение Azure, облачные службы, учетной записи хранилища Azure или общедоступный веб-сервер.
3. Источник Hello возвращает hello файл toohello пограничного сервера, включая необязательные заголовки HTTP, описывающий файл hello время жизни (TTL).
4. Hello пограничный сервер кэширует файл hello и возвращает hello файл toohello исходной запрашивающей стороны (Анна).  файл Hello остается кэшированные на пограничном сервере hello, вплоть до истечения срока ЖИЗНИ hello.  Если источник hello не был указан параметр TTL, TTL по умолчанию hello составляет семь дней.
5. Дополнительные пользователи могут hello запрос же текстовый файл с помощью этой же URL-адрес, а также может быть направленной toothat же POP.
6. Если hello TTL для hello файла еще не истек, hello пограничный сервер возвращает hello файл из кэша hello.  Такая схема повышает скорость взаимодействия с пользователем и устраняет задержки.

## <a name="azure-cdn-features"></a>Компоненты Azure CDN
Существует три продукта Azure CDN: **Azure CDN уровня "Стандартный" от Akamai**, **Azure CDN уровня "Стандартный" от Verizon** и **Azure CDN уровня "Премиум" от Verizon**.  Hello следующей таблице перечислены функции hello, доступные с помощью каждого продукта.

|  | Akamai уровня "Стандартный" | Verizon уровня "Стандартный" | Verizon уровня "Premium" |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Возможности для повышения производительности и оптимизации__ |
| [Динамическое ускорение сайтов](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Динамическое ускорение сайтов — адаптивное сжатие изображений](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Динамическое ускорение сайтов — предварительная выборка объектов](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [Оптимизация потоковой передачи видео](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [Оптимизация больших файлов](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [Глобальная балансировка нагрузки сервера (GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Быстрая очистка.](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Предварительная загрузка ресурса.](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| [Кэширование строк запроса.](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Двойной стек IPv4/IPv6 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Поддержка HTTP/2](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Безопасность__ |
| Поддержка HTTPS с конечной точкой CDN |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Пользовательский домен HTTPS](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [Поддержка пользовательских доменных имен.](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Геофильтрация](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Проверка подлинности по маркерам](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [Защита от атак DDoS](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Analytics и отчетность__ |
| [Базовая аналитика.](cdn-analyze-usage-patterns.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Расширенные HTTP-отчеты.](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [Статистика в режиме реального времени.](cdn-real-time-stats.md) | | |**&#x2713;** |
| [Оповещения в реальном времени](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Простота использования__ |
| Простая интеграция со службами Azure, такими как [служба хранилища](cdn-create-a-storage-account-with-cdn.md), [облачные службы](cdn-cloud-service-with-cdn.md), [веб-приложения](../app-service-web/app-service-web-tutorial-content-delivery-network.md) и [службы мультимедиа](../media-services/media-services-portal-manage-streaming-endpoints.md). |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Управление с помощью [REST API](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md) или [PowerShell](cdn-manage-powershell.md). |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Настраиваемый модуль доставки контента на основе правил.](cdn-rules-engine.md) | | |**&#x2713;** |
| Параметры кэша и заголовка (с использованием [обработчика правил](cdn-rules-engine.md)) | | |**&#x2713;** |
| Перенаправление или перезапись URL-адреса (с использованием [обработчика правил](cdn-rules-engine.md)) | | |**&#x2713;** |
| Правила для мобильных устройств (с использованием [обработчик правил](cdn-rules-engine.md)) | | |**&#x2713;** |

\*Verizon поддерживает доставку больших файлов и мультимедиа непосредственно через общую веб-доставку.


> [!TIP]
> Можно ли хотелось бы toosee в Azure CDN?  [Расскажите нам о ней](https://feedback.azure.com/forums/169397-cdn). 
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
tooget к работе с CDN, в разделе [использование Azure CDN](cdn-create-new-endpoint.md).

Если вы являетесь действующим клиентом CDN, теперь вы можете управлять своими конечными точками CDN посредством hello [портал Microsoft Azure](https://portal.azure.com) или [PowerShell](cdn-manage-powershell.md).

toosee hello CDN в действии, ознакомьтесь с hello [video наши сеанса 2016 построения](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Узнайте, как tooautomate Azure CDN с [.NET](cdn-app-dev-net.md) или [Node.js](cdn-app-dev-node.md).

Сведения о ценах на CDN см. на [этой странице](https://azure.microsoft.com/pricing/details/cdn/).

