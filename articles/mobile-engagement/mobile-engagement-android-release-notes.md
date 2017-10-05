---
title: "Интеграция пакета Android SDK для Служб мобильного взаимодействия Azure"
description: "Последние обновления и процедуры пакета Android SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="0ad9c-103">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="0ad9c-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="0ad9c-104">4.3.1 (17.07.2017)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="0ad9c-105">Исправлена проблема с аварийным завершением работы, которое изредка могло происходить при вызове `EngagementAgentUtils.isInDedicatedEngagementProcess` (также используется классом `EngagementApplication`).</span><span class="sxs-lookup"><span data-stu-id="0ad9c-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="0ad9c-106">4.3.0 (27.06.2017)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="0ad9c-107">Поддержка Android 8 (предыдущие версии пакета SDK не будут работать с Android 8).</span><span class="sxs-lookup"><span data-stu-id="0ad9c-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="0ad9c-108">Удалена зависимость от библиотеки поддержки.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-108">No more dependency on support library.</span></span>
* <span data-ttu-id="0ad9c-109">Удален класс `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="0ad9c-110">Из-за [ограничений на фоновое выполнение приложений](https://developer.android.com/preview/features/background.html) в Android 8 журналы в фоновом режиме могут отображаться с задержкой (когда пользователь воспользуется устройством), что, в свою очередь, может повлиять на отображение статистики по **доставленным** push-уведомлениям и **отображенным системным уведомлениям**. Причина — соответствующие данные не поступают, пока устройство находится в спящем режиме. (Это не повлияет на отображение уведомления, подачу устройством звукового сигнала и вибросигнала в реальном времени.)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="0ad9c-111">Из-за [ограничений на доступ к геолокационным данным в фоновом режиме](https://developer.android.com/preview/features/background-location-limits.html) данные о текущем местонахождении не будут часто обновляться в Android 8.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="0ad9c-112">4.2.4 (30.03.2017)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="0ad9c-113">Исправление цвета текста уведомления в приложениях на Android 7 для совпадения с цветом в старых версиях Android.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="0ad9c-114">4.2.3 (10.08.2016)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="0ad9c-115">Больше не блокируется сеть Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-115">No more WIFI lock.</span></span>
* <span data-ttu-id="0ad9c-116">Устранена взаимоблокировка при вызове getDeviceId перед инициализацией (ошибка появилась в версии 4.2.0).</span><span class="sxs-lookup"><span data-stu-id="0ad9c-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="0ad9c-117">4.2.2 (17.05.2016)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="0ad9c-118">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="0ad9c-119">4.2.1 (10.05.2016)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="0ad9c-120">Безопасность: отключение доступа к локальному файлу веб-представления.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="0ad9c-121">Безопасность: удаление класса `EngagementPreferenceActivity`, расширяющего устаревший и небезопасный класс `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="0ad9c-122">Безопасность: действия модуля Reach теперь официально используют `exported="false"`, этот флаг можно также применять в предыдущих версиях пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="0ad9c-123">4.2.0 (11.03.2016)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="0ad9c-124">Пакет SDK теперь лицензируется MIT.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="0ad9c-125">Разрешено указание пользовательского идентификатора устройства во время инициализации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="0ad9c-126">4.1.5 (01.02.2016)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="0ad9c-127">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="0ad9c-128">4.1.4 (26.01.2016)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="0ad9c-129">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="0ad9c-130">4.1.3 (09.12.2015)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="0ad9c-131">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="0ad9c-132">4.1.2 (25.11.2015)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="0ad9c-133">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="0ad9c-134">4.1.1 (04.11.2015)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="0ad9c-135">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="0ad9c-136">4.1.0 (25.08.2015)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="0ad9c-137">Обработка новой модели разрешений для Android M.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="0ad9c-138">Возможность настройки функций расположения в среде выполнения, а не с помощью `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="0ad9c-139">Исправление ошибки разрешений: если используется `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="0ad9c-140">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="0ad9c-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="0ad9c-142">Внутренние изменения протокола для повышения надежности аналитики и push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="0ad9c-143">Системные push-уведомления (GCM/ADM) теперь также используются для уведомлений из приложений, поэтому их учетные данные необходимо задавать для всех типов кампаний push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="0ad9c-144">Исправлены ошибки общих уведомлений: ранее они отображались только 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="0ad9c-145">Исправлена ошибка веб-представления: щелчок по ссылке также приводил к открытию URL-адреса действия по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="0ad9c-146">Исправлена ошибка, связанная с редкими сбоями при управлении локальным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="0ad9c-147">Исправлена ошибка, связанная с динамическим управлением строкой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="0ad9c-148">Обновлено лицензионное соглашение с пользователем.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="0ad9c-149">3.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="0ad9c-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="0ad9c-150">Первый выпуск Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="0ad9c-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="0ad9c-151">Конфигурация appId заменена на конфигурацию строки подключения.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="0ad9c-152">Удален API для отправки и получения произвольных сообщений XMPP из произвольных сущностей XMPP.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="0ad9c-153">Удален API для отправки и получения сообщений между устройствами.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="0ad9c-154">Улучшения безопасности.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-154">Security improvements.</span></span>
* <span data-ttu-id="0ad9c-155">Удалено отслеживание Google Play и SmartAd.</span><span class="sxs-lookup"><span data-stu-id="0ad9c-155">Google Play and SmartAd tracking removed.</span></span>

