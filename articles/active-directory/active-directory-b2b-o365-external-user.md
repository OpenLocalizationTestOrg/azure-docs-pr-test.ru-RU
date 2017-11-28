---
title: "Внешний общий доступ Office 365 и служба совместной работы Azure Active Directory B2B | Документация Майкрософт"
description: "Справочные материалы по сопоставлению утверждений для службы совместной работы Azure Active Directory B2B."
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: cad0ce8f745f3d6ca14436fd714b08c60de0e459
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="f3143-103">Внешний общий доступ Office 365 и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f3143-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="f3143-104">Внешний общий доступ в Office 365 (OneDrive, SharePoint Online, единые группы и т. д.) и служба совместной работы Azure Active Directory (Azure AD) B2B — это одно и то же с технической точки зрения.</span><span class="sxs-lookup"><span data-stu-id="f3143-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically the same thing.</span></span> <span data-ttu-id="f3143-105">Все решения внешнего общего доступа (за исключением OneDrive и SharePoint Online), в том числе гости в группах Office 365, уже используют для общего доступа API приглашения службы совместной работы Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="f3143-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses the Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="f3143-106">В OneDrive и SharePoint Online используется другой диспетчер приглашений.</span><span class="sxs-lookup"><span data-stu-id="f3143-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="f3143-107">Поддержка внешнего общего доступа в OneDrive и SharePoint Online была реализована до того, как ее внедрили в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3143-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="f3143-108">Со временем функция внешнего общего доступа OneDrive и SharePoint Online обросла дополнительными компонентами, и миллионы пользователей используют встроенную модель общего доступа этого продукта.</span><span class="sxs-lookup"><span data-stu-id="f3143-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use the product's in-built sharing pattern.</span></span> <span data-ttu-id="f3143-109">Однако существуют незначительные различия в принципах работы внешнего общего доступа OneDrive и SharePoint Online и службы совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="f3143-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="f3143-110">OneDrive и SharePoint Online добавляют пользователей в каталог после того, как пользователи активировали приглашения.</span><span class="sxs-lookup"><span data-stu-id="f3143-110">OneDrive/SharePoint Online adds users to the directory after users have redeemed their invitations.</span></span> <span data-ttu-id="f3143-111">Таким образом, до активации вы не видите пользователя на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3143-111">So, before redemption, you don't see the user in Azure AD portal.</span></span> <span data-ttu-id="f3143-112">В то же время если пользователь приглашается из другого сайта, то создается новое приглашение.</span><span class="sxs-lookup"><span data-stu-id="f3143-112">If another site invites a user in the meantime, a new invitation is generated.</span></span> <span data-ttu-id="f3143-113">При использовании службы совместной работы Azure AD B2B пользователь добавляется непосредственно после отправки приглашения, поэтому он сразу везде отображается.</span><span class="sxs-lookup"><span data-stu-id="f3143-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="f3143-114">Процесс активации приглашения в OneDrive и SharePoint Online отличается от аналогичной процедуры в службе совместной работы Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="f3143-114">The redemption experience in OneDrive/SharePoint Online looks different from the experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="f3143-115">После того как пользователь активирует приглашение, интерфейсы будут выглядеть одинаково.</span><span class="sxs-lookup"><span data-stu-id="f3143-115">After a user redeems an invitation, the experiences look alike.</span></span>

- <span data-ttu-id="f3143-116">Пользователей, приглашенных в службу совместной работы Azure AD B2B, можно выбирать в диалоговых окнах общего доступа OneDrive и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="f3143-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="f3143-117">Приглашенные пользователи OneDrive и SharePoint Online также отображаются в Azure AD после того, как они активируют свои приглашения.</span><span class="sxs-lookup"><span data-stu-id="f3143-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="f3143-118">Чтобы управлять внешним общим доступом в OneDrive и SharePoint Online с помощью службы совместной работы Azure AD B2B, задайте для параметра внешнего общего доступа OneDrive и SharePoint Online значение **Only allow sharing with external users already in the directory** (Разрешить общий доступ только внешним пользователям, которые уже внесены в каталог).</span><span class="sxs-lookup"><span data-stu-id="f3143-118">To manage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set the OneDrive/SharePoint Online external sharing setting to **Only allow sharing with external users already in the directory**.</span></span> <span data-ttu-id="f3143-119">Пользователи могут перейти на внешние сайты, предоставляющие общий доступ, и выбрать из внешних сотрудников, добавленных администратором.</span><span class="sxs-lookup"><span data-stu-id="f3143-119">Users can go to externally shared sites and pick from external collaborators that the admin has added.</span></span> <span data-ttu-id="f3143-120">Администратор может добавлять внешних сотрудников с помощью интерфейсов API приглашения службы совместной работы B2B.</span><span class="sxs-lookup"><span data-stu-id="f3143-120">The admin can add the external collaborators through the B2B collaboration invitation APIs.</span></span>

![Настройка внешнего общего доступа в OneDrive и SharePoint Online](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="f3143-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3143-122">Next steps</span></span>

<span data-ttu-id="f3143-123">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="f3143-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f3143-124">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="f3143-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f3143-125">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f3143-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="f3143-126">Добавление пользователя службы совместной работы Azure Active Directory B2B в роль</span><span class="sxs-lookup"><span data-stu-id="f3143-126">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="f3143-127">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f3143-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="f3143-128">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f3143-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="f3143-129">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f3143-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="f3143-130">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="f3143-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="f3143-131">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f3143-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="f3143-132">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3143-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="f3143-133">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f3143-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
