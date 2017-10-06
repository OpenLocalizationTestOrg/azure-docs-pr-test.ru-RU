---
title: "Azure Active Directory B2C: получение токена с помощью приложения Android | Документация Майкрософт"
description: "В этой статье будет показано, как toocreate Android приложение, которое использует AppAuth с учетными данными пользователей Azure Active Directory B2C toomanage и проверки подлинности пользователей."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure AD B2C. Вход с помощью приложения Android

Hello платформы удостоверений использует открытых стандартов, такие как OAuth2 и OpenID Connect. Это позволяет разработчикам tooleverage всех библиотек, которые они будут toointegrate с наших служб. Разработчики tooaid с помощью платформы с другими библиотеками, мы написали несколько пошаговых руководств, как это один toodemonstrate как tooconfigure сторонних производителей библиотеки tooconnect toohello платформы удостоверений. Большинство библиотек, которые реализуют [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) будут работать на платформе Microsoft Identity может tooconnect toohello.

> [!WARNING]
> Корпорация Майкрософт не предоставляет исправления для библиотек сторонних производителей и не выполняла их проверку. В этом примере использует сторонних производителей библиотеку вызывается AppAuth которого была протестирована на совместимость в основных сценариях с Azure AD B2C hello. Проблемы и запрашивать новые функции должно быть проект с открытым исходным направленной toohello библиотеки. Дополнительные сведения см. в [этой статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).  
>
>

Если вы новый tooOAuth2 или OpenID Connect большая часть конфигурации этого образца может оказаться гораздо tooyou смысле. Рекомендуется рассмотреть приведен краткий [Обзор протокола hello, мы здесь описаны](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Создание каталога Azure AD B2C

Перед использованием Azure AD B2C необходимо создать каталог или клиент. Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д. Если каталог B2C еще не создан, [создайте его](active-directory-b2c-get-started.md), прежде чем продолжить.

## <a name="create-an-application"></a>Создание приложения

Далее необходимо toocreate приложения в каталоге B2C. Это предоставляет сведения Azure AD, что ему требуется toocommunicate безопасно вместе с приложением. toocreate мобильного приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md). Не забудьте сделать следующее.

* Включить **Native Client** в приложение hello.
* Копировать hello **идентификатор приложения** , назначенный tooyour приложения. Этот идентификатор потребуется позднее.
* Настройте **URI перенаправления** собственного клиента (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Этот идентификатор также потребуется позднее.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Создание политик

В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md). Это приложение предусматривает одну процедуру идентификации, сочетающую в себе вход и регистрацию. Необходимые toocreate этой политики, как описано в [статье политики](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). При создании политики hello, нужно убедиться, что:

* Выберите hello **отображаемое имя** как атрибут регистрации в политике.
* Выберите hello **отображаемое имя** и **идентификатор объекта** утверждений приложения в каждой политике. Можно также выбрать другие утверждения.
* Копировать hello **имя** каждой политики, после его создания. Он должен иметь префикс hello `b2c_1_`.  Имя политики hello потребуется позднее.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

После создания политики вы готовы toobuild приложения.

## <a name="download-hello-sample-code"></a>Загрузить пример кода hello

Мы разместили рабочий пример, использующий AppAuth с Azure AD B2C, [на сайте GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Можно загрузить кода hello и запустите его. Вы можете быстро приступить к работе с приложением с помощью Azure AD B2C конфигурацию в соответствии с инструкциями hello в hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

Образец Hello является модификацией образца hello, предоставляемые [AppAuth](https://openid.github.io/AppAuth-Android/). Посетите их toolearn страницы, Дополнительные сведения о AppAuth и его компонентов.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Изменение toouse вашего приложения Azure AD B2C, с AppAuth

> [!NOTE]
> AppAuth поддерживает Android API версии 16 (Jellybean) и более поздних. Мы советуем использовать API версии 23 и более поздних.
>

### <a name="configuration"></a>Конфигурация

Соединение можно настроить с помощью Azure AD B2C, либо указав обнаружение hello URI или указав конечную точку авторизации hello и маркера URI конечных точек. В любом случае потребуется hello следующую информацию:

* идентификатор клиента (например, contoso.onmicrosoft.com);
* имя политики (например, B2C\_1\_SignUpIn).

Если выбрана tooautomatically обнаружение hello авторизации и маркер URI конечных точек, вы должны будете toofetch сведения из процесса обнаружения hello URI. URI могут быть вызваны замена hello клиента обнаружения Hello\_идентификатор и политику hello\_имя в hello URL-адреса:

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

Затем вы можете получать hello авторизации и маркеров URI конечных точек и создания объекта AuthorizationServiceConfiguration, выполнив следующие hello:

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

Вместо обнаружения tooobtain hello авторизации и маркеров URI конечных точек, можно также указать их явным образом, заменив hello клиента\_идентификатор и политику hello\_имя в hello URL ниже:

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Выполните следующий код toocreate hello объекта AuthorizationServiceConfiguration:

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Авторизация

После настройки или извлечения конфигурации службы авторизации можно сформировать запрос авторизации. запрос toocreate hello, вам потребуется hello следующую информацию:

* идентификатор клиента (например, 00000000-0000-0000-0000-000000000000);
* URI перенаправления с настраиваемой схемой (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect).

Оба элемента нужно сохранить при [регистрации приложения](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

См. toohello [AppAuth руководство](https://openid.github.io/AppAuth-Android/) на как toocomplete hello оставшаяся часть процедуры hello. Если вам требуется tooquickly Приступая к работе с работающем приложении, ознакомьтесь с [выборка](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Следуйте указаниям hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter конфигурацию Azure AD B2C.

Мы всегда являются предложения и откройте toofeedback! Если возникли проблемы с этим разделом, или иметь рекомендации по улучшению это содержимое, мы ценим ваши отзывы hello нижней части страницы приветствия. Для запросов, компонент, добавьте их слишком[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

