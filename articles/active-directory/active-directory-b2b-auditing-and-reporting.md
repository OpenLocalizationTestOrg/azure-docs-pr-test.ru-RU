---
title: "Аудит и отчеты для пользователей службы совместной работы Azure Active Directory B2B | Документация Майкрософт"
description: "Свойства гостевого пользователя службы совместной работы Azure Active Directory B2B можно настраивать."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: ba782270f3280e52235bc13148d232284b55762a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="auditing-and-reporting-a-b2b-collaboration-user"></a><span data-ttu-id="36c16-103">Аудит и отчеты для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="36c16-103">Auditing and reporting a B2B collaboration user</span></span>
<span data-ttu-id="36c16-104">Для гостевых пользователей доступны такие же возможности аудита, как и для пользователей-участников.</span><span class="sxs-lookup"><span data-stu-id="36c16-104">With guest users, you have auditing capabilities similar to with member users.</span></span> <span data-ttu-id="36c16-105">Ниже приведен пример журнала приглашений и активаций приглашенного пользователя Сэма Угла (Sam Oogle).</span><span class="sxs-lookup"><span data-stu-id="36c16-105">Here's an example of the invitation and redemption history of invitee Sam Oogle:</span></span>

![журнал аудита](./media/active-directory-b2b-auditing-and-reporting/audit-log.png)

<span data-ttu-id="36c16-107">Вы можете подробней рассмотреть каждое из этих событий.</span><span class="sxs-lookup"><span data-stu-id="36c16-107">You can dive into each of these events to get the details.</span></span> <span data-ttu-id="36c16-108">Например, давайте просмотрим сведения о принятии приглашения.</span><span class="sxs-lookup"><span data-stu-id="36c16-108">For example, let's look at the acceptance details.</span></span>

![сведения о действии](./media/active-directory-b2b-auditing-and-reporting/activity-details.png)

<span data-ttu-id="36c16-110">Вы можете также экспортировать эти журналы из Azure AD и с помощью любого инструмента для создания отчетов создавать собственные настраиваемые отчеты.</span><span class="sxs-lookup"><span data-stu-id="36c16-110">You can also export these logs from Azure AD and use the reporting tool of your choice to get customized reports.</span></span>

### <a name="next-steps"></a><span data-ttu-id="36c16-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36c16-111">Next steps</span></span>

<span data-ttu-id="36c16-112">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="36c16-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="36c16-113">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="36c16-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="36c16-114">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="36c16-114">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="36c16-115">Добавление пользователя службы совместной работы Azure Active Directory B2B в роль</span><span class="sxs-lookup"><span data-stu-id="36c16-115">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="36c16-116">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="36c16-116">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="36c16-117">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="36c16-117">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="36c16-118">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="36c16-118">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="36c16-119">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="36c16-119">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="36c16-120">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="36c16-120">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="36c16-121">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36c16-121">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="36c16-122">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="36c16-122">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="36c16-123">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="36c16-123">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
