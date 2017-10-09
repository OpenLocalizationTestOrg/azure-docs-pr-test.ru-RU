---
title: "aaaLocation Reporting для Azure Mobile Engagement Android SDK"
description: "Описывает способ tooconfigure расположения отчетов для Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="d5f96-103">Создание отчетов о расположении для пакета SDK для Android в Службах мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="d5f96-103">Location Reporting for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5f96-104">Android</span><span class="sxs-lookup"><span data-stu-id="d5f96-104">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="d5f96-105">Описывается, как расположение toodo отчетов для приложения Android.</span><span class="sxs-lookup"><span data-stu-id="d5f96-105">This topic describes how toodo location reporting for your Android application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5f96-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d5f96-106">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a><span data-ttu-id="d5f96-107">Отчеты о расположении</span><span class="sxs-lookup"><span data-stu-id="d5f96-107">Location reporting</span></span>
<span data-ttu-id="d5f96-108">Если требуется сообщила toobe расположения, необходимо tooadd несколько строк конфигурации (между hello `<application>` и `</application>` теги).</span><span class="sxs-lookup"><span data-stu-id="d5f96-108">If you want locations toobe reported, you need tooadd a few lines of configuration (between hello `<application>` and `</application>` tags).</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="d5f96-109">Отчеты о расположении отложенной области</span><span class="sxs-lookup"><span data-stu-id="d5f96-109">Lazy area location reporting</span></span>
<span data-ttu-id="d5f96-110">Отчеты о местоположении неактивной области позволяет отчетов hello страны, региону и местоположению, связанных с устройствами.</span><span class="sxs-lookup"><span data-stu-id="d5f96-110">Lazy area location reporting enables reporting hello country, region, and locality associated with devices.</span></span> <span data-ttu-id="d5f96-111">Этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора ячейки или Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="d5f96-111">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="d5f96-112">Hello области устройства отображается только один раз за сеанс.</span><span class="sxs-lookup"><span data-stu-id="d5f96-112">hello device area is reported at most once per session.</span></span> <span data-ttu-id="d5f96-113">Hello GPS никогда не используется, и таким образом расположение отчета этого типа низкий влияет на hello батареи.</span><span class="sxs-lookup"><span data-stu-id="d5f96-113">hello GPS is never used, and thus this type of location report has low impact on hello battery.</span></span>

<span data-ttu-id="d5f96-114">Области отчета — используется toocompute географической статистические данные о пользователях, сеансах, события и ошибки.</span><span class="sxs-lookup"><span data-stu-id="d5f96-114">Reported areas are used toocompute geographic statistics about users, sessions, events, and errors.</span></span> <span data-ttu-id="d5f96-115">Они также могут использоваться в качестве критерия для рекламных компаний Reach.</span><span class="sxs-lookup"><span data-stu-id="d5f96-115">They can also be used as criterion in Reach campaigns.</span></span>

<span data-ttu-id="d5f96-116">Включить расположение неактивной области отчетов с помощью конфигурации hello, упомянутых выше в этой процедуре:</span><span class="sxs-lookup"><span data-stu-id="d5f96-116">You enable lazy area location reporting by using hello configuration previously mentioned in this procedure:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d5f96-117">Необходимо также toospecify разрешение расположение.</span><span class="sxs-lookup"><span data-stu-id="d5f96-117">You also need toospecify a location permission.</span></span> <span data-ttu-id="d5f96-118">В данном коде используется разрешение ``COARSE`` .</span><span class="sxs-lookup"><span data-stu-id="d5f96-118">This code uses ``COARSE`` permission:</span></span>

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

<span data-ttu-id="d5f96-119">Вместо него можно использовать ``ACCESS_FINE_LOCATION`` , если это требуется приложению.</span><span class="sxs-lookup"><span data-stu-id="d5f96-119">If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.</span></span>

### <a name="real-time-location-reporting"></a><span data-ttu-id="d5f96-120">Отчет о расположении в реальном времени</span><span class="sxs-lookup"><span data-stu-id="d5f96-120">Real-time location reporting</span></span>
<span data-ttu-id="d5f96-121">Отчеты о местоположении в реальном времени позволяет отчетов hello широты и долготы, связанных с устройствами.</span><span class="sxs-lookup"><span data-stu-id="d5f96-121">Real-time location reporting enables reporting hello latitude and longitude associated with devices.</span></span> <span data-ttu-id="d5f96-122">По умолчанию этот тип отчетов о расположении использует только сетевые расположения (на основе идентификатора соты или Wi-Fi).</span><span class="sxs-lookup"><span data-stu-id="d5f96-122">By default, this type of location reporting only uses network locations, based on Cell ID or WIFI.</span></span> <span data-ttu-id="d5f96-123">Hello отчетов активен только при запуске приложения hello в переднего плана (например, во время сеанса).</span><span class="sxs-lookup"><span data-stu-id="d5f96-123">hello reporting is only active when hello application runs in foreground (for example, during a session).</span></span>

<span data-ttu-id="d5f96-124">В режиме реального времени расположения: *не* используется toocompute статистики.</span><span class="sxs-lookup"><span data-stu-id="d5f96-124">Real-time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="d5f96-125">Их единственной целью является использование hello tooallow в режиме реального времени геозон \<Reach аудитории географическое зонирование\> критерий в кампаниях Reach.</span><span class="sxs-lookup"><span data-stu-id="d5f96-125">Their only purpose is tooallow hello use of real-time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="d5f96-126">в режиме реального времени расположение tooenable отчетов, добавьте строку из toowhere кода задаются строки подключения Engagement hello в операцией запуска hello.</span><span class="sxs-lookup"><span data-stu-id="d5f96-126">tooenable real-time location reporting, add a line of code toowhere you set hello Engagement connection string in hello launcher activity.</span></span> <span data-ttu-id="d5f96-127">результат Hello выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d5f96-127">hello result looks like hello following:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a><span data-ttu-id="d5f96-128">Отчеты на базе GPS</span><span class="sxs-lookup"><span data-stu-id="d5f96-128">GPS based reporting</span></span>
<span data-ttu-id="d5f96-129">По умолчанию отчеты о расположении в реальном времени используют только сетевые расположения.</span><span class="sxs-lookup"><span data-stu-id="d5f96-129">By default, real-time location reporting only uses network-based locations.</span></span> <span data-ttu-id="d5f96-130">Используйте hello tooenable расположений GPS, которые являются гораздо более точным, используйте hello объекта конфигурации:</span><span class="sxs-lookup"><span data-stu-id="d5f96-130">tooenable hello use of GPS-based locations, which are far more precise, use hello configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d5f96-131">Также необходим hello tooadd следующие разрешения, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="d5f96-131">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a><span data-ttu-id="d5f96-132">Отчет в фоновом режиме</span><span class="sxs-lookup"><span data-stu-id="d5f96-132">Background reporting</span></span>
<span data-ttu-id="d5f96-133">По умолчанию отчеты о местоположении в реальном времени активен только при запуске приложения hello в переднего плана (например, во время сеанса).</span><span class="sxs-lookup"><span data-stu-id="d5f96-133">By default, real-time location reporting is only active when hello application runs in foreground (for example, during a session).</span></span> <span data-ttu-id="d5f96-134">hello tooenable также отчетов в фоновом режиме, используйте этот объект конфигурации:</span><span class="sxs-lookup"><span data-stu-id="d5f96-134">tooenable hello reporting also in background, use this configuration object:</span></span>

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> <span data-ttu-id="d5f96-135">При запуске приложения hello в фоновом режиме, выводятся только на основе сетевого расположения, даже если включена hello GPS.</span><span class="sxs-lookup"><span data-stu-id="d5f96-135">When hello application runs in background, only network-based locations are reported, even if you enabled hello GPS.</span></span>
> 
> 

<span data-ttu-id="d5f96-136">Если пользователь hello перезагрузки устройства hello фона расположение отчета будет остановлена.</span><span class="sxs-lookup"><span data-stu-id="d5f96-136">If hello user reboots their device, hello background location report is stopped.</span></span> <span data-ttu-id="d5f96-137">toomake автоматический перезапуск во время загрузки, добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="d5f96-137">toomake it automatically restart at boot time, add this code.</span></span>

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

<span data-ttu-id="d5f96-138">Также необходим hello tooadd следующие разрешения, если они отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="d5f96-138">You also need tooadd hello following permission if missing:</span></span>

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a><span data-ttu-id="d5f96-139">Разрешения в Android M</span><span class="sxs-lookup"><span data-stu-id="d5f96-139">Android M permissions</span></span>
<span data-ttu-id="d5f96-140">Начиная с Android M, управление некоторыми разрешениями осуществляется в среде выполнения и требует согласия пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5f96-140">Starting with Android M, some permissions are managed at runtime and need user approval.</span></span>

<span data-ttu-id="d5f96-141">Если целевая Android API уровня 23 hello среды выполнения разрешения отключены по умолчанию для новых установок приложения.</span><span class="sxs-lookup"><span data-stu-id="d5f96-141">If you target Android API level 23, hello runtime permissions are turned off by default for new app installations.</span></span> <span data-ttu-id="d5f96-142">В противном случае они будут включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d5f96-142">Otherwise they are turned on by default.</span></span>

<span data-ttu-id="d5f96-143">Можно включить или отключить эти разрешения из меню параметров устройства hello.</span><span class="sxs-lookup"><span data-stu-id="d5f96-143">You can enable/disable those permissions from hello device settings menu.</span></span> <span data-ttu-id="d5f96-144">Отключение разрешений из меню системы hello разрывает hello фоновые процессы приложения hello, поведение системы, и никак не повлияет на возможность принудительной tooreceive в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="d5f96-144">Turning off permissions from hello system menu kills hello background processes of hello application, which is a system behavior, and has no impact on ability tooreceive push in background.</span></span>

<span data-ttu-id="d5f96-145">В контексте hello reporting расположение мобильного охвата требуются разрешения hello, требующих утверждения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d5f96-145">In hello context of Mobile Engagement location reporting, hello permissions that require approval at runtime are:</span></span>

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

<span data-ttu-id="d5f96-146">Запросите разрешения пользователя hello, с помощью стандартной системы диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="d5f96-146">Request permissions from hello user using a standard system dialog.</span></span> <span data-ttu-id="d5f96-147">Если пользователь hello утверждает, сообщите ``EngagementAgent`` tootake, можно превратить в учетной записи в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="d5f96-147">If hello user approves, tell ``EngagementAgent`` tootake that change into account in real-time.</span></span> <span data-ttu-id="d5f96-148">В противном случае изменения hello — обработанные hello Далее время hello запускает hello приложение пользователя.</span><span class="sxs-lookup"><span data-stu-id="d5f96-148">Otherwise hello change is processed hello next time hello user launches hello application.</span></span>

<span data-ttu-id="d5f96-149">Ниже приведен toouse пример кода в действии разрешения toorequest приложения и результат прямого hello при положительном слишком``EngagementAgent``:</span><span class="sxs-lookup"><span data-stu-id="d5f96-149">Here is a code sample toouse in an activity of your application toorequest permissions and forward hello result if positive too``EngagementAgent``:</span></span>

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
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
