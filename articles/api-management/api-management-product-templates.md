---
title: "шаблоны aaaProduct в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как содержимое hello toocustomize продукта hello страниц в портал разработчика управления API Azure hello."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a>Шаблоны продуктов в службе управления API Azure
Управления API Azure предоставляет hello возможность toocustomize hello содержимое страницы портала разработчиков с помощью набора шаблонов, которые настраивают их содержимого. С помощью [DotLiquid](http://dotliquidmarkup.org/) синтаксис и hello редактора, таких как [DotLiquid для конструкторов](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), предоставленным набором локализации и [строковые ресурсы](api-management-template-resources.md#strings), [ Ресурсы глиф](api-management-template-resources.md#glyphs), и [страницы элементов управления](api-management-page-controls.md), у вас есть гибкость tooconfigure hello содержимого hello страниц по своему усмотрению, с помощью этих шаблонов.  
  
 шаблоны Hello в этом разделе разрешить доступ к содержимому hello toocustomize hello продукта страниц на портале разработчиков hello.  
  
-   [Список продуктов](#ProductList)  
  
-   [Продукт](#Product)  
  
> [!NOTE]
>  Примеры шаблонов по умолчанию включены в следующие документации hello, но являются toochange субъекта из-за toocontinuous улучшения. Можно просмотреть шаблоны динамической по умолчанию hello в портал разработчиков hello, перейдя по toohello требуемого отдельных шаблонов. Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="ProductList"></a> Список продуктов  
 Hello **список продуктов** шаблон позволяет toocustomize текст hello hello страницу списка продуктов на портале разработчиков hello.  
  
 ![Список продуктов](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>Шаблон по умолчанию  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
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
  
### <a name="controls"></a>Управление  
 Hello `Product list` шаблона может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).  
  
-   [paging-control](api-management-page-controls.md#paging-control)  
  
-   [search-control](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>Модель данных  
  
|Свойство|Тип|Описание|  
|--------------|----------|-----------------|  
|Разбиение по страницам|Сущность [разбиения по страницам](api-management-template-data-model-reference.md#Paging).|сведения о Hello разбиения на страницы для hello коллекции продуктов.|  
|Фильтрация|Сущность [фильтрации](api-management-template-data-model-reference.md#Filtering).|Здравствуйте, фильтрации данных для списка продуктов hello страницы.|  
|Продукты|Коллекция сущностей [Продукт](api-management-template-data-model-reference.md#Product).|Hello продуктов видимым toohello текущего пользователя.|  
  
### <a name="sample-template-data"></a>Пример данных шаблона  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <a name="Product"></a> Продукт  
 Hello **продукта** шаблон позволяет текст hello toocustomize продукта страницы приветствия на портале разработчиков hello.  
  
 ![Страница продукта на портале разработчика](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>Шаблон по умолчанию  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a>Управление  
 Hello `Product list` шаблона может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).  
  
-   [subscribe-button](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>Модель данных  
  
|Свойство|Тип|Описание|  
|--------------|----------|-----------------|  
|Продукт|[Продукт](api-management-template-data-model-reference.md#Product)|Hello указанного продукта.|  
|IsDeveloperSubscribed|Логическое|Является ли текущий пользователь hello подписанных toothis продукта.|  
|SubscriptionState|number|Состояние подписки hello Hello. Возможны следующие состояния.<br /><br /> -   `0 - suspended`— hello подписки заблокирован, и подписчик hello не может вызывать API продуктов hello.<br />-   `1 - active`— hello подписка активна.<br />-   `2 - expired`— Подписка hello достигнут датой истечения срока действия и было отключено.<br />-   `3 - submitted`— запрос подписки hello, сделал developer Привет, но еще не был утвержден или отклонен.<br />-   `4 - rejected`— отклонил запрос подписки hello администратором.<br />-   `5 - cancelled`— hello разработчик или администратор отменили подписку hello.|  
|Ограничения|array|Это свойство является устаревшим и не должно использоваться.|  
|DelegatedSubscriptionEnabled|Логическое|Указывает, включено ли [делегирование](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) для этой подписки.|  
|DelegatedSubscriptionUrl|string|Если включено делегирование, hello делегированных URL-адрес подписки.|  
|IsAgreed|Логическое|Если продукт hello условия, ли текущий пользователь hello согласованное toohello условия.|  
|Подписки|Коллекция сущностей [Сводка по подписке](api-management-template-data-model-reference.md#SubscriptionSummary).|продукт toohello Hello подписок.|  
|Apis|коллекция сущностей [API](api-management-template-data-model-reference.md#API)|Здравствуйте, API-интерфейсы в этот продукт.|  
|CannotAddBecauseSubscriptionNumberLimitReached|Логическое|Является ли текущего пользователя hello подходящих toosubscribe toothis продукт с учета toohello подписки ограничение.|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|Логическое|Право toosubscribe toothis продукт с учета toomultiple подписок или не является ли hello текущего пользователя.|  
  
### <a name="sample-template-data"></a>Пример данных шаблона  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).
