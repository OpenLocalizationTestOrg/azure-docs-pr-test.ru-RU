---
title: "Обзор веб-пакета SDK для Служб мобильного взаимодействия Azure | Документация Майкрософт"
description: "Последние обновления и процедуры для веб-пакета SDK для Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="f42bb-103">Веб-пакет SDK для Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="f42bb-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="f42bb-104">Начните с этой статьи, чтобы получить подробную информацию об интеграции Служб мобильного взаимодействия Azure в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="f42bb-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="f42bb-105">Если вы хотите поэкспериментировать, прежде чем интегрировать свое веб-приложение, ознакомьтесь с нашим [15-минутным руководством](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f42bb-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="f42bb-106">Процедуры по интеграции</span><span class="sxs-lookup"><span data-stu-id="f42bb-106">Integration procedures</span></span>
1. <span data-ttu-id="f42bb-107">Узнайте, [как интегрировать Службы мобильного взаимодействия в свое веб-приложение](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="f42bb-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="f42bb-108">Реализация плана добавления тегов описана в статье [Как использовать API Служб мобильного взаимодействия в веб-приложении](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="f42bb-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="f42bb-109">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="f42bb-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="f42bb-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="f42bb-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="f42bb-111">Фиксированный сбой в режиме закрытого просмотра (Safari).</span><span class="sxs-lookup"><span data-stu-id="f42bb-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="f42bb-112">Фиксированный сбой в браузерах с отключенными файлами cookie.</span><span class="sxs-lookup"><span data-stu-id="f42bb-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="f42bb-113">Информацию о всех версиях см. в [полной версии заметок о выпуске](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="f42bb-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="f42bb-114">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="f42bb-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="f42bb-115">Обновление с версии 1.2.1 до 2.0.0</span><span class="sxs-lookup"><span data-stu-id="f42bb-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="f42bb-116">В этих разделах описан процесс переноса веб-пакета SDK для Служб мобильного взаимодействия из службы Capptain от Capptain SAS в приложение Служб мобильного взаимодействия Azure.</span><span class="sxs-lookup"><span data-stu-id="f42bb-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="f42bb-117">При переходе с версии, предшествующей 1.2.1, сначала ознакомьтесь с информацией о переходе на версию 1.2.1 на веб-сайте Capptain, а затем выполните следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="f42bb-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="f42bb-118">Эта версия веб-пакета SDK для Служб мобильного взаимодействия не поддерживает функции Samsung Smart TV, Opera TV, webOS и Reach.</span><span class="sxs-lookup"><span data-stu-id="f42bb-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f42bb-119">Службы Capptain и Службы мобильного взаимодействия Azure отличаются друг от друга. В представленных ниже процедурах описывается способ переноса только для клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="f42bb-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="f42bb-120">При переносе веб-пакета SDK для Служб мобильного взаимодействия в приложение данные не будут перенесены с сервера Capptain на сервер Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="f42bb-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="f42bb-121">Файлы JavaScript</span><span class="sxs-lookup"><span data-stu-id="f42bb-121">JavaScript files</span></span>
<span data-ttu-id="f42bb-122">Замените файл capptain-sdk.js файлом azure-engagement.js, а затем обновите соответствующим образом импортируемые элементы в сценарии.</span><span class="sxs-lookup"><span data-stu-id="f42bb-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="f42bb-123">Удаление модуля Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="f42bb-123">Remove Capptain Reach</span></span>
<span data-ttu-id="f42bb-124">Эта версия веб-пакета SDK для Служб мобильного взаимодействия не поддерживает функцию Reach.</span><span class="sxs-lookup"><span data-stu-id="f42bb-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="f42bb-125">Если вы интегрировали модуль Capptain Reach в приложение, его необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="f42bb-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="f42bb-126">Удалите импортированный код CSS Reach со страницы, также удалите связанный CSS-файл (по умолчанию: capptain-reach.css).</span><span class="sxs-lookup"><span data-stu-id="f42bb-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="f42bb-127">Удалите следующие ресурсы Reach: изображение для закрытия (по умолчанию: capptain-close.png) и фирменный значок (по умолчанию: capptain-notification-icon).</span><span class="sxs-lookup"><span data-stu-id="f42bb-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="f42bb-128">Удалите пользовательский интерфейс Reach для получения уведомлений в приложении.</span><span class="sxs-lookup"><span data-stu-id="f42bb-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="f42bb-129">Макет по умолчанию выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f42bb-129">The default layout looks like this:</span></span>

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

<span data-ttu-id="f42bb-130">Удалите пользовательский интерфейс Reach для текстовых и веб-объявлений и опросов.</span><span class="sxs-lookup"><span data-stu-id="f42bb-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="f42bb-131">Макет по умолчанию выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f42bb-131">The default layout looks like this:</span></span>

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

<span data-ttu-id="f42bb-132">Удалите объект `reach` из конфигурации, если таковой имеется.</span><span class="sxs-lookup"><span data-stu-id="f42bb-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="f42bb-133">Это выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f42bb-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="f42bb-134">Удалите все прочие настройки Reach, например категории.</span><span class="sxs-lookup"><span data-stu-id="f42bb-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="f42bb-135">Удаление нерекомендуемых интерфейсов API</span><span class="sxs-lookup"><span data-stu-id="f42bb-135">Remove deprecated APIs</span></span>
<span data-ttu-id="f42bb-136">Некоторые интерфейсы API из Capptain являются нерекомендуемыми в веб-пакете SDK для Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="f42bb-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="f42bb-137">Удалите все вызовы к следующим API: `agent.connect`, `agent.disconnect`, `agent.pause` и `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="f42bb-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="f42bb-138">Удалите все следующие обратные вызовы из конфигурации Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived` и `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="f42bb-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="f42bb-139">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="f42bb-139">Configuration</span></span>
<span data-ttu-id="f42bb-140">Службы мобильного взаимодействия используют строку подключения для настройки идентификаторов пакета SDK, таких как идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="f42bb-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="f42bb-141">Замените идентификатор приложения строкой подключения.</span><span class="sxs-lookup"><span data-stu-id="f42bb-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="f42bb-142">Обратите внимание, что глобальный объект для настройки пакета SDK меняется с `capptain` на `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="f42bb-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="f42bb-143">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="f42bb-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="f42bb-144">После миграции:</span><span class="sxs-lookup"><span data-stu-id="f42bb-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="f42bb-145">Теперь строка подключения для приложения отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f42bb-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="f42bb-146">Интерфейсы API JavaScript</span><span class="sxs-lookup"><span data-stu-id="f42bb-146">JavaScript APIs</span></span>
<span data-ttu-id="f42bb-147">Глобальный объект JavaScript `window.capptain` был переименован в `window.azureEngagement`, но можно использовать псевдоним `window.engagement` для вызовов API.</span><span class="sxs-lookup"><span data-stu-id="f42bb-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="f42bb-148">Этот псевдоним нельзя использовать для определения конфигурации пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="f42bb-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="f42bb-149">Например: `capptain.deviceId` становится `engagement.deviceId`, `capptain.agent.startActivity` становится `engagement.agent.startActivity` и т. д.</span><span class="sxs-lookup"><span data-stu-id="f42bb-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="f42bb-150">Если вы уже интегрировали в свое приложение предыдущую версию веб-пакета SDK для Служб мобильного взаимодействия Azure, ознакомьтесь с [процедурами обновления](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="f42bb-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

