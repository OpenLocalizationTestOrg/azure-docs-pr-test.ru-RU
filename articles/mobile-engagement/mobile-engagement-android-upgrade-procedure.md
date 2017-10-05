---
title: "Интеграция пакета Android SDK для Служб мобильного взаимодействия Azure"
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
ms.openlocfilehash: 1f047f93fa8bc852b28c86e91d0c007a94fb4299
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="743c9-103">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="743c9-103">Upgrade procedures</span></span>
<span data-ttu-id="743c9-104">Если вы уже интегрировали в приложение старую версию пакета SDK, при обновлении пакета SDK необходимо учитывать следующее.</span><span class="sxs-lookup"><span data-stu-id="743c9-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="743c9-105">Если вы пропустили несколько версий пакета SDK, вам понадобиться выполнить несколько процедур.</span><span class="sxs-lookup"><span data-stu-id="743c9-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="743c9-106">Например, при миграции из версии 1.4.0 в 1.6.0, необходимо сначала выполнить процедуру "из версии 1.4.0 в 1.5.0", а затем процедуру "из версии 1.5.0 в 1.6.0".</span><span class="sxs-lookup"><span data-stu-id="743c9-106">For example if you migrate from 1.4.0 to 1.6.0 you have to first follow the "from 1.4.0 to 1.5.0" procedure then the "from 1.5.0 to 1.6.0" procedure.</span></span>

<span data-ttu-id="743c9-107">Независимо от того, с какой версии выполняется обновление, необходимо заменить `mobile-engagement-VERSION.jar` на новую версию.</span><span class="sxs-lookup"><span data-stu-id="743c9-107">Whatever the version you upgrade from, you have to replace the `mobile-engagement-VERSION.jar` with the new one.</span></span>

## <a name="from-420-to-421"></a><span data-ttu-id="743c9-108">Версии с 4.2.0 до 4.2.1</span><span class="sxs-lookup"><span data-stu-id="743c9-108">From 4.2.0 to 4.2.1</span></span>
<span data-ttu-id="743c9-109">Фактически это действие можно выполнить в любой версии пакета SDK — это повышает безопасность при интеграции действий модуля Reach.</span><span class="sxs-lookup"><span data-stu-id="743c9-109">This step can actually be done on any version of the SDK, its a security improvement when you integrate Reach activities.</span></span>

<span data-ttu-id="743c9-110">Теперь ко всем действиям модуля Reach необходимо добавлять `exported="false"` .</span><span class="sxs-lookup"><span data-stu-id="743c9-110">You should now add `exported="false"` to all Reach activities.</span></span>

<span data-ttu-id="743c9-111">Действия модуля Reach должны выглядеть в `AndroidManifest.xml`следующим образом.</span><span class="sxs-lookup"><span data-stu-id="743c9-111">Reach activities should now look like this on your `AndroidManifest.xml`:</span></span>

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

## <a name="from-400-to-410"></a><span data-ttu-id="743c9-112">С версии 4.0.0 до версии 4.1.0</span><span class="sxs-lookup"><span data-stu-id="743c9-112">From 4.0.0 to 4.1.0</span></span>
<span data-ttu-id="743c9-113">Пакет SDK теперь обрабатывает новую модель разрешений из Android M.</span><span class="sxs-lookup"><span data-stu-id="743c9-113">The SDK now handle new permission model from Android M.</span></span>

<span data-ttu-id="743c9-114">Если вы используете характеристики расположений или общие уведомления, ознакомьтесь с [этим разделом](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="743c9-114">If you use location features or big picture notifications please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>

<span data-ttu-id="743c9-115">Помимо новой модели разрешений, теперь поддерживается настройка характеристик расположений во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="743c9-115">In addition to the new permission model, we now support configuring location features at runtime.</span></span>
<span data-ttu-id="743c9-116">Кроме того, по-прежнему обеспечивается поддержка совместимости с параметрами манифеста для расположения, но сейчас эта возможность устарела.</span><span class="sxs-lookup"><span data-stu-id="743c9-116">We are still compatible with the manifest parameters for location but it's now deprecated.</span></span> <span data-ttu-id="743c9-117">Чтобы использовать конфигурацию среды выполнения, удалите следующие разделы из ``AndroidManifest.xml``:</span><span class="sxs-lookup"><span data-stu-id="743c9-117">To use runtime configuration, remove the following sections from your ``AndroidManifest.xml``:</span></span>

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

<span data-ttu-id="743c9-118">и ознакомьтесь с [этой обновленной процедурой](mobile-engagement-android-integrate-engagement.md#location-reporting) , чтобы вместо этого использовать конфигурацию среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="743c9-118">and read [this updated procedure](mobile-engagement-android-integrate-engagement.md#location-reporting) to use runtime configuration instead.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="743c9-119">С версии 3.0.0 до версии 4.0.0</span><span class="sxs-lookup"><span data-stu-id="743c9-119">From 3.0.0 to 4.0.0</span></span>
### <a name="native-push"></a><span data-ttu-id="743c9-120">Системные push-уведомления</span><span class="sxs-lookup"><span data-stu-id="743c9-120">Native push</span></span>
<span data-ttu-id="743c9-121">Системные push-уведомления (GCM/ADM) теперь также используются для уведомлений из приложений, поэтому их учетные данные необходимо задавать для всех типов кампаний push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="743c9-121">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>

<span data-ttu-id="743c9-122">Если вы еще не сделали этого, следуйте [этой процедуре](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span><span class="sxs-lookup"><span data-stu-id="743c9-122">If not already done please follow [this procedure](mobile-engagement-android-integrate-engagement-reach.md#native-push).</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="743c9-123">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="743c9-123">AndroidManifest.xml</span></span>
<span data-ttu-id="743c9-124">Возможности интеграции с Reach были изменены в ``AndroidManifest.xml``.</span><span class="sxs-lookup"><span data-stu-id="743c9-124">Reach integration has been modified in ``AndroidManifest.xml``.</span></span>

<span data-ttu-id="743c9-125">Замените это:</span><span class="sxs-lookup"><span data-stu-id="743c9-125">Replace this:</span></span>

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

<span data-ttu-id="743c9-126">на</span><span class="sxs-lookup"><span data-stu-id="743c9-126">By</span></span>

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

<span data-ttu-id="743c9-127">Теперь при выборе объявления (текстового или с веб-содержимым) или опроса может отображаться экран загрузки.</span><span class="sxs-lookup"><span data-stu-id="743c9-127">There is possibly a loading screen now when you click on an announcement (with text/web content) or a poll.</span></span>
<span data-ttu-id="743c9-128">Чтобы кампании работали в версии 4.0.0, необходимо добавить этот код:</span><span class="sxs-lookup"><span data-stu-id="743c9-128">You have to add this for those campaigns to work in 4.0.0:</span></span>

    <activity
      android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity"
      android:theme="@android:style/Theme.Dialog">
      <intent-filter>
        <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
        <category android:name="android.intent.category.DEFAULT"/>
      </intent-filter>
    </activity>

### <a name="resources"></a><span data-ttu-id="743c9-129">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="743c9-129">Resources</span></span>
<span data-ttu-id="743c9-130">Внедрите новый файл `res/layout/engagement_loading.xml` в проект.</span><span class="sxs-lookup"><span data-stu-id="743c9-130">Embed the new `res/layout/engagement_loading.xml` file into your project.</span></span>

## <a name="from-240-to-300"></a><span data-ttu-id="743c9-131">Из версии 2.4.0 в 3.0.0</span><span class="sxs-lookup"><span data-stu-id="743c9-131">From 2.4.0 to 3.0.0</span></span>
<span data-ttu-id="743c9-132">Ниже описан процесс переноса интеграции пакета SDK из службы Capptain от Capptain SAS в приложение Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="743c9-132">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> <span data-ttu-id="743c9-133">При миграции с более ранней версии сначала ознакомьтесь с информацией о переносе на версию 2.4.0 на веб-сайте Capptain, а затем примените следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="743c9-133">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 2.4.0 first and then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="743c9-134">Службы Capptain и Службы мобильного взаимодействия Azure отличаются друг от друга. В представленных ниже процедурах описывается способ переноса только для клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="743c9-134">Capptain and Mobile Engagement are not the same services, and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="743c9-135">При переносе пакета SDK в приложение данные НЕ будут перенесены с серверов Capptain на серверы Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="743c9-135">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers.</span></span>
> 
> 

### <a name="jar-file"></a><span data-ttu-id="743c9-136">JAR-файл</span><span class="sxs-lookup"><span data-stu-id="743c9-136">JAR file</span></span>
<span data-ttu-id="743c9-137">Замените `capptain.jar` на `mobile-engagement-VERSION.jar` в папке `libs`.</span><span class="sxs-lookup"><span data-stu-id="743c9-137">Replace `capptain.jar` by `mobile-engagement-VERSION.jar` in your `libs` folder.</span></span>

### <a name="resource-files"></a><span data-ttu-id="743c9-138">Файлы ресурсов</span><span class="sxs-lookup"><span data-stu-id="743c9-138">Resource files</span></span>
<span data-ttu-id="743c9-139">Каждый предоставленный файл ресурсов (с префиксом `capptain_`) должен быть заменен на новый (с префиксом `engagement_`).</span><span class="sxs-lookup"><span data-stu-id="743c9-139">Every resource file that we provided (prefixed by `capptain_`) has to be replaced by the new ones (prefixed with `engagement_`).</span></span>

<span data-ttu-id="743c9-140">Если вы настроили эти файлы, потребуется повторно применить настройку к новым файлам. **Все идентификаторы файлов ресурсов также были переименованы.**</span><span class="sxs-lookup"><span data-stu-id="743c9-140">If you customized those files, you have to re-apply your customization on the new files, **all the identifiers in the resource files have also been renamed**.</span></span>

### <a name="application-id"></a><span data-ttu-id="743c9-141">Идентификатор приложения</span><span class="sxs-lookup"><span data-stu-id="743c9-141">Application ID</span></span>
<span data-ttu-id="743c9-142">Теперь служба Engagement использует строку подключения для настройки идентификаторов пакета SDK, таких как идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="743c9-142">Now Engagement uses a connection string to configure the SDK identifiers such as the application identifier.</span></span>

<span data-ttu-id="743c9-143">Необходимо использовать метод `EngagementAgent.init` в действии запуска следующим образом:</span><span class="sxs-lookup"><span data-stu-id="743c9-143">You have to use `EngagementAgent.init` method in your launcher activity like this:</span></span>

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

<span data-ttu-id="743c9-144">Теперь строка подключения для приложения отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="743c9-144">The connection string for your application is displayed on Azure Portal.</span></span>

<span data-ttu-id="743c9-145">Удалите все вызовы к `CapptainAgent.configure`, так как `EngagementAgent.init` заменяет этот метод.</span><span class="sxs-lookup"><span data-stu-id="743c9-145">Please remove any call to `CapptainAgent.configure` as `EngagementAgent.init` replaces that method.</span></span>

<span data-ttu-id="743c9-146">`appId` больше нельзя настраивать с помощью `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="743c9-146">The `appId` can no longer be configured using `AndroidManifest.xml`.</span></span>

<span data-ttu-id="743c9-147">Удалите этот раздел из `AndroidManifest.xml`, если он имеется:</span><span class="sxs-lookup"><span data-stu-id="743c9-147">Please remove this section from your `AndroidManifest.xml` if you have it:</span></span>

            <meta-data android:name="capptain:appId" android:value="<YOUR_APPID>"/>

### <a name="java-api"></a><span data-ttu-id="743c9-148">API Java</span><span class="sxs-lookup"><span data-stu-id="743c9-148">Java API</span></span>
<span data-ttu-id="743c9-149">Любой вызов любого класса Java пакета SDK должен быть переименован, например `CapptainAgent.getInstance(this)` нужно переименовать в `EngagementAgent.getInstance(this)`, `extends CapptainActivity` нужно переименовать в `extends EngagementActivity` и т. д.</span><span class="sxs-lookup"><span data-stu-id="743c9-149">Every call to any Java class of our SDK has to be renamed; for example, `CapptainAgent.getInstance(this)` must be renamed `EngagementAgent.getInstance(this)`, `extends CapptainActivity` must be renamed `extends EngagementActivity` etc...</span></span>

<span data-ttu-id="743c9-150">Если была выполнена интеграция с файлами параметров агента по умолчанию, то теперь имя файла по умолчанию — `engagement.agent`, а ключ — `engagement:agent`.</span><span class="sxs-lookup"><span data-stu-id="743c9-150">If you were integrated with default agent preference files, the default file name is now `engagement.agent` and the key is `engagement:agent`.</span></span>

<span data-ttu-id="743c9-151">При создании веб-объявлений теперь используется модуль привязки Javascript `engagementReachContent`.</span><span class="sxs-lookup"><span data-stu-id="743c9-151">When creating web announcements, the Javascript binder is now `engagementReachContent`.</span></span>

### <a name="androidmanifestxml"></a><span data-ttu-id="743c9-152">AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="743c9-152">AndroidManifest.xml</span></span>
<span data-ttu-id="743c9-153">Выполнено много изменений. Служба больше не используется совместно, а большое количество получателей больше нельзя экспортировать.</span><span class="sxs-lookup"><span data-stu-id="743c9-153">A lot of changes happened there, the service is not shared anymore, and a lot of receivers are not exportable anymore.</span></span>

<span data-ttu-id="743c9-154">Объявление службы теперь упрощено, удален фильтр намерений и все метаданные в нем, а также добавлен `exportable=false`.</span><span class="sxs-lookup"><span data-stu-id="743c9-154">The service declaration is now simpler; remove the intent filter and all meta-data inside it, and add `exportable=false`.</span></span>

<span data-ttu-id="743c9-155">Кроме того, все переименовано для использования службы Engagement.</span><span class="sxs-lookup"><span data-stu-id="743c9-155">Plus everything is renamed to use engagement.</span></span>

<span data-ttu-id="743c9-156">Теперь это выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="743c9-156">It now looks like:</span></span>

            <service
              android:name="com.microsoft.azure.engagement.service.EngagementService"
              android:exported="false"
              android:label="<Your application name>Service"
              android:process=":Engagement"/>

<span data-ttu-id="743c9-157">При необходимости включить журналы тестирования метаданные теперь перемещаются в тег приложения и переименовываются:</span><span class="sxs-lookup"><span data-stu-id="743c9-157">When you want to enable test logs, the meta-data has now been moved to the application tag and has been renamed:</span></span>

            <application>

              <meta-data android:name="engagement:log:test" android:value="true" />

              <service/>

            </application>

<span data-ttu-id="743c9-158">Все остальные метаданные только что были переименованы. Здесь приводится полный список (разумеется, следует переименовывать только те, которые используются):</span><span class="sxs-lookup"><span data-stu-id="743c9-158">All other meta-data have just been renamed, here is the full list (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="743c9-159">Отслеживание Google Play и SmartAd удалено из пакета SDK. Необходимо просто удалить это без замены.</span><span class="sxs-lookup"><span data-stu-id="743c9-159">Google Play and SmartAd tracking has been removed from SDK you just have to remove this without replacement:</span></span>

            <meta-data 
                android:name="capptain:track:installReferrerForwardList"
                android:value="com.class1,com.class2"/>
            <meta-data
                android:name="capptain:track:adservers"
                android:value="smartad" />

<span data-ttu-id="743c9-160">Действия модуля Reach теперь объявляются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="743c9-160">The Reach activities are now declared like this:</span></span>

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

<span data-ttu-id="743c9-161">Если действия модуля Reach настроены, необходимо изменить только действия намерений для соответствия `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` или `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span><span class="sxs-lookup"><span data-stu-id="743c9-161">If you have custom Reach activities, you need only to change the intent actions to match either `com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT` or `com.microsoft.azure.engagement.reach.intent.action.POLL`.</span></span>

<span data-ttu-id="743c9-162">Получатели рассылок были переименованы, кроме того, было добавлено `exported=false`.</span><span class="sxs-lookup"><span data-stu-id="743c9-162">The broadcast receivers have been renamed, plus we now add `exported=false`.</span></span> <span data-ttu-id="743c9-163">Ниже приводится полный список получателей с новой спецификацией (разумеется, необходимо переименовывать только тех, которые используются):</span><span class="sxs-lookup"><span data-stu-id="743c9-163">Here is the full list of the receivers with the new specification, (of course rename only the ones you use):</span></span>

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

<span data-ttu-id="743c9-164">Получатель отслеживания был удален, поэтому нужно удалить данный раздел:</span><span class="sxs-lookup"><span data-stu-id="743c9-164">Tracking receiver has been removed, so you have to remove this section:</span></span>

          <receiver android:name="com.ubikod.capptain.android.sdk.track.CapptainTrackReceiver">
            <intent-filter>
              <action android:name="com.ubikod.capptain.intent.action.APPID_GOT" />
              <!-- possibly <action android:name="com.android.vending.INSTALL_REFERRER" /> -->
            </intent-filter>
          </receiver>

<span data-ttu-id="743c9-165">Обратите внимание, что объявление реализации получателя рассылок **EngagementMessageReceiver** изменено в `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="743c9-165">Note that the declaration of your implementation of the broadcast receiver **EngagementMessageReceiver** has changed in the `AndroidManifest.xml`.</span></span> <span data-ttu-id="743c9-166">Это вызвано тем, что API используется для отправки и удаления произвольных сообщений XMPP из произвольных сущностей XMPP, а API для отправки и получения сообщений между устройствами был удален.</span><span class="sxs-lookup"><span data-stu-id="743c9-166">This is because the API to send and remove arbitrary XMPP messages from arbitrary XMPP entities and the API to send and receive messages between devices have been removed.</span></span> <span data-ttu-id="743c9-167">Таким образом, необходимо также удалить следующие обратные вызовы из реализации **EngagementMessageReceiver** :</span><span class="sxs-lookup"><span data-stu-id="743c9-167">Thus, you have also to delete the following callbacks from your **EngagementMessageReceiver** implementation :</span></span>

            protected void onDeviceMessageReceived(android.content.Context context, java.lang.String deviceId, java.lang.String payload)

<span data-ttu-id="743c9-168">и</span><span class="sxs-lookup"><span data-stu-id="743c9-168">and</span></span>

            protected void onXMPPMessageReceived(android.content.Context context, android.os.Bundle message)

<span data-ttu-id="743c9-169">затем удалить все вызовы в **EngagementAgent** для:</span><span class="sxs-lookup"><span data-stu-id="743c9-169">then delete any call on **EngagementAgent** for :</span></span>

            sendMessageToDevice(java.lang.String deviceId, java.lang.String payload, java.lang.String packageName)

<span data-ttu-id="743c9-170">и</span><span class="sxs-lookup"><span data-stu-id="743c9-170">and</span></span>

            sendXMPPMessage(android.os.Bundle msg)

### <a name="proguard"></a><span data-ttu-id="743c9-171">Proguard</span><span class="sxs-lookup"><span data-stu-id="743c9-171">Proguard</span></span>
<span data-ttu-id="743c9-172">На настройку Proguard может оказать влияние ребрендинг, правила теперь выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="743c9-172">Proguard configuration can be impacted by rebranding, the rules are now looking like:</span></span>

            -dontwarn android.**
            -keep class android.support.v4.** { *; }

            -keep public class * extends android.os.IInterface
            -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
              <methods>;
            }

