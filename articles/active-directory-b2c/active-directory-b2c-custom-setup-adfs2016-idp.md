---
title: "Azure Active Directory B2C. Добавление ADFS в качестве поставщика удостоверений SAML с помощью пользовательских политик"
description: "Как tooarticle по настройке служб федерации Active Directory 2016 с помощью протокола SAML и пользовательских политик"
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C. Добавление ADFS в качестве поставщика удостоверений SAML с помощью пользовательских политик

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

В этой статье показано, как tooenable вход для пользователей из учетной записи служб федерации Active Directory с помощью hello [настраиваемые политики](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Предварительные требования

Hello завершения шагов в hello [Приступая к работе с помощью настроенных политик](active-directory-b2c-get-started-custom.md) статьи.

А именно:

1.  Создание отношения доверия с проверяющей стороной ADFS.
2.  Добавление tooAzure сертификатов служб федерации Active Directory доверия с проверяющей стороной hello AD B2C.
3.  Добавление политики tooa поставщика утверждений.
4.  Регистрация учетной записи служб федерации Active Directory hello утверждений поставщика tooa пользователя пути.
5.  Отправка tooan политики hello Azure AD B2C клиента и его проверка.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate утверждениям доверия с проверяющей стороной

toouse служб федерации Active Directory как поставщик удостоверений в Azure Active Directory (Azure AD) B2C требуется toocreate ADFS доверия с проверяющей стороной и передайте в него hello нужные параметры.

tooadd новый доверяющей стороны отношение доверия, используя оснастку hello AD FS управления и вручную настроить параметры hello выполнять hello после процедуры на сервере федерации.

Членство в **Администраторы**, или в эквивалентной на локальном компьютере hello hello минимальные необходимые toocomplete этой процедуры. Подробные сведения об использовании соответствующих учетных записей hello и членстве в группах в [локальные и доменные группы по умолчанию](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  В диспетчере серверов щелкните **Средства**, а затем выберите **ADFS Management** (Управление ADFS).

2.  Выберите **Add Relying Party Trust** (Добавить отношение доверия с проверяющей стороной).
    ![Добавление отношения доверия проверяющей стороны](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  На hello **приветствия** выберите **утверждения в маркере безопасности** и нажмите кнопку **запустить**.
    ![На странице приветствия hello выберите утверждения в маркере безопасности](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  На hello **Выбор источника данных** щелкните **ввод данных о проверяющей стороне hello вручную**, а затем нажмите кнопку **Далее**.
    ![Ввод данных о проверяющей стороне hello](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  На hello **укажите отображаемое имя** введите имя в **отображаемое имя**в разделе **заметки** введите описание для этого доверия с проверяющей стороной и нажмите кнопку **Далее** .
    ![Указание отображаемого имени и примечаний](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  необязательный параметр. Если имеется необязательный токен сертификат шифрования, затем на hello **Настройка сертификата** щелкните **Обзор** toolocate файл сертификата и нажмите кнопку **Далее** .
    ![Настройка сертификата](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  На hello **настроить URL-адрес** страницу, выберите hello **включить поддержку протокола SAML 2.0 WebSSO hello** флажок. В разделе **URL-адрес службы единого входа SAML 2.0 проверяющей стороной**, введите URL конечной точки службы hello Security Assertion Markup Language (SAML) для этого доверия с проверяющей стороной и нажмите кнопку **Далее**.  Для hello **URL-адрес службы единого входа SAML 2.0 проверяющей стороной**, вставьте hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. Замените {tenant} на имя вашего клиента (например, contosob2c.onmicrosoft.com) и введите имя политики расширения (например, B2C_1A_TrustFrameworkExtensions) hello {политики}.
    > [!IMPORTANT]
    >Имя политики Hello — hello один наследника signup_or_signin политики, в данном случае это: `B2C_1A_TrustFrameworkExtensions`.
    >Например может быть hello URL-адрес: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![URL-адрес службы SAML 2.0 SSO проверяющей стороны](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. На hello **настроить идентификаторы** укажите hello же URL-адрес как hello предыдущего шага, щелкните **добавить** tooadd их toohello, а затем нажмите **Далее**.
    ![Идентификаторы отношений доверия проверяющей стороны](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  На hello **выберите политику управления доступом к** выберите политику и нажмите кнопку **Далее**.
    ![Выбор политики управления доступом](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  На hello **готов tooAdd доверия** страницы, проверьте параметры hello и нажмите кнопку **Далее** toosave сведения об отношениях доверия проверяющей стороны.
    ![Сохранение сведений об отношении доверия с проверяющей стороной](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  На hello **Готово** щелкните **закрыть**, это действие автоматически отображает hello **изменение правил для утверждений** диалоговое окно.
    ![Изменение правил утверждений](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Щелкните **Добавить правило**.  
      ![Добавление нового правила](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  В разделе **Claim rule template** (Шаблон правила утверждения) выберите **Send LDAP attributes as claims** (Отправка атрибутов LDAP как утверждений).
    ![Выбор шаблона правила "Отправка атрибутов LDAP как утверждений"](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Укажите **имя правила утверждения**. Для hello **хранилище атрибутов** выберите **выберите Active Directory** hello после утверждения, а затем нажмите кнопку **Готово** и **ОК**.
    ![Настройка свойств правила](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  В диспетчере сервера выберите **доверия с проверяющей стороной** выберите hello доверия с проверяющей стороной вы создали и нажмите кнопку **свойства**.
    ![Изменение свойств проверяющей стороны](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Один hello доверяющей стороны отношения доверия (B2C Демонстрация) свойства окну, нажмите кнопку **подписи** и нажмите кнопку **добавить**.  
    ![Настройка подписи](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  Добавьте сертификат подписи (CERT-файл без закрытого ключа).  
    ![Добавление сертификата подписи](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  На hello доверяющей стороны доверия (B2C Демонстрация) окно "Свойства" нажмите кнопку **Дополнительно** вкладку и измените hello **безопасного хэш-алгоритм** слишком**SHA-1**, нажмите кнопку **ОК**.  
    ![Набор безопасности tooSHA-алгоритм хеширования](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Добавить hello служб федерации Active Directory учетная запись приложения ключа tooAzure AD B2C
Федерации с учетными записями служб федерации Active Directory требуется секрет клиента tootrust служб федерации Active Directory учетная запись Azure AD B2C имени приложения hello. Необходимо toostore сертификат служб федерации Active Directory в клиенте Azure AD B2C. 

1.  Клиент Azure AD B2C tooyour перейдите и выберите **B2C параметры** > **Identity Framework качества**
2.  Выберите **ключей политики** ключей tooview hello, доступных в клиенте.
3.  Щелкните **+Добавить**.
4.  В пункте **Параметры** используйте вариант **Отправить**.
5.  Для параметра **Имя** используйте значение `ADFSSamlCert`.  
    префикс Hello `B2C_1A_` могут быть добавлены автоматически.
6.  При отправке файла hello ** выберите файл PFX-файл сертификата с закрытым ключом. Примечание: этот сертификат (hello закрытым ключом) должен быть hello один выдан, использующиеся для проверяющей стороны hello служб федерации Active Directory.
![Отправка ключа политики](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  Нажмите кнопку **Создать**
8.  Убедитесь, что вы создали ключ hello `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Добавление поставщика утверждений в политику расширения
Если требуется в toosign пользователей с помощью служб федерации Active Directory учетная запись необходима учетная запись служб федерации Active Directory toodefine как поставщик утверждений. Другими словами необходимо toospecify, Azure AD B2C взаимодействует с конечной точки. Конечная точка Hello предоставляет набор утверждений, которые используются в Azure AD B2C tooverify проверку определенного пользователя.

Определите ADFS в качестве поставщика утверждений, добавив узел `<ClaimsProvider>` в файл политики расширения.

1. Откройте файл политики для расширения hello (TrustFrameworkExtensions.xml) из рабочий каталог. Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.
2. Найти hello `<ClaimsProviders>` раздела
3. Добавьте следующий фрагмент XML в hello hello `ClaimsProviders` и замените `identityProvider` с DNS-сервера (произвольное значение, указывающее домен) и сохраните файл hello. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Регистрация поставщика утверждений tooSign для hello служб федерации Active Directory учетная запись вверх или вход в пути пользователя
На этом этапе hello поставщик удостоверений настроен.  Тем не менее не доступен в любом hello регистрации-повышение/вход экранов. Теперь необходим hello tooadd ADFS удостоверение учетной записи поставщика пользователь tooyour `SignUpOrSignIn` пути пользователя. toomake его доступным, мы создаем копию существующего шаблона пути пользователя.  Затем мы изменить его, включив в него поставщик идентификатора ADFS hello:
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Откройте файл базовый hello политики (например, TrustFrameworkBase.xml).
2.  Найти hello `<UserJourneys>` элемент и скопируйте hello всему содержимому `<UserJourneys>` узла.
3.  Откройте файл hello расширения (например, TrustFrameworkExtensions.xml) и найти hello `<UserJourneys>` элемента. Если элемент hello не существует, добавьте его.
4.  Вставьте hello всему содержимому `<UserJournesy>` узел, который вы скопировали как дочерний hello `<UserJourneys>` элемента.

### <a name="display-hello-button"></a>Отображение кнопки hello
Hello `<ClaimsProviderSelections>` элемент определяет список hello параметры выбора поставщика утверждений и их порядок.  `<ClaimsProviderSelection>`элемент является аналогом tooan кнопку поставщика удостоверений на странице регистрации-повышение/вход. При добавлении `<ClaimsProviderSelection>` элемент для учетной записи служб федерации Active Directory новая кнопка отображается, когда пользователь попадает на странице приветствия. tooadd этого элемента:

1.  Найти hello `<UserJourney>` узел, который содержит `Id="SignUpOrSignIn"` в пути пользователя hello, скопированный.
2.  Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`
3.  Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Действие tooan кнопки ссылки hello

Теперь, когда имеется кнопка на месте, необходимо toolink его tooan действие. Действие Hello в этом случае является для Azure AD B2C toocommunicate с tooreceive учетной записи служб федерации Active Directory маркер. Свяжите действие tooan кнопки hello, связывания hello технические профиля для поставщика утверждений служб федерации Active Directory учетной записи.

1.  Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.
2.  Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Убедитесь, hello `Id` имеет одинаковое значение, что и hello `TargetClaimsExchangeId` в предшествующих раздел hello.
> * Убедитесь, `TechnicalProfileReferenceId` задано toohello технические профиль, созданный ранее (Contoso-SAML2).

## <a name="upload-hello-policy-tooyour-tenant"></a>Отправка hello политики tooyour клиента
1.  В hello [портал Azure](https://portal.azure.com), для переключения в hello [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)и откройте hello **Azure AD B2C** колонку.
2.  Выберите **Инфраструктура процедур идентификации**.
3.  Откройте hello **все политики** колонку.
4.  Щелкните **Отправить политику**.
5.  Проверьте **перезаписать hello политики, если он существует** поле.
6.  **Отправка** TrustFrameworkExtensions.xml и убедитесь, что он не позволяет проверки hello

## <a name="test-hello-custom-policy-by-using-run-now"></a>Тестирование настраиваемой политики hello с использованием выполнить
1.  Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.
2.  Откройте **B2C_1A_signup_signin**, hello проверяющей стороны (RP) настраиваемой политики загруженный. Выберите **Запустить сейчас**.
3.  Необходимо будет toosign учетной записью служб федерации Active Directory.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[Необязательно] Регистрация служб федерации Active Directory hello учетной записи поставщика утверждений tooProfile редактирования пути пользователя
Вы можете поставщик удостоверений учетных записей служб федерации Active Directory hello tooadd также пользователя tooyour `ProfileEdit` пути пользователя. toomake доступно, мы повторяем hello последние два этапа:

### <a name="display-hello-button"></a>Отображение кнопки hello
1.  Откройте файл hello расширения политики (например, TrustFrameworkExtensions.xml).
2.  Найти hello `<UserJourney>` узел, который содержит `Id="ProfileEdit"` в пути пользователя hello, скопированный.
3.  Найдите hello `<OrchestrationStep>` узел, который включает в себя`Order="1"`
4.  Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Действие tooan кнопки ссылки hello
1.  Найти hello `<OrchestrationStep>` , включающего `Order="2"` в hello `<UserJourney>` узла.
2.  Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Тестирование настраиваемой политики профиля Редактирование hello с использованием выполнить
1.  Откройте **параметры Azure AD B2C** и перейти слишком**возможности платформы идентификации**.
2.  Откройте **B2C_1A_ProfileEdit**, hello проверяющей стороны (RP) настраиваемой политики загруженный. Выберите **Запустить сейчас**.
3.  Необходимо будет toosign учетной записью служб федерации Active Directory.

## <a name="download-hello-complete-policy-files"></a>Загрузка файлов политики завершения hello
Необязательно: Мы рекомендуем сборки с помощью файлы политики настраиваемый hello, Приступая к работе с пользовательских политик перемещайтесь по завершении сценария. [Файлы примеров политики, предназначенные только для справки](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
