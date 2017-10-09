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
# <a name="walkthrough-integrate-rest-api-claims-exchanges-in-your-azure-ad-b2c-user-journey-as-validation-on-user-input"></a>Пошаговое руководство. Интеграция обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как проверка входных данных

Hello удостоверения качества Framework (IEF), лежащей в основе Azure Active Directory B2C (Azure AD B2C) позволяет hello удостоверение разработчика toointegrate взаимодействия с API REST в пути пользователя.  

В конце этого пошагового руководства hello будет может toocreate путешествия пользователя Azure AD B2C взаимодействует с службы RESTful.

Hello IEF отправляет данные в утверждениях и получает данные обратно в заявках. Hello взаимодействий с hello API:

- можно реализовать как обмен утверждениями REST API или профиль проверки, выполняемой на этапе оркестрации;
- Обычно проверяет входные данные от пользователя hello. Если значение hello от пользователя hello отклоняется, hello пользователя можно повторить попытку tooenter допустимое значение с возможностью hello tooreturn сообщение об ошибке.

Можно также создать hello взаимодействия на этапе orchestration. Дополнительные сведения см. в статье [Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации](active-directory-b2c-rest-api-step-custom.md).

Пример профиля проверки hello мы будем использовать пути пользователя изменить профиль hello в файл пакета начального приветствия ProfileEdit.xml.

Мы можно проверить это имя hello, предоставляемых пользователем hello в профиле hello редактирования не входит в список исключений.

## <a name="prerequisites"></a>Предварительные требования

- Toocomplete клиента Azure AD B2C локальную учетную запись регистрации-повышение/вход, как описано в [Приступая к работе](active-directory-b2c-get-started-custom.md).
- Toointeract конечной точки REST API с. Для этого руководства мы настроили демонстрационный сайт [WingTipGames](https://wingtipgamesb2c.azurewebsites.net/), используя службу REST API.

## <a name="step-1-prepare-hello-rest-api-function"></a>Шаг 1: Подготовка функции API-интерфейса REST hello

> [!NOTE]
> Настройка функций API-интерфейса REST находится за пределами hello рамки этой статьи. [Функции Azure](https://docs.microsoft.com/azure/azure-functions/functions-reference) обеспечивает лучший набор средств служб RESTful toocreate в облаке hello.

Мы создали функцию Azure, которая получает утверждение, ожидаемое как `playerTag`. функция Hello проверяет существование этого утверждения. Можно получить доступ к код завершения Azure функции hello в [GitHub](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/AzureFunctionsSamples).

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

Hello IEF ожидает hello `userMessage` утверждения, hello Azure функция возвращает. Это утверждение будет представлен как пользователь toohello строки при сбое проверки hello, например при возврате состояния 409 (конфликт) в предшествующих пример hello.

## <a name="step-2-configure-hello-restful-api-claims-exchange-as-a-technical-profile-in-your-trustframeworkextensionsxml-file"></a>Шаг 2: Настройка exchange утверждений RESTful API hello как технические профиля в файле TrustFrameworkExtensions.xml

Технические профиль является полной конфигурации hello обмена hello требуемого с hello службы RESTful. Откройте файл TrustFrameworkExtensions.xml hello и добавьте следующий фрагмент XML внутри hello hello `<ClaimsProviders>` элемента.

> [!NOTE]
> В следующий XML-код, RESTful поставщика hello `Version=1.0.0.0` говорится, что протокол hello. Рассматривайте его как hello функцию, которая будет взаимодействовать с внешней службы hello. <!-- TODO: A full definition of hello schema can be found...link tooRESTful Provider schema definition>-->

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

Hello `InputClaims` элемент определяет hello утверждений, которые будут отправляться от службы REST toohello IEF hello. В этом примере hello содержимое утверждения hello `givenName` будет отправлено службе REST toohello как `playerTag`. В этом примере hello IEF непредвиденным утверждений обратно. Вместо этого он ожидает ответа от службы REST hello и действует на основании hello коды состояния, которые он получает.

## <a name="step-3-include-hello-restful-service-claims-exchange-in-self-asserted-technical-profile-where-you-want-toovalidate-hello-user-input"></a>Шаг 3: Включите exchange утверждения службы RESTful hello в самозаверяемые технические профиля, где требуется ввод данных пользователем toovalidate hello

Hello чаще всего этапа проверки hello используется hello взаимодействия с пользователем. Все диалоги, где пользователь hello является ожидаемым tooprovide ввода не *самим пользователем технические профилей*. В этом примере мы добавим технические профиль toohello проверки частный Asserted ProfileUpdate hello. Это профиль технические hello, hello файл политики проверяющей стороны (RP) `Profile Edit` использует.

tooadd hello утверждений exchange toohello самим пользователем технические профиля:

1. Откройте файл TrustFrameworkBase.xml hello и выполните поиск `<TechnicalProfile Id="SelfAsserted-ProfileUpdate">`.
2. Проверьте конфигурацию hello технические профиля. Обратите внимание, как hello exchange с пользователем hello определяется как утверждения, задаваемые hello пользователя (входящих утверждений) и утверждения, которые будут являться назад от поставщика самозаверяемые hello (исходящие утверждения).
3. Найдите `TechnicalProfileReferenceId="SelfAsserted-ProfileUpdate`. Обратите внимание, что этот профиль вызывается как этап оркестрации 6 `<UserJourney Id="ProfileEdit">`.

## <a name="step-4-upload-and-test-hello-profile-edit-rp-policy-file"></a>Шаг 4: Отправка и тестирования файл политики RP редактирование профиля hello

1. Отправьте новую версию файла TrustFrameworkExtensions.xml hello hello.
2. Используйте **запустить сейчас** профиль hello tootest изменить файл политики RP.
3. Выполнение проверки hello одним из существующих имен hello (например, mcvinny) в hello **заданное имя** поля. Если все настроено правильно, должно появиться сообщение, уведомляющее пользователя hello hello проигрывателя тег уже используется.

## <a name="next-steps"></a>Дальнейшие действия

[Изменение hello профиля редактирования и пользователь toogather Дополнительные сведения о регистрации от пользователей](active-directory-b2c-create-custom-attributes-profile-edit-custom.md)

[Пошаговое руководство. Интеграция обмена утверждениями REST API в пути взаимодействия пользователя Azure AD B2C как этап оркестрации](active-directory-b2c-rest-api-step-custom.md)
