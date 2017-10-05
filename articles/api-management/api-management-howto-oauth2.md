---
title: "Авторизация учетных записей разработчиков с помощью протокола OAuth 2.0 в службе управления Azure API | Документация Майкрософт"
description: "Сведения об авторизации пользователей с помощью OAuth 2.0 в службе управления API."
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
ms.openlocfilehash: a19c453bb3271374b587f3d0b35adad55863b490
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-authorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="618ee-103">Авторизация учетных записей разработчиков с помощью протокола OAuth 2.0 в службе управления Azure API</span><span class="sxs-lookup"><span data-stu-id="618ee-103">How to authorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="618ee-104">Многие интерфейсы API поддерживают протокол [OAuth 2.0](http://oauth.net/2/) , позволяющий защитить API, а также и предоставлять доступ только действительным пользователям и только к ресурсам, на которые эти пользователи имеют право.</span><span class="sxs-lookup"><span data-stu-id="618ee-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) to secure the API and ensure that only valid users have access, and they can only access resources to which they're entitled.</span></span> <span data-ttu-id="618ee-105">Чтобы использовать интерактивную  консоль разработчика управления API Azure с такими API, служба позволяет настроить экземпляр службы для работы с API с поддержкой OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="618ee-105">In order to use Azure API Management's interactive Developer Console with such APIs, the service allows you to configure your service instance to work with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="618ee-106"><a name="prerequisites"> </a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="618ee-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="618ee-107">В этом руководстве описано, как настроить экземпляр службы API Management для авторизации учетных записей разработчиков по протоколу OAuth 2.0. В нем не рассматривается настройка поставщика OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="618ee-107">This guide shows you how to configure your API Management service instance to use OAuth 2.0 authorization for developer accounts, but does not show you how to configure an OAuth 2.0 provider.</span></span> <span data-ttu-id="618ee-108">Настройка каждого поставщика OAuth 2.0 имеет свои особенности, хотя инструкции в целом схожи, а данные, необходимые для настройки этого протокола в экземпляре службы API Management, одинаковы.</span><span class="sxs-lookup"><span data-stu-id="618ee-108">The configuration for each OAuth 2.0 provider is different, although the steps are similar, and the required pieces of information used in configuring OAuth 2.0 in your API Management service instance are the same.</span></span> <span data-ttu-id="618ee-109">В примерах в этом разделе в качестве поставщика OAuth 2.0 используется служба Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="618ee-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="618ee-110">Дополнительные сведения о настройке OAuth 2.0 с использованием Azure Active Directory см. в примере [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet].</span><span class="sxs-lookup"><span data-stu-id="618ee-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see the [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="618ee-111"><a name="step1"> </a>Настройка сервера авторизации OAuth 2.0 в управлении API</span><span class="sxs-lookup"><span data-stu-id="618ee-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="618ee-112">Чтобы начать работу, щелкните **Publisher portal** (Портал издателя) на портале Azure для службы управления API.</span><span class="sxs-lookup"><span data-stu-id="618ee-112">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Портал издателя][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="618ee-114">Если экземпляр службы управления API еще не создан, см. раздел [Создание экземпляра управления API][Create an API Management service instance] в руководстве [Начало работы со службой управления Azure API][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="618ee-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="618ee-115">В меню **Управление API** слева выберите пункт **Безопасность**, перейдите на вкладку **OAuth 2.0** и щелкните ссылку **Add authorization server** (Добавить сервер авторизации).</span><span class="sxs-lookup"><span data-stu-id="618ee-115">Click **Security** from the **API Management** menu on the left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![OAuth 2.0][api-management-oauth2]

<span data-ttu-id="618ee-117">После перехода по ссылке **Add authorization server**открывается форма нового сервера авторизации.</span><span class="sxs-lookup"><span data-stu-id="618ee-117">After clicking **Add authorization server**, the new authorization server form is displayed.</span></span>

![Новый сервер][api-management-oauth2-server-1]

<span data-ttu-id="618ee-119">В полях **Имя** и **Описание** введите имя и (при желании) описание.</span><span class="sxs-lookup"><span data-stu-id="618ee-119">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="618ee-120">Эти поля служат для идентификации сервера авторизации OAuth 2.0 в текущем экземпляре службы API Management. Их значения не извлекаются с сервера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="618ee-120">These fields are used to identify the OAuth 2.0 authorization server within the current API Management service instance and their values do not come from the OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="618ee-121">Заполните поле **Client registration page URL** (URL-адрес страницы регистрации клиента).</span><span class="sxs-lookup"><span data-stu-id="618ee-121">Enter the **Client registration page URL**.</span></span> <span data-ttu-id="618ee-122">Это страница, на которой пользователи могут создавать свои учетные записи и управлять ими. Ее URL-адрес зависит от используемого поставщика OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="618ee-122">This page is where users can create and manage their accounts, and varies depending on the OAuth 2.0 provider used.</span></span> <span data-ttu-id="618ee-123">**URL-адрес страницы регистрации клиента** указывает на страницу, на которой пользователи могут создавать и настраивать собственные учетные записи для поставщиков OAuth 2.0, поддерживающих пользовательское управление учетными записями.</span><span class="sxs-lookup"><span data-stu-id="618ee-123">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="618ee-124">В некоторых организациях эта функциональность не настраивается и не используется, даже если поставщик OAuth 2.0 ее поддерживает.</span><span class="sxs-lookup"><span data-stu-id="618ee-124">Some organizations do not configure or use this functionality even if the OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="618ee-125">Если у вашего поставщика OAuth 2.0 не настроено пользовательское управление учетными записями, введите здесь URL-адрес-заполнитель, такой как URL-адрес вашей компании или URL-адрес `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="618ee-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as the URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="618ee-126">В следующем разделе формы содержатся параметры **Authorization code grant types** (Типы предоставления кода авторизации), **Authorization endpoint URL** (URL-адрес конечной точки авторизации) и **Authorization request method** (Метод запроса авторизации).</span><span class="sxs-lookup"><span data-stu-id="618ee-126">The next section of the form contains the **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Новый сервер][api-management-oauth2-server-2]

<span data-ttu-id="618ee-128">Установите нужные флажки в разделе **Authorization code grant types** .</span><span class="sxs-lookup"><span data-stu-id="618ee-128">Specify the **Authorization code grant types** by checking the desired types.</span></span> <span data-ttu-id="618ee-129">**Authorization code** (Код авторизации).</span><span class="sxs-lookup"><span data-stu-id="618ee-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="618ee-130">Введите URL-адрес в поле **Authorization endpoint URL**.</span><span class="sxs-lookup"><span data-stu-id="618ee-130">Enter the **Authorization endpoint URL**.</span></span> <span data-ttu-id="618ee-131">Для Azure Active Directory этот URL-адрес будет аналогичен следующему URL-адресу, где `<client_id>` заменяется идентификатором клиента, по которому сервер OAuth 2.0 опознает ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="618ee-131">For Azure Active Directory, this URL will be similar to the following URL, where `<client_id>` is replaced with the client id that identifies your application to the OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="618ee-132">Параметр **Authorization request method** указывает на то, каким образом запрос авторизации отправляется на сервер OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="618ee-132">The **Authorization request method** specifies how the authorization request is sent to the OAuth 2.0 server.</span></span> <span data-ttu-id="618ee-133">По умолчанию выбран вариант **GET** .</span><span class="sxs-lookup"><span data-stu-id="618ee-133">By default **GET** is selected.</span></span>

<span data-ttu-id="618ee-134">В следующем разделе можно настроить параметры **Token endpoint URL** (URL-адрес конечной точки маркера), **Client authentication methods** (Способы проверки подлинности клиента), **Access token sending method** (Способ отправки маркера доступа) и **Default scope** (Область по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="618ee-134">The next section is where the **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Новый сервер][api-management-oauth2-server-3]

<span data-ttu-id="618ee-136">Для сервера OAuth 2.0 Azure Active Directory параметр**Token endpoint URL** будет иметь следующий формат, где `<APPID>` имеет вид `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="618ee-136">For an Azure Active Directory OAuth 2.0 server, the **Token endpoint URL** will have the following format, where `<APPID>`  has the format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="618ee-137">Параметр **Client authentication methods** по умолчанию имеет значение **Basic** (Обычная), а параметр **Access token sending method** — значение **Authorization header** (Заголовок авторизации).</span><span class="sxs-lookup"><span data-stu-id="618ee-137">The default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="618ee-138">Эти значения можно настроить в данном разделе формы вместе с параметром **Default scope**.</span><span class="sxs-lookup"><span data-stu-id="618ee-138">These values are configured on this section of the form, along with the **Default scope**.</span></span>

<span data-ttu-id="618ee-139">В разделе **Client credentials** (Учетные данные клиента) содержатся поля **Client ID** (Идентификатор клиента) и **Client secret** (Секрет клиента), значения которых получены в ходе создания и настройки сервера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="618ee-139">The **Client credentials** section contains the **Client ID** and **Client secret**, which are obtained during the creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="618ee-140">После определения значений **Client ID** и **Client secret** генерируется параметр **redirect_uri** (URI перенаправления) для **кода авторизации**.</span><span class="sxs-lookup"><span data-stu-id="618ee-140">Once the **Client ID** and **Client secret** are specified, the **redirect_uri** for the **authorization code** is generated.</span></span> <span data-ttu-id="618ee-141">Этот универсальный код ресурса (URI) используется для настройки URL-адреса ответа в конфигурации сервера OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="618ee-141">This URI is used to configure the reply URL in your OAuth 2.0 server configuration.</span></span>

![Новый сервер][api-management-oauth2-server-4]

<span data-ttu-id="618ee-143">Если параметр **Authorization code grant types** имеет значение **Resource owner password** (Пароль владельца ресурса), то в разделе **Resource owner password credentials** (Учетные данные владельца ресурса) нужно указать соответствующие учетные данные. В противном случае эти поля можно оставить пустыми.</span><span class="sxs-lookup"><span data-stu-id="618ee-143">If **Authorization code grant types** is set to **Resource owner password**, the **Resource owner password credentials** section is used to specify those credentials; otherwise you can leave it blank.</span></span>

![Новый сервер][api-management-oauth2-server-5]

<span data-ttu-id="618ee-145">После заполнения формы нажмите кнопку **Save** (Сохранить), чтобы сохранить конфигурацию сервера авторизации OAuth 2.0 для службы API Management.</span><span class="sxs-lookup"><span data-stu-id="618ee-145">Once the form is complete, click **Save** to save the API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="618ee-146">Сохранив конфигурацию сервера, вы можете настроить интерфейсы API для ее использования, как описано в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="618ee-146">Once the server configuration is saved, you can configure APIs to use this configuration, as shown in the next section.</span></span>

## <span data-ttu-id="618ee-147"><a name="step2"> </a>Настройка API для авторизации пользователей по протоколу OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="618ee-147"><a name="step2"> </a>Configure an API to use OAuth 2.0 user authorization</span></span>
<span data-ttu-id="618ee-148">В меню **API Management** (Управление API) слева выберите пункт **APIs** (Интерфейсы API), щелкните имя нужного API, перейдите на вкладку **Security** (Безопасность) и установите флажок **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="618ee-148">Click **APIs** from the **API Management** menu on the left, click the name of the desired API, click **Security**, and then check the box for **OAuth 2.0**.</span></span>

![Авторизация пользователя][api-management-user-authorization]

<span data-ttu-id="618ee-150">В раскрывающемся списке **Authorization server** (Сервер авторизации) выберите нужный пункт и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="618ee-150">Select the desired **Authorization server** from the drop-down list, and click **Save**.</span></span>

![Авторизация пользователя][api-management-user-authorization-save]

## <span data-ttu-id="618ee-152"><a name="step3"> </a>Тестирование авторизации пользователей по протоколу OAuth 2.0 на портале разработчика</span><span class="sxs-lookup"><span data-stu-id="618ee-152"><a name="step3"> </a>Test the OAuth 2.0 user authorization in the Developer Portal</span></span>
<span data-ttu-id="618ee-153">Настроив сервер авторизации OAuth 2.0 и его использование интерфейсом API, вы можете протестировать сервер, перейдя на портал разработчика и вызвав интерфейс API.</span><span class="sxs-lookup"><span data-stu-id="618ee-153">Once you have configured your OAuth 2.0 authorization server and configured your API to use that server, you can test it by going to the Developer Portal and calling an API.</span></span>  <span data-ttu-id="618ee-154">В правом верхнем меню выберите пункт **Developer portal** (Портал разработчика).</span><span class="sxs-lookup"><span data-stu-id="618ee-154">Click **Developer portal** in the top right menu.</span></span>

![Портал разработчика][api-management-developer-portal-menu]

<span data-ttu-id="618ee-156">Щелкните **APIs** в меню вверху и выберите **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="618ee-156">Click **APIs** in the top menu and select **Echo API**.</span></span>

![Echo API][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="618ee-158">Если есть только один настроенный или видимый API для данной учетной записи, тогда щелчок по API сразу приведет к операциям для этого API.</span><span class="sxs-lookup"><span data-stu-id="618ee-158">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="618ee-159">Выберите операцию **GET Resource**, щелкните **Open Console** (Открыть консоль) и выберите в раскрывающемся списке пункт **Authorization code** (Код авторизации).</span><span class="sxs-lookup"><span data-stu-id="618ee-159">Select the **GET Resource** operation, click **Open Console**, and then select **Authorization code** from the drop-down.</span></span>

![Открытие консоли][api-management-open-console]

<span data-ttu-id="618ee-161">После выбора пункта **Authorization code** появляется всплывающее окно с формой входа поставщика OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="618ee-161">When **Authorization code** is selected, a pop-up window is displayed with the sign-in form of the OAuth 2.0 provider.</span></span> <span data-ttu-id="618ee-162">В этом примере форма входа предоставляется службой Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="618ee-162">In this example the sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="618ee-163">Если всплывающие окна отключены, то в браузере появится запрос на их включение.</span><span class="sxs-lookup"><span data-stu-id="618ee-163">If you have pop-ups disabled you will be prompted to enable them by the browser.</span></span> <span data-ttu-id="618ee-164">Включив всплывающие окна, еще раз выберите пункт **Authorization code** , чтобы открыть форму входа.</span><span class="sxs-lookup"><span data-stu-id="618ee-164">After you enable them, select **Authorization code** again and the sign-in form will be displayed.</span></span>
> 
> 

![входа][api-management-oauth2-signin]

<span data-ttu-id="618ee-166">После входа поле **Request headers** (Заголовки запроса) заполняется заголовком `Authorization : Bearer`, используемым для авторизации запроса.</span><span class="sxs-lookup"><span data-stu-id="618ee-166">Once you have signed in, the **Request headers** are populated with an `Authorization : Bearer` header that authorizes the request.</span></span>

![Маркер заголовка запроса][api-management-request-header-token]

<span data-ttu-id="618ee-168">Теперь вы можете настроить остальные параметры и отправить запрос.</span><span class="sxs-lookup"><span data-stu-id="618ee-168">At this point you can configure the desired values for the remaining parameters, and submit the request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="618ee-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="618ee-169">Next steps</span></span>
<span data-ttu-id="618ee-170">Для получения дополнительных сведений об использовании OAuth 2.0 и службы управления API см. следующий видеоролик и эту [статью](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="618ee-170">For more information about using OAuth 2.0 and API Management, see the following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

