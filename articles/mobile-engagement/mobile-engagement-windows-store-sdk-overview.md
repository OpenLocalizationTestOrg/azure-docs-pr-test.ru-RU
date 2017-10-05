---
title: "Интеграция пакета SDK универсальных приложений Windows для Служб мобильного взаимодействия Azure | Документация Майкрософт"
description: "Интеграция универсальных приложений для Windows с пакетом SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 9ded187d-5c07-4377-a41c-ce205dd38b50
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: d616ad58156a19e89b3e106639a38df67cbd0abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="0846d-103">Интеграция пакета SDK универсальных приложений для Windows для Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="0846d-103">Windows Universal SDK Integration for Azure Mobile Engagement</span></span>
<span data-ttu-id="0846d-104">В этом документе описываются все параметры интеграции и конфигурации, доступные для пакета SDK универсальных приложений для Windows для Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="0846d-104">This document describes all the integration and configuration options available for the Azure Mobile Engagement Windows Universal SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0846d-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0846d-105">Prerequisites</span></span>
<span data-ttu-id="0846d-106">Прежде чем приступить к этому учебнику, необходимо изучить [наш 15-минутный учебник](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0846d-106">Before starting this tutorial, you must first complete our [15-minute tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="advanced-features"></a><span data-ttu-id="0846d-107">Дополнительные функции</span><span class="sxs-lookup"><span data-stu-id="0846d-107">Advanced features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="0846d-108">Функции отчетов</span><span class="sxs-lookup"><span data-stu-id="0846d-108">Reporting features</span></span>
<span data-ttu-id="0846d-109">Можно добавить такие функции:</span><span class="sxs-lookup"><span data-stu-id="0846d-109">You can add these features:</span></span>

1. [<span data-ttu-id="0846d-110">дополнительные параметры отчетов;</span><span class="sxs-lookup"><span data-stu-id="0846d-110">Advanced reporting options</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
2. [<span data-ttu-id="0846d-111">Расширенные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="0846d-111">Advanced configuration options</span></span>](mobile-engagement-windows-store-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="0846d-112">Уведомления</span><span class="sxs-lookup"><span data-stu-id="0846d-112">Notifications</span></span>
[<span data-ttu-id="0846d-113">Как интегрировать Reach (Notifications) в универсальное приложение для Windows</span><span class="sxs-lookup"><span data-stu-id="0846d-113">How to integrate Reach (Notifications) in your Windows Universal app</span></span>](mobile-engagement-windows-store-integrate-engagement-reach.md)

### <a name="tag-plan-implementation"></a><span data-ttu-id="0846d-114">Реализация плана добавления тегов:</span><span class="sxs-lookup"><span data-stu-id="0846d-114">Tag plan implementation:</span></span>
[<span data-ttu-id="0846d-115">Как использовать API для расширенного добавления тегов Служб мобильного взаимодействия в универсальном приложении для Windows</span><span class="sxs-lookup"><span data-stu-id="0846d-115">How to use the advanced Mobile Engagement tagging API in your Windows Universal app</span></span>](mobile-engagement-windows-store-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="0846d-116">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="0846d-116">Release notes</span></span>
### <a name="341-11032016"></a><span data-ttu-id="0846d-117">3.4.1 (03.11.2016)</span><span class="sxs-lookup"><span data-stu-id="0846d-117">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="0846d-118">Улучшение стабильности.</span><span class="sxs-lookup"><span data-stu-id="0846d-118">Stability improvements.</span></span>

<span data-ttu-id="0846d-119">Сведения о предыдущих версиях см. в [полных заметках о выпуске](mobile-engagement-windows-store-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="0846d-119">For earlier versions, see the [complete release notes](mobile-engagement-windows-store-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="0846d-120">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="0846d-120">Upgrade procedures</span></span>
<span data-ttu-id="0846d-121">Если вы уже интегрировали в приложение старую версию службы Engagement, при обновлении пакета SDK необходимо учитывать следующее.</span><span class="sxs-lookup"><span data-stu-id="0846d-121">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="0846d-122">Если вы пропустили несколько версий пакета SDK, то вам понадобится выполнить несколько процедур.</span><span class="sxs-lookup"><span data-stu-id="0846d-122">If you missed several versions of the SDK, you may have to follow several procedures.</span></span> <span data-ttu-id="0846d-123">Посмотрите полные [процедуры обновления](mobile-engagement-windows-store-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="0846d-123">See the complete [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md).</span></span> <span data-ttu-id="0846d-124">Например, при миграции с версии 0.10.1 в версию 0.11.0 необходимо сначала выполнить процедуру миграции «с 0.9.0 в 0.10.1», а затем процедуру миграции «с 0.10.1 в 0.11.0».</span><span class="sxs-lookup"><span data-stu-id="0846d-124">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

### <a name="from-330-to-340"></a><span data-ttu-id="0846d-125">С 3.3.0 в 3.4.0</span><span class="sxs-lookup"><span data-stu-id="0846d-125">From 3.3.0 to 3.4.0</span></span>
#### <a name="test-logs"></a><span data-ttu-id="0846d-126">Журналы тестирования</span><span class="sxs-lookup"><span data-stu-id="0846d-126">Test logs</span></span>
<span data-ttu-id="0846d-127">Теперь журналы консоли, созданные с помощью пакета SDK, можно включать, отключать или фильтровать.</span><span class="sxs-lookup"><span data-stu-id="0846d-127">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="0846d-128">Для настройки обновите свойство `EngagementAgent.Instance.TestLogEnabled`, присвоив ему одно из значений, доступных в перечислении `EngagementTestLogLevel`, например:</span><span class="sxs-lookup"><span data-stu-id="0846d-128">To customize, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the values available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

#### <a name="resources"></a><span data-ttu-id="0846d-129">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="0846d-129">Resources</span></span>
<span data-ttu-id="0846d-130">Было улучшено наложение Reach.</span><span class="sxs-lookup"><span data-stu-id="0846d-130">The Reach overlay has been improved.</span></span> <span data-ttu-id="0846d-131">Оно входит в состав ресурсов пакета SDK NuGet.</span><span class="sxs-lookup"><span data-stu-id="0846d-131">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="0846d-132">Во время обновления до новой версии пакета SDK можно выбрать возможность сохранения существующих файлов из папки наложения для ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0846d-132">While upgrading to the new version of the SDK, you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="0846d-133">Если вы используете предыдущее наложение или интегрируете элементы `WebView` вручную, можно оставить существующие файлы — наложение будет работать.</span><span class="sxs-lookup"><span data-stu-id="0846d-133">If the previous overlay is working for you, or you are integrating the `WebView` elements manually, then you can decide to keep your exiting files, it will still work.</span></span>
* <span data-ttu-id="0846d-134">Чтобы выполнить обновление до нового наложения, замените всю папку `overlay` из ресурсов на новую из пакета SDK (приложения UWP: после обновления можно получить новую папку наложения из %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="0846d-134">To update to the new overlay, replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="0846d-135">Новое наложение перезапишет изменения, внесенные в предыдущую версию.</span><span class="sxs-lookup"><span data-stu-id="0846d-135">Using the new overlay overwrites any customizations made on the previous version.</span></span>
> 
> 

### <a name="upgrade-from-older-versions"></a><span data-ttu-id="0846d-136">Обновление предыдущих версий</span><span class="sxs-lookup"><span data-stu-id="0846d-136">Upgrade from older versions</span></span>
<span data-ttu-id="0846d-137">См. статью [Процедуры обновления SDK универсальных приложений для Windows](mobile-engagement-windows-store-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="0846d-137">See [Upgrade Procedures](mobile-engagement-windows-store-upgrade-procedure.md)</span></span>

