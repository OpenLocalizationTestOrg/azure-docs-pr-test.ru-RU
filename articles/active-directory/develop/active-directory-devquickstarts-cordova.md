---
title: "Приступая к работе AD Cordova aaaAzure | Документы Microsoft"
description: "Как toobuild приложения Cordova, интегрируется с Azure AD для входа в систему и вызывает Azure API, защищенные AD с помощью OAuth."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a>Интеграция Azure AD с приложением Apache Cordova
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Можно использовать Apache Cordova toodevelop HTML5 и JavaScript приложения, работающие на мобильных устройствах, как полноценные собственного приложения. В Azure Active Directory (Azure AD) можно добавить приложений Cordova tooyour возможности проверки подлинности корпоративного уровня.

Подключаемый модуль Cordova использует собственные пакеты SDK Azure AD для приложений iOS, Android, Магазина Windows и Windows Phone. С помощью подключаемого модуля, можно усилить приложения toosupport вход в систему с учетными записями пользователей Windows Server Active Directory, получить доступ tooOffice 365 и API-интерфейсов Azure и даже защитить вызовы tooyour собственные пользовательские веб-API.

В этом учебнике мы будем использовать hello подключаемых модулей Apache Cordova для библиотеки проверки подлинности Active Directory (ADAL) tooimprove простое приложение, добавив hello следующие атрибуты:

* реализация проверки подлинности пользователя и получения маркера путем добавления всего нескольких строк кода;
* Использовать этот токен tooinvoke hello Graph API tooquery этого каталога и отображения результатов hello.  
* Проверка подлинности toominimize ADAL кэша маркера hello запрашивает пользователя hello.

toomake этих усовершенствований, необходимо:

1. зарегистрировать приложение в Azure AD;
2. Добавьте код tooyour приложения toorequest маркеры.
3. Добавление токена hello toouse код для выполнения запросов к Graph API hello и отображения результатов.
4. Создать проект развертывания hello Cordova со всех платформ hello требуется tootarget, добавить hello Cordova ADAL подключаемого модуля и тестирование решения hello в эмуляторах.

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника, необходимо:

* Клиент Azure AD с учетной записью с правами на разработку приложений.
* Среда разработки, которая настроена toouse Apache Cordova.  

Если оба уже установлено, перейдите непосредственно toostep 1.

Если у вас нет клиента Azure AD, используйте hello [инструкции tooget один](active-directory-howto-tenant.md).

Если у вас нет Apache Cordova на компьютере, установите hello следующее:

* [Git.](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org/download/)
* [Cordova CLI](https://cordova.apache.org/) (можно легко установить через диспетчер пакетов NPM: `npm install -g cordova`).

Hello предыдущих установок должен работать на hello ПК и hello Mac.

У каждой целевой платформы свои требования.

* toobuild и запуска приложения для Планшетных Windows или Windows Phone:
  * Установите [Visual Studio 2013 для Windows с обновлением 2 или более поздней версии](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express или другая версия) или [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).

* toobuild и запустите приложение для iOS:

  * Установите Xcode 6.x или более поздней версии. Загрузите его из hello [сайта разработчика Apple](http://developer.apple.com/downloads) или hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).
  * Установите [ios-sim](https://www.npmjs.org/package/ios-sim). Он используется toostart приложений iOS в симуляторе iOS с hello командной строки. (Его можно легко установить через hello терминалов: `npm install -g ios-sim`.)
* toobuild и запуска приложения для Android:

  * Установить [пакет средств разработки Java (JDK) версии 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) или более поздней. Убедитесь, что `JAVA_HOME` (переменной среды) правильно установлен в соответствии с путь установки JDK toohello (например, C:\Program Files\Java\jdk1.7.0_75).
  * Установка [пакета SDK для Android](http://developer.android.com/sdk/installing/index.html?pkg=tools) и добавить hello `<android-sdk-location>\tools` tooyour расположение (например, C:\tools\Android\android-sdk\tools) `PATH` переменной среды.
  * Откройте диспетчер Android SDK Manager (например, через hello терминалов: `android`) и установить:
    * *Android 5.0.1 (API уровня 21)* ;
    * *Android SDK Build Tools* версии 19.1.0 или более поздней;
    * *Android Support Repository* (дополнительно).

  любой экземпляр эмулятора по умолчанию не предоставляет возможность Hello пакета SDK для Android. Сделать это с `android avd` из hello терминалов и затем выбрав **создать**, если требуется, чтобы приложение Android toorun hello в эмуляторе. Рекомендуемый уровень API — 19 или выше. Дополнительные сведения о hello Android эмулятора и параметрами создания см. в разделе [диспетчер AVD](http://developer.android.com/tools/help/avd-manager.html) на сайте Android hello.

## <a name="step-1-register-an-application-with-azure-ad"></a>Шаг 1. Регистрация приложения в Azure AD
Этот шаг не является обязательным. Этот учебник предоставляет предварительную подготовку значения, которые можно использовать toosee образец hello без выполнения любой инициализации своим собственным клиентом. Тем не менее рекомендуется выполнить этот шаг и ближе познакомиться с hello процесса, так как он понадобится, при создании собственных приложений.

Azure AD выдает токены tooonly известные приложений. Прежде чем использовать Azure AD из приложения, необходимо toocreate запись для него в клиенте. tooregister новое приложение в клиенте:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello выберите свою учетную запись. В hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.
3. Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.
5. Следуйте инструкциям hello и создать **собственное клиентское приложение**. (Хотя приложения Cordova основаны на HTML, мы создаем собственное клиентское приложение. Hello **собственное клиентское приложение** должен быть выбран вариант, или не будет работать приложение hello.)
  * **Имя** описывает toousers вашего приложения.
  * **URI перенаправления** — hello URI, который использовал tooreturn маркеры tooyour приложения. Введите **http://MyDirectorySearcherApp**.

После завершения регистрации Azure AD присваивает значение приложении tooyour приложения уникальный идентификатор. Вам потребуется это значение в последующих разделах hello. Его можно найти на вкладке приложения hello созданного приложения hello.

toorun `DirSearchClient Sample`, предоставьте hello hello созданного приложения разрешение tooquery API Azure AD Graph:

1. Из hello **параметры** выберите **требуемые разрешения**, а затем выберите **добавить**.  
2. Hello приложения Azure Active Directory, выберите **Microsoft Graph** как hello API и добавьте hello **доступ к каталогу hello как пользователя, выполнившего вход hello** разрешение в списке **полномочные Разрешения**.  Это позволяет вашей hello tooquery приложения Graph API для пользователей.

## <a name="step-2-clone-hello-sample-app-repository"></a>Шаг 2: Клонирование репозитория приложения образец hello
Оболочки или командной строки введите следующую команду hello:

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a>Шаг 3: Создание приложения Cordova hello
Существует несколько способов toocreate Cordova приложения. В этом учебнике мы будем использовать hello Cordova интерфейс командной строки (CLI).

1. Оболочки или командной строки введите следующую команду hello:

        cordova create DirSearchClient

   Эта команда создает структуру папок hello и формирование шаблонов для проекта Cordova hello.

2. Переместите новую папку DirSearchClient toohello:

        cd .\DirSearchClient

3. Скопируйте содержимое hello hello начального проекта во вложенной папке hello www с помощью диспетчера файлов или следующую команду в оболочка hello:

  * Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`
  * Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`

4. Добавьте белого списка hello подключаемого модуля. Это требуется для вызова Graph API hello.

        cordova plugin add cordova-plugin-whitelist

5. Добавьте все платформы hello, что требуется toosupport. toohave рабочий образец, необходимо tooexecute по крайней мере один из следующих команд hello. Обратите внимание, что не быть может tooemulate iOS в Windows или эмулировать Windows на компьютере Mac.

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. Добавьте hello ADAL для проекта tooyour подключаемого модуля Cordova:

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a>Шаг 4: Добавление кода tooauthenticate пользователей и получать токены из Azure AD
приложение Hello, которое вы разрабатываете в этом учебнике будет предоставляют возможность поиска каталог с простым. Hello пользователя можно введите псевдоним hello любого пользователя в каталоге hello и визуализировать некоторые основные атрибуты. Hello начальный проект содержит определение hello hello основной пользовательский интерфейс приложения hello (в www/index.html) и формирование шаблонов hello, настраивающий событий базовое приложение циклов привязки интерфейса пользователя и результаты логики отображения (в www/js/index.js). Hello только слева для вас останется tooadd hello логику, которая реализует идентификаторов задач.

Hello прежде всего необходимо toodo в коде является вводит значения протокола hello, используемые для идентификации приложения Azure AD и hello ресурсы, предназначенные. Эти значения будут запросы маркеров используется tooconstruct hello позже. Вставьте следующий фрагмент кода hello верхней части файла index.js hello hello:

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

Hello `redirectUri` и `clientId` значения должны совпадать hello значения, которые описывают приложение в Azure AD. Можно найти соответствующие hello **Настройка** вкладке hello портал Azure, как описано в шаге 1 ранее в этом учебнике.

> [!NOTE]
> Если вы выбрали для вашего собственного клиента не Регистрация нового приложения, можно просто вставить hello заранее настроенные значения как есть. Можно просматривать выполняется образец hello, хотя рекомендуется всегда создавать записи для приложения, предназначенные для рабочей среды.

Добавьте код запроса маркера hello. Вставьте следующий фрагмент кода между hello hello `search` и `renderData` определения:

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
Рассмотрим эту функцию, разбив ее на две основные части.
В этом примере является спроектированный toowork с любым клиентом как противоположность toobeing привязан tooa одну из них. Она использует hello конечную «/ Общие», которая позволяет любой учетной записи пользователя tooenter hello во время проверки подлинности и направляет клиента toohello hello запроса, к которой он принадлежит.

Эта часть hello метод проверяет toosee кэш ADAL hello, если токен уже хранится. В этом случае hello способе клиентов hello токен hello происхождения для повторной инициализации ADAL. Это — tooavoid необходимые дополнительные запросы, поскольку использование hello объекта «/ общие» всегда приводит попросить пользователя tooenter hello новую учетную запись.

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
во второй части Hello hello метод выполняет hello правильный запрос маркера. Hello `acquireTokenSilentAsync` метод запрашивает ADAL tooreturn маркер hello указанного ресурса без отображения любой UI. Что может произойти, если hello кэша уже есть подходящий описателя хранения, или если токен обновления можно использовать tooget новый маркер доступа без отображения предупреждений. В случае неудачной попытки, мы прибегнуть к `acquireTokenAsync`--наглядно будет предложено hello tooauthenticate пользователя.

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
Теперь, когда у нас есть токен hello, мы наконец вызова Graph API hello и hello поискового запроса, который необходимо выполнить. Вставьте следующий фрагмент кода ниже hello hello `authenticate` определение:

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
файлы начального приветствия предоставлен простой UX для ввода псевдонима пользователя в текстовом поле. Этот метод используется, значение tooconstruct запрос, использовать ее в сочетании с маркером доступа hello, отправить его tooMicrosoft Graph и проанализировать результаты hello. Hello `renderData` берет на себя метод, уже присутствует в файле начального приветствия, наглядно представить результаты hello.

## <a name="step-5-run-hello-app"></a>Шаг 5: Запуск приложения hello
Приложение будет toorun все готово. Его работы является простым: при запуске приложение hello, введите псевдоним hello hello пользователя необходимо toolook, а затем нажмите кнопку hello. Будет предложено ввести учетные данные для проверки подлинности. После успешной проверки подлинности и успешного поиска отображаются атрибуты hello hello поиск пользователя.

Последующие запуски выполнит поиск hello без отображения предупреждений, благодаря использованию toohello наличие hello ранее получены маркера в кэше.

Hello конкретные действия для запуска приложения hello зависят от платформы.

### <a name="windows-10"></a>Windows 10
   Планшет или ПК: `cordova run windows --archs=x64 -- --appx=uap`

   Мобильных устройств (требуется tooa подключенное устройство Windows 10 Mobile PC):`cordova run windows --archs=arm -- --appx=uap --phone`

   > [!NOTE]
   > Во время первого запуска hello вас попросят toosign в лицензию разработчика. Дополнительные сведения см. в статье [Получение лицензии разработчика](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-81-tabletpc"></a>Планшеты или компьютеры с Windows 8.1
   `cordova run windows`

   > [!NOTE]
   > Во время первого запуска hello вас попросят toosign в лицензию разработчика. Дополнительные сведения см. в статье [Получение лицензии разработчика](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).

### <a name="windows-phone-81"></a>Windows Phone 8.1
   toorun на подключенном устройстве:`cordova run windows --device -- --phone`

   toorun на эмулятор по умолчанию hello:`cordova emulate windows -- --phone`

   Используйте `cordova run windows --list -- --phone` toosee все доступные целевые объекты и `cordova run windows --target=<target_name> -- --phone` toorun приложения hello на конкретном устройстве или эмуляторе (например, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).

### <a name="android"></a>Android
   toorun на подключенном устройстве:`cordova run android --device`

   toorun на эмулятор по умолчанию hello:`cordova emulate android`

   Убедитесь, что вы создали экземпляр эмулятор из диспетчера AVD, как описано ранее в подразделе «Необходимые условия» hello.

   Используйте `cordova run android --list` toosee все доступные целевые объекты и `cordova run android --target=<target_name>` toorun приложения hello на конкретном устройстве или эмуляторе (например, `cordova run android --target="Nexus4_emulator"`).

### <a name="ios"></a>iOS
   toorun на подключенном устройстве:`cordova run ios --device`

   toorun на эмулятор по умолчанию hello:`cordova emulate ios`

   > [!NOTE]
   > Убедитесь, что у вас есть hello `ios-sim` toorun установлен пакет на эмуляторе hello. Дополнительные сведения см. в разделе hello «необходимые условия» раздела.

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a>Дальнейшие действия
Для ссылки, пример hello завершена (без настройки) доступен в [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).

Вы можете теперь сценарии перемещения на toomore advanced (и другие интересные). Может потребоваться tootry: [защитить веб-API Node.js в Azure AD](active-directory-devquickstarts-webapi-nodejs.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
