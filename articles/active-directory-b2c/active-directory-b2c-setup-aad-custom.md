---
title: "Azure Active Directory B2C. Добавление поставщика Azure AD с помощью пользовательских политик | Документы Майкрософт"
description: "Сведения о пользовательских политиках Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C. Выполнение входа с помощью учетных записей Azure AD

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

В этой статье показано, как tooenable вход для пользователей в определенной организации Azure Active Directory (Azure AD) через использование hello [настраиваемые политики](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Предварительные требования

Hello завершения шагов в hello [Приступая к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) статьи.

А именно:

1. Создание клиента Azure Active Directory B2C (Azure AD B2C).
2. Создание приложения Azure AD B2C.
3. Регистрация двух приложений подсистемы политик.
4. Настройка ключей.
5. Настройка пакета начального приветствия.

## <a name="create-an-azure-ad-app"></a>Создание приложения Azure AD

tooenable вход для пользователей в конкретной организации Azure AD необходимо tooregister приложения в рамках клиента hello организации Azure AD.

>[!NOTE]
> Мы используем «contoso.com» для клиента hello организации Azure AD и «fabrikamb2c.onmicrosoft.com», как клиент Azure AD B2C hello в hello, следуя инструкциям.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
1. На верхней панели hello выберите вашу учетную запись. Из hello **каталога** выберите клиента hello организации Azure AD, где требуется tooregister приложения (contoso.com).
1. Выберите **больше услуг** в левой области hello и выполните поиск «Регистрации приложения».
1. Выберите **Регистрация нового приложения**.
1. Введите значение имя для приложения (например, `Azure AD B2C App`).
1. Выберите **веб-приложения и API** для типа приложения hello.
1. Для **URL-адрес входа**, введите URL-адреса, hello где `yourtenant` заменяется именем hello вашего клиента Azure AD B2C (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Сохранить код приложения hello.
1. Выберите только что созданный hello приложение.
1. В разделе hello **параметры** колонке выберите **ключей**.
1. Создайте ключ и сохраните его. Используется в hello действия, описанные в следующем разделе hello.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Добавление ключа tooAzure hello Azure AD AD B2C

Требуется ключ приложения contoso.com toostore hello в клиенте Azure AD B2C. toodo это:
1. Клиент Azure AD B2C tooyour перейдите и выберите **B2C параметры** > **Identity Framework качества** > **ключи политики**.
1. Щелкните **+Добавить**.
1. Выберите или введите следующие параметры:
   * Выберите **Вручную**.
   * Для параметра **Имя** выберите имя, соответствующее имени клиента Azure AD (например, `ContosoAppSecret`).  префикс Hello `B2C_1A_` автоматически добавляется toohello имя ключа.
   * Вставьте ключ приложения hello **секрет** поле.
   * Выберите **Подпись**.
1. Нажмите кнопку **Создать**.
1. Убедитесь, что вы создали ключ hello `B2C_1A_ContosoAppSecret`.


## <a name="add-a-claims-provider-in-your-base-policy"></a>Добавление поставщика утверждений в базовую политику

Если требуется в toosign пользователей с помощью Azure AD необходимо toodefine Azure AD в качестве поставщика утверждений. Другими словами необходимо toospecify конечную точку, которая будет взаимодействовать Azure AD B2C. Конечная точка Hello предоставит набор утверждений, которые используются в Azure AD B2C tooverify проверку определенного пользователя. 

Azure AD можно определить в качестве поставщика утверждений, добавив Azure AD toohello `<ClaimsProvider>` узла в файле расширения hello политики:

1. Откройте файл расширения hello (TrustFrameworkExtensions.xml) из рабочий каталог.
1. Найти hello `<ClaimsProviders>` раздела. Если он не существует, добавьте его в корневом узле hello.
1. Добавьте новый `<ClaimsProvider>`, как показано ниже.

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. В разделе hello `<ClaimsProvider>` узел, значение hello обновления для `<Domain>` tooa уникальное значение, которое может быть используется toodistinguish его от других поставщиков удостоверений.
1. В разделе hello `<ClaimsProvider>` узел, значение hello обновления для `<DisplayName>` tooa понятное имя для hello поставщика утверждений. В настоящее время это значение не используется.

### <a name="update-hello-technical-profile"></a>Обновление профиля технические hello

tooget токена из конечной точки Azure AD hello необходимо протоколы hello toodefine использование Azure AD B2C toocommunicate с Azure AD. Это выполняется внутри hello `<TechnicalProfile>` элемент `<ClaimsProvider>`.
1. Обновить идентификатор hello hello `<TechnicalProfile>` узла. Этот идентификатор является toothis используется toorefer технические профиль из других частей hello политики.
1. Измените значение в hello `<DisplayName>`. Это значение будет отображаться hello вход кнопку на экране входа.
1. Измените значение в hello `<Description>`.
1. Azure AD использует протокол OpenID Connect hello, поэтому убедитесь, это значение hello для `<Protocol>` — `"OpenIdConnect"`.

Требуется tooupdate hello `<Metadata>` раздела hello XML-файл называется tooearlier tooreflect hello настройки для конкретных клиента Azure AD. В XML-файле hello обновите значения метаданных hello следующим образом:

1. Задать `<Item Key="METADATA">` слишком`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, где `yourAzureADtenant` — это имя клиента Azure AD (contoso.com).
1. Откройте ваш браузер и перейдите toohello `METADATA` URL-адрес, который был обновлен.
1. В браузере hello поиска hello объекта «issuer» и скопируйте его значение. Он должен выглядеть hello следующим образом: `https://sts.windows.net/{tenantId}/`.
1. Вставьте значение hello `<Item Key="ProviderName">` hello XML-файл.
1. Задать `<Item Key="client_id">` toohello код приложения от регистрации приложения hello.
1. Задать `<Item Key="IdTokenAudience">` toohello код приложения от регистрации приложения hello.
1. Убедитесь, что `<Item Key="response_types">` задано слишком`id_token`.
1. Убедитесь, что `<Item Key="UsePolicyInRedirectUri">` задано слишком`false`.

Также необходим секретный hello Azure AD toolink, который зарегистрирован в вашей toohello клиента Azure AD B2C Azure AD `<ClaimsProvider>` сведения:

* В hello `<CryptographicKeys>` раздела hello предшествующий XML-файл, измените значение в hello `StorageReferenceId` toohello идентификатор ссылки секрета hello, которое было определено (например, `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>Отправить файл hello расширения для проверки

К этому моменту вы настроили политикой, чтобы Azure AD B2C известно как toocommunicate с каталогом Azure AD. Попробуйте отправить файл расширения hello вашей tooconfirm только политики, нет ли проблем в данный момент. toodo так:

1. Откройте hello **все политики** колонки в клиенте Azure AD B2C.
1. Проверьте hello **перезаписать hello политики, если он существует** поле.
1. Отправить файл расширения hello (TrustFrameworkExtensions.xml) и что он не выдал hello проверки.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Регистрация пользователя hello Azure AD утверждений поставщика tooa пути

Необходимо tooone tooadd hello Azure AD identity поставщика для вашего пути пользователя. На этом этапе Настройка поставщика удостоверений hello, но он не доступен в любом hello регистрации-повышение/вход экранов. toomake ее доступной, она будет создана копия существующего шаблона пути пользователя и затем изменить ее, чтобы он также поставщика удостоверений hello Azure AD:

1. Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).
1. Найти hello `<UserJourneys>` элемент и скопируйте hello всей `<UserJourney>` узел, который содержит `Id="SignUpOrSignIn"`.
1. Откройте файл hello расширения (например, TrustFrameworkExtensions.xml) и найти hello `<UserJourneys>` элемента. Если элемент hello не существует, добавьте его.
1. Вставить hello всей `<UserJourney>` узел, который вы скопировали как дочерний hello `<UserJourneys>` элемента.
1. Переименуйте идентификатор hello hello новый пользователь пути (например, переименуйте как `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>Экран приветствия «кнопка»

Hello `<ClaimsProviderSelection>` элемент является аналогом tooan удостоверение поставщика кнопку на экране регистрации-повышение/вход. При добавлении `<ClaimsProviderSelection>` элемент для Azure AD новая кнопка отображается, когда пользователь попадает на странице приветствия. tooadd этого элемента:

1. Найти hello `<OrchestrationStep>` узел, который содержит `Order="1"` в только что созданный пользователь путешествия hello.
1. Добавьте hello следующее:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. Задать `TargetClaimsExchangeId` tooan соответствующее значение. Мы рекомендуем следующие hello же соглашениями, что и другие:  *\[ClaimProviderName\]Exchange*.

### <a name="link-hello-button-tooan-action"></a>Действие tooan кнопки ссылки hello

Теперь, когда имеется кнопка на месте, необходимо toolink его tooan действие. Действие Hello в этом случае является для Azure AD B2C toocommunicate с Azure AD tooreceive маркер. Свяжите действие tooan кнопки hello, связывания hello технические профиля для поставщика утверждений Azure AD.

1. Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.
1. Добавьте hello следующее:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. Обновление `Id` toohello одинаковое значение, что и `TargetClaimsExchangeId` в предшествующих раздел hello.
1. Обновление `TechnicalProfileReferenceId` toohello идентификатор hello технические профиля, созданную ранее (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Отправка файла обновленного расширения hello

Изменение файла hello расширения завершено. Сохраните его. Затем отправьте файл hello и убедитесь, что успешного выполнения всех проверок.

### <a name="update-hello-rp-file"></a>Обновить файл RP hello

Требуется tooupdate hello проверяющей стороны (RP) файл, который будет инициировать только что созданный пользователь путешествия hello:

1. Создайте копию SignUpOrSignIn.xml в рабочий каталог и переименуйте его (например, переименуйте его tooSignUpOrSignInWithAAD.xml).
1. Привет открыть новый файл и обновление hello `PolicyId` для атрибута `<TrustFrameworkPolicy>` с уникальным значением (например, SignUpOrSignInWithAAD). <br> Это будет имя hello политики (например, B2C\_1A\_SignUpOrSignInWithAAD).
1. Изменение hello `ReferenceId` атрибута в `<DefaultUserJourney>` toomatch идентификатор hello hello пути нового пользователя, созданного (SignUpOrSignUsingContoso).
1. Сохранить изменения и отправить файл hello.

## <a name="troubleshooting"></a>Устранение неполадок

Тестирование hello пользовательскую политику, которая только что переданный, команду колонке **запустить сейчас**. Узнайте, как проблемы toodiagnose [Устранение неполадок](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Дальнейшие действия

Отправить отзыв слишком[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
