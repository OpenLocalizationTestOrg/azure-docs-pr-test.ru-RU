---
title: "aaaAzure интеграции пакета SDK Android Mobile Engagement"
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
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a><span data-ttu-id="305e1-103">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="305e1-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="305e1-104">4.3.1 (17.07.2017)</span><span class="sxs-lookup"><span data-stu-id="305e1-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="305e1-105">Исключена аварийного завершения работы, которая могла происходить редко, при вызове `EngagementAgentUtils.isInDedicatedEngagementProcess`, который также используется для hello `EngagementApplication` класса.</span><span class="sxs-lookup"><span data-stu-id="305e1-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="305e1-106">4.3.0 (27.06.2017)</span><span class="sxs-lookup"><span data-stu-id="305e1-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="305e1-107">8 Поддержка Android (предыдущие версии hello SDK не будет работать в Android 8).</span><span class="sxs-lookup"><span data-stu-id="305e1-107">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="305e1-108">Удалена зависимость от библиотеки поддержки.</span><span class="sxs-lookup"><span data-stu-id="305e1-108">No more dependency on support library.</span></span>
* <span data-ttu-id="305e1-109">Удален класс `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="305e1-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="305e1-110">Из-за слишком[ограничения выполнения фоновой](https://developer.android.com/preview/features/background.html) в Android 8 журналы в фоновом режиме может быть отложен до hello пользователь взаимодействует с устройством hello, это повлияет на кампании Push **доставлено** и **Системное уведомление выводится** статистики задерживается, если устройство hello находится в спящем режиме (hello уведомление будет отображаться, будет кольца и компакт-дисков в реальном времени без проблем).</span><span class="sxs-lookup"><span data-stu-id="305e1-110">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="305e1-111">Из-за слишком[ограничения расположения фона](https://developer.android.com/preview/features/background-location-limits.html), расположение hello реального времени в фоновом режиме не будет часто обновляться в Android 8.</span><span class="sxs-lookup"><span data-stu-id="305e1-111">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="305e1-112">4.2.4 (30.03.2017)</span><span class="sxs-lookup"><span data-stu-id="305e1-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="305e1-113">Исправьте уведомлений в приложения, цвета текста на Android 7 toobe Здравствуйте таким же, как более старые версии Android.</span><span class="sxs-lookup"><span data-stu-id="305e1-113">Fix in-app notification text colors on Android 7 toobe hello same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="305e1-114">4.2.3 (10.08.2016)</span><span class="sxs-lookup"><span data-stu-id="305e1-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="305e1-115">Больше не блокируется сеть Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="305e1-115">No more WIFI lock.</span></span>
* <span data-ttu-id="305e1-116">Устранена взаимоблокировка при вызове getDeviceId перед инициализацией (ошибка появилась в версии 4.2.0).</span><span class="sxs-lookup"><span data-stu-id="305e1-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="305e1-117">4.2.2 (17.05.2016)</span><span class="sxs-lookup"><span data-stu-id="305e1-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="305e1-118">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="305e1-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="305e1-119">4.2.1 (10.05.2016)</span><span class="sxs-lookup"><span data-stu-id="305e1-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="305e1-120">Безопасность: отключение доступа к локальному файлу веб-представления.</span><span class="sxs-lookup"><span data-stu-id="305e1-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="305e1-121">Безопасность: удаление класса `EngagementPreferenceActivity`, расширяющего устаревший и небезопасный класс `PreferenceActivity`.</span><span class="sxs-lookup"><span data-stu-id="305e1-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="305e1-122">Безопасность: reach действия — теперь задокументированы toouse `exported="false"`, этот флаг можно также использовать в предыдущих версиях пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="305e1-122">Security: reach activities are now documented toouse `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="305e1-123">4.2.0 (11.03.2016)</span><span class="sxs-lookup"><span data-stu-id="305e1-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="305e1-124">пакет SDK для Hello теперь лицензировано MIT.</span><span class="sxs-lookup"><span data-stu-id="305e1-124">hello SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="305e1-125">Разрешено указание пользовательского идентификатора устройства во время инициализации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="305e1-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="305e1-126">4.1.5 (01.02.2016)</span><span class="sxs-lookup"><span data-stu-id="305e1-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="305e1-127">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="305e1-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="305e1-128">4.1.4 (26.01.2016)</span><span class="sxs-lookup"><span data-stu-id="305e1-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="305e1-129">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="305e1-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="305e1-130">4.1.3 (09.12.2015)</span><span class="sxs-lookup"><span data-stu-id="305e1-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="305e1-131">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="305e1-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="305e1-132">4.1.2 (25.11.2015)</span><span class="sxs-lookup"><span data-stu-id="305e1-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="305e1-133">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="305e1-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="305e1-134">4.1.1 (04.11.2015)</span><span class="sxs-lookup"><span data-stu-id="305e1-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="305e1-135">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="305e1-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="305e1-136">4.1.0 (25.08.2015)</span><span class="sxs-lookup"><span data-stu-id="305e1-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="305e1-137">Обработка новой модели разрешений для Android M.</span><span class="sxs-lookup"><span data-stu-id="305e1-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="305e1-138">Возможность настройки функций расположения в среде выполнения, а не с помощью `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="305e1-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="305e1-139">Исправление ошибки разрешений: если используется `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="305e1-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="305e1-140">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="305e1-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="305e1-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="305e1-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="305e1-142">Внутренний протокол изменяет toomake аналитики и принудительной более надежным.</span><span class="sxs-lookup"><span data-stu-id="305e1-142">Internal protocol changes toomake analytics and push more reliable.</span></span>
* <span data-ttu-id="305e1-143">Собственные Push-уведомления (GCM/ADM) теперь также используется для уведомлений приложения, необходимо настроить учетные данные собственной отправки hello для любого типа кампании push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="305e1-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="305e1-144">Исправлены ошибки общих уведомлений: ранее они отображались только 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="305e1-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="305e1-145">Исправить ошибку в виде веб-страницы: щелчок ссылки также выполняла URL-адрес действия по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="305e1-145">Fix a bug in web view: clicking on a link was also executing hello default action URL.</span></span>
* <span data-ttu-id="305e1-146">Устраните сбой редких связанных toolocal управления хранилищем.</span><span class="sxs-lookup"><span data-stu-id="305e1-146">Fix a rare crash related toolocal storage management.</span></span>
* <span data-ttu-id="305e1-147">Исправлена ошибка, связанная с динамическим управлением строкой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="305e1-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="305e1-148">Обновлено лицензионное соглашение с пользователем.</span><span class="sxs-lookup"><span data-stu-id="305e1-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="305e1-149">3.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="305e1-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="305e1-150">Первый выпуск Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="305e1-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="305e1-151">Конфигурация appId заменена на конфигурацию строки подключения.</span><span class="sxs-lookup"><span data-stu-id="305e1-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="305e1-152">Удалить API toosend и получать произвольный XMPP сообщения из произвольных XMPP сущностей.</span><span class="sxs-lookup"><span data-stu-id="305e1-152">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="305e1-153">Удалить API toosend и получения сообщений между устройствами.</span><span class="sxs-lookup"><span data-stu-id="305e1-153">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="305e1-154">Улучшения безопасности.</span><span class="sxs-lookup"><span data-stu-id="305e1-154">Security improvements.</span></span>
* <span data-ttu-id="305e1-155">Удалено отслеживание Google Play и SmartAd.</span><span class="sxs-lookup"><span data-stu-id="305e1-155">Google Play and SmartAd tracking removed.</span></span>

