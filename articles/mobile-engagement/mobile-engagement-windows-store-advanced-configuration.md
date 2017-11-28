---
title: "aaaAdvanced конфигурации для универсальных приложений Engagement пакета SDK для Windows"
description: "Параметры расширенной конфигурации Служб мобильного взаимодействия Azure при использовании с универсальными приложениями для Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="0589e-103">Расширенная конфигурация пакета SDK службы Engagement для универсальных приложений для Windows</span><span class="sxs-lookup"><span data-stu-id="0589e-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0589e-104">Универсальная платформа Windows</span><span class="sxs-lookup"><span data-stu-id="0589e-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="0589e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="0589e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="0589e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="0589e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="0589e-107">Android</span><span class="sxs-lookup"><span data-stu-id="0589e-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="0589e-108">Эта процедура описывает, как tooconfigure различные параметры конфигурации для приложения Azure Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="0589e-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0589e-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0589e-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="0589e-110">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="0589e-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="0589e-111">Отключение автоматического создания отчетов о сбоях</span><span class="sxs-lookup"><span data-stu-id="0589e-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="0589e-112">Можно отключить hello аварийного завершения автоматического компонент рвением отчетов.</span><span class="sxs-lookup"><span data-stu-id="0589e-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="0589e-113">Тогда при возникновении необработанного исключения служба Engagement не будет выполнять никаких действий.</span><span class="sxs-lookup"><span data-stu-id="0589e-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="0589e-114">Если отключить эту функцию, то при возникновении необработанного аварийного завершения приложения Engagement не отправляет аварийного завершения hello **AND** не приводит к закрытию сеанса hello и заданий.</span><span class="sxs-lookup"><span data-stu-id="0589e-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="0589e-115">автоматического создания отчетов, о сбоях toodisable настроить конфигурацию, в зависимости от того, она была объявлена как hello:</span><span class="sxs-lookup"><span data-stu-id="0589e-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="0589e-116">Из файла `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="0589e-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="0589e-117">Отчет набора аварийное завершение работы слишком`false` между `<reportCrash>` и `</reportCrash>` тегов.</span><span class="sxs-lookup"><span data-stu-id="0589e-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="0589e-118">Из объекта `EngagementConfiguration` во время выполнения</span><span class="sxs-lookup"><span data-stu-id="0589e-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="0589e-119">Задать toofalse сбоя отчетов с помощью объекта EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="0589e-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="0589e-120">Отключение отчетов в реальном времени</span><span class="sxs-lookup"><span data-stu-id="0589e-120">Disable real time reporting</span></span>
<span data-ttu-id="0589e-121">По умолчанию hello Engagement службы отчетов входит в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="0589e-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="0589e-122">Если приложение сообщает журналы часто, это лучше toobuffer hello журналы и tooreport их все за один раз на основе рабочее время.</span><span class="sxs-lookup"><span data-stu-id="0589e-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="0589e-123">Это называется пакетным режимом.</span><span class="sxs-lookup"><span data-stu-id="0589e-123">This is called “burst mode”.</span></span>

<span data-ttu-id="0589e-124">toodo таким образом, необходимо вызвать метод hello:</span><span class="sxs-lookup"><span data-stu-id="0589e-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="0589e-125">Hello аргумент представляет собой значение в **миллисекунд**.</span><span class="sxs-lookup"><span data-stu-id="0589e-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="0589e-126">Каждый раз, когда требуется, чтобы в режиме реального времени ведения журнала hello tooreactivate, вызовите метод hello без какого-либо параметра или со значением hello 0.</span><span class="sxs-lookup"><span data-stu-id="0589e-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="0589e-127">Пакетный режим немного увеличивает hello аккумулятора, но оказывает влияние на hello монитор Engagement: продолжительность все сеансы и задания являются скругленными toohello пороговое значение пакетного режима (таким образом, сеансы и задания короче, чем порог повышения hello не могут быть видны).</span><span class="sxs-lookup"><span data-stu-id="0589e-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="0589e-128">Мы рекомендуем использовать пороговое значение пакета не более 30 000 (30 с).</span><span class="sxs-lookup"><span data-stu-id="0589e-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="0589e-129">Сохраненные журналы — это ограниченная too300 элементы.</span><span class="sxs-lookup"><span data-stu-id="0589e-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="0589e-130">Если отправка занимает слишком много времени, некоторые журналы могут быть потеряны.</span><span class="sxs-lookup"><span data-stu-id="0589e-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="0589e-131">Порог повышения Hello не может быть tooa настроенный период меньше секунды.</span><span class="sxs-lookup"><span data-stu-id="0589e-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="0589e-132">Если сделать это, hello SDK показывает трассировки с ошибкой hello и автоматически сбрасывает toohello значение по умолчанию, ноль секунд.</span><span class="sxs-lookup"><span data-stu-id="0589e-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="0589e-133">Это hello tooreport триггеры SDK hello регистрирует в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="0589e-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
