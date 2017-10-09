---
title: "aaaUse Azure Active Directory tooauthenticate пакетной службы Azure службы решения | Документы Microsoft"
description: "Пакет поддерживает Azure AD для проверки подлинности из hello пакетной службы."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Аутентификация решений пакетной службы с помощью Active Directory

Пакетная служба Azure поддерживает аутентификацию [Azure Active Directory][aad_about] (Azure AD). Azure AD — многопользовательский облачный каталог и служба управления удостоверениями корпорации Майкрософт. Azure сама использует Azure AD tooauthenticate клиентов, Администраторы служб и пользователей организации.

Процесс аутентификации Azure AD в пакетной службе Azure можно выполнить двумя способами:

- С помощью **встроенной проверки подлинности** tooauthenticate пользователя, который взаимодействует с приложением hello. Приложения с помощью встроенной проверки подлинности собирает учетные данные пользователя и использует эти учетные данные доступа tooauthenticate tooBatch ресурсы.
- С помощью **участника-службы** tooauthenticate автоматической установки приложения. Участника службы определяет политику hello и разрешения для приложения в приложение hello toorepresent заказов, при доступе к ресурсам во время выполнения.

toolearn Дополнительные сведения о Azure AD см. hello [документация Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Режим аутентификации и выделения пула

При создании учетной записи пакетной службы вы можете указать, где должны быть выделены пулы, созданные для этой учетной записи. Вы можете tooallocate пулы hello по умолчанию пакетной службы подписки или в подписку пользователя. Выбор влияет на способ проверки подлинности tooresources доступа в такой учетной записи.

- **Подписка пакетной службы.** По умолчанию пулы выделяются в подписке пакетной службы. Если этот параметр выбран, можно выполнить проверку подлинности tooresources доступа в такой учетной записи с помощью [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) или с помощью Azure AD.
- **Подписка пользователя.** Вы можете tooallocate пулы пакета в подписки пользователя, указанной вами. Если выбран этот вариант, нужно выполнять проверку подлинности с помощью Azure AD.

## <a name="endpoints-for-authentication"></a>Конечные точки аутентификации

tooauthenticate пакета приложений с Azure AD, необходимо tooinclude некоторые хорошо известных конечных точек в коде.

### <a name="azure-ad-endpoint"></a>Конечная точка Azure AD

Базовый Hello конечной точки центра Azure AD:

`https://login.microsoftonline.com/`

tooauthenticate с Azure AD, используйте эту конечную точку, вместе с ИД клиента hello (идентификатор каталога). Идентификатор клиента Hello определяет hello toouse клиента Azure AD для проверки подлинности. tooretrieve Здравствуйте ИД клиента, выполните hello действия, описанные в [получить hello ИД клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> Hello конечная точка клиента требуется при проверке подлинности с помощью субъекта-службы. 
> 
> Hello клиентская конечная точка является обязательным при проверке подлинности с помощью встроенной проверки подлинности, но рекомендуется. Вы также можете использовать Обычная конечная точка Azure AD hello. Hello Обычная конечная точка представляет собой универсальный учетные данные, сбора интерфейс при конкретного клиента не предоставлен. общую конечную точку Hello `https://login.microsoftonline.com/common`.
>
>

Дополнительные сведения о конечных точках Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Конечная точка ресурса пакетной службы

Используйте hello **конечной точки ресурсов пакета Azure** toohello пакетная служба запрашивает tooacquire токен для проверки подлинности:

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Регистрация приложения в клиенте

Hello первый шаг в применении tooauthenticate Azure AD зарегистрировать приложение в клиент Azure AD. Регистрация приложения позволяет toocall hello Azure [библиотеку аутентификации Active Directory] [ aad_adal] (ADAL) в коде. Hello ADAL предоставляет API для проверки подлинности в Azure AD из приложения. Регистрация приложения требуется ли планирование встроенной проверки подлинности toouse или субъектом-службой.

При регистрации приложения необходимо указать сведения о tooAzure вашего приложения AD. Затем Azure AD предоставляет идентификатора приложения используйте tooassociate приложения в Azure AD во время выполнения. toolearn Дополнительные сведения о идентификатор приложения hello, в разделе [приложений и объектов участника службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister пакета приложения, повторите шаги hello в hello [Добавление приложения](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) статьи [интеграция приложений с Azure Active Directory][aad_integrate]. Если приложение регистрируется как собственное приложение, можно указать любой допустимый URI для hello **URI перенаправления**. Не обязательно toobe реальные конечной точки.

После зарегистрировались приложения, вы увидите, что идентификатор hello приложения:

![Регистрация приложения пакетной службы в Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

Дополнительные сведения о регистрации приложения в Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Получить идентификатор клиента hello для Active Directory

Идентификатор клиента Hello определяет hello клиента Azure AD, предоставляет приложение tooyour службы проверки подлинности. tooget Здравствуйте ИД клиента, выполните следующие действия:

1. В hello портал Azure выберите в Active Directory.
2. Щелкните **Свойства**.
3. Скопируйте значение GUID hello, предоставленный для идентификатора hello каталога. Это значение также называется идентификатором hello клиента.

![Скопируйте каталог с Идентификатором hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Использование встроенной аутентификации

tooauthenticate с помощью встроенной проверки подлинности, необходимо toogrant вашей toohello tooconnect разрешения приложения API пакетной службы. Этот шаг включает API приложения tooauthenticate вызовы toohello пакетной службы в Azure AD.

После [регистрации приложения](#register-your-application-with-an-azure-ad-tenant), выполните следующие действия в его доступ к toohello пакетная служба Azure портала toogrant hello:

1. В области навигации слева hello hello портал Azure, выберите **более служб**, нажмите кнопку **регистрации приложения**.
2. Найдите имя приложения в списке hello регистраций приложения hello:

    ![Поиск имени приложения](./media/batch-aad-auth/search-app-registration.png)

3. Откройте hello **параметры** колонку для вашего приложения. В hello **доступ к API** выберите **требуемые разрешения**.
4. В hello **разрешения, необходимые** колонка, щелкните hello **добавить** кнопки.
5. На первом шаге найдите hello API пакета. Поиск для каждого из этих строк, пока не найдете hello API:
    1. **MicrosoftAzureBatch**;
    2. **Microsoft Azure Batch**. Более новые клиенты Azure AD могут использовать это имя.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** идентификатор hello hello API пакета. 
6. Найдя hello API пакета, выберите его и нажмите кнопку hello **выберите** кнопки.
6. На шаге 2, выберите hello флажок рядом слишком**пакетная служба Azure Access** и нажмите кнопку hello **выберите** кнопки.
7. Нажмите кнопку hello **сделать** кнопки.

Hello **требуемые разрешения** колонке теперь показывают, что у приложения Azure AD, доступ к tooboth ADAL и hello API пакетной службы. Разрешения предоставляются tooADAL автоматически при первой регистрации приложения в Azure AD.

![Предоставление разрешений API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Использование субъекта-службы 

tooauthenticate приложения, которое выполняется в автоматическом режиме, используйте участника службы. После зарегистрировались приложения, выполните следующие действия в hello Azure портала tooconfigure участника-службы.

1. Запросите секретный ключ приложения.
2. Назначение роли tooyour RBAC приложения.

### <a name="request-a-secret-key-for-your-application"></a>Запрос секретного ключа приложения

Когда приложение использует для проверки подлинности субъекта-службы, она отправляет идентификатор приложения hello и секретного ключа tooAzure AD. Вам требуется toocreate и скопируйте hello секретного ключа toouse из кода.

Выполните следующие действия в hello портал Azure.

1. В области навигации слева hello hello портал Azure, выберите **более служб**, нажмите кнопку **регистрации приложения**.
2. Найдите имя приложения в списке hello регистраций приложения hello.
3. Экран приветствия **параметры** колонку. В hello **доступ к API** выберите **ключей**.
4. toocreate ключа, введите описание ключа hello. Затем выберите длительность для ключа hello одного или двух лет. 
5. Нажмите кнопку hello **Сохранить** кнопку toocreate и отобразить ключ hello. Скопируйте hello значение ключа tooa надежном месте, как будет tooaccess может его снова после оставить hello колонку. 

    ![Создание секретного ключа](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>Назначение роли tooyour RBAC приложения

tooauthenticate с субъектом-службой необходимо tooassign приложения tooyour RBAC роли. Выполните следующие действия.

1. В hello портал Azure перейдите toohello пакетной учетной записи, используемого приложением.
2. В hello **параметры** колонку для hello пакетной учетной записи, выберите **управления доступа (IAM)**.
3. Нажмите кнопку hello **добавить** кнопки. 
4. Из hello **роли** раскрывающийся список, выберите либо hello _участника_ или _чтения_ роли для приложения. Дополнительные сведения об этих ролях см. в разделе [приступить к работе с элементом управления доступом на основе ролей в hello портал Azure](../active-directory/role-based-access-control-what-is.md).  
5. В hello **выберите** введите имя приложения hello. Выберите приложение из списка hello и нажмите кнопку **Сохранить**.

После этого приложение с назначенной ролью RBAC должно появиться в параметрах контроля доступа. 

![Назначение роли tooyour RBAC приложения](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Получить идентификатор клиента hello для Azure Active Directory

Идентификатор клиента Hello определяет hello клиента Azure AD, предоставляет приложение tooyour службы проверки подлинности. tooget Здравствуйте ИД клиента, выполните следующие действия:

1. В hello портал Azure выберите в Active Directory.
2. Щелкните **Свойства**.
3. Скопируйте значение GUID hello, предоставленный для идентификатора hello каталога. Это значение также называется идентификатором hello клиента.

![Скопируйте каталог с Идентификатором hello](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Примеры кода

Hello в этом разделе примерах кода tooauthenticate с Azure AD с помощью встроенной проверки подлинности, как с субъектом-службой. В этих примерах кода используются .NET, но основные понятия hello аналогичны и для других языков.

> [!NOTE]
> Срок действия маркера проверки подлинности Azure AD истекает через час. При использовании долгоживущие **BatchClient** объекта, мы рекомендуем, что можно получить маркер из ADAL на каждый запрос tooensure всегда имеет допустимый токен. 
>
>
> tooachieve, в .NET, написать метод, извлекает hello токена из Azure AD и передать этот метод tooa **BatchTokenCredentials** как делегат. Hello делегата метод будет вызван на каждый запрос toohello пакетной службы tooensure, предоставляемого допустимый токен. По умолчанию ADAL кэширует маркеры, поэтому новый маркер извлекается из Azure AD только при необходимости. Дополнительные сведения о маркерах в Azure AD см. в статье [Сценарии аутентификации в Azure Active Directory][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Пример кода. Использование встроенной аутентификации Azure AD с библиотекой .NET для пакетной службы

tooauthenticate со встроенной проверкой подлинности из пакета .NET, ссылка hello [пакета Azure .NET](https://www.nuget.org/packages/Azure.Batch/) пакета и hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) пакета.

Включить следующие hello `using` инструкций в коде:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Ссылка hello Azure AD конечной точки в коде, включая hello клиента идентификатор. tooretrieve Здравствуйте ИД клиента, выполните hello действия, описанные в [получить hello ИД клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Справочник по hello пакета ресурсов конечной точки службы:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Укажите ссылку на учетную запись пакетной службы:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Укажите идентификатор приложения hello (идентификатор клиента) для вашего приложения. Идентификатор приложения Hello доступен из регистрации вашего приложения в hello портала Azure:

```csharp
private const string ClientId = "<application-id>";
```

Кроме того, скопируйте URI, которое определено во время процесса регистрации hello перенаправления hello. Здравствуйте, URI, заданный в коде должен соответствовать hello перенаправления, указанный при регистрации приложения hello URI перенаправления:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Запись токена проверки подлинности hello tooacquire метод обратного вызова из Azure AD. Hello **GetAuthenticationTokenAsync** метод обратного вызова, показанный здесь вызывает ADAL tooauthenticate пользователь взаимодействует с приложением hello. Hello **AcquireTokenAsync** метод предоставляемых по ADAL приглашения hello свои учетные данные пользователя, после чего приложение hello выполняется один раз hello пользователя предоставляет их (если он уже добавлен в кэш учетных данных):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Создать **BatchTokenCredentials** объекта, который принимает делегат в качестве параметра hello. Использовать эти учетные данные tooopen **BatchClient** объекта. Можно использовать этот **BatchClient** объекта для последующих операций, выполняемых hello пакетной службы:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>Пример кода. Использование субъекта-службы Azure AD с библиотекой .NET для пакетной службы

tooauthenticate с субъектом-службой из пакета .NET, ссылка hello [пакета Azure .NET](https://www.nuget.org/packages/Azure.Batch/) пакета и hello [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) пакета.

Включить следующие hello `using` инструкций в коде:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Ссылка hello Azure AD конечной точки в коде, включая hello клиента идентификатор. При использовании субъекта-службы необходимо указать конечную точку определенного клиента. tooretrieve Здравствуйте ИД клиента, выполните hello действия, описанные в [получить hello ИД клиента для Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Справочник по hello пакета ресурсов конечной точки службы:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Укажите ссылку на учетную запись пакетной службы:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Укажите идентификатор приложения hello (идентификатор клиента) для вашего приложения. Идентификатор приложения Hello доступен из регистрации вашего приложения в hello портала Azure:

```csharp
private const string ClientId = "<application-id>";
```

Укажите hello секретного ключа, скопированный из hello портала Azure:

```csharp
private const string ClientKey = "<secret-key>";
```

Запись токена проверки подлинности hello tooacquire метод обратного вызова из Azure AD. Hello **GetAuthenticationTokenAsync** метод обратного вызова, здесь показаны вызовы ADAL для автоматической проверки подлинности:

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Создать **BatchTokenCredentials** объекта, который принимает делегат в качестве параметра hello. Использовать эти учетные данные tooopen **BatchClient** объекта. Затем можно использовать, **BatchClient** объекта для последующих операций, выполняемых hello пакетной службы:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о Azure AD см. hello [документация Azure Active Directory](https://docs.microsoft.com/azure/active-directory/). Подробные примеры, показывающие, как toouse ADAL доступны в hello [образцы кода Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) библиотеки.

toolearn Дополнительные сведения о субъектах, в разделе [приложений и объектов участника службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md). toocreate участника службы с помощью hello Azure портала, см. в разделе [использовать приложение портала toocreate Active Directory и участника-службы, могут обращаться к ресурсам](../resource-group-create-service-principal-portal.md). Вы также можете создать субъект-службу с помощью PowerShell или Azure CLI. 

приложения tooauthenticate пакета управления, с помощью Azure AD см. [решения для проверки подлинности пакета управления с помощью Active Directory](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "Что такое Microsoft Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Сценарии аутентификации в Azure Active Directory"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Интеграция приложений с Azure Active Directory"
[azure_portal]: http://portal.azure.com
