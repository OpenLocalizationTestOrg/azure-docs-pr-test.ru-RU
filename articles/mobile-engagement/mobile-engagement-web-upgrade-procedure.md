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
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a>Процедуры обновления веб-пакета SDK для Служб мобильного взаимодействия Azure
Если уже имеется встроенный более ранней версии Azure Mobile Engagement Web SDK hello в веб-приложения, необходимо при обновлении hello SDK следующие точки hello tooconsider.

Если вы не выполнили несколько версий hello Mobile Engagement Web SDK, может потребоваться toocomplete несколько процедур во время обновления hello. Например, если выполняется миграция из 1.4.0 too1.6.0 первый выполните hello процедуры tooupgrade из 1.4.0 too1.5.0. Выполните процедуры tooupgrade hello из 1.5.0 too1.6.0.

Независимо от версии обновления, замените все более ранние версии файла hello azure-engagement.js hello последнюю версию файла hello.

## <a name="upgrade-from-121-too200"></a>Обновление с 1.2.1 too2.0.0
В этом разделе описывается, как toomigrate пакет SDK Mobile Engagement Web интеграции из обновления Capptain hello, предлагаемых Capptain SAS, приложение Azure Mobile Engagement tooan. При миграции из более ранней версии, проверьте hello см. в Capptain toofirst веб-сайт too1.2.1 миграции и примените hello следующих процедур.

Эта версия hello Mobile Engagement Web SDK не поддерживает смарт-ТВ Samsung, Opera ТВ, webOS или функции hello Reach.

> [!IMPORTANT]
> Capptain и Azure Mobile Engagement не являются hello одной службы. После процедуры Hello выделены только как toomigrate hello клиентского приложения. Миграция hello Mobile Engagement Web SDK в приложение hello не выполняют миграцию данных из Capptain tooa мобильного охвата серверных компонентов.
> 
> 

### <a name="javascript-files"></a>Файлы JavaScript
Замените файл hello capptain-sdk.js файл hello azure-engagement.js, а потом изменить сценарий импортирует соответствующим образом.

### <a name="remove-capptain-reach"></a>Удаление модуля Capptain Reach
Эта версия hello Mobile Engagement Web SDK не поддерживает функции hello Reach. Если охват Capptain интегрированы в приложение, необходимо tooremove его.

Удалите hello достичь CSS импорта со страницы и удалите hello связанные CSS-файл (capptain-reach.css, по умолчанию).

Удалить следующие ресурсы Reach hello: hello закрыть изображение (capptain-close.png, по умолчанию) и hello фирменной символики значок (capptain уведомления-, по умолчанию).

Удалите hello достичь пользовательского интерфейса для уведомления в приложении. макет по умолчанию Hello выглядит следующим образом:

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

Удалите hello достичь пользовательского интерфейса для текста и веб-объявлений и для опросов. макет по умолчанию Hello выглядит следующим образом:

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

Удалите hello `reach` объекта из вашей конфигурации, если он существует. Это выглядит следующим образом.

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Удалите все прочие настройки Reach, например категории.

### <a name="remove-deprecated-apis"></a>Удаление нерекомендуемых интерфейсов API
Некоторые интерфейсы API из Capptain являются устаревшими в hello Mobile Engagement Web SDK.

Удалите все вызовы toohello следующие API-интерфейсы: `agent.connect`, `agent.disconnect`, `agent.pause`, и `agent.sendMessageToDevice`.

Удалите все экземпляры hello следующую обратные вызовы из конфигурации Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, и `onPushMessageReceived`.

### <a name="configuration"></a>Конфигурация
Mobile Engagement используются идентификаторы SDK tooconfigure строку подключения, например, идентификатор приложения hello.

Замените идентификатор приложения hello строки подключения. Обратите внимание на то что hello глобальный объект hello настройки SDK изменится с `capptain` слишком`azureEngagement`.

Перед миграцией:

    window.capptain = {
      appId: ...,
      [...]
    };

После миграции:

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

Hello строку подключения для приложения отображается в hello портала Azure.

### <a name="javascript-apis"></a>Интерфейсы API JavaScript
глобальный объект JavaScript Hello `window.capptain` был переименован `window.azureEngagement` , но можно использовать hello `window.engagement` псевдоним для вызовов API. Нельзя использовать настройки hello псевдоним toodefine hello SDK.

Например: `capptain.deviceId` становится `engagement.deviceId`, `capptain.agent.startActivity` становится `engagement.agent.startActivity` и т. д.

