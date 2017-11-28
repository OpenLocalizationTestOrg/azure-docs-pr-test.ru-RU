---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 11618586-c709-49ca-bcd8-745323ff1af6
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: df5c82812fe0a242eaa5df8c906030237215b7eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="d38dd-103">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="d38dd-103">Upgrade procedures</span></span>
<span data-ttu-id="d38dd-104">Если уже имеется встроенный более старой версии нашего пакета SDK в приложение, у вас есть следующие точки, при обновлении hello SDK hello tooconsider.</span><span class="sxs-lookup"><span data-stu-id="d38dd-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="d38dd-105">Вы можете иметь toofollow несколько процедур если пропущены несколько версий пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="d38dd-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="d38dd-106">Например, если выполняется миграция из 1.4.0 too1.6.0, у вас есть toofirst выполните hello» из 1.4.0 too1.5.0» процедуры, а затем hello» из 1.5.0 too1.6.0» процедуры.</span><span class="sxs-lookup"><span data-stu-id="d38dd-106">For example if you migrate from 1.4.0 too1.6.0 you have toofirst follow hello "from 1.4.0 too1.5.0" procedure then hello "from 1.5.0 too1.6.0" procedure.</span></span>

<span data-ttu-id="d38dd-107">Какую бы версию hello обновления, у вас есть tooreplace hello `mobile-engagement-VERSION.jar` с hello новый.</span><span class="sxs-lookup"><span data-stu-id="d38dd-107">Whatever hello version you upgrade from, you have tooreplace hello `mobile-engagement-VERSION.jar` with hello new one.</span></span>

## <a name="from-420-too421"></a><span data-ttu-id="d38dd-108">Из 4.2.0 too4.2.1</span><span class="sxs-lookup"><span data-stu-id="d38dd-108">From 4.2.0 too4.2.1</span></span>
<span data-ttu-id="d38dd-109">Фактически это действие можно выполнить в любой версии пакета SDK для hello, он улучшения безопасности при интеграции Reach действий.</span><span class="sxs-lookup"><span data-stu-id="d38dd-109">This step can actually be done on any version of hello SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="d38dd-110">Теперь вы должны добавить `exported="false"` tooall Reach действий.</span><span class="sxs-lookup"><span data-stu-id="d38dd-110">You should now add `exported="false"` tooall Reach activities.</span></span>

<span data-ttu-id="d38dd-111">Действия модуля Reach должны выглядеть в `AndroidManifest.xml`следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d38dd-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
              </intent-filter>
            </activity>
            <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

## <a name="from-400-too410"></a><span data-ttu-id="d38dd-112">Из 4.0.0 too4.1.0</span><span class="sxs-lookup"><span data-stu-id="d38dd-112">From 4.0.0 too4.1.0</span></span>
<span data-ttu-id="d38dd-113">Hello SDK теперь дескриптор новый модель разрешений с Android M.</span><span class="sxs-lookup"><span data-stu-id="d38dd-113">hello SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="d38dd-114">Если вы используете характеристики расположений или общие уведомления, ознакомьтесь с [этим разделом](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="d38dd-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="d38dd-115">В дополнение к этому toohello новой модели разрешений, добавлена поддержка настройки расположения компонентов во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d38dd-115">In addition toohello new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="d38dd-116">Мы по-прежнему совместимы с параметрами манифеста hello для расположения, но сейчас он устарел.</span><span class="sxs-lookup"><span data-stu-id="d38dd-116">We are still compatible with hello manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="d38dd-117">Конфигурация среды выполнения toouse, remove hello следующие разделы из вашего ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="d38dd-117">toouse runtime configuration, remove hello following sections from your ``AndroidManifest.xml``:</span></span>

    <meta-data
      android:name="engagement:locationReport:lazyArea"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:background"
      android:value="true"/>
    <meta-data
      android:name="engagement:locationReport:realTime:fine"
      android:value="true"/>

<span data-ttu-id="d38dd-118">и чтения [это обновляется процедуры](mobile-engagement-android-integrate-engagement.md#location-reporting) конфигурации среды выполнения toouse вместо него.</span><span class="sxs-lookup"><span data-stu-id="d38dd-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) toouse runtime configuration instead.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="d38dd-119">Из 3.0.0 too4.0.0</span><span class="sxs-lookup"><span data-stu-id="d38dd-119">From 3.0.0 too4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="d38dd-120">Системные push-уведомления</span><span class="sxs-lookup"><span data-stu-id="d38dd-120">Native push</span></span>
<span data-ttu-id="d38dd-121">Собственные Push-уведомления (GCM/ADM) теперь также используется для уведомлений приложения, необходимо настроить учетные данные собственной отправки hello для любого типа кампании push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="d38dd-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="d38dd-122">Если вы еще не сделали этого, следуйте [этой процедуре](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="d38dd-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="d38dd-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d38dd-123">AndroidManifest.xml</span></span>
<span data-ttu-id="d38dd-124">Возможности интеграции с Reach были изменены в ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="d38dd-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="d38dd-125">Замените это:</span><span class="sxs-lookup"><span data-stu-id="d38dd-125">Replace this:</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="d38dd-126">на</span><span class="sxs-lookup"><span data-stu-id="d38dd-126">By</span></span>

    <receiver
      android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
      android:exported="false">
      <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
        <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
      </intent-filter>
    </receiver>
    <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
      <intent-filter>
        <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
      </intent-filter>
    </receiver>

<span data-ttu-id="d38dd-127">Теперь при выборе объявления (текстового или с веб-содержимым) или опроса может отображаться экран загрузки.</span><span class="sxs-lookup"><span data-stu-id="d38dd-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="d38dd-128">У вас есть tooadd это для этих toowork кампаний в 4.0.0:</span><span class="sxs-lookup"><span data-stu-id="d38dd-128">You have tooadd this for those campaigns toowork in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="d38dd-129">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="d38dd-129">Resources</span></span>
<span data-ttu-id="d38dd-130">Внедрение новых hello `res/layout/engagement_loading.xml` файл в проект.</span><span class="sxs-lookup"><span data-stu-id="d38dd-130">Embed hello new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-too300"></a><span data-ttu-id="d38dd-131">Из 2.4.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="d38dd-131">From 2.4.0 too3.0.0</span></span>
<span data-ttu-id="d38dd-132">Hello ниже описаны как toomigrate SDK-интеграция с hello обновления Capptain предлагаемых Capptain SAS в приложение на платформе Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d38dd-132">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="d38dd-133">При переносе из более ранней версии, обратитесь к веб-сайт toomigrate hello Capptain too2.4.0 сначала, а затем примените hello после процедуры.</span><span class="sxs-lookup"><span data-stu-id="d38dd-133">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too2.4.0 first and then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d38dd-134">Capptain и мобильного охвата, не hello и теми же службами и процедуры, представленные ниже представлены только как toomigrate hello клиентское приложение hello.</span><span class="sxs-lookup"><span data-stu-id="d38dd-134">Capptain and Mobile Engagement are not hello same services, and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="d38dd-135">Миграция hello SDK в приложение hello не выполняют миграцию данных из hello Capptain toohello мобильного охвата серверов.</span><span class="sxs-lookup"><span data-stu-id="d38dd-135">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="d38dd-136">JAR-файл</span><span class="sxs-lookup"><span data-stu-id="d38dd-136">JAR file</span></span>
<span data-ttu-id="d38dd-137">Замените `capptain.jar` на `mobile-engagement-VERSION.jar` в папке `libs`.</span><span class="sxs-lookup"><span data-stu-id="d38dd-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="d38dd-138">Файлы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d38dd-138">Resource files</span></span>
<span data-ttu-id="d38dd-139">Каждый файл ресурсов, который мы создали (префиксом `capptain_`) toobe заменен hello новых (с префиксом `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="d38dd-139">Every resource file that we provided (prefixed by `capptain_`) has toobe replaced by hello new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="d38dd-140">Если настройки этих файлов имеется toore-применить настройки для новых файлов hello, **все идентификаторы hello в файлах ресурсов hello также были переименованы**.</span><span class="sxs-lookup"><span data-stu-id="d38dd-140">If you customized those files, you have toore-apply your customization on hello new files, **all hello identifiers in hello resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="d38dd-141">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="d38dd-141">Application ID</span></span>
<span data-ttu-id="d38dd-142">Теперь Engagement использует соединение строка tooconfigure hello SDK идентификаторы, такие как идентификатор приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d38dd-142">Now Engagement uses a connection string tooconfigure hello SDK identifiers such as hello application identifier.</span></span>

<span data-ttu-id="d38dd-143">У вас есть toouse `EngagementAgent.init` метод в операцией запуска следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d38dd-143">You have toouse `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="d38dd-144">Hello строку подключения для приложения отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d38dd-144">hello connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="d38dd-145">Удалите любой вызов слишком`CapptainAgent.configure` как `EngagementAgent.init` заменяет этот метод.</span><span class="sxs-lookup"><span data-stu-id="d38dd-145">Please remove any call too`CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="d38dd-146">Hello `appId` больше не могут быть настроены в `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="d38dd-146">hello `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="d38dd-147">Удалите этот раздел из `AndroidManifest.xml`, если он имеется:</span><span class="sxs-lookup"><span data-stu-id="d38dd-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="d38dd-148">API Java</span><span class="sxs-lookup"><span data-stu-id="d38dd-148">Java API</span></span>
<span data-ttu-id="d38dd-149">Каждый вызов tooany класс Java нашего пакета SDK содержит toobe переименовано; например `CapptainAgent.getInstance(this)` необходимо переименовать `EngagementAgent.getInstance(this)`, `extends CapptainActivity` необходимо переименовать `extends EngagementActivity` и т.д...</span><span class="sxs-lookup"><span data-stu-id="d38dd-149">Every call tooany Java class of our SDK has toobe renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="d38dd-150">Если были интегрированы с файлами предпочтений по умолчанию агента, имя файла по умолчанию hello теперь является `engagement.agent` и нажата клавиша hello `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="d38dd-150">If you were integrated with default agent preference files, hello default file name is now `engagement.agent` and hello key is `engagement:agent`.</span></span>

<span data-ttu-id="d38dd-151">При создании веб-объявления, hello связыватель Javascript теперь является `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="d38dd-151">When creating web announcements, hello Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="d38dd-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d38dd-152">AndroidManifest.xml</span></span>
<span data-ttu-id="d38dd-153">Много изменений произошло, hello службы больше не используется совместно и много получателей больше не может быть экспортирован.</span><span class="sxs-lookup"><span data-stu-id="d38dd-153">A lot of changes happened there, hello service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="d38dd-154">объявления Hello службы теперь проще; Удалите фильтр намерения hello и все метаданные внутри него и добавьте `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="d38dd-154">hello service declaration is now simpler; remove hello intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="d38dd-155">Кроме того, все является переименованный toouse обязательств.</span><span class="sxs-lookup"><span data-stu-id="d38dd-155">Plus everything is renamed toouse engagement.</span></span>

<span data-ttu-id="d38dd-156">Теперь это выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d38dd-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="d38dd-157">При необходимости журналы тестирования tooenable hello метаданных был перемещен тег toohello приложения и был переименован:</span><span class="sxs-lookup"><span data-stu-id="d38dd-157">When you want tooenable test logs, hello meta-data has now been moved toohello application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="d38dd-158">Все другие метаданные просто были переименованы, ниже приведен полный список hello (Конечно переименования только hello из них использовать):</span><span class="sxs-lookup"><span data-stu-id="d38dd-158">All other meta-data have just been renamed, here is hello full list (of course rename only hello ones you use):</span></span>

            <meta-data
              android:name="engagement:reportCrash"
              android:value="true"/>
            <meta-data
              android:name="engagement:sessionTimeout"
              android:value="10000"/>
            <meta-data
              android:name="engagement:burstThreshold"
              android:value="0"/>
            <meta-data
              android:name="engagement:connection:delay"
              android:value="0"/>
            <meta-data
              android:name="engagement:locationReport:lazyArea"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:background"
              android:value="false"/>
            <meta-data
              android:name="engagement:locationReport:realTime:fine"
              android:value="false"/>
            <meta-data
              android:name="engagement:agent:settings:name"
              android:value="engagement.agent"/>
            <meta-data
              android:name="engagement:agent:settings:mode"
              android:value="0"/>
            <meta-data
              android:name="engagement:gcm:sender"
              android:value="<YOUR_PROJECT_NUMBER>\n"/>
            <meta-data
              android:name="engagement:adm:register"
              android:value="true"/>
            <meta-data
              android:name="engagement:reach:notification:icon"
              android:value="<DRAWABLE_NAME_WITHOUT_EXTENSION>"/>

            <activity android:name="SomeActivityWithoutReachOverlay">
              <meta-data
                android:name="engagement:notification:overlay"
                android:value="false"/>
            </activity>

<span data-ttu-id="d38dd-159">Отслеживание Google Play и SmartAd был удален из пакета SDK достаточно tooremove это без замены:</span><span class="sxs-lookup"><span data-stu-id="d38dd-159">Google Play and SmartAd tracking has been removed from SDK you just have tooremove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="d38dd-160">действия Reach Hello, теперь объявляются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d38dd-160">hello Reach activities are now declared like this:</span></span>

            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/plain"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <data android:mimeType="text/html"/>
              </intent-filter>
            </activity>
            <activity
              android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity"
              android:theme="@android:style/Theme.Light">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT"/>
              </intent-filter>
            </activity>

<span data-ttu-id="d38dd-161">При наличии пользовательских действий Reach только toochange hello намерения действия toomatch требуется либо `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` или `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="d38dd-161">If you have custom Reach activities, you need only toochange hello intent actions toomatch either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="d38dd-162">Hello широковещательных получатели были переименованы и теперь добавьте `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="d38dd-162">hello broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="d38dd-163">Ниже приведен полный список hello hello приемники с новой спецификации hello, (Конечно переименования только hello тех, которые вы используете):</span><span class="sxs-lookup"><span data-stu-id="d38dd-163">Here is hello full list of hello receivers with hello new specification, (of course rename only hello ones you use):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver"
              android:exported="false">
              <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver"
              android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
              android:permission="com.amazon.device.messaging.permission.SEND">
              <intent-filter>
                <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
                <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
                <category android:name="<your_package_name>"/>
              </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementConnectionReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.CONNECTED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.DISCONNECTED"/>
              </intent-filter>
            </receiver>

            <receiver
              android:name="<your_sub_class_of_com.microsoft.azure.engagement.EngagementMessageReceiver.java>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.MESSAGE"/>
              </intent-filter>
            </receiver>

<span data-ttu-id="d38dd-164">Отслеживание получателя были удалены, их необходимо tooremove в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="d38dd-164">Tracking receiver has been removed, so you have tooremove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="d38dd-165">Обратите внимание, что объявления hello реализации hello широковещательных получателя **EngagementMessageReceiver** изменилось в hello `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="d38dd-165">Note that hello declaration of your implementation of hello broadcast receiver **EngagementMessageReceiver** has changed in hello `AndroidManifest.xml`.</span></span> <span data-ttu-id="d38dd-166">Это обусловлено toosend hello API и удаление произвольного XMPP сообщений из произвольных XMPP сущностей и hello API toosend и получения сообщений между устройства будут удалены.</span><span class="sxs-lookup"><span data-stu-id="d38dd-166">This is because hello API toosend and remove arbitrary XMPP messages from arbitrary XMPP entities and hello API toosend and receive messages between devices have been removed.</span></span> <span data-ttu-id="d38dd-167">Таким образом, у вас есть также hello toodelete следующие обратные вызовы из вашего **EngagementMessageReceiver** реализации:</span><span class="sxs-lookup"><span data-stu-id="d38dd-167">Thus, you have also toodelete hello following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="d38dd-168">и</span><span class="sxs-lookup"><span data-stu-id="d38dd-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="d38dd-169">затем удалить все вызовы в **EngagementAgent** для:</span><span class="sxs-lookup"><span data-stu-id="d38dd-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="d38dd-170">и</span><span class="sxs-lookup"><span data-stu-id="d38dd-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="d38dd-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="d38dd-171">Proguard</span></span>
<span data-ttu-id="d38dd-172">Ребрендинг приветствия правила теперь похожее может влиять proguard конфигурации:</span><span class="sxs-lookup"><span data-stu-id="d38dd-172">Proguard configuration can be impacted by rebranding, hello rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

