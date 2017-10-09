---
title: "aaaAzure iOS Mobile Engagement заметки о выпуске пакета SDK | Документы Microsoft"
description: "Последние обновления и указания для пакета SDK для iOS для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="d5132-103">Заметки о выпуске пакета SDK для Служб мобильного взаимодействия Azure (iOS)</span><span class="sxs-lookup"><span data-stu-id="d5132-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="d5132-104">4.1.0 (17.07.2017)</span><span class="sxs-lookup"><span data-stu-id="d5132-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="d5132-105">Исправлена проблема с исчезающими на заднем фоне эмблемами.</span><span class="sxs-lookup"><span data-stu-id="d5132-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="d5132-106">Исправлена проблема с предупреждениями в XCode 9 о невызванных в основной очереди API-интерфейсах.</span><span class="sxs-lookup"><span data-stu-id="d5132-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="d5132-107">Исправлена утечка памяти при опросах охвата.</span><span class="sxs-lookup"><span data-stu-id="d5132-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="d5132-108">Прекращена поддержка iOS 6.X.</span><span class="sxs-lookup"><span data-stu-id="d5132-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="d5132-109">Начиная с этой версии цель развертывания hello приложения должен быть по крайней мере iOS 7.</span><span class="sxs-lookup"><span data-stu-id="d5132-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="d5132-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="d5132-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="d5132-111">Улучшенная доставка журнала в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="d5132-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="d5132-112">4.0.0 (12.09.2016)</span><span class="sxs-lookup"><span data-stu-id="d5132-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="d5132-113">Исправлена ошибка, из-за которой не приводились в действие уведомления на устройствах iOS 10.</span><span class="sxs-lookup"><span data-stu-id="d5132-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="d5132-114">Устаревшая версия XCode 7 заменена новой версией.</span><span class="sxs-lookup"><span data-stu-id="d5132-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="d5132-115">3.2.4 (06/30/2016)</span><span class="sxs-lookup"><span data-stu-id="d5132-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="d5132-116">Исправлено агрегирование данных из технических и других журналов.</span><span class="sxs-lookup"><span data-stu-id="d5132-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="d5132-117">3.2.3 (07.06.2016)</span><span class="sxs-lookup"><span data-stu-id="d5132-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="d5132-118">Ошибка основных hello отзыв доставки которых не появляется, когда приложение находится в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="d5132-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="d5132-119">Оптимизированный hello отправки технических журналов.</span><span class="sxs-lookup"><span data-stu-id="d5132-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="d5132-120">3.2.2 (07.04.2016)</span><span class="sxs-lookup"><span data-stu-id="d5132-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="d5132-121">Исправлена ошибка при отмене запроса HTTP, что иногда приводит toocrash.</span><span class="sxs-lookup"><span data-stu-id="d5132-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="d5132-122">3.2.1 (11.12.2015)</span><span class="sxs-lookup"><span data-stu-id="d5132-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="d5132-123">Фиксированный hello задержки при запуске нового экземпляра приложения, уведомление о прямых ссылок</span><span class="sxs-lookup"><span data-stu-id="d5132-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="d5132-124">3.2.0 (08.10.2015)</span><span class="sxs-lookup"><span data-stu-id="d5132-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="d5132-125">Включить Bitcode в toomake SDK hello, она работает с **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="d5132-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="d5132-126">Исправленные ошибки, связанные с уведомления tooin приложения.</span><span class="sxs-lookup"><span data-stu-id="d5132-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="d5132-127">Уведомления в приложение hello становится более надежным, низкого заряда батарей и других подобных ситуациях.</span><span class="sxs-lookup"><span data-stu-id="d5132-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="d5132-128">Удалены лишние журналы консоли, созданные библиотекой сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="d5132-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="d5132-129">3.1.0 (26.08.2015)</span><span class="sxs-lookup"><span data-stu-id="d5132-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="d5132-130">Исправьте ошибку совместимости iOS 9 с библиотекой стороннего производителя.</span><span class="sxs-lookup"><span data-stu-id="d5132-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="d5132-131">Она вызывала сбои при отправке результатов опросов, сведений о приложении или дополнительных данных.</span><span class="sxs-lookup"><span data-stu-id="d5132-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="d5132-132">3.0.0 (06/19/2015)</span><span class="sxs-lookup"><span data-stu-id="d5132-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="d5132-133">Службы мобильного взаимодействия используют автоматические push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="d5132-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="d5132-134">Прекращена поддержка iOS 4.X.</span><span class="sxs-lookup"><span data-stu-id="d5132-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="d5132-135">Начиная с этой версии цель развертывания hello приложения должен быть по крайней мере iOS 6.</span><span class="sxs-lookup"><span data-stu-id="d5132-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="d5132-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="d5132-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="d5132-137">ИД устройства Mobile Engagement Hello для устройств < iOS 6 теперь выполняется на основе GUID, созданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="d5132-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="d5132-138">2.1.0 (24.04.2015)</span><span class="sxs-lookup"><span data-stu-id="d5132-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="d5132-139">Добавлена поддержка Swift.</span><span class="sxs-lookup"><span data-stu-id="d5132-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="d5132-140">При нажатии на уведомление hello действие, которое URL-адрес теперь выполняется справа после открытия приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d5132-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="d5132-141">В пакет SDK добавлен отсутствующий файл заголовка.</span><span class="sxs-lookup"><span data-stu-id="d5132-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="d5132-142">Устранена проблема, при отключенной мобильного охвата hello аварийного завершения-формирования отчетов.</span><span class="sxs-lookup"><span data-stu-id="d5132-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="d5132-143">Версия 2.0.0 (17.02.2015)</span><span class="sxs-lookup"><span data-stu-id="d5132-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="d5132-144">Первый выпуск Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="d5132-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="d5132-145">Конфигурация appId/sdkKey заменена конфигурацией строки подключения.</span><span class="sxs-lookup"><span data-stu-id="d5132-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="d5132-146">Удалить API toosend и получать произвольный XMPP сообщения из произвольных XMPP сущностей.</span><span class="sxs-lookup"><span data-stu-id="d5132-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="d5132-147">Удалить API toosend и получения сообщений между устройствами.</span><span class="sxs-lookup"><span data-stu-id="d5132-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="d5132-148">Улучшения безопасности.</span><span class="sxs-lookup"><span data-stu-id="d5132-148">Security improvements.</span></span>
* <span data-ttu-id="d5132-149">Удалено средство отслеживания SmartAd.</span><span class="sxs-lookup"><span data-stu-id="d5132-149">SmartAd tracking removed.</span></span>
