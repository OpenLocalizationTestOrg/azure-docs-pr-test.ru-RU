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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="b8b6d-103">Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации</span><span class="sxs-lookup"><span data-stu-id="b8b6d-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="b8b6d-104">Hello удостоверения качества Framework (IEF), лежащей в основе Azure Active Directory B2C (Azure AD B2C) позволяет hello удостоверение разработчика toointegrate взаимодействия с API REST в пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="b8b6d-105">В конце этого пошагового руководства hello будет может toocreate путешествия пользователя Azure AD B2C взаимодействует с службы RESTful.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="b8b6d-106">Hello IEF отправляет данные в утверждениях и получает данные обратно в заявках.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="b8b6d-107">Hello exchange утверждений REST API:</span><span class="sxs-lookup"><span data-stu-id="b8b6d-107">hello REST API claims exchange:</span></span>

- <span data-ttu-id="b8b6d-108">может разрабатываться как этап оркестрации;</span><span class="sxs-lookup"><span data-stu-id="b8b6d-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="b8b6d-109">может вызывать внешнее действие,</span><span class="sxs-lookup"><span data-stu-id="b8b6d-109">Can trigger an external action.</span></span> <span data-ttu-id="b8b6d-110">например записывать событие во внешнюю базу данных;</span><span class="sxs-lookup"><span data-stu-id="b8b6d-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="b8b6d-111">Можно использовать toofetch значение и затем сохранить ее в базе данных пользователей hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-111">Can be used toofetch a value and then store it in hello user database.</span></span>

<span data-ttu-id="b8b6d-112">Можно использовать утверждения hello получено более поздней версии toochange hello хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-112">You can use hello received claims later toochange hello flow of execution.</span></span>

<span data-ttu-id="b8b6d-113">Можно также создать hello взаимодействия как профиль проверки.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-113">You can also design hello interaction as a validation profile.</span></span> <span data-ttu-id="b8b6d-114">Дополнительные сведения см. в статье [Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b8b6d-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="b8b6d-115">Hello случае, когда пользователь выполняет изменить профиль, необходимо:</span><span class="sxs-lookup"><span data-stu-id="b8b6d-115">hello scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="b8b6d-116">Поиск пользователя hello во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-116">Look up hello user in an external system.</span></span>
2. <span data-ttu-id="b8b6d-117">Получите Город hello, где зарегистрирован этот пользователь.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-117">Get hello city where that user is registered.</span></span>
3. <span data-ttu-id="b8b6d-118">Возвращает атрибут toohello приложения в утверждения.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-118">Return that attribute toohello application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8b6d-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8b6d-119">Prerequisites</span></span>

- <span data-ttu-id="b8b6d-120">Toocomplete клиента Azure AD B2C локальную учетную запись регистрации-повышение/вход, как описано в [Приступая к работе](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b8b6d-120">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="b8b6d-121">Toointeract конечной точки REST API с.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-121">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="b8b6d-122">В этом пошаговом руководстве в качестве примера используется простой веб-перехватчик приложения-функции Azure.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="b8b6d-123">*Рекомендуется*: полный hello [API-интерфейса REST утверждений Пошаговое руководство exchange в качестве этапа проверки](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="b8b6d-123">*Recommended*: Complete hello [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="b8b6d-124">Шаг 1: Подготовка функции API-интерфейса REST hello</span><span class="sxs-lookup"><span data-stu-id="b8b6d-124">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="b8b6d-125">Настройка функций API-интерфейса REST находится за пределами hello рамки этой статьи.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-125">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="b8b6d-126">[Функции Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) обеспечивает лучший набор средств служб RESTful toocreate в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="b8b6d-127">Мы настроили функцию Azure, которая получает заявку под названием `email`, и затем возвращает hello утверждения `city` со значением hello назначенный `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-127">We have set up an Azure function that receives a claim called `email`, and then returns hello claim `city` with hello assigned value of `Redmond`.</span></span> <span data-ttu-id="b8b6d-128">Образец Hello Azure функция находится на [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="b8b6d-128">hello sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="b8b6d-129">Hello `userMessage` утверждения с hello Azure функция возвращает является необязательным в этом контексте и hello IEF пропустит этот файл.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-129">hello `userMessage` claim that hello Azure function returns is optional in this context, and hello IEF will ignore it.</span></span> <span data-ttu-id="b8b6d-130">Вы потенциально можно использовать как сообщение передается toohello приложения и описанных ниже toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-130">You can potentially use it as a message passed toohello application and presented toohello user later.</span></span>

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

<span data-ttu-id="b8b6d-131">Приложение Azure функция позволяет легко tooget hello функция URL-адрес, который включает идентификатор hello определенной функции hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-131">An Azure function app makes it easy tooget hello function URL, which includes hello identifier of hello specific function.</span></span> <span data-ttu-id="b8b6d-132">В этом случае является hello URL-адрес: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-132">In this case, hello URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="b8b6d-133">Вы можете его использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-133">You can use it for testing.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="b8b6d-134">Шаг 2: Настройка exchange утверждений RESTful API hello как технические профиля в файле TrustFrameworExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="b8b6d-134">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="b8b6d-135">Технические профиль является полной конфигурации hello обмена hello требуемого с hello службы RESTful.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-135">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="b8b6d-136">Откройте файл TrustFrameworkExtensions.xml hello и добавьте следующий фрагмент XML внутри hello hello `<ClaimsProvider>` элемента.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-136">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="b8b6d-137">В следующий XML-код, RESTful поставщика hello `Version=1.0.0.0` говорится, что протокол hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-137">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="b8b6d-138">Рассматривайте его как hello функцию, которая будет взаимодействовать с внешней службы hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-138">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="b8b6d-139">Hello `<InputClaims>` элемент определяет hello утверждений, которые будут отправляться от службы REST toohello IEF hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-139">hello `<InputClaims>` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="b8b6d-140">В этом примере hello содержимое утверждения hello `givenName` будут отправляться как hello утверждения службы REST toohello `email`.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-140">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as hello claim `email`.</span></span>  

<span data-ttu-id="b8b6d-141">Hello `<OutputClaims>` элемент определяет hello утверждений, hello IEF будет ожидать от службы REST hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-141">hello `<OutputClaims>` element defines hello claims that hello IEF will expect from hello REST service.</span></span> <span data-ttu-id="b8b6d-142">Независимо от числа утверждения, полученные hello hello IEF будет использовать только те, которые определены здесь.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-142">Regardless of hello number of claims that are received, hello IEF will use only those identified here.</span></span> <span data-ttu-id="b8b6d-143">В этом примере полученные утверждения в качестве `city` сопоставленных tooan IEF утверждения будет вызван `city`.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-143">In this example, a claim received as `city` will be mapped tooan IEF claim called `city`.</span></span>

## <a name="step-3-add-hello-new-claim-city-toohello-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="b8b6d-144">Шаг 3: Добавление нового утверждения hello `city` toohello схемы файла TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="b8b6d-144">Step 3: Add hello new claim `city` toohello schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="b8b6d-145">Утверждение Hello `city` еще не определен в любом месте в нашем схемы.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-145">hello claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="b8b6d-146">Таким образом, добавьте определение внутри элемента hello `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-146">So, add a definition inside hello element `<BuildingBlocks>`.</span></span> <span data-ttu-id="b8b6d-147">Можно найти этот элемент в начале файла TrustFrameworkExtensions.xml hello hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-147">You can find this element at hello beginning of hello TrustFrameworkExtensions.xml file.</span></span>

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

## <a name="step-4-include-hello-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="b8b6d-148">Шаг 4: Включать hello REST службы утверждения exchange в качестве шага orchestration в поездке пользователя изменить профиль в TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="b8b6d-148">Step 4: Include hello REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="b8b6d-149">Добавьте шаг toohello профиль изменить пользователя пути после hello пользователя с проверкой подлинности (orchestration шагах 1-4 hello следующий XML-код) и hello пользователь предоставляет сведения о профиле hello обновлены (шаг 5).</span><span class="sxs-lookup"><span data-stu-id="b8b6d-149">Add a step toohello profile edit user journey, after hello user has been authenticated (orchestration steps 1-4 in hello following XML) and hello user has provided hello updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="b8b6d-150">Существует множество вариантов использования, где hello вызова интерфейса API REST можно использовать в качестве шага orchestration.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-150">There are many use cases where hello REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="b8b6d-151">В качестве шага orchestration его можно использовать в качестве внешней системы tooan обновление после успешного завершения задачи, такой как первой регистрации или как профиль обновления tookeep сведения, синхронизированные.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-151">As an orchestration step, it can be used as an update tooan external system after a user has successfully completed a task like first-time registration, or as a profile update tookeep information synchronized.</span></span> <span data-ttu-id="b8b6d-152">В этом случае это используется tooaugment hello информация toohello приложения вместо изменения профиля hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-152">In this case, it's used tooaugment hello information provided toohello application after hello profile edit.</span></span>

<span data-ttu-id="b8b6d-153">Копировать профиль hello изменение пользователя пути XML-код из hello TrustFrameworkBase.xml tooyour TrustFrameworkExtensions.xml файла внутри hello `<UserJourneys>` элемента.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-153">Copy hello profile edit user journey XML code from hello TrustFrameworkBase.xml file tooyour TrustFrameworkExtensions.xml file inside hello `<UserJourneys>` element.</span></span> <span data-ttu-id="b8b6d-154">Внесите изменения hello в шаге 6.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-154">Then make hello modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="b8b6d-155">Если порядок hello не соответствует версии, убедитесь, что вставке кода hello в качестве шага hello перед hello `ClaimsExchange` типа `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-155">If hello order does not match your version, make sure that you insert hello code as hello step before hello `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="b8b6d-156">Hello последний XML для hello пользователя пути должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b8b6d-156">hello final XML for hello user journey should look like this:</span></span>

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

## <a name="step-5-add-hello-claim-city-tooyour-relying-party-policy-file-so-hello-claim-is-sent-tooyour-application"></a><span data-ttu-id="b8b6d-157">Шаг 5: Добавление утверждений hello `city` политики проверяющей стороной tooyour файл, hello утверждения отправляется tooyour приложения</span><span class="sxs-lookup"><span data-stu-id="b8b6d-157">Step 5: Add hello claim `city` tooyour relying party policy file so hello claim is sent tooyour application</span></span>

<span data-ttu-id="b8b6d-158">Измените файл ProfileEdit.xml проверяющей стороны (RP) и измените hello `<TechnicalProfile Id="PolicyProfile">` hello следующий элемент tooadd: `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-158">Edit your ProfileEdit.xml relying party (RP) file and modify hello `<TechnicalProfile Id="PolicyProfile">` element tooadd hello following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="b8b6d-159">После добавления нового утверждения hello технические профиля hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b8b6d-159">After you add hello new claim, hello technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="b8b6d-160">Шаг 6. Передача изменений и проверка</span><span class="sxs-lookup"><span data-stu-id="b8b6d-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="b8b6d-161">Перезаписывать существующие версии hello hello политики.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-161">Overwrite hello existing versions of hello policy.</span></span>

1.  <span data-ttu-id="b8b6d-162">(Необязательно:) Сохраните существующую версию hello (загрузка) расширения файла перед продолжением работы.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-162">(Optional:) Save hello existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="b8b6d-163">tookeep hello начальной сложности низкий, мы рекомендуем не отправлять несколько версий hello расширения файла.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-163">tookeep hello initial complexity low, we recommend that you do not upload multiple versions of hello extensions file.</span></span>
2.  <span data-ttu-id="b8b6d-164">(Необязательно:) Переименуйте новую версию hello hello идентификатор политики для редактирования файла hello политику, изменив `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-164">(Optional:) Rename hello new version of hello policy ID for hello policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="b8b6d-165">Отправьте файл расширения hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-165">Upload hello extensions file.</span></span>
4.  <span data-ttu-id="b8b6d-166">Отправьте файл RP редактирование политики hello.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-166">Upload hello policy edit RP file.</span></span>
5.  <span data-ttu-id="b8b6d-167">Используйте **выполнить** tootest hello политики.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-167">Use **Run Now** tootest hello policy.</span></span> <span data-ttu-id="b8b6d-168">Маркер проверки hello, hello IEF возвращает toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-168">Review hello token that hello IEF returns toohello application.</span></span>

<span data-ttu-id="b8b6d-169">Если все настроено правильно, hello маркер будет содержать новое утверждение hello `city`, со значением hello `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="b8b6d-169">If everything is set up correctly, hello token will include hello new claim `city`, with hello value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b8b6d-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8b6d-170">Next steps</span></span>

<span data-ttu-id="b8b6d-171">[Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journeys as validation on user input](active-directory-b2c-rest-api-validation-custom.md) (Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных)</span><span class="sxs-lookup"><span data-stu-id="b8b6d-171">[Use a REST API as a validation step](active-directory-b2c-rest-api-validation-custom.md)</span></span>

[<span data-ttu-id="b8b6d-172">Изменение hello редактирования toogather Дополнительные сведения о профиле от пользователей</span><span class="sxs-lookup"><span data-stu-id="b8b6d-172">Modify hello profile edit toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
