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
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="12c34-103">Шаблоны продуктов в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="12c34-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="12c34-104">Управления API Azure предоставляет hello возможность toocustomize hello содержимое страницы портала разработчиков с помощью набора шаблонов, которые настраивают их содержимого.</span><span class="sxs-lookup"><span data-stu-id="12c34-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="12c34-105">С помощью [DotLiquid](http://dotliquidmarkup.org/) синтаксис и hello редактора, таких как [DotLiquid для конструкторов](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), предоставленным набором локализации и [строковые ресурсы](api-management-template-resources.md#strings), [ Ресурсы глиф](api-management-template-resources.md#glyphs), и [страницы элементов управления](api-management-page-controls.md), у вас есть гибкость tooconfigure hello содержимого hello страниц по своему усмотрению, с помощью этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="12c34-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="12c34-106">шаблоны Hello в этом разделе разрешить доступ к содержимому hello toocustomize hello продукта страниц на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="12c34-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="12c34-107">Список продуктов</span><span class="sxs-lookup"><span data-stu-id="12c34-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="12c34-108">Продукт</span><span class="sxs-lookup"><span data-stu-id="12c34-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="12c34-109">Примеры шаблонов по умолчанию включены в следующие документации hello, но являются toochange субъекта из-за toocontinuous улучшения.</span><span class="sxs-lookup"><span data-stu-id="12c34-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="12c34-110">Можно просмотреть шаблоны динамической по умолчанию hello в портал разработчиков hello, перейдя по toohello требуемого отдельных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="12c34-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="12c34-111">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="12c34-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="12c34-112"><a name="ProductList"></a> Список продуктов</span><span class="sxs-lookup"><span data-stu-id="12c34-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="12c34-113">Hello **список продуктов** шаблон позволяет toocustomize текст hello hello страницу списка продуктов на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="12c34-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="12c34-114">![Список продуктов](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="12c34-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="12c34-115">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="12c34-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="12c34-116">Управление</span><span class="sxs-lookup"><span data-stu-id="12c34-116">Controls</span></span>  
 <span data-ttu-id="12c34-117">Hello `Product list` шаблона может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="12c34-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="12c34-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="12c34-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="12c34-119">search-control</span><span class="sxs-lookup"><span data-stu-id="12c34-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="12c34-120">Модель данных</span><span class="sxs-lookup"><span data-stu-id="12c34-120">Data model</span></span>  
  
|<span data-ttu-id="12c34-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="12c34-121">Property</span></span>|<span data-ttu-id="12c34-122">Тип</span><span class="sxs-lookup"><span data-stu-id="12c34-122">Type</span></span>|<span data-ttu-id="12c34-123">Описание</span><span class="sxs-lookup"><span data-stu-id="12c34-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="12c34-124">Разбиение по страницам</span><span class="sxs-lookup"><span data-stu-id="12c34-124">Paging</span></span>|<span data-ttu-id="12c34-125">Сущность [разбиения по страницам](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="12c34-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="12c34-126">сведения о Hello разбиения на страницы для hello коллекции продуктов.</span><span class="sxs-lookup"><span data-stu-id="12c34-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="12c34-127">Фильтрация</span><span class="sxs-lookup"><span data-stu-id="12c34-127">Filtering</span></span>|<span data-ttu-id="12c34-128">Сущность [фильтрации](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="12c34-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="12c34-129">Здравствуйте, фильтрации данных для списка продуктов hello страницы.</span><span class="sxs-lookup"><span data-stu-id="12c34-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="12c34-130">Продукты</span><span class="sxs-lookup"><span data-stu-id="12c34-130">Products</span></span>|<span data-ttu-id="12c34-131">Коллекция сущностей [Продукт](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="12c34-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="12c34-132">Hello продуктов видимым toohello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="12c34-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="12c34-133">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="12c34-133">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="12c34-134"><a name="Product"></a> Продукт</span><span class="sxs-lookup"><span data-stu-id="12c34-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="12c34-135">Hello **продукта** шаблон позволяет текст hello toocustomize продукта страницы приветствия на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="12c34-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="12c34-136">![Страница продукта на портале разработчика](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="12c34-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="12c34-137">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="12c34-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="12c34-138">Управление</span><span class="sxs-lookup"><span data-stu-id="12c34-138">Controls</span></span>  
 <span data-ttu-id="12c34-139">Hello `Product list` шаблона может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="12c34-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="12c34-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="12c34-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="12c34-141">Модель данных</span><span class="sxs-lookup"><span data-stu-id="12c34-141">Data model</span></span>  
  
|<span data-ttu-id="12c34-142">Свойство</span><span class="sxs-lookup"><span data-stu-id="12c34-142">Property</span></span>|<span data-ttu-id="12c34-143">Тип</span><span class="sxs-lookup"><span data-stu-id="12c34-143">Type</span></span>|<span data-ttu-id="12c34-144">Описание</span><span class="sxs-lookup"><span data-stu-id="12c34-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="12c34-145">Продукт</span><span class="sxs-lookup"><span data-stu-id="12c34-145">Product</span></span>|[<span data-ttu-id="12c34-146">Продукт</span><span class="sxs-lookup"><span data-stu-id="12c34-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="12c34-147">Hello указанного продукта.</span><span class="sxs-lookup"><span data-stu-id="12c34-147">hello specified product.</span></span>|  
|<span data-ttu-id="12c34-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="12c34-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="12c34-149">Логическое</span><span class="sxs-lookup"><span data-stu-id="12c34-149">boolean</span></span>|<span data-ttu-id="12c34-150">Является ли текущий пользователь hello подписанных toothis продукта.</span><span class="sxs-lookup"><span data-stu-id="12c34-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="12c34-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="12c34-151">SubscriptionState</span></span>|<span data-ttu-id="12c34-152">number</span><span class="sxs-lookup"><span data-stu-id="12c34-152">number</span></span>|<span data-ttu-id="12c34-153">Состояние подписки hello Hello.</span><span class="sxs-lookup"><span data-stu-id="12c34-153">hello state of hello subscription.</span></span> <span data-ttu-id="12c34-154">Возможны следующие состояния.</span><span class="sxs-lookup"><span data-stu-id="12c34-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="12c34-155">-   `0 - suspended`— hello подписки заблокирован, и подписчик hello не может вызывать API продуктов hello.</span><span class="sxs-lookup"><span data-stu-id="12c34-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="12c34-156">-   `1 - active`— hello подписка активна.</span><span class="sxs-lookup"><span data-stu-id="12c34-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="12c34-157">-   `2 - expired`— Подписка hello достигнут датой истечения срока действия и было отключено.</span><span class="sxs-lookup"><span data-stu-id="12c34-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="12c34-158">-   `3 - submitted`— запрос подписки hello, сделал developer Привет, но еще не был утвержден или отклонен.</span><span class="sxs-lookup"><span data-stu-id="12c34-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="12c34-159">-   `4 - rejected`— отклонил запрос подписки hello администратором.</span><span class="sxs-lookup"><span data-stu-id="12c34-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="12c34-160">-   `5 - cancelled`— hello разработчик или администратор отменили подписку hello.</span><span class="sxs-lookup"><span data-stu-id="12c34-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="12c34-161">Ограничения</span><span class="sxs-lookup"><span data-stu-id="12c34-161">Limits</span></span>|<span data-ttu-id="12c34-162">array</span><span class="sxs-lookup"><span data-stu-id="12c34-162">array</span></span>|<span data-ttu-id="12c34-163">Это свойство является устаревшим и не должно использоваться.</span><span class="sxs-lookup"><span data-stu-id="12c34-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="12c34-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="12c34-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="12c34-165">Логическое</span><span class="sxs-lookup"><span data-stu-id="12c34-165">boolean</span></span>|<span data-ttu-id="12c34-166">Указывает, включено ли [делегирование](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) для этой подписки.</span><span class="sxs-lookup"><span data-stu-id="12c34-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="12c34-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="12c34-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="12c34-168">string</span><span class="sxs-lookup"><span data-stu-id="12c34-168">string</span></span>|<span data-ttu-id="12c34-169">Если включено делегирование, hello делегированных URL-адрес подписки.</span><span class="sxs-lookup"><span data-stu-id="12c34-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="12c34-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="12c34-170">IsAgreed</span></span>|<span data-ttu-id="12c34-171">Логическое</span><span class="sxs-lookup"><span data-stu-id="12c34-171">boolean</span></span>|<span data-ttu-id="12c34-172">Если продукт hello условия, ли текущий пользователь hello согласованное toohello условия.</span><span class="sxs-lookup"><span data-stu-id="12c34-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="12c34-173">Подписки</span><span class="sxs-lookup"><span data-stu-id="12c34-173">Subscriptions</span></span>|<span data-ttu-id="12c34-174">Коллекция сущностей [Сводка по подписке](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="12c34-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="12c34-175">продукт toohello Hello подписок.</span><span class="sxs-lookup"><span data-stu-id="12c34-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="12c34-176">Apis</span><span class="sxs-lookup"><span data-stu-id="12c34-176">Apis</span></span>|<span data-ttu-id="12c34-177">коллекция сущностей [API](api-management-template-data-model-reference.md#API)</span><span class="sxs-lookup"><span data-stu-id="12c34-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="12c34-178">Здравствуйте, API-интерфейсы в этот продукт.</span><span class="sxs-lookup"><span data-stu-id="12c34-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="12c34-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="12c34-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="12c34-180">Логическое</span><span class="sxs-lookup"><span data-stu-id="12c34-180">boolean</span></span>|<span data-ttu-id="12c34-181">Является ли текущего пользователя hello подходящих toosubscribe toothis продукт с учета toohello подписки ограничение.</span><span class="sxs-lookup"><span data-stu-id="12c34-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="12c34-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="12c34-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="12c34-183">Логическое</span><span class="sxs-lookup"><span data-stu-id="12c34-183">boolean</span></span>|<span data-ttu-id="12c34-184">Право toosubscribe toothis продукт с учета toomultiple подписок или не является ли hello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="12c34-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="12c34-185">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="12c34-185">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="12c34-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12c34-186">Next steps</span></span>
<span data-ttu-id="12c34-187">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="12c34-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
