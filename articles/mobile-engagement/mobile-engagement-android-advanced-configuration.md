---
title: "Конфигурация aaaAdvanced для Azure Mobile Engagement Android SDK"
description: "Описывает дополнительные параметры конфигурации, включая Android манифест с Azure Mobile Engagement Android SDK hello hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a><span data-ttu-id="fd6ef-103">Расширенная конфигурация для пакета SDK Android для Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="fd6ef-103">Advanced configuration for Azure Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd6ef-104">Универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="fd6ef-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="fd6ef-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="fd6ef-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="fd6ef-106">iOS</span><span class="sxs-lookup"><span data-stu-id="fd6ef-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="fd6ef-107">Android</span><span class="sxs-lookup"><span data-stu-id="fd6ef-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
>
>

<span data-ttu-id="fd6ef-108">Эта процедура описывает, как tooconfigure различные параметры конфигурации для приложения Azure Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd6ef-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fd6ef-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a><span data-ttu-id="fd6ef-110">Требования к разрешениям</span><span class="sxs-lookup"><span data-stu-id="fd6ef-110">Permission Requirements</span></span>
<span data-ttu-id="fd6ef-111">Некоторые параметры необходимы специальные разрешения, которые перечисленные здесь ссылки и в строках hello определенного компонента.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-111">Some options require specific permissions, all of which are listed here for reference, and in-line in hello specific feature.</span></span> <span data-ttu-id="fd6ef-112">Добавьте эти разрешения toohello AndroidManifest.xml проекта непосредственно перед или после hello `<application>` тег.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-112">Add these permissions toohello AndroidManifest.xml of your project immediately before or after hello `<application>` tag.</span></span>

<span data-ttu-id="fd6ef-113">Код разрешения Hello должен toolook следующего вида hello, где следует заполнить hello соответствующее разрешение из hello приведен в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-113">hello permission code needs toolook like hello following, where you fill in hello appropriate permission from hello table that follows.</span></span>

    <uses-permission android:name="android.permission.[specific permission]"/>


| <span data-ttu-id="fd6ef-114">Разрешение</span><span class="sxs-lookup"><span data-stu-id="fd6ef-114">Permission</span></span> | <span data-ttu-id="fd6ef-115">Применение</span><span class="sxs-lookup"><span data-stu-id="fd6ef-115">When used</span></span> |
| --- | --- |
| <span data-ttu-id="fd6ef-116">ИНТЕРНЕТ</span><span class="sxs-lookup"><span data-stu-id="fd6ef-116">INTERNET</span></span> |<span data-ttu-id="fd6ef-117">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-117">Required.</span></span> <span data-ttu-id="fd6ef-118">Базовые отчеты</span><span class="sxs-lookup"><span data-stu-id="fd6ef-118">For basic reporting</span></span> |
| <span data-ttu-id="fd6ef-119">ACCESS_NETWORK_STATE</span><span class="sxs-lookup"><span data-stu-id="fd6ef-119">ACCESS_NETWORK_STATE</span></span> |<span data-ttu-id="fd6ef-120">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-120">Required.</span></span> <span data-ttu-id="fd6ef-121">Базовые отчеты</span><span class="sxs-lookup"><span data-stu-id="fd6ef-121">For basic reporting</span></span> |
| <span data-ttu-id="fd6ef-122">RECEIVE_BOOT_COMPLETED</span><span class="sxs-lookup"><span data-stu-id="fd6ef-122">RECEIVE_BOOT_COMPLETED</span></span> |<span data-ttu-id="fd6ef-123">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-123">Required.</span></span> <span data-ttu-id="fd6ef-124">tooshow копирование центра уведомлений hello после перезагрузки устройства</span><span class="sxs-lookup"><span data-stu-id="fd6ef-124">tooshow up hello notifications center after device reboot</span></span> |
| <span data-ttu-id="fd6ef-125">WAKE_LOCK</span><span class="sxs-lookup"><span data-stu-id="fd6ef-125">WAKE_LOCK</span></span> |<span data-ttu-id="fd6ef-126">(рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="fd6ef-126">Recommended.</span></span> <span data-ttu-id="fd6ef-127">Включает сбор данных при использовании Wi-Fi или при выключенном экране</span><span class="sxs-lookup"><span data-stu-id="fd6ef-127">Enables collecting data when using WiFi or when screen is off</span></span> |
| <span data-ttu-id="fd6ef-128">VIBRATE</span><span class="sxs-lookup"><span data-stu-id="fd6ef-128">VIBRATE</span></span> |<span data-ttu-id="fd6ef-129">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-129">Optional.</span></span> <span data-ttu-id="fd6ef-130">Включает вибрацию при получении уведомления</span><span class="sxs-lookup"><span data-stu-id="fd6ef-130">Enables vibration when notifications are received</span></span> |
| <span data-ttu-id="fd6ef-131">DOWNLOAD_WITHOUT_NOTIFICATION</span><span class="sxs-lookup"><span data-stu-id="fd6ef-131">DOWNLOAD_WITHOUT_NOTIFICATION</span></span> |<span data-ttu-id="fd6ef-132">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-132">Optional.</span></span> <span data-ttu-id="fd6ef-133">Включает общие уведомления Android</span><span class="sxs-lookup"><span data-stu-id="fd6ef-133">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="fd6ef-134">WRITE_EXTERNAL_STORAGE</span><span class="sxs-lookup"><span data-stu-id="fd6ef-134">WRITE_EXTERNAL_STORAGE</span></span> |<span data-ttu-id="fd6ef-135">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-135">Optional.</span></span> <span data-ttu-id="fd6ef-136">Включает общие уведомления Android</span><span class="sxs-lookup"><span data-stu-id="fd6ef-136">Enables Android Big Picture Notification</span></span> |
| <span data-ttu-id="fd6ef-137">ACCESS_COARSE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="fd6ef-137">ACCESS_COARSE_LOCATION</span></span> |<span data-ttu-id="fd6ef-138">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-138">Optional.</span></span> <span data-ttu-id="fd6ef-139">Включает отчет о расположении в реальном времени</span><span class="sxs-lookup"><span data-stu-id="fd6ef-139">Enables Real-time location reporting</span></span> |
| <span data-ttu-id="fd6ef-140">ACCESS_FINE_LOCATION</span><span class="sxs-lookup"><span data-stu-id="fd6ef-140">ACCESS_FINE_LOCATION</span></span> |<span data-ttu-id="fd6ef-141">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-141">Optional.</span></span> <span data-ttu-id="fd6ef-142">Включает отчет о расположении на основе GPS</span><span class="sxs-lookup"><span data-stu-id="fd6ef-142">Enables GPS-based location reporting</span></span> |

<span data-ttu-id="fd6ef-143">Начиная с Android M [управление некоторыми разрешениями осуществляется в среде выполнения](mobile-engagement-android-location-reporting.md#android-m-permissions).</span><span class="sxs-lookup"><span data-stu-id="fd6ef-143">Starting with Android M, [some permissions are managed at run time](mobile-engagement-android-location-reporting.md#android-m-permissions).</span></span>

<span data-ttu-id="fd6ef-144">Если вы уже используете ``ACCESS_FINE_LOCATION``, то tooalso не нужно использовать ``ACCESS_COARSE_LOCATION``.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-144">If you are already using ``ACCESS_FINE_LOCATION``, then you don't need tooalso use ``ACCESS_COARSE_LOCATION``.</span></span>

## <a name="android-manifest-configuration-options"></a><span data-ttu-id="fd6ef-145">Варианты настройки манифеста для Android</span><span class="sxs-lookup"><span data-stu-id="fd6ef-145">Android Manifest configuration options</span></span>
### <a name="crash-report"></a><span data-ttu-id="fd6ef-146">Отчет о сбоях</span><span class="sxs-lookup"><span data-stu-id="fd6ef-146">Crash report</span></span>
<span data-ttu-id="fd6ef-147">отчеты о сбоях toodisable, добавьте следующий код между hello `<application>` и `</application>` теги:</span><span class="sxs-lookup"><span data-stu-id="fd6ef-147">toodisable crash reports, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a><span data-ttu-id="fd6ef-148">Пороговое значение пакета</span><span class="sxs-lookup"><span data-stu-id="fd6ef-148">Burst threshold</span></span>
<span data-ttu-id="fd6ef-149">По умолчанию hello Engagement службы отчетов входит в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-149">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="fd6ef-150">Если журналы отчетов приложения часто изменяться, это лучше toobuffer hello журналы и tooreport их все за один раз на обычное время базового (называемые «быстрый режим»).</span><span class="sxs-lookup"><span data-stu-id="fd6ef-150">If your application report logs vary frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (called "burst mode").</span></span> <span data-ttu-id="fd6ef-151">toodo таким образом, добавьте следующий код между hello `<application>` и `</application>` теги:</span><span class="sxs-lookup"><span data-stu-id="fd6ef-151">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

<span data-ttu-id="fd6ef-152">Пакетный режим немного увеличивает hello аккумулятора, но оказывает влияние на hello монитор Engagement: продолжительность все сеансы и задания являются скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны).</span><span class="sxs-lookup"><span data-stu-id="fd6ef-152">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="fd6ef-153">Пороговое значение пакета не должно превышать 30 000 (30 с).</span><span class="sxs-lookup"><span data-stu-id="fd6ef-153">Your burst threshold should be no longer than 30000 (30s).</span></span>

### <a name="session-timeout"></a><span data-ttu-id="fd6ef-154">Время ожидания сеанса</span><span class="sxs-lookup"><span data-stu-id="fd6ef-154">Session timeout</span></span>
 <span data-ttu-id="fd6ef-155">Можно завершить действие, нажав клавишу hello **Главная** или **обратно** ключа по параметр телефону hello простоя или переходе в другое приложение.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-155">You can end an activity by pressing hello **Home** or **Back** key, by setting hello phone idle or by jumping into another application.</span></span> <span data-ttu-id="fd6ef-156">По умолчанию сеанс будет завершен десять секунд после окончания hello его последнее действие.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-156">By default, a session is ended ten seconds after hello end of its last activity.</span></span> <span data-ttu-id="fd6ef-157">Это позволяет избежать разбиения сеанса каждого пользователя hello времени завершает работу и возвращает toohello приложение быстро, проверяющее может произойти при hello пользователь выбирает изображения, уведомления и т. д. Вы можете toomodify этот параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-157">This avoids a session split each time hello user exits and returns toohello application quickly, which can happen when hello user picks up an image, checks a notification, etc. You may want toomodify this parameter.</span></span> <span data-ttu-id="fd6ef-158">toodo таким образом, добавьте следующий код между hello `<application>` и `</application>` теги:</span><span class="sxs-lookup"><span data-stu-id="fd6ef-158">toodo so, add this code between hello `<application>` and `</application>` tags:</span></span>

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a><span data-ttu-id="fd6ef-159">Выключение отчетов журналов</span><span class="sxs-lookup"><span data-stu-id="fd6ef-159">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="fd6ef-160">Использование вызова метода</span><span class="sxs-lookup"><span data-stu-id="fd6ef-160">Using a method call</span></span>
<span data-ttu-id="fd6ef-161">Если требуется toostop Engagement отправляет журналов, можно вызвать:</span><span class="sxs-lookup"><span data-stu-id="fd6ef-161">If you want Engagement toostop sending logs, you can call:</span></span>

    EngagementAgent.getInstance(context).setEnabled(false);

<span data-ttu-id="fd6ef-162">Этот вызов является постоянным: он использует файл общих параметров.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-162">This call is persistent: it uses a shared preferences file.</span></span>

<span data-ttu-id="fd6ef-163">Если Engagement активен при вызове этой функции, может потребоваться одной минуты для службы toostop hello.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-163">If Engagement is active when you call this function, it may take one minute for hello service toostop.</span></span> <span data-ttu-id="fd6ef-164">Однако он не будет запускать службы hello во всех hello следующих запусках приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-164">However it won't launch hello service at all hello next time you launch hello application.</span></span>

<span data-ttu-id="fd6ef-165">Можно включить снова отчетов путем вызова hello одинаково функционировать с журнала `true`.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-165">You can enable log reporting again by calling hello same function with `true`.</span></span>

### <a name="integration-in-your-own-preferenceactivity"></a><span data-ttu-id="fd6ef-166">Интеграция в собственное `PreferenceActivity`</span><span class="sxs-lookup"><span data-stu-id="fd6ef-166">Integration in your own `PreferenceActivity`</span></span>
<span data-ttu-id="fd6ef-167">Вместо вызова этой функции вы можете интегрировать данный параметр непосредственно в существующее `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-167">Instead of calling this function, you can also integrate this setting directly in your existing `PreferenceActivity`.</span></span>

<span data-ttu-id="fd6ef-168">Можно настроить toouse Engagement предпочтениями-файл (hello нужный режим) в hello `AndroidManifest.xml` , что файл `application meta-data`:</span><span class="sxs-lookup"><span data-stu-id="fd6ef-168">You can configure Engagement toouse your preferences file (with hello desired mode) in hello `AndroidManifest.xml` file with `application meta-data`:</span></span>

* <span data-ttu-id="fd6ef-169">Hello `engagement:agent:settings:name` ключ является именем hello используется toodefine hello Общие настройки файла.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-169">hello `engagement:agent:settings:name` key is used toodefine hello name of hello shared preferences file.</span></span>
* <span data-ttu-id="fd6ef-170">Hello `engagement:agent:settings:mode` ключа является режимом hello используется toodefine hello Общие настройки файла.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-170">hello `engagement:agent:settings:mode` key is used toodefine hello mode of hello shared preferences file.</span></span> <span data-ttu-id="fd6ef-171">Используйте hello же режим, как и в вашей `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-171">Use hello same mode as in your `PreferenceActivity`.</span></span> <span data-ttu-id="fd6ef-172">режим Hello должен быть передан как число: при использовании в коде является комбинацией флагов константой проверить общее значение hello.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-172">hello mode must be passed as a number: if you are using a combination of constant flags in your code, check hello total value.</span></span>

<span data-ttu-id="fd6ef-173">Engagement всегда использует hello `engagement:key` логическое ключа из файла параметров hello для управления этот параметр.</span><span class="sxs-lookup"><span data-stu-id="fd6ef-173">Engagement always uses hello `engagement:key` boolean key within hello preferences file for managing this setting.</span></span>

<span data-ttu-id="fd6ef-174">Следующий пример Hello `AndroidManifest.xml` показано hello значения по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="fd6ef-174">hello following example of `AndroidManifest.xml` shows hello default values:</span></span>

    <application>
        [...]
        <meta-data
          android:name="engagement:agent:settings:name"
          android:value="engagement.agent" />
        <meta-data
          android:name="engagement:agent:settings:mode"
          android:value="0" />

<span data-ttu-id="fd6ef-175">Затем можно добавить `CheckBoxPreference` в макете предпочтения как hello, выполнив одно:</span><span class="sxs-lookup"><span data-stu-id="fd6ef-175">Then you can add a `CheckBoxPreference` in your preference layout like hello following one:</span></span>

    <CheckBoxPreference
      android:key="engagement:enabled"
      android:defaultValue="true"
      android:title="Use Engagement"
      android:summaryOn="Engagement is enabled."
      android:summaryOff="Engagement is disabled." />
