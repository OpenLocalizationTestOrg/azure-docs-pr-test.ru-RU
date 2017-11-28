---
title: "aaaMonitor сайта SharePoint с помощью Application Insights"
description: "Начало мониторинга нового приложения с помощью нового ключа инструментирования"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="218c9-103">Мониторинг сайта SharePoint с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="218c9-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="218c9-104">Azure Application Insights отслеживает hello доступности, производительности и использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="218c9-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="218c9-105">Здесь вы узнаете, как tooset ее для сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="218c9-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="218c9-106">Создание ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="218c9-106">Create an Application Insights resource</span></span>
<span data-ttu-id="218c9-107">В hello [портал Azure](https://portal.azure.com), создать новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="218c9-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="218c9-108">Выберите в качестве типа приложения hello ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="218c9-108">Choose ASP.NET as hello application type.</span></span>

![Щелкните свойства, выберите раздел hello и нажмите клавиши ctrl + C](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="218c9-110">открывается колонка Hello — hello месте, где вы увидите данные производительности и использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="218c9-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="218c9-111">Назад tooit tooget входа tooAzure, при очередном следует найти плитки для него на начальном экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="218c9-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="218c9-112">Также можно выбрать пункт Обзор toofind его.</span><span class="sxs-lookup"><span data-stu-id="218c9-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="218c9-113">Добавьте наш сценарий tooyour веб-страницы</span><span class="sxs-lookup"><span data-stu-id="218c9-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="218c9-114">В быстром запуске получение hello скрипта для веб-страниц:</span><span class="sxs-lookup"><span data-stu-id="218c9-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="218c9-115">Вставить скрипт hello непосредственно перед hello &lt;/head&gt; тег каждой страницы, которую должна tootrack.</span><span class="sxs-lookup"><span data-stu-id="218c9-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="218c9-116">Если веб-сайт имеет главной страницы, можно поместить скрипт hello существует.</span><span class="sxs-lookup"><span data-stu-id="218c9-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="218c9-117">Например, в проекте ASP.NET MVC скрипт следует разместить на странице View\Shared\_Layout.cshtml.</span><span class="sxs-lookup"><span data-stu-id="218c9-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="218c9-118">сценарий Hello содержит ключ инструментирования hello, указывающий ресурс Application Insights tooyour телеметрии hello.</span><span class="sxs-lookup"><span data-stu-id="218c9-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="218c9-119">Добавить tooyour сайта hello кодовые страницы</span><span class="sxs-lookup"><span data-stu-id="218c9-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="218c9-120">На главной странице приветствия</span><span class="sxs-lookup"><span data-stu-id="218c9-120">On hello master page</span></span>
<span data-ttu-id="218c9-121">При редактировании главной страницы сайта hello, предоставляющего мониторинг на каждой странице узла hello.</span><span class="sxs-lookup"><span data-stu-id="218c9-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="218c9-122">Извлечение hello главную страницу и измените его с помощью SharePoint Designer или в другом редакторе.</span><span class="sxs-lookup"><span data-stu-id="218c9-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="218c9-123">Добавьте код hello непосредственно перед hello </head> тег.</span><span class="sxs-lookup"><span data-stu-id="218c9-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="218c9-124">На отдельных страницах</span><span class="sxs-lookup"><span data-stu-id="218c9-124">Or on individual pages</span></span>
<span data-ttu-id="218c9-125">toomonitor ограниченный набор страниц, добавить скрипт hello отдельно tooeach страницы.</span><span class="sxs-lookup"><span data-stu-id="218c9-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="218c9-126">Вставить веб-часть и внедрить фрагмент кода hello в нем.</span><span class="sxs-lookup"><span data-stu-id="218c9-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="218c9-127">Просмотр данных о приложении</span><span class="sxs-lookup"><span data-stu-id="218c9-127">View data about your app</span></span>
<span data-ttu-id="218c9-128">Разверните приложение заново.</span><span class="sxs-lookup"><span data-stu-id="218c9-128">Redeploy your app.</span></span>

<span data-ttu-id="218c9-129">Возвращаемое tooyour колонке приложения в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="218c9-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="218c9-130">Hello первого события будут отображаться в поиске.</span><span class="sxs-lookup"><span data-stu-id="218c9-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="218c9-131">Нажмите кнопку «Обновить» через несколько секунд, если ожидаете дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="218c9-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="218c9-132">Из колонки Обзор hello, нажмите кнопку **аналитики использования** toocharts toosee пользователей, сеансы и представления страницы:</span><span class="sxs-lookup"><span data-stu-id="218c9-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="218c9-133">Щелкните любой диаграммы toosee Дополнительные сведения — например просмотров страниц:</span><span class="sxs-lookup"><span data-stu-id="218c9-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="218c9-134">или "Пользователей":</span><span class="sxs-lookup"><span data-stu-id="218c9-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="218c9-135">Запись идентификатора пользователя</span><span class="sxs-lookup"><span data-stu-id="218c9-135">Capturing User Id</span></span>
<span data-ttu-id="218c9-136">фрагмент кода Hello стандартной веб-страницы без записи hello идентификатор пользователя из SharePoint, но это можно сделать с помощью лишь небольшое изменение.</span><span class="sxs-lookup"><span data-stu-id="218c9-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="218c9-137">Скопируйте ключ инструментирования приложения из раскрывающегося списка в Application Insights основных hello.</span><span class="sxs-lookup"><span data-stu-id="218c9-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="218c9-138">В приведенном ниже фрагменте hello, замените ключ инструментирования hello «XXXX».</span><span class="sxs-lookup"><span data-stu-id="218c9-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="218c9-139">Внедрение hello сценария в приложении SharePoint вместо фрагмент кода hello, получаемых из портала hello.</span><span class="sxs-lookup"><span data-stu-id="218c9-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="218c9-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="218c9-140">Next Steps</span></span>
* <span data-ttu-id="218c9-141">[Веб-тестов](app-insights-monitor-web-app-availability.md) toomonitor hello доступности веб-узла.</span><span class="sxs-lookup"><span data-stu-id="218c9-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="218c9-142">[Использование Application Insights](app-insights-overview.md) для других типов приложений.</span><span class="sxs-lookup"><span data-stu-id="218c9-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


