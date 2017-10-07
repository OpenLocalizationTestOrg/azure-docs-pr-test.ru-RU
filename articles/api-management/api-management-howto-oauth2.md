---
title: "с помощью OAuth 2.0 в Azure API управления учетными записями разработчиков aaaAuthorize | Документы Microsoft"
description: "Узнайте, как tooauthorize пользователей, используя OAuth 2.0 в службе управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>Как разработчик tooauthorize учетных записей с помощью OAuth 2.0 в Azure API Management
Многие API-интерфейсы поддерживают [OAuth 2.0](http://oauth.net/2/) toosecure hello API и убедитесь, что только допустимые пользователи имеют доступ, и они доступны только ресурсы toowhich они выполняется под названием. В Azure API порядок toouse управления интерактивной консоли разработчика с такие интерфейсы API, служба hello позволяет tooconfigure toowork экземпляра вашей службы с вашей OAuth 2.0 включена API.

## <a name="prerequisites"> </a>Предварительные требования
В этом руководстве показано, как tooconfigure вашей toouse экземпляра службы управления API авторизации OAuth 2.0 для разработчика учетные записи, но не показывается, как поставщик tooconfigure OAuth 2.0. Hello конфигурации для каждого OAuth 2.0, поставщик может быть различным, несмотря на то, что шаги hello похожи и образов hello необходимые сведения, используемые в настройке OAuth 2.0 в вашего экземпляра службы управления API hello таким же. В примерах в этом разделе в качестве поставщика OAuth 2.0 используется служба Azure Active Directory.

> [!NOTE]
> Дополнительные сведения о настройке OAuth 2.0, с помощью Azure Active Directory см. в разделе hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] образца.
> 
> 

## <a name="step1"> </a>Настройка сервера авторизации OAuth 2.0 в управлении API
tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API.

![Портал издателя][api-management-management-console]

> [!NOTE]
> Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.
> 
> 

Нажмите кнопку **безопасности** из hello **API управления** hello, пункт меню **OAuth 2.0**, а затем нажмите кнопку **добавить сервер авторизации**.

![OAuth 2.0][api-management-oauth2]

После нажатия кнопки **добавить сервер авторизации**, отображается hello новую форму сервера авторизации.

![Новый сервер][api-management-oauth2-server-1]

Введите имя и описание (необязательно) в hello **имя** и **описание** поля. 

> [!NOTE]
> Эти поля обязательны для сервера авторизации используется tooidentify hello OAuth 2.0 в текущем экземпляре службы управления API hello и их значения не исходят от сервера hello OAuth 2.0.
> 
> 

Введите hello **URL-адрес страницы регистрации клиента**. Эта страница является, где пользователи могут создавать и управлять их учетными записями и изменяется в зависимости от используемого поставщика hello OAuth 2.0. Hello **URL-адрес страницы регистрации клиента** точки toohello страницы, что у пользователей, можно использовать toocreate и настроить свои собственные учетные записи для поставщиков OAuth 2.0, которые поддерживают управление учетными записями пользователей. В некоторых организациях применения этих функциональных возможностей, даже если это поддерживает поставщик hello OAuth 2.0 или не задан. Если нет Управление пользователями учетных записей, которые настроены для поставщика OAuth 2.0, введите URL заполнитель например hello URL-адрес вашей компании или URL-адреса таких как `https://placeholder.contoso.com`.

Следующий раздел Hello hello формы содержит hello **типы разрешений кода авторизации**, **URL-адрес конечной точки авторизации**, и **метод запроса авторизации** параметры.

![Новый сервер][api-management-oauth2-server-2]

Укажите hello **типы разрешений кода авторизации** путем проверки типов требуемого hello. **Authorization code** (Код авторизации).

Введите hello **URL-адрес конечной точки авторизации**. Для Azure Active Directory, этот URL-адрес будет примерно toohello URL-адреса, где `<client_id>` заменяется hello идентификатор клиента, который идентифицирует сервер приложений toohello OAuth 2.0.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

Hello **метод запроса авторизации** определяет способ отправки запроса авторизации hello server toohello OAuth 2.0. По умолчанию выбран вариант **GET** .

Следующий раздел Hello находится там, где hello **токен URL-адрес конечной точки**, **методы проверки подлинности клиента**, **маркера доступа метод отправки**, и **областьпоумолчанию** указаны.

![Новый сервер][api-management-oauth2-server-3]

Сервер Azure Active Directory OAuth 2.0 hello **токен URL-адрес конечной точки** будет иметь следующий формат, hello где `<APPID>` имеет формат hello `yourapp.onmicrosoft.com`.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

по умолчанию Hello **методы проверки подлинности клиента** — **основные**, и **маркера доступа метод отправки** — **заголовок авторизации**. Эти значения можно настроить на этот раздел hello форме вместе с hello **область по умолчанию**.

Hello **учетные данные клиента** раздел содержит hello **идентификатор клиента** и **секрет клиента**, которой предоставляются во время процесса создания и настройки hello вашей OAuth 2.0 сервер. Здравствуйте, один раз **идентификатор клиента** и **секрет клиента** указаны, hello **redirect_uri** для hello **код авторизации** создается. Этот URI является URL-адрес ответа hello tooconfigure используется при настройке сервера OAuth 2.0.

![Новый сервер][api-management-oauth2-server-4]

Если **типы разрешений кода авторизации** задано слишком**пароль владельца ресурса**, hello **учетные данные владельца ресурса** раздел является используется toospecify эти учетные записи; в противном случае можно оставить пустым.

![Новый сервер][api-management-oauth2-server-5]

После завершения hello формы щелкните **Сохранить** конфигурации сервера авторизации toosave hello API управления OAuth 2.0. После сохранения конфигурации сервера hello можно настроить интерфейсы API toouse этой конфигурации, как показано в следующем разделе hello.

## <a name="step2"></a>Настройка API toouse авторизации пользователя OAuth 2.0
Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, щелкните имя требуемого hello API hello, **безопасности**и установите флажок hello для **OAuth 2.0**.

![Авторизация пользователя][api-management-user-authorization]

Выберите hello требуемого **сервер авторизации** hello раскрывающегося списка и нажмите кнопку **Сохранить**.

![Авторизация пользователя][api-management-user-authorization-save]

## <a name="step3"></a>Проверки авторизации пользователя hello OAuth 2.0 в hello портал разработчиков
После настройки сервера авторизации OAuth 2.0 и настройки вашей toouse API сервера можно проверить его, перейдя toohello портал разработчиков и вызова интерфейса API.  Нажмите кнопку **портал разработчиков** в правом верхнем меню hello.

![Портал разработчика][api-management-developer-portal-menu]

Нажмите кнопку **API-интерфейсы** в верхнем меню hello и выберите **Echo API**.

![Echo API][api-management-apis-echo-api]

> [!NOTE]
> Если у вас есть только один API-Интерфейс настройки или видимым tooyour учетной записи, выбрав API-интерфейсы вы перейдете непосредственно toohello операции для этого API-интерфейса.
> 
> 

Выберите hello **получить ресурс** операцию, нажмите кнопку **откройте консоль**и выберите **код авторизации** hello в раскрывающемся списке.

![Открытие консоли][api-management-open-console]

Когда **код авторизации** — флажок установлен, всплывающее окно отображается с hello формы входа поставщика hello OAuth 2.0. В этом примере hello входа в форме обеспечивается Azure Active Directory.

> [!NOTE]
> При наличии всплывающих окон отключено, будет предложено tooenable их браузером hello. После того как вы включите их, выберите **код авторизации** снова и hello будет показана форма входа.
> 
> 

![входа][api-management-oauth2-signin]

После входа hello **заголовки запроса** заполняются `Authorization : Bearer` заголовок, который авторизует запрос hello.

![Маркер заголовка запроса][api-management-request-header-token]

На этом этапе можно настроить hello требуемого значения для оставшихся параметров hello и отправить запрос hello. 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об использовании OAuth 2.0 и API управления см. ниже hello видео- и сопутствующие [статьи](api-management-howto-protect-backend-with-aad.md).

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

