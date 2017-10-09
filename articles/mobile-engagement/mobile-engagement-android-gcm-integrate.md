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
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>Как tooIntegrate GCM с мобильного охвата
> [!IMPORTANT]
> Необходимо выполнить процедуры интеграции hello, описанной в hello как tooIntegrate Engagement на Android документ до следующего руководства.
> 
> В этом документе полезно только в том случае, если уже интеграции hello достигают модуля и план toopush Google Play устройств. кампании Reach toointegrate в вашем приложении, ознакомьтесь сначала как tooIntegrate Engagement Reach на Android.
> 
> 

## <a name="introduction"></a>Введение
Интеграция GCM позволяет вашей toobe приложения передано.

GCM полезных данных всегда помещается toohello SDK содержит hello `azme` ключа в hello объекта данных. Таким образом, если вы в своем приложении используете GCM для другой цели, вы можете фильтровать push-передачи в зависимости от этого ключа.

> [!IMPORTANT]
> С помощью GCM отправлять push-уведомления можно только на устройства под управлением Android 2.2 или выше с установленным Google Play, а также включенным фоновым подключением Google. Тем не менее, этот код можно безопасно интегрировать и на неподдерживаемых  устройствах (он использует только намерения).
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>Создание проекта Google Cloud Messaging с ключом API
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>Интеграция пакета SDK
### <a name="managing-device-registrations"></a>Управление регистрацией устройств
Каждое устройство должно отправить toohello команда регистрации серверам Google, в противном случае они не могут использоваться.

Устройства также можно отменить регистрацию уведомления GCM (hello устройства отменяется автоматически при удалении приложения hello).

Если вы не используете [Google воспроизвести SDK] или не уже отправляется намерение регистрации hello самостоятельно, можно сделать Engagement автоматически зарегистрировать устройство hello для вас.

tooenable это, добавьте следующие tooyour hello `AndroidManifest.xml` файла внутри hello `<application/>` тег:

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Связи Push обязательств со службой регистрации идентификатора toohello и получать уведомления
В порядке toocommunicate hello регистрации с идентификатором hello устройства toohello Engagement Push службы и получать его уведомления, добавить следующие tooyour hello `AndroidManifest.xml` файла внутри hello `<application/>` тег (даже если регистрация устройств управлять самостоятельно):

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

Убедитесь, имеются следующие разрешения в hello вашей `AndroidManifest.xml` (после hello `</application>` тега).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Предоставление мобильного охвата доступа tooyour ключ API GCM
Выполните [в этом руководстве](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) tooyour доступа мобильного охвата toogrant ключ API GCM.

[Google воспроизвести SDK]:https://developers.google.com/cloud-messaging/android/start
