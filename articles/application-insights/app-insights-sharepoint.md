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
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Мониторинг сайта SharePoint с помощью Application Insights
Azure Application Insights отслеживает hello доступности, производительности и использовании приложения. Здесь вы узнаете, как tooset ее для сайта SharePoint.

## <a name="create-an-application-insights-resource"></a>Создание ресурса Application Insights
В hello [портал Azure](https://portal.azure.com), создать новый ресурс Application Insights. Выберите в качестве типа приложения hello ASP.NET.

![Щелкните свойства, выберите раздел hello и нажмите клавиши ctrl + C](./media/app-insights-sharepoint/01-new.png)

открывается колонка Hello — hello месте, где вы увидите данные производительности и использовании приложения. Назад tooit tooget входа tooAzure, при очередном следует найти плитки для него на начальном экране приветствия. Также можно выбрать пункт Обзор toofind его.

## <a name="add-our-script-tooyour-web-pages"></a>Добавьте наш сценарий tooyour веб-страницы
В быстром запуске получение hello скрипта для веб-страниц:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Вставить скрипт hello непосредственно перед hello &lt;/head&gt; тег каждой страницы, которую должна tootrack. Если веб-сайт имеет главной страницы, можно поместить скрипт hello существует. Например, в проекте ASP.NET MVC скрипт следует разместить на странице View\Shared\_Layout.cshtml.

сценарий Hello содержит ключ инструментирования hello, указывающий ресурс Application Insights tooyour телеметрии hello.

### <a name="add-hello-code-tooyour-site-pages"></a>Добавить tooyour сайта hello кодовые страницы
#### <a name="on-hello-master-page"></a>На главной странице приветствия
При редактировании главной страницы сайта hello, предоставляющего мониторинг на каждой странице узла hello.

Извлечение hello главную страницу и измените его с помощью SharePoint Designer или в другом редакторе.

![](./media/app-insights-sharepoint/03-master.png)

Добавьте код hello непосредственно перед hello </head> тег. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>На отдельных страницах
toomonitor ограниченный набор страниц, добавить скрипт hello отдельно tooeach страницы. 

Вставить веб-часть и внедрить фрагмент кода hello в нем.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Просмотр данных о приложении
Разверните приложение заново.

Возвращаемое tooyour колонке приложения в hello [портал Azure](https://portal.azure.com).

Hello первого события будут отображаться в поиске. 

![](./media/app-insights-sharepoint/09-search.png)

Нажмите кнопку «Обновить» через несколько секунд, если ожидаете дополнительные данные.

Из колонки Обзор hello, нажмите кнопку **аналитики использования** toocharts toosee пользователей, сеансы и представления страницы:

![](./media/app-insights-sharepoint/06-usage.png)

Щелкните любой диаграммы toosee Дополнительные сведения — например просмотров страниц:

![](./media/app-insights-sharepoint/07-pages.png)

или "Пользователей":

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Запись идентификатора пользователя
фрагмент кода Hello стандартной веб-страницы без записи hello идентификатор пользователя из SharePoint, но это можно сделать с помощью лишь небольшое изменение.

1. Скопируйте ключ инструментирования приложения из раскрывающегося списка в Application Insights основных hello. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. В приведенном ниже фрагменте hello, замените ключ инструментирования hello «XXXX». 
2. Внедрение hello сценария в приложении SharePoint вместо фрагмент кода hello, получаемых из портала hello.

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



## <a name="next-steps"></a>Дальнейшие действия
* [Веб-тестов](app-insights-monitor-web-app-availability.md) toomonitor hello доступности веб-узла.
* [Использование Application Insights](app-insights-overview.md) для других типов приложений.

<!--Link references-->


