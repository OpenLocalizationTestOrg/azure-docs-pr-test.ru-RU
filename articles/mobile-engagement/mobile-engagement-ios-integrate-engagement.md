---
title: "aaaAzure iOS Mobile Engagement SDK-интеграция | Документы Microsoft"
description: "Последние обновления и указания для пакета SDK для iOS для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a>Как tooIntegrate участия в iOS
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

Эта процедура описывает hello простейший способ tooactivate Engagement аналитики и наблюдение за функциями в приложении iOS.

Hello Engagement SDK требует iOS7 + и Xcode 8 +: hello целевого объекта развертывания приложения необходимо по крайней мере iOS 7.

> [!NOTE]
> Если действительно зависят XCode 7, то вы можете использовать hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Во время выполнения с устройства iOS 10 см. на hello модулем этой предыдущей версии имеется известная ошибка [hello reach модуль интеграции](mobile-engagement-ios-integrate-engagement-reach.md) для получения дополнительных сведений. Если выбирается toouse hello SDK v3.2.4 просто пропустить hello `UserNotifications.framework` импорта в следующем шаге hello.
>
>

следующие шаги Hello — это отчет hello достаточно tooactivate журналов необходимости toocompute все статистические данные о пользователей, сеансы, действия, сбои и Technicals. Hello журналов требуется отчет toocompute другие статистические данные, как события, ошибок и задания должны выполняться вручную с помощью Engagement API hello (см. [как toouse hello дополнительные теги API в приложении iOS Mobile Engagement](mobile-engagement-ios-use-engagement-api.md) с момента статистику зависят от приложения.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>Внедрение hello Engagement SDK в проект iOS
* Загрузите пакет SDK для iOS hello из [здесь](http://aka.ms/qk2rnj).
* Добавить hello Engagement SDK tooyour iOS проекта: в Xcode, щелкните правой кнопкой мыши проект и выберите **» слишком добавить файлы...»** и выберите hello `EngagementSDK` папки.
* Engagement требует дополнительных платформ toowork: в обозревателе проектов hello, откройте панель проекта и выберите hello правильный. Откройте hello **«Этапы сборки»** вкладке и в hello **«Ссылку двоичного файла с библиотеками»** меню, добавьте эти платформы:

  * `UserNotifications.framework`-задать связь hello как`Optional`
  * `AdSupport.framework`-задать связь hello как`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> можно удалить Hello AdSupport framework. Взаимодействия должен это hello toocollect framework IDFA. Тем не менее, можно отключить коллекцию IDFA \<ios sdk-engagement idfa\> toocomply с новой политикой Apple hello относительно этот код.
>
>

## <a name="initialize-hello-engagement-sdk"></a>Инициализировать hello Engagement SDK
Необходимые toomodify делегат вашего приложения.

* Вверху hello файл реализации импортируйте hello Engagement агента:

      [...]
      #import "EngagementAgent.h"
* Инициализация Engagement внутри метода hello "**applicationDidFinishLaunching:**«или»**приложения: didFinishLaunchingWithOptions:**":

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>Упрощенные отчеты
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>Рекомендуемый метод: перегрузка классов `UIViewController`
В отчете hello tooactivate порядок всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, можно просто сделать все вашей `UIViewController` вложенные классы наследуют от hello `EngagementViewController` классы (такие же правила для `UITableViewController`  - \> `EngagementTableViewController`).

**Без Engagement:**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**С Engagement:**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>Альтернативный метод: вызов `startActivity()` вручную
Если невозможно или нежелательно toooverload вашей `UIViewController` классы, вместо этого можно запустить ваши действия, вызвав `EngagementAgent`методы напрямую.

> [!IMPORTANT]
> пакет SDK для iOS Hello автоматически вызывает hello `endActivity()` метод при закрытии приложения hello. Таким образом, *высокой* рекомендуется toocall hello `startActivity` метод изменении hello действий пользователя hello и слишком*никогда* hello вызовов `endActivity` метод, с момента вызова этого метода заставляет Hello toobe текущий сеанс завершен.
>
>

## <a name="location-reporting"></a>Отчеты о расположении
Apple условия обслуживания позволяет приложениям toouse расположение отслеживания статистики только для цели. Таким образом рекомендуется tooenable расположение отчеты только в том случае, если приложение использует также отслеживание по другой причине размещения hello.

Начиная с iOS 8, необходимо указать как приложение использует службы определения местоположения, задав строку для ключа hello описание [NSLocationWhenInUseUsageDescription] или [NSLocationAlwaysUsageDescription]в файле Info.plist приложения. Если необходимо tooreport расположение в фоновом режиме hello обязательств, добавьте раздел hello NSLocationAlwaysUsageDescription. Во всех остальных случаях добавьте раздел hello NSLocationWhenInUseUsageDescription. Обратите внимание, что NSLocationAlwaysAndWhenInUseUsageDescription и NSLocationWhenInUseUsageDescription tooreport фона расположение на iOS 11.

### <a name="lazy-area-location-reporting"></a>Отчеты о расположении отложенной области
Отчеты о местоположении неактивной области позволяет tooreport hello Страна, регион и локальность связанных toodevices. Этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора ячейки или Wi-Fi). Hello области устройства отображается только один раз за сеанс. Hello GPS никогда не используется, и таким образом, этот тип расположения отчета имеет очень мало (не toosay не) влияние на hello батареи.

Области отчета — используется toocompute географической статистические данные о пользователях, сеансах, события и ошибки. Они также могут использоваться в качестве критерия для рекламных компаний Reach. Hello последнее известное области, указанное для устройство может быть полученные Спасибо toohello [API устройства].

расположение неактивной области tooenable отчетов, добавьте hello, следующей строкой после инициализации агента Engagement hello:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>Отчет о расположении в реальном времени
Отчеты о местоположении реальном времени позволяет tooreport hello широты и долготы связанные toodevices. По умолчанию отчеты о местоположении этого типа использует только сетевые расположения (на основании идентификатора ячейки или Wi-Fi) и hello reporting активен только при запуске приложения hello в переднего плана (т. е. во время сеанса).

Расположены в режиме реального времени *не* используется toocompute статистики. Их единственной целью является использование hello tooallow географическом разграничении в режиме реального времени \<Reach аудитории географическое зонирование\> критерий в кампаниях Reach.

расположение реального времени tooenable отчетов, добавьте hello, следующей строкой после инициализации агента Engagement hello:

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>Отчеты на базе GPS
По умолчанию отчеты о расположении в реальном времени используют только сетевые расположения. Использование hello tooenable GPS на основе расположения (которые являются гораздо более точные), добавьте:

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>Отчет в фоновом режиме
По умолчанию отчеты о местоположении реального времени активен только при запуске приложения hello в переднего плана (т. е. во время сеанса). Добавьте также отчетов в фоновом режиме, hello tooenable:

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> При запуске приложения hello в фоновом режиме, выводятся только на основе сетевого расположения, даже если включена hello GPS.
>
>

Реализация этой функции будет вызывать [startMonitoringSignificantLocationChanges] переходом приложения в фоновый hello. Имейте в виду, что он будет автоматически перезапустите приложения hello фона при получении нового расположения события.

## <a name="advanced-reporting"></a>Расширенные отчеты
При необходимости следует tooreport приложения определенных событий, ошибок и задания необходимо toouse hello Engagement API через методы hello hello `EngagementAgent` класса. Объект этого класса можно получить путем вызова hello `[EngagementAgent shared]` статический метод.

Hello Engagement API позволяет toouse всем Engagement расширенные возможности и подробно описан в hello как tooUse API взаимодействия для операций ввода-вывода (а также в технической документации hello объекта hello `EngagementAgent` класса).

## <a name="disable-idfa-collection"></a>Отключение сбора IDFA
По умолчанию, Engagement будет использовать hello [IDFA] toouniquely идентификации пользователя. Но если вы не используете рекламу в другом месте в приложение hello, могут быть отклонены по hello процесс проверки App Store. Можно отключить коллекцию IDFA, добавив макрос препроцессора hello `ENGAGEMENT_DISABLE_IDFA` в pch-файл (или в hello `Build Settings` приложения). Это будет убедитесь, что нет ссылок на слишком`ASIdentifierManager`, `advertisingIdentifier` или `isAdvertisingTrackingEnabled` в сборке приложения hello.

Интеграция в hello **prefix.pch** файла:

    #define ENGAGEMENT_DISABLE_IDFA
    ...

Можно проверить, что коллекцию IDFA hello правильно отключена в приложения, проверьте журналы тестирования Engagement hello. Hello, интеграции тестирования в разделе\<ios-sdk-engagement тест idfa\> документации для получения дополнительных сведений.

## <a name="disable-log-reporting"></a>Выключение отчетов журналов
### <a name="using-a-method-call"></a>Использование вызова метода
Если требуется toostop Engagement отправляет журналов, можно вызвать:

    [[EngagementAgent shared] setEnabled:NO];

Этот вызов является постоянным: он использует `NSUserDefaults` toostore hello сведения.

Можно включить снова отчетов путем вызова hello одинаково функционировать с журнала `YES`.

### <a name="integration-in-your-settings-bundle"></a>Интеграция в пакет параметров
Вместо вызова данной функции вы также можете интегрировать данный параметр напрямую в существующий файл `Settings.bundle` . Здравствуйте, строка `engagement_agent_enabled` должно использоваться как идентификатор предпочтений hello должен быть связан tooa переключатель (`PSToggleSwitchSpecifier`).

Следующий пример Hello `Settings.bundle` показано, как tooimplement его:

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[API устройства]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
