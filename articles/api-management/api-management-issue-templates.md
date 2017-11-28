---
title: "шаблоны aaaIssue в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toocustomize hello содержимого страниц проблема hello hello портал разработчиков в службе управления API Azure."
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
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="ac7ab-103">Шаблоны проблем в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="ac7ab-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="ac7ab-104">Управления API Azure предоставляет hello возможность toocustomize hello содержимое страницы портала разработчиков с помощью набора шаблонов, которые настраивают их содержимого.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="ac7ab-105">С помощью [DotLiquid](http://dotliquidmarkup.org/) синтаксис и hello редактора, таких как [DotLiquid для конструкторов](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), предоставленным набором локализации и [строковые ресурсы](api-management-template-resources.md#strings), [ Ресурсы глиф](api-management-template-resources.md#glyphs), и [страницы элементов управления](api-management-page-controls.md), у вас есть гибкость tooconfigure hello содержимого hello страниц по своему усмотрению, с помощью этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="ac7ab-106">шаблоны Hello в этом разделе разрешить доступ к содержимому hello toocustomize страниц hello проблемы на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="ac7ab-107">Список проблем</span><span class="sxs-lookup"><span data-stu-id="ac7ab-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="ac7ab-108">Примеры шаблонов по умолчанию включены в следующие документации hello, но являются toochange субъекта из-за toocontinuous улучшения.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="ac7ab-109">Можно просмотреть шаблоны динамической по умолчанию hello в портал разработчиков hello, перейдя по toohello требуемого отдельных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="ac7ab-110">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ac7ab-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="ac7ab-111"><a name="IssueList"></a> Список проблем</span><span class="sxs-lookup"><span data-stu-id="ac7ab-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="ac7ab-112">Hello **список проблем** шаблон позволяет текст hello toocustomize страницу списка hello проблемы на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="ac7ab-113">![Список проблем на портале разработчика](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "список проблем на портале разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="ac7ab-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="ac7ab-114">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ac7ab-114">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="ac7ab-115">Управление</span><span class="sxs-lookup"><span data-stu-id="ac7ab-115">Controls</span></span>  
 <span data-ttu-id="ac7ab-116">Hello `Issue list` шаблона может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="ac7ab-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="ac7ab-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="ac7ab-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="ac7ab-118">Модель данных</span><span class="sxs-lookup"><span data-stu-id="ac7ab-118">Data model</span></span>  
  
|<span data-ttu-id="ac7ab-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="ac7ab-119">Property</span></span>|<span data-ttu-id="ac7ab-120">Тип</span><span class="sxs-lookup"><span data-stu-id="ac7ab-120">Type</span></span>|<span data-ttu-id="ac7ab-121">Описание</span><span class="sxs-lookup"><span data-stu-id="ac7ab-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="ac7ab-122">Проблемы</span><span class="sxs-lookup"><span data-stu-id="ac7ab-122">Issues</span></span>|<span data-ttu-id="ac7ab-123">Коллекция сущностей [проблем](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="ac7ab-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="ac7ab-124">Hello проблемы видимым toohello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="ac7ab-125">Разбиение по страницам</span><span class="sxs-lookup"><span data-stu-id="ac7ab-125">Paging</span></span>|<span data-ttu-id="ac7ab-126">Сущность [разбиения по страницам](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="ac7ab-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="ac7ab-127">сведения о Hello разбиения на страницы для коллекции приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="ac7ab-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="ac7ab-128">IsAuthenticated</span></span>|<span data-ttu-id="ac7ab-129">Логическое</span><span class="sxs-lookup"><span data-stu-id="ac7ab-129">boolean</span></span>|<span data-ttu-id="ac7ab-130">Является ли текущий пользователь hello портал разработчиков toohello вошедшего в систему.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="ac7ab-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="ac7ab-131">CanReportIssues</span></span>|<span data-ttu-id="ac7ab-132">Логическое</span><span class="sxs-lookup"><span data-stu-id="ac7ab-132">boolean</span></span>|<span data-ttu-id="ac7ab-133">Hello текущий пользователь имеет ли toofile разрешения проблемы.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="ac7ab-134">Поиск</span><span class="sxs-lookup"><span data-stu-id="ac7ab-134">Search</span></span>|<span data-ttu-id="ac7ab-135">строка</span><span class="sxs-lookup"><span data-stu-id="ac7ab-135">string</span></span>|<span data-ttu-id="ac7ab-136">Это свойство является устаревшим и не должно использоваться.</span><span class="sxs-lookup"><span data-stu-id="ac7ab-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="ac7ab-137">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="ac7ab-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
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

## <a name="next-steps"></a><span data-ttu-id="ac7ab-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac7ab-138">Next steps</span></span>
<span data-ttu-id="ac7ab-139">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ac7ab-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
