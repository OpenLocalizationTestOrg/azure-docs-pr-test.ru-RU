---
title: "Мониторинг сайта SharePoint с помощью Application Insights"
description: "Начало мониторинга нового приложения с помощью нового ключа инструментирования"
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: mbullwin
ms.openlocfilehash: 9c07ba125e0f9eae2b8f94661abf6dc1efc0cdad
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/01/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Мониторинг сайта SharePoint с помощью Application Insights
Azure Application Insights позволяет отслеживать доступность, производительность и использование приложений. В этой статье вы узнаете, как настроить эту службу для сайта SharePoint.

## <a name="create-an-application-insights-resource"></a>Создание ресурса Application Insights
На [портале Azure](https://portal.azure.com)создайте новый ресурс Application Insights. Выберите приложение ASP.NET в качестве типа приложения.

![Нажмите «Свойства», выберите ключ и нажмите сочетание клавиш CTRL + C](./media/app-insights-sharepoint/01-new.png)

В отобразившейся колонке будут содержатся данные о производительности и использовании приложения. Чтобы возвратиться к нему после очередного входа в Azure, найдите соответствующую плитку на начальном экране. Ее также можно найти, щелкнув «Обзор».

## <a name="add-our-script-to-your-web-pages"></a>Добавьте свой скрипт на веб-страницы
В разделе «Быстрый запуск» получите сценарий для веб-страниц:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Вставляйте скрипт перед тегом &lt;/head&gt; на каждой странице, где необходимо отслеживание. Если на вашем веб-сайте есть главная страница, можно разместить сценарий на ней. Например, в проекте ASP.NET MVC скрипт следует разместить на странице View\Shared\_Layout.cshtml.

Сценарий содержит ключ инструментирования, который направляет данные телеметрии к ресурсу Application Insights.

### <a name="add-the-code-to-your-site-pages"></a>Добавление кода на страницы сайта
#### <a name="on-the-master-page"></a>На главной странице
Отредактировав главную страницу сайта, можно обеспечить мониторинг каждой страницы сайта.

Ознакомьтесь с главной страницей и измените ее с помощью SharePoint Designer или другого редактора.

![](./media/app-insights-sharepoint/03-master.png)

Добавьте код прямо перед тегом </head> . 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>На отдельных страницах
Для мониторинга ограниченного набора страниц добавьте сценарий отдельно для каждой страницы. 

Вставьте веб-часть и внедрите в нее фрагмент кода.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Просмотр данных о приложении
Разверните приложение заново.

Вернитесь к колонке приложения на [портале Azure](https://portal.azure.com).

В окне поиска отобразятся первые события. 

![](./media/app-insights-sharepoint/09-search.png)

Нажмите кнопку «Обновить» через несколько секунд, если ожидаете дополнительные данные.

В колонке "Обзор" выберите **Аналитика использования** , чтобы просмотреть диаграммы пользователей, сеансов и просмотров страницы:

![](./media/app-insights-sharepoint/06-usage.png)

Щелкните любую диаграмму для просмотра дополнительных сведений, например "Просмотры страницы":

![](./media/app-insights-sharepoint/07-pages.png)

или "Пользователей":

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Запись идентификатора пользователя
Фрагмент кода стандартной веб-страницы не записывает идентификатор пользователя из SharePoint, однако эту возможность можно реализовать, внеся небольшое изменение.

1. Скопируйте ключ инструментирования приложения из раскрывающегося списка "Основные компоненты" в Application Insights. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Вставьте ключ инструментирования вместо строки "XXXX" в приведенном ниже фрагменте кода. 
2. Внедрите скрипт в приложение SharePoint вместо фрагмента кода, полученного с портала.

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that the SP.UserProfiles.js file is loaded before the custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get the current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for the target user. 
    // To get the PersonProperties object for the current user, use the 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load the PersonProperties object and send the request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if the executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if the executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a>Дальнейшие действия
* [Использование веб-тестов](app-insights-monitor-web-app-availability.md) для мониторинга доступности сайта.
* [Использование Application Insights](app-insights-overview.md) для других типов приложений.

<!--Link references-->


