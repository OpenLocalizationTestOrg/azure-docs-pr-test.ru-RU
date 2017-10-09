---
title: "aaaHow toocreate API в службе управления API Azure"
description: "Узнайте, как toocreate и настройки API-интерфейсов в API управления Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>Как toocreate API в службе управления API Azure
API в API Management представляет набор операций, которые могут быть вызваны клиентскими приложениями. Новые интерфейсы API, создаются в портал издателя hello, а затем hello требуемого операции добавляются. После добавления операций hello hello API добавляется tooa продукта и могут быть опубликованы. После публикации API-Интерфейс может быть подписанным tooand используется разработчиками.

В этом руководстве показано hello первым шагом в процессе hello: как toocreate и настройте новый интерфейс API в службе управления API. Дополнительные сведения о добавлении операций и публикация продукта см. в разделе [как tooan tooadd операций API] [ How tooadd operations tooan API] и [как toocreate и публикация продукта] [ How toocreate and publish a product].

## <a name="create-new-api"> </a>Создание нового API
API-интерфейсы создаются и настраиваются на портале hello издателя. tooaccess hello издателя, щелкните **портал издателя** в hello портала Azure для службы управления API.

![Портал издателя][api-management-management-console]

> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **добавить API**.

![Создание API][api-management-create-api]

Используйте hello **добавьте новый интерфейс API** tooconfigure окно hello новый API.

![Добавление нового API][api-management-add-new-api]

Hello следующие поля, используемые tooconfigure hello новый API.

* **Имя веб-API** предоставляет уникальное и описательное имя для hello API. Он отображается в порталах hello разработчиком и издателем.
* **URL-адрес службы веб-** ссылки hello реализации hello API службы HTTP. API управления перенаправляет запросы toothis адрес.
* **Суффикс URL-адреса API Web** — присоединенных toohello базовый URL-адрес для службы управления hello API. Hello базовый URL-адрес является общим для всех интерфейсов API, расположенных в экземпляре службы управления API. API управления API-интерфейсы отличает их суффикс и таким образом суффикс hello должно быть уникальным для каждого API для данного издателя.
* **Схема URL-адреса API Web** определяет, какие протоколы могут быть используется tooaccess hello API. По умолчанию указан протокол HTTPs.
* toooptionally добавить этот новый продукт tooa API, нажмите кнопку hello **продуктов (необязательно)** раскрывающийся список и выберите продукт. Этот шаг может быть повторяющихся несколько раз tooadd hello API toomultiple продуктов.

После hello требуемого значения настроены, нажмите кнопку **Сохранить**. После создания нового API hello hello сводной страницы для hello API отображается в портал издателя hello.

![Сводные данные API][api-management-api-summary]

## <a name="configure-api-settings"> </a>Настройка параметров API
Можно использовать hello **параметры** tooverify и измените конфигурацию hello API. **Имя веб-API**, **веб-URL-адрес службы**, и **суффикс URL-адрес API** изначально устанавливаются при создании hello API и можно изменить здесь. **Описание** предоставляет дополнительное описание, и **схему URL-адрес API** определяет, какие протоколы могут быть используется tooaccess hello API.

![Параметры API][api-management-api-settings]

Проверка подлинности шлюза tooconfigure hello серверной реализации hello API службы, рекомендуется выбрать hello **безопасности** hello вкладку **с учетными данными** раскрывающегося списка можно использовать tooconfigure **HTTP Основные** или **клиентские сертификаты** проверки подлинности. Обычная проверка подлинности toouse HTTP, просто введите учетные данные требуемого hello. Сведения об использовании проверки подлинности сертификата клиента см. в разделе [как toosecure серверными службами с помощью клиента сертификат проверки подлинности в Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].

Hello **безопасности** вкладке также можно использовать tooconfigure **авторизации пользователей** с помощью OAuth 2.0. Дополнительные сведения см. в разделе [как разработчик tooauthorize учетных записей с помощью OAuth 2.0 в Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Параметры базовой проверки подлинности][api-management-api-settings-credentials]

Нажмите кнопку **Сохранить** toosave можно производить любые изменения toohello параметры API.

## <a name="next-steps"> </a>Дальнейшие действия
После создания API и заданы параметры hello, следующие действия hello, tooadd hello операций toohello API, добавьте hello API tooa продукта и опубликовать его, чтобы он был доступен для разработчиков. Дополнительные сведения см. следующие статьи hello.

* [Как tooan tooadd операций API][How tooadd operations tooan API]
* [Как toocreate и публикация продукта][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
