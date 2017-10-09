---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a>Как tooIntegrate ADM с Engagement
> [!IMPORTANT]
> Необходимо выполнить процедуры интеграции hello, описанной в hello как tooIntegrate Engagement на Android документ до следующего руководства.
> 
> В этом документе полезно только в том случае, если уже встроенный hello Reach модуля и план toopush Amazon устройств. кампании Reach toointegrate в вашем приложении, ознакомьтесь сначала как tooIntegrate Engagement Reach на Android.
> 
> 

## <a name="introduction"></a>Введение
Интеграция ADM позволяет toobe вашего приложения, помещенный при разработке для устройств Amazon Android.

Полезные данные ADM всегда помещается toohello SDK содержит hello `azme` ключа в hello объекта данных. Таким образом, если вы в своем приложении используете ADM для другой цели, вы можете фильтровать push-передачи на основе этого ключа.

> [!IMPORTANT]
> Только устройства Amazon Kindle под управлением Android 4.0.3 или более поздней версии поддерживаются службой Amazon Device Messaging (ADM). Тем не менее, этот код можно безопасно интегрировать на других устройствах.
> 
> 

## <a name="sign-up-tooadm"></a>Регистрация tooADM
Если это еще не сделано, необходимо включить ADM в учетной записи Amazon.

подробно описан в процедуре Hello: [ <https://developer.amazon.com/sdk/adm/credentials.html>].

После завершения процедуры hello, вы получите:

* OAuth учетных данных (идентификатор клиента и секрет клиента) для возможности toopush toobe Engagement устройств.
* Ключ API, который должен быть интегрирован в приложение.

## <a name="sdk-integration"></a>Интеграция пакета SDK
### <a name="managing-device-registrations"></a>Управление регистрацией устройств
Каждое устройство должно отправить toohello команда регистрации ADM серверов, в противном случае они не могут использоваться.

Если вы уже используете hello [ADM клиентская библиотека]и уже есть [интеграции ADM] можно непосредственно перейти tooandroid-sdk-adm-receive.

Если не имеется встроенный ADM еще Engagement имеет более простой способ tooenable его в приложении:

Отредактируйте файл `AndroidManifest.xml`:

* Добавьте Здравствуйте Amazon пространства имен, hello должен начинаться следующим образом:
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* Внутри hello `<application/>` , добавьте в этом разделе:
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* После добавления тега amazon hello, может содержать ошибку сборки, если цели построения проекта под Android 2.1. У вас есть toouse **Android 2.1 +** собран (не волнуйтесь, вы сможете получить `minSdkVersion` задать too4).
* Интегрировать hello ADM ключ API в качестве ресурса, следуя [этой процедуры].

Следуйте инструкциям hello hello далее разделах.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Связи Push обязательств со службой регистрации идентификатора toohello и получать уведомления
В порядке toocommunicate hello регистрации с идентификатором hello устройства toohello Engagement Push службы и получать его уведомления, добавить следующие tooyour hello `AndroidManifest.xml` файла внутри hello `<application/>` тег (даже если используется ADM без участия):

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

Убедитесь, имеются следующие разрешения в hello вашей `AndroidManifest.xml` (перед hello `</application>` тега).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>Предоставление учетных данных OAuth для платформы Engagement
Отправьте учетные данные OAuth (идентификатор и секрет клиента) на портал Engagement.

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM клиентская библиотека]:https://developer.amazon.com/sdk/adm/setup.html
[интеграции ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[этой процедуры]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
