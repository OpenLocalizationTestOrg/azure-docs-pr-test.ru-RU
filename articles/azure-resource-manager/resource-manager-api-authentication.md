---
title: "aaaAzure Active Directory проверки подлинности и диспетчер ресурсов | Документы Microsoft"
description: "Для разработчиков руководство по tooauthentication hello API диспетчера ресурсов Azure и Azure Active Directory для интеграции приложения с помощью подписок Azure."
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>Использовать подписки tooaccess проверки подлинности API диспетчера ресурсов
## <a name="introduction"></a>Введение
Если разработчик программного обеспечения, которому нужен toocreate приложение, которое управляет ресурсами Azure клиента, в этом разделе показано, как tooauthenticate с hello API диспетчера ресурсов Azure и получать tooresources доступ в другие подписки.

Приложения могут обращаться к hello API диспетчера ресурсов в двумя способами:

1. **Доступ от имени пользователя.**Используйте этот метод для приложений, осуществляющих доступ к ресурсам от имени выполнившего вход пользователя. Этот метод подходит для приложений, например веб-приложений и программ командной строки, которые осуществляют только интерактивное управление ресурсами Azure.
2. **Доступ только для приложений.**Используйте этот метод для приложений, на которых запущены службы управляющих программ и запланированные задания. удостоверение приложения Hello предоставляется toohello прямой доступ к ресурсам. Этот способ подходит для приложений, которым необходим долгосрочной tooAzure автономного доступа (автоматический режим).

Этот раздел содержит пошаговые инструкции toocreate приложение, которое использует оба эти метода авторизации. В нем показано, как tooperform каждый шаг с помощью API-интерфейса REST или C#. Hello приложения ASP.NET MVC доступна на [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).

## <a name="what-hello-web-app-does"></a>Какое приложение hello web не
Hello веб-приложения:

1. Вход пользователя Azure в систему.
2. Запрашивает доступ пользователя toogrant hello web app tooResource диспетчера.
3. Получение маркера доступа от имени пользователя для доступа к Resource Manager.
4. Использует toocall токена (из шага 3) диспетчера ресурсов и роль участника tooa приложение hello назначение службы в hello подписки, которая предоставляет подписки toohello долгосрочной доступа приложения hello.
5. Получение маркера доступа только для приложений.
6. Использует ресурсы toomanage токена (из шага 5) в подписке hello через диспетчер ресурсов.

Ниже приведена последовательность конца в конец hello hello веб-приложения.

![Поток проверки подлинности Resource Manager](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

Как пользователь, укажите идентификатор подписки hello hello подписки нужно toouse:

![предоставление идентификатора подписки](./media/resource-manager-api-authentication/sample-ux-1.png)

Выберите toouse hello учетной записи для входа.

![выбор учетной записи](./media/resource-manager-api-authentication/sample-ux-2.png)

Укажите свои учетные данные.

![предоставление учетных данных](./media/resource-manager-api-authentication/sample-ux-3.png)

Предоставьте tooyour доступ приложения hello подписок Azure:

![Предоставление доступа](./media/resource-manager-api-authentication/sample-ux-4.png)

Управляйте своими подключенными подписками.

![Подключение подписки](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>Регистрация приложения
Прежде чем приступить к программированию, сначала нужно зарегистрировать веб-приложение в Azure Active Directory (AD). Регистрация приложения Hello создает центра удостоверение для приложения в Azure AD. Она содержит основные сведения о приложении, такие как идентификатор клиента OAuth, URL-адреса ответа и учетные данные, приложение использует tooauthenticate и доступа к API диспетчера ресурсов Azure. Регистрация приложения Hello также записывает hello, различными делегированы разрешения, необходимые приложению при доступе к API-интерфейсы Microsoft от имени пользователя hello.

Так как приложение получает доступ к другой подписке, его необходимо настроить как мультитенантное. Проверка toopass, укажите домен, связанный с Azure Active Directory. toosee hello домены, связанные с Azure Active Directory, вход toohello [классический портал](https://manage.windowsazure.com). Выберите свою службу Azure Active Directory и щелкните **Домены**.

Привет, в следующем примере показано, как tooregister hello приложения с помощью Azure PowerShell. Необходимо иметь hello последнюю версию (августа 2016 г.) Azure PowerShell для этой команды toowork.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

toolog в качестве hello приложения AD, понадобится идентификатор приложения hello и пароль. toosee код приложения hello, возвращенный предыдущей командой hello, используйте:

    $app.ApplicationId

Привет, в следующем примере показано, как tooregister hello приложения с помощью Azure CLI.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

Hello результатов включать hello AppId, который требуется при проверке подлинности, как приложение hello.

### <a name="optional-configuration---certificate-credential"></a>Дополнительная настройка. Учетные данные сертификата
Azure AD также поддерживает учетные данные сертификата для приложений: создать самозаверяющий сертификат, hello закрытый ключ должен оставаться и добавить регистрацию приложения hello открытого ключа tooyour Azure AD. Для проверки подлинности приложение отправляет tooAzure небольшой полезных данных, AD, подписывается с помощью закрытого ключа и Azure AD проверяет подпись hello, с помощью открытого ключа hello, которое вы зарегистрировали.

Сведения о создании приложения AD с помощью сертификата см. в разделе [toocreate использование Azure PowerShell участника службы ресурсы tooaccess](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) или [toocreate использования Azure CLI участника службы ресурсы tooaccess](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>Получение идентификатора клиента из идентификатора подписки
toorequest маркер, который может быть toocall используется диспетчер ресурсов приложению tooknow hello идентификатор клиента hello Azure AD, на котором размещена hello подписки Azure. Скорее всего, пользователи знают идентификаторы подписок, но идентификаторы клиентов Azure Active Directory знает не каждый. tooget hello идентификатор клиента пользователя, попросите пользователя hello для подписки с идентификатором hello. Укажите, идентификатор подписки, при отправке запроса о подписке hello:

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

Hello запроса происходит сбой, так как hello пользователь не вошел еще, hello идентификатор клиента можно получить из ответа hello. В это исключение получить идентификатор клиента hello из hello значение заголовка ответа для **WWW-Authenticate**. Вы видите этой реализации hello [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) метод.

## <a name="get-user--app-access-token"></a>Получение маркера доступа от имени пользователя
Приложение перенаправляет пользователя hello tooAzure AD с помощью OAuth 2.0 авторизовать запрос — tooauthenticate hello учетные данные пользователя и вернуть код авторизации. Приложение использует tooget код авторизации hello маркер доступа для диспетчера ресурсов. Hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) метод создает запрос на авторизацию hello.

В этом разделе показано hello REST API запросов tooauthenticate hello пользователя. Также можно использовать вспомогательные библиотеки tooperform аутентификации в коде. Дополнительные сведения об этих библиотеках см. в статье [Библиотеки проверки подлинности Azure Active Directory](../active-directory/active-directory-authentication-libraries.md). Рекомендации по интеграции функции управления удостоверениями в приложение см. в статье [Руководство разработчика по Azure Active Directory](../active-directory/active-directory-developers-guide.md).

### <a name="auth-request-oauth-20"></a>Запрос проверки подлинности (OAuth 2.0)
Выполните открыть подключение и OAuth2.0 авторизации запросов идентификатора конечной точки Authorize toohello Azure AD:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

Параметры строки запроса Hello, доступные для этого запроса описаны в hello [запрос кода авторизации](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) раздела.

Следующий пример показывает как Hello toorequest OAuth2.0 авторизации:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Azure AD проверяет подлинность пользователя hello и при необходимости запрашивает приложение hello пользователя toogrant разрешение toohello. Он возвращает toohello кода hello авторизации URL-адрес ответа приложения. В зависимости от hello response_mode Azure AD, либо отправляет обратно hello данных в строке запроса или как отправленные данные по запросу.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>Запрос проверки подлинности (Open ID Connect)
Если вы не только обратиться tooaccess диспетчера ресурсов Azure от имени пользователя hello, но также позволяют toosign hello пользователя в приложении tooyour, с помощью учетной записи Azure AD, отправить откройте идентификатор подключения авторизовать запрос. Откройте подключение идентификатор приложения также получают id_token из Azure AD, что приложения могут использовать toosign hello пользователя.

Параметры строки запроса Hello, доступные для этого запроса описаны в hello [запрос входа hello отправки](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) раздела.

Пример запроса Open ID Connect:

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Azure AD проверяет подлинность пользователя hello и при необходимости запрашивает приложение hello пользователя toogrant разрешение toohello. Он возвращает toohello кода hello авторизации URL-адрес ответа приложения. В зависимости от hello response_mode Azure AD, либо отправляет обратно hello данных в строке запроса или как отправленные данные по запросу.

Пример ответа Open ID Connect:

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>Запрос токена (предоставление кода OAuth 2.0)
Теперь, когда приложение получило hello код авторизации из Azure AD, это маркер доступа hello tooget времени для диспетчера ресурсов Azure.  Учет маркеров запрос OAuth2.0 кода Grant toohello токена Azure AD конечной точки:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Параметры строки запроса Hello, доступные для этого запроса описаны в hello [используйте код авторизации hello](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) раздела.

Hello в следующем примере показан запрос для маркера предоставление кода с помощью учетных данных пароля.

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

При работе с учетными данными сертификата, создайте JSON Web Token (JWT) и знак (RSA-SHA256) с помощью закрытого ключа учетных данных сертификата приложения hello. Hello утверждение для маркера hello отображаются типы в [утверждения маркера JWT](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims). Справочную информацию см. в разделе hello [кода библиотеки проверки подлинности Active Directory (.NET)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign маркеры JWT утверждение клиента.

В разделе hello [спецификации Open ID подключения](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) подробные сведения о проверке подлинности клиента.

Hello в следующем примере показан запрос для кода маркера предоставление учетных данных сертификата.

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

Пример ответа для токена предоставления кода:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>Обработка ответа токена предоставления кода
Успешный ответ маркера содержит маркер доступа hello (пользователя и приложения) для диспетчера ресурсов Azure. Приложение использует этот доступ маркера tooaccess диспетчера ресурсов от имени пользователя hello. время жизни Hello маркеров доступа, выданный Azure AD — один час. Маловероятно, что веб-приложения требуется маркер доступа toorenew hello (пользователя и приложения). Если требуется маркер доступа toorenew hello, используйте токен обновления hello, получаемых приложением в ответ на токен hello. Учет маркеров запроса OAuth2.0 toohello токена Azure AD конечной точки:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Hello toouse параметры с запросом hello обновления описаны в разделе [обновление токена доступа hello](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).

Hello следующем примере показано, как токен обновления toouse hello:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Токены обновления могут быть используется tooget новых токенов доступа для диспетчера ресурсов Azure, но они не подходит для автономного доступа для приложения. время жизни маркеров обновления Hello ограничен и токены обновления являются toohello связанного пользователя. Если hello пользователь оставляет hello организации, с помощью токена обновления hello приложения hello теряет доступ. Этот способ не подходит для приложений, используемых командами toomanage свои ресурсы Azure.

## <a name="check-if-user-can-assign-access-toosubscription"></a>Проверьте, если пользователь может назначать toosubscription доступа
Приложение теперь имеет токен tooaccess диспетчера ресурсов Azure от имени пользователя hello. Hello следующим шагом является tooconnect подписки toohello приложения. После подключения, приложения могут управлять эти подписки даже в том случае, если пользователь hello не существуют (долгосрочной автономного доступа).

Для каждой подписки tooconnect, вызовите hello [разрешения списка диспетчера ресурсов](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine ли hello пользователь имеет права управления доступом для hello подписки.

Hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) этот вызов реализует метод hello пример приложения ASP.NET MVC.

Следующий пример показывает как Hello toorequest разрешения пользователя для подписки. 83cfe939-2402-4581-b761-4f59b0a041e4 — идентификатор hello hello подписки.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

Примером разрешения пользователя tooget hello ответа на подписки является:

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

разрешения Hello API возвращает несколько разрешений. Каждое разрешение состоит из разрешенных действий (actions) и запрещенных действий (notActions). Если действие, которое присутствует в hello допускается любое разрешение список действий и не присутствует в списке notactions hello этого разрешения, пользователь hello допускается tooperform это действие. **Microsoft.Authorization/roleassignments/Write** — действие hello, который предоставляет доступ management rights. Приложение необходимо выделить toolook результат hello разрешения для сопоставления регулярных выражений в строку этого действия в действиях hello и notactions всех разрешений.

## <a name="get-app-only-access-token"></a>Получение маркера доступа только для приложений
Теперь вы знаете, если hello пользователя можно назначить доступ toohello подписки Azure. следующие действия Hello таковы.

1. Назначьте hello соответствующие RBAC роли tooyour удостоверение приложения в подписке hello.
2. Проверьте назначение доступа hello путем запроса разрешений приложения hello в подписке hello, или обратившись токен только приложения с помощью диспетчера ресурсов.
3. Соединение записей hello в структуре данных приложения «подключенных подписками» — сохранение hello идентификатор подписки hello.

Давайте взглянем на первом шаге hello ближе. tooassign hello соответствующие RBAC роли toohello удостоверения приложения, необходимо определить:

* Идентификатор объекта Hello удостоверение приложения в hello пользователя Azure Active Directory
* Идентификатор роли RBAC hello, приложению в подписке hello Hello

Когда приложение впервые проверяет подлинность пользователя из Azure AD, в этом экземпляре Azure AD создается объект субъекта-службы для приложения. Azure позволяет toobe роли RBAC назначены участникам tooservice toogrant прямой доступ toocorresponding приложения в ресурсах Azure. Это действие именно то, что мы желаем toodo. Идентификатор запроса hello Azure AD Graph API toodetermine hello hello субъекта-службы приложения в hello выполнившего вход пользователя в Azure AD.

Имеется только маркер доступа для диспетчера ресурсов Azure — нужно новый hello toocall токена доступа к API Azure AD Graph. Каждое приложение в Azure AD имеет разрешение tooquery свой собственный объект участника службы, поэтому достаточно маркер доступа только для приложений.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>Получение маркера доступа только для приложений для API Graph Azure AD
tooauthenticate приложения и получить токен tooAzure AD Graph API, выдавать OAuth2.0 предоставление учетных данных клиента потока запроса маркера tooAzure AD маркера конечной точки (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/токен**).

Hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) метод hello пример приложения ASP.net MVC получает доступ только для приложений маркера для Graph API с помощью hello библиотеку аутентификации Active Directory для .NET.

Параметры строки запроса Hello, доступные для этого запроса описаны в hello [запроса на токен доступа](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) раздела.

Пример запроса на токен предоставления учетных данных клиента:

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

Пример ответа токена предоставления учетных данных клиента:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>Получение идентификатора объекта субъекта-службы приложения в Azure AD пользователя
Теперь воспользуйтесь hello tooquery токена доступа только для приложения hello [субъекты-службы Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) hello toodetermine API идентификатор объекта участника-службы приложения hello в каталоге hello.

Hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) этот вызов реализует метод hello пример приложения ASP.net MVC.

Следующий пример показывает как Hello toorequest участника-службы приложения. a0448380-c346-4f9f-b897-c18733de9394 — hello идентификатор клиента приложения hello.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

Hello примере показан запрос toohello ответа для приложения службы субъекта

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Получение идентификатора роли RBAC Azure
tooassign hello соответствующие RBAC роли tooyour субъекта-службы, необходимо определить идентификатор hello роли Azure RBAC hello.

Hello справа роль RBAC для приложения:

* Если приложение наблюдает только за подписку hello без внесения изменений, требуются только разрешения чтения на hello подписки. Назначить hello **чтения** роли.
* Если приложение управляет подписки Azure hello, создание или изменение или удаление сущностей, он требует наличия разрешения участника hello.
  * toomanage определенного типа ресурсов, назначение ролей для конкретного ресурса участника hello (участника виртуальной машины, виртуальные сети участника, участник учетной записи хранилища, и т. д.)
  * toomanage какой-либо тип ресурса, назначьте hello **участника** роли.

Hello назначение ролей для приложения является видимым toousers, поэтому выберите hello наименьших необходимых прав доступа.

Вызовите hello [определение роли диспетчера ресурсов API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist все роли Azure RBAC и поиска затем перебора hello результат toofind hello требуемого определения роли по имени.

Hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) этот вызов реализует метод hello пример приложения ASP.net MVC.

Hello следующий запрос в примере как идентификатор роли tooget Azure RBAC. 09cbd307-aa71-4aca-b346-5f253e6e3ebb — идентификатор hello hello подписки.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

Hello ответа имеет hello следующий формат:

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

Необязательно toocall этот API на постоянной основе. После определения Здравствуйте хорошо известный идентификатор GUID hello определения роли, можно сконструировать идентификатор определения роли hello как:

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

Ниже приведены hello хорошо известные идентификаторы GUID часто используемых встроенных ролей.

| Роль | Guid |
| --- | --- |
| Читатель |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| Участник |b24988ac-6180-42a0-ab88-20f7382dd24c |
| Участник виртуальной машины |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| Участник виртуальной сети |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| Участник учетной записи хранения |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| Участник веб-сайта |de139f84-1756-47ae-9be6-808fbbe84772 |
| Участник веб-плана |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| Участник SQL Server |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| Участник БД SQL |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>Назначьте роль tooapplication RBAC
У вас есть все необходимое tooassign hello соответствующие RBAC роли tooyour участника-службы с помощью hello [диспетчера ресурсов создать назначение ролей](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.

Hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) этот вызов реализует метод hello пример приложения ASP.net MVC.

Пример запроса tooassign RBAC роли tooapplication:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

В запросе hello используются hello следующие значения:

| Guid | Описание |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |Идентификатор Hello hello подписки |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |Идентификатор объекта Hello hello участника-службы приложения hello |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |Идентификатор роли модуля чтения hello Hello |
| 4f87261d-2816-465d-8311-70a27558df4c |новый идентификатор guid, созданный для hello создать назначение ролей |

Hello ответа имеет hello следующий формат:

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>Получение маркера доступа только для приложений для Azure Resource Manager
toovalidate приложение имеет доступ hello требуемого hello подписки, выполните задачу теста на hello подписки с помощью маркера только для приложений.

tooget маркер доступа только для приложений, следуйте инструкциям из раздела [получить маркер доступа только для приложений для Azure AD Graph API](#app-azure-ad-graph), с другим значением параметра hello ресурсов:

    https://management.core.windows.net/

Hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) метод hello пример приложения ASP.NET MVC получает доступ только для приложений для диспетчера ресурсов Azure с помощью токена hello библиотеку аутентификации Active Directory для .net.

#### <a name="get-applications-permissions-on-subscription"></a>Получение разрешений приложения для подписки
toocheck, ваше приложение имеет hello требуемого доступ на подписку Azure, может также вызвать hello [разрешения диспетчера ресурсов](https://docs.microsoft.com/rest/api/authorization/permissions) API. Этот подход является аналогичные toohow определить, имеет ли пользователь hello права управления доступом для hello подписки. Однако на этот раз вызовите hello разрешения API с маркером доступа только для приложения hello, полученный в предыдущем шаге hello.

Hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) этот вызов реализует метод hello пример приложения ASP.NET MVC.

## <a name="manage-connected-subscriptions"></a>Управление подключенными подписками
При соответствующей роли RBAC hello назначен субъект-служба приложения tooyour в подписке hello, приложения можно сохранить мониторинг и управление его с помощью маркера доступа только для приложений для диспетчера ресурсов Azure.

Если владелец подписки удаляет назначение роли приложения с помощью классического портала hello или средства командной строки, приложение будет tooaccess больше не будет этой подписки. В этом случае необходимо hello пользователь уведомляется о том, что hello соединение с подпиской hello было разорвано из внешнего приложения hello и дать им параметр слишком «восстановить» hello соединения. «Восстановить» повторно просто создать назначение ролей hello, был удален в автономном режиме.

Так же, как вы включили hello пользователя tooconnect подписки tooyour приложения, необходимо разрешить слишком подписки toodisconnect hello пользователя. С access management точки зрения отключите означает удаление назначения ролей hello с субъектом-службой приложения hello в подписке hello. При необходимости состояние приложения hello для hello подписки может быть удалена слишком.
Только пользователи с разрешением доступа управления в подписке hello, может toodisconnect hello подписки.

Hello [RevokeRoleFromServicePrincipalOnSubscription метод](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) пример приложения hello ASP.net MVC реализует этот вызов.

Теперь пользователи могут легко подключать подписки Azure к приложениям и управлять ими с помощью этих подписок.
