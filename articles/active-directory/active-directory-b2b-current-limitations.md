---
title: "Ограничения службы совместной работы Azure Active Directory B2B | Документация Майкрософт"
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
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="22f22-103">Ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="22f22-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="22f22-104">К службе совместной работы Azure Active Directory B2B применяются ограничения, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="22f22-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="22f22-105">Возможное дублирование Многофакторной идентификации</span><span class="sxs-lookup"><span data-stu-id="22f22-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="22f22-106">С помощью Azure AD B2B вы можете принудительно применять многофакторную проверку подлинности в ресурсной организации (приглашающей организации).</span><span class="sxs-lookup"><span data-stu-id="22f22-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="22f22-107">Причины такого подхода подробно описаны в разделе [Многофакторная идентификация пользователей службы совместной работы Azure Active Directory B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="22f22-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="22f22-108">Если ваш партнер уже настроил многофакторную проверку подлинности и принудительно применяет ее, возможно, его пользователи должны будут выполнять эту проверку один раз в своей организации, а затем еще раз — в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="22f22-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="22f22-109">Мгновенное включение</span><span class="sxs-lookup"><span data-stu-id="22f22-109">Instant-on</span></span>
<span data-ttu-id="22f22-110">В рабочих потоках службы совместной работы B2B пользователи добавляются в каталог и динамически обновляются в процессе активации приглашений, при назначении приложений и т. д.</span><span class="sxs-lookup"><span data-stu-id="22f22-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="22f22-111">Операции обновления и записи обычно выполняются в одном экземпляре каталога и должны реплицироваться по всем экземплярам.</span><span class="sxs-lookup"><span data-stu-id="22f22-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="22f22-112">Репликация будет завершена после обновления всех экземпляров.</span><span class="sxs-lookup"><span data-stu-id="22f22-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="22f22-113">Иногда, когда объект записывается или обновляется в одном экземпляре, а вызов для извлечения этого объекта попадает на другой экземпляр, это вызывает задержку репликации.</span><span class="sxs-lookup"><span data-stu-id="22f22-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="22f22-114">В таком случае выполните обновление или повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="22f22-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="22f22-115">Если вы пишете приложение с помощью нашего API, то повторы с некоторой задержкой являются хорошей защитной практикой для облегчения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="22f22-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22f22-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22f22-116">Next steps</span></span>

<span data-ttu-id="22f22-117">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="22f22-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="22f22-118">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="22f22-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="22f22-119">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="22f22-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="22f22-120">Добавление пользователя службы совместной работы Azure Active Directory B2B в роль</span><span class="sxs-lookup"><span data-stu-id="22f22-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="22f22-121">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="22f22-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="22f22-122">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="22f22-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="22f22-123">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="22f22-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="22f22-124">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="22f22-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="22f22-125">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="22f22-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="22f22-126">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f22-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="22f22-127">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="22f22-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
