---
title: "Шаблоны продуктов в службе управления API Azure | Документация Майкрософт"
description: "Сведения о настройке содержимого страниц продуктов на портале разработчика в службе управления API Azure."
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
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="31db8-103">Шаблоны продуктов в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="31db8-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="31db8-104">Служба управления API Azure позволяет настраивать содержимое страниц портала разработчика с помощью набора шаблонов.</span><span class="sxs-lookup"><span data-stu-id="31db8-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="31db8-105">С помощью этих шаблонов вы можете гибко настраивать содержимое страниц, используя синтаксис [DotLiquid](http://dotliquidmarkup.org/), любой удобный текстовый редактор, например [DotLiquid для разработчиков](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), и предоставленный набор локализованных [строковых ресурсов](api-management-template-resources.md#strings), [ресурсов глифов](api-management-template-resources.md#glyphs), а также [элементов управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="31db8-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="31db8-106">С помощью шаблонов в этом разделе вы сможете настроить содержимое страниц продуктов на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="31db8-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="31db8-107">Список продуктов</span><span class="sxs-lookup"><span data-stu-id="31db8-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="31db8-108">Продукт</span><span class="sxs-lookup"><span data-stu-id="31db8-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="31db8-109">Примеры стандартных шаблонов включены в следующую документацию, но могут в любой момент измениться, так как ведется постоянная работа по их улучшению.</span><span class="sxs-lookup"><span data-stu-id="31db8-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="31db8-110">Актуальные шаблоны по умолчанию можно просмотреть на портале разработчика, перейдя к требуемому отдельному шаблону.</span><span class="sxs-lookup"><span data-stu-id="31db8-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="31db8-111">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="31db8-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="31db8-112"><a name="ProductList"></a> Список продуктов</span><span class="sxs-lookup"><span data-stu-id="31db8-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="31db8-113">Шаблон **списка продуктов** позволяет настроить текст страницы со списком продуктов на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="31db8-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="31db8-114">![Список продуктов](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="31db8-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="31db8-115">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="31db8-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="31db8-116">Управление</span><span class="sxs-lookup"><span data-stu-id="31db8-116">Controls</span></span>  
 <span data-ttu-id="31db8-117">В шаблоне `Product list` можно использовать следующие [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="31db8-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="31db8-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="31db8-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="31db8-119">search-control</span><span class="sxs-lookup"><span data-stu-id="31db8-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="31db8-120">Модель данных</span><span class="sxs-lookup"><span data-stu-id="31db8-120">Data model</span></span>  
  
|<span data-ttu-id="31db8-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="31db8-121">Property</span></span>|<span data-ttu-id="31db8-122">Тип</span><span class="sxs-lookup"><span data-stu-id="31db8-122">Type</span></span>|<span data-ttu-id="31db8-123">Описание</span><span class="sxs-lookup"><span data-stu-id="31db8-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="31db8-124">Разбиение по страницам</span><span class="sxs-lookup"><span data-stu-id="31db8-124">Paging</span></span>|<span data-ttu-id="31db8-125">Сущность [разбиения по страницам](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="31db8-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="31db8-126">Сведения о разбиении по страницам для коллекции продуктов.</span><span class="sxs-lookup"><span data-stu-id="31db8-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="31db8-127">Фильтрация</span><span class="sxs-lookup"><span data-stu-id="31db8-127">Filtering</span></span>|<span data-ttu-id="31db8-128">Сущность [фильтрации](api-management-template-data-model-reference.md#Filtering).</span><span class="sxs-lookup"><span data-stu-id="31db8-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="31db8-129">Сведения о фильтрации для страницы со списком продуктов.</span><span class="sxs-lookup"><span data-stu-id="31db8-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="31db8-130">Продукты</span><span class="sxs-lookup"><span data-stu-id="31db8-130">Products</span></span>|<span data-ttu-id="31db8-131">Коллекция сущностей [Продукт](api-management-template-data-model-reference.md#Product).</span><span class="sxs-lookup"><span data-stu-id="31db8-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="31db8-132">Все продукты, которые доступны для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="31db8-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="31db8-133">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="31db8-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="31db8-134"><a name="Product"></a> Продукт</span><span class="sxs-lookup"><span data-stu-id="31db8-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="31db8-135">Шаблон **продукта** позволяет настроить текст страницы со информацией о продукте на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="31db8-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="31db8-136">![Страница продукта на портале разработчика](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="31db8-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="31db8-137">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="31db8-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="31db8-138">Управление</span><span class="sxs-lookup"><span data-stu-id="31db8-138">Controls</span></span>  
 <span data-ttu-id="31db8-139">В шаблоне `Product list` можно использовать следующие [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="31db8-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="31db8-140">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="31db8-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="31db8-141">Модель данных</span><span class="sxs-lookup"><span data-stu-id="31db8-141">Data model</span></span>  
  
|<span data-ttu-id="31db8-142">Свойство</span><span class="sxs-lookup"><span data-stu-id="31db8-142">Property</span></span>|<span data-ttu-id="31db8-143">Тип</span><span class="sxs-lookup"><span data-stu-id="31db8-143">Type</span></span>|<span data-ttu-id="31db8-144">Описание</span><span class="sxs-lookup"><span data-stu-id="31db8-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="31db8-145">Продукт</span><span class="sxs-lookup"><span data-stu-id="31db8-145">Product</span></span>|[<span data-ttu-id="31db8-146">Продукт</span><span class="sxs-lookup"><span data-stu-id="31db8-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="31db8-147">Выбранный продукт.</span><span class="sxs-lookup"><span data-stu-id="31db8-147">The specified product.</span></span>|  
|<span data-ttu-id="31db8-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="31db8-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="31db8-149">Логическое</span><span class="sxs-lookup"><span data-stu-id="31db8-149">boolean</span></span>|<span data-ttu-id="31db8-150">Указывает, подписан ли текущий пользователь на этот продукт.</span><span class="sxs-lookup"><span data-stu-id="31db8-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="31db8-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="31db8-151">SubscriptionState</span></span>|<span data-ttu-id="31db8-152">number</span><span class="sxs-lookup"><span data-stu-id="31db8-152">number</span></span>|<span data-ttu-id="31db8-153">Состояние подписки.</span><span class="sxs-lookup"><span data-stu-id="31db8-153">The state of the subscription.</span></span> <span data-ttu-id="31db8-154">Возможны следующие состояния.</span><span class="sxs-lookup"><span data-stu-id="31db8-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="31db8-155">—-    `0 - suspended`: подписка заблокирована, и подписчик не может вызвать ни один API продукта.</span><span class="sxs-lookup"><span data-stu-id="31db8-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="31db8-156">— -   `1 - active`: подписка активна.</span><span class="sxs-lookup"><span data-stu-id="31db8-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="31db8-157">— -   `2 - expired`: срок действия подписки истек, и она была деактивирована.</span><span class="sxs-lookup"><span data-stu-id="31db8-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="31db8-158">— -   `3 - submitted`: запрос разработчика на подписку выполнен, но еще не был утвержден или отклонен.</span><span class="sxs-lookup"><span data-stu-id="31db8-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="31db8-159">—-    `4 - rejected`: администратор отклонил запрос на подписку.</span><span class="sxs-lookup"><span data-stu-id="31db8-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="31db8-160">-   `5 - cancelled`: подписка отменена разработчиком или администратором.</span><span class="sxs-lookup"><span data-stu-id="31db8-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="31db8-161">Ограничения</span><span class="sxs-lookup"><span data-stu-id="31db8-161">Limits</span></span>|<span data-ttu-id="31db8-162">array</span><span class="sxs-lookup"><span data-stu-id="31db8-162">array</span></span>|<span data-ttu-id="31db8-163">Это свойство является устаревшим и не должно использоваться.</span><span class="sxs-lookup"><span data-stu-id="31db8-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="31db8-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="31db8-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="31db8-165">Логическое</span><span class="sxs-lookup"><span data-stu-id="31db8-165">boolean</span></span>|<span data-ttu-id="31db8-166">Указывает, включено ли [делегирование](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) для этой подписки.</span><span class="sxs-lookup"><span data-stu-id="31db8-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="31db8-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="31db8-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="31db8-168">строка</span><span class="sxs-lookup"><span data-stu-id="31db8-168">string</span></span>|<span data-ttu-id="31db8-169">Если делегирование включено, содержит URL-адрес делегированной подписки.</span><span class="sxs-lookup"><span data-stu-id="31db8-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="31db8-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="31db8-170">IsAgreed</span></span>|<span data-ttu-id="31db8-171">Логическое</span><span class="sxs-lookup"><span data-stu-id="31db8-171">boolean</span></span>|<span data-ttu-id="31db8-172">Указывает, принял ли текущий пользователь условия использования продукта, если они определены.</span><span class="sxs-lookup"><span data-stu-id="31db8-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="31db8-173">Подписки</span><span class="sxs-lookup"><span data-stu-id="31db8-173">Subscriptions</span></span>|<span data-ttu-id="31db8-174">Коллекция сущностей [Сводка по подписке](api-management-template-data-model-reference.md#SubscriptionSummary).</span><span class="sxs-lookup"><span data-stu-id="31db8-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="31db8-175">Подписки на продукт.</span><span class="sxs-lookup"><span data-stu-id="31db8-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="31db8-176">Apis</span><span class="sxs-lookup"><span data-stu-id="31db8-176">Apis</span></span>|<span data-ttu-id="31db8-177">Коллекция сущностей [API](api-management-template-data-model-reference.md#API).</span><span class="sxs-lookup"><span data-stu-id="31db8-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="31db8-178">API-интерфейсы, существующие для этого продукта.</span><span class="sxs-lookup"><span data-stu-id="31db8-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="31db8-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="31db8-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="31db8-180">Логическое</span><span class="sxs-lookup"><span data-stu-id="31db8-180">boolean</span></span>|<span data-ttu-id="31db8-181">Определяет, имеет ли текущий пользователь право подписаться на этот продукт в контексте лимита подписки.</span><span class="sxs-lookup"><span data-stu-id="31db8-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="31db8-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="31db8-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="31db8-183">Логическое</span><span class="sxs-lookup"><span data-stu-id="31db8-183">boolean</span></span>|<span data-ttu-id="31db8-184">Определяет, имеет ли текущий пользователь право подписаться на этот продукт в контексте допустимости нескольких подписок.</span><span class="sxs-lookup"><span data-stu-id="31db8-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="31db8-185">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="31db8-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="31db8-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31db8-186">Next steps</span></span>
<span data-ttu-id="31db8-187">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="31db8-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>