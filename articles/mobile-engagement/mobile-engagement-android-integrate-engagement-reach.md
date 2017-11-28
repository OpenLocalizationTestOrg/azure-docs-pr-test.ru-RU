---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ec3fab3-35ec-458e-bf41-6cdd69e3fa44
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 06/27/2016
ms.author: piyushjo
ms.openlocfilehash: 4ab6143771bdc0758a548abb529d6bde98fc0e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-android"></a><span data-ttu-id="9cf26-103">Как tooIntegrate Engagement Reach на Android</span><span class="sxs-lookup"><span data-stu-id="9cf26-103">How tooIntegrate Engagement Reach on Android</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cf26-104">Необходимо выполнить процедуры интеграции hello, описанной в hello как tooIntegrate Engagement на Android документ до следующего руководства.</span><span class="sxs-lookup"><span data-stu-id="9cf26-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> 

## <a name="standard-integration"></a><span data-ttu-id="9cf26-105">Стандартная интеграция</span><span class="sxs-lookup"><span data-stu-id="9cf26-105">Standard integration</span></span>

<span data-ttu-id="9cf26-106">Скопируйте файлы ресурсов Reach из hello SDK в проект:</span><span class="sxs-lookup"><span data-stu-id="9cf26-106">Copy Reach resource files from hello SDK in your project :</span></span>

* <span data-ttu-id="9cf26-107">Скопируйте файлы hello из hello `res/layout` папки в комплекте с hello SDK в hello `res/layout` папку приложения.</span><span class="sxs-lookup"><span data-stu-id="9cf26-107">Copy hello files from hello `res/layout` folder delivered with hello SDK into hello `res/layout` folder of your application.</span></span>
* <span data-ttu-id="9cf26-108">Скопируйте файлы hello из hello `res/drawable` папки в комплекте с hello SDK в hello `res/drawable` папку приложения.</span><span class="sxs-lookup"><span data-stu-id="9cf26-108">Copy hello files from hello `res/drawable` folder delivered with hello SDK into hello `res/drawable` folder of your application.</span></span>

<span data-ttu-id="9cf26-109">Отредактируйте файл `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="9cf26-109">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="9cf26-110">Добавьте следующий раздел hello (между hello `<application>` и `</application>` теги):</span><span class="sxs-lookup"><span data-stu-id="9cf26-110">Add hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
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
          <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
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
* <span data-ttu-id="9cf26-111">Требуется это разрешение tooreplay системных уведомлений не были щелчке при загрузке (в противном случае они будут храниться на диске, но больше не отображаются, может быть tooinclude это).</span><span class="sxs-lookup"><span data-stu-id="9cf26-111">You need this permission tooreplay system notifications that were not clicked at boot (otherwise they will be kept on disk but won't be displayed anymore, you really have tooinclude this).</span></span>
  
          <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
* <span data-ttu-id="9cf26-112">Указать значок, используемый для уведомления (как в приложении и системные из них) путем копирования и изменения hello в следующем разделе (между hello `<application>` и `</application>` теги):</span><span class="sxs-lookup"><span data-stu-id="9cf26-112">Specify an icon used for notifications (both in app and system ones) by copying and editing hello following section (between hello `<application>` and `</application>` tags):</span></span>
  
          <meta-data android:name="engagement:reach:notification:icon" android:value="<name_of_icon_WITHOUT_file_extension_and_WITHOUT_'@drawable/'>" />

> [!IMPORTANT]
> <span data-ttu-id="9cf26-113">Этот раздел **обязателен** , если вы планируете использовать системные уведомления при создании кампаний Reach.</span><span class="sxs-lookup"><span data-stu-id="9cf26-113">This section is **mandatory** if you plan on using system notifications when creating Reach campaigns.</span></span> <span data-ttu-id="9cf26-114">В Android системные уведомления без значков не отображаются.</span><span class="sxs-lookup"><span data-stu-id="9cf26-114">Android prevents system notifications without icons from being shown.</span></span> <span data-ttu-id="9cf26-115">Таким образом, опущен в этом разделе, конечные пользователи не могли tooreceive их.</span><span class="sxs-lookup"><span data-stu-id="9cf26-115">So if you omit this section, your end users will not be able tooreceive them.</span></span>
> 
> 

* <span data-ttu-id="9cf26-116">При создании кампаний с с использованием самых общих системных уведомлений требуется hello tooadd следующие разрешения (после hello `</application>` тега), если отсутствует:</span><span class="sxs-lookup"><span data-stu-id="9cf26-116">If you create campaigns with system notifications using big picture, you need tooadd hello following permissions (after hello `</application>` tag) if missing:</span></span>
  
          <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
          <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
  
  * <span data-ttu-id="9cf26-117">Если ваше приложение ориентировано на API Android уровня 23 или более высокого, на Android M для разрешения ``WRITE_EXTERNAL_STORAGE`` требуется утверждение пользователя.</span><span class="sxs-lookup"><span data-stu-id="9cf26-117">On Android M and if your application targets Android API level 23 or greater, ``WRITE_EXTERNAL_STORAGE`` permission requires user approval.</span></span> <span data-ttu-id="9cf26-118">Ознакомьтесь с [этим разделом](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="9cf26-118">Please read [this section](mobile-engagement-android-integrate-engagement.md#android-m-permissions).</span></span>
* <span data-ttu-id="9cf26-119">Для системных уведомлений, которые также можно указать в hello достичь кампании, если hello устройства следует кольца и/или компакт-дисков.</span><span class="sxs-lookup"><span data-stu-id="9cf26-119">For system notifications you can also specify in hello Reach campaign if hello device should ring and/or vibrate.</span></span> <span data-ttu-id="9cf26-120">Для него toowork, у вас есть toomake убедиться, что объявлены следующие разрешения hello (после hello `</application>` тега):</span><span class="sxs-lookup"><span data-stu-id="9cf26-120">For it toowork, you have toomake sure you declared hello following permission (after hello `</application>` tag):</span></span>
  
          <uses-permission android:name="android.permission.VIBRATE" />
  
  <span data-ttu-id="9cf26-121">Без этого разрешения Android предотвращает отображение системных уведомлений, если установлен кольцо hello или hello компакт-дисков, параметр в диспетчере hello достижения кампании.</span><span class="sxs-lookup"><span data-stu-id="9cf26-121">Without this permission, Android prevents system notifications from being shown if you checked hello ring or hello vibrate option in hello Reach Campaign manager.</span></span>

## <a name="native-push"></a><span data-ttu-id="9cf26-122">Системные push-уведомления</span><span class="sxs-lookup"><span data-stu-id="9cf26-122">Native Push</span></span>
<span data-ttu-id="9cf26-123">Теперь, когда вы настроили модулем, необходимо tooconfigure кампании собственных push toobe может tooreceive hello на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-123">Now that you configured Reach module, you need tooconfigure native push toobe able tooreceive hello campaigns on hello device.</span></span>

<span data-ttu-id="9cf26-124">Для Android поддерживаются две службы:</span><span class="sxs-lookup"><span data-stu-id="9cf26-124">We support two services on Android:</span></span>

* <span data-ttu-id="9cf26-125">Google Play устройств: используйте [Google Cloud Messaging] по следующей hello [как руководство tooIntegrate GCM с проектной](mobile-engagement-android-gcm-integrate.md) руководства.</span><span class="sxs-lookup"><span data-stu-id="9cf26-125">Google Play devices: Use [Google Cloud Messaging] by following hello [How tooIntegrate GCM with Engagement guide](mobile-engagement-android-gcm-integrate.md) guide.</span></span>
* <span data-ttu-id="9cf26-126">Amazon устройств: используйте [Amazon Device Messaging] по следующей hello [как руководство tooIntegrate ADM с проектной](mobile-engagement-android-adm-integrate.md) руководства.</span><span class="sxs-lookup"><span data-stu-id="9cf26-126">Amazon devices: Use [Amazon Device Messaging] by following hello [How tooIntegrate ADM with Engagement guide](mobile-engagement-android-adm-integrate.md) guide.</span></span>

<span data-ttu-id="9cf26-127">Если требуется, чтобы tootarget Amazon и Google Play устройства, его возможных toohave весь код внутри 1 AndroidManifest.xml/APK для разработки приложений.</span><span class="sxs-lookup"><span data-stu-id="9cf26-127">If you want tootarget both Amazon and Google Play devices, its possible toohave everything inside 1 AndroidManifest.xml/APK for development.</span></span> <span data-ttu-id="9cf26-128">Однако при отправке tooAmazon, они могут отклонять приложения, если они находят GCM кода.</span><span class="sxs-lookup"><span data-stu-id="9cf26-128">But when submitting tooAmazon, they may reject your application if they find GCM code.</span></span>

<span data-ttu-id="9cf26-129">В этом случае следует использовать несколько APK.</span><span class="sxs-lookup"><span data-stu-id="9cf26-129">You should use multiple APKs in that case.</span></span>

<span data-ttu-id="9cf26-130">**Приложение будет теперь готовы tooreceive и отображения достичь кампаний!**</span><span class="sxs-lookup"><span data-stu-id="9cf26-130">**Your application is now ready tooreceive and display reach campaigns!**</span></span>

## <a name="how-toohandle-data-push"></a><span data-ttu-id="9cf26-131">Как отправить данные toohandle</span><span class="sxs-lookup"><span data-stu-id="9cf26-131">How toohandle data push</span></span>
### <a name="integration"></a><span data-ttu-id="9cf26-132">Интеграция</span><span class="sxs-lookup"><span data-stu-id="9cf26-132">Integration</span></span>
<span data-ttu-id="9cf26-133">Если требуется toobe вашего приложения может помещает tooreceive данных Reach, имеют toocreate вложенный класс `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` и ссылаться на него hello `AndroidManifest.xml` файла (между hello `<application>` и/или `</application>` теги):</span><span class="sxs-lookup"><span data-stu-id="9cf26-133">If you want your application toobe able tooreceive Reach data pushes, you have toocreate a sub-class of `com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver` and reference it in hello `AndroidManifest.xml` file (between hello `<application>` and/or `</application>` tags):</span></span>

            <receiver android:name="<your_sub_class_of_com.microsoft.azure.engagement.reach.EngagementReachDataPushReceiver>"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DATA_PUSH" />
              </intent-filter>
            </receiver>

<span data-ttu-id="9cf26-134">Можно переопределить hello `onDataPushStringReceived` и `onDataPushBase64Received` обратные вызовы.</span><span class="sxs-lookup"><span data-stu-id="9cf26-134">Then you can override hello `onDataPushStringReceived` and `onDataPushBase64Received` callbacks.</span></span> <span data-ttu-id="9cf26-135">Пример:</span><span class="sxs-lookup"><span data-stu-id="9cf26-135">Here is an example:</span></span>

            public class MyDataPushReceiver extends EngagementReachDataPushReceiver
            {
              @Override
              protected Boolean onDataPushStringReceived(Context context, String category, String body)
              {
                Log.d("tmp", "String data push message received: " + body);
                return true;
              }

              @Override
              protected Boolean onDataPushBase64Received(Context context, String category, byte[] decodedBody, String encodedBody)
              {
                Log.d("tmp", "Base64 data push message received: " + encodedBody);
                // Do something useful with decodedBody like updating an image view
                return true;
              }
            }

### <a name="category"></a><span data-ttu-id="9cf26-136">Категория</span><span class="sxs-lookup"><span data-stu-id="9cf26-136">Category</span></span>
<span data-ttu-id="9cf26-137">параметр категории Hello не является обязательным при создании кампании Push-данных и позволяет ваши данные toofilter помещает в стек.</span><span class="sxs-lookup"><span data-stu-id="9cf26-137">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="9cf26-138">Это полезно, если у вас есть несколько широковещательных приемники обработки различных типов данных Push-уведомлений, или если требуются различные toopush из `Base64` tooidentify данных и необходимо их типа перед синтаксическим анализом их.</span><span class="sxs-lookup"><span data-stu-id="9cf26-138">This is useful if you have several broadcast receivers handling different types of data pushes, or if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

### <a name="callbacks-return-parameter"></a><span data-ttu-id="9cf26-139">Параметр возврата обратных вызовов</span><span class="sxs-lookup"><span data-stu-id="9cf26-139">Callbacks' return parameter</span></span>
<span data-ttu-id="9cf26-140">Ниже приведены некоторые рекомендации по tooproperly дескриптор hello возвращаемого параметра `onDataPushStringReceived` и `onDataPushBase64Received`:</span><span class="sxs-lookup"><span data-stu-id="9cf26-140">Here are some guidelines tooproperly handle hello return parameter of `onDataPushStringReceived` and `onDataPushBase64Received`:</span></span>

* <span data-ttu-id="9cf26-141">Широковещательные получатель должен возвращать `null` с hello обратного вызова, если он не знает, как push toohandle данных.</span><span class="sxs-lookup"><span data-stu-id="9cf26-141">A broadcast receiver should return `null` in hello callback if it does not know how toohandle a data push.</span></span> <span data-ttu-id="9cf26-142">Следует использовать toodetermine категории hello ли широковещательных приемника должен обрабатывать Принудительная отправка данных hello, или нет.</span><span class="sxs-lookup"><span data-stu-id="9cf26-142">You should use hello category toodetermine whether your broadcast receiver should handle hello data push or not.</span></span>
* <span data-ttu-id="9cf26-143">Один получатель широковещательных hello должен возвращать `true` с hello обратного вызова, если он принимает hello Принудительная отправка данных.</span><span class="sxs-lookup"><span data-stu-id="9cf26-143">One of hello broadcast receiver should return `true` in hello callback if it accepts hello data push.</span></span>
* <span data-ttu-id="9cf26-144">Один получатель широковещательных hello должен возвращать `false` с hello обратного вызова, если она распознает hello Принудительная отправка данных, а затем отбрасывает ее для какой-либо причине.</span><span class="sxs-lookup"><span data-stu-id="9cf26-144">One of hello broadcast receiver should return `false` in hello callback if it recognizes hello data push, but discards it for whatever reason.</span></span> <span data-ttu-id="9cf26-145">Например, возвращают `false` при получении hello данные являются недопустимыми.</span><span class="sxs-lookup"><span data-stu-id="9cf26-145">For example, return `false` when hello received data is invalid.</span></span>
* <span data-ttu-id="9cf26-146">Если один широковещательных получателя возвращает `true` while другой один возвращает `false` для hello же Принудительная отправка данных, поведение hello не определен, запрещается.</span><span class="sxs-lookup"><span data-stu-id="9cf26-146">If one broadcast receiver returns `true` while another one returns `false` for hello same data push, hello behavior is undefined, you should never do that.</span></span>

<span data-ttu-id="9cf26-147">Тип возвращаемого значения Hello используется только для hello Reach статистики:</span><span class="sxs-lookup"><span data-stu-id="9cf26-147">hello return type is used only for hello Reach statistics:</span></span>

* <span data-ttu-id="9cf26-148">`Replied`увеличивается, если один из получателей широковещательных hello вернул либо `true` или `false`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-148">`Replied` is incremented if one of hello broadcast receivers returned either `true` or `false`.</span></span>
* <span data-ttu-id="9cf26-149">`Actioned`увеличивается только в том случае, если один hello широковещательных приемники возвращается `true`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-149">`Actioned` is incremented only if one of hello broadcast receivers returned `true`.</span></span>

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="9cf26-150">Как toocustomize кампании</span><span class="sxs-lookup"><span data-stu-id="9cf26-150">How toocustomize campaigns</span></span>
<span data-ttu-id="9cf26-151">toocustomize кампаний, вы можете изменить макеты hello в пакет SDK для Reach hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-151">toocustomize campaigns, you can modify hello layouts provided in hello Reach SDK.</span></span>

<span data-ttu-id="9cf26-152">Следует сохранять все hello идентификаторы, используемые в макете hello и оставьте типы hello hello представлений, использующих идентификатор, особенно для представления текста и изображения представления.</span><span class="sxs-lookup"><span data-stu-id="9cf26-152">You should keep all hello identifiers used in hello layouts and keep hello types of hello views that use an identifier, especially for text views and image views.</span></span> <span data-ttu-id="9cf26-153">Некоторые представления являются просто использовать toohide или отобразить области, поэтому их тип может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="9cf26-153">Some views are just used toohide or show areas so their type may be changed.</span></span> <span data-ttu-id="9cf26-154">Если предполагается тип hello toochange представления в макетах hello предоставленный проверьте hello исходного кода.</span><span class="sxs-lookup"><span data-stu-id="9cf26-154">Please check hello source code if you intend toochange hello type of a view in hello provided layouts.</span></span>

### <a name="notifications"></a><span data-ttu-id="9cf26-155">Уведомления</span><span class="sxs-lookup"><span data-stu-id="9cf26-155">Notifications</span></span>
<span data-ttu-id="9cf26-156">Существует два типа уведомлений: системные уведомления и уведомления приложения, использующие разные файлы разметки.</span><span class="sxs-lookup"><span data-stu-id="9cf26-156">There are two types of notifications: system and in-app notifications which use different layout files.</span></span>

#### <a name="system-notifications"></a><span data-ttu-id="9cf26-157">Системные уведомления</span><span class="sxs-lookup"><span data-stu-id="9cf26-157">System notifications</span></span>
<span data-ttu-id="9cf26-158">toocustomize системных уведомлений требуется toouse hello **категории**.</span><span class="sxs-lookup"><span data-stu-id="9cf26-158">toocustomize system notifications you need toouse hello **categories**.</span></span> <span data-ttu-id="9cf26-159">Можно легко слишком[категории](#categories).</span><span class="sxs-lookup"><span data-stu-id="9cf26-159">You can jump too[Categories](#categories).</span></span>

#### <a name="in-app-notifications"></a><span data-ttu-id="9cf26-160">Уведомления в приложении</span><span class="sxs-lookup"><span data-stu-id="9cf26-160">In-app notifications</span></span>
<span data-ttu-id="9cf26-161">По умолчанию уведомление в приложении является представление, динамически добавляемых toohello текущей активности пользователя Спасибо toohello Android метод интерфейса `addContentView()`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-161">By default, an in-app notification is a view that is dynamically added toohello current activity user interface thanks toohello Android method `addContentView()`.</span></span> <span data-ttu-id="9cf26-162">Это называется наложением уведомлений.</span><span class="sxs-lookup"><span data-stu-id="9cf26-162">This is called a notification overlay.</span></span> <span data-ttu-id="9cf26-163">Уведомления наложений прекрасно подходят для быстрого интеграции, так как они не требуют вы toomodify любого макета в приложении.</span><span class="sxs-lookup"><span data-stu-id="9cf26-163">Notification overlays are great for a fast integration because they do not require you toomodify any layout in your application.</span></span>

<span data-ttu-id="9cf26-164">toomodify вида hello накладывает на уведомления, можно просто изменить файл hello `engagement_notification_area.xml` должен tooyour.</span><span class="sxs-lookup"><span data-stu-id="9cf26-164">toomodify hello look of your notification overlays, you can simply modify hello file `engagement_notification_area.xml` tooyour needs.</span></span>

> [!NOTE]
> <span data-ttu-id="9cf26-165">файл Hello `engagement_notification_overlay.xml` является hello, используемые toocreate наложения уведомления включает в себя файл hello `engagement_notification_area.xml`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-165">hello file `engagement_notification_overlay.xml` is hello one that is used toocreate a notification overlay, it includes hello file `engagement_notification_area.xml`.</span></span> <span data-ttu-id="9cf26-166">Также можно настроить его toosuit потребностям (например, для позиционирования hello области уведомлений в пределах hello наложения).</span><span class="sxs-lookup"><span data-stu-id="9cf26-166">You can also customize it toosuit your needs (such as for positioning hello notification area within hello overlay).</span></span>
> 
> 

##### <a name="include-notification-layout-as-part-of-an-activity-layout"></a><span data-ttu-id="9cf26-167">Включите разметку уведомления в состав разметки действия</span><span class="sxs-lookup"><span data-stu-id="9cf26-167">Include notification layout as part of an activity layout</span></span>
<span data-ttu-id="9cf26-168">Наложения удобны для быстрой интеграции, но в определенных случаях их использование может быть неудобно или может вызывать нежелательные побочные эффекты.</span><span class="sxs-lookup"><span data-stu-id="9cf26-168">Overlays are great for a fast integration but can be inconvenient or have side effects in special cases.</span></span> <span data-ttu-id="9cf26-169">Hello наложения системы можно настроить на уровне активности, сделав его легко tooprevent побочные эффекты для специальных действий.</span><span class="sxs-lookup"><span data-stu-id="9cf26-169">hello overlay system can be customized at an activity level, making it easy tooprevent side effects for special activities.</span></span>

<span data-ttu-id="9cf26-170">Вы можете tooinclude нашей макета уведомления в вашей существующей макета Спасибо toohello Android **включают** инструкции.</span><span class="sxs-lookup"><span data-stu-id="9cf26-170">You can decide tooinclude our notification layout in your existing layout thanks toohello Android **include** statement.</span></span> <span data-ttu-id="9cf26-171">Hello ниже приведен пример измененного `ListActivity` макета, содержащие только `ListView`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-171">hello following is an example of a modified `ListActivity` layout containing just a `ListView`.</span></span>

<span data-ttu-id="9cf26-172">**До интеграции с Engagement:**</span><span class="sxs-lookup"><span data-stu-id="9cf26-172">**Before Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <ListView
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@android:id/list"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent" />

<span data-ttu-id="9cf26-173">**После интеграции с Engagement:**</span><span class="sxs-lookup"><span data-stu-id="9cf26-173">**After Engagement integration :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <LinearLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:orientation="vertical"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <ListView
                android:id="@android:id/list"
                android:layout_width="fill_parent"
                android:layout_height="fill_parent"
                android:layout_weight="1" />

              <include layout="@layout/engagement_notification_area" />

            </LinearLayout>

<span data-ttu-id="9cf26-174">В этом примере мы добавили родительского контейнера, так как исходный макет hello использовать представления списка в качестве элементов верхнего уровня hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-174">In this example we added a parent container since hello original layout used a list view as hello top level element.</span></span> <span data-ttu-id="9cf26-175">Мы также добавили `android:layout_weight="1"` toobe может tooadd настроены представление представление списка `android:layout_height="fill_parent"`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-175">We also added `android:layout_weight="1"` toobe able tooadd a view below a list view configured with `android:layout_height="fill_parent"`.</span></span>

<span data-ttu-id="9cf26-176">Hello Engagement Reach SDK автоматически обнаруживает макета уведомления hello включается в это действие и не будет добавлять наложение для этого действия.</span><span class="sxs-lookup"><span data-stu-id="9cf26-176">hello Engagement Reach SDK automatically detects that hello notification layout is included in this activity and will not add an overlay for this activity.</span></span>

> [!TIP]
> <span data-ttu-id="9cf26-177">При использовании ListActivity в приложении отображается наложения Reach помешают отклик tooclicked элементов в представлении списка hello больше.</span><span class="sxs-lookup"><span data-stu-id="9cf26-177">If you use a ListActivity in your application, a visible Reach overlay will prevent you from reacting tooclicked items in hello list view anymore.</span></span> <span data-ttu-id="9cf26-178">Это известная проблема.</span><span class="sxs-lookup"><span data-stu-id="9cf26-178">This is a known issue.</span></span> <span data-ttu-id="9cf26-179">toowork этой проблемы мы советуем вам tooembed hello уведомления макета в макете действия собственный список как в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-179">toowork around this problem we suggest you tooembed hello notification layout in your own list activity layout like in hello previous sample.</span></span>
> 
> 

##### <a name="disabling-application-notification-per-activity"></a><span data-ttu-id="9cf26-180">Отключение уведомлений приложения для определенных действий</span><span class="sxs-lookup"><span data-stu-id="9cf26-180">Disabling application notification per activity</span></span>
<span data-ttu-id="9cf26-181">Если вы не хотите hello toobe наложения добавлен tooyour действия, и если макет hello уведомление не было добавлено в собственный макет, можно отключить наложение hello для этого действия в hello `AndroidManifest.xml` путем добавления `meta-data` раздела, как показано в следующих hello Пример:</span><span class="sxs-lookup"><span data-stu-id="9cf26-181">If you don't want hello overlay toobe added tooyour activity, and if you don't include hello notification layout in your own layout, you can disable hello overlay for this activity in hello `AndroidManifest.xml` by adding a `meta-data` section like in hello following example:</span></span>

            <activity android:name="SplashScreenActivity">
              <meta-data android:name="engagement:notification:overlay" android:value="false"/>
            </activity>

#### <span data-ttu-id="9cf26-182">Категории <a name="categories"></a></span><span class="sxs-lookup"><span data-stu-id="9cf26-182"><a name="categories"></a> Categories</span></span>
<span data-ttu-id="9cf26-183">При изменении hello, предоставляемые макеты, то изменить hello вида все уведомления.</span><span class="sxs-lookup"><span data-stu-id="9cf26-183">When you modify hello provided layouts, you modify hello look of all your notifications.</span></span> <span data-ttu-id="9cf26-184">Категории позволяют вам toodefine, различные целевые ищет (возможно поведения) уведомления.</span><span class="sxs-lookup"><span data-stu-id="9cf26-184">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="9cf26-185">Категорию можно указать при создании рекламной кампании.</span><span class="sxs-lookup"><span data-stu-id="9cf26-185">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="9cf26-186">Учтите, что категории также позволяют настраивать объявления и опросы. Это описано далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="9cf26-186">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="9cf26-187">tooregister обработчик категории для уведомления, потребуется tooadd вызов при инициализации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-187">tooregister a category handler for your notifications, you need tooadd a call when hello application is initialized.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cf26-188">Прочитайте предупреждение hello об атрибуте hello android: процесс \<android-sdk-engagement-process\> в hello как tooIntegrate обязательств по теме Android, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="9cf26-188">Please read hello warning about hello android:process attribute \<android-sdk-engagement-process\> in hello How tooIntegrate Engagement on Android topic before proceeding.</span></span>
> 
> 

<span data-ttu-id="9cf26-189">Hello следующий пример предполагает подтвержден предыдущим предупреждением hello и используйте вложенный класс `EngagementApplication`:</span><span class="sxs-lookup"><span data-stu-id="9cf26-189">hello following example assumes you acknowledged hello previous warning and use a sub-class of `EngagementApplication`:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), "myCategory");
              }
            }

<span data-ttu-id="9cf26-190">Hello `MyNotifier` объект представляет реализацию hello обработчика категории уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-190">hello `MyNotifier` object is hello implementation of hello notification category handler.</span></span> <span data-ttu-id="9cf26-191">Реализация hello `EngagementNotifier` интерфейс или класс sub реализации по умолчанию hello: `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-191">It is either an implementation of hello `EngagementNotifier` interface or a sub class of hello default implementation: `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="9cf26-192">Обратите внимание, что hello же уведомляющий может обрабатывать несколько категорий, можно зарегистрировать их следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9cf26-192">Note that hello same notifier can handle several categories, you can register them like this:</span></span>

            reachAgent.registerNotifier(new MyNotifier(this), "myCategory", "myAnotherCategory");

<span data-ttu-id="9cf26-193">Реализация категории по умолчанию hello tooreplace, вы можете зарегистрировать реализации, такой как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9cf26-193">tooreplace hello default category implementation, you can register your implementation like in hello following example:</span></span>

            public class MyApplication extends EngagementApplication
            {
              @Override
              protected void onApplicationProcessCreate()
              {
                // [...] other init
                EngagementReachAgent reachAgent = EngagementReachAgent.getInstance(this);
                reachAgent.registerNotifier(new MyNotifier(this), Intent.CATEGORY_DEFAULT); // "android.intent.category.DEFAULT"
              }
            }

<span data-ttu-id="9cf26-194">используется обработчиком текущей категории Hello передается как параметр в большинство методов, можно переопределить в `EngagementDefaultNotifier`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-194">hello current category used in a handler is passed as a parameter in most methods you can override in `EngagementDefaultNotifier`.</span></span>

<span data-ttu-id="9cf26-195">Она передается либо как параметр `String`, либо опосредованно в объекте `EngagementReachContent`, содержащем метод `getCategory()`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-195">It is passed either as a `String` parameter or indirectly in a `EngagementReachContent` object which has a `getCategory()` method.</span></span>

<span data-ttu-id="9cf26-196">Большая часть процесса создания hello уведомлений можно изменить путем переопределения методов на `EngagementDefaultNotifier`для дополнительную настройку чувствовать себя свободного tootake взглянуть на hello технической документации и hello исходного кода.</span><span class="sxs-lookup"><span data-stu-id="9cf26-196">You can change most of hello notification creation process by redefining methods on `EngagementDefaultNotifier`, for more advanced customization feel free tootake a look at hello technical documentation and at hello source code.</span></span>

##### <a name="in-app-notifications"></a><span data-ttu-id="9cf26-197">Уведомления в приложении</span><span class="sxs-lookup"><span data-stu-id="9cf26-197">In-app notifications</span></span>
<span data-ttu-id="9cf26-198">Если необходимо просто toouse дополнительные раскладки для определенной категории, это можно реализовать как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-198">If you just want toouse alternate layouts for a specific category, you can implement this as in hello following example:</span></span>

            public class MyNotifier extends EngagementDefaultNotifier
            {
              public MyNotifier(Context context)
              {
                super(context);
              }

              @Override
              protected int getOverlayLayoutId(String category)
              {
                return R.layout.my_notification_overlay;
              }


              @Override
              public Integer getOverlayViewId(String category)
              {
                return R.id.my_notification_overlay;
              }

              @Override
              public Integer getInAppAreaId(String category)
              {
                return R.id.my_notification_area;
              }
            }

<span data-ttu-id="9cf26-199">**Пример `my_notification_overlay.xml` :**</span><span class="sxs-lookup"><span data-stu-id="9cf26-199">**Example of `my_notification_overlay.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <RelativeLayout
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:id="@+id/my_notification_overlay"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <include layout="@layout/my_notification_area" />

            </RelativeLayout>

<span data-ttu-id="9cf26-200">Как видите, идентификатор представления наложения hello отличается от стандартного Привет одному.</span><span class="sxs-lookup"><span data-stu-id="9cf26-200">As you can see, hello overlay view identifier is different than hello standard one.</span></span> <span data-ttu-id="9cf26-201">Важно, чтобы у каждой разметки использовался уникальный идентификатор для наложений.</span><span class="sxs-lookup"><span data-stu-id="9cf26-201">It is important that each layout use a unique identifier for overlays.</span></span>

<span data-ttu-id="9cf26-202">**Пример `my_notification_area.xml` :**</span><span class="sxs-lookup"><span data-stu-id="9cf26-202">**Example of `my_notification_area.xml` :**</span></span>

            <?xml version="1.0" encoding="utf-8"?>
            <merge
              xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="fill_parent"
              android:layout_height="fill_parent">

              <RelativeLayout
                android:id="@+id/my_notification_area"
                android:layout_width="fill_parent"
                android:layout_height="64dp"
                android:layout_alignParentTop="true"
                android:background="#B000">

                <LinearLayout
                  android:orientation="horizontal"
                  android:layout_width="fill_parent"
                  android:layout_height="fill_parent"
                  android:gravity="center_vertical">

                  <ImageView
                    android:id="@+id/engagement_notification_icon"
                    android:layout_width="48dp"
                    android:layout_height="48dp" />

                  <LinearLayout
                    android:id="@+id/engagement_notification_text"
                    android:orientation="vertical"
                    android:layout_width="fill_parent"
                    android:layout_height="fill_parent"
                    android:layout_weight="1"
                    android:gravity="center_vertical">

                    <TextView
                      android:id="@+id/engagement_notification_title"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:singleLine="true"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Medium" />

                    <TextView
                      android:id="@+id/engagement_notification_message"
                      android:layout_width="fill_parent"
                      android:layout_height="wrap_content"
                      android:maxLines="2"
                      android:ellipsize="end"
                      android:textAppearance="@android:style/TextAppearance.Small" />

                  </LinearLayout>

                  <ImageView
                    android:id="@+id/engagement_notification_image"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:adjustViewBounds="true" />

                  <ImageButton
                    android:id="@+id/engagement_notification_close_area"
                    android:visibility="invisible"
                    android:layout_width="wrap_content"
                    android:layout_height="fill_parent"
                    android:src="@android:drawable/btn_dialog"
                    android:background="#0F00" />

                </LinearLayout>

                <ImageButton
                  android:id="@+id/engagement_notification_close"
                  android:layout_width="wrap_content"
                  android:layout_height="fill_parent"
                  android:layout_alignParentRight="true"
                  android:src="@android:drawable/btn_dialog"
                  android:background="#0F00" />

              </RelativeLayout>

            </merge>

<span data-ttu-id="9cf26-203">Как видите, идентификатор представления области уведомлений hello отличается от стандартного Привет одному.</span><span class="sxs-lookup"><span data-stu-id="9cf26-203">As you can see, hello notification area view identifier is different than hello standard one.</span></span> <span data-ttu-id="9cf26-204">Важно, чтобы у каждой разметки использовался уникальный идентификатор областей уведомления.</span><span class="sxs-lookup"><span data-stu-id="9cf26-204">It is important that each layout uses a unique identifier for notification areas.</span></span>

<span data-ttu-id="9cf26-205">Этот простой пример категории делает уведомления приложения (или в приложении), в верхней части hello экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="9cf26-205">This simple example of category makes application (or in-app) notifications displayed at hello top of hello screen.</span></span> <span data-ttu-id="9cf26-206">Не был изменен hello стандартные идентификаторы, используемые в области уведомлений hello сам.</span><span class="sxs-lookup"><span data-stu-id="9cf26-206">We did not change hello standard identifiers used in hello notification area itself.</span></span>

<span data-ttu-id="9cf26-207">Если требуется, наличие tooredefine hello toochange `EngagementDefaultNotifier.prepareInAppArea` метод.</span><span class="sxs-lookup"><span data-stu-id="9cf26-207">If you want toochange that, you have tooredefine hello `EngagementDefaultNotifier.prepareInAppArea` method.</span></span> <span data-ttu-id="9cf26-208">Рекомендуется toolook hello технической документации и исходного кода hello `EngagementNotifier` и `EngagementDefaultNotifier` Если требуется дополнительная настройка уровня.</span><span class="sxs-lookup"><span data-stu-id="9cf26-208">It's recommended toolook at hello technical documentation and at hello source code of `EngagementNotifier` and `EngagementDefaultNotifier` if you want this level of advanced customization.</span></span>

##### <a name="system-notifications"></a><span data-ttu-id="9cf26-209">Системные уведомления</span><span class="sxs-lookup"><span data-stu-id="9cf26-209">System notifications</span></span>
<span data-ttu-id="9cf26-210">Расширив `EngagementDefaultNotifier`, можно переопределить `onNotificationPrepared` tooalter hello уведомления, подготовленное для реализации по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-210">By extending `EngagementDefaultNotifier`, you can override `onNotificationPrepared` tooalter hello notification that was prepared by hello default implementation.</span></span>

<span data-ttu-id="9cf26-211">Например:</span><span class="sxs-lookup"><span data-stu-id="9cf26-211">For example:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content)
              throws RuntimeException
            {
              if ("ongoing".equals(content.getCategory()))
                notification.flags |= Notification.FLAG_ONGOING_EVENT;
              return true;
            }

<span data-ttu-id="9cf26-212">Этот пример делает Системное уведомление для содержимого, отображаемого как текущее событие при использовании категории «текущую» hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-212">This example makes a system notification for a content being displayed as an ongoing event when hello "ongoing" category is used.</span></span>

<span data-ttu-id="9cf26-213">Если требуется toobuild hello `Notification` объекта с нуля, можно вернуть `false` toohello метод и вызовите `notify` самостоятельно на hello `NotificationManager`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-213">If you want toobuild hello `Notification` object from scratch, you can return `false` toohello method and call `notify` yourself on hello `NotificationManager`.</span></span> <span data-ttu-id="9cf26-214">В этом случае важно поддерживать `contentIntent`, `deleteIntent` и hello идентификатор уведомления, используемый в `EngagementReachReceiver`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-214">In that case it's important that you keep a `contentIntent`, a `deleteIntent` and hello notification identifier used by `EngagementReachReceiver`.</span></span>

<span data-ttu-id="9cf26-215">Вот правильный пример такой реализации:</span><span class="sxs-lookup"><span data-stu-id="9cf26-215">Here is a correct example of such an implementation:</span></span>

            @Override
            protected boolean onNotificationPrepared(Notification notification, EngagementReachInteractiveContent content) throws RuntimeException
            {
              /* Required fields */
              NotificationCompat.Builder builder = new NotificationCompat.Builder(mContext)
                .setSmallIcon(notification.icon)              // icon is mandatory
                .setContentIntent(notification.contentIntent) // keep content intent
                .setDeleteIntent(notification.deleteIntent);  // keep delete intent

              /* Your customization */
              // builder.set...

              /* Dismiss option can be managed only after build */
              Notification myNotification = builder.build();
              if (!content.isNotificationCloseable())
                myNotification.flags |= Notification.FLAG_NO_CLEAR;

              /* Notify here instead of super class */
              NotificationManager manager = (NotificationManager) mContext.getSystemService(Context.NOTIFICATION_SERVICE);
              manager.notify(getNotificationId(content), myNotification); // notice hello call tooget hello right identifier

              /* Return false, we notify ourselves */
              return false;
            }

##### <a name="notification-only-announcements"></a><span data-ttu-id="9cf26-216">Объявления только для уведомлений</span><span class="sxs-lookup"><span data-stu-id="9cf26-216">Notification only announcements</span></span>
<span data-ttu-id="9cf26-217">Hello управление hello щелкните уведомление только объявления можно настраивать путем переопределения `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello подготовленных `Intent`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-217">hello management of hello click on a notification only announcement can be customized by overriding `EngagementDefaultNotifier.onNotifAnnouncementIntentPrepared` toomodify hello prepared `Intent`.</span></span> <span data-ttu-id="9cf26-218">Этот метод позволяет флаги hello tootune легко.</span><span class="sxs-lookup"><span data-stu-id="9cf26-218">Using this method allows you tootune hello flags easily.</span></span>

<span data-ttu-id="9cf26-219">Пример hello tooadd `SINGLE_TOP` флаг:</span><span class="sxs-lookup"><span data-stu-id="9cf26-219">For example tooadd hello `SINGLE_TOP` flag:</span></span>

            @Override
            protected Intent onNotifAnnouncementIntentPrepared(EngagementNotifAnnouncement notifAnnouncement,
              Intent intent)
            {
              intent.addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
              return intent;
            }

<span data-ttu-id="9cf26-220">Для пользователей предыдущих версий обязательств Обратите внимание, что системных уведомлений без действия URL-адрес теперь запускается приложение hello Если это было в фоновом режиме, этот метод можно вызывать с помощью объявления без URL-адрес действия.</span><span class="sxs-lookup"><span data-stu-id="9cf26-220">For legacy Engagement users, please note that system notifications without action URL now launches hello application if it was in background, so this method can be called with an announcement without action URL.</span></span> <span data-ttu-id="9cf26-221">При настройке намерение hello, необходимо учитывать.</span><span class="sxs-lookup"><span data-stu-id="9cf26-221">You should consider that when customizing hello intent.</span></span>

<span data-ttu-id="9cf26-222">Вы также можете реализовать `EngagementNotifier.executeNotifAnnouncementAction` с нуля.</span><span class="sxs-lookup"><span data-stu-id="9cf26-222">You can also implement `EngagementNotifier.executeNotifAnnouncementAction` from scratch.</span></span>

##### <a name="notification-life-cycle"></a><span data-ttu-id="9cf26-223">Жизненный цикл уведомления</span><span class="sxs-lookup"><span data-stu-id="9cf26-223">Notification life cycle</span></span>
<span data-ttu-id="9cf26-224">При использовании категории по умолчанию hello, некоторые методы жизненного цикла вызываются на hello `EngagementReachInteractiveContent` объекта tooreport статистики и обновление hello кампании состояния:</span><span class="sxs-lookup"><span data-stu-id="9cf26-224">When using hello default category, some life cycle methods are called on hello `EngagementReachInteractiveContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="9cf26-225">Здравствуйте, когда hello уведомления отображается в приложении, или поместить в строке состояния hello, `displayNotification` (который предоставляет статистические данные) вызывается метод по `EngagementReachAgent` Если `handleNotification` возвращает `true`.</span><span class="sxs-lookup"><span data-stu-id="9cf26-225">When hello notification is displayed in application or put in hello status bar, hello `displayNotification` method is called (which reports statistics) by `EngagementReachAgent` if `handleNotification` returns `true`.</span></span>
* <span data-ttu-id="9cf26-226">При закрытии hello уведомления hello `exitNotification` вызывается метод, статистика выводится и далее кампаний теперь могут быть обработаны.</span><span class="sxs-lookup"><span data-stu-id="9cf26-226">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="9cf26-227">Если щелкнуть уведомление hello `actionNotification` — вызове сообщается статистики и намерением hello связанные запускается.</span><span class="sxs-lookup"><span data-stu-id="9cf26-227">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated intent is launched.</span></span>

<span data-ttu-id="9cf26-228">Если реализация `EngagementNotifier` обходы hello поведение по умолчанию, вы получите toocall эти методы жизненного цикла по самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="9cf26-228">If your implementation of `EngagementNotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="9cf26-229">Hello в следующих примерах показаны некоторые случаи, где пропускается hello поведение по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="9cf26-229">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="9cf26-230">Вы не расширяли `EngagementDefaultNotifier`, например реализовали обработку категорий с нуля.</span><span class="sxs-lookup"><span data-stu-id="9cf26-230">You don't extend `EngagementDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="9cf26-231">Для системных уведомлений, используемое hello `onNotificationPrepared` и изменен `contentIntent` или `deleteIntent` в hello `Notification` объекта.</span><span class="sxs-lookup"><span data-stu-id="9cf26-231">For system notifications, you overrode hello `onNotificationPrepared` and you modified `contentIntent` or `deleteIntent` in hello `Notification` object.</span></span>
* <span data-ttu-id="9cf26-232">Для уведомления в приложении, используемое `prepareInAppArea`, по крайней мере быть убедиться, что toomap `actionNotification` tooone U.I элементов управления.</span><span class="sxs-lookup"><span data-stu-id="9cf26-232">For in-app notifications, you overrode `prepareInAppArea`, be sure toomap at least `actionNotification` tooone of your U.I controls.</span></span>

> [!NOTE]
> <span data-ttu-id="9cf26-233">Если `handleNotification` создает исключение, hello содержимого удаляется и `dropContent` вызывается.</span><span class="sxs-lookup"><span data-stu-id="9cf26-233">If `handleNotification` throws an exception, hello content is deleted and `dropContent` is called.</span></span> <span data-ttu-id="9cf26-234">Это отражается в статистике, после этого можно обрабатывать последующие кампании.</span><span class="sxs-lookup"><span data-stu-id="9cf26-234">This is reported in statistics and next campaigns can now be processed.</span></span>
> 
> 

### <a name="announcements-and-polls"></a><span data-ttu-id="9cf26-235">Объявления и опросы</span><span class="sxs-lookup"><span data-stu-id="9cf26-235">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="9cf26-236">Макеты</span><span class="sxs-lookup"><span data-stu-id="9cf26-236">Layouts</span></span>
<span data-ttu-id="9cf26-237">Вы можете изменить hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` и `engagement_poll.xml` файлы toocustomize текста извещения, объявлений веб- и опросов.</span><span class="sxs-lookup"><span data-stu-id="9cf26-237">You can modify hello `engagement_text_announcement.xml`, `engagement_web_announcement.xml` and `engagement_poll.xml` files toocustomize text announcements, web announcements and polls.</span></span>

<span data-ttu-id="9cf26-238">Эти файлы используют два распространенных макетов области заголовка hello и область кнопок hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-238">These files share two common layouts for hello title area and hello button area.</span></span> <span data-ttu-id="9cf26-239">Hello макет заголовка hello достаточно `engagement_content_title.xml` и использует hello eponymous drawable файла для фона hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-239">hello layout for hello title is `engagement_content_title.xml` and uses hello eponymous drawable file for hello background.</span></span> <span data-ttu-id="9cf26-240">Hello макет для кнопки действия и выхода hello является `engagement_button_bar.xml` и использует hello eponymous drawable файла для фона hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-240">hello layout for hello action and exit buttons is `engagement_button_bar.xml` and uses hello eponymous drawable file for hello background.</span></span>

<span data-ttu-id="9cf26-241">В опросе, hello вопрос макета и их вариантов динамически завышенными hello несколько раз с помощью `engagement_question.xml` файл макета для вопросов hello и hello `engagement_choice.xml` файл варианты hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-241">In a poll, hello question layout and their choices are dynamically inflated using several times hello `engagement_question.xml` layout file for hello questions and hello `engagement_choice.xml` file for hello choices.</span></span>

#### <a name="categories"></a><span data-ttu-id="9cf26-242">Категории</span><span class="sxs-lookup"><span data-stu-id="9cf26-242">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="9cf26-243">Альтернативные макеты</span><span class="sxs-lookup"><span data-stu-id="9cf26-243">Alternate layouts</span></span>
<span data-ttu-id="9cf26-244">Подобно уведомления категория кампании hello может быть используется toohave дополнительные раскладки для объявлений и опросов.</span><span class="sxs-lookup"><span data-stu-id="9cf26-244">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="9cf26-245">Например, toocreate категорию для объявления текста, можно расширить `EngagementTextAnnouncementActivity` и ссылок на него hello `AndroidManifest.xml` файла:</span><span class="sxs-lookup"><span data-stu-id="9cf26-245">For example, toocreate a category for a text announcement, you can extend `EngagementTextAnnouncementActivity` and reference it hello `AndroidManifest.xml` file:</span></span>

            <activity android:name="com.your_company.MyCustomTextAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/plain" />
              </intent-filter>
            </activity>

<span data-ttu-id="9cf26-246">Обратите внимание, этой категории hello в назначение hello используется фильтр toomake отличие hello действие объявления по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-246">Note that hello category in hello intent filter is used toomake hello difference with hello default announcement activity.</span></span>

<span data-ttu-id="9cf26-247">пакет SDK для Reach Hello использует hello намерения системы tooresolve hello нужного действия для определенной категории и оно переключится на категории по умолчанию hello Если сбой разрешения hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-247">hello Reach SDK uses hello intent system tooresolve hello right activity for a specific category and it falls back on hello default category if hello resolution failed.</span></span>

<span data-ttu-id="9cf26-248">То есть tooimplement `MyCustomTextAnnouncementActivity`, вы просто toochange hello макет должен быть (но сохранить hello и те же идентификаторы представления), у вас toodefine hello класса, например в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="9cf26-248">Then you have tooimplement `MyCustomTextAnnouncementActivity`, if you just want toochange hello layout (but keep hello same view identifiers), you just have toodefine hello class like in hello following example:</span></span>

            public class MyCustomTextAnnouncementActivity extends EngagementTextAnnouncementActivity
            {
              @Override
              protected String getLayoutName()
              {
                return "my_text_announcement";  // tell super class toouse R.layout.my_text_announcement
              }
            }

<span data-ttu-id="9cf26-249">категории по умолчанию hello tooreplace текст объявлений, просто замените `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` реализацией.</span><span class="sxs-lookup"><span data-stu-id="9cf26-249">tooreplace hello default category of text announcements, simply replace `android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity"` by your implementation.</span></span>

<span data-ttu-id="9cf26-250">Аналогичным образом можно настраивать веб-объявления и опросы.</span><span class="sxs-lookup"><span data-stu-id="9cf26-250">Web announcements and polls can be customized in a similar fashion.</span></span>

<span data-ttu-id="9cf26-251">Для объявления web можно расширить `EngagementWebAnnouncementActivity` и объявить свои действия в hello `AndroidManifest.xml` как и в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="9cf26-251">For web announcements you can extend `EngagementWebAnnouncementActivity` and declare your activity in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomWebAnnouncementActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="my_category" />
                <data android:mimeType="text/html" />    <!-- only difference with text announcements in hello intent is hello data mime type -->
              </intent-filter>
            </activity>

<span data-ttu-id="9cf26-252">Опрашивает можно расширить `EngagementPollActivity` и объявите вашей hello в `AndroidManifest.xml` в следующий пример hello, например:</span><span class="sxs-lookup"><span data-stu-id="9cf26-252">For polls you can extend `EngagementPollActivity` and declare your in hello `AndroidManifest.xml` like in hello following example:</span></span>

            <activity android:name="com.your_company.MyCustomPollActivity">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="my_category" />
              </intent-filter>
            </activity>

##### <a name="implementation-from-scratch"></a><span data-ttu-id="9cf26-253">Реализация с нуля</span><span class="sxs-lookup"><span data-stu-id="9cf26-253">Implementation from scratch</span></span>
<span data-ttu-id="9cf26-254">Можно реализовать категорий для действий, объявления (и опроса) без расширения один hello `Engagement*Activity` классов, предоставляемых hello пакет SDK для Reach.</span><span class="sxs-lookup"><span data-stu-id="9cf26-254">You can implement categories for your announcement (and poll) activities without extending one of hello `Engagement*Activity` classes provided by hello Reach SDK.</span></span> <span data-ttu-id="9cf26-255">Это полезно например следует ли toodefine макет, который не использует hello же представления в качестве стандартных макетов hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-255">This is useful for example if you want toodefine a layout that does not use hello same views as hello standard layouts.</span></span>

<span data-ttu-id="9cf26-256">Как и для настройки дополнительных уведомлений рекомендуется toolook в исходный код hello hello стандартную реализацию.</span><span class="sxs-lookup"><span data-stu-id="9cf26-256">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

<span data-ttu-id="9cf26-257">Ниже приведены некоторые вещи tookeep помните: Reach запускает действие hello с определенной целью (соответствующий toohello намерения фильтр) плюс дополнительный параметр, который является идентификатором содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-257">Here are some things tookeep in mind: Reach will launch hello activity with a specific intent (corresponding toohello intent filter) plus an extra parameter which is hello content identifier.</span></span>

<span data-ttu-id="9cf26-258">Это можно сделать содержимого объекта hello tooretrieve, которые содержат поля hello, указанный при создании hello кампании на веб-сайте hello вы:</span><span class="sxs-lookup"><span data-stu-id="9cf26-258">tooretrieve hello content object which contain hello fields you specified when creating hello campaign on hello web site you can do this:</span></span>

            public class MyCustomTextAnnouncement extends EngagementActivity
            {
              private EngagementAnnouncement mContent;

              @Override
              protected void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);

                /* Get content */
                mContent = EngagementReachAgent.getInstance(this).getContent(getIntent());
                if (mContent == null)
                {
                  /* If problem with content, exit */
                  finish();
                  return;
                }

                setContentView(R.layout.my_text_announcement);

                /* Configure views by querying fields on mContent */
                // ...
              }
            }

<span data-ttu-id="9cf26-259">Для статистики, следует сообщать hello содержимое отображается в hello `onResume` событий:</span><span class="sxs-lookup"><span data-stu-id="9cf26-259">For statistics, you should report hello content is displayed in hello `onResume` event:</span></span>

            @Override
            protected void onResume()
            {
             /* Mark hello content displayed */
             mContent.displayContent(this);
             super.onResume();
            }

<span data-ttu-id="9cf26-260">Затем, не забывайте toocall либо `actionContent(this)` или `exitContent(this)` содержимого hello объекта до действие hello в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="9cf26-260">Then, don't forget toocall either `actionContent(this)` or `exitContent(this)` on hello content object before hello activity goes into background.</span></span>

<span data-ttu-id="9cf26-261">Если вы не вызываете либо `actionContent` или `exitContent`, статистические данные не могут быть переданы (т. е. не analytics hello кампании) и более важно, hello Далее кампаний не будет уведомлен до перезапуска процесса приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-261">If you don't call either `actionContent` or `exitContent`, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly, hello next campaigns will not be notified until hello application process is restarted.</span></span>

<span data-ttu-id="9cf26-262">Ориентация или другие изменения в конфигурацию можно делать непростой задачей toodetermine кода hello действие hello переходит в фоновом режиме или нет, hello выполняет стандартную реализацию убедиться, что содержимое hello сообщила о завершился ухода пользователя hello действие hello (или с нажав клавишу `HOME` или `BACK`), но не изменяет ориентацию hello.</span><span class="sxs-lookup"><span data-stu-id="9cf26-262">Orientation or other configuration changes can make hello code tricky toodetermine whether hello activity goes into background or not, hello standard implementation makes sure hello content is reported as exited if hello user leaves hello activity (either by pressing `HOME` or `BACK`) but not if hello orientation changes.</span></span>

<span data-ttu-id="9cf26-263">Вот hello интересное hello реализации:</span><span class="sxs-lookup"><span data-stu-id="9cf26-263">Here is hello interesting part of hello implementation:</span></span>

            @Override
            protected void onUserLeaveHint()
            {
              finish();
            }

            @Override
            protected void onPause()
            {
              if (isFinishing() && mContent != null)
              {
                /*
                 * Exit content on exit, this is has no effect if another process method has already been
                 * called so we don't have toocheck anything here.
                 */
                mContent.exitContent(this);
              }
              super.onPause();
            }

<span data-ttu-id="9cf26-264">Как видите, если вызван `actionContent(this)` завершения действия hello, а затем `exitContent(this)` может быть вызван без необходимости вступать в силу.</span><span class="sxs-lookup"><span data-stu-id="9cf26-264">As you can see, if you called `actionContent(this)` then finished hello activity, `exitContent(this)` can be safely called without having any effect.</span></span>

[here]:http://developer.android.com/tools/extras/support-library.html#Downloading
[Google Cloud Messaging]:http://developer.android.com/guide/google/gcm/index.html
[Amazon Device Messaging]:https://developer.amazon.com/sdk/adm.html
