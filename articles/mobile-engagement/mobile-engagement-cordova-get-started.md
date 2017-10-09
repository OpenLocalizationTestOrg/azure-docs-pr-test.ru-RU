---
title: "aaaGet работы с Azure Mobile Engagement для Cordova/Phonegap"
description: "Узнайте, как toouse Azure Mobile Engagement Analytics и Push-уведомления для приложений Cordova/Phonegap."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Начало работы со Службами мобильного взаимодействия Azure для Cordova (Phonegap)
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как toounderstand toouse Azure Mobile Engagement, использования и отправить push уведомления toosegmented пользователям для мобильного приложения, разработанные с помощью Cordova.

В этом учебнике вы создадим пустое приложение Cordova на компьютере Mac и интегрируем пакет SDK для Служб мобильного взаимодействия. Приложение будет собирать базовые данные аналитики и получать push-уведомления с помощью системы push-уведомлений Apple (APNS) для iOS и Google Cloud Messaging (GCM) для Android. Мы Развернем этот tooan устройстве iOS или Android для тестирования. 

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).
> 
> 

Этот учебник требует hello следующее:

* XCode, которую можно установить в магазине приложений Mac (для развертывания tooiOS)
* [Android SDK & эмулятор](http://developer.android.com/sdk/installing/index.html) (для развертывания tooAndroid)
* Сертификат push-уведомлений (P12), который можно получить в центре разработки Apple (для APNS)
* Номер проекта GCM, который можно найти в консоли разработчиков Google (для GCM)
* [Подключаемый модуль Cordova для Служб мобильного взаимодействия](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> Можно найти исходного кода hello и hello ReadMe для подключаемого модуля Cordova hello на [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme">
            </a>Настройка Служб мобильного взаимодействия для приложения Cordova
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции» hello минимальный набор данных требуется toocollect и отправить push-уведомление. 

Мы создадим простое приложение с интеграцией hello toodemonstrate Cordova:

### <a name="create-a-new-cordova-project"></a>Создание нового проекта Cordova
1. Запустите *терминалов* окна на ваш Mac компьютера и типа hello после которого будет создан новый проект Cordova с помощью шаблона по умолчанию hello. Убедитесь, что публикация hello профиля вы со временем toodeploy используйте приложение iOS использует «com.mycompany.myapp» как hello идентификатор приложения. 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. Выполните следующие tooconfigure hello проекта для **iOS** и запустите его в симуляторе iOS hello:
   
        $ cordova platform add ios 
        $ cordova run ios
3. Выполните следующие tooconfigure hello проекта для **Android** и запустите его в эмуляторе Android hello. Убедитесь, что параметры эмулятора Android SDK своей цели как Google API-интерфейсы (Google Inc.) с ЦП hello / ABI как Google API-интерфейсы ARM.  
   
        $ cordova platform add android
        $ cordova run android
4. Добавьте подключаемый модуль Cordova Console hello. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Подключение Engagement tooMobile внутренний сервер приложений
1. Установите подключаемый модуль Azure Mobile Engagement Cordova hello в то же время предоставляя значения переменных tooconfigure hello hello-подключаемого модуля:
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Значок Android достичь* : должно быть именем hello hello ресурса не все расширения, а также drawable префикс (ex: mynotificationicon), и файл значка hello должны быть скопированы в проекте android (платформы/android/res/drawable)

*iOS достичь значок* : должно быть именем hello hello ресурсов без расширения (пример: mynotificationicon.png), и файл значка hello должен быть добавлен в проект iOS с XCode (с помощью меню Добавить файлы hello)

## <a id="monitor"></a>Включение мониторинга в реальном времени
1. В проект Cordova hello — изменить **www/js/index.js** toodeclare Engagement tooMobile нового действия один раз hello вызовов hello tooadd *deviceReady* полученных событий.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Запустите приложение hello:
   
   * **Для iOS:**
     
       В `Terminal` окна запуска приложения в новом экземпляре симулятора, выполнив следующие hello:
     
           cordova run ios
   * **Для Android:**
     
       В `Terminal` окна запуска приложения в новом экземпляре эмулятора, выполнив следующие hello:
     
           cordova run android
3. Вы можете увидеть следующее hello в журналах hello консоли:
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Включение функции отправки и приема push-уведомлений и обмена сообщениями в приложении
Mobile Engagement позволяет toointeract с пользователями с помощью Push-уведомления и сообщения в контексте hello кампаний в приложения. Этот модуль вызывается REACH на портале мобильного охвата hello.
Hello ниже настроит вашего приложения tooreceive их.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Настройка учетных данных для отправки push-уведомлений из Служб мобильного взаимодействия
tooallow мобильного охвата toosend Push-уведомления от вашего имени, необходимо его доступ к tooyour Apple iOS сертификат или ключ API GCM сервера toogrant. 

1. Перейдите tooyour порталу мобильного охвата. Убедитесь в приложение hello мы используем для этого проекта и выберите команду hello **Владейте** кнопку в нижней части hello:
   
    ![][1]
2. На странице параметров hello будут перемещаться в портал обязательств. Из отсутствует щелкните hello **системные Push-уведомления** раздела:
   
    ![][2]
3. Настройте сертификат Apple iOS или ключ API сервера GCM.
   
    **[iOS]**
   
    а. Выберите сертификат P12, загрузите его и введите пароль:
   
    ![][3]
   
    **[Android]**
   
    а. Щелкните значок редактирования hello перед **ключ API** в раздел параметров GCM hello во всплывающем hello, который отображается, hello GCM ключа сервера и нажмите кнопку **ОК**. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Включить push-уведомления в приложение Cordova hello
Изменить **www/js/index.js** tooadd hello вызовов tooMobile Engagement toorequest push-уведомления и объявить обработчик:

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Выполните приложение hello
**[iOS]**

1. Мы будет использовать XCode toobuild и развернуть приложение hello на устройстве tootest hello push-уведомлений, поскольку iOS только позволяет принудительные уведомления tooan само устройство. Go toohello расположение, где создается проекта Cordova и перейдите в слишком**...\platforms\ios** расположение. Откройте hello собственного xcodeproj-файл в XCode. 
2. Построение и развертывание hello Cordova приложения toohello устройствами iOS hello учетную запись, имеющую hello подготовительный профиль, содержащий только что переданный порталу мобильного охвата toohello и hello идентификатор приложения, который соответствует hello, который был предоставлен при создании сертификатов hello приложение Hello Cordova. Можно извлечь hello *идентификатор пакета* в ваш **ресурсов\*-info.plist** файл в XCode toomatch ее вверх. 
3. Вы увидите всплывающее hello стандартных операций ввода-вывода на устройстве, о том, что приложение hello запросов на разрешение toosend уведомления. Разрешение "hello". 

**[Android]**

Можно просто использовать Android приложение hello toorun hello эмулятора, как уведомления GCM, поддерживаются в эмуляторе Android hello. 

    cordova run android

## <a id="send"></a>Отправить уведомление о tooyour приложение
Теперь мы создадим простой кампании Push-уведомлений, будет отправить приложение tooyour push, запущенного на устройстве hello:

1. Перейдите toohello **достичь** вкладка на портале мобильного охвата
2. Нажмите кнопку **новое извещение** toocreate кампании push-уведомлений
   
    ![][6]
3. Предоставить входные данные toocreate кампанию **[Android]**
   
   * Задайте **имя** кампании. 
   * Выберите hello **тип доставки** как *Системное уведомление* *простой*
   * Выберите hello **время доставки** как *«Any времени»*
   * Укажите **заголовок** для уведомления будет первая строка hello в отправке hello.
   * Укажите **сообщение** для вашей уведомление, которое будет использоваться в качестве текста сообщения hello. 
     
     ![][11]
4. Предоставить входные данные toocreate кампанию **[iOS]**
   
   * Задайте **имя** кампании. 
   * Выберите hello **время доставки** как *«только вне приложения»*
   * Укажите **заголовок** для уведомления будет первая строка hello в отправке hello.
   * Укажите **сообщение** для вашей уведомление, которое будет использоваться в качестве текста сообщения hello. 
     
     ![][12]
5. Прокрутите вниз и выберите раздел содержимого hello **только уведомления**
   
    ![][8]
6. [Необязательно] Можно также указать URL-адрес действия. Убедитесь, что используется схема URL-адрес, указанный при настройке подключаемого модуля hello **AZME\_ПЕРЕНАПРАВЛЕНИЯ\_URL-адрес** переменной например *myapp://test*.  
7. Возможные основные кампании параметр hello, процедура завершена. Теперь прокрутите список вниз и нажмите hello **создать** кнопку toosave кампанию.
8. И, наконец, **активируйте** кампанию.
   
    ![][10]
9. Теперь push-уведомления в рамках этой кампании будут отображаться на устройстве или в эмуляторе. 

## <a id="next-steps"></a>Дальнейшие действия
[Обзор методов, доступных в пакете Cordova SDK для Служб мобильного взаимодействия](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

