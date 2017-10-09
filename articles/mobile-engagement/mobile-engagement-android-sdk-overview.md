---
title: "aaaAndroid интеграции пакета SDK для Azure Mobile Engagement"
description: "Описывает способ toointegrate Azure Mobile Engagement SDK в приложения Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="1f3f3-103">Интеграция пакета SDK для Служб мобильного взаимодействия Azure с Android</span><span class="sxs-lookup"><span data-stu-id="1f3f3-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f3f3-104">Универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="1f3f3-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="1f3f3-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1f3f3-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="1f3f3-106">iOS</span><span class="sxs-lookup"><span data-stu-id="1f3f3-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="1f3f3-107">Android</span><span class="sxs-lookup"><span data-stu-id="1f3f3-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="1f3f3-108">В этом документе приводится описание всех hello интеграции и настройки параметров для Azure Mobile Engagement Android SDK.</span><span class="sxs-lookup"><span data-stu-id="1f3f3-108">This document describes all hello integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f3f3-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1f3f3-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="1f3f3-110">Дополнительные функции</span><span class="sxs-lookup"><span data-stu-id="1f3f3-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="1f3f3-111">Функции отчетов</span><span class="sxs-lookup"><span data-stu-id="1f3f3-111">Reporting Features</span></span>
<span data-ttu-id="1f3f3-112">Можно добавить такие функции:</span><span class="sxs-lookup"><span data-stu-id="1f3f3-112">You can add these features:</span></span>

1. [<span data-ttu-id="1f3f3-113">дополнительные параметры отчетов;</span><span class="sxs-lookup"><span data-stu-id="1f3f3-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="1f3f3-114">параметры отчетов о местонахождении;</span><span class="sxs-lookup"><span data-stu-id="1f3f3-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="1f3f3-115">дополнительные параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1f3f3-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="1f3f3-116">Уведомления:</span><span class="sxs-lookup"><span data-stu-id="1f3f3-116">Notifications:</span></span>
[<span data-ttu-id="1f3f3-117">Как toointegrate Reach (уведомлений) в приложении Android</span><span class="sxs-lookup"><span data-stu-id="1f3f3-117">How toointegrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="1f3f3-118">Google Cloud Messaging (GCM): [как tooIntegrate GCM с мобильного охвата](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="1f3f3-118">Google Cloud Messaging (GCM): [How tooIntegrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="1f3f3-119">Обмен сообщениями устройства Amazon (ADM): [как tooIntegrate ADM с мобильного охвата](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="1f3f3-119">Amazon Device Messaging (ADM): [How tooIntegrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="1f3f3-120">Реализация плана добавления тегов:</span><span class="sxs-lookup"><span data-stu-id="1f3f3-120">Tag plan implementation:</span></span>
[<span data-ttu-id="1f3f3-121">Как toouse hello advanced мобильного охвата, добавление тегов API в приложении Android</span><span class="sxs-lookup"><span data-stu-id="1f3f3-121">How toouse hello advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="1f3f3-122">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="1f3f3-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="1f3f3-123">4.3.1 (17.07.2017)</span><span class="sxs-lookup"><span data-stu-id="1f3f3-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="1f3f3-124">Исключена аварийного завершения работы, которая могла происходить редко, при вызове `EngagementAgentUtils.isInDedicatedEngagementProcess`, который также используется для hello `EngagementApplication` класса.</span><span class="sxs-lookup"><span data-stu-id="1f3f3-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="1f3f3-125">4.3.0 (27.06.2017)</span><span class="sxs-lookup"><span data-stu-id="1f3f3-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="1f3f3-126">8 Поддержка Android (предыдущие версии hello SDK не будет работать в Android 8).</span><span class="sxs-lookup"><span data-stu-id="1f3f3-126">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="1f3f3-127">Удалена зависимость от библиотеки поддержки.</span><span class="sxs-lookup"><span data-stu-id="1f3f3-127">No more dependency on support library.</span></span>
* <span data-ttu-id="1f3f3-128">Удален класс `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="1f3f3-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="1f3f3-129">Из-за слишком[ограничения выполнения фоновой](https://developer.android.com/preview/features/background.html) в Android 8 журналы в фоновом режиме может быть отложен до hello пользователь взаимодействует с устройством hello, это повлияет на кампании Push **доставлено** и **Системное уведомление выводится** статистики задерживается, если устройство hello находится в спящем режиме (hello уведомление будет отображаться, будет кольца и компакт-дисков в реальном времени без проблем).</span><span class="sxs-lookup"><span data-stu-id="1f3f3-129">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="1f3f3-130">Из-за слишком[ограничения расположения фона](https://developer.android.com/preview/features/background-location-limits.html), расположение hello реального времени в фоновом режиме не будет часто обновляться в Android 8.</span><span class="sxs-lookup"><span data-stu-id="1f3f3-130">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="1f3f3-131">Для всех версий см. в разделе hello [завершения заметки о выпуске](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="1f3f3-131">For all versions, see hello [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="1f3f3-132">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="1f3f3-132">Upgrade procedures</span></span>
<span data-ttu-id="1f3f3-133">Если вы уже интегрировали более старую версию нашего пакета SDK в приложение, ознакомьтесь с разделом [Процедуры обновления](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="1f3f3-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

