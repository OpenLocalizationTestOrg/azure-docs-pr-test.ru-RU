---
title: "Azure Active Directory B2C. Обмен утверждениями REST API как метод проверки | Документация Майкрософт"
description: "В этой статье описываются пользовательские политики Azure Active Directory B2C"
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
ms.openlocfilehash: eb44a0d2234c9ee3801d8b3a1655d877aa2f4fef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="013eb-103">Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных</span><span class="sxs-lookup"><span data-stu-id="013eb-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="013eb-104">Инфраструктура процедур идентификации, лежащая в основе Azure Active Directory B2C (Azure AD B2C), позволяет разработчикам служб удостоверений интегрировать взаимодействие с REST API в пути взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="013eb-104">The Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables the identity developer to integrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="013eb-105">В конце этого пошагового руководства вы сможете создать путь взаимодействия пользователя Azure AD B2C, который взаимодействует со службами RESTful.</span><span class="sxs-lookup"><span data-stu-id="013eb-105">At the end of this walkthrough, you will be able to create an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="013eb-106">Инфраструктура процедур идентификации отправляет и получает данные в утверждениях.</span><span class="sxs-lookup"><span data-stu-id="013eb-106">The IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="013eb-107">Взаимодействие с API:</span><span class="sxs-lookup"><span data-stu-id="013eb-107">The interaction with the API:</span></span>

- <span data-ttu-id="013eb-108">можно реализовать как обмен утверждениями REST API или профиль проверки, выполняемой на этапе оркестрации;</span><span class="sxs-lookup"><span data-stu-id="013eb-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="013eb-109">обычно проверяет входные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="013eb-109">Typically validates input from the user.</span></span> <span data-ttu-id="013eb-110">Если полученное значение отклоняется, то пользователь может повторно ввести допустимое значение с возможностью возвращения сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="013eb-110">If the value from the user is rejected, the user can try again to enter a valid value with the opportunity to return an error message.</span></span>

<span data-ttu-id="013eb-111">Взаимодействие можно также реализовать на этапе оркестрации.</span><span class="sxs-lookup"><span data-stu-id="013eb-111">You can also design the interaction as an orchestration step.</span></span> <span data-ttu-id="013eb-112">Дополнительные сведения см. в статье [Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="013eb-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="013eb-113">В качестве примера профиля проверки мы будем использовать путь взаимодействия пользователя для изменения профиля в файле начального пакета ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="013eb-113">For the validation profile example, we will use the profile edit user journey in the starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="013eb-114">Мы можем проверить, не входит ли имя, указанное пользователем в политике изменения профиля, в список исключений.</span><span class="sxs-lookup"><span data-stu-id="013eb-114">We can verify that the name provided by the user in the profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="013eb-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="013eb-115">Prerequisites</span></span>

- <span data-ttu-id="013eb-116">Клиент Azure AD B2C, необходимый для регистрации или входа с использованием локальной учетной записи, как описано в статье [Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="013eb-116">An Azure AD B2C tenant configured to complete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="013eb-117">Конечная точка REST API, с которой устанавливается взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="013eb-117">A REST API endpoint to interact with.</span></span> <span data-ttu-id="013eb-118">Для этого руководства мы настроили демонстрационный сайт [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/), используя службу REST API.</span><span class="sxs-lookup"><span data-stu-id="013eb-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-the-rest-api-function"></a><span data-ttu-id="013eb-119">Шаг 1. Подготовка функции REST API</span><span class="sxs-lookup"><span data-stu-id="013eb-119">Step 1: Prepare the REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="013eb-120">В рамках этой статьи настройка функций REST API не рассматривается.</span><span class="sxs-lookup"><span data-stu-id="013eb-120">Setup of REST API functions is outside the scope of this article.</span></span> <span data-ttu-id="013eb-121">[Функции Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) предоставляют отличный набор инструментов для создания служб RESTful в облаке.</span><span class="sxs-lookup"><span data-stu-id="013eb-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit to create RESTful services in the cloud.</span></span>

<span data-ttu-id="013eb-122">Мы создали функцию Azure, которая получает утверждение, ожидаемое как `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="013eb-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="013eb-123">Функция проверяет, существует ли это утверждение.</span><span class="sxs-lookup"><span data-stu-id="013eb-123">The function validates whether this claim exists.</span></span> <span data-ttu-id="013eb-124">Полный код функции Azure доступен на сайте [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="013eb-124">You can access the complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

```csharp
if (requestContentAsJObject.playerTag == null)
{
  return request.CreateResponse(HttpStatusCode.BadRequest);
}

var playerTag = ((string) requestContentAsJObject.playerTag).ToLower();

if (playerTag == "mcvinny" || playerTag == "msgates123" || playerTag == "revcottonmarcus")
{
  return request.CreateResponse<ResponseContent>(
    HttpStatusCode.Conflict,
    new ResponseContent
    {
      version = "1.0.0",
      status = (int) HttpStatusCode.Conflict,
      userMessage = $"The player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="013eb-125">Инфраструктура процедур идентификации ожидает, что функция Azure вернет утверждение `userMessage`.</span><span class="sxs-lookup"><span data-stu-id="013eb-125">The IEF expects the `userMessage` claim that the Azure function returns.</span></span> <span data-ttu-id="013eb-126">Это утверждение будет представлено пользователю в виде строки, если при проверке произойдет сбой, например при возвращении кода состояния 409 (конфликт) в примере выше.</span><span class="sxs-lookup"><span data-stu-id="013eb-126">This claim will be presented as a string to the user if the validation fails, such as when a 409 conflict status is returned in the preceding example.</span></span>

## <a name="step-2-configure-the-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="013eb-127">Шаг 2. Настройка обмена утверждениями RESTful API как технического профиля в файле TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="013eb-127">Step 2: Configure the RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="013eb-128">Технический профиль представляет собой полную конфигурацию обмена, заданную с помощью службы RESTful.</span><span class="sxs-lookup"><span data-stu-id="013eb-128">A technical profile is the full configuration of the exchange desired with the RESTful service.</span></span> <span data-ttu-id="013eb-129">Откройте файл TrustFrameworkExtensions.xml и добавьте следующий фрагмент XML-кода в элемент `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="013eb-129">Open the TrustFrameworkExtensions.xml file and add the following XML snippet inside the `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="013eb-130">В следующем XML-коде поставщик RESTful `Version=1.0.0.0` описан как протокол.</span><span class="sxs-lookup"><span data-stu-id="013eb-130">In the following XML, RESTful provider `Version=1.0.0.0` is described as the protocol.</span></span> <span data-ttu-id="013eb-131">Рассматривайте его как функцию, которая будет взаимодействовать с внешней службой.</span><span class="sxs-lookup"><span data-stu-id="013eb-131">Consider it as the function that will interact with the external service.</span></span> <!-- TODO: A full definition of the schema can be found...link to RESTful Provider schema definition>-->

```xml
<ClaimsProvider>
    <DisplayName>REST APIs</DisplayName>
    <TechnicalProfiles>
        <TechnicalProfile Id="AzureFunctions-CheckPlayerTagWebHook">
            <DisplayName>Check Player Tag Web Hook Azure Function</DisplayName>
            <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.RestfulProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
            <Metadata>
                <Item Key="ServiceUrl">https://wingtipb2cfuncs.azurewebsites.net/api/CheckPlayerTagWebHook?code=L/05YRSpojU0nECzM4Tp3LjBiA2ZGh3kTwwp1OVV7m0SelnvlRVLCg==</Item>
                <Item Key="AuthenticationType">None</Item>
                <Item Key="SendClaimsIn">Body</Item>
            </Metadata>
            <InputClaims>
                <InputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="playerTag" />
            </InputClaims>
            <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
        </TechnicalProfile>
        <TechnicalProfile Id="SelfAsserted-ProfileUpdate">
            <ValidationTechnicalProfiles>
                <ValidationTechnicalProfile ReferenceId="AzureFunctions-CheckPlayerTagWebHook" />
            </ValidationTechnicalProfiles>
        </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

<span data-ttu-id="013eb-132">Элемент `InputClaims` определяет утверждения, которые отправляются из инфраструктуры процедур идентификации в службу REST.</span><span class="sxs-lookup"><span data-stu-id="013eb-132">The `InputClaims` element defines the claims that will be sent from the IEF to the REST service.</span></span> <span data-ttu-id="013eb-133">В этом примере содержимое утверждения `givenName` отправляется в службу REST как `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="013eb-133">In this example, the contents of the claim `givenName` will be sent to the REST service as `playerTag`.</span></span> <span data-ttu-id="013eb-134">В этом примере инфраструктура процедур идентификации не ожидает возврата утверждений.</span><span class="sxs-lookup"><span data-stu-id="013eb-134">In this example, the IEF does not expect claims back.</span></span> <span data-ttu-id="013eb-135">Вместо этого она ожидает ответ от службы REST и действует на основе полученного кода состояния.</span><span class="sxs-lookup"><span data-stu-id="013eb-135">Instead, it waits for a response from the REST service and acts based on the status codes that it receives.</span></span>

## <a name="step-3-include-the-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-to-validate-the-user-input"></a><span data-ttu-id="013eb-136">Шаг 3. Включение обмена утверждениями службы REST в самоподтвержденном техническом профиле, в котором необходимо реализовать проверку входных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="013eb-136">Step 3: Include the RESTful service claims exchange in self-asserted technical profile where you want to validate the user input</span></span>

<span data-ttu-id="013eb-137">Чаще всего этап проверки используется при взаимодействии с пользователем.</span><span class="sxs-lookup"><span data-stu-id="013eb-137">The most common use of the validation step is in the interaction with a user.</span></span> <span data-ttu-id="013eb-138">Все взаимодействия, где пользователь должен предоставить входные данные, выполняются с использованием *самоподтвержденных технических профилей*.</span><span class="sxs-lookup"><span data-stu-id="013eb-138">All interactions where the user is expected to provide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="013eb-139">В этом примере мы добавим этап проверки в технический профиль Self-Asserted-ProfileUpdate.</span><span class="sxs-lookup"><span data-stu-id="013eb-139">For this example, we will add the validation to the Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="013eb-140">Это технический профиль, используемый файлом политики проверяющей стороны `Profile Edit`.</span><span class="sxs-lookup"><span data-stu-id="013eb-140">This is the technical profile that the relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="013eb-141">Чтобы добавить обмен утверждениями в самоподтвержденный технический профиль, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="013eb-141">To add the claims exchange to the self-asserted technical profile:</span></span>

1. <span data-ttu-id="013eb-142">Откройте файл TrustFrameworkBase.xml и найдите `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="013eb-142">Open the TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="013eb-143">Проверьте конфигурацию этого технического профиля.</span><span class="sxs-lookup"><span data-stu-id="013eb-143">Review the configuration of this technical profile.</span></span> <span data-ttu-id="013eb-144">Просмотрите, как определен обмен утверждениями, запрашивающими данные пользователя (входящие утверждения), и утверждениями, возвращаемыми самоподтвержденным поставщиком (исходящие утверждения).</span><span class="sxs-lookup"><span data-stu-id="013eb-144">Observe how the exchange with the user is defined as claims that will be asked of the user (input claims) and claims that will be expected back from the self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="013eb-145">Найдите `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Обратите внимание, что этот профиль вызывается как этап оркестрации 6 `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="013eb-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-the-profile-edit-rp-policy-file"></a><span data-ttu-id="013eb-146">Шаг 4. Отправка и тестирование файла политики изменения профиля проверяющей стороны</span><span class="sxs-lookup"><span data-stu-id="013eb-146">Step 4: Upload and test the profile edit RP policy file</span></span>

1. <span data-ttu-id="013eb-147">Отправьте новую версию файла TrustFrameworkExtensions.xml.</span><span class="sxs-lookup"><span data-stu-id="013eb-147">Upload the new version of the TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="013eb-148">Проверьте файл политики изменения профиля проверяющей стороны с помощью кнопки **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="013eb-148">Use **Run now** to test the profile edit RP policy file.</span></span>
3. <span data-ttu-id="013eb-149">Выполните проверку, указав одно из имеющихся имен (например, mcvinny) в поле **Заданное имя**.</span><span class="sxs-lookup"><span data-stu-id="013eb-149">Test the validation by providing one of the existing names (for example, mcvinny) in the **Given Name** field.</span></span> <span data-ttu-id="013eb-150">Если все настроено правильно, то должно отобразиться сообщение, указывающее, что playerTag уже используется.</span><span class="sxs-lookup"><span data-stu-id="013eb-150">If everything is set up correctly, you should receive a message that notifies the user that the player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="013eb-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="013eb-151">Next steps</span></span>

[<span data-ttu-id="013eb-152">Azure Active Directory B2C. Создание и использование настраиваемых атрибутов в пользовательской политике изменения профиля</span><span class="sxs-lookup"><span data-stu-id="013eb-152">Modify the profile edit and user registration to gather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="013eb-153">Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации</span><span class="sxs-lookup"><span data-stu-id="013eb-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
