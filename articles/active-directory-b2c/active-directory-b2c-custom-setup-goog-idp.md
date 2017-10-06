---
title: "Azure Active Directory B2C. Добавление Google+ в качестве поставщика удостоверений OAuth2 с помощью пользовательских политик"
description: "Пример использования Google+ в качестве поставщика удостоверений с помощью протокола OAuth2"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Azure Active Directory B2C. Добавление Google+ в качестве поставщика удостоверений OAuth2 с помощью пользовательских политик

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

В этом руководстве показано, как tooenable вход для пользователей с учетной записью Google + за счет использования hello [настраиваемые политики](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Предварительные требования

Hello завершения шагов в hello [Приступая к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) статьи.

А именно:

1.  Создание учетной записи в приложении Google+.
2.  Добавление hello Google + учетная запись приложения ключа tooAzure AD B2C
3.  Добавление политики tooa поставщика утверждений
4.  Регистрация hello Google + учетной записи утверждения поставщика tooa пользователя пути
5.  Отправка tooan политики hello Azure AD B2C клиента и его проверка

## <a name="create-a-google-account-application"></a>Создание приложения для учетной записи Google+
toouse Google + как поставщик удостоверений в Azure Active Directory (Azure AD) B2C должны toocreate приложения Google + и передайте в него hello нужные параметры. Приложение Google+ можно зарегистрировать здесь: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1.  Go toohello [Google Developers Console](https://console.developers.google.com/) и выполните вход с помощью Google + данные своей учетной записи.
2.  Щелкните **Create project** (Создать проект), введите значение в поле **Project name** (Имя проекта) и щелкните **Create** (Создать).

3.  Щелкните hello **меню проекты**.

    ![Учетная запись Google+, меню "Выберите проект"](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  Щелкните hello  **+**  кнопки.

    ![Учетная запись Google+, создание проекта](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  Введите **имя проекта** и нажмите кнопку **Создать**.

    ![Учетная запись Google+, новый проект](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  Подождите, пока проект hello готов и щелкнуть hello **меню проекты**.

    ![Подождите, пока новый проект будет готов toouse Google + учетная запись —](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  Щелкните имя проекта.

    ![Google + учетная запись — нового проекта выберите hello](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  Нажмите кнопку **API диспетчера** и нажмите кнопку **учетные данные** в hello навигации слева.
9.  Нажмите кнопку hello **экран согласия OAuth** вкладку вверху hello.

    ![Учетная запись Google+, настройка окна запроса доступа OAuth](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  Выберите или укажите допустимый **электронный адрес**, заполните поле **Product name** (Название продукта) и нажмите кнопку **Save** (Сохранить).

    ![Google+, учетные данные приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  Щелкните **New credentials** (Создать учетные данные) и выберите **OAuth client ID** (Идентификатор клиента OAuth).

    ![Google+, создание учетных данных приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  Из списка **Application type** (Тип приложения) выберите **Web application** (Веб-приложение).

    ![Google+, выбор типа приложения](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  Укажите **имя** приложения, введите `https://login.microsoftonline.com` в hello **право JavaScript origins** поля, и `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **авторизованные URIперенаправления**поля. Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com). Hello **{tenant}** значение учитывает регистр. Щелкните **Создать**.

    ![Google+, предоставление авторизованных источников JavaScript и URI перенаправления](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  Скопируйте значения hello **идентификатор клиента** и **секрет клиента**. Требуется обоих tooconfigure Google + как поставщика удостоверений в вашем клиенте. **Секрет клиента** — это важные учетные данные безопасности.

    ![Google + - копирования значения hello клиента идентификатор и секрет клиента](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>Добавить hello Google + учетная запись приложения ключа tooAzure AD B2C
С помощью учетных записей Google + отношению федерации требуется секрет клиента tootrust учетной записи Google + Azure AD B2C имени приложения hello. Необходимые toostore секрет приложения Google + в клиенте Azure AD B2C.  

1.  Клиент Azure AD B2C tooyour перейдите и выберите **B2C параметры** > **Identity Framework качества**
2.  Выберите **ключей политики** ключей tooview hello, доступных в клиенте.
3.  Щелкните **+Добавить**.
4.  В пункте **Параметры** используйте вариант **Вручную**.
5.  Для параметра **Имя** используйте значение `GoogleSecret`.  
    префикс Hello `B2C_1A_` могут быть добавлены автоматически.
6.  В hello **секрет** введите ваш секрет приложения Майкрософт от https://apps.dev.microsoft.com
7.  Для параметра **Использование ключа** задайте значение **Подпись**.
8.  Нажмите кнопку **Создать**
9.  Убедитесь, что вы создали ключ hello `B2C_1A_GoogleSecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Добавление поставщика утверждений в политику расширения

Если требуется с помощью учетной записи Google + toosign пользователей в качестве поставщика утверждений требуется toodefine Google + учетная запись. Другими словами необходимо toospecify, Azure AD B2C взаимодействует с конечной точки. Конечная точка Hello предоставляет набор утверждений, которые используются в Azure AD B2C tooverify проверку определенного пользователя.

Определите учетную запись Google+ в качестве поставщика утверждений, добавив узел `<ClaimsProvider>` в файл расширения политики:

1.  Откройте файл политики для расширения hello (TrustFrameworkExtensions.xml) из рабочий каталог. Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.
2.  Найти hello `<ClaimsProviders>` раздела
3.  Добавьте следующий фрагмент XML в hello hello `ClaimsProviders` и замените `client_id` значение с Google + учетная запись приложения ИД клиента перед сохранением файла hello.  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Регистрация hello Google + учетной записи утверждения поставщика tooSign вверх или вход в пути пользователя

Поставщик удостоверений Hello настроена.  Тем не менее не доступен в любом hello регистрации-повышение/вход экранов. Добавить hello Google + пользователя учетной записи удостоверения поставщика tooyour `SignUpOrSignIn` пути пользователя. toomake его доступным, мы создаем копию существующего шаблона пути пользователя.  Затем мы добавьте поставщик удостоверений, hello Google + учетной записи:

>[!NOTE]
>
>Если вы скопировали hello `<UserJourneys>` элемент из основного файла политики toohello расширение файла (TrustFrameworkExtensions.xml) toothis раздел можно пропустить.

1.  Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).
2.  Найти hello `<UserJourneys>` элемент и скопируйте hello всему содержимому `<UserJourneys>` узла.
3.  Откройте файл hello расширения (например, TrustFrameworkExtensions.xml) и найти hello `<UserJourneys>` элемента. Если элемент hello не существует, добавьте его.
4.  Вставьте hello всему содержимому `<UserJournesy>` узел, который вы скопировали как дочерний hello `<UserJourneys>` элемента.

### <a name="display-hello-button"></a>Отображение кнопки hello
Hello `<ClaimsProviderSelections>` элемент определяет список hello параметры выбора поставщика утверждений и их порядок.  `<ClaimsProviderSelection>`элемент является аналогом tooan кнопку поставщика удостоверений на странице регистрации-повышение/вход. При добавлении `<ClaimsProviderSelection>` элемент для учетной записи Google + новая кнопка отображается, когда пользователь попадает на странице приветствия. tooadd этого элемента:

1.  Найти hello `<UserJourney>` узел, который содержит `Id="SignUpOrSignIn"` в пути пользователя hello, скопированный.
2.  Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`
3.  Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Действие tooan кнопки ссылки hello
Теперь, когда имеется кнопка на месте, необходимо toolink его tooan действие. Действие Hello в этом случае является для Azure AD B2C toocommunicate с tooreceive учетной записи Google + маркер.

1.  Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.
2.  Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * Убедитесь, hello `Id` имеет одинаковое значение, что и hello `TargetClaimsExchangeId` в предшествующих раздел hello
> * Убедитесь, `TechnicalProfileReferenceId` идентификатор задан toohello технические профиль, созданный ранее (Google-OAUTH).

## <a name="upload-hello-policy-tooyour-tenant"></a>Отправка hello политики tooyour клиента
1.  В hello [портал Azure](https://portal.azure.com), для переключения в hello [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)и откройте hello **Azure AD B2C** колонку.
2.  Выберите **Инфраструктура процедур идентификации**.
3.  Откройте hello **все политики** колонку.
4.  Щелкните **Отправить политику**.
5.  Проверьте **перезаписать hello политики, если он существует** поле.
6.  **Отправка** TrustFrameworkExtensions.xml и убедитесь, что он не позволяет проверки hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Тестирование настраиваемой политики hello с использованием выполнить
1.  Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.

    >[!NOTE]
    >
    >    **Теперь запустите** требует по крайней мере одно приложение toobe предварительно зарегистрирован на приветствия клиента. 
    >    toolearn приложений tooregister. в статье hello Azure AD B2C [приступить к работе](active-directory-b2c-get-started.md) статьи или hello [регистрацию приложения](active-directory-b2c-app-registration.md) статьи.


2.  Откройте **B2C_1A_signup_signin**, hello проверяющей стороны (RP) настраиваемой политики загруженный. Выберите **Запустить сейчас**.
3.  Необходимо будет toosign Google + учетной записью.

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[Необязательно] Регистрация hello Google + учетной записи утверждения поставщика tooProfile изменить пользователя пути
Вы можете tooadd hello Google + учетной записи поставщика удостоверений также пользователя tooyour `ProfileEdit` пути пользователя. toomake доступно, мы повторяем hello последние два этапа:

### <a name="display-hello-button"></a>Отображение кнопки hello
1.  Откройте файл hello расширения политики (например, TrustFrameworkExtensions.xml).
2.  Найти hello `<UserJourney>` узел, который содержит `Id="ProfileEdit"` в пути пользователя hello, скопированный.
3.  Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`
4.  Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Действие tooan кнопки ссылки hello
1.  Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.
2.  Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Тестирование настраиваемой политики профиля Редактирование hello с использованием выполнить

1.  Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.
2.  Откройте **B2C_1A_ProfileEdit**, hello проверяющей стороны (RP) настраиваемой политики загруженный. Выберите **Запустить сейчас**.
3.  Необходимо будет toosign Google + учетной записью.

## <a name="download-hello-complete-policy-files"></a>Загрузка файлов политики завершения hello
Необязательно: Мы рекомендуем Построение сценария используется файлы политики настраиваемый после завершения работы Приступая к работе с пользовательских политик перемещайтесь вместо использования этих файлов образца hello.  [Примеры файлов политики для справки](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
