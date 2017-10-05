---
title: "Непредвиденный запрос на согласие при входе в приложение | Документы Майкрософт"
description: "Способы устранения неполадок, когда пользователь видит неожиданный запрос на согласие для приложения, которое вы интегрировали с Azure AD."
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
ms.openlocfilehash: e5b823e1251a7221f73efe6838d439f827f9665d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-to-an-application"></a><span data-ttu-id="84e3c-103">Непредвиденный запрос на согласие при входе в приложение</span><span class="sxs-lookup"><span data-stu-id="84e3c-103">Unexpected consent prompt when signing in to an application</span></span>

<span data-ttu-id="84e3c-104">Для правильной работы многим приложениям, интегрирующимся с Azure Active Directory, нужны разрешения на доступ к разным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="84e3c-104">Many applications that integrate with Azure Active Directory require permissions to various resources in order to run.</span></span> <span data-ttu-id="84e3c-105">Если эти ресурсы также интегрированы с Azure Active Directory, доступ к ним запрашивается с помощью инфраструктуры согласия Azure AD.</span><span class="sxs-lookup"><span data-stu-id="84e3c-105">When these resources are also integrated with Azure Active Directory, permissions to access them is requested using the Azure AD consent framework.</span></span> 

<span data-ttu-id="84e3c-106">Это приводит к отображению запроса на согласие при первом запуске приложения, что часто является единовременной операцией.</span><span class="sxs-lookup"><span data-stu-id="84e3c-106">This results in a consent prompt being shown the first time an application is used, which is often a one-time operation.</span></span> 

## <a name="scenarios-in-which-users-see-consent-prompts"></a><span data-ttu-id="84e3c-107">Сценарии, в которых пользователи видят запрос на согласие</span><span class="sxs-lookup"><span data-stu-id="84e3c-107">Scenarios in which users see consent prompts</span></span>

<span data-ttu-id="84e3c-108">Дополнительные запросы можно ожидать в разных сценариях:</span><span class="sxs-lookup"><span data-stu-id="84e3c-108">Additional prompts can be expected in various scenarios:</span></span>

* <span data-ttu-id="84e3c-109">Изменился набор требуемых приложению разрешений.</span><span class="sxs-lookup"><span data-stu-id="84e3c-109">The set of permissions required by the application have changed.</span></span>

* <span data-ttu-id="84e3c-110">Пользователь, который изначально дал согласие для приложения, не являлся администратором, а теперь другой пользователь (без прав администратора) впервые открывает приложение.</span><span class="sxs-lookup"><span data-stu-id="84e3c-110">The user who originally consented to the application was not an administrator, and now a different (non-admin) User is using the application for the first time.</span></span>

* <span data-ttu-id="84e3c-111">Пользователь, который изначально дал согласие для приложения, являлся администратором, однако он сделал это не от имени всей организации.</span><span class="sxs-lookup"><span data-stu-id="84e3c-111">The user who originally consented to the application was an administrator, but they did not consent on-behalf of the entire organization.</span></span>

* <span data-ttu-id="84e3c-112">Приложение использует [добавочное и динамическое согласие](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) для запроса дополнительных разрешений после изначального предоставления согласия.</span><span class="sxs-lookup"><span data-stu-id="84e3c-112">The application is using [incremental and dynamic consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) to request additional permissions after consent was initially granted.</span></span> <span data-ttu-id="84e3c-113">Такой подход часто применяется, когда расширенным функциям приложения нужны дополнительные разрешения сверх базового набора.</span><span class="sxs-lookup"><span data-stu-id="84e3c-113">This is often used when optional features of an application additional require permissions beyond those required for baseline functionality.</span></span>

* <span data-ttu-id="84e3c-114">Согласие было отозвано после первоначального предоставления.</span><span class="sxs-lookup"><span data-stu-id="84e3c-114">Consent was revoked after being granted initially.</span></span>

* <span data-ttu-id="84e3c-115">Разработчик настроил приложение для обязательного запроса на согласие при каждом использовании (обратите внимание, что такой подход не является рекомендуемым).</span><span class="sxs-lookup"><span data-stu-id="84e3c-115">The developer has configured the application to require a consent prompt every time it is used (note: this is not best practice).</span></span>

## <a name="next-steps"></a><span data-ttu-id="84e3c-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84e3c-116">Next steps</span></span>

-   [<span data-ttu-id="84e3c-117">Приложения, разрешения и согласие в Azure Active Directory (конечная точка версии 1.0)</span><span class="sxs-lookup"><span data-stu-id="84e3c-117">Apps, permissions, and consent in Azure Active Directory (v1.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [<span data-ttu-id="84e3c-118">Области, разрешения и согласие в Azure Active Directory (конечная точка версии 2.0)</span><span class="sxs-lookup"><span data-stu-id="84e3c-118">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


