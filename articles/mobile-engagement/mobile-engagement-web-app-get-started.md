---
title: "aaaGet работы с Azure Mobile Engagement для веб-приложений | Документы Microsoft"
description: "Узнайте, как toouse Azure Mobile Engagement с analytics и отправка уведомлений для веб-приложений."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Приступая к работе со Службами мобильного взаимодействия Azure для веб-приложений
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования веб-приложения.

> [!NOTE]
> Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов. Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Этот учебник требует hello следующее:

* Visual Studio 2015 или другой редактор по вашему выбору;
* [веб-пакет SDK](http://aka.ms/P7b453)

Этот пакет SDK веб находится в предварительной версии и поддерживает только аналитика в момент hello и еще не поддерживает отправку уведомлений push браузера или в приложении. 

> [!NOTE]
> toocomplete этого учебника необходимо иметь активную учетную запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>Настройка Служб мобильного взаимодействия для веб-приложения
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений
В этом руководстве содержатся «базовой интеграции,» передаются данные toocollect минимальный набор необходимых hello.

Мы создадим базовое веб-приложение с помощью Visual Studio toodemonstrate hello интеграции на то, что с помощью любого веб-приложения, созданные за пределами Visual Studio, также можно выполнить действия hello. 

### <a name="create-a-new-web-app"></a>Создание нового веб-приложения
Hello следующие шаги предполагают использование Visual Studio 2015 hello хотя hello действия схожи в более ранних версиях Visual Studio. 

1. Запустите Visual Studio и в hello **Главная** выберите **новый проект**.
2. Во всплывающем hello выберите **Web** -> **веб-приложение ASP.Net**. Заполните приложение hello **имя**, **расположение** и **имя решения**, а затем нажмите кнопку **ОК**.
3. В hello **выберите шаблон** всплывающее окно, выберите **пустой** под **шаблоны ASP.Net 4.5** и нажмите кнопку **ОК**. 

Вы создали новый пустой проект веб-приложения в которую будем интегрировать hello Azure Mobile Engagement Web SDK.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Подключение Engagement tooMobile внутренний сервер приложений
1. Создайте новую папку с именем **javascript** в решении и добавьте hello Web SDK JS-файл **azure engagement.js** в него. 
2. Добавьте новый файл с именем **main.js** в этой папке javascript с hello, следующий код. Убедитесь, что строка подключения tooupdate hello. Это `azureEngagement` объект будет tooaccess используется пакет SDK веб-методов. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Использование JS-файлов в Visual Studio][1]

## <a name="enable-real-time-monitoring"></a>Включение мониторинга в режиме реального времени
В toostart порядок отправки данных и убедитесь, что пользователи hello active необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello действия. Действие в контексте hello веб-приложение является веб-страницы. 

1. Создание новой страницы вызывается **home.html** решения и набор его как запуск hello страница для веб-приложения. 
2. Включить hello два сценарии JavaScript, который мы добавили ранее на этой странице, добавив следующие hello внутри тега body hello. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Обновить тег toocall hello текст EngagementAgent `startActivity` метод
   
        <body onload="engagement.agent.startActivity('Home')">
4. Вот как будет выглядеть страница **home.html** :
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>Подключение приложения с возможностью его отслеживания в режиме реального времени
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>Расширение аналитики
Вот все методы hello, доступных с Web SDK, который можно использовать для анализа.

1. Действия и веб-страницы:
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. События
   
        engagement.agent.sendEvent(name, extras);
3. Ошибки
   
        engagement.agent.sendError(name, extras);
4. Задания
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

