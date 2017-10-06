---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a><span data-ttu-id="c3211-103">Как tooIntegrate Engagement для Android</span><span class="sxs-lookup"><span data-stu-id="c3211-103">How tooIntegrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3211-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="c3211-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="c3211-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="c3211-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="c3211-106">iOS</span><span class="sxs-lookup"><span data-stu-id="c3211-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="c3211-107">Android</span><span class="sxs-lookup"><span data-stu-id="c3211-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="c3211-108">Эта процедура описывает hello простейший способ tooactivate Engagement аналитики и наблюдение за функциями в приложении Android.</span><span class="sxs-lookup"><span data-stu-id="c3211-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3211-109">Минимальный уровень пакета API SDK Android должен быть 10 или выше (Android 2.3.3 ил выше).</span><span class="sxs-lookup"><span data-stu-id="c3211-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="c3211-110">следующие шаги Hello — это отчет hello достаточно tooactivates журналов необходимости toocompute все статистические данные о пользователей, сеансы, действия, сбои и Technicals.</span><span class="sxs-lookup"><span data-stu-id="c3211-110">hello following steps are enough tooactivates hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="c3211-111">Hello журналов требуется отчет toocompute другие статистические данные, как события, ошибок и задания должны выполняться вручную с помощью hello Engagement API (в разделе [как toouse hello advanced мобильного охвата, добавление тегов API в Android](mobile-engagement-android-use-engagement-api.md) с момента их Статистика зависит от приложения.</span><span class="sxs-lookup"><span data-stu-id="c3211-111">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="c3211-112">Внедрение hello Engagement SDK и службы в проекте Android</span><span class="sxs-lookup"><span data-stu-id="c3211-112">Embed hello Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="c3211-113">Здравствуйте, загрузки из пакета SDK для Android [здесь](https://aka.ms/vq9mfn) получить `mobile-engagement-VERSION.jar` и поместить их в hello `libs` папку проекта Android (создайте папку библиотеки hello, если он еще не существует).</span><span class="sxs-lookup"><span data-stu-id="c3211-113">Download hello Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into hello `libs` folder of your Android project (create hello libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3211-114">При создании пакета приложения с ProGuard tookeep необходимо некоторые классы.</span><span class="sxs-lookup"><span data-stu-id="c3211-114">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="c3211-115">Можно использовать следующий фрагмент конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="c3211-115">You can use hello following configuration snippet:</span></span>
> 
> <span data-ttu-id="c3211-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="c3211-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="c3211-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="c3211-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="c3211-118">Укажите строку подключения обязательств, вызывающему Привет, следующий метод в операцией запуска hello:</span><span class="sxs-lookup"><span data-stu-id="c3211-118">Specify your Engagement connection string by calling hello following method in hello launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="c3211-119">Hello строку подключения для приложения отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c3211-119">hello connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="c3211-120">Если отсутствует, добавьте следующие разрешения Android hello (перед hello `<application>` тега):</span><span class="sxs-lookup"><span data-stu-id="c3211-120">If missing, add hello following Android permissions (before hello `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="c3211-121">Добавьте следующий раздел hello (между hello `<application>` и `</application>` теги):</span><span class="sxs-lookup"><span data-stu-id="c3211-121">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="c3211-122">Изменение `<Your application name>` с именем приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c3211-122">Change `<Your application name>` by hello name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="c3211-123">Hello `android:label` атрибута можно toochoose имя hello hello Engagement службы, которое будет отображаться toohello конечных пользователей на экране «Запуск службы» Привет телефона.</span><span class="sxs-lookup"><span data-stu-id="c3211-123">hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it will appear toohello end-users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="c3211-124">Это рекомендуется этот атрибут tooset слишком`"<Your application name>Service"` (например `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="c3211-124">It is recommended tooset this attribute too`"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="c3211-125">Указание hello `android:process` атрибут гарантирует, что hello Engagement службы будет выполняться в отдельном процессе (работающем участия в hello же процесс, как приложение сделает main или UI-потока потенциально менее отвечать на запросы).</span><span class="sxs-lookup"><span data-stu-id="c3211-125">Specifying hello `android:process` attribute ensures that hello Engagement service will run in its own process (running Engagement in hello same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="c3211-126">Любой код, поместите в `Application.onCreate()` и обратные вызовы других приложений будет выполняться для вашего приложения процессов, включая службы Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="c3211-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="c3211-127">Может иметь нежелательные побочные эффекты (например, выделения ненужные памяти и потоки в процессе hello Engagement повторяющиеся широковещательных получателей или службы).</span><span class="sxs-lookup"><span data-stu-id="c3211-127">It may have unwanted side effects (like unneeded memory allocations and threads in hello Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="c3211-128">При переопределении `Application.onCreate()`, это рекомендуемое tooadd hello, следующий фрагмент кода в начале hello вашей `Application.onCreate()` функции:</span><span class="sxs-lookup"><span data-stu-id="c3211-128">If you override `Application.onCreate()`, it's recommended tooadd hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="c3211-129">Вам доступны такие же действия hello `Application.onTerminate()`, `Application.onLowMemory()` и `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="c3211-129">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="c3211-130">Кроме того, можно расширить `EngagementApplication` вместо расширение `Application`: hello обратного вызова `Application.onCreate()` hello Проверка процесса и вызывает `Application.onApplicationProcessCreate()` только если hello текущий процесс не hello один hello Engagement службы размещения, hello и те же правила применяются для Здравствуйте других обратных вызовов.</span><span class="sxs-lookup"><span data-stu-id="c3211-130">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="c3211-131">Упрощенные отчеты</span><span class="sxs-lookup"><span data-stu-id="c3211-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="c3211-132">Рекомендуемый метод: перегрузка классов `Activity`</span><span class="sxs-lookup"><span data-stu-id="c3211-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="c3211-133">В отчете hello tooactivate порядок всех журналов hello, необходимых в Engagement toocompute пользователей, сеансы, действия, сбои и технические данные, достаточно лишь toomake все вашей `*Activity` вложенные классы наследуются от соответствующего hello `Engagement*Activity` классы (например если распространяется действие устаревших `ListActivity`, убедитесь, он расширяет `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="c3211-133">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you just have toomake all your `*Activity` sub-classes inherit from hello corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="c3211-134">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c3211-134">**Without Engagement :**</span></span>

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

<span data-ttu-id="c3211-135">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c3211-135">**With Engagement :**</span></span>

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> <span data-ttu-id="c3211-136">При использовании `EngagementListActivity` или `EngagementExpandableListActivity`, убедитесь, что любой вызов слишком`requestWindowFeature(...);` выполняется до вызова hello слишком`super.onCreate(...);`, в противном случае произойдет сбой.</span><span class="sxs-lookup"><span data-stu-id="c3211-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="c3211-137">Эти классы можно найти в hello `src` папке и скопируйте их в проект.</span><span class="sxs-lookup"><span data-stu-id="c3211-137">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="c3211-138">классы Hello также находятся в hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="c3211-138">hello classes are also in hello **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="c3211-139">Альтернативный метод: вызов `startActivity()` и `endActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="c3211-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="c3211-140">Если невозможно или нежелательно toooverload вашей `Activity` классов, можно вместо этого начала и окончания действия пользователя путем вызова `EngagementAgent`методы напрямую.</span><span class="sxs-lookup"><span data-stu-id="c3211-140">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3211-141">Hello Android SDK никогда не вызывает hello `endActivity()` даже при закрытии приложения hello метод (в Android приложения фактически никогда не закрыты).</span><span class="sxs-lookup"><span data-stu-id="c3211-141">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="c3211-142">Таким образом, *высокой* рекомендуется toocall hello `startActivity()` метод в hello `onResume` обратного вызова *все* действия и hello `endActivity()` метод в hello `onPause()` обратный вызов из *все* ваши действия.</span><span class="sxs-lookup"><span data-stu-id="c3211-142">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="c3211-143">Это hello единственным способом toobe убедиться, что сеансы не попадают.</span><span class="sxs-lookup"><span data-stu-id="c3211-143">This is hello only way toobe sure that sessions will not be leaked.</span></span> <span data-ttu-id="c3211-144">Если сеанс утечка, hello Engagement службы никогда не отключится от внутреннего сервера охвата hello (поскольку служба hello остается подключенным, поскольку сеанс находится в состоянии ожидания).</span><span class="sxs-lookup"><span data-stu-id="c3211-144">If a session is leaked, hello Engagement service will never disconnect from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="c3211-145">Пример:</span><span class="sxs-lookup"><span data-stu-id="c3211-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="c3211-146">Этот пример очень похож toohello `EngagementActivity` класс и его вариантов, исходный код которого приведен в hello `src` папки.</span><span class="sxs-lookup"><span data-stu-id="c3211-146">This example very similiar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="c3211-147">Тест</span><span class="sxs-lookup"><span data-stu-id="c3211-147">Test</span></span>
<span data-ttu-id="c3211-148">Теперь проверьте интеграцией мобильное приложение запускается в эмуляторе или устройстве и убедиться, что он регистрирует сеанс на вкладке монитора hello.</span><span class="sxs-lookup"><span data-stu-id="c3211-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on hello Monitor tab.</span></span>

<span data-ttu-id="c3211-149">Далее разделах Hello являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="c3211-149">hello next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="c3211-150">Отчеты о расположении</span><span class="sxs-lookup"><span data-stu-id="c3211-150">Location reporting</span></span>
<span data-ttu-id="c3211-151">Если требуется сообщила toobe расположения, необходимо tooadd несколько строк конфигурации (между hello `<application>` и `</application>` теги).</span><span class="sxs-lookup"><span data-stu-id="c3211-151">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="c3211-152">Отчеты о расположении отложенной области</span><span class="sxs-lookup"><span data-stu-id="c3211-152">Lazy area location reporting</span></span>
<span data-ttu-id="c3211-153">Отчеты о местоположении неактивной области позволяет tooreport hello Страна, регион и локальность связанных toodevices.</span><span class="sxs-lookup"><span data-stu-id="c3211-153">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="c3211-154">Этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора ячейки или Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="c3211-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="c3211-155">Hello области устройства отображается только один раз за сеанс.</span><span class="sxs-lookup"><span data-stu-id="c3211-155">hello device area is reported at most once per session.</span></span> <span data-ttu-id="c3211-156">Hello GPS никогда не используется, и таким образом, этот тип расположения отчета имеет очень мало (не toosay не) влияние на hello батареи.</span><span class="sxs-lookup"><span data-stu-id="c3211-156">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="c3211-157">Области отчета — используется toocompute географической статистические данные о пользователях, сеансах, события и ошибки.</span><span class="sxs-lookup"><span data-stu-id="c3211-157">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="c3211-158">Они также могут использоваться в качестве критерия для рекламных компаний Reach.</span><span class="sxs-lookup"><span data-stu-id="c3211-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="c3211-159">расположение неактивной области tooenable отчетов, это можно сделать с помощью конфигурации hello, упомянутых выше в этой процедуре:</span><span class="sxs-lookup"><span data-stu-id="c3211-159">tooenable lazy area location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="c3211-160">Также необходим hello tooadd следующие разрешения, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="c3211-160">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="c3211-161">Вы также можете продолжить использовать команду ``ACCESS_FINE_LOCATION``, если она уже используется в приложении.</span><span class="sxs-lookup"><span data-stu-id="c3211-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="c3211-162">Отчет о расположении в реальном времени</span><span class="sxs-lookup"><span data-stu-id="c3211-162">Real time location reporting</span></span>
<span data-ttu-id="c3211-163">Отчеты о местоположении реальном времени позволяет tooreport hello широты и долготы связанные toodevices.</span><span class="sxs-lookup"><span data-stu-id="c3211-163">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="c3211-164">По умолчанию отчеты о местоположении этого типа использует только сетевые расположения (на основании идентификатора ячейки или Wi-Fi) и hello reporting активен только при запуске приложения hello в переднего плана (т. е. во время сеанса).</span><span class="sxs-lookup"><span data-stu-id="c3211-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="c3211-165">Расположены в режиме реального времени *не* используется toocompute статистики.</span><span class="sxs-lookup"><span data-stu-id="c3211-165">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="c3211-166">Их единственной целью является использование hello tooallow географическом разграничении в режиме реального времени \<Reach аудитории географическое зонирование\> критерий в кампаниях Reach.</span><span class="sxs-lookup"><span data-stu-id="c3211-166">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="c3211-167">расположение реального времени tooenable отчетов, это можно сделать с помощью конфигурации hello, упомянутых выше в этой процедуре:</span><span class="sxs-lookup"><span data-stu-id="c3211-167">tooenable real time location reporting, you can do it by using hello configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="c3211-168">Также необходим hello tooadd следующие разрешения, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="c3211-168">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="c3211-169">Вы также можете продолжить использовать команду ``ACCESS_FINE_LOCATION``, если она уже используется в приложении.</span><span class="sxs-lookup"><span data-stu-id="c3211-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="c3211-170">Отчеты на базе GPS</span><span class="sxs-lookup"><span data-stu-id="c3211-170">GPS based reporting</span></span>
<span data-ttu-id="c3211-171">По умолчанию отчеты о расположении в реальном времени используют только сетевые расположения.</span><span class="sxs-lookup"><span data-stu-id="c3211-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="c3211-172">Использование hello tooenable GPS на основе расположения (которые являются гораздо более точные), используйте hello объекта конфигурации:</span><span class="sxs-lookup"><span data-stu-id="c3211-172">tooenable hello use of GPS based locations (which are far more precise), use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="c3211-173">Также необходим hello tooadd следующие разрешения, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="c3211-173">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="c3211-174">Отчет в фоновом режиме</span><span class="sxs-lookup"><span data-stu-id="c3211-174">Background reporting</span></span>
<span data-ttu-id="c3211-175">По умолчанию отчеты о местоположении реального времени активен только при запуске приложения hello в переднего плана (т. е. во время сеанса).</span><span class="sxs-lookup"><span data-stu-id="c3211-175">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="c3211-176">также tooenable hello отчетов, в фоновом режиме, используйте hello объекта конфигурации:</span><span class="sxs-lookup"><span data-stu-id="c3211-176">tooenable hello reporting also in background, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="c3211-177">При запуске приложения hello в фоновом режиме, выводятся только на основе сетевого расположения, даже если включена hello GPS.</span><span class="sxs-lookup"><span data-stu-id="c3211-177">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="c3211-178">Hello фона расположение отчета будет остановлено, если пользователь hello перезагружает его устройство, можно добавить этот toomake автоматический перезапуск во время загрузки:</span><span class="sxs-lookup"><span data-stu-id="c3211-178">hello background location report will be stopped if hello user reboots its device, you can add this toomake it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="c3211-179">Также необходим hello tooadd следующие разрешения, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="c3211-179">You also need tooadd hello following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="c3211-180">Разрешения в Android M</span><span class="sxs-lookup"><span data-stu-id="c3211-180">Android M permissions</span></span>
<span data-ttu-id="c3211-181">Начиная с Android M, управление некоторыми разрешениями осуществляется в среде выполнения и требует согласия пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3211-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="c3211-182">разрешения Hello среда выполнения будет отключена по умолчанию для новых установок приложения при использовании Android API уровня 23.</span><span class="sxs-lookup"><span data-stu-id="c3211-182">hello runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="c3211-183">В противном случае они будут включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c3211-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="c3211-184">Hello пользователь может включить или отключить эти разрешения из меню параметров устройства hello.</span><span class="sxs-lookup"><span data-stu-id="c3211-184">hello user can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="c3211-185">Отключение разрешений у системного меню разрывает фоновые процессы приложения hello, это поведение системы и не оказывает влияния на возможность принудительной tooreceive в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="c3211-185">Turning off permissions from system menu kills background processes of hello application, this is a system behavior and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="c3211-186">В контексте hello мобильного охвата требуются разрешения hello, требующих утверждения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c3211-186">In hello context of Mobile Engagement, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="c3211-187">`WRITE_EXTERNAL_STORAGE` (только если для него планируется использовать API Android уровня 23)</span><span class="sxs-lookup"><span data-stu-id="c3211-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="c3211-188">Hello внешнего хранилища используется только для компонентов общую картину Reach.</span><span class="sxs-lookup"><span data-stu-id="c3211-188">hello external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="c3211-189">Если найти попросить пользователей это разрешение toobe нарушают работу, его можно удалить, если используется только для мобильного охвата, но по цене hello отключить общую картину.</span><span class="sxs-lookup"><span data-stu-id="c3211-189">If you find asking users this permission toobe disruptive, you can remove it if you used it only for Mobile Engagement but at hello cost of disabling big picture feature.</span></span>

<span data-ttu-id="c3211-190">Для доступа к функциям расположения hello должен запросить toouser разрешения с помощью стандартной системы диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="c3211-190">For hello location features, you should request permissions toouser using a standard system dialog.</span></span> <span data-ttu-id="c3211-191">Если hello пользователь утверждает, необходимо tootell ``EngagementAgent`` tootake, изменения в учетную запись в реальном времени (в противном случае изменение hello будет обработана hello Далее hello пользователь запускает hello приложении время).</span><span class="sxs-lookup"><span data-stu-id="c3211-191">If hello user approves, you need tootell ``EngagementAgent`` tootake that change into account in real time (otherwise hello change will be processed hello next time hello user launches hello application).</span></span>

<span data-ttu-id="c3211-192">Ниже приведен toouse пример кода в действии разрешения toorequest приложения и результат прямого hello при положительном слишком``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="c3211-192">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="c3211-193">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="c3211-193">Advanced reporting</span></span>
<span data-ttu-id="c3211-194">При необходимости следует tooreport приложения определенных событий, ошибок и задания необходимо toouse hello Engagement API через методы hello hello `EngagementAgent` класса.</span><span class="sxs-lookup"><span data-stu-id="c3211-194">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="c3211-195">Объект этого класса можно получить путем вызова hello `EngagementAgent.getInstance()` статический метод.</span><span class="sxs-lookup"><span data-stu-id="c3211-195">An object of this class can be retreived by calling hello `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="c3211-196">Hello Engagement API позволяет toouse всем Engagement расширенные возможности и подробно описан в hello как tooUse API Engagement для Android (а также в технической документации hello объекта hello `EngagementAgent` класса).</span><span class="sxs-lookup"><span data-stu-id="c3211-196">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on Android (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="c3211-197">Расширенная конфигурация (в AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="c3211-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="c3211-198">Блокировки пробуждения</span><span class="sxs-lookup"><span data-stu-id="c3211-198">Wake locks</span></span>
<span data-ttu-id="c3211-199">Toobe отправку статистические данные в реальном времени, когда с помощью Wi-Fi или при отключенном экран приветствия, добавьте hello, следуя дополнительное разрешение:</span><span class="sxs-lookup"><span data-stu-id="c3211-199">If you want toobe sure that statistics are sent in real time when using Wifi or when hello screen is off, add hello following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="c3211-200">Отчет о сбоях</span><span class="sxs-lookup"><span data-stu-id="c3211-200">Crash report</span></span>
<span data-ttu-id="c3211-201">Отчеты о сбоях toodisable, добавить это (между hello `<application>` и `</application>` теги):</span><span class="sxs-lookup"><span data-stu-id="c3211-201">If you want toodisable crash reports, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="c3211-202">Пороговое значение пакета</span><span class="sxs-lookup"><span data-stu-id="c3211-202">Burst threshold</span></span>
<span data-ttu-id="c3211-203">По умолчанию hello Engagement службы отчетов входит в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="c3211-203">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="c3211-204">Если приложение сообщает журналов производится очень часто, это лучше toobuffer hello журналы и tooreport их все за один раз на обычное время базового (это называется «пакетный режим» hello).</span><span class="sxs-lookup"><span data-stu-id="c3211-204">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello "burst mode").</span></span> <span data-ttu-id="c3211-205">toodo таким образом, добавьте это (между hello `<application>` и `</application>` теги):</span><span class="sxs-lookup"><span data-stu-id="c3211-205">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="c3211-206">Hello пакетный режим немного увеличить батареи hello жизни но оказывает влияние на hello монитор Engagement: все сеансы и задания будут скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны).</span><span class="sxs-lookup"><span data-stu-id="c3211-206">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="c3211-207">Это рекомендуется toouse Повышение порогового значения больше чем 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="c3211-207">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="c3211-208">Время ожидания сеанса</span><span class="sxs-lookup"><span data-stu-id="c3211-208">Session timeout</span></span>
<span data-ttu-id="c3211-209">По умолчанию сеанс — десятках завершается после окончания hello его последним действием (что обычно происходит, нажав клавишу Home hello или клавиша, "Назад" по параметр телефону hello простоя или переходе в другое приложение).</span><span class="sxs-lookup"><span data-stu-id="c3211-209">By default, a session is ended 10s after hello end of its last activity (which usually occurs by pressing hello Home or Back key, by setting hello phone idle or by jumping into another application).</span></span> <span data-ttu-id="c3211-210">Это tooavoid сеанса разбиение каждого пользователя hello времени выхода и возврата приложения toohello очень быстро (что может произойти при он взять образ, проверьте уведомления, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c3211-210">This is tooavoid a session split each time hello user exit and return toohello application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="c3211-211">Вы можете toomodify этот параметр.</span><span class="sxs-lookup"><span data-stu-id="c3211-211">You may want toomodify this parameter.</span></span> <span data-ttu-id="c3211-212">toodo таким образом, добавьте это (между hello `<application>` и `</application>` теги):</span><span class="sxs-lookup"><span data-stu-id="c3211-212">toodo so, add this (between hello `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="c3211-213">Выключение отчетов журналов</span><span class="sxs-lookup"><span data-stu-id="c3211-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="c3211-214">Использование вызова метода</span><span class="sxs-lookup"><span data-stu-id="c3211-214">Using a method call</span></span>
<span data-ttu-id="c3211-215">Если требуется toostop Engagement отправляет журналов, можно вызвать:</span><span class="sxs-lookup"><span data-stu-id="c3211-215">If you want Engagement toostop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="c3211-216">Этот вызов является постоянным: он использует файл общих параметров.</span><span class="sxs-lookup"><span data-stu-id="c3211-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="c3211-217">Если Engagement активен при вызове этой функции, может потребоваться 1 минуты для службы toostop hello.</span><span class="sxs-lookup"><span data-stu-id="c3211-217">If Engagement is active when you call this function, it may take 1 minute for hello service toostop.</span></span> <span data-ttu-id="c3211-218">Однако он не будет запускать службы hello во всех hello следующих запусках приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c3211-218">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="c3211-219">Можно включить снова отчетов путем вызова hello одинаково функционировать с журнала `true`.</span><span class="sxs-lookup"><span data-stu-id="c3211-219">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="c3211-220">Интеграция в собственное `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="c3211-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="c3211-221">Вместо вызова этой функции вы можете интегрировать данный параметр непосредственно в существующее `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="c3211-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="c3211-222">Можно настроить toouse Engagement предпочтениями-файл (hello нужный режим) в hello `AndroidManifest.xml` , что файл `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="c3211-222">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="c3211-223">Hello `engagement:agent:settings:name` ключ является именем hello используется toodefine hello Общие настройки файла.</span><span class="sxs-lookup"><span data-stu-id="c3211-223">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="c3211-224">Hello `engagement:agent:settings:mode` ключа используется toodefine режим hello hello Общие настройки файла, необходимо использовать hello же режим, как и в вашей `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="c3211-224">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file, you should use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="c3211-225">режим Hello должен быть передан как число: при использовании в коде является комбинацией флагов константой проверить общее значение hello.</span><span class="sxs-lookup"><span data-stu-id="c3211-225">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="c3211-226">Engagement всегда использовать hello `engagement:key` логическое ключа из файла параметров hello для управления этот параметр.</span><span class="sxs-lookup"><span data-stu-id="c3211-226">Engagement always use hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="c3211-227">Следующий пример Hello `AndroidManifest.xml` показано hello значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="c3211-227">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="c3211-228">Затем можно добавить `CheckBoxPreference` в макете предпочтения как hello, выполнив одно:</span><span class="sxs-lookup"><span data-stu-id="c3211-228">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
