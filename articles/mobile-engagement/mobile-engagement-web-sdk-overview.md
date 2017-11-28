---
title: "Обзор пакета SDK для Mobile Engagement Web aaaAzure | Документы Microsoft"
description: "Здравствуйте, последние обновления и процедуры для hello Web SDK для Azure Mobile Engagement"
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
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="56659-103">Веб-пакет SDK для Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="56659-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="56659-104">Начало для всех hello подробные сведения о том, как toointegrate Azure Mobile Engagement в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="56659-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="56659-105">При желании toogive его try прежде чем начать с собственного веб-приложения. в разделе нашей [15-минутных учебника](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="56659-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="56659-106">Процедуры по интеграции</span><span class="sxs-lookup"><span data-stu-id="56659-106">Integration procedures</span></span>
1. <span data-ttu-id="56659-107">Дополнительные сведения [как toointegrate Mobile Engagement в веб-приложении](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="56659-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="56659-108">Реализация плана тег, узнайте [как toouse hello дополнительные теги API в веб-приложения Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="56659-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="56659-109">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="56659-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="56659-110">2.0.2 (10/18/2016)</span><span class="sxs-lookup"><span data-stu-id="56659-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="56659-111">Фиксированный сбой в режиме закрытого просмотра (Safari).</span><span class="sxs-lookup"><span data-stu-id="56659-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="56659-112">Фиксированный сбой в браузерах с отключенными файлами cookie.</span><span class="sxs-lookup"><span data-stu-id="56659-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="56659-113">Для всех версий см. в разделе hello [завершения заметки о выпуске](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="56659-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="56659-114">Процедуры обновления</span><span class="sxs-lookup"><span data-stu-id="56659-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="56659-115">Обновление с 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="56659-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="56659-116">Hello следующих разделах описаны как toomigrate пакет SDK Mobile Engagement Web интеграции из обновления Capptain hello, предлагаемых Capptain SAS, приложение Azure Mobile Engagement tooan.</span><span class="sxs-lookup"><span data-stu-id="56659-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="56659-117">При миграции из более ранней версии, чем 1.2.1, сначала обратитесь к веб-сайт toomigrate hello Capptain too1.2.1 и примените hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="56659-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="56659-118">Эта версия hello Mobile Engagement Web SDK не поддерживает смарт-ТВ Samsung, Opera ТВ, webOS или функции hello Reach.</span><span class="sxs-lookup"><span data-stu-id="56659-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56659-119">Capptain и Azure Mobile Engagement не являются hello одной службы и выделите hello следующих процедур, как только toomigrate hello клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="56659-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="56659-120">Миграция hello Mobile Engagement Web SDK в приложение hello не выполняют миграцию данных из Capptain tooa мобильного охвата серверных компонентов.</span><span class="sxs-lookup"><span data-stu-id="56659-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="56659-121">Файлы JavaScript</span><span class="sxs-lookup"><span data-stu-id="56659-121">JavaScript files</span></span>
<span data-ttu-id="56659-122">Замените файл hello capptain-sdk.js файл hello azure-engagement.js, а потом изменить сценарий импортирует соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="56659-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="56659-123">Удаление модуля Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="56659-123">Remove Capptain Reach</span></span>
<span data-ttu-id="56659-124">Эта версия hello Mobile Engagement Web SDK не поддерживает функции hello Reach.</span><span class="sxs-lookup"><span data-stu-id="56659-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="56659-125">Если Capptain Reach, интегрированы в приложение, необходимо tooremove его.</span><span class="sxs-lookup"><span data-stu-id="56659-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="56659-126">Удалите hello достичь CSS импорта со страницы и удалите hello связанные CSS-файл (capptain-reach.css, по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="56659-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="56659-127">Удалить следующие ресурсы Reach hello: hello закрыть изображение (capptain-close.png, по умолчанию) и hello фирменной символики значок (capptain уведомления-, по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="56659-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="56659-128">Удалите hello достичь пользовательского интерфейса для уведомления в приложении.</span><span class="sxs-lookup"><span data-stu-id="56659-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="56659-129">макет по умолчанию Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="56659-129">hello default layout looks like this:</span></span>

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

<span data-ttu-id="56659-130">Удалите hello достичь пользовательского интерфейса для текста и веб-объявлений и для опросов.</span><span class="sxs-lookup"><span data-stu-id="56659-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="56659-131">макет по умолчанию Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="56659-131">hello default layout looks like this:</span></span>

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

<span data-ttu-id="56659-132">Удалите hello `reach` объекта из вашей конфигурации, если он существует.</span><span class="sxs-lookup"><span data-stu-id="56659-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="56659-133">Это выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="56659-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="56659-134">Удалите все прочие настройки Reach, например категории.</span><span class="sxs-lookup"><span data-stu-id="56659-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="56659-135">Удаление нерекомендуемых интерфейсов API</span><span class="sxs-lookup"><span data-stu-id="56659-135">Remove deprecated APIs</span></span>
<span data-ttu-id="56659-136">Некоторые интерфейсы API из Capptain являются устаревшими в hello Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="56659-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="56659-137">Удалите все вызовы toohello следующие API-интерфейсы: `agent.connect`, `agent.disconnect`, `agent.pause`, и `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="56659-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="56659-138">Удалите следующую обратные вызовы из конфигурации Capptain hello: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, и `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="56659-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="56659-139">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="56659-139">Configuration</span></span>
<span data-ttu-id="56659-140">Mobile Engagement используются идентификаторы SDK tooconfigure строку подключения, например, идентификатор приложения hello.</span><span class="sxs-lookup"><span data-stu-id="56659-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="56659-141">Замените идентификатор приложения hello строки подключения.</span><span class="sxs-lookup"><span data-stu-id="56659-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="56659-142">Обратите внимание на то что hello глобальный объект hello настройки SDK изменится с `capptain` слишком`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="56659-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="56659-143">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="56659-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="56659-144">После миграции:</span><span class="sxs-lookup"><span data-stu-id="56659-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="56659-145">Hello строку подключения для приложения отображается в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="56659-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="56659-146">Интерфейсы API JavaScript</span><span class="sxs-lookup"><span data-stu-id="56659-146">JavaScript APIs</span></span>
<span data-ttu-id="56659-147">глобальный объект JavaScript Hello `window.capptain` был переименован `window.azureEngagement`, но вы можете использовать hello `window.engagement` псевдоним для вызовов API.</span><span class="sxs-lookup"><span data-stu-id="56659-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="56659-148">Нельзя использовать эту конфигурацию пакета SDK для hello toodefine псевдоним.</span><span class="sxs-lookup"><span data-stu-id="56659-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="56659-149">Например: `capptain.deviceId` становится `engagement.deviceId`, `capptain.agent.startActivity` становится `engagement.agent.startActivity` и т. д.</span><span class="sxs-lookup"><span data-stu-id="56659-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="56659-150">Если уже имеется встроенный более ранней версии Azure Mobile Engagement Web SDK hello в приложение, прочитайте о [обновить процедуры](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="56659-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

