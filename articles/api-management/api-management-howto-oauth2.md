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
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="d40f7-103">Как разработчик tooauthorize учетных записей с помощью OAuth 2.0 в Azure API Management</span><span class="sxs-lookup"><span data-stu-id="d40f7-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="d40f7-104">Многие API-интерфейсы поддерживают [OAuth 2.0](http://oauth.net/2/) toosecure hello API и убедитесь, что только допустимые пользователи имеют доступ, и они доступны только ресурсы toowhich они выполняется под названием.</span><span class="sxs-lookup"><span data-stu-id="d40f7-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="d40f7-105">В Azure API порядок toouse управления интерактивной консоли разработчика с такие интерфейсы API, служба hello позволяет tooconfigure toowork экземпляра вашей службы с вашей OAuth 2.0 включена API.</span><span class="sxs-lookup"><span data-stu-id="d40f7-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="d40f7-106"><a name="prerequisites"> </a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d40f7-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="d40f7-107">В этом руководстве показано, как tooconfigure вашей toouse экземпляра службы управления API авторизации OAuth 2.0 для разработчика учетные записи, но не показывается, как поставщик tooconfigure OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d40f7-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="d40f7-108">Hello конфигурации для каждого OAuth 2.0, поставщик может быть различным, несмотря на то, что шаги hello похожи и образов hello необходимые сведения, используемые в настройке OAuth 2.0 в вашего экземпляра службы управления API hello таким же.</span><span class="sxs-lookup"><span data-stu-id="d40f7-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="d40f7-109">В примерах в этом разделе в качестве поставщика OAuth 2.0 используется служба Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d40f7-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="d40f7-110">Дополнительные сведения о настройке OAuth 2.0, с помощью Azure Active Directory см. в разделе hello [WebApp-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] образца.</span><span class="sxs-lookup"><span data-stu-id="d40f7-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="d40f7-111"><a name="step1"> </a>Настройка сервера авторизации OAuth 2.0 в управлении API</span><span class="sxs-lookup"><span data-stu-id="d40f7-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="d40f7-112">tooget работу, нажмите кнопку **портал издателя** в hello портала Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="d40f7-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="d40f7-114">Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [приступить к работе со службой управления API Azure] [ Get started with Azure API Management] учебника.</span><span class="sxs-lookup"><span data-stu-id="d40f7-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="d40f7-115">Нажмите кнопку **безопасности** из hello **API управления** hello, пункт меню **OAuth 2.0**, а затем нажмите кнопку **добавить сервер авторизации**.</span><span class="sxs-lookup"><span data-stu-id="d40f7-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="d40f7-117">После нажатия кнопки **добавить сервер авторизации**, отображается hello новую форму сервера авторизации.</span><span class="sxs-lookup"><span data-stu-id="d40f7-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![Новый сервер][api-management-oauth2-server-1]

<span data-ttu-id="d40f7-119">Введите имя и описание (необязательно) в hello **имя** и **описание** поля.</span><span class="sxs-lookup"><span data-stu-id="d40f7-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="d40f7-120">Эти поля обязательны для сервера авторизации используется tooidentify hello OAuth 2.0 в текущем экземпляре службы управления API hello и их значения не исходят от сервера hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d40f7-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="d40f7-121">Введите hello **URL-адрес страницы регистрации клиента**.</span><span class="sxs-lookup"><span data-stu-id="d40f7-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="d40f7-122">Эта страница является, где пользователи могут создавать и управлять их учетными записями и изменяется в зависимости от используемого поставщика hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d40f7-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="d40f7-123">Hello **URL-адрес страницы регистрации клиента** точки toohello страницы, что у пользователей, можно использовать toocreate и настроить свои собственные учетные записи для поставщиков OAuth 2.0, которые поддерживают управление учетными записями пользователей.</span><span class="sxs-lookup"><span data-stu-id="d40f7-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="d40f7-124">В некоторых организациях применения этих функциональных возможностей, даже если это поддерживает поставщик hello OAuth 2.0 или не задан.</span><span class="sxs-lookup"><span data-stu-id="d40f7-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="d40f7-125">Если нет Управление пользователями учетных записей, которые настроены для поставщика OAuth 2.0, введите URL заполнитель например hello URL-адрес вашей компании или URL-адреса таких как `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d40f7-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="d40f7-126">Следующий раздел Hello hello формы содержит hello **типы разрешений кода авторизации**, **URL-адрес конечной точки авторизации**, и **метод запроса авторизации** параметры.</span><span class="sxs-lookup"><span data-stu-id="d40f7-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Новый сервер][api-management-oauth2-server-2]

<span data-ttu-id="d40f7-128">Укажите hello **типы разрешений кода авторизации** путем проверки типов требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="d40f7-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="d40f7-129">**Authorization code** (Код авторизации).</span><span class="sxs-lookup"><span data-stu-id="d40f7-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="d40f7-130">Введите hello **URL-адрес конечной точки авторизации**.</span><span class="sxs-lookup"><span data-stu-id="d40f7-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="d40f7-131">Для Azure Active Directory, этот URL-адрес будет примерно toohello URL-адреса, где `<client_id>` заменяется hello идентификатор клиента, который идентифицирует сервер приложений toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d40f7-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="d40f7-132">Hello **метод запроса авторизации** определяет способ отправки запроса авторизации hello server toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d40f7-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="d40f7-133">По умолчанию выбран вариант **GET** .</span><span class="sxs-lookup"><span data-stu-id="d40f7-133">By default **GET** is selected.</span></span>

<span data-ttu-id="d40f7-134">Следующий раздел Hello находится там, где hello **токен URL-адрес конечной точки**, **методы проверки подлинности клиента**, **маркера доступа метод отправки**, и **областьпоумолчанию** указаны.</span><span class="sxs-lookup"><span data-stu-id="d40f7-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Новый сервер][api-management-oauth2-server-3]

<span data-ttu-id="d40f7-136">Сервер Azure Active Directory OAuth 2.0 hello **токен URL-адрес конечной точки** будет иметь следующий формат, hello где `<APPID>` имеет формат hello `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="d40f7-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="d40f7-137">по умолчанию Hello **методы проверки подлинности клиента** — **основные**, и **маркера доступа метод отправки** — **заголовок авторизации**.</span><span class="sxs-lookup"><span data-stu-id="d40f7-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="d40f7-138">Эти значения можно настроить на этот раздел hello форме вместе с hello **область по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="d40f7-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="d40f7-139">Hello **учетные данные клиента** раздел содержит hello **идентификатор клиента** и **секрет клиента**, которой предоставляются во время процесса создания и настройки hello вашей OAuth 2.0 сервер.</span><span class="sxs-lookup"><span data-stu-id="d40f7-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="d40f7-140">Здравствуйте, один раз **идентификатор клиента** и **секрет клиента** указаны, hello **redirect_uri** для hello **код авторизации** создается.</span><span class="sxs-lookup"><span data-stu-id="d40f7-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="d40f7-141">Этот URI является URL-адрес ответа hello tooconfigure используется при настройке сервера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d40f7-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![Новый сервер][api-management-oauth2-server-4]

<span data-ttu-id="d40f7-143">Если **типы разрешений кода авторизации** задано слишком**пароль владельца ресурса**, hello **учетные данные владельца ресурса** раздел является используется toospecify эти учетные записи; в противном случае можно оставить пустым.</span><span class="sxs-lookup"><span data-stu-id="d40f7-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![Новый сервер][api-management-oauth2-server-5]

<span data-ttu-id="d40f7-145">После завершения hello формы щелкните **Сохранить** конфигурации сервера авторизации toosave hello API управления OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d40f7-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="d40f7-146">После сохранения конфигурации сервера hello можно настроить интерфейсы API toouse этой конфигурации, как показано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d40f7-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="d40f7-147"><a name="step2"></a>Настройка API toouse авторизации пользователя OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="d40f7-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="d40f7-148">Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, щелкните имя требуемого hello API hello, **безопасности**и установите флажок hello для **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="d40f7-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![Авторизация пользователя][api-management-user-authorization]

<span data-ttu-id="d40f7-150">Выберите hello требуемого **сервер авторизации** hello раскрывающегося списка и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d40f7-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![Авторизация пользователя][api-management-user-authorization-save]

## <span data-ttu-id="d40f7-152"><a name="step3"></a>Проверки авторизации пользователя hello OAuth 2.0 в hello портал разработчиков</span><span class="sxs-lookup"><span data-stu-id="d40f7-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="d40f7-153">После настройки сервера авторизации OAuth 2.0 и настройки вашей toouse API сервера можно проверить его, перейдя toohello портал разработчиков и вызова интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="d40f7-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="d40f7-154">Нажмите кнопку **портал разработчиков** в правом верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="d40f7-154">Click **Developer portal** in hello top right menu.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="d40f7-156">Нажмите кнопку **API-интерфейсы** в верхнем меню hello и выберите **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="d40f7-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="d40f7-158">Если у вас есть только один API-Интерфейс настройки или видимым tooyour учетной записи, выбрав API-интерфейсы вы перейдете непосредственно toohello операции для этого API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d40f7-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="d40f7-159">Выберите hello **получить ресурс** операцию, нажмите кнопку **откройте консоль**и выберите **код авторизации** hello в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="d40f7-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![Открытие консоли][api-management-open-console]

<span data-ttu-id="d40f7-161">Когда **код авторизации** — флажок установлен, всплывающее окно отображается с hello формы входа поставщика hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="d40f7-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="d40f7-162">В этом примере hello входа в форме обеспечивается Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d40f7-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="d40f7-163">При наличии всплывающих окон отключено, будет предложено tooenable их браузером hello.</span><span class="sxs-lookup"><span data-stu-id="d40f7-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="d40f7-164">После того как вы включите их, выберите **код авторизации** снова и hello будет показана форма входа.</span><span class="sxs-lookup"><span data-stu-id="d40f7-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![входа][api-management-oauth2-signin]

<span data-ttu-id="d40f7-166">После входа hello **заголовки запроса** заполняются `Authorization : Bearer` заголовок, который авторизует запрос hello.</span><span class="sxs-lookup"><span data-stu-id="d40f7-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![Маркер заголовка запроса][api-management-request-header-token]

<span data-ttu-id="d40f7-168">На этом этапе можно настроить hello требуемого значения для оставшихся параметров hello и отправить запрос hello.</span><span class="sxs-lookup"><span data-stu-id="d40f7-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d40f7-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d40f7-169">Next steps</span></span>
<span data-ttu-id="d40f7-170">Дополнительные сведения об использовании OAuth 2.0 и API управления см. ниже hello видео- и сопутствующие [статьи](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="d40f7-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

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

