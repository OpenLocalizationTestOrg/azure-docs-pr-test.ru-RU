---
title: "Элементы управления страницей в службе управления API Azure | Документация Майкрософт"
description: "Сведения об элементах управления страницей, доступных для использования в шаблонах портала разработчика в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="cc294-103">Элементы управления страницей в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="cc294-103">Azure API Management page controls</span></span>
<span data-ttu-id="cc294-104">Служба управления API Azure предоставляет следующие элементы управления страницей для использования в шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="cc294-105">Чтобы применить элемент управления, поместите его в нужное место шаблона портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="cc294-106">Некоторые элементы управления имеют параметры, как например [app-actions](#app-actions), представленный в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="cc294-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="cc294-107">Значения для этих параметров передаются в составе модели данных для шаблона.</span><span class="sxs-lookup"><span data-stu-id="cc294-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="cc294-108">В большинстве случаев достаточно просто скопировать представленный пример для элемента управления, и он сразу будет правильно работать.</span><span class="sxs-lookup"><span data-stu-id="cc294-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="cc294-109">Дополнительные сведения о значениях параметров вы найдете в разделе модели данных для каждого шаблона, в котором можно использовать соответствующий элемент управления.</span><span class="sxs-lookup"><span data-stu-id="cc294-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="cc294-110">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="cc294-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="cc294-111">Элементы управления страницей в шаблонах портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="cc294-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="cc294-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="cc294-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="cc294-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="cc294-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="cc294-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="cc294-115">providers</span><span class="sxs-lookup"><span data-stu-id="cc294-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="cc294-116">search-control</span><span class="sxs-lookup"><span data-stu-id="cc294-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="cc294-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="cc294-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="cc294-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="cc294-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="cc294-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="cc294-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="cc294-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="cc294-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="cc294-121">Элемент управления `app-actions` предоставляет пользовательский интерфейс для взаимодействия с приложениями на странице профиля пользователя на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="cc294-122">![элемент управления действиями](./media/api-management-page-controls/APIM-app-actions-control.png "элемент управления действиями для APIM")</span><span class="sxs-lookup"><span data-stu-id="cc294-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc294-123">Использование</span><span class="sxs-lookup"><span data-stu-id="cc294-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc294-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc294-124">Parameters</span></span>  
  
|<span data-ttu-id="cc294-125">Параметр</span><span class="sxs-lookup"><span data-stu-id="cc294-125">Parameter</span></span>|<span data-ttu-id="cc294-126">Описание</span><span class="sxs-lookup"><span data-stu-id="cc294-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="cc294-127">appId</span><span class="sxs-lookup"><span data-stu-id="cc294-127">appId</span></span>|<span data-ttu-id="cc294-128">Идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="cc294-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc294-129">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-129">Developer portal templates</span></span>  
 <span data-ttu-id="cc294-130">Элемент управления `app-actions` можно использовать в следующих шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc294-131">Приложения</span><span class="sxs-lookup"><span data-stu-id="cc294-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="cc294-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="cc294-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="cc294-133">Элемент управления `basic-signin` предоставляет интерфейс для получения учетных данных пользователя на странице входа на портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="cc294-134">![базовый элемент управления входом](./media/api-management-page-controls/APIM-basic-signin-control.png "базовый элемент управления входом для APIM")</span><span class="sxs-lookup"><span data-stu-id="cc294-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc294-135">Использование</span><span class="sxs-lookup"><span data-stu-id="cc294-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc294-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc294-136">Parameters</span></span>  
 <span data-ttu-id="cc294-137">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="cc294-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc294-138">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-138">Developer portal templates</span></span>  
 <span data-ttu-id="cc294-139">Элемент управления `basic-signin` можно использовать в следующих шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc294-140">Вход</span><span class="sxs-lookup"><span data-stu-id="cc294-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="cc294-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="cc294-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="cc294-142">Элемент `paging-control` предоставляет функцию разбиения по страницам, которую можно использовать на страницах со списками на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="cc294-143">![элемент управления разбиением по страницам ](./media/api-management-page-controls/APIM-paging-control.png "элемент управления разбиением по страницам для APIM")</span><span class="sxs-lookup"><span data-stu-id="cc294-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc294-144">Использование</span><span class="sxs-lookup"><span data-stu-id="cc294-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc294-145">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc294-145">Parameters</span></span>  
 <span data-ttu-id="cc294-146">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="cc294-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc294-147">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-147">Developer portal templates</span></span>  
 <span data-ttu-id="cc294-148">Элемент управления `paging-control` можно использовать в следующих шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc294-149">Список API</span><span class="sxs-lookup"><span data-stu-id="cc294-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="cc294-150">Список проблем</span><span class="sxs-lookup"><span data-stu-id="cc294-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="cc294-151">Список продуктов</span><span class="sxs-lookup"><span data-stu-id="cc294-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="cc294-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="cc294-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="cc294-153">Элемент управления `providers` предоставляет интерфейс для выбора поставщика проверки подлинности на странице входа на портал разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="cc294-154">![Элемент управления поставщиками](./media/api-management-page-controls/APIM-providers-control.png "Элемент управления поставщиками для APIM")</span><span class="sxs-lookup"><span data-stu-id="cc294-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc294-155">Использование</span><span class="sxs-lookup"><span data-stu-id="cc294-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc294-156">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc294-156">Parameters</span></span>  
 <span data-ttu-id="cc294-157">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="cc294-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc294-158">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-158">Developer portal templates</span></span>  
 <span data-ttu-id="cc294-159">Элемент управления `providers` можно использовать в следующих шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc294-160">Вход</span><span class="sxs-lookup"><span data-stu-id="cc294-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="cc294-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="cc294-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="cc294-162">Элемент `search-control` предоставляет функцию поиска, которую можно использовать на страницах со списками на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="cc294-163">![Элемент управления поиском](./media/api-management-page-controls/APIM-search-control.png "Элемент управления поиском для APIM")</span><span class="sxs-lookup"><span data-stu-id="cc294-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc294-164">Использование</span><span class="sxs-lookup"><span data-stu-id="cc294-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc294-165">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc294-165">Parameters</span></span>  
 <span data-ttu-id="cc294-166">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="cc294-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc294-167">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-167">Developer portal templates</span></span>  
 <span data-ttu-id="cc294-168">Элемент управления `search-control` можно использовать в следующих шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc294-169">Список API</span><span class="sxs-lookup"><span data-stu-id="cc294-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="cc294-170">Список продуктов</span><span class="sxs-lookup"><span data-stu-id="cc294-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="cc294-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="cc294-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="cc294-172">Элемент управления `sign-up` предоставляет интерфейс для получения информации о профиле пользователя на странице регистрации на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="cc294-173">![Элемент управления регистрацией](./media/api-management-page-controls/APIM-sign-up-control.png "Элемент управления регистрацией для APIM")</span><span class="sxs-lookup"><span data-stu-id="cc294-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc294-174">Использование</span><span class="sxs-lookup"><span data-stu-id="cc294-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc294-175">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc294-175">Parameters</span></span>  
 <span data-ttu-id="cc294-176">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="cc294-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc294-177">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-177">Developer portal templates</span></span>  
 <span data-ttu-id="cc294-178">Элемент управления `sign-up` можно использовать в следующих шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc294-179">Регистрация</span><span class="sxs-lookup"><span data-stu-id="cc294-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="cc294-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="cc294-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="cc294-181">Элемент `subscribe-button` предоставляет функцию оформления подписки пользователя на продукт.</span><span class="sxs-lookup"><span data-stu-id="cc294-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="cc294-182">![Элемент управления подпиской](./media/api-management-page-controls/APIM-subscribe-button-control.png "Элемент управления подпиской для APIM")</span><span class="sxs-lookup"><span data-stu-id="cc294-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc294-183">Использование</span><span class="sxs-lookup"><span data-stu-id="cc294-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc294-184">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc294-184">Parameters</span></span>  
 <span data-ttu-id="cc294-185">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="cc294-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc294-186">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-186">Developer portal templates</span></span>  
 <span data-ttu-id="cc294-187">Элемент управления `subscribe-button` можно использовать в следующих шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc294-188">Продукт</span><span class="sxs-lookup"><span data-stu-id="cc294-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="cc294-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="cc294-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="cc294-190">Элемент управления `subscription-cancel` предоставляет интерфейс для отмены подписки на продукт на странице профиля пользователя на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="cc294-191">![Элемент управления отменой подписки](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Элемент управления отменой подписки для APIM")</span><span class="sxs-lookup"><span data-stu-id="cc294-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="cc294-192">Использование</span><span class="sxs-lookup"><span data-stu-id="cc294-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="cc294-193">Параметры</span><span class="sxs-lookup"><span data-stu-id="cc294-193">Parameters</span></span>  
  
|<span data-ttu-id="cc294-194">Параметр</span><span class="sxs-lookup"><span data-stu-id="cc294-194">Parameter</span></span>|<span data-ttu-id="cc294-195">Описание</span><span class="sxs-lookup"><span data-stu-id="cc294-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="cc294-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cc294-196">subscriptionId</span></span>|<span data-ttu-id="cc294-197">Идентификатор подписки, которую следует отменить.</span><span class="sxs-lookup"><span data-stu-id="cc294-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="cc294-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="cc294-198">cancelUrl</span></span>|<span data-ttu-id="cc294-199">URL-адрес для отмены подписки.</span><span class="sxs-lookup"><span data-stu-id="cc294-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="cc294-200">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="cc294-200">Developer portal templates</span></span>  
 <span data-ttu-id="cc294-201">Элемент управления `subscription-cancel` можно использовать в следующих шаблонах портала разработчика.</span><span class="sxs-lookup"><span data-stu-id="cc294-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="cc294-202">Продукт</span><span class="sxs-lookup"><span data-stu-id="cc294-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="cc294-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc294-203">Next steps</span></span>
<span data-ttu-id="cc294-204">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cc294-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>