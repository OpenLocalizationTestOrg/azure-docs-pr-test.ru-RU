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
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="3d393-103">Как tooIntegrate участия в iOS</span><span class="sxs-lookup"><span data-stu-id="3d393-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3d393-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="3d393-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="3d393-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="3d393-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="3d393-106">iOS</span><span class="sxs-lookup"><span data-stu-id="3d393-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="3d393-107">Android</span><span class="sxs-lookup"><span data-stu-id="3d393-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="3d393-108">Эта процедура описывает hello простейший способ tooactivate Engagement аналитики и наблюдение за функциями в приложении iOS.</span><span class="sxs-lookup"><span data-stu-id="3d393-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="3d393-109">Hello Engagement SDK требует iOS7 + и Xcode 8 +: hello целевого объекта развертывания приложения необходимо по крайней мере iOS 7.</span><span class="sxs-lookup"><span data-stu-id="3d393-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="3d393-110">Если действительно зависят XCode 7, то вы можете использовать hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="3d393-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="3d393-111">Во время выполнения с устройства iOS 10 см. на hello модулем этой предыдущей версии имеется известная ошибка [hello reach модуль интеграции](mobile-engagement-ios-integrate-engagement-reach.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="3d393-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="3d393-112">Если выбирается toouse hello SDK v3.2.4 просто пропустить hello `UserNotifications.framework` импорта в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="3d393-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="3d393-113">следующие шаги Hello — это отчет hello достаточно tooactivate журналов необходимости toocompute все статистические данные о пользователей, сеансы, действия, сбои и Technicals.</span><span class="sxs-lookup"><span data-stu-id="3d393-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="3d393-114">Hello журналов требуется отчет toocompute другие статистические данные, как события, ошибок и задания должны выполняться вручную с помощью Engagement API hello (см. [как toouse hello дополнительные теги API в приложении iOS Mobile Engagement](mobile-engagement-ios-use-engagement-api.md) с момента статистику зависят от приложения.</span><span class="sxs-lookup"><span data-stu-id="3d393-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="3d393-115">Внедрение hello Engagement SDK в проект iOS</span><span class="sxs-lookup"><span data-stu-id="3d393-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="3d393-116">Загрузите пакет SDK для iOS hello из [здесь](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="3d393-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="3d393-117">Добавить hello Engagement SDK tooyour iOS проекта: в Xcode, щелкните правой кнопкой мыши проект и выберите **» слишком добавить файлы...»** и выберите hello `EngagementSDK` папки.</span><span class="sxs-lookup"><span data-stu-id="3d393-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="3d393-118">Engagement требует дополнительных платформ toowork: в обозревателе проектов hello, откройте панель проекта и выберите hello правильный.</span><span class="sxs-lookup"><span data-stu-id="3d393-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="3d393-119">Откройте hello **«Этапы сборки»** вкладке и в hello **«Ссылку двоичного файла с библиотеками»** меню, добавьте эти платформы:</span><span class="sxs-lookup"><span data-stu-id="3d393-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="3d393-120">`UserNotifications.framework`-задать связь hello как`Optional`</span><span class="sxs-lookup"><span data-stu-id="3d393-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="3d393-121">`AdSupport.framework`-задать связь hello как`Optional`</span><span class="sxs-lookup"><span data-stu-id="3d393-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="3d393-122">можно удалить Hello AdSupport framework.</span><span class="sxs-lookup"><span data-stu-id="3d393-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="3d393-123">Взаимодействия должен это hello toocollect framework IDFA.</span><span class="sxs-lookup"><span data-stu-id="3d393-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="3d393-124">Тем не менее, можно отключить коллекцию IDFA \<ios sdk-engagement idfa\> toocomply с новой политикой Apple hello относительно этот код.</span><span class="sxs-lookup"><span data-stu-id="3d393-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="3d393-125">Инициализировать hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="3d393-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="3d393-126">Необходимые toomodify делегат вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="3d393-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="3d393-127">Вверху hello файл реализации импортируйте hello Engagement агента:</span><span class="sxs-lookup"><span data-stu-id="3d393-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="3d393-128">Инициализация Engagement внутри метода hello "**applicationDidFinishLaunching:**«или»**приложения: didFinishLaunchingWithOptions:**":</span><span class="sxs-lookup"><span data-stu-id="3d393-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="3d393-129">Упрощенные отчеты</span><span class="sxs-lookup"><span data-stu-id="3d393-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="3d393-130">Рекомендуемый метод: перегрузка классов `UIViewController`</span><span class="sxs-lookup"><span data-stu-id="3d393-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="3d393-131">В отчете hello tooactivate порядок всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, можно просто сделать все вашей `UIViewController` вложенные классы наследуют от hello `EngagementViewController` классы (такие же правила для `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="3d393-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="3d393-132">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="3d393-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="3d393-133">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="3d393-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="3d393-134">Альтернативный метод: вызов `startActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="3d393-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="3d393-135">Если невозможно или нежелательно toooverload вашей `UIViewController` классы, вместо этого можно запустить ваши действия, вызвав `EngagementAgent`методы напрямую.</span><span class="sxs-lookup"><span data-stu-id="3d393-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d393-136">пакет SDK для iOS Hello автоматически вызывает hello `endActivity()` метод при закрытии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3d393-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="3d393-137">Таким образом, *высокой* рекомендуется toocall hello `startActivity` метод изменении hello действий пользователя hello и слишком*никогда* hello вызовов `endActivity` метод, с момента вызова этого метода заставляет Hello toobe текущий сеанс завершен.</span><span class="sxs-lookup"><span data-stu-id="3d393-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="3d393-138">Отчеты о расположении</span><span class="sxs-lookup"><span data-stu-id="3d393-138">Location reporting</span></span>
<span data-ttu-id="3d393-139">Apple условия обслуживания позволяет приложениям toouse расположение отслеживания статистики только для цели.</span><span class="sxs-lookup"><span data-stu-id="3d393-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="3d393-140">Таким образом рекомендуется tooenable расположение отчеты только в том случае, если приложение использует также отслеживание по другой причине размещения hello.</span><span class="sxs-lookup"><span data-stu-id="3d393-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="3d393-141">Начиная с iOS 8, необходимо указать как приложение использует службы определения местоположения, задав строку для ключа hello описание [NSLocationWhenInUseUsageDescription] или [NSLocationAlwaysUsageDescription]в файле Info.plist приложения.</span><span class="sxs-lookup"><span data-stu-id="3d393-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="3d393-142">Если необходимо tooreport расположение в фоновом режиме hello обязательств, добавьте раздел hello NSLocationAlwaysUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="3d393-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="3d393-143">Во всех остальных случаях добавьте раздел hello NSLocationWhenInUseUsageDescription.</span><span class="sxs-lookup"><span data-stu-id="3d393-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="3d393-144">Обратите внимание, что NSLocationAlwaysAndWhenInUseUsageDescription и NSLocationWhenInUseUsageDescription tooreport фона расположение на iOS 11.</span><span class="sxs-lookup"><span data-stu-id="3d393-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="3d393-145">Отчеты о расположении отложенной области</span><span class="sxs-lookup"><span data-stu-id="3d393-145">Lazy area location reporting</span></span>
<span data-ttu-id="3d393-146">Отчеты о местоположении неактивной области позволяет tooreport hello Страна, регион и локальность связанных toodevices.</span><span class="sxs-lookup"><span data-stu-id="3d393-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="3d393-147">Этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора ячейки или Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="3d393-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="3d393-148">Hello области устройства отображается только один раз за сеанс.</span><span class="sxs-lookup"><span data-stu-id="3d393-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="3d393-149">Hello GPS никогда не используется, и таким образом, этот тип расположения отчета имеет очень мало (не toosay не) влияние на hello батареи.</span><span class="sxs-lookup"><span data-stu-id="3d393-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="3d393-150">Области отчета — используется toocompute географической статистические данные о пользователях, сеансах, события и ошибки.</span><span class="sxs-lookup"><span data-stu-id="3d393-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="3d393-151">Они также могут использоваться в качестве критерия для рекламных компаний Reach.</span><span class="sxs-lookup"><span data-stu-id="3d393-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="3d393-152">Hello последнее известное области, указанное для устройство может быть полученные Спасибо toohello [API устройства].</span><span class="sxs-lookup"><span data-stu-id="3d393-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="3d393-153">расположение неактивной области tooenable отчетов, добавьте hello, следующей строкой после инициализации агента Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="3d393-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="3d393-154">Отчет о расположении в реальном времени</span><span class="sxs-lookup"><span data-stu-id="3d393-154">Real time location reporting</span></span>
<span data-ttu-id="3d393-155">Отчеты о местоположении реальном времени позволяет tooreport hello широты и долготы связанные toodevices.</span><span class="sxs-lookup"><span data-stu-id="3d393-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="3d393-156">По умолчанию отчеты о местоположении этого типа использует только сетевые расположения (на основании идентификатора ячейки или Wi-Fi) и hello reporting активен только при запуске приложения hello в переднего плана (т. е. во время сеанса).</span><span class="sxs-lookup"><span data-stu-id="3d393-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="3d393-157">Расположены в режиме реального времени *не* используется toocompute статистики.</span><span class="sxs-lookup"><span data-stu-id="3d393-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="3d393-158">Их единственной целью является использование hello tooallow географическом разграничении в режиме реального времени \<Reach аудитории географическое зонирование\> критерий в кампаниях Reach.</span><span class="sxs-lookup"><span data-stu-id="3d393-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="3d393-159">расположение реального времени tooenable отчетов, добавьте hello, следующей строкой после инициализации агента Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="3d393-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="3d393-160">Отчеты на базе GPS</span><span class="sxs-lookup"><span data-stu-id="3d393-160">GPS based reporting</span></span>
<span data-ttu-id="3d393-161">По умолчанию отчеты о расположении в реальном времени используют только сетевые расположения.</span><span class="sxs-lookup"><span data-stu-id="3d393-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="3d393-162">Использование hello tooenable GPS на основе расположения (которые являются гораздо более точные), добавьте:</span><span class="sxs-lookup"><span data-stu-id="3d393-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="3d393-163">Отчет в фоновом режиме</span><span class="sxs-lookup"><span data-stu-id="3d393-163">Background reporting</span></span>
<span data-ttu-id="3d393-164">По умолчанию отчеты о местоположении реального времени активен только при запуске приложения hello в переднего плана (т. е. во время сеанса).</span><span class="sxs-lookup"><span data-stu-id="3d393-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="3d393-165">Добавьте также отчетов в фоновом режиме, hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="3d393-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="3d393-166">При запуске приложения hello в фоновом режиме, выводятся только на основе сетевого расположения, даже если включена hello GPS.</span><span class="sxs-lookup"><span data-stu-id="3d393-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="3d393-167">Реализация этой функции будет вызывать [startMonitoringSignificantLocationChanges] переходом приложения в фоновый hello.</span><span class="sxs-lookup"><span data-stu-id="3d393-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="3d393-168">Имейте в виду, что он будет автоматически перезапустите приложения hello фона при получении нового расположения события.</span><span class="sxs-lookup"><span data-stu-id="3d393-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="3d393-169">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="3d393-169">Advanced reporting</span></span>
<span data-ttu-id="3d393-170">При необходимости следует tooreport приложения определенных событий, ошибок и задания необходимо toouse hello Engagement API через методы hello hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="3d393-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="3d393-171">Объект этого класса можно получить путем вызова hello `[EngagementAgent shared]` статический метод.</span><span class="sxs-lookup"><span data-stu-id="3d393-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="3d393-172">Hello Engagement API позволяет toouse всем Engagement расширенные возможности и подробно описан в hello как tooUse API взаимодействия для операций ввода-вывода (а также в технической документации hello объекта hello `EngagementAgent` класса).</span><span class="sxs-lookup"><span data-stu-id="3d393-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="3d393-173">Отключение сбора IDFA</span><span class="sxs-lookup"><span data-stu-id="3d393-173">Disable IDFA collection</span></span>
<span data-ttu-id="3d393-174">По умолчанию, Engagement будет использовать hello [IDFA] toouniquely идентификации пользователя.</span><span class="sxs-lookup"><span data-stu-id="3d393-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="3d393-175">Но если вы не используете рекламу в другом месте в приложение hello, могут быть отклонены по hello процесс проверки App Store.</span><span class="sxs-lookup"><span data-stu-id="3d393-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="3d393-176">Можно отключить коллекцию IDFA, добавив макрос препроцессора hello `ENGAGEMENT_DISABLE_IDFA` в pch-файл (или в hello `Build Settings` приложения).</span><span class="sxs-lookup"><span data-stu-id="3d393-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="3d393-177">Это будет убедитесь, что нет ссылок на слишком`ASIdentifierManager`, `advertisingIdentifier` или `isAdvertisingTrackingEnabled` в сборке приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3d393-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="3d393-178">Интеграция в hello **prefix.pch** файла:</span><span class="sxs-lookup"><span data-stu-id="3d393-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="3d393-179">Можно проверить, что коллекцию IDFA hello правильно отключена в приложения, проверьте журналы тестирования Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="3d393-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="3d393-180">Hello, интеграции тестирования в разделе\<ios-sdk-engagement тест idfa\> документации для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="3d393-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="3d393-181">Выключение отчетов журналов</span><span class="sxs-lookup"><span data-stu-id="3d393-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="3d393-182">Использование вызова метода</span><span class="sxs-lookup"><span data-stu-id="3d393-182">Using a method call</span></span>
<span data-ttu-id="3d393-183">Если требуется toostop Engagement отправляет журналов, можно вызвать:</span><span class="sxs-lookup"><span data-stu-id="3d393-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="3d393-184">Этот вызов является постоянным: он использует `NSUserDefaults` toostore hello сведения.</span><span class="sxs-lookup"><span data-stu-id="3d393-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="3d393-185">Можно включить снова отчетов путем вызова hello одинаково функционировать с журнала `YES`.</span><span class="sxs-lookup"><span data-stu-id="3d393-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="3d393-186">Интеграция в пакет параметров</span><span class="sxs-lookup"><span data-stu-id="3d393-186">Integration in your settings bundle</span></span>
<span data-ttu-id="3d393-187">Вместо вызова данной функции вы также можете интегрировать данный параметр напрямую в существующий файл `Settings.bundle` .</span><span class="sxs-lookup"><span data-stu-id="3d393-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="3d393-188">Здравствуйте, строка `engagement_agent_enabled` должно использоваться как идентификатор предпочтений hello должен быть связан tooa переключатель (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="3d393-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="3d393-189">Следующий пример Hello `Settings.bundle` показано, как tooimplement его:</span><span class="sxs-lookup"><span data-stu-id="3d393-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
