---
title: "Azure Active Directory B2C. Добавление поставщика SAML Salesforce с помощью пользовательских политик | Документы Майкрософт"
description: "Дополнительные сведения о том, как toocreate Azure Active Directory B2C пользовательской политики и управлять ими."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C. Выполнение входа с помощью учетных записей Salesforce через SAML

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

В этой статье показано, как toouse [настраиваемые политики](active-directory-b2c-overview-custom.md) tooset копирование вход для пользователей в определенной организации Salesforce.

## <a name="prerequisites"></a>Предварительные требования

### <a name="azure-ad-b2c-setup"></a>Настройка Azure AD B2C

Убедитесь, что выполнены все шаги hello, которые показывают, как слишком[приступить к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) в Azure Active Directory B2C (Azure AD B2C).

В частности, описаны такие возможности:

* Создание клиента Azure AD B2C.
* Создание приложения Azure AD B2C.
* Регистрация двух приложений подсистемы политик.
* Настройка ключей.
* Настройка пакета начального приветствия.

### <a name="salesforce-setup"></a>Настройка Salesforce

В этой статье предполагается, что уже выполнены следующие hello:

* Подписка на учетную запись Salesforce. Вы можете зарегистрироваться для получения [бесплатной учетной записи Developer Edition](https://developer.salesforce.com/signup).
* [Настройка собственного домена](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) для организации Salesforce.

## <a name="set-up-salesforce-so-users-can-federate"></a>Настройка Salesforce для федерации пользователей

toohelp Azure AD B2C взаимодействовать с Salesforce, необходимо, чтобы URL-адрес метаданных Salesforce tooget hello.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Настройка Salesforce в качестве поставщика удостоверений

> [!NOTE]
> В этой статье предполагается, что вы используете [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).

1. [Войдите в tooSalesforce](https://login.salesforce.com/). 
2. На hello влево меню в разделе **параметры**, разверните **удостоверение**и нажмите кнопку **поставщика удостоверений**.
3. Щелкните **Enable Identity Provider** (Включить поставщик удостоверений).
4. В разделе **сертификата выберите hello**выберите hello сертификат, который будет toocommunicate toouse Salesforce с Azure AD B2C. (Можно использовать сертификат по умолчанию hello.) Щелкните **Сохранить**. 

### <a name="create-a-connected-app-in-salesforce"></a>Создание подключенного приложения в Salesforce

1. На hello **поставщика удостоверений** страницы, перейдите в слишком**поставщиков услуг**.
2. Щелкните **Service Providers are now created via Connected Apps. Click here** (Поставщики услуг теперь создаются с помощью подключенных приложений. Щелкните здесь).
3. В разделе **основные сведения**, введите подключенного приложения hello необходимые значения.
4. В разделе **параметры веб-приложения**выберите hello **включить SAML** флажок.
5. В hello **идентификатор сущности** введите следующий URL-адрес hello. Заменили hello значение `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. В hello **URL-адрес ACS** введите следующий URL-адрес hello. Заменили hello значение `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. Оставьте значения по умолчанию hello другие параметры.
8. Прокрутите toohello нижней части списка hello и нажмите кнопку **Сохранить**.

### <a name="get-hello-metadata-url"></a>Получить URL-адрес метаданных hello

1. На странице Общие сведения о подключенных приложения hello, нажмите кнопку **управление**.
2. Скопируйте значение hello для **конечную точку обнаружения метаданных**, а затем сохраните его. Оно будет использоваться далее в этой статье.

### <a name="set-up-salesforce-users-toofederate"></a>Настройка toofederate пользователей Salesforce

1. На hello **управление** страницы подключенных приложений, перейти слишком**профилей**.
2. Щелкните **Управление профилями**.
3. Выберите профили hello (или группы пользователей), которые должны toofederate с Azure AD B2C. Системный администратор, выберите hello **системный администратор** флажок, так что можно создать федерацию с помощью учетной записи Salesforce.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Создание сертификата подписи для Azure AD B2C

Подписанные Azure AD B2C toobe необходимость tooSalesforce отправлены запросы. toogenerate сертификата подписи, откройте Azure PowerShell и выполните следующие команды hello.

> [!NOTE]
> Убедитесь, что необходимо обновить имя клиента hello и пароль в верхнем две строки hello.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Добавить tooAzure подписи сертификата hello SAML AD B2C

Отправьте подписи сертификата клиента Azure AD B2C tooyour hello. 

1. Go tooyour Azure AD B2C клиента. Последовательно выберите **Settings** > **Identity Experience Framework** > **Policy Keys** (Параметры, Инфраструктура процедур идентификации, Ключи политики).
2. Щелкните **+Добавить**, а затем:
    1. Щелкните **Параметры** > **Отправить**.
    2. Введите **имя** (например, SAMLSigningCert). префикс Hello *B2C_1A_* автоматически добавляется toohello имя ключа.
    3. tooselect свой сертификат, выберите **отправить файл управления**. 
    4. Введите пароль сертификата hello, заданный в скрипте PowerShell hello.
3. Щелкните **Создать**.
4. Убедитесь, что ключ создан (например, B2C_1A_SAMLSigningCert). Запишите hello полное имя (включая *B2C_1A_*). Можно будет ссылаться toothis ключ позже в политике hello.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>Создать hello поставщика утверждений Salesforce SAML в базовый политике

Вам требуется toodefine Salesforce в качестве поставщика утверждений, пользователи могут войти в с помощью Salesforce. Другими словами вы должны hello toospecify конечную точку, которая будет взаимодействовать Azure AD B2C. Конечная точка Hello будет *предоставляют* набор *утверждений* , Azure AD B2C использует tooverify проверку определенного пользователя. toodo это, добавьте `<ClaimsProvider>` для Salesforce в файле расширения hello политики:

1. В рабочий каталог откройте файл расширения hello (TrustFrameworkExtensions.xml).
2. Найти hello `<ClaimsProviders>` раздела. Если он не существует, создайте его в корневом узле hello.
3. Добавьте новый `<ClaimsProvider>`:

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

В разделе hello `<ClaimsProvider>` узла:

1. Измените значение hello `<Domain>` tooa уникальное значение, отличающее `<ClaimsProvider>` от других поставщиков удостоверений.
2. Измените значение в hello `<DisplayName>` tooa отображаемое имя для hello поставщика утверждений. Сейчас это значение не используется.

### <a name="update-hello-technical-profile"></a>Обновление профиля технические hello

tooget маркер SAML из Salesforce, определите протоколы hello, использование Azure AD B2C toocommunicate с Azure Active Directory (Azure AD). Для этого в hello `<TechnicalProfile>` элемент `<ClaimsProvider>`:

1. Обновить идентификатор hello hello `<TechnicalProfile>` узла. Этот идентификатор является toothis используется toorefer технические профиль из других частей hello политики.
2. Измените значение в hello `<DisplayName>`. Это значение отображается hello вход кнопку на страницу входа.
3. Измените значение в hello `<Description>`.
4. SalesForce с помощью протокола hello SAML 2.0. Убедитесь, что значение hello для `<Protocol>` — **SAML2**.

Обновление hello `<Metadata>` раздела hello, предшествующий настройки hello tooreflect XML для определенной учетной записи Salesforce. Обновление hello значения метаданных для hello XML:

1. Обновите значение hello `<Item Key="PartnerEntity">` с hello Salesforce URL-адрес метаданных скопированное ранее. Он имеет следующий формат hello: 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. В hello `<CryptographicKeys>` статьи, значение hello обновления для обоих экземпляров `StorageReferenceId` toohello имя hello ключа сертификата подписи (например, B2C_1A_SAMLSigningCert).

### <a name="upload-hello-extension-file-for-verification"></a>Отправить файл hello расширения для проверки

Политика настроена, чтобы Azure AD B2C известно как toocommunicate с Salesforce. Попробуйте отправить файл hello расширения политики, tooverify, что в нем не все проблемы до сих. файл расширения hello tooupload политики:

1. В клиенте Azure AD B2C go toohello **все политики** колонку.
2. Выберите hello **перезаписать hello политики, если он существует** флажок.
3. Отправьте файл расширения hello (TrustFrameworkExtensions.xml). Убедитесь, что проверка пройдена.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Регистрация hello Salesforce SAML утверждения поставщика tooa пользователя пути

Затем добавьте hello tooone поставщика удостоверений Salesforce SAML для вашего пути пользователя. На этом этапе Настройка поставщика удостоверений hello, но он не доступен на всех страницах регистрации или входа пользователя hello. tooadd hello удостоверение поставщика tooa страницы входа, сначала необходимо создать копию существующего шаблона пути пользователя. Измените шаблон hello, придав ему hello поставщика удостоверений Azure AD.

1. Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).
2. Найти hello `<UserJourneys>` элемент, а затем hello Копировать всю `<UserJourney>` значений, включая идентификатор = «SignUpOrSignIn».
3. Откройте файл hello расширения (например, TrustFrameworkExtensions.xml). Найти hello `<UserJourneys>` элемента. Если элемент hello не существует, создайте его.
4. Вставить hello всего скопировать `<UserJourney>` как дочерний hello `<UserJourneys>` элемента.
5. Переименуйте идентификатор hello hello новый `<UserJourney>` (например, SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>Кнопку поставщика удостоверений hello отображения

Hello `<ClaimsProviderSelection>` элемент является аналогом tooan кнопку поставщика удостоверений на странице регистрации или входа. Добавив `<ClaimsProviderSelection>` элемент для Salesforce новая кнопка отображается при посещении toothis страницы. Кнопка поставщика удостоверений hello toodisplay:

1. В hello `<UserJourney>` , созданный, найти hello `<OrchestrationStep>` с `Order="1"`.
2. Добавьте следующий XML-код hello:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. Задать `TargetClaimsExchangeId` tooa логическое значение. Мы рекомендуем следующие hello же соглашениями, что и другие (например,  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>Действие tooan кнопку поставщика удостоверений ссылки hello

Теперь, когда имеется кнопка поставщика удостоверений в месте, свяжите его tooan действие. В этом случае hello действии для Azure AD B2C toocommunicate с Salesforce tooreceive маркера SAML. Это можно сделать путем связывания hello технические профиля для вашего Salesforce SAML поставщика утверждений:

1. В hello `<UserJourney>` узел, найти hello `<OrchestrationStep>` с `Order="2"`.
2. Добавьте следующий XML-код hello:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. Обновление `Id` toohello одинаковое значение, которые использовали для `TargetClaimsExchangeId`.
4. Обновление `TechnicalProfileReferenceId` toohello `Id` hello технические профиля созданную ранее (например, ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Отправка файла обновленного расширения hello

Изменение файла hello расширения завершено. Сохраните и отправьте этот файл. Убедитесь, что все проверки пройдены успешно.

### <a name="update-hello-relying-party-file"></a>Обновить проверяющей стороной файл hello

Затем обновите hello проверяющей стороны (RP) файл, который инициирует hello пути пользователя, созданный вами:

1. Создайте копию SignUpOrSignIn.xml в рабочем каталоге. Затем переименуйте ее (например, SignUpOrSignInWithAAD.xml).
2. Привет открыть новый файл и обновление hello `PolicyId` для атрибута `<TrustFrameworkPolicy>` с уникальным значением. Это имя hello политики (например, SignUpOrSignInWithAAD).
3. Изменение hello `ReferenceId` атрибута в `<DefaultUserJourney>` toomatch hello `Id` из нового пользователя пути hello созданный вами (например, SignUpOrSignUsingContoso).
4. Сохранить изменения, а затем отправьте файл hello.

## <a name="test-and-troubleshoot"></a>Тестирование и устранение неполадок

пользовательские политики hello tootest, только что переданного, в hello портал Azure, перейдите в колонку toohello политики и нажмите кнопку **запустить сейчас**. В случае неудачи см. сведения в разделе [Устранение неполадок пользовательских политик](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Дальнейшие действия

Отправить отзыв слишком[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
