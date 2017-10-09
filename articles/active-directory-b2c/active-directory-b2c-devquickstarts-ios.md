---
title: "Azure AD B2C: получение токена с помощью приложения iOS | Документация Майкрософт"
description: "В этой статье будет показано, как toocreate приложения iOS, использующее AppAuth удостоверений пользователей Azure Active Directory B2C toomanage и с проверки подлинности пользователей."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure AD B2C. Вход с помощью приложения iOS

Hello платформы удостоверений использует открытых стандартов, такие как OAuth2 и OpenID Connect. Использование открытый стандартный протокол предоставляет широкий выбор разработчик, при выборе toointegrate библиотеки с помощью наших служб. Мы предоставили данного пошагового руководства и других подобных тем tooaid разработчики при написании приложения, которые подключаются toohello платформы Microsoft Identity. Большинство библиотек, которые реализуют [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) являются платформой удостоверений Microsoft может tooconnect toohello.

> [!WARNING]
> Корпорация Майкрософт не предоставляет исправления для библиотек сторонних производителей и не выполняла их проверку. Этот образец использует стороннюю библиотеку, вызывается AppAuth которого была протестирована на совместимость в основных сценариях с Azure AD B2C hello. Проблемы и запрашивать новые функции должно быть проект с открытым исходным направленной toohello библиотеки. Дополнительные сведения см. в [этой статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).
>
>

Если вы новый tooOAuth2 или OpenID Connect, большая часть конфигурации этого образца может оказаться гораздо tooyou смысле. Рекомендуется рассмотреть приведен краткий [Обзор протокола hello, мы здесь описаны](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Создание каталога Azure AD B2C
Перед использованием Azure AD B2C необходимо создать каталог или клиент. Каталог — это контейнер для всех пользователей, приложений, групп и т. д. Если каталог B2C еще не создан, [создайте его](active-directory-b2c-get-started.md), прежде чем продолжить.

## <a name="create-an-application"></a>Создание приложения
Далее необходимо toocreate приложения в каталоге B2C. Регистрация приложения Hello информация Azure AD, он должен toocommunicate безопасно вместе с приложением. toocreate мобильного приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md). Не забудьте сделать следующее.

* Включить **Native client** в приложение hello.
* Копировать hello **идентификатор приложения** , назначенный tooyour приложения. Этот GUID понадобится позже.
* Задайте **URI перенаправления** с настраиваемой схемой (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Этот URI понадобится позже.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Создание политик
В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md). Это приложение предусматривает одну процедуру идентификации, сочетающую в себе вход и регистрацию. Создайте эту политику, как описано в [справочной статье о политиках](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). При создании политики hello, нужно убедиться, что:

* В разделе **регистрации атрибуты**выберите атрибут hello **отображаемое имя**.  Можно также выбрать другие атрибуты.
* В разделе **утверждений приложения**, выберите hello утверждений **отображаемое имя** и **идентификатор объекта пользователя**. Можно также выбрать другие утверждения.
* Копировать hello **имя** каждой политики, после его создания. Имя политики добавляется префикс с `b2c_1_` при сохранении политики hello.  Требуется имя политики hello позже.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

После создания политики вы готовы toobuild приложения.

## <a name="download-hello-sample-code"></a>Загрузить пример кода hello
Мы разместили рабочий пример, использующий AppAuth с Azure AD B2C, [на сайте GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Можно загрузить кода hello и запустите его. toouse собственные Azure AD B2C клиента, следуйте инструкциям hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

В этом примере был создан в соответствии с инструкциями hello README по hello [iOS AppAuth проекта на GitHub](https://github.com/openid/AppAuth-iOS). Дополнительные сведения о работе образец hello и библиотеки hello ссылаться hello README AppAuth на GitHub.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Изменение toouse вашего приложения Azure AD B2C, с AppAuth

> [!NOTE]
> AppAuth поддерживает iOS 7 и более поздние версии.  Однако toosupport социальных имена входа в Google, SFSafariViewController потребуется которых требуется iOS 9 или более поздней версии.
>

### <a name="configuration"></a>Конфигурация

Соединение с Azure AD B2C можно настроить, указав конечную точку авторизации hello и маркера URI конечных точек.  toogenerate эти URI необходимо hello следующую информацию:
* идентификатор клиента (например, contoso.onmicrosoft.com);
* имя политики (например, B2C\_1\_SignUpIn).

Hello конечная точка маркера URI могут быть вызваны замена hello клиента\_идентификатор и политику hello\_имя в hello URL-адреса:

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

Hello конечную точку авторизации URI могут быть вызваны замена hello клиента\_идентификатор и политику hello\_имя в hello URL-адреса:

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Выполните следующий код toocreate hello объекта AuthorizationServiceConfiguration:

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Авторизация

После настройки или извлечения конфигурации службы авторизации можно сформировать запрос авторизации. запрос toocreate hello, требуется hello следующую информацию:  
* идентификатор клиента (например, 00000000-0000-0000-0000-000000000000);
* URI перенаправления с настраиваемой схемой (например, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).

Оба элемента нужно сохранить при [регистрации приложения](#create-an-application).

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

tooset копирование вашего приложения toohandle hello перенаправления toohello URI со схемой пользовательские hello список hello tooupdate «Схем URL-адрес» в необходимы вашей Info.pList.
* Откройте файл Info.pList.
* Наведите указатель на строку как «Пакет ОС типа кода» и нажмите кнопку hello \+ символов.
* Переименуйте hello новый строку «URL-адрес типы».
* Щелкните hello стрелка влево toohello дерева hello tooopen «Типы URL-адрес».
* Щелкните hello стрелка toohello слева от «0 элементов"tooopen hello дерева.
* Переименуйте первый элемент, под элемент 0 too'URL схемы.
* Щелкните hello стрелка влево toohello дерева hello tooopen «URL-схем».
* В столбце «Значение» hello, остается пустым полем toohello элемента «Элемент 0"под «URL-схем».  Задайте приложение для hello значение tooyour уникальную схему.  Hello значение должно соответствовать hello схемы, используемой в redirectURL, при создании объекта OIDAuthorizationRequest hello.  В нашем примере мы использовали схему hello «com.onmicrosoft.fabrikamb2c.exampleapp».

См. toohello [AppAuth руководство](https://openid.github.io/AppAuth-iOS/) на как toocomplete hello оставшаяся часть процедуры hello. Если вам требуется tooquickly Приступая к работе с работающем приложении, ознакомьтесь с [выборка](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Следуйте указаниям hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter конфигурацию Azure AD B2C.

Мы всегда являются предложения и откройте toofeedback! Если возникли проблемы с этим разделом, или иметь рекомендации по улучшению это содержимое, мы ценим ваши отзывы hello нижней части страницы приветствия. Для запросов, компонент, добавьте их слишком[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
