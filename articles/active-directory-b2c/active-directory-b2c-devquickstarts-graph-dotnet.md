---
title: "Azure Active Directory B2C: Использование hello Graph API | Документы Microsoft"
description: "Как toocall hello Graph API для клиента B2C с помощью процесса hello tooautomate удостоверения приложения."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>Azure AD B2C: Использовать Graph API hello
Клиенты Azure Active Directory (Azure AD) B2C обычно toobe очень большой. Это означает, что многие распространенные задачи управления клиента должны toobe выполнены программно. Основным примером может служить управление пользователями. Может потребоваться toomigrate существующий клиент B2C tooa хранилища пользователя. Можно toohost регистрации пользователей на веб-узле и создать учетные записи пользователей в вашем каталоге Azure AD B2C фоновом hello. Эти типы задач требуется возможность toocreate hello, чтение, обновление и удаление учетных записей пользователей. Эти задачи можно сделать с помощью API Azure AD Graph hello.

Для клиентов B2C существует два основного режима взаимодействия с Graph API hello.

* Для интерактивного, однократного запуска задачи должен работать от имени учетной записи администратора в клиенте B2C hello при выполнении задач hello. Этот режим требует toosign администратора с использованием учетных данных, перед выполнением этого администратору toohello все вызовы Graph API.
* Для автоматических, непрерывные задачи следует использовать некоторый тип учетной записи службы, который предоставляется с задачами управления tooperform hello необходимые права. В Azure AD это можно сделать путем регистрации приложения и проверка подлинности tooAzure AD. Это делается с помощью **идентификатор приложения** , использующий hello [предоставления учетных данных клиента OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api). В этом случае приложение hello выступает в качестве себя, а не как пользователь, toocall hello Graph API.

В этой статье мы обсудим, как tooperform hello вариант автоматического использования. toodemonstrate, мы выполним сборку .NET 4.5 `B2CGraphClient` , выполняющего пользователя создания, чтения, обновления и удаления (CRUD). Hello будут у клиента Windows интерфейс командной строки (CLI) позволяет вам tooinvoke различные методы. Однако hello код toobehave в неинтерактивной, автоматические виде.

## <a name="get-an-azure-ad-b2c-tenant"></a>Получение клиента Azure AD B2C
До создания приложений или пользователей или вообще взаимодействовать с Azure AD, потребуется клиент Azure AD B2C и учетную запись глобального администратора в клиенте hello. Если у вас нет клиента, создайте его, следуя инструкциям в статье [Предварительная версия Azure Active Directory B2C: создание клиента Azure AD B2C](active-directory-b2c-get-started.md).

## <a name="register-your-application-in-your-tenant"></a>Регистрация приложения в клиенте
После того как вы клиента B2C, необходимо tooregister к приложению через hello [портала Azure](https://portal.azure.com).

> [!IMPORTANT]
> API Graph hello toouse с вашим клиентом B2C, вам потребуется tooregister выделенных приложений с помощью универсального hello *регистрации приложения* колонки в hello портала Azure **не** Azure AD B2C  *Приложения* колонку. Нельзя повторно использовать hello существующие B2C приложений, которые зарегистрированы в Azure AD B2C hello *приложений* колонку.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Выберите клиент Azure AD B2C, выбрав вашей учетной записи в верхнем правом углу hello страницы приветствия.
3. Hello левой панели навигации, выберите **более служб**, нажмите кнопку **регистрации приложения**и нажмите кнопку **добавить**.
4. Следуйте инструкциям hello и создайте новое приложение. 
    1. Выберите **веб-приложения и API** как тип приложения hello.    
    2. Укажите **любой URI перенаправления** (например, https://B2CGraphAPI), так как он неважен в этом примере.  
5. Hello приложение будет показано вверх в списке hello приложений, щелкните ее tooobtain hello **идентификатор приложения** (также известный как идентификатор клиента). Скопируйте его, так как он потребуется вам в одном из следующих разделов.
6. В колонке параметров hello щелкните **ключей** и добавьте новый раздел (также известный как секрет клиента). Также скопируйте его для использования в одном из следующих разделов.

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>Настройка разрешений на создание, чтение и обновление для приложения
Теперь необходимо tooconfigure вашей tooget приложения, которые hello все необходимые разрешения toocreate, чтение, обновление и удаление пользователей.

1. Продолжить в Здравствуйте колонке регистрации приложения портала Azure, выберите приложение.
2. В колонке параметров hello щелкните **требуемые разрешения**.
3. В колонке hello необходимые разрешения, нажмите кнопку **Windows Azure Active Directory**.
4. В колонке hello разрешить доступ, выберите hello **чтение и запись данных каталога** разрешений у **разрешения приложения** и нажмите кнопку **Сохранить**.
5. Наконец, в колонке hello необходимые разрешения, щелкните hello **GRANT, предоставление разрешений** кнопки.

Теперь у вас есть приложение, имеющее разрешения toocreate, чтение и обновление пользователей из вашего клиента B2C.

## <a name="configure-delete-permissions-for-your-application"></a>Настройка разрешений на удаление для приложения
В настоящее время hello *чтение и запись данных каталога* разрешение **не** включают возможность toodo hello удалений, например, удаление пользователей. Если требуется toogive пользователей toodelete возможности приложения hello, необходим toodo эти дополнительные действия, которые включают PowerShell, в противном случае toohello Далее раздел можно пропустить.

Во-первых, загрузите и установите hello [Microsoft Online Services помощник по входу](http://go.microsoft.com/fwlink/?LinkID=286152). Затем загрузите и установите hello [64-разрядного модуля Azure Active Directory для Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).

После установки модуля PowerShell hello, откройте PowerShell и подключения клиента tooyour B2C. После запуска `Get-Credential`, то предложит ввести имя пользователя и пароль, введите имя пользователя hello и пароль учетной записи администратора клиента B2C.

> [!IMPORTANT]
> Требуется toouse B2C учетную запись администратора, **локального** toohello B2C клиента. Эти учетные записи выглядят следующим образом: myusername@myb2ctenant.onmicrosoft.com.

```powershell
Connect-MsolService
```

Теперь мы будем использовать hello **идентификатор приложения** в скрипте hello ниже tooassign hello приложения hello роли учетной записи пользователя администратор которого оно toodelete пользователям разрешается. Эти роли имеют хорошо известные идентификаторы, поэтому все, что нужно toodo является входным вашей **идентификатор приложения** в hello приведенный ниже сценарий.

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

Приложение теперь также имеет разрешения toodelete пользователей из вашего клиента B2C.

## <a name="download-configure-and-build-hello-sample-code"></a>Загрузить, настройки и создания кода образца hello
Во-первых Загрузите образец кода hello и его запуска. После этого мы сможем рассмотреть его подробнее.  Вы можете [загрузить пример кода hello как ZIP-файл](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip). Его можно клонировать в необходимый каталог.

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

Откройте hello `B2CGraphClient\B2CGraphClient.sln` решения Visual Studio в Visual Studio. В hello `B2CGraphClient` проекта, откройте hello файл `App.config`. Замените параметры три приложения hello собственные значения.

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

После этого щелкните правой кнопкой мыши на hello `B2CGraphClient` решение и постройте образец hello. Если вам удастся выполнить это действие, в каталоге `B2CGraphClient\bin\Debug` появится исполняемый файл `B2C.exe`.

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>Создавать пользовательские операции CRUD с помощью hello Graph API
Откройте hello toouse B2CGraphClient, `cmd` Windows команд запроса и изменить ваш каталог toohello `Debug` каталога. Затем запустите hello `B2C Help` команды.

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

Появится краткое описание каждой команды. Каждый раз при вызове одной из этих команд `B2CGraphClient` делает запрос toohello API Azure AD Graph.

### <a name="get-an-access-token"></a>Получение маркера доступа
Любой запрос toohello Graph API требуется маркер доступа для проверки подлинности. `B2CGraphClient`Открытая библиотеку проверки подлинности Active Directory (ADAL) использует hello toohelp получения маркера доступа. ADAL упрощает получение маркеров, так как предоставляет простой API и выполняет некоторые важные действия, такие как кэширование маркеров доступа. У вас нет токенов ADAL tooget toouse, хотя. Их можно получать, составляя HTTP-запросы вручную.

> [!NOTE]
> Этот пример кода использует ADAL v2 в порядке toocommunicate с hello Graph API.  Необходимо использовать ADAL версии 2 или 3 в маркеров доступа tooget заказа, которые можно использовать с hello API Azure AD Graph.
> 
> 

Когда `B2CGraphClient` запускается, он создает экземпляр hello `B2CGraphClient` класса. Устанавливает Hello конструктор для этого класса проверки подлинности ADAL формирование шаблонов:

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

Мы будем использовать hello `B2C Get-User` команду в качестве примера. Когда `B2C Get-User` вызывается без дополнительные входные данные, hello hello вызовов CLI `B2CGraphClient.GetAllUsers(...)` метод. Этот метод вызывает метод `B2CGraphClient.SendGraphGetRequest(...)`, который отправляет Graph API toohello запрос HTTP GET. Прежде чем `B2CGraphClient.SendGraphGetRequest(...)` отправляет Здравствуйте запрос GET, он сначала получает токен доступа с помощью ADAL:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

Вы может получить маркер доступа для hello Graph API, вызывающему Привет ADAL `AuthenticationContext.AcquireToken(...)` метод. ADAL возвращает `access_token` , представляющий удостоверение приложения hello.

### <a name="read-users"></a>Чтение пользователей
При необходимости tooget список пользователей или получить конкретного пользователя из hello Graph API можно отправлять HTTP- `GET` запроса toohello `/users` конечной точки. Запрос для всех пользователей hello в клиенте выглядит следующим образом:

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee этот запрос запуска:

 ```
 > B2C Get-User
 ```

Существует два toonote важных событий.

* Hello токена доступа, полученного через ADAL добавляется toohello `Authorization` заголовок с помощью hello `Bearer` схемы.
* Для клиентов B2C, необходимо использовать параметр запроса hello `api-version=1.6`.

Оба эти данные обрабатываются в hello `B2CGraphClient.SendGraphGetRequest(...)` метод:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>Создание учетных записей пользователей-клиентов
При создании учетных записей пользователей в клиенте B2C можно отправлять HTTP- `POST` запроса toohello `/users` конечной точки:

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

Большая часть этих свойств в данном запросе являются необходимые toocreate пользователей клиента. toolearn, щелкните пункт [здесь](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser). Обратите внимание, что hello `//` комментарии были включены для иллюстрации. Их не нужно добавлять в запрос.

toosee запрос hello, выполните одну из следующих команд hello:

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

Hello `Create-User` команда принимает JSON-файл в качестве входного параметра. Он содержит представление JSON объекта пользователя. Существуют два файла .json образец в примере кода hello: `usertemplate-email.json` и `usertemplate-username.json`. Вы можете изменить эти файлы toosuit вашим потребностям. В дополнение к этому toohello обязательные поля выше, несколько дополнительных полей, которые можно использовать, включаются в эти файлы. Сведения о необязательных полей hello можно найти в hello [Справочник по API Azure AD Graph сущности](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).

Можно увидеть, как создается запрос POST hello в `B2CGraphClient.SendGraphPostRequest(...)`.

* Он присоединяет toohello токена доступа `Authorization` заголовок запроса hello.
* Затем задается параметр `api-version=1.6`.
* Он включает hello объекта пользователя JSON в тексте hello hello запроса.

> [!NOTE]
> Hello учетные записи, следует ли toomigrate из существующего хранилища пользователя имеет нижней стойкость пароля, чем hello [стойкость надежный пароль, обеспечиваемая Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), вы можете отключить hello надежного пароля с помощью hello `DisableStrongPassword`значение в hello `passwordPolicies` свойство. Например, можно изменить hello создайте пользовательский запрос, приведенный выше, следующим образом: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.
> 
> 

### <a name="update-consumer-user-accounts"></a>Обновление учетных записей пользователей-клиентов
При обновлении пользовательские объекты, процесс hello — примерно toohello один использовать toocreate пользовательские объекты. Однако этот процесс использует hello HTTP `PATCH` метод:

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

Попробуйте tooupdate пользователя, обновив файлы JSON с новыми данными. Затем можно использовать `B2CGraphClient` toorun одной из этих команд:

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

Проверять hello `B2CGraphClient.SendGraphPatchRequest(...)` метод подробные сведения о том, как toosend этого запроса.

### <a name="search-users"></a>Поиск пользователей
Искать пользователей в клиенте B2C можно разными способами. Один с помощью hello пользователя идентификатор объекта или две, используя идентификатор входа пользователя hello (т. е. hello `signInNames` свойство).

Выполните одну из следующих hello команд toosearch для конкретного пользователя:

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

Вот несколько примеров.

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>Удаление пользователей
Hello процесс удаления пользователя достаточно прост. Используйте hello HTTP `DELETE` метода и конструкции hello URL-адрес с hello исправьте идентификатор объекта:

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee пример, введите этот команды и представление hello запроса delete, печатной toohello консоли:

```
> B2C Delete-User <object-id-of-user>
```

Проверять hello `B2CGraphClient.SendGraphDeleteRequest(...)` метод подробные сведения о том, как toosend этого запроса.

Можно выполнять многие другие действия с hello API Azure AD Graph в toouser управления сложения. Дополнительные сведения о каждом действии и примеры запросов см. в [справочнике по API Graph для Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog).

## <a name="use-custom-attributes"></a>Использование настраиваемых атрибутов
Большинство приложения-потребители должны toostore своего рода пользовательские сведения профиля. Это можно сделать одним из способов является toodefine настраиваемого атрибута в клиенте B2C. Затем можно считать этот атрибут hello так же, как обрабатывать любые другие свойства в объекте пользователя. Можно обновить атрибут hello атрибут hello delete, запрос по атрибуту hello, отправка hello атрибут в качестве утверждения в маркеры входа в систему и многое другое.

toodefine настраиваемого атрибута в клиенте B2C см hello [ссылку настраиваемого атрибута B2C](active-directory-b2c-reference-custom-attr.md).

Можно просмотреть hello настраиваемых атрибутов, определенных в B2C клиента с помощью `B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

Hello вывода этих функций показывает hello сведения каждого пользовательского атрибута, такие как:

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

Можно использовать полное имя, например hello `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, как свойство объектов-пользователей.  Добавьте в файл .json hello новое свойство и значение для свойства hello, а затем запустите:

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

Использование `B2CGraphClient`позволяет получить приложение-службу, которое обеспечивает управление пользователями клиента B2C программным путем. `B2CGraphClient`использует собственный toohello tooauthenticate удостоверение приложения Azure AD Graph API. Кроме того, B2CGraphClient получает маркеры, используя секрет клиента. Добавляя эту функцию в свое приложение, учитывайте некоторые ключевые особенности приложений B2C.

* Необходимо toogrant hello приложения hello соответствующие разрешения в клиенте hello.
* На данном этапе необходимо токены доступа tooget toouse ADAL (не MSAL). (Кроме того, сообщения протокола можно отправлять напрямую, не используя библиотеку.)
* При вызове Graph API hello использовать `api-version=1.6`.
* При создании и обновлении пользователей-клиентов требуются некоторые свойства, как описано выше.

Если у вас есть вопросы или запросы для действия, которые вы хотите tooperform с помощью Graph API hello на клиенте B2C комментарий в этой статье или файл проблему в репозитории примеров кода hello GitHub.

