---
title: "Tootroubleshoot аналитики приложений пользовательских политик - Azure AD B2C | Документы Microsoft"
description: "как tootrace Application Insights toosetup hello выполнения пользовательских политик"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: saeda
ms.openlocfilehash: c02d7178512c7f9e022385371c3effd4f8cb7726
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="55c8d-103">Azure Active Directory B2C: сбор журналов</span><span class="sxs-lookup"><span data-stu-id="55c8d-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="55c8d-104">В этой статье приводятся действия по сбору журналов из Azure AD B2C, с помощью которых вы сможете диагностировать неполадки в пользовательских политиках.</span><span class="sxs-lookup"><span data-stu-id="55c8d-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="55c8d-105">В настоящее время hello журналы подробные действия, описанные здесь, предназначены **только** tooaid в разработке пользовательских политик.</span><span class="sxs-lookup"><span data-stu-id="55c8d-105">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="55c8d-106">Не используйте режим разработки в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="55c8d-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="55c8d-107">Журналы собирать все утверждения, отправляемые tooand от поставщиков удостоверений hello во время разработки.</span><span class="sxs-lookup"><span data-stu-id="55c8d-107">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="55c8d-108">Если использовать в рабочей среде разработчика hello несет ответственности персональных данных (в частном порядке характера) собираются в журнал подробные сведения о приложении hello, которой они владеют.</span><span class="sxs-lookup"><span data-stu-id="55c8d-108">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="55c8d-109">Эти подробные журналы собираются только в том случае, когда политика hello помещается в **режим разработки**.</span><span class="sxs-lookup"><span data-stu-id="55c8d-109">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="55c8d-110">Использование Application Insights</span><span class="sxs-lookup"><span data-stu-id="55c8d-110">Use Application Insights</span></span>

<span data-ttu-id="55c8d-111">Azure AD B2C поддерживает функцию для отправки данных tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="55c8d-111">Azure AD B2C supports a feature for sending data tooApplication Insights.</span></span>  <span data-ttu-id="55c8d-112">Application Insights предоставляет toodiagnose способом исключения и визуализировать проблемах производительности приложения.</span><span class="sxs-lookup"><span data-stu-id="55c8d-112">Application Insights provides a way toodiagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="55c8d-113">Настройка Application Insights</span><span class="sxs-lookup"><span data-stu-id="55c8d-113">Setup Application Insights</span></span>

1. <span data-ttu-id="55c8d-114">Go toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="55c8d-114">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="55c8d-115">Убедитесь, что вы находитесь в hello клиента с подпиской Azure (не вашего клиента Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="55c8d-115">Ensure you are in hello tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="55c8d-116">Нажмите кнопку **+ создать** в меню навигации слева hello.</span><span class="sxs-lookup"><span data-stu-id="55c8d-116">Click **+ New** in hello left-hand navigation menu.</span></span>
1. <span data-ttu-id="55c8d-117">Найдите и выберите **Application Insights**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="55c8d-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="55c8d-118">Заполните форму hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="55c8d-118">Complete hello form and click **Create**.</span></span> <span data-ttu-id="55c8d-119">Выберите **Общие** для hello **тип приложения**.</span><span class="sxs-lookup"><span data-stu-id="55c8d-119">Select **General** for hello **Application Type**.</span></span>
1. <span data-ttu-id="55c8d-120">После создания ресурса Привет откройте ресурс Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="55c8d-120">Once hello resource has been created, open hello Application Insights resource.</span></span>
1. <span data-ttu-id="55c8d-121">Найти **свойства** в hello в левом меню и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="55c8d-121">Find **Properties** in hello left-menu, and click on it.</span></span>
1. <span data-ttu-id="55c8d-122">Копировать hello **ключ инструментирования** и сохраните его в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="55c8d-122">Copy hello **Instrumentation Key** and save it for hello next section.</span></span>

### <a name="set-up-hello-custom-policy"></a><span data-ttu-id="55c8d-123">Настройка пользовательской политики hello</span><span class="sxs-lookup"><span data-stu-id="55c8d-123">Set up hello custom policy</span></span>

1. <span data-ttu-id="55c8d-124">Откройте файл RP hello (например, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="55c8d-124">Open hello RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="55c8d-125">Добавьте следующие атрибуты toohello hello `<TrustFrameworkPolicy>` элемента:</span><span class="sxs-lookup"><span data-stu-id="55c8d-125">Add hello following attributes toohello `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="55c8d-126">Если он не существует, добавьте дочерний узел `<UserJourneyBehaviors>` toohello `<RelyingParty>` узла.</span><span class="sxs-lookup"><span data-stu-id="55c8d-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` toohello `<RelyingParty>` node.</span></span> <span data-ttu-id="55c8d-127">Он должен быть расположен сразу после hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`</span><span class="sxs-lookup"><span data-stu-id="55c8d-127">It must be located immediately after hello `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="55c8d-128">Добавьте следующий узлом в качестве дочернего элемента hello hello `<UserJourneyBehaviors>` элемента.</span><span class="sxs-lookup"><span data-stu-id="55c8d-128">Add hello following node as a child of hello `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="55c8d-129">Убедитесь, что tooreplace `{Your Application Insights Key}` с hello **ключ инструментирования** , полученный из Application Insights в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="55c8d-129">Make sure tooreplace `{Your Application Insights Key}` with hello **Instrumentation Key** that you obtained from Application Insights in hello previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="55c8d-130">`DeveloperMode="true"`сообщает телеметрии hello tooexpedite ApplicationInsights через конвейер обработки hello, хорошо для разработки, но ограничением на большую нагрузку.</span><span class="sxs-lookup"><span data-stu-id="55c8d-130">`DeveloperMode="true"` tells ApplicationInsights tooexpedite hello telemetry through hello processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="55c8d-131">`ClientEnabled="true"`отправляет hello ApplicationInsights клиентский сценарий для отслеживания представление и клиентские ошибки страниц (не требуется).</span><span class="sxs-lookup"><span data-stu-id="55c8d-131">`ClientEnabled="true"` sends hello ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="55c8d-132">`ServerEnabled="true"`отправляет hello существующих UserJourneyRecorder JSON как пользовательское событие tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="55c8d-132">`ServerEnabled="true"` sends hello existing UserJourneyRecorder JSON as a custom event tooApplication Insights.</span></span>
<span data-ttu-id="55c8d-133">Пример:</span><span class="sxs-lookup"><span data-stu-id="55c8d-133">Sample:</span></span>

  ```XML
  <TrustFrameworkPolicy
    ...
    TenantId="fabrikamb2c.onmicrosoft.com"
    PolicyId="SignUpOrSignInWithAAD"
    DeploymentMode="Development"
    UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="YourPolicyName" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
  </TrustFrameworkPolicy>
  ```

3. <span data-ttu-id="55c8d-134">Передача политики hello.</span><span class="sxs-lookup"><span data-stu-id="55c8d-134">Upload hello policy.</span></span>

### <a name="see-hello-logs-in-application-insights"></a><span data-ttu-id="55c8d-135">См. журналы hello в Application Insights</span><span class="sxs-lookup"><span data-stu-id="55c8d-135">See hello logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="55c8d-136">Новые журналы отобразятся в Application Insights через некоторое время (менее 5 минут).</span><span class="sxs-lookup"><span data-stu-id="55c8d-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="55c8d-137">Открытие ресурса Application Insights hello, созданную в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="55c8d-137">Open hello Application Insights resource that you created in hello [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="55c8d-138">В hello **Обзор** меню, щелкните **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="55c8d-138">In hello **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="55c8d-139">Откройте новую вкладку в Application Insights</span><span class="sxs-lookup"><span data-stu-id="55c8d-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="55c8d-140">Ниже приведен список запросов, которые можно использовать журналы toosee hello</span><span class="sxs-lookup"><span data-stu-id="55c8d-140">Here is a list of queries you can use toosee hello logs</span></span>

| <span data-ttu-id="55c8d-141">Запрос</span><span class="sxs-lookup"><span data-stu-id="55c8d-141">Query</span></span> | <span data-ttu-id="55c8d-142">Описание</span><span class="sxs-lookup"><span data-stu-id="55c8d-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="55c8d-143">traces</span><span class="sxs-lookup"><span data-stu-id="55c8d-143">traces</span></span> | <span data-ttu-id="55c8d-144">Просмотреть все hello журналы, формируемые службой Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="55c8d-144">See all of hello logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="55c8d-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="55c8d-145">traces \\</span></span>| <span data-ttu-id="55c8d-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="55c8d-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="55c8d-147">Просмотреть все hello журналы, формируемые службой Azure AD B2C для hello последний день</span><span class="sxs-lookup"><span data-stu-id="55c8d-147">See all of hello logs generated by Azure AD B2C for hello last day</span></span>

<span data-ttu-id="55c8d-148">Hello записей может быть длительным.</span><span class="sxs-lookup"><span data-stu-id="55c8d-148">hello entries may be long.</span></span>  <span data-ttu-id="55c8d-149">Экспорт tooCSV для рассмотрим это более подробно.</span><span class="sxs-lookup"><span data-stu-id="55c8d-149">Export tooCSV for a closer look.</span></span>

<span data-ttu-id="55c8d-150">Дополнительные сведения о средстве аналитики hello [здесь](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="55c8d-150">You can learn more about hello Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="55c8d-151">Сообщество Hello разработала разработчиков пользовательских пути просмотра toohelp удостоверений.</span><span class="sxs-lookup"><span data-stu-id="55c8d-151">hello community has developed a user journey viewer toohelp identity developers.</span></span>  <span data-ttu-id="55c8d-152">Это средство не поддерживается Майкрософт и предоставляется исключительно в том виде, в котором оно было создано.</span><span class="sxs-lookup"><span data-stu-id="55c8d-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="55c8d-153">Считывает из экземпляра Application Insights и обеспечивает представление структуры также событий пути hello пользователем.</span><span class="sxs-lookup"><span data-stu-id="55c8d-153">It reads from your Application Insights instance and provides a well-structure view of hello user journey events.</span></span>  <span data-ttu-id="55c8d-154">Получить исходный код hello и развернуть его в собственное решение.</span><span class="sxs-lookup"><span data-stu-id="55c8d-154">You obtain hello source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="55c8d-155">В настоящее время hello журналы подробные действия, описанные здесь, предназначены **только** tooaid в разработке пользовательских политик.</span><span class="sxs-lookup"><span data-stu-id="55c8d-155">Currently, hello detailed activity logs described here are designed **ONLY** tooaid in development of custom policies.</span></span> <span data-ttu-id="55c8d-156">Не используйте режим разработки в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="55c8d-156">Do not use development mode in production.</span></span>  <span data-ttu-id="55c8d-157">Журналы собирать все утверждения, отправляемые tooand от поставщиков удостоверений hello во время разработки.</span><span class="sxs-lookup"><span data-stu-id="55c8d-157">Logs collect all claims sent tooand from hello identity providers during development.</span></span>  <span data-ttu-id="55c8d-158">Если использовать в рабочей среде разработчика hello несет ответственности персональных данных (в частном порядке характера) собираются в журнал подробные сведения о приложении hello, которой они владеют.</span><span class="sxs-lookup"><span data-stu-id="55c8d-158">If used in production, hello developer assumes responsibility for PII (Privately Identifiable Information) collected in hello App Insights log that they own.</span></span>  <span data-ttu-id="55c8d-159">Эти подробные журналы собираются только в том случае, когда политика hello помещается в **режим разработки**.</span><span class="sxs-lookup"><span data-stu-id="55c8d-159">These detailed logs are only collected when hello policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="55c8d-160">Репозиторий GitHub с примерами неподдерживаемых пользовательских политик и связанных с ними средств</span><span class="sxs-lookup"><span data-stu-id="55c8d-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="55c8d-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55c8d-161">Next Steps</span></span>

<span data-ttu-id="55c8d-162">Просмотр данных hello в Application Insights toohelp понимаете как hello платформы идентификации качества базовой B2C работает toodeliver возникает собственные удостоверения.</span><span class="sxs-lookup"><span data-stu-id="55c8d-162">Explore hello data in Application Insights toohelp you understand how hello Identity Experience Framework underlying B2C works toodeliver your own identity experiences.</span></span>
