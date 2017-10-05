---
title: "Шаблоны портала разработчика в службе управления API Azure | Документация Майкрософт"
description: "Сведения о настройке содержимого страниц портала разработчика с использованием набора шаблонов в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 5189f3d8-2a4c-4dc8-ab19-11c7df0114d4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dc3f32a3cff2e66a798bd8f6c19c6b56a47643ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-developer-portal-templates"></a><span data-ttu-id="75a76-103">Шаблоны портала разработчика в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="75a76-103">Azure API Management Developer Portal Templates</span></span>
<span data-ttu-id="75a76-104">Служба управления API Azure позволяет настраивать содержимое страниц портала разработчика с помощью набора шаблонов.</span><span class="sxs-lookup"><span data-stu-id="75a76-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="75a76-105">С помощью синтаксиса [DotLiquid](http://dotliquidmarkup.org/), выбранного редактора, например [DotLiquid для разработчиков](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), и указанного набора локализованных [строковых ресурсов](api-management-template-resources.md#strings), [ресурсов глифов](api-management-template-resources.md#glyphs), а также [элементов управления на странице](api-management-page-controls.md) можно гибко настраивать содержимое страниц по своему усмотрению с использованием этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="75a76-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="75a76-106">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="75a76-106">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  



  
##  <span data-ttu-id="75a76-107"><a name="DeveloperPortalTemplates"></a>Шаблоны портала разработчика</span><span class="sxs-lookup"><span data-stu-id="75a76-107"><a name="DeveloperPortalTemplates"></a> Developer portal templates</span></span>  
  
-   [<span data-ttu-id="75a76-108">Интерфейсы API</span><span class="sxs-lookup"><span data-stu-id="75a76-108">APIs</span></span>](api-management-api-templates.md)  
    -   [<span data-ttu-id="75a76-109">Список API</span><span class="sxs-lookup"><span data-stu-id="75a76-109">API list</span></span>](api-management-api-templates.md#APIList)  
    -   [<span data-ttu-id="75a76-110">Операция</span><span class="sxs-lookup"><span data-stu-id="75a76-110">Operation</span></span>](api-management-api-templates.md#Product)  
    -   [<span data-ttu-id="75a76-111">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="75a76-111">Code samples</span></span>](api-management-api-templates.md#CodeSamples)  
        -   [<span data-ttu-id="75a76-112">Curl</span><span class="sxs-lookup"><span data-stu-id="75a76-112">Curl</span></span>](api-management-api-templates.md#Curl)  
        -   [<span data-ttu-id="75a76-113">C#</span><span class="sxs-lookup"><span data-stu-id="75a76-113">C#</span></span>](api-management-api-templates.md#CSharp)  
        -   [<span data-ttu-id="75a76-114">Java</span><span class="sxs-lookup"><span data-stu-id="75a76-114">Java</span></span>](api-management-api-templates.md#Stub)  
        -   [<span data-ttu-id="75a76-115">JavaScript</span><span class="sxs-lookup"><span data-stu-id="75a76-115">JavaScript</span></span>](api-management-api-templates.md#JavaScript)  
        -   [<span data-ttu-id="75a76-116">Objective C</span><span class="sxs-lookup"><span data-stu-id="75a76-116">Objective C</span></span>](api-management-api-templates.md#ObjectiveC)  
        -   [<span data-ttu-id="75a76-117">PHP</span><span class="sxs-lookup"><span data-stu-id="75a76-117">PHP</span></span>](api-management-api-templates.md#PHP)  
        -   [<span data-ttu-id="75a76-118">Python</span><span class="sxs-lookup"><span data-stu-id="75a76-118">Python</span></span>](api-management-api-templates.md#Python)  
        -   [<span data-ttu-id="75a76-119">Ruby</span><span class="sxs-lookup"><span data-stu-id="75a76-119">Ruby</span></span>](api-management-api-templates.md#Ruby)  
-   [<span data-ttu-id="75a76-120">Продукты</span><span class="sxs-lookup"><span data-stu-id="75a76-120">Products</span></span>](api-management-product-templates.md)  
    -   [<span data-ttu-id="75a76-121">Список продуктов</span><span class="sxs-lookup"><span data-stu-id="75a76-121">Product list</span></span>](api-management-product-templates.md#ProductList)  
    -   [<span data-ttu-id="75a76-122">Продукт</span><span class="sxs-lookup"><span data-stu-id="75a76-122">Product</span></span>](api-management-product-templates.md#Product)  
-   [<span data-ttu-id="75a76-123">Приложения</span><span class="sxs-lookup"><span data-stu-id="75a76-123">Applications</span></span>](api-management-application-templates.md)  
    -   [<span data-ttu-id="75a76-124">Список приложений</span><span class="sxs-lookup"><span data-stu-id="75a76-124">Application list</span></span>](api-management-application-templates.md#ProductList)  
    -   [<span data-ttu-id="75a76-125">Приложения</span><span class="sxs-lookup"><span data-stu-id="75a76-125">Application</span></span>](api-management-application-templates.md#Application)  
-   [<span data-ttu-id="75a76-126">Проблемы</span><span class="sxs-lookup"><span data-stu-id="75a76-126">Issues</span></span>](api-management-issue-templates.md)  
    -   [<span data-ttu-id="75a76-127">Список проблем</span><span class="sxs-lookup"><span data-stu-id="75a76-127">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
-   [<span data-ttu-id="75a76-128">Профиль пользователя</span><span class="sxs-lookup"><span data-stu-id="75a76-128">User Profile</span></span>](api-management-user-profile-templates.md)  
    -   [<span data-ttu-id="75a76-129">Профиль</span><span class="sxs-lookup"><span data-stu-id="75a76-129">Profile</span></span>](api-management-user-profile-templates.md#Profile)  
    -   <span data-ttu-id="75a76-130">[Подписки](api-management-user-profile-templates.md#Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="75a76-130">[Subscriptions](api-management-user-profile-templates.md#Subscriptions)</span></span>  
    -   <span data-ttu-id="75a76-131">[Приложения](api-management-user-profile-templates.md#Applications).</span><span class="sxs-lookup"><span data-stu-id="75a76-131">[Applications](api-management-user-profile-templates.md#Applications)</span></span>  
    -   [<span data-ttu-id="75a76-132">Обновить сведения об учетной записи</span><span class="sxs-lookup"><span data-stu-id="75a76-132">Update account info</span></span>](api-management-user-profile-templates.md#UpdateAccountInfo)  
-   [<span data-ttu-id="75a76-133">Страницы</span><span class="sxs-lookup"><span data-stu-id="75a76-133">Pages</span></span>](api-management-page-templates.md)  
    -   [<span data-ttu-id="75a76-134">Вход</span><span class="sxs-lookup"><span data-stu-id="75a76-134">Sign in</span></span>](api-management-page-templates.md#SignIn)  
    -   [<span data-ttu-id="75a76-135">Регистрация</span><span class="sxs-lookup"><span data-stu-id="75a76-135">Sign up</span></span>](api-management-page-templates.md#SignUp)  
    -   [<span data-ttu-id="75a76-136">Страница не найдена</span><span class="sxs-lookup"><span data-stu-id="75a76-136">Page not found</span></span>](api-management-page-templates.md#PageNotFound)


## <a name="next-steps"></a><span data-ttu-id="75a76-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75a76-137">Next steps</span></span>  
-   [<span data-ttu-id="75a76-138">Справочник по шаблонам</span><span class="sxs-lookup"><span data-stu-id="75a76-138">Template reference</span></span>](api-management-developer-portal-templates-reference.md)  
-   [<span data-ttu-id="75a76-139">Справочник по моделям данных</span><span class="sxs-lookup"><span data-stu-id="75a76-139">Data model reference</span></span>](api-management-template-data-model-reference.md)  
-   [<span data-ttu-id="75a76-140">Элементы управления страницы</span><span class="sxs-lookup"><span data-stu-id="75a76-140">Page controls</span></span>](api-management-page-controls.md)  
-   [<span data-ttu-id="75a76-141">Ресурсы шаблонов</span><span class="sxs-lookup"><span data-stu-id="75a76-141">Template resources</span></span>](api-management-template-resources.md)