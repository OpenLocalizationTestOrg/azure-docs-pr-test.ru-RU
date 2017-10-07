---
title: "приложение Android v2.0 Active Directory aaaAzure | Документы Microsoft"
description: "Как приложение Android, выполняющий вход пользователей с личной учетной записи Майкрософт и рабочих или учебных учетных записей и вызовы toobuild hello Graph API с помощью библиотек сторонних производителей."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Добавить tooan входа в приложение Android с помощью библиотеки сторонних разработчиков с API Graph с помощью конечной точки v2.0 hello
Hello платформы удостоверений использует открытых стандартов, такие как OAuth2 и OpenID Connect. Разработчики могут использовать любую библиотеку, они должны toointegrate с наших служб. toohelp разработчики используют нашей платформы с другими библиотеками, мы написали несколько пошаговых руководств, как это один toodemonstrate как tooconfigure сторонних библиотек tooconnect toohello платформы удостоверений. Большинство библиотек, которые реализуют [spec hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) могут подключаться toohello платформы удостоверений.

С помощью приложения hello, создает в этом пошаговом руководстве пользователей можно войти в организации tootheir и выполните поиск сами в своей организации с помощью Graph API hello.

Если вы новый tooOAuth2 или OpenID Connect, большая часть конфигурации этого образца может оказаться tooyou смысле. Мы рекомендуем прочитать раздел [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md), чтобы получить соответствующие сведения.

> [!NOTE]
> Некоторые возможности платформы, имеющие выражения в hello OAuth2 или OpenID Connect стандартами, например условный доступ и управление политикой Intune, требуется вы toouse нашей открытой библиотеки удостоверений Microsoft Azure.
> 
> 

Конечная точка v2.0 Hello не поддерживает все сценарии Azure Active Directory и возможности.

> [!NOTE]
> toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-hello-code-from-github"></a>Загрузка кода hello из GitHub
поддерживается Hello кода для этого учебника [на GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).  можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) или основу hello клона:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

Можно также просто загрузить образец hello и начать работу прямо сейчас.

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>регистрация приложения;
Создание нового приложения в hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните hello подробное описание действий по [как tooregister приложения с конечной точкой v2.0 hello](active-directory-v2-app-registration.md).  Не забудьте:

* Копировать hello **идентификатор приложения** это назначенные tooyour приложения, так как он понадобится скоро.
* Добавить hello **Mobile** платформы для приложения.

> Примечание: предоставляет портал регистрации приложения hello **URI перенаправления** значение. Однако в этом примере необходимо использовать значение по умолчанию hello `https://login.microsoftonline.com/common/oauth2/nativeclient`.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Загрузить библиотеки стороннего NXOAuth2 hello и создание рабочей области
В этом пошаговом руководстве будет использоваться hello OIDCAndroidLib из GitHub, который является библиотекой OAuth2 основании hello код Google OpenID Connect. Он реализует профиля собственное приложение hello и поддерживает конечную точку авторизации hello hello пользователя. Это все, что hello потребуется toointegrate с платформой удостоверений Microsoft hello.

Клонирование репозитория tooyour hello OIDCAndroidLib компьютера.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Настройка среды Android Studio
1. Создайте новый проект Android Studio и примите значения по умолчанию hello в мастере hello.
   
    ![Создание нового проекта в Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Целевые устройства Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Добавить действие toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset проекта модулей переместить расположение проекта toohello hello клонирования репозитория. Можно также создать проект hello и клонируйте его непосредственно toohello расположение проекта.
   
    ![Модули проекта](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Откройте параметры модулей hello проекта с помощью контекстного меню hello, или с помощью клавиш Ctrl + Alt + Осно + S hello.
   
    ![Параметры модулей проекта](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Удалите модуль приложения по умолчанию hello, так как требуется только параметры проекта hello.
   
    ![Модуль приложения по умолчанию Hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Импортировать модули из hello клонированного репозитория toohello текущего проекта.
   
    ![Импорт проекта gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![создать новую страницу модуля](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Повторите эти шаги для hello `oidlib-sample` модуля.
7. Проверка зависимостей oidclib hello на hello `oidlib-sample` модуля.
   
    ![oidclib зависимости от модуля oidlib образец hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. Нажмите кнопку **ОК** и дождитесь завершения синхронизации с Gradle.
   
    Раздел settings.gradle должен выглядеть следующим образом.
   
    ![Снимок экрана settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Построение toomake пример приложения hello убедиться, что этот образец hello работает правильно.
   
    Вы не будет возможности toouse это в Azure Active Directory еще. Нам нужно tooconfigure некоторые конечные точки сначала. Это tooensure Android Studio проблем нет, прежде чем начать настройку пример приложения hello.
10. Построение и запуск `oidlib-sample` hello в качестве назначения Android Studio.
    
    ![Ход выполнения сборки oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Удалить hello `app ` каталог, была оставлена при удалении модуля hello из проекта hello, так как Android Studio не удаляет его в целях безопасности.
    
    ![Структура файлов, которая включает в себя каталог приложения hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. Откройте hello **изменение конфигураций** меню tooremove hello запустить конфигурацию, которая также была оставлена при удалении модуля hello из проекта hello.
    
    ![Меню "Изменить конфигурации"](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Конфигурация запуска приложения](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Настройка конечных точек hello образца hello
Теперь, когда имеется hello `oidlib-sample` выполняется успешно, изменим tooget некоторые конечные точки этой работы с Azure Active Directory.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>Настроить клиент путем редактирования файла oidc_clientconf.xml hello
1. Поскольку используется только tooget потоки OAuth2 маркер и вызвать hello Graph API, установите hello toodo клиента OAuth2 только. В примере, который станет доступен позже, мы будем использовать OIDC.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Настройте ИД клиента, полученный из портала регистрации hello.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. Настройте на URI перенаправления с одной hello ниже.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. Настройка областей, вы должны в порядке tooaccess hello Graph API.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

Hello `User.Read` значение в `oidc_scopes` позволяет вам tooread hello базовый профиль hello вход пользователя.
Дополнительные сведения о всех доступных областей hello в [области разрешений Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Пояснения об использовании `openid` или `offline_access` в качестве областей действия в OpenID Connect см. в разделе [Протоколы версии 2.0 — поток кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Настройте конечные точки клиента, изменив файл oidc_endpoints.xml hello
* Откройте hello `oidc_endpoints.xml` и создайте hello следующие изменения:
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

Если используется протокол OAuth2, эти конечные точки никогда не должны изменяться.

> [!NOTE]
> Здравствуйте, конечные точки для `userInfoEndpoint` и `revocationEndpoint` в настоящее время не поддерживаются в Azure Active Directory. Если оставить эти значения example.com по умолчанию hello, появится напоминание, они недоступны в образце hello :-)
> 
> 

## <a name="configure-a-graph-api-call"></a>Настройка вызова API Graph
* Откройте hello `HomeActivity.java` и создайте hello следующие изменения:
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

Здесь простой вызов API Graph возвращает нашу информацию.

Это и есть все изменения hello необходимые toodo. Запустите hello `oidlib-sample` приложения и нажмите кнопку **входа**.

После вы успешно прошли проверку подлинности, выберите hello **запроса защищенный ресурс** кнопку tootest вашей toohello вызова Graph API.

## <a name="get-security-updates-for-our-product"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем вам tooget уведомления об инцидентах безопасности, перейдя по адресу hello [Технический центр безопасности](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.

