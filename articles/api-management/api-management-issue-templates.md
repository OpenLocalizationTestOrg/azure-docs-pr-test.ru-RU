---
title: "Шаблоны проблем в службе управления API Azure | Документация Майкрософт"
description: "Сведения о настройке содержимого страниц проблем на портале разработчика в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="226f6-103">Шаблоны проблем в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="226f6-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="226f6-104">Служба управления API Azure позволяет настраивать содержимое страниц портала разработчика с помощью набора шаблонов.</span><span class="sxs-lookup"><span data-stu-id="226f6-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="226f6-105">С помощью синтаксиса [DotLiquid](http://dotliquidmarkup.org/), выбранного редактора, например [DotLiquid для разработчиков](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), и указанного набора локализованных [строковых ресурсов](api-management-template-resources.md#strings), [ресурсов глифов](api-management-template-resources.md#glyphs), а также [элементов управления на странице](api-management-page-controls.md) можно гибко настраивать содержимое страниц по своему усмотрению с использованием этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="226f6-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="226f6-106">С помощью шаблонов в этом разделе вы сможете настроить содержимое страниц проблем на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="226f6-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="226f6-107">Список проблем</span><span class="sxs-lookup"><span data-stu-id="226f6-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="226f6-108">Примеры шаблонов по умолчанию включены в следующую документацию, но могут в любой момент измениться, так как ведется постоянная работа по их улучшению.</span><span class="sxs-lookup"><span data-stu-id="226f6-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="226f6-109">Актуальные шаблоны по умолчанию можно просмотреть на портале разработчика, перейдя к требуемому отдельному шаблону.</span><span class="sxs-lookup"><span data-stu-id="226f6-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="226f6-110">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="226f6-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="226f6-111"><a name="IssueList"></a> Список проблем</span><span class="sxs-lookup"><span data-stu-id="226f6-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="226f6-112">Шаблон **списка проблем** позволяет настроить текст страницы со списком проблем на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="226f6-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="226f6-113">![Список проблем на портале разработчика](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "список проблем на портале разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="226f6-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="226f6-114">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="226f6-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="226f6-115">Управление</span><span class="sxs-lookup"><span data-stu-id="226f6-115">Controls</span></span>  
 <span data-ttu-id="226f6-116">В шаблоне `Issue list` можно использовать следующие [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="226f6-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="226f6-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="226f6-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="226f6-118">Модель данных</span><span class="sxs-lookup"><span data-stu-id="226f6-118">Data model</span></span>  
  
|<span data-ttu-id="226f6-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="226f6-119">Property</span></span>|<span data-ttu-id="226f6-120">Тип</span><span class="sxs-lookup"><span data-stu-id="226f6-120">Type</span></span>|<span data-ttu-id="226f6-121">Описание</span><span class="sxs-lookup"><span data-stu-id="226f6-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="226f6-122">Проблемы</span><span class="sxs-lookup"><span data-stu-id="226f6-122">Issues</span></span>|<span data-ttu-id="226f6-123">Коллекция сущностей [проблем](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="226f6-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="226f6-124">Проблемы, которые отображаются для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="226f6-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="226f6-125">Разбиение по страницам</span><span class="sxs-lookup"><span data-stu-id="226f6-125">Paging</span></span>|<span data-ttu-id="226f6-126">Сущность [разбиения по страницам](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="226f6-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="226f6-127">Сведения о разбиении по страницам для коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="226f6-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="226f6-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="226f6-128">IsAuthenticated</span></span>|<span data-ttu-id="226f6-129">Логическое</span><span class="sxs-lookup"><span data-stu-id="226f6-129">boolean</span></span>|<span data-ttu-id="226f6-130">Указывает, выполнил ли текущий пользователь вход на портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="226f6-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="226f6-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="226f6-131">CanReportIssues</span></span>|<span data-ttu-id="226f6-132">Логическое</span><span class="sxs-lookup"><span data-stu-id="226f6-132">boolean</span></span>|<span data-ttu-id="226f6-133">Указывает, имеет ли текущий пользователь разрешения на сообщение о проблеме.</span><span class="sxs-lookup"><span data-stu-id="226f6-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="226f6-134">Поиск</span><span class="sxs-lookup"><span data-stu-id="226f6-134">Search</span></span>|<span data-ttu-id="226f6-135">строка</span><span class="sxs-lookup"><span data-stu-id="226f6-135">string</span></span>|<span data-ttu-id="226f6-136">Это свойство является устаревшим и не должно использоваться.</span><span class="sxs-lookup"><span data-stu-id="226f6-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="226f6-137">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="226f6-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="226f6-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="226f6-138">Next steps</span></span>
<span data-ttu-id="226f6-139">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="226f6-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>