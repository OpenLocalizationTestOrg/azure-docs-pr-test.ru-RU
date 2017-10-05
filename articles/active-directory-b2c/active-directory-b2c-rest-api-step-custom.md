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
ms.openlocfilehash: dc319c97e64e55861b84cc3943667418077a05d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-an-orchestration-step"></a><span data-ttu-id="0ede3-103">Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации</span><span class="sxs-lookup"><span data-stu-id="0ede3-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>

<span data-ttu-id="0ede3-104">Инфраструктура процедур идентификации, лежащая в основе Azure Active Directory B2C (Azure AD B2C), позволяет разработчикам служб удостоверений интегрировать взаимодействие с REST API в пути взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="0ede3-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="0ede3-105">В конце этого пошагового руководства вы сможете создать путь взаимодействия пользователя Azure AD B2C, который взаимодействует со службами RESTful.</span><span class="sxs-lookup"><span data-stu-id="0ede3-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="0ede3-106">Инфраструктура процедур идентификации отправляет и получает данные в утверждениях.</span><span class="sxs-lookup"><span data-stu-id="0ede3-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="0ede3-107">Обмен утверждениями REST API:</span><span class="sxs-lookup"><span data-stu-id="0ede3-107">The REST API claims exchange:</span></span>

- <span data-ttu-id="0ede3-108">может разрабатываться как этап оркестрации;</span><span class="sxs-lookup"><span data-stu-id="0ede3-108">Can be designed as an orchestration step.</span></span>
- <span data-ttu-id="0ede3-109">может вызывать внешнее действие,</span><span class="sxs-lookup"><span data-stu-id="0ede3-109">Can trigger an external action.</span></span> <span data-ttu-id="0ede3-110">например записывать событие во внешнюю базу данных;</span><span class="sxs-lookup"><span data-stu-id="0ede3-110">For instance, it can log an event in an external database.</span></span>
- <span data-ttu-id="0ede3-111">может использоваться, чтобы получить значение, а затем сохранить его в базе данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="0ede3-111">Can be used to fetch a value and then store it in the user database.</span></span>

<span data-ttu-id="0ede3-112">Полученные утверждения могут позже использоваться для изменения процедуры выполнения.</span><span class="sxs-lookup"><span data-stu-id="0ede3-112">You can use the received claims later to change the flow of execution.</span></span>

<span data-ttu-id="0ede3-113">Взаимодействие можно также реализовать как профиль проверки.</span><span class="sxs-lookup"><span data-stu-id="0ede3-113">You can also design the interaction as a validation profile.</span></span> <span data-ttu-id="0ede3-114">Дополнительные сведения см. в статье [Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0ede3-114">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>

<span data-ttu-id="0ede3-115">В сценарии (когда пользователь изменяет профиль) выполняются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0ede3-115">The scenario is that when a user performs a profile edit, we want to:</span></span>

1. <span data-ttu-id="0ede3-116">Поиск пользователя во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="0ede3-116">Look up the user in an external system.</span></span>
2. <span data-ttu-id="0ede3-117">Получение места регистрации пользователя.</span><span class="sxs-lookup"><span data-stu-id="0ede3-117">Get the city where that user is registered.</span></span>
3. <span data-ttu-id="0ede3-118">Возвращение этого атрибута как утверждения обратно в приложение.</span><span class="sxs-lookup"><span data-stu-id="0ede3-118">Return that attribute to the application as a claim.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ede3-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ede3-119">Prerequisites</span></span>

- <span data-ttu-id="0ede3-120">Клиент Azure AD B2C, необходимый для регистрации или входа с использованием локальной учетной записи, как описано в статье [Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0ede3-120">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="0ede3-121">Конечная точка REST API, с которой устанавливается взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="0ede3-121">A REST API endpoint to interact with.</span></span> <span data-ttu-id="0ede3-122">В этом пошаговом руководстве в качестве примера используется простой веб-перехватчик приложения-функции Azure.</span><span class="sxs-lookup"><span data-stu-id="0ede3-122">This walkthrough uses a simple Azure function app webhook as an example.</span></span>
- <span data-ttu-id="0ede3-123">*Мы рекомендуем* ознакомиться с [пошаговым руководством по использованию обмена утверждениями REST API как проверки](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="0ede3-123">*Recommended*: Complete the [REST API claims exchange walkthrough as a validation step](active-directory-b2c-rest-api-validation-custom.md).</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="0ede3-124">Шаг 1. Подготовка функции REST API</span><span class="sxs-lookup"><span data-stu-id="0ede3-124">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="0ede3-125">В рамках этой статьи настройка функций REST API не рассматривается.</span><span class="sxs-lookup"><span data-stu-id="0ede3-125">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="0ede3-126">[Функции Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) предоставляют отличный набор инструментов для создания служб RESTful в облаке.</span><span class="sxs-lookup"><span data-stu-id="0ede3-126">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="0ede3-127">Мы настроили функцию Azure, которая получает утверждение `email`, а затем возвращает утверждение `city` с присвоенным значением `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-127">We have set up an Azure function that receives a claim called `email`, and then returns the claim `city` with the assigned value of `Redmond`.</span></span> <span data-ttu-id="0ede3-128">Пример функции Azure можно найти на портале [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="0ede3-128">The sample Azure function is on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

<span data-ttu-id="0ede3-129">Утверждение `userMessage`, возвращенное функцией Azure, является необязательным в этом контексте и будет игнорироваться инфраструктурой процедур идентификации.</span><span class="sxs-lookup"><span data-stu-id="0ede3-129">The `userMessage` claim that the Azure function returns is optional in this context, and the IEF will ignore it.</span></span> <span data-ttu-id="0ede3-130">Потенциально его можно использовать в качестве сообщения, переданного приложению, а затем позже представленного пользователю.</span><span class="sxs-lookup"><span data-stu-id="0ede3-130">You can potentially use it as a message passed to the application and presented to the user later.</span></span>

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

<span data-ttu-id="0ede3-131">С помощью приложения-функции Azure можно легко получить URL-адрес функции, который включает идентификатор определенной функции.</span><span class="sxs-lookup"><span data-stu-id="0ede3-131">An Azure function app makes it easy to get the function URL, which includes the identifier of the specific function.</span></span> <span data-ttu-id="0ede3-132">В этом случае URL-адрес — https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span><span class="sxs-lookup"><span data-stu-id="0ede3-132">In this case, the URL is: https://wingtipb2cfuncs.azurewebsites.net/api/LookUpLoyaltyWebHook?code=MQuG7BIE3eXBaCZ/YCfY1SHabm55HEphpNLmh1OP3hdfHkvI2QwPrw==.</span></span> <span data-ttu-id="0ede3-133">Вы можете его использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="0ede3-133">You can use it for testing.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworextensionsxml-file"></a><span data-ttu-id="0ede3-134">Шаг 2. Настройка обмена утверждениями RESTful API как технического профиля в файле TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="0ede3-134">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworExtensions.xml file</span></span>

<span data-ttu-id="0ede3-135">Технический профиль представляет собой полную конфигурацию обмена, заданную с помощью службы RESTful.</span><span class="sxs-lookup"><span data-stu-id="0ede3-135">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="0ede3-136">Откройте файл TrustFrameworkExtensions.xml и добавьте следующий фрагмент XML-кода в элемент `<ClaimsProvider>`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-136">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProvider>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="0ede3-137">В следующем XML-коде поставщик RESTful `Version=1.0.0.0` описан как протокол.</span><span class="sxs-lookup"><span data-stu-id="0ede3-137">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="0ede3-138">Рассматривайте его как функцию, которая будет взаимодействовать с внешней службой.</span><span class="sxs-lookup"><span data-stu-id="0ede3-138">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

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

<span data-ttu-id="0ede3-139">Элемент `<InputClaims>` определяет утверждения, которые отправляются из инфраструктуры процедур идентификации в службу REST.</span><span class="sxs-lookup"><span data-stu-id="0ede3-139">The `<InputClaims>` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="0ede3-140">В этом примере содержимое утверждения `givenName` отправляется в службу REST как утверждение `email`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-140">In this example, the contents of the claim `givenName` will be sent to the REST service as the claim `email`.</span></span>  

<span data-ttu-id="0ede3-141">Элемент `<OutputClaims>` определяет утверждения, которые инфраструктура процедур идентификации ожидает получить из службы REST.</span><span class="sxs-lookup"><span data-stu-id="0ede3-141">The `<OutputClaims>` element defines the claims that the IEF will expect from the REST service.</span></span> <span data-ttu-id="0ede3-142">Несмотря на количество полученных утверждений, инфраструктура процедур идентификации будет использовать только те, которые указаны здесь.</span><span class="sxs-lookup"><span data-stu-id="0ede3-142">Regardless of the number of claims that are received, the IEF will use only those identified here.</span></span> <span data-ttu-id="0ede3-143">В этом примере утверждение, полученное как `city`, будет сопоставлено с утверждением инфраструктуры процедур идентификации `city`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-143">In this example, a claim received as `city` will be mapped to an IEF claim called `city`.</span></span>

## <a name="step-3-add-the-new-claim-city-to-the-schema-of-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="0ede3-144">Шаг 3. Добавление нового утверждения `city` в схему файла TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="0ede3-144">Step 3: Add the new claim `city` to the schema of your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="0ede3-145">Утверждение `city` еще нигде не определено в схеме.</span><span class="sxs-lookup"><span data-stu-id="0ede3-145">The claim `city` is not yet defined anywhere in our schema.</span></span> <span data-ttu-id="0ede3-146">Поэтому добавьте определение внутрь элемента `<BuildingBlocks>`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-146">So, add a definition inside the element `<BuildingBlocks>`.</span></span> <span data-ttu-id="0ede3-147">Этот элемент можно найти в начале файла TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="0ede3-147">You can find this element at the beginning of the TrustFrameworkExtensions.xml file.</span></span>

```XML
<BuildingBlocks>
    <!--The claimtype city must be added to the TrustFrameworkPolicy-->
    <!-- You can add new claims in the BASE file Section III, or in the extensions file-->
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

## <a name="step-4-include-the-rest-service-claims-exchange-as-an-orchestration-step-in-your-profile-edit-user-journey-in-trustframeworkextensionsxml"></a><span data-ttu-id="0ede3-148">Шаг 4. Включение обмена утверждениями службы REST как этап оркестрации в пути взаимодействия пользователя для изменения профиля в файле TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="0ede3-148">Step 4: Include the REST service claims exchange as an orchestration step in your profile edit user journey in TrustFrameworkExtensions.xml</span></span>

<span data-ttu-id="0ede3-149">Добавьте этап в путь взаимодействия пользователя для изменения профиля после аутентификации пользователя (этапы оркестрации 1–4 в приведенном ниже XML-коде) и предоставления обновленных сведений о профиле (шаг 5).</span><span class="sxs-lookup"><span data-stu-id="0ede3-149">Add a step to the profile edit user journey, after the user has been authenticated (orchestration steps 1-4 in the following XML) and the user has provided the updated profile information (step 5).</span></span>

> [!NOTE]
> <span data-ttu-id="0ede3-150">Вызов REST API может использоваться как этап оркестрации в разных ситуациях.</span><span class="sxs-lookup"><span data-stu-id="0ede3-150">There are many use cases where the REST API call can be used as an orchestration step.</span></span> <span data-ttu-id="0ede3-151">Как этап оркестрации он может использоваться в качестве обновления внешней системы после успешного выполнения пользователем задания, например первой регистрации или обновления профиля для синхронизации сведений.</span><span class="sxs-lookup"><span data-stu-id="0ede3-151">As an orchestration step, it can be used as an update to an external system after a user has successfully completed a task like first-time registration, or as a profile update to keep information synchronized.</span></span> <span data-ttu-id="0ede3-152">В этом случае вызов REST API используется для расширения сведений, предоставленных приложению после изменения профиля.</span><span class="sxs-lookup"><span data-stu-id="0ede3-152">In this case, it's used to augment the information provided to the application after the profile edit.</span></span>

<span data-ttu-id="0ede3-153">Скопируйте XML-код пути взаимодействия пользователя для изменения профиля из файла TrustFrameworkBase.xml в файл TrustFrameworkExtensions.xml внутри элемента `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-153">Copy the profile edit user journey XML code from the TrustFrameworkBase.xml file to your TrustFrameworkExtensions.xml file inside the `<UserJourneys>` element.</span></span> <span data-ttu-id="0ede3-154">А затем внесите необходимые изменения, описанные на шаге 6.</span><span class="sxs-lookup"><span data-stu-id="0ede3-154">Then make the modification under step 6.</span></span>

```XML
<OrchestrationStep Order="6" Type="ClaimsExchange">
    <ClaimsExchanges>
        <ClaimsExchange Id="GetLoyaltyData" TechnicalProfileReferenceId="AzureFunctions-LookUpLoyaltyWebHook" />
    </ClaimsExchanges>
</OrchestrationStep>
```

> [!IMPORTANT]
> <span data-ttu-id="0ede3-155">Если порядок не соответствует вашей версии, то вставьте этот код как этап перед типом `ClaimsExchange` `SendClaims`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-155">If the order does not match your version, make sure that you insert the code as the step before the `ClaimsExchange` type `SendClaims`.</span></span>

<span data-ttu-id="0ede3-156">Конечный XML-код пути взаимодействия пользователя должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0ede3-156">The final XML for the user journey should look like this:</span></span>

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
        <!-- Add a step 6 to the user journey before the JWT token is created-->
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

## <a name="step-5-add-the-claim-city-to-your-relying-party-policy-file-so-the-claim-is-sent-to-your-application"></a><span data-ttu-id="0ede3-157">Шаг 5. Добавление утверждения `city` в файл политики проверяющей стороны для отправки утверждения приложению</span><span class="sxs-lookup"><span data-stu-id="0ede3-157">Step 5: Add the claim `city` to your relying party policy file so the claim is sent to your application</span></span>

<span data-ttu-id="0ede3-158">Необходимо изменить файл проверяющей стороны ProfileEdit.xml, а также элемент `<TechnicalProfile Id="PolicyProfile">` для добавления `<OutputClaim ClaimTypeReferenceId="city" />`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-158">Edit your ProfileEdit.xml relying party (RP) file and modify the `<TechnicalProfile Id="PolicyProfile">` element to add the following: `<OutputClaim ClaimTypeReferenceId="city" />`.</span></span>

<span data-ttu-id="0ede3-159">После добавления нового утверждения технический профиль должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0ede3-159">After you add the new claim, the technical profile looks like this:</span></span>

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

## <a name="step-6-upload-your-changes-and-test"></a><span data-ttu-id="0ede3-160">Шаг 6. Передача изменений и проверка</span><span class="sxs-lookup"><span data-stu-id="0ede3-160">Step 6: Upload your changes and test</span></span>

<span data-ttu-id="0ede3-161">Перезапишите существующие версии политики.</span><span class="sxs-lookup"><span data-stu-id="0ede3-161">Overwrite the existing versions of the policy.</span></span>

1.  <span data-ttu-id="0ede3-162">(Необязательно) Прежде чем продолжить, сохраните существующую версию файла расширений (скачав ее).</span><span class="sxs-lookup"><span data-stu-id="0ede3-162">(Optional:) Save the existing version (by downloading) of your extensions file before you proceed.</span></span> <span data-ttu-id="0ede3-163">Чтобы не усложнять работу, не рекомендуется передавать несколько версий файла расширений.</span><span class="sxs-lookup"><span data-stu-id="0ede3-163">To keep the initial complexity low, we recommend that you do not upload multiple versions of the extensions file.</span></span>
2.  <span data-ttu-id="0ede3-164">(Необязательно) Переименуйте новую версию идентификатора политики для файла изменения политики, изменив `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-164">(Optional:) Rename the new version of the policy ID for the policy edit file by changing   `PolicyId="B2C_1A_TrustFrameworkProfileEdit"`.</span></span>
3.  <span data-ttu-id="0ede3-165">Передайте файл расширений.</span><span class="sxs-lookup"><span data-stu-id="0ede3-165">Upload the extensions file.</span></span>
4.  <span data-ttu-id="0ede3-166">Отправьте файл проверяющей стороны для изменения политики.</span><span class="sxs-lookup"><span data-stu-id="0ede3-166">Upload the policy edit RP file.</span></span>
5.  <span data-ttu-id="0ede3-167">Используйте параметр **Запустить сейчас**, чтобы проверить политику.</span><span class="sxs-lookup"><span data-stu-id="0ede3-167">Use **Run Now** to test the policy.</span></span> <span data-ttu-id="0ede3-168">Просмотрите маркер, возвращаемый инфраструктурой процедур идентификации в приложение.</span><span class="sxs-lookup"><span data-stu-id="0ede3-168">Review the token that the IEF returns to the application.</span></span>

<span data-ttu-id="0ede3-169">Если все установлено правильно, токен будет содержать новое утверждение `city` со значением `Redmond`.</span><span class="sxs-lookup"><span data-stu-id="0ede3-169">If everything is set up correctly, the token will include the new claim `city`, with the value `Redmond`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0ede3-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ede3-170">Next steps</span></span>

<span data-ttu-id="0ede3-171">[Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journeys as validation on user input](active-directory-b2c-rest-api-validation-custom.md) (Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных)</span><span class="sxs-lookup"><span data-stu-id="0ede3-171">[Use a REST API as a validation step](active-directory-b2c-rest-api-validation-custom.md)</span></span>

[<span data-ttu-id="0ede3-172">Azure Active Directory B2C. Создание и использование настраиваемых атрибутов в пользовательской политике изменения профиля</span><span class="sxs-lookup"><span data-stu-id="0ede3-172">Modify the profile edit to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)
