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
# <a name="azure-mobile-engagement-web-sdk"></a>Веб-пакет SDK для Служб мобильного взаимодействия Azure
Начало для всех hello подробные сведения о том, как toointegrate Azure Mobile Engagement в веб-приложения. При желании toogive его try прежде чем начать с собственного веб-приложения. в разделе нашей [15-минутных учебника](mobile-engagement-web-app-get-started.md).

## <a name="integration-procedures"></a>Процедуры по интеграции
1. Дополнительные сведения [как toointegrate Mobile Engagement в веб-приложении](mobile-engagement-web-integrate-engagement.md).
2. Реализация плана тег, узнайте [как toouse hello дополнительные теги API в веб-приложения Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="release-notes"></a>Заметки о выпуске
### <a name="202-10182016"></a>2.0.2 (10/18/2016)
* Фиксированный сбой в режиме закрытого просмотра (Safari).
* Фиксированный сбой в браузерах с отключенными файлами cookie.

Для всех версий см. в разделе hello [завершения заметки о выпуске](mobile-engagement-web-release-notes.md).

## <a name="upgrade-procedures"></a>Процедуры обновления
### <a name="upgrade-from-121-too200"></a>Обновление с 1.2.1 too2.0.0
Hello следующих разделах описаны как toomigrate пакет SDK Mobile Engagement Web интеграции из обновления Capptain hello, предлагаемых Capptain SAS, приложение Azure Mobile Engagement tooan. При миграции из более ранней версии, чем 1.2.1, сначала обратитесь к веб-сайт toomigrate hello Capptain too1.2.1 и примените hello следующих процедур.

Эта версия hello Mobile Engagement Web SDK не поддерживает смарт-ТВ Samsung, Opera ТВ, webOS или функции hello Reach.

> [!IMPORTANT]
> Capptain и Azure Mobile Engagement не являются hello одной службы и выделите hello следующих процедур, как только toomigrate hello клиентского приложения. Миграция hello Mobile Engagement Web SDK в приложение hello не выполняют миграцию данных из Capptain tooa мобильного охвата серверных компонентов.
> 
> 

#### <a name="javascript-files"></a>Файлы JavaScript
Замените файл hello capptain-sdk.js файл hello azure-engagement.js, а потом изменить сценарий импортирует соответствующим образом.

#### <a name="remove-capptain-reach"></a>Удаление модуля Capptain Reach
Эта версия hello Mobile Engagement Web SDK не поддерживает функции hello Reach. Если Capptain Reach, интегрированы в приложение, необходимо tooremove его.

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

#### <a name="remove-deprecated-apis"></a>Удаление нерекомендуемых интерфейсов API
Некоторые интерфейсы API из Capptain являются устаревшими в hello Mobile Engagement Web SDK.

Удалите все вызовы toohello следующие API-интерфейсы: `agent.connect`, `agent.disconnect`, `agent.pause`, и `agent.sendMessageToDevice`.

Удалите следующую обратные вызовы из конфигурации Capptain hello: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, и `onPushMessageReceived`.

#### <a name="configuration"></a>Конфигурация
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

Hello строку подключения для приложения отображается в hello портал Azure.

#### <a name="javascript-apis"></a>Интерфейсы API JavaScript
глобальный объект JavaScript Hello `window.capptain` был переименован `window.azureEngagement`, но вы можете использовать hello `window.engagement` псевдоним для вызовов API. Нельзя использовать эту конфигурацию пакета SDK для hello toodefine псевдоним.

Например: `capptain.deviceId` становится `engagement.deviceId`, `capptain.agent.startActivity` становится `engagement.agent.startActivity` и т. д.

Если уже имеется встроенный более ранней версии Azure Mobile Engagement Web SDK hello в приложение, прочитайте о [обновить процедуры](mobile-engagement-web-upgrade-procedure.md).

