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
ms.openlocfilehash: cec6c6e110514a8bbe0e0780f36738ff21ae2f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a><span data-ttu-id="851d1-103">Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных</span><span class="sxs-lookup"><span data-stu-id="851d1-103">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as validation on user input</span></span>

<span data-ttu-id="851d1-104">Hello удостоверения качества Framework (IEF), лежащей в основе Azure Active Directory B2C (Azure AD B2C) позволяет hello удостоверение разработчика toointegrate взаимодействия с API REST в пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="851d1-104">hello Identity Experience Framework (IEF) that underlies Azure Active Directory B2C (Azure AD B2C) enables hello identity developer toointegrate an interaction with a RESTful API in a user journey.</span></span>  

<span data-ttu-id="851d1-105">В конце этого пошагового руководства hello будет может toocreate путешествия пользователя Azure AD B2C взаимодействует с службы RESTful.</span><span class="sxs-lookup"><span data-stu-id="851d1-105">At hello end of this walkthrough, you will be able toocreate an Azure AD B2C user journey that interacts with RESTful services.</span></span>

<span data-ttu-id="851d1-106">Hello IEF отправляет данные в утверждениях и получает данные обратно в заявках.</span><span class="sxs-lookup"><span data-stu-id="851d1-106">hello IEF sends data in claims and receives data back in claims.</span></span> <span data-ttu-id="851d1-107">Hello взаимодействий с hello API:</span><span class="sxs-lookup"><span data-stu-id="851d1-107">hello interaction with hello API:</span></span>

- <span data-ttu-id="851d1-108">можно реализовать как обмен утверждениями REST API или профиль проверки, выполняемой на этапе оркестрации;</span><span class="sxs-lookup"><span data-stu-id="851d1-108">Can be designed as a REST API claims exchange or as a validation profile, which happens inside an orchestration step.</span></span>
- <span data-ttu-id="851d1-109">Обычно проверяет входные данные от пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="851d1-109">Typically validates input from hello user.</span></span> <span data-ttu-id="851d1-110">Если значение hello от пользователя hello отклоняется, hello пользователя можно повторить попытку tooenter допустимое значение с возможностью hello tooreturn сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="851d1-110">If hello value from hello user is rejected, hello user can try again tooenter a valid value with hello opportunity tooreturn an error message.</span></span>

<span data-ttu-id="851d1-111">Можно также создать hello взаимодействия на этапе orchestration.</span><span class="sxs-lookup"><span data-stu-id="851d1-111">You can also design hello interaction as an orchestration step.</span></span> <span data-ttu-id="851d1-112">Дополнительные сведения см. в статье [Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="851d1-112">For more information, see [Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step](active-directory-b2c-rest-api-step-custom.md).</span></span>

<span data-ttu-id="851d1-113">Пример профиля проверки hello мы будем использовать пути пользователя изменить профиль hello в файл пакета начального приветствия ProfileEdit.xml.</span><span class="sxs-lookup"><span data-stu-id="851d1-113">For hello validation profile example, we will use hello profile edit user journey in hello starter pack file ProfileEdit.xml.</span></span>

<span data-ttu-id="851d1-114">Мы можно проверить это имя hello, предоставляемых пользователем hello в профиле hello редактирования не входит в список исключений.</span><span class="sxs-lookup"><span data-stu-id="851d1-114">We can verify that hello name provided by hello user in hello profile edit is not part of an exclusion list.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="851d1-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="851d1-115">Prerequisites</span></span>

- <span data-ttu-id="851d1-116">Toocomplete клиента Azure AD B2C локальную учетную запись регистрации-повышение/вход, как описано в [Приступая к работе](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="851d1-116">An Azure AD B2C tenant configured toocomplete a local account sign-up/sign-in, as described in [Getting started](active-directory-b2c-get-started-custom.md).</span></span>
- <span data-ttu-id="851d1-117">Toointeract конечной точки REST API с.</span><span class="sxs-lookup"><span data-stu-id="851d1-117">A REST API endpoint toointeract with.</span></span> <span data-ttu-id="851d1-118">Для этого руководства мы настроили демонстрационный сайт [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/), используя службу REST API.</span><span class="sxs-lookup"><span data-stu-id="851d1-118">For this walkthrough, we've set up a demo site called [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/) with a REST API service.</span></span>

## <a name="step-1-prepare-hello-rest-api-function"></a><span data-ttu-id="851d1-119">Шаг 1: Подготовка функции API-интерфейса REST hello</span><span class="sxs-lookup"><span data-stu-id="851d1-119">Step 1: Prepare hello REST API function</span></span>

> [!NOTE]
> <span data-ttu-id="851d1-120">Настройка функций API-интерфейса REST находится за пределами hello рамки этой статьи.</span><span class="sxs-lookup"><span data-stu-id="851d1-120">Setup of REST API functions is outside hello scope of this article.</span></span> <span data-ttu-id="851d1-121">[Функции Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) обеспечивает лучший набор средств служб RESTful toocreate в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="851d1-121">[Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-reference) provides an excellent toolkit toocreate RESTful services in hello cloud.</span></span>

<span data-ttu-id="851d1-122">Мы создали функцию Azure, которая получает утверждение, ожидаемое как `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="851d1-122">We have created an Azure function that receives a claim that it expects as `playerTag`.</span></span> <span data-ttu-id="851d1-123">функция Hello проверяет существование этого утверждения.</span><span class="sxs-lookup"><span data-stu-id="851d1-123">hello function validates whether this claim exists.</span></span> <span data-ttu-id="851d1-124">Можно получить доступ к код завершения Azure функции hello в [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span><span class="sxs-lookup"><span data-stu-id="851d1-124">You can access hello complete Azure function code in [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).</span></span>

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
      userMessage = $"hello player tag '{requestContentAsJObject.playerTag}' is already used."
    },
    new JsonMediaTypeFormatter(),
    "application/json");
}

return request.CreateResponse(HttpStatusCode.OK);
```

<span data-ttu-id="851d1-125">Hello IEF ожидает hello `userMessage` утверждения, hello Azure функция возвращает.</span><span class="sxs-lookup"><span data-stu-id="851d1-125">hello IEF expects hello `userMessage` claim that hello Azure function returns.</span></span> <span data-ttu-id="851d1-126">Это утверждение будет представлен как пользователь toohello строки при сбое проверки hello, например при возврате состояния 409 (конфликт) в предшествующих пример hello.</span><span class="sxs-lookup"><span data-stu-id="851d1-126">This claim will be presented as a string toohello user if hello validation fails, such as when a 409 conflict status is returned in hello preceding example.</span></span>

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a><span data-ttu-id="851d1-127">Шаг 2: Настройка exchange утверждений RESTful API hello как технические профиля в файле TrustFrameworkExtensions.xml</span><span class="sxs-lookup"><span data-stu-id="851d1-127">Step 2: Configure hello RESTful API claims exchange as a technical profile in your TrustFrameworkExtensions.xml file</span></span>

<span data-ttu-id="851d1-128">Технические профиль является полной конфигурации hello обмена hello требуемого с hello службы RESTful.</span><span class="sxs-lookup"><span data-stu-id="851d1-128">A technical profile is hello full configuration of hello exchange desired with hello RESTful service.</span></span> <span data-ttu-id="851d1-129">Откройте файл TrustFrameworkExtensions.xml hello и добавьте следующий фрагмент XML внутри hello hello `<ClaimsProviders>` элемента.</span><span class="sxs-lookup"><span data-stu-id="851d1-129">Open hello TrustFrameworkExtensions.xml file and add hello following XML snippet inside hello `<ClaimsProviders>` element.</span></span>

> [!NOTE]
> <span data-ttu-id="851d1-130">В следующий XML-код, RESTful поставщика hello `Version=1.0.0.0` говорится, что протокол hello.</span><span class="sxs-lookup"><span data-stu-id="851d1-130">In hello following XML, RESTful provider `Version=1.0.0.0` is described as hello protocol.</span></span> <span data-ttu-id="851d1-131">Рассматривайте его как hello функцию, которая будет взаимодействовать с внешней службы hello.</span><span class="sxs-lookup"><span data-stu-id="851d1-131">Consider it as hello function that will interact with hello external service.</span></span> <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

<span data-ttu-id="851d1-132">Hello `InputClaims` элемент определяет hello утверждений, которые будут отправляться от службы REST toohello IEF hello.</span><span class="sxs-lookup"><span data-stu-id="851d1-132">hello `InputClaims` element defines hello claims that will be sent from hello IEF toohello REST service.</span></span> <span data-ttu-id="851d1-133">В этом примере hello содержимое утверждения hello `givenName` будет отправлено службе REST toohello как `playerTag`.</span><span class="sxs-lookup"><span data-stu-id="851d1-133">In this example, hello contents of hello claim `givenName` will be sent toohello REST service as `playerTag`.</span></span> <span data-ttu-id="851d1-134">В этом примере hello IEF непредвиденным утверждений обратно.</span><span class="sxs-lookup"><span data-stu-id="851d1-134">In this example, hello IEF does not expect claims back.</span></span> <span data-ttu-id="851d1-135">Вместо этого он ожидает ответа от службы REST hello и действует на основании hello коды состояния, которые он получает.</span><span class="sxs-lookup"><span data-stu-id="851d1-135">Instead, it waits for a response from hello REST service and acts based on hello status codes that it receives.</span></span>

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a><span data-ttu-id="851d1-136">Шаг 3: Включите exchange утверждения службы RESTful hello в самозаверяемые технические профиля, где требуется ввод данных пользователем toovalidate hello</span><span class="sxs-lookup"><span data-stu-id="851d1-136">Step 3: Include hello RESTful service claims exchange in self-asserted technical profile where you want toovalidate hello user input</span></span>

<span data-ttu-id="851d1-137">Hello чаще всего этапа проверки hello используется hello взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="851d1-137">hello most common use of hello validation step is in hello interaction with a user.</span></span> <span data-ttu-id="851d1-138">Все диалоги, где пользователь hello является ожидаемым tooprovide ввода не *самим пользователем технические профилей*.</span><span class="sxs-lookup"><span data-stu-id="851d1-138">All interactions where hello user is expected tooprovide input are *self-asserted technical profiles*.</span></span> <span data-ttu-id="851d1-139">В этом примере мы добавим технические профиль toohello проверки частный Asserted ProfileUpdate hello.</span><span class="sxs-lookup"><span data-stu-id="851d1-139">For this example, we will add hello validation toohello Self-Asserted-ProfileUpdate technical profile.</span></span> <span data-ttu-id="851d1-140">Это профиль технические hello, hello файл политики проверяющей стороны (RP) `Profile Edit` использует.</span><span class="sxs-lookup"><span data-stu-id="851d1-140">This is hello technical profile that hello relying party (RP) policy file `Profile Edit` uses.</span></span>

<span data-ttu-id="851d1-141">tooadd hello утверждений exchange toohello самим пользователем технические профиля:</span><span class="sxs-lookup"><span data-stu-id="851d1-141">tooadd hello claims exchange toohello self-asserted technical profile:</span></span>

1. <span data-ttu-id="851d1-142">Откройте файл TrustFrameworkBase.xml hello и выполните поиск `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span><span class="sxs-lookup"><span data-stu-id="851d1-142">Open hello TrustFrameworkBase.xml file and search for `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.</span></span>
2. <span data-ttu-id="851d1-143">Проверьте конфигурацию hello технические профиля.</span><span class="sxs-lookup"><span data-stu-id="851d1-143">Review hello configuration of this technical profile.</span></span> <span data-ttu-id="851d1-144">Обратите внимание, как hello exchange с пользователем hello определяется как утверждения, задаваемые hello пользователя (входящих утверждений) и утверждения, которые будут являться назад от поставщика самозаверяемые hello (исходящие утверждения).</span><span class="sxs-lookup"><span data-stu-id="851d1-144">Observe how hello exchange with hello user is defined as claims that will be asked of hello user (input claims) and claims that will be expected back from hello self-asserted provider (output claims).</span></span>
3. <span data-ttu-id="851d1-145">Найдите `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Обратите внимание, что этот профиль вызывается как этап оркестрации 6 `<UserJourney Id="ProfileEdit">`.</span><span class="sxs-lookup"><span data-stu-id="851d1-145">Search for `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`, and notice that this profile is invoked as orchestration step 6 of `<UserJourney Id="ProfileEdit">`.</span></span>

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a><span data-ttu-id="851d1-146">Шаг 4: Отправка и тестирования файл политики RP редактирование профиля hello</span><span class="sxs-lookup"><span data-stu-id="851d1-146">Step 4: Upload and test hello profile edit RP policy file</span></span>

1. <span data-ttu-id="851d1-147">Отправьте новую версию файла TrustFrameworkExtensions.xml hello hello.</span><span class="sxs-lookup"><span data-stu-id="851d1-147">Upload hello new version of hello TrustFrameworkExtensions.xml file.</span></span>
2. <span data-ttu-id="851d1-148">Используйте **запустить сейчас** профиль hello tootest изменить файл политики RP.</span><span class="sxs-lookup"><span data-stu-id="851d1-148">Use **Run now** tootest hello profile edit RP policy file.</span></span>
3. <span data-ttu-id="851d1-149">Выполнение проверки hello одним из существующих имен hello (например, mcvinny) в hello **заданное имя** поля.</span><span class="sxs-lookup"><span data-stu-id="851d1-149">Test hello validation by providing one of hello existing names (for example, mcvinny) in hello **Given Name** field.</span></span> <span data-ttu-id="851d1-150">Если все настроено правильно, должно появиться сообщение, уведомляющее пользователя hello hello проигрывателя тег уже используется.</span><span class="sxs-lookup"><span data-stu-id="851d1-150">If everything is set up correctly, you should receive a message that notifies hello user that hello player tag is already used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="851d1-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="851d1-151">Next steps</span></span>

[<span data-ttu-id="851d1-152">Изменение hello профиля редактирования и пользователь toogather Дополнительные сведения о регистрации от пользователей</span><span class="sxs-lookup"><span data-stu-id="851d1-152">Modify hello profile edit and user registration toogather additional information from your users</span></span>](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[<span data-ttu-id="851d1-153">Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации</span><span class="sxs-lookup"><span data-stu-id="851d1-153">Walkthrough: Integrate REST API claims exchanges in your Azure AD B2C user journey as an orchestration step</span></span>](active-directory-b2c-rest-api-step-custom.md)
