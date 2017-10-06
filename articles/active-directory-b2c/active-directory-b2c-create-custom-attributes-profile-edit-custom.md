---
title: "Azure Active Directory B2C: Добавить собственные политики toocustom атрибуты и использовать редактирования профиля | Документы Microsoft"
description: "Пошаговое руководство по использованию свойства расширения, настраиваемые атрибуты и включить их в пользовательском интерфейсе hello"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Azure Active Directory B2C. Создание и использование настраиваемых атрибутов в пользовательской политике изменения профиля

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

В этой статье создайте настраиваемый атрибут в вашем каталоге Azure AD B2C и использовать этот новый атрибут в качестве пользовательского утверждения в пути пользователя изменить профиль hello.

## <a name="prerequisites"></a>Предварительные требования

Hello завершения действия в статье hello [Приступая к работе с пользовательских политик](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Используйте настраиваемые атрибуты toocollect сведения о клиентах в Azure Active Directory B2C использование пользовательских политик
Каталог Azure Active Directory (Azure AD) B2C поставляется со встроенным набором атрибутов: Given Name, Surname, City, Postal Code, userPrincipalName и т. д.  Часто требуется toocreate собственные атрибуты.  Например:
* В приложении с клиентом требуются toopersist атрибут, например «LoyaltyNumber.»
* Поставщик удостоверений имеет уникальный идентификатор пользователя, который необходимо сохранить, например uniqueUserGUID.
* Пути пользовательского должен toopersist hello состояние пользователя, например «migrationStatus.»

С помощью Azure AD B2C можно расширить hello набор атрибутов, хранящихся на каждой учетной записи пользователя. Можно также чтение и запись данных атрибутов с помощью hello [API Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

Свойства расширения расширить схему hello hello пользовательских объектов в каталоге hello.  свойство расширения условия Hello, настраиваемых атрибутов и пользовательских утверждений см. toohello, же в контексте hello этой статьи и hello имя изменяется в зависимости от контекста hello (приложения, объект, политики).

Свойства расширения можно зарегистрировать только в объекте приложения, даже если они содержат данные для пользователя. Hello свойство вложенного toohello приложения. объект приложения Hello должен быть предоставленный доступ на запись tooregister свойства расширения. 100 свойства расширения (для всех типов и всех приложений) могут быть записаны tooany один объект. Свойства расширения добавляются toohello тип целевого каталога и сразу становится доступным в клиенте каталога Azure AD B2C hello.
При удалении приложения hello, эти свойства расширения, а также данные, содержащиеся в них для всех пользователей также удаляются. Если свойство расширения удаляется с hello приложения, оно будет удалено на hello целевые объекты каталога, а hello значения удалены.

Свойства расширения существуют только в контексте hello зарегистрированного приложения в клиенте hello. Идентификатор объекта Hello этого приложения должны быть включены в hello TechnicalProfile, использующих его.

>[!NOTE]
>каталог Azure AD B2C Hello обычно включает веб-приложения с именем `b2c-extensions-app`.  Это приложение главным образом используется hello b2c встроенных политик для пользовательских утверждений hello, созданные с помощью портала Azure hello.  С помощью этого расширения tooregister приложений для пользовательских политик b2c рекомендуется для опытных пользователей.  Инструкции, включаются в hello раздел следующие шаги в этой статье.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Создание нового toostore приложения hello расширение свойств

1. Откройте сеанс браузера и перейдите toohello [Azure портальных](https://portal.azure.com) и выполните вход с учетными данными администратора hello нужно tooconfigure каталоге B2C.
1. Нажмите кнопку **Azure Active Directory** hello меню навигации слева. Может потребоваться его, выбрав более служб toofind >.
1. Щелкните **Регистрация приложений** и выберите пункт **Регистрация нового приложения**.
1. Предоставляют следующие hello рекомендуется записей:
  * Укажите имя для веб-приложения hello: **WebApp-GraphAPI-DirectoryExtensions**
  * Тип приложения: веб-приложение или API.
  * URL-адрес входа: https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions.
1. Выберите "Создать". Успешное завершение отображается в hello **уведомления**
1. Выберите только что созданный hello веб-приложение: **WebApp-GraphAPI-DirectoryExtensions**
1. Выберите параметры: **Необходимые разрешения**
1. Выберите API: **Windows Active Directory**
1. Установите флажки в разделе "Разрешения приложения": **Чтение и запись данных каталога** и **Сохранение**
1. Выберите команду **Предоставить разрешения** и нажмите кнопку **Да**.
1. Буфер обмена tooyour скопировать и сохранить следующие идентификаторы из WebApp-GraphAPI-DirectoryExtensions hello > Параметры > Свойства >
*  **Идентификатор приложения**. Пример: `103ee0e6-f92d-4183-b576-8c3739027780`
* **Идентификатор объекта**. Пример: `80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Изменение вашей настраиваемой политики tooadd hello ApplicationObjectId

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
>Hello <TechnicalProfile Id="AAD-Common"> является ссылка tooas «Общие», поскольку его элементы включаются в и повторно использовать в все hello Azure Active Directory TechnicalProfiles при помощи элемента hello:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>При hello TechnicalProfile записывает для первого свойства в расширение времени toohello только что созданный hello, могут возникнуть одноразовый ошибки.  свойства расширения Hello создается hello первый раз, в которой он используется.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>С помощью нового свойства расширения hello / настраиваемый атрибут в пути пользователя


1. Откройте hello проверяющей Party(RP) файл, который описывает политикой изменение пути пользователя.  При запуске, возможно, рекомендуется toodownload, уже настроенные версии hello RP PolicyEdit файл непосредственно из hello Azure B2C настраиваемой политики раздела hello портал Azure.  Вы также можете открыть XML-файл из папки хранилища.
2. Добавьте пользовательское утверждение `loyaltyId`.  Включая hello пользовательских утверждений в hello `<RelyingParty>` элемент, он передается в качестве параметра toohello UserJourney TechnicalProfiles и состава hello маркер для приложения hello.
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. Добавьте файл расширения политики утверждений определения toohello `TrustFrameworkExtensions.xml` внутри hello `<ClaimsSchema>` элемента, как показано.
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. Добавить hello же утверждения политики базовый файл определения toohello `TrustFrameworkBase.xml`.  
>Добавление `ClaimType` определение в hello base и hello расширения файла не обычно требуется, однако поскольку hello дальнейшие действия добавит hello extension_loyaltyId tooTechnicalProfiles в базовом файле hello, проверяющий элемент управления политики hello отклонит передачи hello hello основного файла без него.
>Может оказаться полезным tootrace выполнение hello hello пути пользователя, с именем «ProfileEdit» в файле TrustFrameworkBase.xml hello.  Поиск пользователя позволят hello hello таким же именем в редакторе и обратите внимание, что шаг 5 Orchestration вызывает hello TechnicalProfileReferenceID = «SelfAsserted ProfileUpdate».  Поиск и проверить этот toofamiliarize TechnicalProfile самостоятельно с потоком hello.
5. Добавить loyaltyId как входной и выходной утверждений в hello TechnicalProfile «SelfAsserted ProfileUpdate»
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. Добавление утверждения в TechnicalProfile «AAD UserWriteProfileUsingObjectId» toopersist hello значение утверждения hello в свойство расширения hello, для hello текущего пользователя в каталоге hello.
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. Добавление утверждения в TechnicalProfile «AAD UserReadUsingObjectId» tooread hello значение атрибута расширения hello, каждый раз, когда пользователь входит в. До сих hello TechnicalProfiles были изменены в потоке hello локальных учетных записей.  При желании hello новый атрибут потока hello социального/федеративной учетной записи другой набор TechnicalProfiles должен toobe изменен. Ознакомьтесь с разделом "Дальнейшие действия".

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
>элемент IncludeTechnicalProfile Hello добавляет все элементы hello общие AAD toothis TechnicalProfile.

## <a name="test-hello-custom-policy-using-run-now"></a>Тестирование настраиваемой политики hello, с помощью «Немедленном запуске»
1. Откройте hello **колонке Azure AD B2C** и перейдите в слишком**Identity Framework качества > пользовательских политик**.
1. Выберите настраиваемую политику hello, загруженный и нажмите кнопку hello **запустить сейчас** кнопки.
1. Должно быть toosign доступ с помощью адреса электронной почты.

маркер идентификатора Hello отправлено обратно tooyour приложение включает hello нового свойства расширения как предшествует extension_loyaltyId пользовательского утверждения. Ознакомьтесь с примером ниже.

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Дальнейшие действия

Добавьте новые потоки toohello утверждения hello для социальных сетей учетных записей входа, изменив приветствия TechnicalProfiles в списке. Эти два TechnicalProfiles используются с toowrite входа социального/федеративной учетной записи и чтения hello пользовательских данных с помощью hello alternativeSecurityId как hello локатора hello объекта пользователя.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

С помощью hello одинаковые атрибуты расширения между встроенные и пользовательские политики.
При добавлении атрибутов расширения (также называемого настраиваемые атрибуты) через взаимодействие с порталом hello те атрибуты, регистрируются с использованием hello ** b2c-расширений приложение, которое существует в каждый клиент b2c.  toouse эти атрибуты расширения в пользовательскую политику:
1. К клиенту b2c portal.azure.com, переход в слишком**Azure Active Directory** и выберите **регистрации приложения**
2. Найдите свое приложение **b2c-extensions-app** и выберите его.
3. В разделе «Основы» hello записи **идентификатор приложения** и hello **идентификатор объекта**
4. Добавьте их в метаданные технического профиля AAD-Common следующим образом:

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

tookeep согласованности hello портала процесс, создайте эти атрибуты с помощью портала hello пользовательского интерфейса *перед* использовать их в пользовательских политик.  При создании атрибута «ActivationStatus» на портале hello, должны ссылаться tooit следующим образом:

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>Справочные материалы

* Объект **технические профиля (TP)** — это тип элемента, можно рассматривать как *функция* , определяющий имя конечной точки, ее метаданные, его протокол и сведения hello exchange утверждений, которые hello удостоверений Взаимодействие с Framework должна быть выполнена.  Если это *функция* вызывается orchestration шаг или из другой TechnicalProfile, hello InputClaims и OutputClaims предоставляются как параметры hello вызывающим объектом.


* Полный список свойств расширений в статье hello [расширения СХЕМЫ КАТАЛОГОВ | ОСНОВНЫЕ ПОНЯТИЯ API GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Расширения атрибутов в Graph API именуются с использованием соглашения о hello `extension_ApplicationObjectID_attributename`. Настраиваемые политики называем атрибуты tooextensions extension_attributename, тем самым исключая hello ApplicationObjectId в hello XML
