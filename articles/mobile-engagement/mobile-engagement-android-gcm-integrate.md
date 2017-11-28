---
title: "Интеграция пакета Android SDK для Служб мобильного взаимодействия Azure"
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
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="b45ba-103">Интеграция GCM с помощью Служб мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="b45ba-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b45ba-104">Перед выполнением действий, описанных в этом руководстве, необходимо выполнить процедуру интеграции, описанную в документе "Интеграция Engagement на платформе Android".</span><span class="sxs-lookup"><span data-stu-id="b45ba-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="b45ba-105">Этот документ пригоден только в том случае, если вы уже встроили модуль обработки рекламных кампаний и план для отправки данных на устройства Google Play.</span><span class="sxs-lookup"><span data-stu-id="b45ba-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="b45ba-106">Для интеграции кампаний, обработанных модулем, в приложение необходимо сначала ознакомиться с разделом «Интеграция модуля обработки рекламных кампаний платформы Engagement для Android».</span><span class="sxs-lookup"><span data-stu-id="b45ba-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="b45ba-107">Введение</span><span class="sxs-lookup"><span data-stu-id="b45ba-107">Introduction</span></span>
<span data-ttu-id="b45ba-108">Интеграция GCM позволяет приложению получать push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="b45ba-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="b45ba-109">Полезные данные GCM, перемещаемые при помощи push-технологии в SDK, всегда содержат ключ `azme` в объекте данных.</span><span class="sxs-lookup"><span data-stu-id="b45ba-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="b45ba-110">Таким образом, если вы в своем приложении используете GCM для другой цели, вы можете фильтровать push-передачи в зависимости от этого ключа.</span><span class="sxs-lookup"><span data-stu-id="b45ba-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b45ba-111">С помощью GCM отправлять push-уведомления можно только на устройства под управлением Android 2.2 или выше с установленным Google Play, а также включенным фоновым подключением Google. Тем не менее, этот код можно безопасно интегрировать и на неподдерживаемых  устройствах (он использует только намерения).</span><span class="sxs-lookup"><span data-stu-id="b45ba-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="b45ba-112">Создание проекта Google Cloud Messaging с ключом API</span><span class="sxs-lookup"><span data-stu-id="b45ba-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="b45ba-113">Интеграция пакета SDK</span><span class="sxs-lookup"><span data-stu-id="b45ba-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="b45ba-114">Управление регистрацией устройств</span><span class="sxs-lookup"><span data-stu-id="b45ba-114">Managing device registrations</span></span>
<span data-ttu-id="b45ba-115">Каждое устройство должно отправлять команду регистрации серверам Google, в противном случае с ними невозможно связаться.</span><span class="sxs-lookup"><span data-stu-id="b45ba-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="b45ba-116">Устройство также может отменить регистрацию на получение уведомлений GCM (отмена регистрации устройства выполняется автоматически при удалении приложения).</span><span class="sxs-lookup"><span data-stu-id="b45ba-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="b45ba-117">Если вы не используете [пакет SDK для Google Play] или еще не отправили намерение регистрации, можно сделать так, чтобы платформа Engagement выполняла регистрацию устройств автоматически.</span><span class="sxs-lookup"><span data-stu-id="b45ba-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="b45ba-118">Для этого добавьте следующий код в файл `AndroidManifest.xml` внутри тега `<application/>`:</span><span class="sxs-lookup"><span data-stu-id="b45ba-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="b45ba-119">Передайте идентификатор регистрации службе Push-уведомлений платформы Engagement и начните получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="b45ba-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="b45ba-120">Чтобы передать идентификатор регистрации устройства службе push-уведомлений Engagement и получать ее уведомления, необходимо добавить следующий код в файл `AndroidManifest.xml` внутри тега `<application/>` (даже если вы управляете регистрацией устройств самостоятельно):</span><span class="sxs-lookup"><span data-stu-id="b45ba-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="b45ba-121">Убедитесь в наличии следующих разрешений в `AndroidManifest.xml` (после тега `</application>`).</span><span class="sxs-lookup"><span data-stu-id="b45ba-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="b45ba-122">Предоставление Службам мобильного взаимодействия доступа к ключу API GCM</span><span class="sxs-lookup"><span data-stu-id="b45ba-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="b45ba-123">Следуйте [этому руководству](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key), чтобы предоставить Службам мобильного взаимодействия доступ к вашему ключу API GCM.</span><span class="sxs-lookup"><span data-stu-id="b45ba-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

<span data-ttu-id="b45ba-124">[пакет SDK для Google Play]:https://developers.google.com/cloud-messaging/android/start</span><span class="sxs-lookup"><span data-stu-id="b45ba-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span></span>
