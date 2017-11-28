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
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="70d62-103">Приступая к работе со Службами мобильного взаимодействия Azure для веб-приложений</span><span class="sxs-lookup"><span data-stu-id="70d62-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="70d62-104">В этом разделе показано, как Azure Mobile Engagement toounderstand toouse использования веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="70d62-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="70d62-105">Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов.</span><span class="sxs-lookup"><span data-stu-id="70d62-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="70d62-106">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="70d62-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="70d62-107">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="70d62-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="70d62-108">Visual Studio 2015 или другой редактор по вашему выбору;</span><span class="sxs-lookup"><span data-stu-id="70d62-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="70d62-109">веб-пакет SDK</span><span class="sxs-lookup"><span data-stu-id="70d62-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="70d62-110">Этот пакет SDK веб находится в предварительной версии и поддерживает только аналитика в момент hello и еще не поддерживает отправку уведомлений push браузера или в приложении.</span><span class="sxs-lookup"><span data-stu-id="70d62-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="70d62-111">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="70d62-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="70d62-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="70d62-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="70d62-113">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="70d62-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="70d62-114">Настройка Служб мобильного взаимодействия для веб-приложения</span><span class="sxs-lookup"><span data-stu-id="70d62-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="70d62-115"><a id="connecting-app"></a>Подключение мобильного охвата toohello внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="70d62-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="70d62-116">В этом руководстве содержатся «базовой интеграции,» передаются данные toocollect минимальный набор необходимых hello.</span><span class="sxs-lookup"><span data-stu-id="70d62-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="70d62-117">Мы создадим базовое веб-приложение с помощью Visual Studio toodemonstrate hello интеграции на то, что с помощью любого веб-приложения, созданные за пределами Visual Studio, также можно выполнить действия hello.</span><span class="sxs-lookup"><span data-stu-id="70d62-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="70d62-118">Создание нового веб-приложения</span><span class="sxs-lookup"><span data-stu-id="70d62-118">Create a new Web App</span></span>
<span data-ttu-id="70d62-119">Hello следующие шаги предполагают использование Visual Studio 2015 hello хотя hello действия схожи в более ранних версиях Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70d62-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="70d62-120">Запустите Visual Studio и в hello **Главная** выберите **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="70d62-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="70d62-121">Во всплывающем hello выберите **Web** -> **веб-приложение ASP.Net**.</span><span class="sxs-lookup"><span data-stu-id="70d62-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="70d62-122">Заполните приложение hello **имя**, **расположение** и **имя решения**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="70d62-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="70d62-123">В hello **выберите шаблон** всплывающее окно, выберите **пустой** под **шаблоны ASP.Net 4.5** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="70d62-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="70d62-124">Вы создали новый пустой проект веб-приложения в которую будем интегрировать hello Azure Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="70d62-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="70d62-125">Подключение Engagement tooMobile внутренний сервер приложений</span><span class="sxs-lookup"><span data-stu-id="70d62-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="70d62-126">Создайте новую папку с именем **javascript** в решении и добавьте hello Web SDK JS-файл **azure engagement.js** в него.</span><span class="sxs-lookup"><span data-stu-id="70d62-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="70d62-127">Добавьте новый файл с именем **main.js** в этой папке javascript с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="70d62-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="70d62-128">Убедитесь, что строка подключения tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="70d62-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="70d62-129">Это `azureEngagement` объект будет tooaccess используется пакет SDK веб-методов.</span><span class="sxs-lookup"><span data-stu-id="70d62-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Использование JS-файлов в Visual Studio][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="70d62-131">Включение мониторинга в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="70d62-131">Enable real-time monitoring</span></span>
<span data-ttu-id="70d62-132">В toostart порядок отправки данных и убедитесь, что пользователи hello active необходимо отправить по крайней мере один внутреннего сервера мобильного охвата toohello действия.</span><span class="sxs-lookup"><span data-stu-id="70d62-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="70d62-133">Действие в контексте hello веб-приложение является веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="70d62-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="70d62-134">Создание новой страницы вызывается **home.html** решения и набор его как запуск hello страница для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="70d62-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="70d62-135">Включить hello два сценарии JavaScript, который мы добавили ранее на этой странице, добавив следующие hello внутри тега body hello.</span><span class="sxs-lookup"><span data-stu-id="70d62-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="70d62-136">Обновить тег toocall hello текст EngagementAgent `startActivity` метод</span><span class="sxs-lookup"><span data-stu-id="70d62-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="70d62-137">Вот как будет выглядеть страница **home.html** :</span><span class="sxs-lookup"><span data-stu-id="70d62-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="70d62-138">Подключение приложения с возможностью его отслеживания в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="70d62-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="70d62-139">Расширение аналитики</span><span class="sxs-lookup"><span data-stu-id="70d62-139">Extend analytics</span></span>
<span data-ttu-id="70d62-140">Вот все методы hello, доступных с Web SDK, который можно использовать для анализа.</span><span class="sxs-lookup"><span data-stu-id="70d62-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="70d62-141">Действия и веб-страницы:</span><span class="sxs-lookup"><span data-stu-id="70d62-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="70d62-142">События</span><span class="sxs-lookup"><span data-stu-id="70d62-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="70d62-143">Ошибки</span><span class="sxs-lookup"><span data-stu-id="70d62-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="70d62-144">Задания</span><span class="sxs-lookup"><span data-stu-id="70d62-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

