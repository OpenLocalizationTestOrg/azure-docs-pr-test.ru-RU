---
title: "Интеграция пакета Android SDK для Служб мобильного взаимодействия Azure"
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
ms.openlocfilehash: 35bd92e52b7a02f58620a03156902f9f91be57ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-engagement-on-android"></a><span data-ttu-id="8085e-103">Интеграция службы Engagement на Android</span><span class="sxs-lookup"><span data-stu-id="8085e-103">How to Integrate Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8085e-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="8085e-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="8085e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="8085e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="8085e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="8085e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="8085e-107">Android</span><span class="sxs-lookup"><span data-stu-id="8085e-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="8085e-108">Эта процедура описывает самый простой способ активации функции аналитики и мониторинга службы Engagement в приложении Android.</span><span class="sxs-lookup"><span data-stu-id="8085e-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Android application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8085e-109">Минимальный уровень пакета API SDK Android должен быть 10 или выше (Android 2.3.3 ил выше).</span><span class="sxs-lookup"><span data-stu-id="8085e-109">Your minimum Android SDK API level must be 10 or higher (Android 2.3.3 or higher).</span></span>
> 
> 

<span data-ttu-id="8085e-110">Следующих действий достаточно для активации отчета журналов, который необходим при вычислении всех статистических данных о пользователях, сеансах, действиях сбоях и технических проблемах.</span><span class="sxs-lookup"><span data-stu-id="8085e-110">The following steps are enough to activates the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="8085e-111">Отчеты по журналам, необходимые для вычисления других статистических данных (например, касающихся событий, ошибок и заданий), требуется создавать вручную с помощью API Служб мобильного взаимодействия (см. статью [Использование API Служб мобильного взаимодействия в Android](mobile-engagement-android-use-engagement-api.md)), так как эти статистические данные зависят от приложения.</span><span class="sxs-lookup"><span data-stu-id="8085e-111">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Android](mobile-engagement-android-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-and-service-into-your-android-project"></a><span data-ttu-id="8085e-112">Внедрение пакета SDK Engagement и службы в проект Android</span><span class="sxs-lookup"><span data-stu-id="8085e-112">Embed the Engagement SDK and service into your Android project</span></span>
<span data-ttu-id="8085e-113">Скачайте пакет Android SDK [отсюда](https://aka.ms/vq9mfn). Поместите `mobile-engagement-VERSION.jar` в папку `libs` вашего проекта Android (создайте папку libs, если она еще не создана).</span><span class="sxs-lookup"><span data-stu-id="8085e-113">Download the Android SDK from [here](https://aka.ms/vq9mfn) Get `mobile-engagement-VERSION.jar` and put them into the `libs` folder of your Android project (create the libs folder if it does not exist yet).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8085e-114">При создании пакета приложения с помощью ProGuard необходимо сохранить некоторые классы.</span><span class="sxs-lookup"><span data-stu-id="8085e-114">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="8085e-115">Можно использовать следующие фрагменты кода конфигурации:</span><span class="sxs-lookup"><span data-stu-id="8085e-115">You can use the following configuration snippet:</span></span>
> 
> <span data-ttu-id="8085e-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span><span class="sxs-lookup"><span data-stu-id="8085e-116">-keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {</span></span>
> 
> <span data-ttu-id="8085e-117"><methods>; }</span><span class="sxs-lookup"><span data-stu-id="8085e-117"><methods>; }</span></span>
> 
> 

<span data-ttu-id="8085e-118">Укажите строку подключения Engagement, вызвав следующий метод в операции запуска.</span><span class="sxs-lookup"><span data-stu-id="8085e-118">Specify your Engagement connection string by calling the following method in the launcher activity:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="8085e-119">Теперь строка подключения для приложения отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="8085e-119">The connection string for your application is displayed on Azure Portal.</span></span>

* <span data-ttu-id="8085e-120">Если она отсутствует, добавьте следующие разрешения Android (перед тегом `<application>`):</span><span class="sxs-lookup"><span data-stu-id="8085e-120">If missing, add the following Android permissions (before the `<application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* <span data-ttu-id="8085e-121">Добавьте следующий раздел (между тегами `<application>` и `</application>`):</span><span class="sxs-lookup"><span data-stu-id="8085e-121">Add the following section (between the `<application>` and `</application>` tags):</span></span>
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* <span data-ttu-id="8085e-122">Замените `<Your application name>` на имя вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="8085e-122">Change `<Your application name>` by the name of your application.</span></span>

> [!TIP]
> <span data-ttu-id="8085e-123">Ключ `android:label` позволяет выбрать имя службы Engagement в том виде, в каком оно будет выводиться для конечных пользователей на экране "Работающие службы" их телефонов.</span><span class="sxs-lookup"><span data-stu-id="8085e-123">The `android:label` attribute allows you to choose the name of the Engagement service as it will appear to the end-users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="8085e-124">Рекомендуется задать для этого атрибута значение `"<Your application name>Service"` (например, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="8085e-124">It is recommended to set this attribute to `"<Your application name>Service"` (e.g. `"AcmeFunGameService"`).</span></span>
> 
> 

<span data-ttu-id="8085e-125">Задание атрибута `android:process` гарантирует, что служба Engagement будет запускаться в своем собственном процессе (запуск службы Engagement в одном процессе с приложением может привести к тому, что основной поток (поток пользовательского интерфейса) станет хуже реагировать).</span><span class="sxs-lookup"><span data-stu-id="8085e-125">Specifying the `android:process` attribute ensures that the Engagement service will run in its own process (running Engagement in the same process as your application will make your main/UI thread potentially less responsive).</span></span>

> [!NOTE]
> <span data-ttu-id="8085e-126">Любой код, помещаемый в `Application.onCreate()` и другие обратные вызовы приложения, будут выполняться для всех процессов приложения, включая службу Engagement.</span><span class="sxs-lookup"><span data-stu-id="8085e-126">Any code you place in `Application.onCreate()` and other application callbacks will be run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="8085e-127">При этом возможны нежелательные побочные эффекты (например, выделение ненужной памяти и потоки в процессе Engagement, повторяющиеся получатели рассылки или службы).</span><span class="sxs-lookup"><span data-stu-id="8085e-127">It may have unwanted side effects (like unneeded memory allocations and threads in the Engagement's process, duplicate broadcast receivers or services).</span></span>
> 
> 

<span data-ttu-id="8085e-128">При переопределении `Application.onCreate()` рекомендуется добавить следующий фрагмент кода в начало функции `Application.onCreate()`:</span><span class="sxs-lookup"><span data-stu-id="8085e-128">If you override `Application.onCreate()`, it's recommended to add the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

<span data-ttu-id="8085e-129">То же самое можно сделать для `Application.onTerminate()`, `Application.onLowMemory()` и `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="8085e-129">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()` and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="8085e-130">Вы можете также расширить `EngagementApplication` вместо расширения `Application`: обратный вызов `Application.onCreate()` проверяет процесс и вызывает `Application.onApplicationProcessCreate()` только в том случае, если текущий процесс не размещает службу Engagement. Эти же правила применяются к другим обратным вызовам.</span><span class="sxs-lookup"><span data-stu-id="8085e-130">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="basic-reporting"></a><span data-ttu-id="8085e-131">Упрощенные отчеты</span><span class="sxs-lookup"><span data-stu-id="8085e-131">Basic reporting</span></span>
### <a name="recommended-method-overload-your-activity-classes"></a><span data-ttu-id="8085e-132">Рекомендуемый метод: перегрузка классов `Activity`</span><span class="sxs-lookup"><span data-stu-id="8085e-132">Recommended method: overload your `Activity` classes</span></span>
<span data-ttu-id="8085e-133">Для активации отчетов всех журналов, которые требуются службе Engagement для вычисления статистических данных пользователей, действий, сбоев и технических проблем, достаточно сделать все подклассы `*Activity` наследуемыми из соответствующих классов `Engagement*Activity` (например, если устаревшее действие расширяет `ListActivity`, сделайте так, чтобы оно расширяло `EngagementListActivity`).</span><span class="sxs-lookup"><span data-stu-id="8085e-133">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you just have to make all your `*Activity` sub-classes inherit from the corresponding `Engagement*Activity` classes (e.g. if your legacy activity extends `ListActivity`, make it extends `EngagementListActivity`).</span></span>

<span data-ttu-id="8085e-134">**Без Engagement:**</span><span class="sxs-lookup"><span data-stu-id="8085e-134">**Without Engagement :**</span></span>

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

<span data-ttu-id="8085e-135">**С Engagement:**</span><span class="sxs-lookup"><span data-stu-id="8085e-135">**With Engagement :**</span></span>

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
> <span data-ttu-id="8085e-136">При использовании `EngagementListActivity` или `EngagementExpandableListActivity` необходимо обеспечить, чтобы любой вызов `requestWindowFeature(...);` выполнялся до вызова `super.onCreate(...);`, в противном случае произойдет сбой.</span><span class="sxs-lookup"><span data-stu-id="8085e-136">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash will occur.</span></span>
> 
> 

<span data-ttu-id="8085e-137">Эти классы можно найти в папке `src` и скопировать их в проект.</span><span class="sxs-lookup"><span data-stu-id="8085e-137">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="8085e-138">Данные классы также представлены в **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="8085e-138">The classes are also in the **JavaDoc**.</span></span>

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="8085e-139">Альтернативный метод: вызов `startActivity()` и `endActivity()` вручную</span><span class="sxs-lookup"><span data-stu-id="8085e-139">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="8085e-140">Если вы не можете перегружать классы `Activity` или не хотите этого делать, вы можете запускать и завершать действия, вызывая методы `EngagementAgent` напрямую.</span><span class="sxs-lookup"><span data-stu-id="8085e-140">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8085e-141">Пакет SDK для Android никогда не вызывает метод `endActivity()`, даже если приложение закрыто (на Android приложения фактически никогда не закрываются).</span><span class="sxs-lookup"><span data-stu-id="8085e-141">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are actually never closed).</span></span> <span data-ttu-id="8085e-142">Поэтому *настоятельно* рекомендуется вызывать метод `startActivity()` в обратном вызове `onResume` *всех* действий, а метод `endActivity()` в обратном вызове `onPause()` *всех* действий.</span><span class="sxs-lookup"><span data-stu-id="8085e-142">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="8085e-143">Это единственный способ гарантировать отсутствие утечки сеансов.</span><span class="sxs-lookup"><span data-stu-id="8085e-143">This is the only way to be sure that sessions will not be leaked.</span></span> <span data-ttu-id="8085e-144">Если наблюдается утечка сеанса, служба Engagement никогда не отключится от внутреннего сервера Engagement (так как служба остается подключенной до тех пор, пока сеанс находится в состоянии ожидания).</span><span class="sxs-lookup"><span data-stu-id="8085e-144">If a session is leaked, the Engagement service will never disconnect from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="8085e-145">Пример:</span><span class="sxs-lookup"><span data-stu-id="8085e-145">Here is an example:</span></span>

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

<span data-ttu-id="8085e-146">Этот пример очень похож на класс `EngagementActivity` и его варианты, исходный код которых предоставляется в папке `src`.</span><span class="sxs-lookup"><span data-stu-id="8085e-146">This example very similiar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="test"></a><span data-ttu-id="8085e-147">Тест</span><span class="sxs-lookup"><span data-stu-id="8085e-147">Test</span></span>
<span data-ttu-id="8085e-148">Теперь проверьте интеграцию, запустив мобильное приложение в эмуляторе или на устройстве и убедившись в том, что сеанс регистрируется на вкладке "Монитор".</span><span class="sxs-lookup"><span data-stu-id="8085e-148">Now please verify your integration by running your mobile app in an emulator or device and verifying that it registers a session on the Monitor tab.</span></span>

<span data-ttu-id="8085e-149">Следующие разделы необязательны.</span><span class="sxs-lookup"><span data-stu-id="8085e-149">The next sections are optional.</span></span>

## <a name="location-reporting"></a><span data-ttu-id="8085e-150">Отчеты о расположении</span><span class="sxs-lookup"><span data-stu-id="8085e-150">Location reporting</span></span>
<span data-ttu-id="8085e-151">Для того чтобы создавались отчеты о расположениях, необходимо добавить несколько строк конфигурации (между тегами `<application>` и `</application>`).</span><span class="sxs-lookup"><span data-stu-id="8085e-151">If you want locations to be reported, you need to add a few lines of configuration (between the `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="8085e-152">Отчеты о расположении отложенной области</span><span class="sxs-lookup"><span data-stu-id="8085e-152">Lazy area location reporting</span></span>
<span data-ttu-id="8085e-153">Отчеты о расположении отложенной области позволяют включать в отчеты страну, область и населенный пункт, связанные с устройствами.</span><span class="sxs-lookup"><span data-stu-id="8085e-153">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="8085e-154">Этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора ячейки или Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="8085e-154">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="8085e-155">Отчеты об области устройства выполняются максимум один раз за сеанс.</span><span class="sxs-lookup"><span data-stu-id="8085e-155">The device area is reported at most once per session.</span></span> <span data-ttu-id="8085e-156">GPS никогда не используется, и в результате этот тип отчета о расположении оказывает исключительно небольшое (если не сказать вообще не оказывает) воздействие на батарею.</span><span class="sxs-lookup"><span data-stu-id="8085e-156">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="8085e-157">Области в отчетах используются для вычисления географических статистических данных о пользователях, сеансах, событиях и ошибках.</span><span class="sxs-lookup"><span data-stu-id="8085e-157">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="8085e-158">Они также могут использоваться в качестве критерия для рекламных компаний Reach.</span><span class="sxs-lookup"><span data-stu-id="8085e-158">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="8085e-159">Чтобы включить отчет о приблизительном местоположении устройств, можно использовать конфигурацию, упомянутую ранее в этой процедуре:</span><span class="sxs-lookup"><span data-stu-id="8085e-159">To enable lazy area location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="8085e-160">Также необходимо добавить следующее разрешение, если оно отсутствует:</span><span class="sxs-lookup"><span data-stu-id="8085e-160">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="8085e-161">Вы также можете продолжить использовать команду ``ACCESS_FINE_LOCATION``, если она уже используется в приложении.</span><span class="sxs-lookup"><span data-stu-id="8085e-161">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="8085e-162">Отчет о расположении в реальном времени</span><span class="sxs-lookup"><span data-stu-id="8085e-162">Real time location reporting</span></span>
<span data-ttu-id="8085e-163">Отчет о расположении в реальном времени позволяет включать в отчет широту и долготу, связанные с устройствами.</span><span class="sxs-lookup"><span data-stu-id="8085e-163">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="8085e-164">По умолчанию такой тип отчета о расположении использует только сетевые расположения (на основе идентификатора ячейки или Wi-Fi). Этот отчет активен только тогда, когда приложение выполняется в фоновом режиме (т.е во время сеанса).</span><span class="sxs-lookup"><span data-stu-id="8085e-164">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="8085e-165">Расположения в реальном времени *НЕ* используются для вычисления статистических данных.</span><span class="sxs-lookup"><span data-stu-id="8085e-165">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="8085e-166">Единственное их назначение — дать возможность использовать критерий геозоны реального времени \<Reach-Audience-geofencing\> в рекламных кампаниях.</span><span class="sxs-lookup"><span data-stu-id="8085e-166">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="8085e-167">Чтобы включить отчет о местоположении устройств в реальном времени, можно использовать конфигурацию, упомянутую ранее в этой процедуре:</span><span class="sxs-lookup"><span data-stu-id="8085e-167">To enable real time location reporting, you can do it by using the configuration previously mentioned in this procedure :</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="8085e-168">Также необходимо добавить следующее разрешение, если оно отсутствует:</span><span class="sxs-lookup"><span data-stu-id="8085e-168">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="8085e-169">Вы также можете продолжить использовать команду ``ACCESS_FINE_LOCATION``, если она уже используется в приложении.</span><span class="sxs-lookup"><span data-stu-id="8085e-169">Or you can keep using ``ACCESS_FINE_LOCATION`` if you already use it in your application.</span></span>

#### <a name="gps-based-reporting"></a><span data-ttu-id="8085e-170">Отчеты на базе GPS</span><span class="sxs-lookup"><span data-stu-id="8085e-170">GPS based reporting</span></span>
<span data-ttu-id="8085e-171">По умолчанию отчеты о расположении в реальном времени используют только сетевые расположения.</span><span class="sxs-lookup"><span data-stu-id="8085e-171">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="8085e-172">Чтобы включить использование расположений на базе GPS (которые значительно точнее), используйте следующий объект конфигурации:</span><span class="sxs-lookup"><span data-stu-id="8085e-172">To enable the use of GPS based locations (which are far more precise), use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="8085e-173">Также необходимо добавить следующее разрешение, если оно отсутствует:</span><span class="sxs-lookup"><span data-stu-id="8085e-173">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="8085e-174">Отчет в фоновом режиме</span><span class="sxs-lookup"><span data-stu-id="8085e-174">Background reporting</span></span>
<span data-ttu-id="8085e-175">По умолчанию отчеты о расположении в реальном времени активны только тогда, когда приложения выполняются в фоновом режиме (т.е. во время сеанса).</span><span class="sxs-lookup"><span data-stu-id="8085e-175">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="8085e-176">Чтобы включить отчеты в фоновом режиме, используйте следующий объект конфигурации:</span><span class="sxs-lookup"><span data-stu-id="8085e-176">To enable the reporting also in background, use the configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="8085e-177">Когда приложение выполняется в фоновом режиме, в отчете показываются только расположения на основе сети, даже если включен GPS.</span><span class="sxs-lookup"><span data-stu-id="8085e-177">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
> 
> 

<span data-ttu-id="8085e-178">Отчет о расположении в фоновом режиме будет остановлен, если пользователь перезагружает устройство. Можно добавить следующий код, чтобы обеспечить его автоматический перезапуск во время загрузки:</span><span class="sxs-lookup"><span data-stu-id="8085e-178">The background location report will be stopped if the user reboots its device, you can add this to make it automatically restart at boot time:</span></span>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

<span data-ttu-id="8085e-179">Также необходимо добавить следующее разрешение, если оно отсутствует:</span><span class="sxs-lookup"><span data-stu-id="8085e-179">You also need to add the following permission if missing:</span></span>

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a><span data-ttu-id="8085e-180">Разрешения в Android M</span><span class="sxs-lookup"><span data-stu-id="8085e-180">Android M permissions</span></span>
<span data-ttu-id="8085e-181">Начиная с Android M, управление некоторыми разрешениями осуществляется в среде выполнения и требует согласия пользователя.</span><span class="sxs-lookup"><span data-stu-id="8085e-181">Starting with Android M, some permissions are managed at runtime and needs user approval.</span></span>

<span data-ttu-id="8085e-182">Разрешения среды выполнения будут по умолчанию отключены для новых установленных приложений, если планируется использовать API Android уровня 23.</span><span class="sxs-lookup"><span data-stu-id="8085e-182">The runtime permissions will be turned off by default for new app installations if you target Android API level 23.</span></span> <span data-ttu-id="8085e-183">В противном случае они будут включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8085e-183">Otherwise it will be turned on by default.</span></span>

<span data-ttu-id="8085e-184">Пользователь может включить или отключить эти разрешения в меню параметров устройства.</span><span class="sxs-lookup"><span data-stu-id="8085e-184">The user can enable/disable those permissions from the device settings menu.</span></span> <span data-ttu-id="8085e-185">Отключение разрешений в системном меню приводит к завершению фоновых процессов приложения. Это поведение системы, которое не влияет на возможность получения push-уведомлений в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="8085e-185">Turning off permissions from system menu kills background processes of the application, this is a system behavior and has no impact on ability to receive push in background.</span></span>

<span data-ttu-id="8085e-186">В контексте Служб мобильного взаимодействия утверждения в среде выполнения требуют следующие разрешения.</span><span class="sxs-lookup"><span data-stu-id="8085e-186">In the context of Mobile Engagement, the permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* <span data-ttu-id="8085e-187">`WRITE_EXTERNAL_STORAGE` (только если для него планируется использовать API Android уровня 23)</span><span class="sxs-lookup"><span data-stu-id="8085e-187">`WRITE_EXTERNAL_STORAGE` (only when targeting Android API level 23 for this one)</span></span>

<span data-ttu-id="8085e-188">Внешнее хранилище используется только для получения общей картины обработки рекламных кампаний.</span><span class="sxs-lookup"><span data-stu-id="8085e-188">The external storage is used only for Reach big picture feature.</span></span> <span data-ttu-id="8085e-189">Если пользователи сообщают вам, что это разрешение мешает в работе, вы можете его удалить, если оно использовалось только для Служб мобильного взаимодействия, но при этом также отключается компонент общей картины.</span><span class="sxs-lookup"><span data-stu-id="8085e-189">If you find asking users this permission to be disruptive, you can remove it if you used it only for Mobile Engagement but at the cost of disabling big picture feature.</span></span>

<span data-ttu-id="8085e-190">Что касается характеристик расположений, разрешения для пользователя следует запрашивать с помощью стандартного диалогового окна системы.</span><span class="sxs-lookup"><span data-stu-id="8085e-190">For the location features, you should request permissions to user using a standard system dialog.</span></span> <span data-ttu-id="8085e-191">В случае утверждения пользователем вам необходимо указать классу ``EngagementAgent`` о необходимости принятия этого изменения во внимание в реальном времени (в противном случае изменение будет обработано, когда пользователь в следующий раз запустит приложение).</span><span class="sxs-lookup"><span data-stu-id="8085e-191">If the user approves, you need to tell ``EngagementAgent`` to take that change into account in real time (otherwise the change will be processed the next time the user launches the application).</span></span>

<span data-ttu-id="8085e-192">Ниже приведен пример кода для использования в действии приложения для запроса разрешений и переадресации результата (если он положительный) в класс ``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="8085e-192">Here is a code sample to use in an activity of your application to request permissions and forward the result if positive to ``EngagementAgent``:</span></span>

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
         * Request location permission, but this won't explain why it is needed to the user.
         * The standard Android documentation explains with more details how to display a rationale activity to explain the user why the permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of the same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want to keep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence the request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a><span data-ttu-id="8085e-193">Расширенные отчеты</span><span class="sxs-lookup"><span data-stu-id="8085e-193">Advanced reporting</span></span>
<span data-ttu-id="8085e-194">Если вы хотите получать отчеты о событиях, ошибках и заданиях, относящихся к конкретному приложению, следует использовать API Engagement при помощи методов класса `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="8085e-194">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="8085e-195">Объект этого класса можно получить с помощью вызова статического метода `EngagementAgent.getInstance()` .</span><span class="sxs-lookup"><span data-stu-id="8085e-195">An object of this class can be retreived by calling the `EngagementAgent.getInstance()` static method.</span></span>

<span data-ttu-id="8085e-196">API службы Engagement позволяет использовать все расширенные возможности Engagement и подробно описывается в разделе "Использование API службы Engagement в Android" (а также в технической документации по классу `EngagementAgent` ).</span><span class="sxs-lookup"><span data-stu-id="8085e-196">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on Android (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="advanced-configuration-in-androidmanifestxml"></a><span data-ttu-id="8085e-197">Расширенная конфигурация (в AndroidManifest.xml)</span><span class="sxs-lookup"><span data-stu-id="8085e-197">Advanced configuration (in AndroidManifest.xml)</span></span>
### <a name="wake-locks"></a><span data-ttu-id="8085e-198">Блокировки пробуждения</span><span class="sxs-lookup"><span data-stu-id="8085e-198">Wake locks</span></span>
<span data-ttu-id="8085e-199">Если необходимо гарантировать отправку статистики в реальном времени при использовании Wi-Fi или при выключенном экране, добавьте следующее необязательное разрешение:</span><span class="sxs-lookup"><span data-stu-id="8085e-199">If you want to be sure that statistics are sent in real time when using Wifi or when the screen is off, add the following optional permission:</span></span>

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a><span data-ttu-id="8085e-200">Отчет о сбоях</span><span class="sxs-lookup"><span data-stu-id="8085e-200">Crash report</span></span>
<span data-ttu-id="8085e-201">Если вы хотите отключить отчеты о сбоях, добавьте следующий код (между тегами `<application>` и `</application>`):</span><span class="sxs-lookup"><span data-stu-id="8085e-201">If you want to disable crash reports, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="8085e-202">Пороговое значение пакета</span><span class="sxs-lookup"><span data-stu-id="8085e-202">Burst threshold</span></span>
<span data-ttu-id="8085e-203">По умолчанию служба Engagement ведет отчеты по журналам в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="8085e-203">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="8085e-204">Если приложение очень часто отправляет отчеты журналов, лучше заносить их в буфер и передавать все вместе через определенные промежутки времени (это называется пакетным режимом).</span><span class="sxs-lookup"><span data-stu-id="8085e-204">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the "burst mode").</span></span> <span data-ttu-id="8085e-205">Чтобы это сделать, добавьте следующий код (между тегами `<application>` и `</application>`):</span><span class="sxs-lookup"><span data-stu-id="8085e-205">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="8085e-206">Пакетный режим немного продлевает время работы батареи, но влияет на Engagement Monitor: время выполнения всех сеансов и заданий будет округляться до порогового значения пакета (таким образом, сеансы и задания, время выполнения которых короче, чем пороговое значение пакета, могут не отображаться).</span><span class="sxs-lookup"><span data-stu-id="8085e-206">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="8085e-207">Мы советуем использовать пороговое значение пакета не более чем 30 000 (30 с).</span><span class="sxs-lookup"><span data-stu-id="8085e-207">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="8085e-208">Время ожидания сеанса</span><span class="sxs-lookup"><span data-stu-id="8085e-208">Session timeout</span></span>
<span data-ttu-id="8085e-209">По умолчанию сеанс завершается через 10 секунд после последнего действия (что обычно происходит при нажатии кнопки Home или Назад, при переводе телефона в ждущий режим или при переходе к другому приложению).</span><span class="sxs-lookup"><span data-stu-id="8085e-209">By default, a session is ended 10s after the end of its last activity (which usually occurs by pressing the Home or Back key, by setting the phone idle or by jumping into another application).</span></span> <span data-ttu-id="8085e-210">Это позволяет избежать разбиения сеанса каждый раз, когда пользователь выходи из приложения и возвращается в него очень быстро (это может наблюдаться при выборе изображения, проверке уведомления и т.д.).</span><span class="sxs-lookup"><span data-stu-id="8085e-210">This is to avoid a session split each time the user exit and return to the application very quickly (which can happen when he pick up a image, check a notification, etc.).</span></span> <span data-ttu-id="8085e-211">Вам может потребоваться изменить данный параметр.</span><span class="sxs-lookup"><span data-stu-id="8085e-211">You may want to modify this parameter.</span></span> <span data-ttu-id="8085e-212">Чтобы это сделать, добавьте следующий код (между тегами `<application>` и `</application>`):</span><span class="sxs-lookup"><span data-stu-id="8085e-212">To do so, add this (between the `<application>` and `</application>` tags):</span></span>

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="8085e-213">Выключение отчетов журналов</span><span class="sxs-lookup"><span data-stu-id="8085e-213">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="8085e-214">Использование вызова метода</span><span class="sxs-lookup"><span data-stu-id="8085e-214">Using a method call</span></span>
<span data-ttu-id="8085e-215">Если необходимо, чтобы служба Engagement перестала отправлять журналы, можно вызвать:</span><span class="sxs-lookup"><span data-stu-id="8085e-215">If you want Engagement to stop sending logs, you can call:</span></span>

            EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="8085e-216">Этот вызов является постоянным: он использует файл общих параметров.</span><span class="sxs-lookup"><span data-stu-id="8085e-216">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="8085e-217">Если служба Engagement активна, вызывается эта функция. Для остановки службы может потребоваться около 1 минуты.</span><span class="sxs-lookup"><span data-stu-id="8085e-217">If Engagement is active when you call this function, it may take 1 minute for the service to stop.</span></span> <span data-ttu-id="8085e-218">Однако в этом случае служба совсем не будет запускаться при следующем запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="8085e-218">However it won't launch the service at all the next time you launch the application.</span></span>

<span data-ttu-id="8085e-219">Вы можете снова включить журнал отчетов путем вызова той же функции с `true`.</span><span class="sxs-lookup"><span data-stu-id="8085e-219">You can enable log reporting again by calling the same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="8085e-220">Интеграция в собственное `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="8085e-220">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="8085e-221">Вместо вызова этой функции вы можете интегрировать данный параметр непосредственно в существующее `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="8085e-221">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="8085e-222">Можно настроить Engagement для использования файла настроек (с нужным режимом) в файле `AndroidManifest.xml` с `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="8085e-222">You can configure Engagement to use your preferences file (with the desired mode) in the `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="8085e-223">Ключ `engagement:agent:settings:name` используется для определения имени общего файла настроек.</span><span class="sxs-lookup"><span data-stu-id="8085e-223">The `engagement:agent:settings:name` key is used to define the name of the shared preferences file.</span></span>
* <span data-ttu-id="8085e-224">Ключ `engagement:agent:settings:mode` определяет режим общего файла настроек. Следует использовать тот же режим, что и в `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="8085e-224">The `engagement:agent:settings:mode` key is used to define the mode of the shared preferences file, you should use the same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="8085e-225">Режим должен передаваться в виде числа: при использовании сочетания постоянных флагов в коде необходимо проверить общее значение.</span><span class="sxs-lookup"><span data-stu-id="8085e-225">The mode must be passed as a number: if you are using a combination of constant flags in your code, check the total value.</span></span>

<span data-ttu-id="8085e-226">Служба Engagement всегда использует логический ключ `engagement:key` в файле настроек для управления данным параметром.</span><span class="sxs-lookup"><span data-stu-id="8085e-226">Engagement always use the `engagement:key` boolean key within the preferences file for managing this setting.</span></span>

<span data-ttu-id="8085e-227">В следующем примере `AndroidManifest.xml` показаны значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="8085e-227">The following example of `AndroidManifest.xml` shows the default values:</span></span>

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

<span data-ttu-id="8085e-228">Затем можно добавить `CheckBoxPreference` в макет параметров, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="8085e-228">Then you can add a `CheckBoxPreference` in your preference layout like the following one:</span></span>

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
