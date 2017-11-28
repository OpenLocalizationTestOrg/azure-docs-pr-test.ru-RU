---
title: "Интеграция пакета Android SDK для Служб мобильного взаимодействия Azure"
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
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="5dcda-103">Интеграция ADM с платформой Engagement</span><span class="sxs-lookup"><span data-stu-id="5dcda-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5dcda-104">Перед выполнением действий, описанных в этом руководстве, необходимо выполнить процедуру интеграции, описанную в документе "Интеграция Engagement на платформе Android".</span><span class="sxs-lookup"><span data-stu-id="5dcda-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="5dcda-105">Этот документ пригоден только в том случае, если вы уже встроили модуль обработки рекламных кампаний и план для отправки данных на устройства Amazon.</span><span class="sxs-lookup"><span data-stu-id="5dcda-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="5dcda-106">Для интеграции кампаний, обработанных модулем, в приложение необходимо сначала ознакомиться с разделом «Интеграция модуля обработки рекламных кампаний платформы Engagement для Android».</span><span class="sxs-lookup"><span data-stu-id="5dcda-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="5dcda-107">Введение</span><span class="sxs-lookup"><span data-stu-id="5dcda-107">Introduction</span></span>
<span data-ttu-id="5dcda-108">Благодаря интеграции ADM можно передавать ваше приложение при помощи push-технологий на устройства Android, созданные Amazon.</span><span class="sxs-lookup"><span data-stu-id="5dcda-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="5dcda-109">Полезные данные ADM, перемещаемые при помощи push-технологии в пакете SDK, всегда содержат ключ `azme` в объекте данных.</span><span class="sxs-lookup"><span data-stu-id="5dcda-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="5dcda-110">Таким образом, если вы в своем приложении используете ADM для другой цели, вы можете фильтровать push-передачи на основе этого ключа.</span><span class="sxs-lookup"><span data-stu-id="5dcda-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5dcda-111">Только устройства Amazon Kindle под управлением Android 4.0.3 или более поздней версии поддерживаются службой Amazon Device Messaging (ADM). Тем не менее, этот код можно безопасно интегрировать на других устройствах.</span><span class="sxs-lookup"><span data-stu-id="5dcda-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="5dcda-112">Подписка на ADM</span><span class="sxs-lookup"><span data-stu-id="5dcda-112">Sign up to ADM</span></span>
<span data-ttu-id="5dcda-113">Если это еще не сделано, необходимо включить ADM в учетной записи Amazon.</span><span class="sxs-lookup"><span data-stu-id="5dcda-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="5dcda-114">Эта процедура подробно описана на странице [<https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="5dcda-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="5dcda-115">После завершения процедуры вы получаете в свое распоряжение:</span><span class="sxs-lookup"><span data-stu-id="5dcda-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="5dcda-116">Учетные данные OAuth (идентификатор и секрет клиента) для платформы Engagement, чтобы иметь возможность направлять push-уведомления своим устройствам.</span><span class="sxs-lookup"><span data-stu-id="5dcda-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="5dcda-117">Ключ API, который должен быть интегрирован в приложение.</span><span class="sxs-lookup"><span data-stu-id="5dcda-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="5dcda-118">Интеграция пакета SDK</span><span class="sxs-lookup"><span data-stu-id="5dcda-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="5dcda-119">Управление регистрацией устройств</span><span class="sxs-lookup"><span data-stu-id="5dcda-119">Managing device registrations</span></span>
<span data-ttu-id="5dcda-120">Каждое устройство должно отправлять команду регистрации серверам ADM, в противном случае с ними невозможно связаться.</span><span class="sxs-lookup"><span data-stu-id="5dcda-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="5dcda-121">Если вы уже используете [клиентскую библиотеку ADM] и [интегрировали ADM], можно переходить прямо к команде android-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="5dcda-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="5dcda-122">Если интеграция ADM еще не выполнена, платформа Engagement предлагает более простой путь для ее включения в приложении.</span><span class="sxs-lookup"><span data-stu-id="5dcda-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="5dcda-123">Отредактируйте файл `AndroidManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="5dcda-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="5dcda-124">Добавьте пространство имен Amazon, файл должен начинаться следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5dcda-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="5dcda-125">Внутри тега `<application/>` добавьте этот раздел:</span><span class="sxs-lookup"><span data-stu-id="5dcda-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="5dcda-126">После добавление тега Amazon может возникнуть ошибка построения, если конечная сборка проекта ниже версии Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="5dcda-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="5dcda-127">Необходимо использовать конечную сборку **версии Android 2.1 или выше** (не беспокойтесь, значение `minSdkVersion` может быть равным 4).</span><span class="sxs-lookup"><span data-stu-id="5dcda-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="5dcda-128">Интегрируйте ключ API ADM как ресурс, выполнив [следующую процедуру].</span><span class="sxs-lookup"><span data-stu-id="5dcda-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="5dcda-129">Затем выполните указания следующих разделов.</span><span class="sxs-lookup"><span data-stu-id="5dcda-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="5dcda-130">Передайте идентификатор регистрации службе Push-уведомлений платформы Engagement и начните получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="5dcda-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="5dcda-131">Чтобы передать идентификатор регистрации устройства службе push-уведомлений Engagement и получать ее уведомления, необходимо добавить следующий код в файл `AndroidManifest.xml` внутри тега `<application/>` (даже в случае использования ADM без платформы Engagement):</span><span class="sxs-lookup"><span data-stu-id="5dcda-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="5dcda-132">Убедитесь в наличии следующих разрешений в `AndroidManifest.xml` (перед тегом `</application>`).</span><span class="sxs-lookup"><span data-stu-id="5dcda-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="5dcda-133">Предоставление учетных данных OAuth для платформы Engagement</span><span class="sxs-lookup"><span data-stu-id="5dcda-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="5dcda-134">Отправьте учетные данные OAuth (идентификатор и секрет клиента) на портал Engagement.</span><span class="sxs-lookup"><span data-stu-id="5dcda-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="5dcda-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="5dcda-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="5dcda-136">[клиентскую библиотеку ADM]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="5dcda-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="5dcda-137">[интегрировали ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="5dcda-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="5dcda-138">[следующую процедуру]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="5dcda-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>
