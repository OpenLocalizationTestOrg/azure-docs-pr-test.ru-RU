---
title: "Azure AD B2C: устранение неполадок в настраиваемых политиках с помощью Application Insights | Документация Майкрософт"
description: "Сведения о настройке Application Insights для отслеживания выполнения пользовательских политик"
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
ms.openlocfilehash: 8c79df33cd5f04f490e2cc6372f7e8ac1c4d9bbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-collecting-logs"></a><span data-ttu-id="7f8e2-103">Azure Active Directory B2C: сбор журналов</span><span class="sxs-lookup"><span data-stu-id="7f8e2-103">Azure Active Directory B2C: Collecting Logs</span></span>

<span data-ttu-id="7f8e2-104">В этой статье приводятся действия по сбору журналов из Azure AD B2C, с помощью которых вы сможете диагностировать неполадки в пользовательских политиках.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-104">This article provides steps for collecting logs from Azure AD B2C so that you can diagnose problems with your custom policies.</span></span>

>[!NOTE]
><span data-ttu-id="7f8e2-105">Сейчас детально описанные здесь журналы действий предназначены **только** для упрощения разработки пользовательских политик.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-105">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="7f8e2-106">Не используйте режим разработки в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-106">Do not use development mode  in production.</span></span>  <span data-ttu-id="7f8e2-107">В журналах регистрируются все утверждения, отправляемые и принимаемые поставщиками удостоверений во время разработки.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-107">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="7f8e2-108">При использовании режима разработки в рабочей среде разработчик несет ответственность за персональные данные (личные сведения), собранные в его журнале App Insights.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-108">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="7f8e2-109">Эти подробные журналы могут собираться, только когда политика помещается в **режим разработки**.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-109">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>


## <a name="use-application-insights"></a><span data-ttu-id="7f8e2-110">Использование Application Insights</span><span class="sxs-lookup"><span data-stu-id="7f8e2-110">Use Application Insights</span></span>

<span data-ttu-id="7f8e2-111">Служба Azure AD B2C поддерживает функцию отправки данных в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-111">Azure AD B2C supports a feature for sending data to Application Insights.</span></span>  <span data-ttu-id="7f8e2-112">Application Insights позволяет диагностировать исключения и визуализировать проблемы производительности в приложениях.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-112">Application Insights provides a way to diagnose exceptions and visualize application performance issues.</span></span>

### <a name="setup-application-insights"></a><span data-ttu-id="7f8e2-113">Настройка Application Insights</span><span class="sxs-lookup"><span data-stu-id="7f8e2-113">Setup Application Insights</span></span>

1. <span data-ttu-id="7f8e2-114">Перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-114">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7f8e2-115">Убедитесь, что вы находитесь в клиенте с подпиской Azure (а не в клиенте Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-115">Ensure you are in the tenant with your Azure subscription (not your Azure AD B2C tenant).</span></span>
1. <span data-ttu-id="7f8e2-116">На панели навигации слева щелкните **+ Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-116">Click **+ New** in the left-hand navigation menu.</span></span>
1. <span data-ttu-id="7f8e2-117">Найдите и выберите **Application Insights**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-117">Search for and select **Application Insights**, then click **Create**.</span></span>
1. <span data-ttu-id="7f8e2-118">Заполните форму и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-118">Complete the form and click **Create**.</span></span> <span data-ttu-id="7f8e2-119">Выберите **универсальный** **тип приложения**.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-119">Select **General** for the **Application Type**.</span></span>
1. <span data-ttu-id="7f8e2-120">Откройте ресурс Application Insights после его создания.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-120">Once the resource has been created, open the Application Insights resource.</span></span>
1. <span data-ttu-id="7f8e2-121">Найдите пункт **Свойства** в меню слева и выберите его.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-121">Find **Properties** in the left-menu, and click on it.</span></span>
1. <span data-ttu-id="7f8e2-122">Скопируйте **ключ инструментирования** и сохраните его для использования в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-122">Copy the **Instrumentation Key** and save it for the next section.</span></span>

### <a name="set-up-the-custom-policy"></a><span data-ttu-id="7f8e2-123">Настройка пользовательской политики</span><span class="sxs-lookup"><span data-stu-id="7f8e2-123">Set up the custom policy</span></span>

1. <span data-ttu-id="7f8e2-124">Откройте файл проверяющей стороны (например, SignUpOrSignin.xml).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-124">Open the RP file (for example, SignUpOrSignin.xml).</span></span>
1. <span data-ttu-id="7f8e2-125">Добавьте следующие атрибуты в элемент `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-125">Add the following attributes to the `<TrustFrameworkPolicy>` element:</span></span>

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. <span data-ttu-id="7f8e2-126">Если он еще не существует, добавьте дочерний узел `<UserJourneyBehaviors>` в узел `<RelyingParty>`.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-126">If it doesn't exist already, add a child node `<UserJourneyBehaviors>` to the `<RelyingParty>` node.</span></span> <span data-ttu-id="7f8e2-127">Он должен находиться сразу после `<DefaultUserJourney ReferenceId="YourPolicyName" />`.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-127">It must be located immediately after the `<DefaultUserJourney ReferenceId="YourPolicyName" />`</span></span>
2. <span data-ttu-id="7f8e2-128">Добавьте следующий узел в качестве дочернего узла элемента `<UserJourneyBehaviors>`.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-128">Add the following node as a child of the `<UserJourneyBehaviors>` element.</span></span> <span data-ttu-id="7f8e2-129">Обязательно замените `{Your Application Insights Key}` **ключом инструментирования**, полученным из Application Insights в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-129">Make sure to replace `{Your Application Insights Key}` with the **Instrumentation Key** that you obtained from Application Insights in the previous section.</span></span>

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * <span data-ttu-id="7f8e2-130">Параметр `DeveloperMode="true"` сообщает Application Insights о том, что необходимо ускорить передачу данных телеметрии через конвейер обработки. Это удобно при разработке, но связано с ограничениями при больших объемах.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-130">`DeveloperMode="true"` tells ApplicationInsights to expedite the telemetry through the processing pipeline, good for development, but constrained at high volumes.</span></span>
  * <span data-ttu-id="7f8e2-131">Параметр `ClientEnabled="true"` отправляет Application Insights клиентский скрипт для отслеживания представления страницы и ошибок на стороне клиента (необязательно).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-131">`ClientEnabled="true"` sends the ApplicationInsights client-side script for tracking page view and client-side errors (not needed).</span></span>
  * <span data-ttu-id="7f8e2-132">Параметр `ServerEnabled="true"` отправляет существующие данные JSON UserJourneyRecorder как пользовательское событие в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-132">`ServerEnabled="true"` sends the existing UserJourneyRecorder JSON as a custom event to Application Insights.</span></span>
<span data-ttu-id="7f8e2-133">Пример:</span><span class="sxs-lookup"><span data-stu-id="7f8e2-133">Sample:</span></span>

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

3. <span data-ttu-id="7f8e2-134">Отправьте политику.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-134">Upload the policy.</span></span>

### <a name="see-the-logs-in-application-insights"></a><span data-ttu-id="7f8e2-135">Просмотр журналов в Application Insights</span><span class="sxs-lookup"><span data-stu-id="7f8e2-135">See the logs in Application Insights</span></span>

>[!NOTE]
> <span data-ttu-id="7f8e2-136">Новые журналы отобразятся в Application Insights через некоторое время (менее 5 минут).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-136">There is a short delay (less than five minutes) before you can see new logs in Application Insights.</span></span>

1. <span data-ttu-id="7f8e2-137">Откройте созданный ресурс Application Insights на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-137">Open the Application Insights resource that you created in the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="7f8e2-138">В меню **Обзор** выберите пункт **Analytics**.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-138">In the **Overview** menu, click on **Analytics**.</span></span>
1. <span data-ttu-id="7f8e2-139">Откройте новую вкладку в Application Insights</span><span class="sxs-lookup"><span data-stu-id="7f8e2-139">Open a new tab in Application Insights.</span></span>
1. <span data-ttu-id="7f8e2-140">Ниже приведен список запросов, которые можно использовать для просмотра журналов.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-140">Here is a list of queries you can use to see the logs</span></span>

| <span data-ttu-id="7f8e2-141">Запрос</span><span class="sxs-lookup"><span data-stu-id="7f8e2-141">Query</span></span> | <span data-ttu-id="7f8e2-142">Описание</span><span class="sxs-lookup"><span data-stu-id="7f8e2-142">Description</span></span> |
|---------------------|--------------------|
<span data-ttu-id="7f8e2-143">traces</span><span class="sxs-lookup"><span data-stu-id="7f8e2-143">traces</span></span> | <span data-ttu-id="7f8e2-144">Просмотр всех журналов, созданных Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7f8e2-144">See all of the logs generated by Azure AD B2C</span></span> |
<span data-ttu-id="7f8e2-145">traces \\</span><span class="sxs-lookup"><span data-stu-id="7f8e2-145">traces \\</span></span>| <span data-ttu-id="7f8e2-146">where timestamp > ago(1d)</span><span class="sxs-lookup"><span data-stu-id="7f8e2-146">where timestamp > ago(1d)</span></span> | <span data-ttu-id="7f8e2-147">Просмотр всех журналов, созданных Azure AD B2C за последний день</span><span class="sxs-lookup"><span data-stu-id="7f8e2-147">See all of the logs generated by Azure AD B2C for the last day</span></span>

<span data-ttu-id="7f8e2-148">Записи могут быть длинными.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-148">The entries may be long.</span></span>  <span data-ttu-id="7f8e2-149">Выполните экспорт в CSV-файл, чтобы изучить их подробнее.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-149">Export to CSV for a closer look.</span></span>

<span data-ttu-id="7f8e2-150">Дополнительные сведения об инструменте Analytics см. [здесь](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span><span class="sxs-lookup"><span data-stu-id="7f8e2-150">You can learn more about the Analytics tool [here](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).</span></span>

>[!NOTE]
><span data-ttu-id="7f8e2-151">Для разработчиков удостоверений сообщество разработало средство просмотра пути взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-151">The community has developed a user journey viewer to help identity developers.</span></span>  <span data-ttu-id="7f8e2-152">Это средство не поддерживается Майкрософт и предоставляется исключительно в том виде, в котором оно было создано.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-152">It is not supported by Microsoft and made available strictly as-is.</span></span>  <span data-ttu-id="7f8e2-153">Оно считывается из экземпляра Application Insights и обеспечивает хорошо структурированное представление событий пути взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-153">It reads from your Application Insights instance and provides a well-structure view of the user journey events.</span></span>  <span data-ttu-id="7f8e2-154">Исходный код можно получить и развернуть в собственном решении.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-154">You obtain the source code and deploy it in your own solution.</span></span>

>[!NOTE]
><span data-ttu-id="7f8e2-155">Сейчас детально описанные здесь журналы действий предназначены **только** для упрощения разработки пользовательских политик.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-155">Currently, the detailed activity logs described here are designed **ONLY** to aid in development of custom policies.</span></span> <span data-ttu-id="7f8e2-156">Не используйте режим разработки в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-156">Do not use development mode in production.</span></span>  <span data-ttu-id="7f8e2-157">В журналах регистрируются все утверждения, отправляемые и принимаемые поставщиками удостоверений во время разработки.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-157">Logs collect all claims sent to and from the identity providers during development.</span></span>  <span data-ttu-id="7f8e2-158">При использовании режима разработки в рабочей среде разработчик несет ответственность за персональные данные (личные сведения), собранные в его журнале App Insights.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-158">If used in production, the developer assumes responsibility for PII (Privately Identifiable Information) collected in the App Insights log that they own.</span></span>  <span data-ttu-id="7f8e2-159">Эти подробные журналы могут собираться, только когда политика помещается в **режим разработки**.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-159">These detailed logs are only collected when the policy is placed on **DEVELOPMENT MODE**.</span></span>

[<span data-ttu-id="7f8e2-160">Репозиторий GitHub с примерами неподдерживаемых пользовательских политик и связанных с ними средств</span><span class="sxs-lookup"><span data-stu-id="7f8e2-160">Github Repository for Unsupported Custom Policy Samples and Related tools</span></span>](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a><span data-ttu-id="7f8e2-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f8e2-161">Next Steps</span></span>

<span data-ttu-id="7f8e2-162">Изучите данные в Application Insights, чтобы понять, как работает платформа Identity Experience Framework, лежащая в основе B2C, чтобы предоставить собственные удостоверения.</span><span class="sxs-lookup"><span data-stu-id="7f8e2-162">Explore the data in Application Insights to help you understand how the Identity Experience Framework underlying B2C works to deliver your own identity experiences.</span></span>
