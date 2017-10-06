---
title: "Azure Active Directory B2C. Обмен утверждениями REST API как этап оркестрации | Документация Майкрософт"
description: "В этой статье описывается интеграция пользовательских политик Azure Active Directory B2C с API."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/24/2017
ms.author: joroja
ms.openlocfilehash: 90a495029f48d70232ef3f99de4ea4d351395aa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a>Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации

Hello удостоверения качества Framework (IEF), лежащей в основе Azure Active Directory B2C (Azure AD B2C) позволяет hello удостоверение разработчика toointegrate взаимодействия с API REST в пути пользователя.  

В конце этого пошагового руководства hello будет может toocreate путешествия пользователя Azure AD B2C взаимодействует с службы RESTful.

Hello IEF отправляет данные в утверждениях и получает данные обратно в заявках. Hello exchange утверждений REST API:

- может разрабатываться как этап оркестрации;
- может вызывать внешнее действие, например записывать событие во внешнюю базу данных;
- Можно использовать toofetch значение и затем сохранить ее в базе данных пользователей hello.

Можно использовать утверждения hello получено более поздней версии toochange hello хода выполнения.

Можно также создать hello взаимодействия как профиль проверки. Дополнительные сведения см. в статье [Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных](active-directory-b2c-rest-api-validation-custom.md).

Hello случае, когда пользователь выполняет изменить профиль, необходимо:

1. Поиск пользователя hello во внешней системе.
2. Получите Город hello, где зарегистрирован этот пользователь.
3. Возвращает атрибут toohello приложения в утверждения.

## <a name="prerequisites"></a>Предварительные требования

- Toocomplete клиента Azure AD B2C локальную учетную запись регистрации-повышение/вход, как описано в [Приступая к работе](active-directory-b2c-get-started-custom.md).
- Toointeract конечной точки REST API с. В этом пошаговом руководстве в качестве примера используется простой веб-перехватчик приложения-функции Azure.
- *Рекомендуется*: полный hello [API-интерфейса REST утверждений Пошаговое руководство exchange в качестве этапа проверки](active-directory-b2c-rest-api-validation-custom.md).

## <a name="step-1-prepare-hello-rest-api-function"></a>Шаг 1: Подготовка функции API-интерфейса REST hello

> [!NOTE]
> Настройка функций API-интерфейса REST находится за пределами hello рамки этой статьи. [Функции Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) обеспечивает лучший набор средств служб RESTful toocreate в облаке hello.

Мы настроили функцию Azure, которая получает заявку под названием `email`, и затем возвращает hello утверждения `city` со значением hello назначенный `Redmond`. Образец Hello Azure функция находится на [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

Hello `userMessage` утверждения с hello Azure функция возвращает является необязательным в этом контексте и hello IEF пропустит этот файл. Вы потенциально можно использовать как сообщение передается toohello приложения и описанных ниже toohello пользователя.

```csharp
if (requestContentAsJObject.email == null)
{
    return request.CreateResponse(HttpStatusCode.BadRequest);
}

var email = ((string) requestContentAsJObject.email).ToLower();

return request.CreateResponse<ResponseContent>(
    HttpStatusCode.OK,
    new ResponseContent
    {
        version = "1.0.0",
        status = (int) HttpStatusCode.OK,
        userMessage = "User Found",
        city = "Redmond"
    },
    new JsonMediaTypeFormatter(),
    "application/json");
```

Приложение Azure функция позволяет легко tooget hello функция URL-адрес, который включает идентификатор hello определенной функции hello. В этом случае является hello URL-адрес: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==. Вы можете его использовать для тестирования.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a>Шаг 2: Настройка exchange утверждений RESTful API hello как технические профиля в файле TrustFrameworExtensions.xml

Технические профиль является полной конфигурации hello обмена hello требуемого с hello службы RESTful. Откройте файл TrustFrameworkExtensions.xml hello и добавьте следующий фрагмент XML внутри hello hello `<ClaimsProvider>` элемента.

> [!NOTE]
> В следующий XML-код, RESTful поставщика hello `Version=1.0.0.0` говорится, что протокол hello. Рассматривайте его как hello функцию, которая будет взаимодействовать с внешней службы hello. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

```XML
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-LookUpLoyaltyWebHook">
            <DisplayName>Check LookUpLoyalty Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="email" />
            </InputClaims>
            <OutputClaims>
                <OutputClaim ClaimTypeReferenceId="city" PartnerClaimType="city" />
            </OutputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

Hello `<InputClaims>` элемент определяет hello утверждений, которые будут отправляться от службы REST toohello IEF hello. В этом примере hello содержимое утверждения hello `givenName` будут отправляться как hello утверждения службы REST toohello `email`.  

Hello `<OutputClaims>` элемент определяет hello утверждений, hello IEF будет ожидать от службы REST hello. Независимо от числа утверждения, полученные hello hello IEF будет использовать только те, которые определены здесь. В этом примере полученные утверждения в качестве `city` сопоставленных tooan IEF утверждения будет вызван `city`.

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a>Шаг 3: Добавление нового утверждения hello `city` toohello схемы файла TrustFrameworkExtensions.xml

Утверждение Hello `city` еще не определен в любом месте в нашем схемы. Таким образом, добавьте определение внутри элемента hello `<BuildingBlocks>`. Можно найти этот элемент в начале файла TrustFrameworkExtensions.xml hello hello.

```XML
<BuildingBlocks>
    <!--hello claimtype city must be added toohello TrustFrameworkPolicy-->
    <!-- You can add new claims in hello BASE file Section III, or in hello extensions file-->
    <ClaimsSchema>
        <ClaimType Id="city">
            <DisplayName>City</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your city</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
    </ClaimsSchema>
</BuildingBlocks>
```

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a>Шаг 4: Включать hello REST службы утверждения exchange в качестве шага orchestration в поездке пользователя изменить профиль в TrustFrameworkExtensions.xml

Добавьте шаг toohello профиль изменить пользователя пути после hello пользователя с проверкой подлинности (orchestration шагах 1-4 hello следующий XML-код) и hello пользователь предоставляет сведения о профиле hello обновлены (шаг 5).

> [!NOTE]
> Существует множество вариантов использования, где hello вызова интерфейса API REST можно использовать в качестве шага orchestration. В качестве шага orchestration его можно использовать в качестве внешней системы tooan обновление после успешного завершения задачи, такой как первой регистрации или как профиль обновления tookeep сведения, синхронизированные. В этом случае это используется tooaugment hello информация toohello приложения вместо изменения профиля hello.

Копировать профиль hello изменение пользователя пути XML-код из hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml файла внутри hello `<UserJourneys>` элемента. Внесите изменения hello в шаге 6.

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> Если порядок hello не соответствует версии, убедитесь, что вставке кода hello в качестве шага hello перед hello `ClaimsExchange` типа `SendClaims`.

Hello последний XML для hello пользователя пути должен выглядеть следующим образом:

```XML
<UserJourney Id="ProfileEdit">
    <OrchestrationSteps>
        <OrchestrationStep Order="1" Type="ClaimsProviderSelection" ContentDefinitionReferenceId="api.idpselections">
            <ClaimsProviderSelections>
                <ClaimsProviderSelection TargetClaimsExchangeId="FacebookExchange" />
                <ClaimsProviderSelection TargetClaimsExchangeId="LocalAccountSigninEmailExchange" />
            </ClaimsProviderSelections>
        </OrchestrationStep>
        <OrchestrationStep Order="2" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="FacebookExchange" TechnicalProfileReferenceId="Facebook-OAUTH" />
                <ClaimsExchange Id="LocalAccountSigninEmailExchange" TechnicalProfileReferenceId="SelfAsserted-LocalAccountSignin-Email" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="3" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>localAccountAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserRead" TechnicalProfileReferenceId="AAD-UserReadUsingAlternativeSecurityId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="4" Type="ClaimsExchange">
            <Preconditions>
                <Precondition Type="ClaimEquals" ExecuteActionsIf="true">
                    <Value>authenticationSource</Value>
                    <Value>socialIdpAuthentication</Value>
                    <Action>SkipThisOrchestrationStep</Action>
                </Precondition>
            </Preconditions>
            <ClaimsExchanges>
                <ClaimsExchange Id="AADUserReadWithObjectId" TechnicalProfileReferenceId="AAD-UserReadUsingObjectId" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="5" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="B2CUserProfileUpdateExchange" TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <!-- Add a step 6 toohello user journey before hello JWT token is created-->
        <OrchestrationStep Order="6" Type="ClaimsExchange">
            <ClaimsExchanges>
                <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
            </ClaimsExchanges>
        </OrchestrationStep>
        <OrchestrationStep Order="7" Type="SendClaims" CpimIssuerTechnicalProfileReferenceId="JwtIssuer" />
    </OrchestrationSteps>
    <ClientDefinition ReferenceId="DefaultWeb" />
</UserJourney>
```

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a>Шаг 5: Добавление утверждений hello `city` политики проверяющей стороной tooyour файл, hello утверждения отправляется tooyour приложения

Измените файл ProfileEdit.xml проверяющей стороны (RP) и измените hello `<TechnicalProfile Id="PolicyProfile">` hello следующий элемент tooadd: `<OutputClaim ClaimTypeReferenceId="city" />`.

После добавления нового утверждения hello технические профиля hello выглядит следующим образом:

```XML
<DisplayName>PolicyProfile</DisplayName>
    <Protocol Name="OpenIdConnect" />
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <SubjectNamingInfo ClaimType="sub" />
</TechnicalProfile>
```

## <a name="step-6-upload-your-changes-and-test"></a>Шаг 6. Передача изменений и проверка

Перезаписывать существующие версии hello hello политики.

1.  (Необязательно:) Сохраните существующую версию hello (загрузка) расширения файла перед продолжением работы. tookeep hello начальной сложности низкий, мы рекомендуем не отправлять несколько версий hello расширения файла.
2.  (Необязательно:) Переименуйте новую версию hello hello идентификатор политики для редактирования файла hello политику, изменив `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.
3.  Отправьте файл расширения hello.
4.  Отправьте файл RP редактирование политики hello.
5.  Используйте **выполнить** tootest hello политики. Маркер проверки hello, hello IEF возвращает toohello приложения.

Если все настроено правильно, hello маркер будет содержать новое утверждение hello `city`, со значением hello `Redmond`.

```JSON
{
  "exp": 1493053292,
  "nbf": 1493049692,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493049692,
  "auth_time": 1493049692,
  "city": "Redmond"
}
```

## <a name="next-steps"></a>Дальнейшие действия

[Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journeys as validation on user input](active-directory-b2c-rest-api-validation-custom.md) (Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных)

[Изменение hello редактирования toogather Дополнительные сведения о профиле от пользователей](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
