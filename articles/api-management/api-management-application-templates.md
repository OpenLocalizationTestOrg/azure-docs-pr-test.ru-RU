---
title: "шаблоны aaaApplication в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toocustomize hello содержимое страницы приложения hello hello портал разработчиков в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="cb892-103">Шаблоны приложений в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="cb892-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="cb892-104">Управления API Azure предоставляет hello возможность toocustomize hello содержимое страницы портала разработчиков с помощью набора шаблонов, которые настраивают их содержимого.</span><span class="sxs-lookup"><span data-stu-id="cb892-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="cb892-105">С помощью [DotLiquid](http://dotliquidmarkup.org/) синтаксис и hello редактора, таких как [DotLiquid для конструкторов](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), предоставленным набором локализации и [строковые ресурсы](api-management-template-resources.md#strings), [ Ресурсы глиф](api-management-template-resources.md#glyphs), и [страницы элементов управления](api-management-page-controls.md), у вас есть гибкость tooconfigure hello содержимого hello страниц по своему усмотрению, с помощью этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="cb892-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="cb892-106">шаблоны Hello в этом разделе позволяют toocustomize hello содержимое страницы приложения hello на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="cb892-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="cb892-107">Список приложений</span><span class="sxs-lookup"><span data-stu-id="cb892-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="cb892-108">Приложения</span><span class="sxs-lookup"><span data-stu-id="cb892-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="cb892-109">Примеры шаблонов по умолчанию включены в следующие документации hello, но являются toochange субъекта из-за toocontinuous улучшения.</span><span class="sxs-lookup"><span data-stu-id="cb892-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="cb892-110">Можно просмотреть шаблоны динамической по умолчанию hello в портал разработчиков hello, перейдя по toohello требуемого отдельных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="cb892-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="cb892-111">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="cb892-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="cb892-112"><a name="ProductList"></a> Список приложений</span><span class="sxs-lookup"><span data-stu-id="cb892-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="cb892-113">Hello **список приложений** шаблон позволяет текст hello toocustomize страницу списка приложения hello на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="cb892-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="cb892-114">![Шаблоны портала разработчиков для страницы со списком приложений](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM шаблонов портала разработчиков для страницы со списком приложений")</span><span class="sxs-lookup"><span data-stu-id="cb892-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="cb892-115">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="cb892-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="cb892-116">Управление</span><span class="sxs-lookup"><span data-stu-id="cb892-116">Controls</span></span>  
 <span data-ttu-id="cb892-117">Hello `Product list` шаблона может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="cb892-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="cb892-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="cb892-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="cb892-119">Модель данных</span><span class="sxs-lookup"><span data-stu-id="cb892-119">Data model</span></span>  
  
|<span data-ttu-id="cb892-120">Свойство</span><span class="sxs-lookup"><span data-stu-id="cb892-120">Property</span></span>|<span data-ttu-id="cb892-121">Тип</span><span class="sxs-lookup"><span data-stu-id="cb892-121">Type</span></span>|<span data-ttu-id="cb892-122">Описание</span><span class="sxs-lookup"><span data-stu-id="cb892-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="cb892-123">Разбиение по страницам</span><span class="sxs-lookup"><span data-stu-id="cb892-123">Paging</span></span>|<span data-ttu-id="cb892-124">Сущность [разбиения по страницам](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="cb892-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="cb892-125">сведения о Hello разбиения на страницы для коллекции приложения hello.</span><span class="sxs-lookup"><span data-stu-id="cb892-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="cb892-126">Приложения</span><span class="sxs-lookup"><span data-stu-id="cb892-126">Applications</span></span>|<span data-ttu-id="cb892-127">Коллекция сущностей [Application](api-management-template-data-model-reference.md#Application) (Приложение).</span><span class="sxs-lookup"><span data-stu-id="cb892-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="cb892-128">Hello приложений отображается toohello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="cb892-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="cb892-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="cb892-129">CategoryName</span></span>|<span data-ttu-id="cb892-130">string</span><span class="sxs-lookup"><span data-stu-id="cb892-130">string</span></span>|<span data-ttu-id="cb892-131">Категория приложения Hello.</span><span class="sxs-lookup"><span data-stu-id="cb892-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="cb892-132">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="cb892-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="cb892-133"><a name="Application"></a> Приложение</span><span class="sxs-lookup"><span data-stu-id="cb892-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="cb892-134">Hello **приложения** шаблон позволяет текст hello toocustomize hello страницы приложения на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="cb892-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="cb892-135">![Шаблоны портала разработчиков для страницы приложения](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM шаблонов портала разработчиков для страницы приложения")</span><span class="sxs-lookup"><span data-stu-id="cb892-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="cb892-136">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="cb892-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="cb892-137">Управление</span><span class="sxs-lookup"><span data-stu-id="cb892-137">Controls</span></span>  
 <span data-ttu-id="cb892-138">Hello `Application` шаблона не позволяет использовать hello любого [страницы элементов управления](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="cb892-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="cb892-139">Модель данных</span><span class="sxs-lookup"><span data-stu-id="cb892-139">Data model</span></span>  
 <span data-ttu-id="cb892-140">Сущность [приложения](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="cb892-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="cb892-141">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="cb892-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="cb892-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb892-142">Next steps</span></span>
<span data-ttu-id="cb892-143">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cb892-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
