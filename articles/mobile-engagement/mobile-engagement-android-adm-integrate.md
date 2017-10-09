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
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="62b36-103">Как tooIntegrate ADM с Engagement</span><span class="sxs-lookup"><span data-stu-id="62b36-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="62b36-104">Необходимо выполнить процедуры интеграции hello, описанной в hello как tooIntegrate Engagement на Android документ до следующего руководства.</span><span class="sxs-lookup"><span data-stu-id="62b36-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="62b36-105">В этом документе полезно только в том случае, если уже встроенный hello Reach модуля и план toopush Amazon устройств.</span><span class="sxs-lookup"><span data-stu-id="62b36-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="62b36-106">кампании Reach toointegrate в вашем приложении, ознакомьтесь сначала как tooIntegrate Engagement Reach на Android.</span><span class="sxs-lookup"><span data-stu-id="62b36-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="62b36-107">Введение</span><span class="sxs-lookup"><span data-stu-id="62b36-107">Introduction</span></span>
<span data-ttu-id="62b36-108">Интеграция ADM позволяет toobe вашего приложения, помещенный при разработке для устройств Amazon Android.</span><span class="sxs-lookup"><span data-stu-id="62b36-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="62b36-109">Полезные данные ADM всегда помещается toohello SDK содержит hello `azme` ключа в hello объекта данных.</span><span class="sxs-lookup"><span data-stu-id="62b36-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="62b36-110">Таким образом, если вы в своем приложении используете ADM для другой цели, вы можете фильтровать push-передачи на основе этого ключа.</span><span class="sxs-lookup"><span data-stu-id="62b36-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62b36-111">Только устройства Amazon Kindle под управлением Android 4.0.3 или более поздней версии поддерживаются службой Amazon Device Messaging (ADM). Тем не менее, этот код можно безопасно интегрировать на других устройствах.</span><span class="sxs-lookup"><span data-stu-id="62b36-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="62b36-112">Регистрация tooADM</span><span class="sxs-lookup"><span data-stu-id="62b36-112">Sign up tooADM</span></span>
<span data-ttu-id="62b36-113">Если это еще не сделано, необходимо включить ADM в учетной записи Amazon.</span><span class="sxs-lookup"><span data-stu-id="62b36-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="62b36-114">подробно описан в процедуре Hello: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="62b36-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="62b36-115">После завершения процедуры hello, вы получите:</span><span class="sxs-lookup"><span data-stu-id="62b36-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="62b36-116">OAuth учетных данных (идентификатор клиента и секрет клиента) для возможности toopush toobe Engagement устройств.</span><span class="sxs-lookup"><span data-stu-id="62b36-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="62b36-117">Ключ API, который должен быть интегрирован в приложение.</span><span class="sxs-lookup"><span data-stu-id="62b36-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="62b36-118">Интеграция пакета SDK</span><span class="sxs-lookup"><span data-stu-id="62b36-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="62b36-119">Управление регистрацией устройств</span><span class="sxs-lookup"><span data-stu-id="62b36-119">Managing device registrations</span></span>
<span data-ttu-id="62b36-120">Каждое устройство должно отправить toohello команда регистрации ADM серверов, в противном случае они не могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="62b36-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="62b36-121">Если вы уже используете hello [ADM клиентская библиотека]и уже есть [интеграции ADM] можно непосредственно перейти tooandroid-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="62b36-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="62b36-122">Если не имеется встроенный ADM еще Engagement имеет более простой способ tooenable его в приложении:</span><span class="sxs-lookup"><span data-stu-id="62b36-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="62b36-123">Отредактируйте файл `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="62b36-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="62b36-124">Добавьте Здравствуйте Amazon пространства имен, hello должен начинаться следующим образом:</span><span class="sxs-lookup"><span data-stu-id="62b36-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="62b36-125">Внутри hello `<application/>` , добавьте в этом разделе:</span><span class="sxs-lookup"><span data-stu-id="62b36-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="62b36-126">После добавления тега amazon hello, может содержать ошибку сборки, если цели построения проекта под Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="62b36-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="62b36-127">У вас есть toouse **Android 2.1 +** собран (не волнуйтесь, вы сможете получить `minSdkVersion` задать too4).</span><span class="sxs-lookup"><span data-stu-id="62b36-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="62b36-128">Интегрировать hello ADM ключ API в качестве ресурса, следуя [этой процедуры].</span><span class="sxs-lookup"><span data-stu-id="62b36-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="62b36-129">Следуйте инструкциям hello hello далее разделах.</span><span class="sxs-lookup"><span data-stu-id="62b36-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="62b36-130">Связи Push обязательств со службой регистрации идентификатора toohello и получать уведомления</span><span class="sxs-lookup"><span data-stu-id="62b36-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="62b36-131">В порядке toocommunicate hello регистрации с идентификатором hello устройства toohello Engagement Push службы и получать его уведомления, добавить следующие tooyour hello `AndroidManifest.xml` файла внутри hello `<application/>` тег (даже если используется ADM без участия):</span><span class="sxs-lookup"><span data-stu-id="62b36-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="62b36-132">Убедитесь, имеются следующие разрешения в hello вашей `AndroidManifest.xml` (перед hello `</application>` тега).</span><span class="sxs-lookup"><span data-stu-id="62b36-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="62b36-133">Предоставление учетных данных OAuth для платформы Engagement</span><span class="sxs-lookup"><span data-stu-id="62b36-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="62b36-134">Отправьте учетные данные OAuth (идентификатор и секрет клиента) на портал Engagement.</span><span class="sxs-lookup"><span data-stu-id="62b36-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html
[ADM клиентская библиотека]:https://developer.amazon.com/sdk/adm/setup.html
[интеграции ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[этой процедуры]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
