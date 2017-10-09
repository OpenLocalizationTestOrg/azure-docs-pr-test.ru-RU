---
title: "Запрос согласия aaaUnexpected при входе в приложение tooan | Документы Microsoft"
description: "Как tootroubleshoot, когда пользователь видит запрос согласия для приложения, интегрированы с Azure AD, вы не ожидали"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a><span data-ttu-id="1e340-103">Запрос согласия Непредвиденная, при входе в приложение tooan</span><span class="sxs-lookup"><span data-stu-id="1e340-103">Unexpected consent prompt when signing in tooan application</span></span>

<span data-ttu-id="1e340-104">Многие приложения, которые интегрируются с Azure Active Directory требуют разрешения toovarious ресурсы в toorun порядке.</span><span class="sxs-lookup"><span data-stu-id="1e340-104">Many applications that integrate with Azure Active Directory require permissions toovarious resources in order toorun.</span></span> <span data-ttu-id="1e340-105">Когда эти ресурсы также интегрированы с Azure Active Directory, разрешения tooaccess их запрашивается при помощи hello Azure AD разрешения framework.</span><span class="sxs-lookup"><span data-stu-id="1e340-105">When these resources are also integrated with Azure Active Directory, permissions tooaccess them is requested using hello Azure AD consent framework.</span></span> 

<span data-ttu-id="1e340-106">Это приведет к запрос согласия, показывается hello при первом запуске приложения используется, что часто является единовременной операцией.</span><span class="sxs-lookup"><span data-stu-id="1e340-106">This results in a consent prompt being shown hello first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="1e340-107">Сценарии, в которых пользователи видят запрос на согласие</span><span class="sxs-lookup"><span data-stu-id="1e340-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="1e340-108">Дополнительные запросы можно ожидать в разных сценариях:</span><span class="sxs-lookup"><span data-stu-id="1e340-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="1e340-109">набор разрешений, необходимые приложения hello Hello изменились.</span><span class="sxs-lookup"><span data-stu-id="1e340-109">hello set of permissions required by hello application have changed.</span></span>

* <span data-ttu-id="1e340-110">Hello пользователя, изначально согласие toohello приложения не являлся администратором, а теперь различных (без прав администратора) пользователь использует приложение hello для hello первый раз.</span><span class="sxs-lookup"><span data-stu-id="1e340-110">hello user who originally consented toohello application was not an administrator, and now a different (non-admin) User is using hello application for hello first time.</span></span>

* <span data-ttu-id="1e340-111">Hello пользователя, изначально согласие toohello приложения являлся администратором, но они не согласие от имени hello всей организации.</span><span class="sxs-lookup"><span data-stu-id="1e340-111">hello user who originally consented toohello application was an administrator, but they did not consent on-behalf of hello entire organization.</span></span>

* <span data-ttu-id="1e340-112">Использование приложения Hello [добавочного, так и динамические согласия](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest дополнительных разрешений после предоставления согласия изначально.</span><span class="sxs-lookup"><span data-stu-id="1e340-112">hello application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest additional permissions after consent was initially granted.</span></span> <span data-ttu-id="1e340-113">Такой подход часто применяется, когда расширенным функциям приложения нужны дополнительные разрешения сверх базового набора.</span><span class="sxs-lookup"><span data-stu-id="1e340-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="1e340-114">Согласие было отозвано после первоначального предоставления.</span><span class="sxs-lookup"><span data-stu-id="1e340-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="1e340-115">Каждый раз при его использовании developer Привет настроил toorequire приложения hello запрос согласия (Примечание: это не лучшее решение).</span><span class="sxs-lookup"><span data-stu-id="1e340-115">hello developer has configured hello application toorequire a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e340-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1e340-116">Next steps</span></span>

-   [<span data-ttu-id="1e340-117">Приложения, разрешения и согласие в Azure Active Directory (конечная точка версии 1.0)</span><span class="sxs-lookup"><span data-stu-id="1e340-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="1e340-118">Области, разрешения и разрешения в hello Azure Active Directory (конечная точка версии 2.0)</span><span class="sxs-lookup"><span data-stu-id="1e340-118">Scopes, permissions, and consent in hello Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


