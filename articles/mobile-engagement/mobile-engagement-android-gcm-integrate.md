---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="ca5c8-103">Как tooIntegrate GCM с мобильного охвата</span><span class="sxs-lookup"><span data-stu-id="ca5c8-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ca5c8-104">Необходимо выполнить процедуры интеграции hello, описанной в hello как tooIntegrate Engagement на Android документ до следующего руководства.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="ca5c8-105">В этом документе полезно только в том случае, если уже интеграции hello достигают модуля и план toopush Google Play устройств.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="ca5c8-106">кампании Reach toointegrate в вашем приложении, ознакомьтесь сначала как tooIntegrate Engagement Reach на Android.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="ca5c8-107">Введение</span><span class="sxs-lookup"><span data-stu-id="ca5c8-107">Introduction</span></span>
<span data-ttu-id="ca5c8-108">Интеграция GCM позволяет вашей toobe приложения передано.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="ca5c8-109">GCM полезных данных всегда помещается toohello SDK содержит hello `azme` ключа в hello объекта данных.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="ca5c8-110">Таким образом, если вы в своем приложении используете GCM для другой цели, вы можете фильтровать push-передачи в зависимости от этого ключа.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca5c8-111">С помощью GCM отправлять push-уведомления можно только на устройства под управлением Android 2.2 или выше с установленным Google Play, а также включенным фоновым подключением Google. Тем не менее, этот код можно безопасно интегрировать и на неподдерживаемых  устройствах (он использует только намерения).</span><span class="sxs-lookup"><span data-stu-id="ca5c8-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="ca5c8-112">Создание проекта Google Cloud Messaging с ключом API</span><span class="sxs-lookup"><span data-stu-id="ca5c8-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="ca5c8-113">Интеграция пакета SDK</span><span class="sxs-lookup"><span data-stu-id="ca5c8-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="ca5c8-114">Управление регистрацией устройств</span><span class="sxs-lookup"><span data-stu-id="ca5c8-114">Managing device registrations</span></span>
<span data-ttu-id="ca5c8-115">Каждое устройство должно отправить toohello команда регистрации серверам Google, в противном случае они не могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="ca5c8-116">Устройства также можно отменить регистрацию уведомления GCM (hello устройства отменяется автоматически при удалении приложения hello).</span><span class="sxs-lookup"><span data-stu-id="ca5c8-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="ca5c8-117">Если вы не используете [Google воспроизвести SDK] или не уже отправляется намерение регистрации hello самостоятельно, можно сделать Engagement автоматически зарегистрировать устройство hello для вас.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="ca5c8-118">tooenable это, добавьте следующие tooyour hello `AndroidManifest.xml` файла внутри hello `<application/>` тег:</span><span class="sxs-lookup"><span data-stu-id="ca5c8-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="ca5c8-119">Связи Push обязательств со службой регистрации идентификатора toohello и получать уведомления</span><span class="sxs-lookup"><span data-stu-id="ca5c8-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="ca5c8-120">В порядке toocommunicate hello регистрации с идентификатором hello устройства toohello Engagement Push службы и получать его уведомления, добавить следующие tooyour hello `AndroidManifest.xml` файла внутри hello `<application/>` тег (даже если регистрация устройств управлять самостоятельно):</span><span class="sxs-lookup"><span data-stu-id="ca5c8-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="ca5c8-121">Убедитесь, имеются следующие разрешения в hello вашей `AndroidManifest.xml` (после hello `</application>` тега).</span><span class="sxs-lookup"><span data-stu-id="ca5c8-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="ca5c8-122">Предоставление мобильного охвата доступа tooyour ключ API GCM</span><span class="sxs-lookup"><span data-stu-id="ca5c8-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="ca5c8-123">Выполните [в этом руководстве](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) tooyour доступа мобильного охвата toogrant ключ API GCM.</span><span class="sxs-lookup"><span data-stu-id="ca5c8-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[Google воспроизвести SDK]:https://developers.google.com/cloud-messaging/android/start
