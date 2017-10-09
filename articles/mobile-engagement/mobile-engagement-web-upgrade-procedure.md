---
title: "процедуры обновления Mobile Engagement Web SDK aaaAzure | Документы Microsoft"
description: "Здравствуйте, последние обновления и процедуры для hello Web SDK для Azure Mobile Engagement"
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
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="b38b7-103">Процедуры обновления веб-пакета SDK для Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="b38b7-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="b38b7-104">Если уже имеется встроенный более ранней версии Azure Mobile Engagement Web SDK hello в веб-приложения, необходимо при обновлении hello SDK следующие точки hello tooconsider.</span><span class="sxs-lookup"><span data-stu-id="b38b7-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="b38b7-105">Если вы не выполнили несколько версий hello Mobile Engagement Web SDK, может потребоваться toocomplete несколько процедур во время обновления hello.</span><span class="sxs-lookup"><span data-stu-id="b38b7-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="b38b7-106">Например, если выполняется миграция из 1.4.0 too1.6.0 первый выполните hello процедуры tooupgrade из 1.4.0 too1.5.0.</span><span class="sxs-lookup"><span data-stu-id="b38b7-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="b38b7-107">Выполните процедуры tooupgrade hello из 1.5.0 too1.6.0.</span><span class="sxs-lookup"><span data-stu-id="b38b7-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="b38b7-108">Независимо от версии обновления, замените все более ранние версии файла hello azure-engagement.js hello последнюю версию файла hello.</span><span class="sxs-lookup"><span data-stu-id="b38b7-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="b38b7-109">Обновление с 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="b38b7-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="b38b7-110">В этом разделе описывается, как toomigrate пакет SDK Mobile Engagement Web интеграции из обновления Capptain hello, предлагаемых Capptain SAS, приложение Azure Mobile Engagement tooan.</span><span class="sxs-lookup"><span data-stu-id="b38b7-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="b38b7-111">При миграции из более ранней версии, проверьте hello см. в Capptain toofirst веб-сайт too1.2.1 миграции и примените hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="b38b7-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="b38b7-112">Эта версия hello Mobile Engagement Web SDK не поддерживает смарт-ТВ Samsung, Opera ТВ, webOS или функции hello Reach.</span><span class="sxs-lookup"><span data-stu-id="b38b7-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b38b7-113">Capptain и Azure Mobile Engagement не являются hello одной службы.</span><span class="sxs-lookup"><span data-stu-id="b38b7-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="b38b7-114">После процедуры Hello выделены только как toomigrate hello клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="b38b7-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="b38b7-115">Миграция hello Mobile Engagement Web SDK в приложение hello не выполняют миграцию данных из Capptain tooa мобильного охвата серверных компонентов.</span><span class="sxs-lookup"><span data-stu-id="b38b7-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="b38b7-116">Файлы JavaScript</span><span class="sxs-lookup"><span data-stu-id="b38b7-116">JavaScript files</span></span>
<span data-ttu-id="b38b7-117">Замените файл hello capptain-sdk.js файл hello azure-engagement.js, а потом изменить сценарий импортирует соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b38b7-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="b38b7-118">Удаление модуля Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="b38b7-118">Remove Capptain Reach</span></span>
<span data-ttu-id="b38b7-119">Эта версия hello Mobile Engagement Web SDK не поддерживает функции hello Reach.</span><span class="sxs-lookup"><span data-stu-id="b38b7-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="b38b7-120">Если охват Capptain интегрированы в приложение, необходимо tooremove его.</span><span class="sxs-lookup"><span data-stu-id="b38b7-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="b38b7-121">Удалите hello достичь CSS импорта со страницы и удалите hello связанные CSS-файл (capptain-reach.css, по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="b38b7-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="b38b7-122">Удалить следующие ресурсы Reach hello: hello закрыть изображение (capptain-close.png, по умолчанию) и hello фирменной символики значок (capptain уведомления-, по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="b38b7-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="b38b7-123">Удалите hello достичь пользовательского интерфейса для уведомления в приложении.</span><span class="sxs-lookup"><span data-stu-id="b38b7-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="b38b7-124">макет по умолчанию Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b38b7-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="b38b7-125">Удалите hello достичь пользовательского интерфейса для текста и веб-объявлений и для опросов.</span><span class="sxs-lookup"><span data-stu-id="b38b7-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="b38b7-126">макет по умолчанию Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b38b7-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="b38b7-127">Удалите hello `reach` объекта из вашей конфигурации, если он существует.</span><span class="sxs-lookup"><span data-stu-id="b38b7-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="b38b7-128">Это выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b38b7-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="b38b7-129">Удалите все прочие настройки Reach, например категории.</span><span class="sxs-lookup"><span data-stu-id="b38b7-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="b38b7-130">Удаление нерекомендуемых интерфейсов API</span><span class="sxs-lookup"><span data-stu-id="b38b7-130">Remove deprecated APIs</span></span>
<span data-ttu-id="b38b7-131">Некоторые интерфейсы API из Capptain являются устаревшими в hello Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="b38b7-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="b38b7-132">Удалите все вызовы toohello следующие API-интерфейсы: `agent.connect`, `agent.disconnect`, `agent.pause`, и `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="b38b7-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="b38b7-133">Удалите все экземпляры hello следующую обратные вызовы из конфигурации Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, и `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="b38b7-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="b38b7-134">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="b38b7-134">Configuration</span></span>
<span data-ttu-id="b38b7-135">Mobile Engagement используются идентификаторы SDK tooconfigure строку подключения, например, идентификатор приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b38b7-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="b38b7-136">Замените идентификатор приложения hello строки подключения.</span><span class="sxs-lookup"><span data-stu-id="b38b7-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="b38b7-137">Обратите внимание на то что hello глобальный объект hello настройки SDK изменится с `capptain` слишком`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="b38b7-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="b38b7-138">Перед миграцией:</span><span class="sxs-lookup"><span data-stu-id="b38b7-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="b38b7-139">После миграции:</span><span class="sxs-lookup"><span data-stu-id="b38b7-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="b38b7-140">Hello строку подключения для приложения отображается в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="b38b7-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="b38b7-141">Интерфейсы API JavaScript</span><span class="sxs-lookup"><span data-stu-id="b38b7-141">JavaScript APIs</span></span>
<span data-ttu-id="b38b7-142">глобальный объект JavaScript Hello `window.capptain` был переименован `window.azureEngagement` , но можно использовать hello `window.engagement` псевдоним для вызовов API.</span><span class="sxs-lookup"><span data-stu-id="b38b7-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="b38b7-143">Нельзя использовать настройки hello псевдоним toodefine hello SDK.</span><span class="sxs-lookup"><span data-stu-id="b38b7-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="b38b7-144">Например: `capptain.deviceId` становится `engagement.deviceId`, `capptain.agent.startActivity` становится `engagement.agent.startActivity` и т. д.</span><span class="sxs-lookup"><span data-stu-id="b38b7-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

