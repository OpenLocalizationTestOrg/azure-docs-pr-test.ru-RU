---
title: "Приступая к работе AD Android aaaAzure | Документы Microsoft"
description: "Как toobuild приложение Android, которое интегрируется с Azure AD для входа в систему и вызовы Azure AD защищены API-интерфейсов с помощью OAuth."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a>Интеграция Azure AD в приложение для Android
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Испытать предварительную версию hello нашим новым [портал разработчиков](https://identity.microsoft.com/Docs/Android), который поможет вам приступить к работе с Azure AD через несколько минут. портал разработчиков Hello поможет hello процесса регистрации приложения и интеграции Azure AD в коде. Завершив работу, вы получите простое приложение, с помощью которого выполняется проверка подлинности пользователей в клиенте и на сервере, принимающем маркеры и проводящем проверку.
>
>

При разработке настольного приложения, Azure Active Directory (Azure AD) упрощает простыми и понятными для вас tooauthenticate пользователей с помощью своих локальных учетных записей Active Directory. Toosecurely вашего приложения также позволяет использовать любой веб-API, защищенные Azure AD, таких как hello API Office 365 или hello Azure API.

Для Android клиентов, которые нужно tooaccess защищенных ресурсов Azure AD предоставляет hello библиотеку проверки подлинности Active Directory (ADAL). Цель Hello ADAL — toomake легко и маркеры доступа tooget вашего приложения. Это, мы создадим приложение Android список дел, насколько просто toodemonstrate:

* Получает маркеры для вызова API списка задач с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* получает список дел пользователя;
* выполняет выход из системы для пользователей.

tooget к работе, потребуется клиент Azure AD, в котором можно создавать пользователей и зарегистрировать приложение. Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a>Шаг 1: Загрузите и запустите сервер образец hello Node.js REST API TODO
Образец Hello Node.js REST API TODO написан специально toowork с существующие выборка для создания задачи REST API одного клиента для Azure AD. Это является необходимым условием для hello быстрого запуска.

Сведения о как tooset это, просмотреть наши примеры, существующие в [Microsoft службы Azure Active Directory образец REST API для Node.js](active-directory-devquickstarts-webapi-nodejs.md).


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a>Этап 2. Регистрация веб-API с помощью клиента Azure AD
Служба каталогов Active Directory позволяет добавлять приложения двух типов:

- Веб-API, которые предоставляют службы toousers
- Запущенное (на веб-hello или на устройстве), открыть веб-API

На этом шаге регистрация hello веб-API, у вас локально для тестирования этого образца. Как правило этот веб-API — службы REST, функциональные возможности предложения, которые должны tooaccess приложения. Azure AD может помочь защитить любую конечную точку.

Мы при условии, что регистрации hello вышеупомянутым API REST TODO. Но это применимо к любой веб-API, необходимо защитить toohelp Azure Active Directory.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello выберите свою учетную запись. В hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.
3. Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.
5. Введите понятное имя для приложения hello (например, **TodoListService**), выберите **веб-приложение или веб-API**и нажмите кнопку **Далее**.
6. Образец hello hello входа URL-адрес, введите базовый URL-адрес hello. По умолчанию это `https://localhost:8080`.
7. Нажмите кнопку **ОК** toocomplete hello регистрации.
8. Во время по-прежнему hello портал Azure, переход на страницу приложения tooyour, найдите значение идентификатора приложения hello и скопируйте его. Оно понадобится позже при настройке приложения.
9. Из hello **параметры** -> **свойства** страницы, обновите URI идентификатора приложения hello - введите `https://<your_tenant_name>/TodoListService`. Замените `<your_tenant_name>` с именем hello вашего клиента Azure AD.

## <a name="step-3-register-hello-sample-android-native-client-application"></a>Шаг 3: Регистрация приложения Android Native Client образец hello
В этом примере необходимо зарегистрировать веб-приложение. Это позволяет toocommunicate вашего приложения с только что зарегистрированные веб-hello API. Azure AD будет отказывать в приеме tooeven разрешить tooask вашего приложения для входа в систему, когда он зарегистрирован. Который является частью безопасности hello hello модели.

Мы при условии, что регистрации пример приложения hello, ссылка на более ранних версий. Но эта процедура подходит для любого приложения, которое вы разрабатываете.

> [!NOTE]
> Может возникнуть вопрос, почему приложение и веб-интерфейс API размещаются в одном клиенте? Как вы могли догадаться, можно создать приложение, которое обращается к внешнему интерфейсу API, зарегистрированному в Azure AD из другого клиента. Если это сделать, клиентам будет предложено использование toohello tooconsent hello API приложения hello. Библиотека проверки подлинности Active Directory для iOS выполняет все необходимые операции для обработки данного согласия. Мы исследуем дополнительных функций, вы увидите, что это является важной частью работы hello необходимые tooaccess набор hello интерфейсы API Microsoft Azure и Office, а также любой другой поставщик службы. Сейчас, так как вы зарегистрировали веб-API и тестируемое приложение hello же клиента, вы не увидите каких-либо запросов согласия. Это обычно hello вариант, если вы разрабатываете приложения только для собственных toouse компании.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello выберите свою учетную запись. В hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.
3. Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.
5. Введите понятное имя для приложения hello (например, **TodoListClient Android**), выберите **собственное клиентское приложение**и нажмите кнопку **Далее**.
6. URI перенаправления hello, введите `http://TodoListClient`. Нажмите кнопку **Готово**
7. Страница "приложение" hello найти значение идентификатора приложения hello и скопируйте его. Оно понадобится позже при настройке приложения.
8. Из hello **параметры** выберите **требуемые разрешения** и выберите **добавить**.  Найдите и выберите TodoListService, добавьте hello **TodoListService доступа** разрешение в списке **делегированные разрешения**и нажмите кнопку **сделать**.

pom.xml toobuild с Maven, можно использовать на верхнем уровне hello.

1. Клонируйте этот репозиторий в любой каталог по своему усмотрению:

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. Следуйте указаниям hello hello [tooset необходимых компонентов, настройку среды Maven для Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).
3. Настройте эмулятор hello с SDK 19.
4. Go toohello корневую папку, где клонирования репозитория hello.
5. Выполните следующую команду: `mvn clean install`
6. Изменение образца hello каталог toohello быстрого запуска.`cd samples\hello`
7. Выполните следующую команду: `mvn android:deploy android:run`

   Вы увидите запуск приложения hello.
8. Введите tootry учетные данные тестового пользователя.

Будут отправлены пакеты JAR рядом с hello AAR пакета.

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a>Шаг 4: Загрузите hello Android ADAL и добавить его в рабочей области Eclipse tooyour
Мы упрощенной для вас toohave несколько параметров toouse ADAL в проекте Android:

* Можно использовать эту библиотеку hello исходного кода tooimport в Eclipse и связать приложение tooyour.
* Если вы используете Android Studio, можно использовать hello AAR пакета формат и ссылка hello двоичных файлов.

### <a name="option-1-source-zip"></a>Способ 1: ZIP-архив с файлами исходного кода
Щелкните toodownload копию исходного кода hello, **загрузить ZIP** hello правой части страницы приветствия. Или [скачайте его с GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).

### <a name="option-2-source-via-git"></a>Способ 2: исходные файлы через Git
исходный код hello tooget hello пакет SDK через Git, введите следующую команду:

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a>Способ 3: двоичные файлы через Gradle
Двоичные файлы hello можно получить из центрального репозитория hello Maven. Hello AAR пакета могут быть включены в проект в Android Studio следующим образом:

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a>Способ 4: AAR через Maven
Если вы используете hello M2Eclipse подключаемый модуль, можно указать hello зависимостей в файле pom.xml:

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a>Параметр 5: Пакет JAR-ФАЙЛ в папке библиотеки hello
Можно получить из репозитория Maven hello hello JAR-файл и вставьте его в hello **библиотеки** в папке проекта. Необходимо toocopy hello необходимые ресурсы tooyour проекта, так как пакеты JAR hello не включайте их.

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a>Шаг 5: Добавление ссылки на tooAndroid ADAL tooyour проекта
1. Добавьте проект tooyour ссылки и указать его как библиотека Android. Если вы уверены как toodo это, можно получить дополнительные сведения о hello [Android Studio сайта](http://developer.android.com/tools/projects/projects-eclipse.html).
2. Добавьте hello зависимостей проекта для отладки в параметрах проекта.
3. Обновление tooinclude файла AndroidManifest.xml проекта:

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. Создайте экземпляр класса AuthenticationContext с вашим MainActivity. Hello сведения данного вызова выходят за рамки этого раздела hello, но достаточно начать можно получить, просмотрев hello [Android Native Client образец](https://github.com/AzureADSamples/NativeClient-Android). В следующем примере hello, SharedPreferences hello кэша по умолчанию, который центр в форме hello `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. Скопируйте этот код блока toohandle hello конец AuthenticationActivity после hello пользователь вводит учетные данные и получает код авторизации:

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. tooask к маркеру, определите обратный вызов.

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. Наконец, запросите маркер с помощью данного обратного вызова:

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

Ниже приведено описание параметров hello.

* *ресурс* является обязательным и находится hello ресурса, которому вы пытаетесь tooaccess.
* Параметр *clientId* является обязательным и поступает из Azure AD.
* *RedirectUri* не требуется toobe, предоставленные для вызова acquireToken hello. В качестве него можно задать имя пакета.
* *PromptBehavior* помогает tooask для кэша hello tooskip учетные данные и файлы cookie.
* *обратный вызов* вызывается после того, обмен которыми осуществляется hello код авторизации для маркера. Он получает объект AuthenticationResult, который имеет маркер доступа, дату окончания срока действия и сведения об идентификаторе маркера.
* Параметр *acquireTokenSilent* является необязательным. Его можно вызвать toohandle кэширование и обновление токена. Он также предоставляет версию sync hello. Он принимает *userid* в качестве параметра.

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

Используя в данном пошаговом руководстве, необходимо иметь какой требуется toosuccessfully интеграции с Azure Active Directory. Дополнительные примеры этой работы, посетите hello AzureADSamples / репозитория в GitHub.

## <a name="important-information"></a>Важные сведения
### <a name="customization"></a>Настройка
Ресурсы проекта библиотеки могут быть перезаписаны ресурсами вашего приложения. Перезапись происходит при сборке приложения. По этой причине можно настроить проверку подлинности действия макета hello должным образом. Быть убедиться, что идентификатор hello tookeep hello элементов управления, ADAL использует (WebView).

### <a name="broker"></a>Broker
приложение корпоративного портала Microsoft Hello предоставляет компонента broker hello. Hello учетная запись создается в AccountManager. Тип учетной записи Hello является «com.microsoft.workaccount». Диспетчер учетных записей разрешает только одну учетную запись единого входа. Он создает файл cookie единого входа для пользователя hello после завершения запроса hello устройств для одного приложения hello.

ADAL использует учетную запись broker hello, если одна учетная запись создается в данной структуры проверки подлинности и выборе не tooskip его. Вы можете пропустить hello broker пользователя с:

   `AuthenticationSettings.Instance.setSkipBroker(true);`

Для использования посредника должны tooregister специальные RedirectUri. RedirectUri указано в формате hello `msauth://packagename/Base64UrlencodedSignature`. Можно получить ваш RedirectUri для приложения с помощью сценария brokerRedirectPrint.ps1 hello или mContext.getBrokerRedirectUri вызов hello API. Сигнатура Hello — связанные tooyour сертификаты подписи.

Текущая модель broker Hello — для одного пользователя. AuthenticationContext предоставляет hello API метод tooget hello broker пользователя.

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

Манифест приложения должен иметь следующие разрешения toouse AccountManager счетов hello. Дополнительные сведения см. в разделе hello [AccountManager сведения на сайте Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).

* GET_ACCOUNTS
* USE_CREDENTIALS
* MANAGE_ACCOUNTS

### <a name="authority-url-and-ad-fs"></a>URL-адрес центра и службы федерации Active Directory
Служб федерации Active Directory (AD FS) не распознается как производственной службе маркеров безопасности, поэтому требуется tooturn обнаружения экземпляра и передайте значение false в конструктор AuthenticationContext hello.

URL-адрес центра Hello требуется экземпляр службы маркеров безопасности и [имя клиента](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).

### <a name="querying-cache-items"></a>Запрос элементов кэша
Библиотека ADAL предоставляет кэш по умолчанию в SharedPrefrecens и несколько простых функций для запроса данных из кэша. Можно получить текущий кэш hello из AuthenticationContext с помощью:

    ITokenCacheStore cache = mContext.getCache();

Можно также предоставить реализации кэша, если требуется, чтобы toocustomize его.

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a>Поведения запроса
ADAL является поведения запроса toospecify параметр. PromptBehavior.Auto покажет hello пользовательского интерфейса, если hello токен обновления является недопустимым, и требуются учетные данные пользователя. PromptBehavior.Always пропустит использование кэша hello и всегда показывать hello пользовательского интерфейса.

### <a name="silent-token-request-from-cache-and-refresh"></a>Автоматический запрос маркера из кэша и обновление
Запрос маркера автоматической не использует hello всплывающих пользовательского интерфейса и не требует действия. Он возвращает маркер из кэша hello, если он доступен. Если истек срок действия маркера hello, этот метод пытается toorefresh его. Если сбой или просроченный маркер обновления hello, он возвращает AuthenticationException.

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

Также данный метод обеспечивает возможность выполнить синхронный вызов. Можно задать значение null toocallback или использовать acquireTokenSilentSync.

### <a name="diagnostics"></a>Диагностика
Это hello основными источниками информации для диагностики проблем.

* Исключения
* Журналы
* Данные трассировки сети

Обратите внимание, что идентификаторы корреляции toohello центра диагностики в библиотеке hello. При желании toocorrelate ADAL запроса с другими операциями, в коде, можно задать вашей идентификаторов корреляции для каждого запроса. Если идентификатор корреляции не задан, то библиотека ADAL создает случайный идентификатор. Все журнала сообщений и затем сетевые вызовы будут помечены с идентификатором hello корреляции. Hello самостоятельно сформированный изменения идентификатора для каждого запроса.

#### <a name="exceptions"></a>Исключения
Исключениями являются hello сначала диагностики. Мы пытаемся tooprovide полезные сообщения об ошибках. Если вы не считаете какое-либо сообщение содержательным, пожалуйста, сообщите нам об этом. Укажите такие сведения об устройстве, как модель и версия SDK.

#### <a name="logs"></a>Журналы
Можно настроить toogenerate библиотеки hello сообщений журнала, которые можно использовать toohelp диагностировать проблемы. Настройка ведения журнала, делая hello следующий вызов tooconfigure обратный вызов, ADAL будет использовать toohand off каждое сообщение журнала, как оно генерируется.

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

Сообщения могут записываться tooa пользовательский файл журнала, как показано в следующим hello. К сожалению, нет стандартного способа получения журналов с устройств. Существуют некоторые службы, которые могут в этом помочь. Можно также придумать собственный, например, отправляющий сервер tooa файл hello.

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

Существуют следующие уровни ведения журнала hello:
* Error (исключение);
* Warn (предупреждение);
* Info (информирование);
* Verbose (дополнительные сведения).

Можно установить уровень журнала hello следующим образом:

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 Все сообщения журнала отправляются toologcat, в обратных вызовах, добавление tooany пользовательского журнала.
Файл журнала tooa из logcat можно получить следующим образом:

    adb logcat > "C:\logmsg\logfile.txt"

 Дополнительные сведения о командах adb см. в разделе hello [logcat сведения на сайте Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).

#### <a name="network-traces"></a>Данные трассировки сети
Можно использовать различные средства toocapture hello трафик HTTP, приводит к возникновению ошибки ADAL.  Это может пригодиться, если вы знакомы с hello протокола OAuth или при необходимости tooMicrosoft tooprovide диагностической информации или по другим каналам поддержки.

Fiddler — hello удобное средство трассировки HTTP. Используйте hello следующие ссылки tooset его запись toocorrectly ADAL сетевого трафика. Для средства трассировки как Fiddler или Чарльз toobe полезно необходимо настроить его трафика toorecord без шифрования SSL.  

> [!NOTE]
> Данные трассировки, записанные таким образом, могут содержать конфиденциальные сведения, такие как маркеры доступа, имена пользователей и пароли. При использовании рабочих учетных записей не передавайте данные трассировки третьим сторонам. При необходимости toosupply toosomeone трассировки в порядке tooget поддержки воспроизвести проблему hello, используя временную учетную запись с имена пользователей и пароли, не столь важно для управления доступом.

* С веб-сайта Telerik hello: [параметр вверх Fiddler для Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)
* Использование GitHub : [Настройка правил Fiddler для библиотеки ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)

### <a name="dialog-mode"></a>Режим диалогового окна
метод acquireToken Hello без действий поддерживает строки диалогового окна.

### <a name="encryption"></a>Шифрование
ADAL шифрует токены hello и хранилища в SharedPreferences по умолчанию. Можно просмотреть сведения о классе toosee hello StorageHelper hello. В Android 4.3 (API уровня 18) введено безопасное хранилище закрытых ключей AndroidKeyStore. Библиотека ADAL использует это хранилище при работе с API уровня 18 и выше. Если требуется toouse ADAL для более ранних версиях пакета SDK, необходимо tooprovide секретный ключ по AuthenticationSettings.INSTANCE.setSecretKey.

### <a name="oauth2-bearer-challenge"></a>Запрос носителя OAuth2
Hello AuthenticationParameters класс предоставляет функциональные возможности tooget authorization_uri из hello запрос OAuth2 носителя.

### <a name="session-cookies-in-webview"></a>Файлы cookie сеанса в веб-представлении
После закрытия приложения hello Android WebView не удаляет файлы cookie сеанса. Это можно сделать с помощью следующего примера кода.

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

Дополнительные сведения о файлах cookie см. в разделе hello [CookieSyncManager сведения на сайте Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).

### <a name="resource-overrides"></a>Переопределения ресурсов
Библиотека ADAL Hello включает английская строк ProgressDialog сообщений. Разработчику следует перезаписать эти сроки, если требуется их локализовать.

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a>Диалоговое окно NTLM
ADAL версии 1.1.0 поддерживает диалоговое окно с NTLM, который обработает событие onReceivedHttpAuthRequest hello из WebViewClient. Можно настроить макет hello и строки для диалоговое окно «hello».

### <a name="cross-app-sso"></a>Единый вход для нескольких приложений
Дополнительные сведения [как tooenable нескольких приложений единого входа в Android с помощью ADAL](active-directory-sso-android.md).  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
