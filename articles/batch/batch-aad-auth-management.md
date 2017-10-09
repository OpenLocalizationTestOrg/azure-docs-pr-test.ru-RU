---
title: "aaaUse Azure Active Directory tooauthenticate пакет управления решения | Документы Microsoft"
description: "Построение приложений с помощью диспетчера ресурсов Azure и поставщик ресурсов пакета hello аутентификации в Azure AD."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Аутентификация решений по управлению пакетной службой с помощью Active Directory

Приложения, вызывающие hello Azure пакета управления службы проверки подлинности в [Azure Active Directory] [ aad_about] (Azure AD). Azure AD — многопользовательский облачный каталог и служба управления удостоверениями корпорации Майкрософт. Azure сама использует Azure AD для проверки подлинности hello клиентов, Администраторы служб и пользователей организации.

Библиотека пакета управления .NET Hello предоставляет типы для работы с учетными записями, ключи учетной записи, приложения и пакеты приложений пакета. Библиотека пакета управления .NET Hello является клиента поставщика ресурсов Azure и используется вместе с [диспетчера ресурсов Azure] [ resman_overview] toomanage эти ресурсы программными средствами. Azure AD — необходимые tooauthenticate запросов, выполненных при помощи любого клиента поставщика ресурсов Azure, включая библиотеку .NET пакета управления hello, а по [диспетчера ресурсов Azure][resman_overview].

В этой статье мы расскажем, с помощью Azure AD tooauthenticate из приложения, использующие библиотеку hello пакета управления .NET. Мы покажем, как tooauthenticate toouse Azure AD администратором подписки или соадминистратором, с помощью встроенной проверки подлинности. Мы используем hello [AccountManagment] [ acct_mgmt_sample] образец проекта, на сайте GitHub, toowalk с помощью Azure AD с библиотекой hello пакета управления .NET.

. в разделе toolearn Подробнее об использовании библиотеки пакета управления .NET hello и образец hello AccountManagement [учетные записи пакета управления и квоты с hello пакета управления клиентской библиотеки для .NET](batch-management-dotnet.md).

## <a name="register-your-application-with-azure-ad"></a>Регистрация приложения в Azure AD

Hello Azure [библиотеку аутентификации Active Directory] [ aad_adal] (ADAL) предоставляет программный интерфейс tooAzure AD для использования в приложениях. toocall ADAL из приложения, необходимо зарегистрировать приложение в клиент Azure AD. При регистрации приложения вы указываете Azure AD с информацией о приложении, включая ее имя в рамках клиента Azure AD hello. Затем Azure AD предоставляет идентификатора приложения используйте tooassociate приложения в Azure AD во время выполнения. toolearn Дополнительные сведения о идентификатор приложения hello, в разделе [приложений и объектов участника службы в Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

hello tooregister AccountManagement образец приложения, выполните действия hello в hello [Добавление приложения](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) статьи [интеграция приложений с Azure Active Directory] [ aad_integrate]. Укажите **собственное клиентское приложение** для типа приложения hello. Здравствуйте, отрасли стандартного URI OAuth 2.0 для hello **URI перенаправления** — `urn:ietf:wg:oauth:2.0:oob`. Тем не менее, можно указать любой допустимый URI (например, `http://myaccountmanagementsample`) для hello **URI перенаправления**, как не обязательно toobe реальные конечной точки:

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

После завершения процесса регистрации hello будет виден идентификатор приложения hello и hello идентификатор объекта (субъекта-службы), указанный для приложения.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Предоставление доступа tooyour hello API диспетчера ресурсов Azure приложения

Далее вам понадобятся toodelegate доступа tooyour приложения toohello API диспетчера ресурсов Azure. Идентификатор Hello Azure AD для hello API диспетчера ресурсов — **API управления службами Windows Azure**.

Выполните следующие действия в hello портал Azure.

1. В области навигации слева hello hello портал Azure, выберите **более служб**, нажмите кнопку **регистрации приложения**и нажмите кнопку **добавить**.
2. Найдите имя приложения в списке hello регистраций приложения hello:

    ![Поиск имени приложения](./media/batch-aad-auth-management/search-app-registration.png)

3. Экран приветствия **параметры** колонку. В hello **доступ к API** выберите **требуемые разрешения**.
4. Нажмите кнопку **добавить** tooadd новый необходимое разрешение. 
5. На шаге 1, введите **API управления службами Windows Azure**, выберите API, который hello список результатов и нажмите кнопку hello **выберите** кнопки.
6. На шаге 2, выберите hello флажок рядом слишком**доступ к Azure классической модели развертывания как пользователи организации**и нажмите кнопку hello **выберите** кнопки.
7. Нажмите кнопку hello **сделать** кнопки.

Hello **требуемые разрешения** колонке теперь показывает, что приложение tooyour разрешения предоставлены tooboth hello ADAL и API диспетчера ресурсов. Разрешения предоставляются tooADAL по умолчанию при первой регистрации приложения в Azure AD.

![Делегировать разрешения toohello API диспетчера ресурсов Azure](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Конечные точки Azure AD

tooauthenticate решениях пакета управления с Azure AD, вам потребуется два хорошо известных конечных точек.

- Hello **Обычная конечная точка Azure AD** предоставляет общие сбора интерфейс при конкретных клиентов не указано, как случае hello встроенной проверки подлинности учетные данные:

    `https://login.microsoftonline.com/common`

- Hello **конечную точку диспетчера ресурсов Azure** является tooacquire используется токен для проверки подлинности службы запросов toohello пакета управления:

    `https://management.core.windows.net/`

AccountManagement пример приложения Hello определяет константы для этих конечных точек. Оставьте их без изменений:

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>Ссылка на идентификатор приложения 

Клиентское приложение использует tooaccess ID (также назывались tooas hello идентификатор клиента) приложения hello Azure AD во время выполнения. После регистрации приложения в Azure portal hello обновите идентификатор приложения код toouse hello, предоставляемые Azure AD для зарегистрированного приложения. В hello AccountManagement образец приложения скопируйте код вашего приложения с подходящей константой hello Azure toohello портала:

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
Кроме того, скопируйте URI, которое определено во время процесса регистрации hello перенаправления hello. Здравствуйте, URI, заданный в коде должен соответствовать hello перенаправления, указанный при регистрации приложения hello URI перенаправления.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Получение маркера проверки подлинности Azure AD

После регистрации примера AccountManagement hello в клиенте Azure AD hello и обновите ваш значениями hello Образец исходного кода, образец hello — Готово tooauthenticate, с помощью Azure AD. При запуске образца hello hello ADAL попыток tooacquire маркер проверки подлинности. На этом этапе предлагается ввести учетные данные Майкрософт: 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

После ввода учетных данных, пример приложения hello продолжением toohello tooissue проверку подлинности запросов управления пакетной службы. 

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о запуске hello [AccountManagement образец приложения][acct_mgmt_sample], в разделе [пакетное управление учетными записями и квоты с hello пакета управления клиентской библиотеки для .NET](batch-management-dotnet.md).

toolearn Дополнительные сведения о Azure AD см. hello [документация Azure Active Directory](https://docs.microsoft.com/azure/active-directory/). Подробные примеры, показывающие, как toouse ADAL доступны в hello [образцы кода Azure](https://azure.microsoft.com/resources/samples/?service=active-directory) библиотеки.

tooauthenticate пакета службы приложения с помощью Azure AD см. [решения службы проверки подлинности пакета с помощью Active Directory](batch-aad-auth.md). 


[aad_about]: ../active-directory/active-directory-whatis.md "Что такое Microsoft Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Сценарии аутентификации в Azure Active Directory"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Интеграция приложений с Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
