---
title: "aaaLimitations совместной работы Azure Active Directory B2B | Документы Microsoft"
description: "Текущие ограничения службы совместной работы Azure Active Directory B2B."
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="a8349-103">Ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a8349-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="a8349-104">Совместная работа Azure Active Directory (Azure AD) B2B сейчас субъекта toohello ограничения, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a8349-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="a8349-105">Возможное дублирование Многофакторной идентификации</span><span class="sxs-lookup"><span data-stu-id="a8349-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="a8349-106">С помощью Azure AD B2B можно применять многофакторную проверку подлинности на hello организации по ресурсам (hello приглашении организации).</span><span class="sxs-lookup"><span data-stu-id="a8349-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="a8349-107">Hello причины такой подход подробно описаны в [условный доступ для совместной работы пользователей B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="a8349-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="a8349-108">Если партнер уже многофакторной проверки подлинности и применяются, их пользователи могут иметь проверки подлинности hello tooperform один раз в домашней организации и затем снова в указанное имя.</span><span class="sxs-lookup"><span data-stu-id="a8349-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="a8349-109">Мгновенное включение</span><span class="sxs-lookup"><span data-stu-id="a8349-109">Instant-on</span></span>
<span data-ttu-id="a8349-110">В потоках hello B2B совместной работы добавьте каталог toohello пользователей и динамически обновлять их во время активации приглашения, назначение приложения и т. д.</span><span class="sxs-lookup"><span data-stu-id="a8349-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="a8349-111">Hello обновления записи обычно происходят в один каталог экземпляра и должны быть реплицированы на всех экземплярах.</span><span class="sxs-lookup"><span data-stu-id="a8349-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="a8349-112">Репликация будет завершена после обновления всех экземпляров.</span><span class="sxs-lookup"><span data-stu-id="a8349-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="a8349-113">Иногда при hello объекта записывается или обновлены в одном экземпляре и hello вызовите tooretrieve этого объекта — tooanother экземпляр, могут возникнуть задержки репликации.</span><span class="sxs-lookup"><span data-stu-id="a8349-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="a8349-114">В этом случае обновите или повторите toohelp.</span><span class="sxs-lookup"><span data-stu-id="a8349-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="a8349-115">При создании приложения с помощью наших API, а затем повторные попытки с некоторыми отсрочки является tooalleviate хорошим и защитного практике эту проблему.</span><span class="sxs-lookup"><span data-stu-id="a8349-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8349-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8349-116">Next steps</span></span>

<span data-ttu-id="a8349-117">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="a8349-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="a8349-118">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="a8349-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="a8349-119">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a8349-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="a8349-120">Добавление роли пользователя tooa B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="a8349-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="a8349-121">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a8349-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="a8349-122">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a8349-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="a8349-123">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a8349-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="a8349-124">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="a8349-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="a8349-125">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="a8349-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="a8349-126">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8349-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="a8349-127">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="a8349-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
