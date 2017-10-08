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
# <a name="azure-active-directory-b2c-collecting-logs"></a>Azure Active Directory B2C: сбор журналов

В этой статье приводятся действия по сбору журналов из Azure AD B2C, с помощью которых вы сможете диагностировать неполадки в пользовательских политиках.

>[!NOTE]
>В настоящее время hello журналы подробные действия, описанные здесь, предназначены **только** tooaid в разработке пользовательских политик. Не используйте режим разработки в рабочей среде.  Журналы собирать все утверждения, отправляемые tooand от поставщиков удостоверений hello во время разработки.  Если использовать в рабочей среде разработчика hello несет ответственности персональных данных (в частном порядке характера) собираются в журнал подробные сведения о приложении hello, которой они владеют.  Эти подробные журналы собираются только в том случае, когда политика hello помещается в **режим разработки**.


## <a name="use-application-insights"></a>Использование Application Insights

Azure AD B2C поддерживает функцию для отправки данных tooApplication аналитики.  Application Insights предоставляет toodiagnose способом исключения и визуализировать проблемах производительности приложения.

### <a name="setup-application-insights"></a>Настройка Application Insights

1. Go toohello [портал Azure](https://portal.azure.com). Убедитесь, что вы находитесь в hello клиента с подпиской Azure (не вашего клиента Azure AD B2C).
1. Нажмите кнопку **+ создать** в меню навигации слева hello.
1. Найдите и выберите **Application Insights**, а затем щелкните **Создать**.
1. Заполните форму hello и нажмите кнопку **создать**. Выберите **Общие** для hello **тип приложения**.
1. После создания ресурса Привет откройте ресурс Application Insights hello.
1. Найти **свойства** в hello в левом меню и щелкните его.
1. Копировать hello **ключ инструментирования** и сохраните его в следующем разделе hello.

### <a name="set-up-hello-custom-policy"></a>Настройка пользовательской политики hello

1. Откройте файл RP hello (например, SignUpOrSignin.xml).
1. Добавьте следующие атрибуты toohello hello `<TrustFrameworkPolicy>` элемента:

  ```XML
  DeploymentMode="Development"
  UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
  ```

1. Если он не существует, добавьте дочерний узел `<UserJourneyBehaviors>` toohello `<RelyingParty>` узла. Он должен быть расположен сразу после hello`<DefaultUserJourney ReferenceId="YourPolicyName" />`
2. Добавьте следующий узлом в качестве дочернего элемента hello hello `<UserJourneyBehaviors>` элемента. Убедитесь, что tooreplace `{Your Application Insights Key}` с hello **ключ инструментирования** , полученный из Application Insights в предыдущем разделе hello.

  ```XML
  <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
  ```

  * `DeveloperMode="true"`сообщает телеметрии hello tooexpedite ApplicationInsights через конвейер обработки hello, хорошо для разработки, но ограничением на большую нагрузку.
  * `ClientEnabled="true"`отправляет hello ApplicationInsights клиентский сценарий для отслеживания представление и клиентские ошибки страниц (не требуется).
  * `ServerEnabled="true"`отправляет hello существующих UserJourneyRecorder JSON как пользовательское событие tooApplication аналитики.
Пример:

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

3. Передача политики hello.

### <a name="see-hello-logs-in-application-insights"></a>См. журналы hello в Application Insights

>[!NOTE]
> Новые журналы отобразятся в Application Insights через некоторое время (менее 5 минут).

1. Открытие ресурса Application Insights hello, созданную в hello [портал Azure](https://portal.azure.com).
1. В hello **Обзор** меню, щелкните **Analytics**.
1. Откройте новую вкладку в Application Insights
1. Ниже приведен список запросов, которые можно использовать журналы toosee hello

| Запрос | Описание |
|---------------------|--------------------|
traces | Просмотреть все hello журналы, формируемые службой Azure AD B2C |
traces \| where timestamp > ago(1d) | Просмотреть все hello журналы, формируемые службой Azure AD B2C для hello последний день

Hello записей может быть длительным.  Экспорт tooCSV для рассмотрим это более подробно.

Дополнительные сведения о средстве аналитики hello [здесь](https://docs.microsoft.com/azure/application-insights/app-insights-analytics).

>[!NOTE]
>Сообщество Hello разработала разработчиков пользовательских пути просмотра toohelp удостоверений.  Это средство не поддерживается Майкрософт и предоставляется исключительно в том виде, в котором оно было создано.  Считывает из экземпляра Application Insights и обеспечивает представление структуры также событий пути hello пользователем.  Получить исходный код hello и развернуть его в собственное решение.

>[!NOTE]
>В настоящее время hello журналы подробные действия, описанные здесь, предназначены **только** tooaid в разработке пользовательских политик. Не используйте режим разработки в рабочей среде.  Журналы собирать все утверждения, отправляемые tooand от поставщиков удостоверений hello во время разработки.  Если использовать в рабочей среде разработчика hello несет ответственности персональных данных (в частном порядке характера) собираются в журнал подробные сведения о приложении hello, которой они владеют.  Эти подробные журналы собираются только в том случае, когда политика hello помещается в **режим разработки**.

[Репозиторий GitHub с примерами неподдерживаемых пользовательских политик и связанных с ними средств](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies)



## <a name="next-steps"></a>Дальнейшие действия

Просмотр данных hello в Application Insights toohelp понимаете как hello платформы идентификации качества базовой B2C работает toodeliver возникает собственные удостоверения.
