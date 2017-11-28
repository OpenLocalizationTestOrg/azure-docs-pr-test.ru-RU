---
title: "Процедуры обновления веб-пакета SDK для Служб мобильного взаимодействия Azure | Документация Майкрософт"
description: "Последние обновления и процедуры для веб-пакета SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: afa8037dcb7a53042fa606e2c4014b442d4be326
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="06c06-103">Процедуры обновления веб-пакета SDK для Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="06c06-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="06c06-104">Если вы уже интегрировали в веб-приложение предыдущую версию веб-пакета SDK для Служб мобильного взаимодействия Azure, то при обновлении пакета SDK необходимо учитывать следующее.</span><span class="sxs-lookup"><span data-stu-id="06c06-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span></span>

<span data-ttu-id="06c06-105">Если вы пропустили несколько версий веб-пакета SDK для Служб мобильного взаимодействия Azure, то в процессе обновления может потребоваться выполнить несколько процедур.</span><span class="sxs-lookup"><span data-stu-id="06c06-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span></span> <span data-ttu-id="06c06-106">Например, при миграции с версии 1.4.0 на 1.6.0 сначала выполните обновление с версии 1.4.0 до 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="06c06-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span></span> <span data-ttu-id="06c06-107">Затем выполните процедуры обновления с версии 1.5.0 до 1.6.0.</span><span class="sxs-lookup"><span data-stu-id="06c06-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span></span>

<span data-ttu-id="06c06-108">Независимо от того, с какой версии выполняется обновление, необходимо заменить предыдущую версию файла azure-engagement.js его последней версией.</span><span class="sxs-lookup"><span data-stu-id="06c06-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span></span>

## <a name="upgrade-from-121-to-200"></a><span data-ttu-id="06c06-109">Обновление с версии 1.2.1 до 2.0.0</span><span class="sxs-lookup"><span data-stu-id="06c06-109">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="06c06-110">В этом разделе описан процесс переноса веб-пакета SDK для Служб мобильного взаимодействия из службы Capptain от Capptain SAS в приложение Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="06c06-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="06c06-111">При миграции с более ранней версии сначала ознакомьтесь с информацией о переносе на версию 1.2.1 на веб-сайте Capptain, а затем выполните описанные ниже процедуры.</span><span class="sxs-lookup"><span data-stu-id="06c06-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span></span>

<span data-ttu-id="06c06-112">Эта версия веб-пакета SDK для Служб мобильного взаимодействия не поддерживает функции Samsung Smart TV, Opera TV, webOS и Reach.</span><span class="sxs-lookup"><span data-stu-id="06c06-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06c06-113">Службы Capptain и Службы мобильного взаимодействия Azure отличаются между собой.</span><span class="sxs-lookup"><span data-stu-id="06c06-113">Capptain and Azure Mobile Engagement are not the same service.</span></span> <span data-ttu-id="06c06-114">В представленных ниже процедурах описывается способ переноса только для клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="06c06-114">The following procedure highlights only how to migrate the client app.</span></span> <span data-ttu-id="06c06-115">При переносе веб-пакета SDK для Служб мобильного взаимодействия в приложение данные не будут перенесены с сервера Capptain на сервер Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="06c06-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="06c06-116">Файлы JavaScript</span><span class="sxs-lookup"><span data-stu-id="06c06-116">JavaScript files</span></span>
<span data-ttu-id="06c06-117">Замените файл capptain-sdk.js файлом azure-engagement.js, а затем обновите соответствующим образом импортируемые элементы в сценарии.</span><span class="sxs-lookup"><span data-stu-id="06c06-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="06c06-118">Удаление модуля Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="06c06-118">Remove Capptain Reach</span></span>
<span data-ttu-id="06c06-119">Эта версия веб-пакета SDK для Служб мобильного взаимодействия не поддерживает функцию Reach.</span><span class="sxs-lookup"><span data-stu-id="06c06-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="06c06-120">Если вы интегрировали модуль Capptain Reach в приложение, то его необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="06c06-120">If you integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="06c06-121">Удалите импортированный код CSS Reach со страницы, также удалите связанный CSS-файл (по умолчанию: capptain-reach.css).</span><span class="sxs-lookup"><span data-stu-id="06c06-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="06c06-122">Удалите следующие ресурсы Reach: изображение для закрытия (по умолчанию: capptain-close.png) и фирменный значок (по умолчанию: capptain-notification-icon).</span><span class="sxs-lookup"><span data-stu-id="06c06-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="06c06-123">Удалите пользовательский интерфейс Reach для получения уведомлений в приложении.</span><span class="sxs-lookup"><span data-stu-id="06c06-123">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="06c06-124">Макет по умолчанию выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="06c06-124">The default layout looks like this:</span></span>

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

<span data-ttu-id="06c06-125">Удалите пользовательский интерфейс Reach для текстовых и веб-объявлений и опросов.</span><span class="sxs-lookup"><span data-stu-id="06c06-125">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="06c06-126">Макет по умолчанию выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="06c06-126">The default layout looks like this:</span></span>

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

<span data-ttu-id="06c06-127">Удалите объект `reach` из конфигурации, если таковой имеется.</span><span class="sxs-lookup"><span data-stu-id="06c06-127">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="06c06-128">Это выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="06c06-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="06c06-129">Удалите все прочие настройки Reach, например категории.</span><span class="sxs-lookup"><span data-stu-id="06c06-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="06c06-130">Удаление нерекомендуемых интерфейсов API</span><span class="sxs-lookup"><span data-stu-id="06c06-130">Remove deprecated APIs</span></span>
<span data-ttu-id="06c06-131">Некоторые интерфейсы API из Capptain являются нерекомендуемыми в веб-пакете SDK для Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="06c06-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="06c06-132">Удалите все вызовы к следующим API: `agent.connect`, `agent.disconnect`, `agent.pause` и `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="06c06-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="06c06-133">Удалите все экземпляры следующих обратных вызовов из конфигурации Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived` и `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="06c06-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="06c06-134">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="06c06-134">Configuration</span></span>
<span data-ttu-id="06c06-135">Службы мобильного взаимодействия используют строку подключения для настройки идентификаторов пакета SDK, таких как идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="06c06-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="06c06-136">Замените идентификатор приложения строкой подключения.</span><span class="sxs-lookup"><span data-stu-id="06c06-136">Replace the application ID with your connection string.</span></span> <span data-ttu-id="06c06-137">Обратите внимание, что глобальный объект для настройки пакета SDK меняется с `capptain` на `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="06c06-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="06c06-138">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="06c06-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="06c06-139">После миграции:</span><span class="sxs-lookup"><span data-stu-id="06c06-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="06c06-140">Теперь строка подключения для приложения отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="06c06-140">The connection string for your application is displayed in the Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="06c06-141">Интерфейсы API JavaScript</span><span class="sxs-lookup"><span data-stu-id="06c06-141">JavaScript APIs</span></span>
<span data-ttu-id="06c06-142">Глобальный объект JavaScript `window.capptain` был переименован в `window.azureEngagement`, но можно использовать псевдоним `window.engagement` для вызовов API.</span><span class="sxs-lookup"><span data-stu-id="06c06-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="06c06-143">Этот псевдоним нельзя использовать для определения конфигурации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="06c06-143">You can't use the alias to define the SDK configuration.</span></span>

<span data-ttu-id="06c06-144">Например: `capptain.deviceId` становится `engagement.deviceId`, `capptain.agent.startActivity` становится `engagement.agent.startActivity` и т. д.</span><span class="sxs-lookup"><span data-stu-id="06c06-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

