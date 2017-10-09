---
title: "Поддержка aaaHTTP/2 в Azure CDN | Документы Microsoft"
description: "Сведения о поддержке HTTP/2 и CDN."
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>Поддержка HTTP/2 в Azure CDN

HTTP/2 соответствует tooHTTP/1.1\ основной версии. Он содержит быстрее веб-тестов производительности, уменьшения времени ответа и улучшенное взаимодействие с пользователем, сохраняя hello известные методы HTTP, коды состояния и семантику. Хотя HTTP/2 спроектированный toowork HTTP и HTTPS, многие клиента веб-браузеры поддерживают только HTTP/2 через TLS.

###<a name="http2-benefits"></a>Преимущества HTTP/2

преимущества Hello HTTP/2:

*   **Мультиплексирование и параллелизм**

    При использовании HTTP 1.1 для выполнения нескольких запросов ресурсов требуется несколько TCP-подключений, и с каждым подключением связаны определенные затраты производительности. HTTP/2 обеспечивает несколько toobe ресурсы, запрошенный для одного подключения TCP.

*   **Сжатие заголовка**

    Сжатие заголовков hello HTTP обслуживаются ресурсов, сети hello сокращает время значительно.

*   **Зависимости потоков**

    Поток зависимости разрешить клиентским hello server toohello tooindicate, какие ресурсы имеют приоритет.


##<a name="http2-browser-support"></a>Поддержка HTTP/2 в браузерах

Все основные обозреватели hello реализована поддержка HTTP/2 в своей текущей версии. Неподдерживаемые браузеры будут автоматически tooHTTP/1.1.

|"Обзор"|Минимальная версия|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>Включение HTTP/2 в Azure CDN

Сейчас поддержка HTTP/2 активна в профилях **Azure CDN от Akamai** и **Azure CDN от Verizon**. Никаких действий со стороны пользователей не требуется.

##<a name="next-steps"></a>Дальнейшие действия

toosee преимущества HTTP/2 hello в действии, в разделе [этой демонстрации из Akamai](https://http2.akamai.com/demo).

toolearn Дополнительные сведения о HTTP/2, посетите hello следующие ресурсы:

*   [Домашняя страница спецификации HTTP/2](https://http2.github.io/)
*   [Официальная страница часто задаваемых вопросов об HTTP/2](https://http2.github.io/faq/)
*   [Сведения об HTTP/2 на сайте Akamai](https://http2.akamai.com/)

toolearn Дополнительные сведения о Azure CDN доступные компоненты, в разделе hello [Общие сведения о Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).
