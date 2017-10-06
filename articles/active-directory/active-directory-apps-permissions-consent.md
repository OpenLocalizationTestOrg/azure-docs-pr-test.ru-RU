---
title: "Приложения, разрешения и согласие в Azure Active Directory | Документация Майкрософт"
description: "Azure AD Connect интегрирует локальные каталоги с Azure Active Directory. Это позволяет tooprovide общего удостоверения для приложений Office 365, Azure и SaaS интегрированы с Azure AD."
keywords: "Введение tooAzure AD, приложений, что такое Azure AD Connect установки active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Приложения, разрешения и согласие в Azure Active Directory
В Azure Active Directory можно добавить каталог tooyour приложений.  приложения Hello можно по-разному в зависимости от типа приложения hello.  tooview приложения hello классическом портале, выберите каталог и выберите приложения.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.

## <a name="types-of-apps"></a>Типы приложений

1. **Приложения с одним клиентом** </br>
    - **Приложения одного клиента** -часто называют tooas бизнес (LOB) приложения. Это hello случай, когда сотрудник вашей организации разрабатывает собственное приложение и хотите пользователей в hello организации toobe может toosign в приложении toohello.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **Прокси приложения приложения** — при предоставлении доступа к локальному приложению, с помощью прокси приложения Azure AD, регистрации приложения одного клиента в клиенте (в дополнение toohello прокси приложения-службы). Это приложение представляет ваше локальное приложение для всех взаимодействий в облаке (например, для проверки подлинности). Прокси-сервер приложений требует Azure AD Basic или более поздних выпусков.


2. **Мультитенантные приложения**
    - **Мультитенантные которых другим пользователям можно разрешить** — аналогично слишком «приложения одного клиента, разрабатывает организации». Основное различие Hello (помимо hello логику в само приложение hello) —, пользователи из других клиентов можно также согласия tooand входа в приложении toohello.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **Мультитенантные приложения других разработчиков, на использование которых может дать согласие Contoso.** Для краткости их можно назвать приложениями с обеспечением согласия. Это сторона hello отразить «мультитенантные, разрабатывает организации». Когда другой организации разрабатывает приложения несколькими клиентами, пользователи вашей организации можно согласия toohello приложения и войдите в tooit.
    - **Приложения Майкрософт, получающие данные напрямую из источника** — это приложения, которые представляют службы Майкрософт. Согласие определяется hello факт регистрации службе hello. Это иногда специальные UX и логику для определенных приложений на основном, которая часто используется при создании политики вокруг приложения toohello доступа.</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **Предварительно интегрированных приложений** -приложения, доступные в коллекции приложений Azure AD, которое можно добавить hello tooyour directory tooprovide одного входа (и в некоторых случаях подготовки) toopopular приложений SaaS.
    - **Единый вход Azure AD** — "настоящий" единый вход для приложений, которые могут интегрироваться с Azure AD, по поддерживаемому протоколу входа, например SAML 2.0 или OpenID Connect. Hello мастер поможет вам выполнить его настройка.
    - **Пароль единого входа**: Azure AD безопасно хранит hello учетные данные пользователя для приложения hello и hello учетные данные» вводится» в форму входа hello по hello расширение браузера для доступа к приложению Azure AD. Этот метод также известен как хранение пароля.

## <a name="permissions"></a>Разрешения

При регистрации приложения hello пользователя, выполняющего регистрации приложения hello (то есть разработчик hello) определяет, какое приложение hello разрешения не требуются и какие ресурсы. (hello ресурсы являются, сами по себе, определяется как другие приложения.) Например кто-то построение приложения для чтения почты, установил бы их приложению разрешение «Доступ к почтовым ящикам как пользователя, выполнившего вход hello» hello в hello «Office 365 Exchange Online» ресурсов:
    
![](media/active-directory-apps-permissions-consent/apps6.png)

В порядке для одного приложения (клиент hello) toorequest определенные разрешения из другого приложения (hello ресурс) developer Привет ресурсов приложения hello определяет hello разрешения, которые существуют. В нашем примере Microsoft hello владельца ресурса приложение «Office 365 Exchange Online» hello определено разрешение с именем «Доступ к почтовым ящикам как пользователя, выполнившего вход hello».

При определении разрешений, разработчик приложения hello необходимо определить, если быть дано разрешение hello, или если требуется согласие администратора. Таким образом, разработчики tooconsent tooallow пользователи на своих собственных tooapps запрашиваются только чувствительности низкого разрешения, однако требуются разрешения конфиденциальных toomore tooconsent "Администраторы". Например, Здравствуйте, «Azure Active Directory» ресурсов приложения, определен, поэтому пользователи могут дать согласие tooapps, запрашиваются ограниченные разрешения только для чтения.  Однако для всех разрешений на чтение и запись требуется согласие администратора.

Так как собственные клиенты не проходят проверку подлинности, приложение, определенное в качестве собственного клиентского приложения, может запрашивать только делегированные разрешения. Это означает, что при получении маркера всегда должен присутствовать реальный пользователь. При получении маркера доступа веб-приложения и веб-API (конфиденциальные клиенты) должны всегда проходить проверку подлинности с помощью Azure AD. То есть они также имеют возможность hello запрашиваются разрешения только для приложений. Например, если одна служба внутреннего интерфейса должен tooauthenticate tooanother внутренней службы. Для приложений, запрашивающих разрешения только для приложения, всегда требуется согласие администратора.

Выводы:



- Приложение (клиент) состояний hello разрешения, которые необходимы для других приложений (ресурсы).
- Приложение (ресурс) с сообщением о разрешениях, предоставляемых tooother приложений (клиентов).
- Разрешение может быть разрешением только для приложения или делегированным разрешением.
- Делегированное разрешение может быть отмечено как "Разрешает согласие пользователя" или "Требует согласия администратора".
- Приложения могут вести себя как клиент (объявляя необходимые разрешения tooa ресурсов), как ресурс (объявляя разрешения, которые он предоставляет) или обоими способами.

## <a name="controls"></a>Управление

Hello ниже приведен список hello admin различных элементов управления, доступных для данного поведения. Здравствуйте, администратор, элементы управления можно получить в классическом портале hello из настроить hello в каталоге.

![](media/active-directory-apps-permissions-consent/apps7.png)

В hello Azure портала в разделе **управления**, **параметры пользователя**.

![](media/active-directory-apps-permissions-consent/apps11.png)



- Можно управлять, могут ли пользователи согласия tooapps:

В классическом портале hello, выберите **пользователи могут предоставлять разрешения tooaccess приложений свои данные.**
![](media/active-directory-apps-permissions-consent/apps8.png)

В hello портал Azure, выберите **пользователи разрешают приложениям tooaccess свои данные**.
![](media/active-directory-apps-permissions-consent/apps12.png)



- Можно управлять ли пользователи могут зарегистрировать свои собственные бизнес-приложения одного клиента: В классическом портала выберите hello **пользователи могут добавлять интегрированные приложения.**
![](media/active-directory-apps-permissions-consent/apps9.png)

В hello портал Azure, выберите **пользователи разрешают приложениям tooaccess свои данные**.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>Даже если пользователям разрешено tooregister одного клиента бизнес-приложений, существуют ограничения, toowhat могут быть зарегистрированы.  
>Например, в отношении разработчиков, которые не являются администраторами каталогов.
>
>- Пользователи не могут превратить приложение с одним клиентом в мультитенантное приложение.
>- При регистрации одного клиента бизнес-приложений, пользователи не могут запрашивать приложения tooother разрешения только для приложений.
>- При регистрации одного клиента бизнес-приложений, пользователи не могут запрашивать приложения tooother делегированных разрешений, если эти разрешения требуется согласие администратора.
>- Пользователи не могут вносить изменения tooapps, они не являются владельцами.



- Вы можете указать, могут ли пользователи самостоятельно добавлять предварительно интегрированные приложения, применяющие единый вход с использованием пароля (хранение паролей). ![](media/active-directory-apps-permissions-consent/apps10.png)



- Вы можете определять условия доступа к приложениям (условный доступ). Имейте в виду, что применяется toohello клиентского приложения и toohello ресурсов приложения. Таким образом Предположим, что задать политику условного доступа, о том, что приложение hello «Office 365 Exchange Online» может осуществляться только из машин, которые соответствуют требованиям.  Эта политика также включится при попытке toouse клиентского приложения, запрашивающий tooExchange разрешения в оперативный режим.



- У вас есть видимости, в которой приложения были согласие tooand, какие из них используются.

1.  При согласии пользователя приложение tooan, в клиенте hello создается объект субъекта-службы. В отчет об аудите hello включено Создание субъекта-службы.
2.  Отчеты действия при входе пользователя позволяют понять, какие приложения hello пользователей вход на. 

## <a name="example"></a>Пример

Например рассмотрим приложение «FabrikamMail для Office 365» hello, которое вы заметили, что на вход пользователей в клиенте. FabrikamMail — это приложение для чтения почты для Android, опубликованное компанией Fabrikam, Inc. Это попадает hello» мультитенантные других разработка, которого может дать согласие Contoso».

Если пользователям разрешается tooconsent, они получают hello запрос согласия пользователя при первом входе в:![](media/active-directory-apps-permissions-consent/apps14.png)

«Доступ к почтовых ящиков» строка hello пользовательского интерфейса согласия для разрешение «Доступ к почтовым ящикам как пользователя, выполнившего вход hello» hello, предоставляемые «Office 365 Exchange Online» (то есть Exchange).

Вы увидите разрешения hello, произведя поиск hello объекта субъекта-службы для Exchange (hello ресурса), которая была добавлена, если вы зарегистрировались в Office 365. Можно представить hello объекта субъекта-службы «экземпляр» приложение hello в клиенте, который используется для записи различных параметров и конфигураций.  Это можно увидеть с помощью hello `Get-AzureADServicePrincipal` в PowerShell.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

Согласие инициируется в том случае, когда hello пользователь нажимает кнопку «Принять». Во-первых в клиенте hello создается объект субъекта-службы для «FabrikamMail для Office 365». Hello субъекта-службы выглядит следующим образом:

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Соглашаетесь tooan приложение создает Oauth2PermissionGrant связь между hello следующее:
  
- Hello объекта пользователя
- клиентские приложения Hello ServicePrincipalName (SPN)
- приложения Hello ресурсов ServicePrincipalName (SPN)
- разрешения в приложение hello ресурсов.  

В случае FabrikamMail hello выглядит примерно следующим образом:

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** — идентификатор основной объект службы FabrikamMail (hello, просто создавались) **PrincipalId** — hello объекта идентификатор пользователя (hello пользователя, согласие), **ResourceId**— служба Exchange идентификатор объекта-участника, область является разрешением hello в Exchange, которое было дано).

Если пользователям не разрешается tooconsent, он увидит экран, на котором говорится, что разрешение не требуется.

