---
title: "элементов управления на странице управления API aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello страницы элементов управления, доступных для использования в шаблонах портала разработчиков в службе управления API Azure."
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
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="bbf87-103">Элементы управления страницей в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="bbf87-103">Azure API Management page controls</span></span>
<span data-ttu-id="bbf87-104">Управления API Azure предоставляет следующие элементы управления для использования в шаблонах портала разработчиков hello hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="bbf87-105">toouse элемент управления поместить его в расположение требуемого hello в шаблоне портала разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="bbf87-106">Некоторые элементы управления, такие как hello [действия приложения](#app-actions) управления, имеют параметры, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="bbf87-107">Hello значения для параметров hello передаются в составе hello модели данных для шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="bbf87-108">В большинстве случаев можно просто вставить в hello заданного пример для каждого элемента управления для него toowork правильно.</span><span class="sxs-lookup"><span data-stu-id="bbf87-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="bbf87-109">Дополнительные сведения о значениях параметра hello видно hello раздел модели данных для каждого шаблона, в котором можно будет использовать элемент управления.</span><span class="sxs-lookup"><span data-stu-id="bbf87-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="bbf87-110">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="bbf87-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="bbf87-111">Элементы управления страницей в шаблонах портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="bbf87-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="bbf87-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="bbf87-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="bbf87-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="bbf87-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="bbf87-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="bbf87-115">providers</span><span class="sxs-lookup"><span data-stu-id="bbf87-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="bbf87-116">search-control</span><span class="sxs-lookup"><span data-stu-id="bbf87-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="bbf87-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="bbf87-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="bbf87-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="bbf87-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="bbf87-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="bbf87-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="bbf87-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="bbf87-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="bbf87-121">Hello `app-actions` управления предоставляет пользовательский интерфейс для взаимодействия с приложениями на странице профиля пользователя hello на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="bbf87-122">![элемент управления действиями](./media/api-management-page-controls/APIM-app-actions-control.png "элемент управления действиями для APIM")</span><span class="sxs-lookup"><span data-stu-id="bbf87-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bbf87-123">Использование</span><span class="sxs-lookup"><span data-stu-id="bbf87-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="bbf87-124">Параметры</span><span class="sxs-lookup"><span data-stu-id="bbf87-124">Parameters</span></span>  
  
|<span data-ttu-id="bbf87-125">Параметр</span><span class="sxs-lookup"><span data-stu-id="bbf87-125">Parameter</span></span>|<span data-ttu-id="bbf87-126">Описание</span><span class="sxs-lookup"><span data-stu-id="bbf87-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="bbf87-127">appId</span><span class="sxs-lookup"><span data-stu-id="bbf87-127">appId</span></span>|<span data-ttu-id="bbf87-128">Идентификатор приложения hello Hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="bbf87-129">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-129">Developer portal templates</span></span>  
 <span data-ttu-id="bbf87-130">Hello `app-actions` управления может быть использована для hello следующие шаблоны портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="bbf87-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="bbf87-131">Приложения</span><span class="sxs-lookup"><span data-stu-id="bbf87-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="bbf87-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="bbf87-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="bbf87-133">Hello `basic-signin` управления предоставляет элемент управления для сбора данных вход пользователя сведения в hello войти в портале разработчика hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="bbf87-134">![базовый элемент управления входом](./media/api-management-page-controls/APIM-basic-signin-control.png "базовый элемент управления входом для APIM")</span><span class="sxs-lookup"><span data-stu-id="bbf87-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bbf87-135">Использование</span><span class="sxs-lookup"><span data-stu-id="bbf87-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="bbf87-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="bbf87-136">Parameters</span></span>  
 <span data-ttu-id="bbf87-137">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bbf87-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="bbf87-138">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-138">Developer portal templates</span></span>  
 <span data-ttu-id="bbf87-139">Hello `basic-signin` управления может быть использована для hello следующие шаблоны портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="bbf87-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="bbf87-140">Вход</span><span class="sxs-lookup"><span data-stu-id="bbf87-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="bbf87-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="bbf87-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="bbf87-142">Hello `paging-control` предоставляет функциональные возможности для разбиения на страницы разработчика страницы портала, отображать список элементов.</span><span class="sxs-lookup"><span data-stu-id="bbf87-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="bbf87-143">![элемент управления разбиением по страницам ](./media/api-management-page-controls/APIM-paging-control.png "элемент управления разбиением по страницам для APIM")</span><span class="sxs-lookup"><span data-stu-id="bbf87-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bbf87-144">Использование</span><span class="sxs-lookup"><span data-stu-id="bbf87-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="bbf87-145">Параметры</span><span class="sxs-lookup"><span data-stu-id="bbf87-145">Parameters</span></span>  
 <span data-ttu-id="bbf87-146">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bbf87-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="bbf87-147">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-147">Developer portal templates</span></span>  
 <span data-ttu-id="bbf87-148">Hello `paging-control` управления может быть использована для hello следующие шаблоны портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="bbf87-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="bbf87-149">Список API</span><span class="sxs-lookup"><span data-stu-id="bbf87-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="bbf87-150">Список проблем</span><span class="sxs-lookup"><span data-stu-id="bbf87-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="bbf87-151">Список продуктов</span><span class="sxs-lookup"><span data-stu-id="bbf87-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="bbf87-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="bbf87-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="bbf87-153">Hello `providers` управления предоставляет элемент управления для выбора поставщиков проверки подлинности в hello входа в портал разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="bbf87-154">![Элемент управления поставщиками](./media/api-management-page-controls/APIM-providers-control.png "Элемент управления поставщиками для APIM")</span><span class="sxs-lookup"><span data-stu-id="bbf87-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bbf87-155">Использование</span><span class="sxs-lookup"><span data-stu-id="bbf87-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="bbf87-156">Параметры</span><span class="sxs-lookup"><span data-stu-id="bbf87-156">Parameters</span></span>  
 <span data-ttu-id="bbf87-157">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bbf87-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="bbf87-158">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-158">Developer portal templates</span></span>  
 <span data-ttu-id="bbf87-159">Hello `providers` управления может быть использована для hello следующие шаблоны портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="bbf87-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="bbf87-160">Вход</span><span class="sxs-lookup"><span data-stu-id="bbf87-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="bbf87-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="bbf87-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="bbf87-162">Hello `search-control` предоставляет функциональные возможности поиска разработчика страницы портала, отображать список элементов.</span><span class="sxs-lookup"><span data-stu-id="bbf87-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="bbf87-163">![Элемент управления поиском](./media/api-management-page-controls/APIM-search-control.png "Элемент управления поиском для APIM")</span><span class="sxs-lookup"><span data-stu-id="bbf87-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bbf87-164">Использование</span><span class="sxs-lookup"><span data-stu-id="bbf87-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="bbf87-165">Параметры</span><span class="sxs-lookup"><span data-stu-id="bbf87-165">Parameters</span></span>  
 <span data-ttu-id="bbf87-166">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bbf87-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="bbf87-167">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-167">Developer portal templates</span></span>  
 <span data-ttu-id="bbf87-168">Hello `search-control` управления может быть использована для hello следующие шаблоны портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="bbf87-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="bbf87-169">Список API</span><span class="sxs-lookup"><span data-stu-id="bbf87-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="bbf87-170">Список продуктов</span><span class="sxs-lookup"><span data-stu-id="bbf87-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="bbf87-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="bbf87-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="bbf87-172">Hello `sign-up` управления предоставляет элемент управления для сбора данных профиля пользователя в страницу на портале разработчиков hello регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="bbf87-173">![Элемент управления регистрацией](./media/api-management-page-controls/APIM-sign-up-control.png "Элемент управления регистрацией для APIM")</span><span class="sxs-lookup"><span data-stu-id="bbf87-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bbf87-174">Использование</span><span class="sxs-lookup"><span data-stu-id="bbf87-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="bbf87-175">Параметры</span><span class="sxs-lookup"><span data-stu-id="bbf87-175">Parameters</span></span>  
 <span data-ttu-id="bbf87-176">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bbf87-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="bbf87-177">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-177">Developer portal templates</span></span>  
 <span data-ttu-id="bbf87-178">Hello `sign-up` управления может быть использована для hello следующие шаблоны портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="bbf87-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="bbf87-179">Регистрация</span><span class="sxs-lookup"><span data-stu-id="bbf87-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="bbf87-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="bbf87-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="bbf87-181">Hello `subscribe-button` предоставляет элемент управления для подписки пользователя tooa продукта.</span><span class="sxs-lookup"><span data-stu-id="bbf87-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="bbf87-182">![Элемент управления подпиской](./media/api-management-page-controls/APIM-subscribe-button-control.png "Элемент управления подпиской для APIM")</span><span class="sxs-lookup"><span data-stu-id="bbf87-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bbf87-183">Использование</span><span class="sxs-lookup"><span data-stu-id="bbf87-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="bbf87-184">Параметры</span><span class="sxs-lookup"><span data-stu-id="bbf87-184">Parameters</span></span>  
 <span data-ttu-id="bbf87-185">Отсутствует.</span><span class="sxs-lookup"><span data-stu-id="bbf87-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="bbf87-186">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-186">Developer portal templates</span></span>  
 <span data-ttu-id="bbf87-187">Hello `subscribe-button` управления может быть использована для hello следующие шаблоны портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="bbf87-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="bbf87-188">Продукт</span><span class="sxs-lookup"><span data-stu-id="bbf87-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="bbf87-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="bbf87-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="bbf87-190">Hello `subscription-cancel` управления предоставляет элемент управления для отмены подписки tooa продукт в hello страницу профиля пользователя на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="bbf87-191">![Элемент управления отменой подписки](./media/api-management-page-controls/APIM-subscription-cancel-control.png "Элемент управления отменой подписки для APIM")</span><span class="sxs-lookup"><span data-stu-id="bbf87-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="bbf87-192">Использование</span><span class="sxs-lookup"><span data-stu-id="bbf87-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="bbf87-193">Параметры</span><span class="sxs-lookup"><span data-stu-id="bbf87-193">Parameters</span></span>  
  
|<span data-ttu-id="bbf87-194">Параметр</span><span class="sxs-lookup"><span data-stu-id="bbf87-194">Parameter</span></span>|<span data-ttu-id="bbf87-195">Описание</span><span class="sxs-lookup"><span data-stu-id="bbf87-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="bbf87-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="bbf87-196">subscriptionId</span></span>|<span data-ttu-id="bbf87-197">идентификатор подписки toocancel hello Hello.</span><span class="sxs-lookup"><span data-stu-id="bbf87-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="bbf87-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="bbf87-198">cancelUrl</span></span>|<span data-ttu-id="bbf87-199">Подписка Hello отменить URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="bbf87-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="bbf87-200">Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="bbf87-200">Developer portal templates</span></span>  
 <span data-ttu-id="bbf87-201">Hello `subscription-cancel` управления может быть использована для hello следующие шаблоны портала разработчиков.</span><span class="sxs-lookup"><span data-stu-id="bbf87-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="bbf87-202">Продукт</span><span class="sxs-lookup"><span data-stu-id="bbf87-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="bbf87-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bbf87-203">Next steps</span></span>
<span data-ttu-id="bbf87-204">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bbf87-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
