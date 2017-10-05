---
title: "Интеграция пакета SDK для Служб мобильного взаимодействия Azure с Android"
description: "Описывает, как интегрировать пакет SDK для Служб мобильного взаимодействия Azure в приложения Android."
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
ms.openlocfilehash: 35935e911f1f17989beb71978396c6d1b7d601d6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="7437b-103">Интеграция пакета SDK для Служб мобильного взаимодействия Azure с Android</span><span class="sxs-lookup"><span data-stu-id="7437b-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7437b-104">Универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="7437b-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="7437b-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7437b-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="7437b-106">iOS</span><span class="sxs-lookup"><span data-stu-id="7437b-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="7437b-107">Android</span><span class="sxs-lookup"><span data-stu-id="7437b-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="7437b-108">В этом документе описываются все параметры интеграции и конфигурации в пакете SDK для Android для Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="7437b-108">This document describes all the integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7437b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7437b-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="7437b-110">Дополнительные функции</span><span class="sxs-lookup"><span data-stu-id="7437b-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="7437b-111">Функции отчетов</span><span class="sxs-lookup"><span data-stu-id="7437b-111">Reporting Features</span></span>
<span data-ttu-id="7437b-112">Можно добавить такие функции:</span><span class="sxs-lookup"><span data-stu-id="7437b-112">You can add these features:</span></span>

1. [<span data-ttu-id="7437b-113">дополнительные параметры отчетов;</span><span class="sxs-lookup"><span data-stu-id="7437b-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="7437b-114">параметры отчетов о местонахождении;</span><span class="sxs-lookup"><span data-stu-id="7437b-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="7437b-115">дополнительные параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7437b-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="7437b-116">Уведомления:</span><span class="sxs-lookup"><span data-stu-id="7437b-116">Notifications:</span></span>
[<span data-ttu-id="7437b-117">Интеграция модуля Reach (уведомления) в приложение Android</span><span class="sxs-lookup"><span data-stu-id="7437b-117">How to integrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="7437b-118">Google Cloud Messaging (GCM): [Интеграция GCM с помощью Служб мобильного взаимодействия](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="7437b-118">Google Cloud Messaging (GCM): [How to Integrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="7437b-119">Amazon Device Messaging (ADM): [Интеграция ADM с помощью Служб мобильного взаимодействия](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="7437b-119">Amazon Device Messaging (ADM): [How to Integrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="7437b-120">Реализация плана добавления тегов:</span><span class="sxs-lookup"><span data-stu-id="7437b-120">Tag plan implementation:</span></span>
[<span data-ttu-id="7437b-121">Использование расширенного API добавления тегов Служб мобильного взаимодействия в приложении Android</span><span class="sxs-lookup"><span data-stu-id="7437b-121">How to use the advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="7437b-122">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="7437b-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="7437b-123">4.3.1 (17.07.2017)</span><span class="sxs-lookup"><span data-stu-id="7437b-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="7437b-124">Исправлена проблема с аварийным завершением работы, которое изредка могло происходить при вызове `EngagementAgentUtils.isInDedicatedEngagementProcess` (также используется классом `EngagementApplication`).</span><span class="sxs-lookup"><span data-stu-id="7437b-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="7437b-125">4.3.0 (27.06.2017)</span><span class="sxs-lookup"><span data-stu-id="7437b-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="7437b-126">Поддержка Android 8 (предыдущие версии пакета SDK не будут работать с Android 8).</span><span class="sxs-lookup"><span data-stu-id="7437b-126">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="7437b-127">Удалена зависимость от библиотеки поддержки.</span><span class="sxs-lookup"><span data-stu-id="7437b-127">No more dependency on support library.</span></span>
* <span data-ttu-id="7437b-128">Удален класс `EngagementFragmentActivity`.</span><span class="sxs-lookup"><span data-stu-id="7437b-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="7437b-129">Из-за [ограничений на фоновое выполнение приложений](https://developer.android.com/preview/features/background.html) в Android 8 журналы в фоновом режиме могут отображаться с задержкой (когда пользователь воспользуется устройством), что, в свою очередь, может повлиять на отображение статистики по **доставленным** push-уведомлениям и **отображенным системным уведомлениям**. Причина — соответствующие данные не поступают, пока устройство находится в спящем режиме. (Это не повлияет на отображение уведомления, подачу устройством звукового сигнала и вибросигнала в реальном времени.)</span><span class="sxs-lookup"><span data-stu-id="7437b-129">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="7437b-130">Из-за [ограничений на доступ к геолокационным данным в фоновом режиме](https://developer.android.com/preview/features/background-location-limits.html) данные о текущем местонахождении не будут часто обновляться в Android 8.</span><span class="sxs-lookup"><span data-stu-id="7437b-130">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="7437b-131">Информацию о всех версиях см. в [полной версии заметок о выпуске](mobile-engagement-android-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="7437b-131">For all versions, see the [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="7437b-132">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="7437b-132">Upgrade procedures</span></span>
<span data-ttu-id="7437b-133">Если вы уже интегрировали более старую версию нашего пакета SDK в приложение, ознакомьтесь с разделом [Процедуры обновления](mobile-engagement-android-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="7437b-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

