---
title: "Azure Active Directory B2C. Добавление учетной записи Майкрософт (MSA) в качестве поставщика удостоверений с помощью пользовательских политик"
description: "Пример использования Майкрософт в качестве поставщика удостоверений с помощью протокола OpenID Connect (OIDC)"
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C. Добавление учетной записи Майкрософт (MSA) в качестве поставщика удостоверений с помощью пользовательских политик

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

В этой статье показано, как tooenable вход для пользователей из учетной записи Майкрософт (MSA) с использованием hello [настраиваемые политики](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Предварительные требования
Hello завершения шагов в hello [Приступая к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) статьи.

А именно:

1.  Создание приложения для учетной записи Майкрософт.
2.  Добавление hello Microsoft учетной записи приложения ключа tooAzure AD B2C
3.  Добавление политики tooa поставщика утверждений
4.  Регистрация пользователя hello учетной записи Майкрософт утверждений поставщика tooa пути
5.  Отправка tooan политики hello Azure AD B2C клиента и его проверка

## <a name="create-a-microsoft-account-application"></a>Создание приложения для учетной записи Майкрософт
Учетная запись Майкрософт toouse как поставщик удостоверений в Azure Active Directory (Azure AD) B2C, требуется toocreate приложение учетной записи Microsoft и передайте в него hello нужные параметры. Вам потребуется учетная запись Майкрософт. Если у вас нет учетной записи, создайте ее на сайте [https://www.live.com/](https://www.live.com/).

1.  Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) и выполните вход с помощью учетных данных вашей учетной записи Майкрософт.
2.  Нажмите кнопку **Добавить приложение**.

    ![Учетная запись Майкрософт, добавление приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  Укажите **имя** вашего приложения, **адрес электронной почты**, снимите флажок **Мы поможем вам начать работу** и нажмите кнопку **Создать**.

    ![Учетная запись Майкрософт, регистрация приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  Скопируйте значение hello **идентификатор приложения**. Необходимо tooconfigure учетную запись Майкрософт как поставщик удостоверений в вашем клиенте.

    ![Учетная запись Майкрософт — скопировать hello значение идентификатора приложения](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  Щелкните **Добавление платформы**.

    ![Учетная запись Майкрософт: добавление платформы](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  Hello списке платформ выберите **Web**.

    ![Учетная запись Майкрософт — hello платформы списке выберите Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  Введите `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` в hello **URI перенаправления** поля. Замените **{tenant}** именем своего клиента (например, contosob2c.onmicrosoft.com).

    ![Учетная запись Майкрософт, установка URL-адресов перенаправления](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  Щелкните **создать новый пароль** под hello **секреты приложения** раздела. Скопируйте новый пароль hello отображается на экране. Необходимо tooconfigure учетную запись Майкрософт как поставщик удостоверений в вашем клиенте. Данный пароль — важный элемент обеспечения безопасности.

    ![Microsoft учетной записи: создание нового пароля](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Учетная запись Майкрософт — Копировать hello новый пароль](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Hello флажок **поддержки пакета SDK Live** под hello **Дополнительно** раздела. Щелкните **Сохранить**.

    ![Учетная запись Майкрософт: поддержка Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Добавить hello Microsoft учетной записи приложения ключа tooAzure AD B2C
Федерации с учетными записями Microsoft требуется секрет клиента tootrust учетной записи Microsoft Azure AD B2C имени приложения hello. Необходимые toostore вашей учетной записи для Microsoft приложения secert в клиенте Azure AD B2C.   

1.  Клиент Azure AD B2C tooyour перейдите и выберите **B2C параметры** > **Identity Framework качества**
2.  Выберите **ключей политики** ключей tooview hello, доступных в клиенте.
3.  Щелкните **+Добавить**.
4.  В пункте **Параметры** используйте вариант **Вручную**.
5.  Для параметра **Имя** используйте значение `MSASecret`.  
    префикс Hello `B2C_1A_` могут быть добавлены автоматически.
6.  В hello **секрет** введите ваш секрет приложения Майкрософт от https://apps.dev.microsoft.com
7.  Для параметра **Использование ключа** задайте значение **Подпись**.
8.  Нажмите кнопку **Создать**
9.  Убедитесь, что вы создали ключ hello `B2C_1A_MSASecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Добавление поставщика утверждений в политику расширения
Если требуется toosign пользователей в с помощью учетной записи Майкрософт, как поставщик утверждений необходимо toodefine учетной записи Майкрософт. Другими словами необходимо toospecify, Azure AD B2C взаимодействует с конечной точки. Конечная точка Hello предоставляет набор утверждений, которые используются в Azure AD B2C tooverify проверку определенного пользователя.

Определите учетную запись Майкрософт в качестве поставщика утверждений, добавив узел `<ClaimsProvider>` в файл расширения политики:

1.  Откройте файл политики для расширения hello (TrustFrameworkExtensions.xml) из рабочий каталог. Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.
2.  Найти hello `<ClaimsProviders>` раздела
3.  Добавьте следующий фрагмент XML в hello `ClaimsProviders` элемента:

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  Замените значение `client_id` на идентификатор клиента приложения учетной записи Майкрософт.

5.  Сохраните файл hello.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Зарегистрировать tooSign поставщика утверждений учетной записи Майкрософт hello вверх или входа в пути пользователя

На этом этапе Настройка поставщика удостоверений hello, но он не доступен в любом hello регистрации-повышение/вход экранов. Теперь необходимо tooyour пользователя поставщика удостоверений tooadd hello учетную запись Майкрософт `SignUpOrSignIn` пути пользователя. toomake его доступным, мы создаем копию существующего шаблона пути пользователя.  Затем мы добавьте поставщик удостоверений hello учетной записи Майкрософт:

> [!NOTE]
>
>Если ранее вы скопировали hello `<UserJourneys>` элемент из основного файла из файла модуля политики toohello `TrustFrameworkExtensions.xml`, toothis раздел можно пропустить.

1.  Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).
2.  Найти hello `<UserJourneys>` элемент и скопируйте hello всему содержимому `<UserJourneys>` узла.
3.  Откройте файл hello расширения (например, TrustFrameworkExtensions.xml) и найти hello `<UserJourneys>` элемента. Если элемент hello не существует, добавьте его.
4.  Вставьте hello всему содержимому `<UserJournesy>` узел, который вы скопировали как дочерний hello `<UserJourneys>` элемента.

### <a name="display-hello-button"></a>Отображение кнопки hello
Hello `<ClaimsProviderSelections>` элемент определяет список hello параметры выбора поставщика утверждений и их порядок.  `<ClaimsProviderSelection>`элемент является аналогом tooan кнопку поставщика удостоверений на странице регистрации-повышение/вход. При добавлении `<ClaimsProviderSelection>` элемент для учетной записи Майкрософт, новая кнопка отображается, когда пользователь попадает на странице приветствия. tooadd этого элемента:

1.  Найти hello `<UserJourney>` узел, который содержит `Id="SignUpOrSignIn"` в пути пользователя hello, скопированный.
2.  Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`
3.  Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Действие tooan кнопки ссылки hello
Теперь, когда имеется кнопка на месте, необходимо toolink его tooan действие. Действие Hello в этом случае является для Azure AD B2C toocommunicate с учетной записью Майкрософт tooreceive маркер. Свяжите действие tooan кнопки hello, связывания hello технические профиля для поставщика утверждений вашей учетной записи Майкрософт.

1.  Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.
2.  Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Убедитесь, hello `Id` имеет одинаковое значение, что и hello `TargetClaimsExchangeId` в предшествующих раздел hello
>   * Убедитесь, `TechnicalProfileReferenceId` идентификатор задан toohello технические профиль, созданный ранее (MSA-OIDC).

## <a name="upload-hello-policy-tooyour-tenant"></a>Отправка hello политики tooyour клиента
1.  В hello [портал Azure](https://portal.azure.com), для переключения в hello [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)и откройте hello **Azure AD B2C** колонку.
2.  Выберите **Инфраструктура процедур идентификации**.
3.  Откройте hello **все политики** колонку.
4.  Щелкните **Отправить политику**.
5.  Проверьте **перезаписать hello политики, если он существует** поле.
6.  **Отправка** TrustFrameworkExtensions.xml и убедитесь, что он не позволяет проверки hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Тестирование настраиваемой политики hello с использованием выполнить

1.  Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.
> [!NOTE]
>
>**Теперь запустите** требует по крайней мере одно приложение toobe предварительно зарегистрирован на приветствия клиента. toolearn приложений tooregister. в статье hello Azure AD B2C [приступить к работе](active-directory-b2c-get-started.md) статьи или hello [регистрацию приложения](active-directory-b2c-app-registration.md) статьи.
2.  Откройте **B2C_1A_signup_signin**, hello проверяющей стороны (RP) настраиваемой политики загруженный. Выберите **Запустить сейчас**.
3.  Необходимо будет toosign учетной записью Майкрософт.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[Необязательно] Регистрация пользователя hello учетной записи Майкрософт утверждений поставщика tooProfile изменения пути
Вы можете поставщика удостоверений tooadd hello учетную запись Майкрософт также пользователя tooyour `ProfileEdit` пути пользователя. toomake доступно, мы повторяем hello последние два этапа:

### <a name="display-hello-button"></a>Отображение кнопки hello
1.  Откройте файл hello расширения политики (например, TrustFrameworkExtensions.xml).
2.  Найти hello `<UserJourney>` узел, который содержит `Id="ProfileEdit"` в пути пользователя hello, скопированный.
3.  Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`
4.  Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Действие tooan кнопки ссылки hello
1.  Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.
2.  Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Тестирование настраиваемой политики профиля Редактирование hello с использованием выполнить
1.  Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.
2.  Откройте **B2C_1A_ProfileEdit**, hello проверяющей стороны (RP) настраиваемой политики загруженный. Выберите **Запустить сейчас**.
3.  Необходимо будет toosign учетной записью Майкрософт.

## <a name="download-hello-complete-policy-files"></a>Загрузка файлов политики завершения hello
Необязательно: Мы рекомендуем Построение сценария используется файлы политики настраиваемый после завершения работы Приступая к работе с пользовательских политик перемещайтесь вместо использования этих файлов образца hello.  [Примеры файлов политики для справки](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
