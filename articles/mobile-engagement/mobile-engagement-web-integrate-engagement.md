---
title: "пакет SDK Mobile Engagement Web интеграции aaaAzure | Документы Microsoft"
description: "Здравствуйте, последние обновления и процедуры для hello Azure Mobile Engagement Web SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Интегрирование Служб мобильного взаимодействия Azure в веб-приложение
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Hello в этой статье описывается hello простейший способ tooactivate hello аналитика и мониторинга в Azure Mobile Engagement в веб-приложении.

Выполните все статистические данные о пользователях, сеансах, действия, сбои и technicals hello действия tooactivate hello журнала отчетов, необходимые toocompute. Для статистики, связанные с приложением, например события, ошибок и задания необходимо активировать журнала отчетов вручную с помощью hello Azure Mobile Engagement API. Дополнительные сведения Узнайте [как toouse hello дополнительные теги API в веб-приложение Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Введение
[Загрузите hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).
Привет, мобильных веб-Engagement пакет SDK поставляется как отдельный файл JavaScript, azure-engagement.js, у вас есть tooinclude на каждой странице сайта или веб-приложения.

> [!IMPORTANT]
> Перед запуском этого скрипта необходимо запустить скрипт или писать tooconfigure Mobile Engagement для вашего приложения фрагмент кода.
> 
> 

## <a name="browser-compatibility"></a>Совместимость с браузерами
Hello Mobile Engagement Web SDK использует собственный JSON кодирования и декодирования, кроме запросы AJAX toocross домена (полагаться на спецификации W3C CORS hello). Она совместима с hello следующие браузеры:

* Microsoft Edge 12 или более поздней версии.
* Internet Explorer 10 или более поздней версии.
* Firefox 3.5 или более поздней версии.
* Chrome 4 или более поздней версии.
* Safari 6 или более поздней версии.
* Opera 12 или более поздней версии.

## <a name="configure-mobile-engagement"></a>Настройка Служб мобильного взаимодействия
Написать сценарий, который создает глобальный `azureEngagement` объекта JavaScript, такого как следующий пример hello. Так как сайт может иметь несколько страниц, в примере предполагается, что этот сценарий включен в каждую страницу. В этом примере hello объекта JavaScript с именем `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Hello `connectionString` значение приложении отображается в hello портал Azure.

> [!NOTE]
> Параметры `appVersionName` и `appVersionCode` являются необязательными. Однако рекомендуется их также настроить, чтобы аналитика могла обрабатывать сведения о версии.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Добавление сценариев Служб мобильного взаимодействия в страницы
Добавьте мобильного охвата сценарии tooyour страниц в одном из следующих способов hello:

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

или

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
После загрузки hello Mobile Engagement Web SDK сценария, он создает hello **engagement** API пакета SDK для hello tooaccess псевдоним. Нельзя использовать эту конфигурацию пакета SDK для hello toodefine псевдоним. В данной документации он используется в справочных целях.

Обратите внимание, что при псевдоним по умолчанию hello конфликтует с другой глобальной переменной со страницы, можно переопределить его в конфигурации hello следующим перед их загрузкой hello Mobile Engagement Web SDK.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>Упрощенные отчеты
Базовые отчеты в Службах мобильного взаимодействия охватывают статистику на уровне сеанса, такую как данные о пользователях, сеансах, действиях и сбоях.

### <a name="session-tracking"></a>Отслеживание сеансов
Сеанс Служб мобильного взаимодействия состоит из последовательности действий, каждое из которых определяется по имени.

На классическом веб-сайте рекомендуется объявлять разные действия на разных страницах сайта. Для веб-сайта или веб-приложения, в какие hello текущей страницы никогда не меняется может потребоваться tootrack hello действий в меньшем масштабе, такие как внутри страницы приветствия.

Либо способом, toostart или измените hello текущая активность пользователей hello вызовов `engagement.agent.startActivity` функции. Например:

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

Hello сервера мобильного охвата автоматически завершает открытый сеанс в течение трех минут после закрытия страницы приложения hello.

Также можно завершить сеанс вручную, вызвав `engagement.agent.endActivity`. Это задает hello текущего пользователя действия too'Idle. "  Hello сеанс будет завершен 10 секунд позже, если только новый вызов слишком`engagement.agent.startActivity` возобновляет hello сеанса.

10-секундная задержка hello hello объекта глобального обязательств, можно настроить следующим образом.

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> Нельзя использовать `engagement.agent.endActivity` в hello `onunload` обратного вызова, так как нельзя выполнять вызовы AJAX на этом этапе.
> 
> 

## <a name="advanced-reporting"></a>Расширенные отчеты
При необходимости следует tooreport события конкретного приложения, ошибок и задания необходимо hello toouse Mobile Engagement API. Доступ к hello Mobile Engagement API через hello `engagement.agent` объекта.

Вы может получить доступ ко всем hello расширенных возможностей мобильного охвата, в hello Mobile Engagement API. Hello API, описанные в статье hello [как toouse hello дополнительные теги API в веб-приложение Mobile Engagement](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-hello-urls-used-for-ajax-calls"></a>Настраивать hello URL-адреса, используемый для вызовов AJAX
Вы можете настроить URL-адреса, которые использует пакет SDK Mobile Engagement Web hello. Например tooredefine hello URL-адрес (hello SDK конечную точку для ведения журнала), можно переопределить конфигурацию hello следующим образом.

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

Если ваш URL-адрес функции возвращают строку, начинающуюся с `/`, `//`, `http://`, или `https://`, не используется схема по умолчанию hello. По умолчанию hello `https://` используется схема для этих URL-адресов. Если схема по умолчанию hello toocustomize, переопределите hello конфигурации, следующим образом:

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
