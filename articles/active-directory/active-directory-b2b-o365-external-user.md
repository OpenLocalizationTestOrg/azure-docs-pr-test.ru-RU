---
title: "aaaOffice 365 внешний общий доступ и совместная работа Azure Active Directory B2B | Документы Microsoft"
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
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="1c2c5-103">Внешний общий доступ Office 365 и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1c2c5-103">Office 365 external sharing and Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="1c2c5-104">Внешний общий доступ в Office 365 (OneDrive, SharePoint Online, объединенные группы, т. д.) и Azure Active Directory (Azure AD) B2B совместной работы с технической точки зрения hello же самое.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-104">External sharing in Office 365 (OneDrive, SharePoint Online, Unified Groups, etc.) and Azure Active Directory (Azure AD) B2B collaboration are technically hello same thing.</span></span> <span data-ttu-id="1c2c5-105">Всем внешним доступом (за исключением OneDrive или SharePoint Online), включая гостей в группах Office 365, уже использует приглашения совместной работы Azure AD B2B hello API-интерфейсы для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-105">All external sharing (except OneDrive/SharePoint Online), including guests in Office 365 Groups, already uses hello Azure AD B2B collaboration invitation APIs for sharing.</span></span>

<span data-ttu-id="1c2c5-106">В OneDrive и SharePoint Online используется другой диспетчер приглашений.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-106">OneDrive/SharePoint Online has a separate invitation manager.</span></span> <span data-ttu-id="1c2c5-107">Поддержка внешнего общего доступа в OneDrive и SharePoint Online была реализована до того, как ее внедрили в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-107">Support for external sharing in OneDrive/SharePoint Online started before Azure AD developed its support.</span></span> <span data-ttu-id="1c2c5-108">Со временем общий доступ к OneDrive или SharePoint Online внешних начисленная несколько функций и несколько миллионов пользователей, применяющих hello продукта встроенные общий доступ к шаблону.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-108">Over time, OneDrive/SharePoint Online external sharing has accrued several features and many millions of users who use hello product's in-built sharing pattern.</span></span> <span data-ttu-id="1c2c5-109">Однако существуют незначительные различия в принципах работы внешнего общего доступа OneDrive и SharePoint Online и службы совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="1c2c5-109">However, there are some subtle differences between how OneDrive/SharePoint Online external sharing works and how Azure AD B2B collaboration works:</span></span>

- <span data-ttu-id="1c2c5-110">OneDrive или SharePoint Online пользователи toohello каталог добавляется после пользователи активирован приглашения.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-110">OneDrive/SharePoint Online adds users toohello directory after users have redeemed their invitations.</span></span> <span data-ttu-id="1c2c5-111">Таким образом прежде чем активации, вы не видите hello пользователя на портале Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-111">So, before redemption, you don't see hello user in Azure AD portal.</span></span> <span data-ttu-id="1c2c5-112">Если другой сайт приглашает пользователя в hello это время, создается новое приглашение.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-112">If another site invites a user in hello meantime, a new invitation is generated.</span></span> <span data-ttu-id="1c2c5-113">При использовании службы совместной работы Azure AD B2B пользователь добавляется непосредственно после отправки приглашения, поэтому он сразу везде отображается.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-113">However, when you use Azure AD B2B collaboration, users are added immediately on invitation so that they show up everywhere.</span></span>

- <span data-ttu-id="1c2c5-114">взаимодействие активации Hello в OneDrive или SharePoint Online отличается от работы hello в совместной работы Azure AD B2B.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-114">hello redemption experience in OneDrive/SharePoint Online looks different from hello experience in Azure AD B2B collaboration.</span></span> <span data-ttu-id="1c2c5-115">После пользователь redeems приглашение, hello взаимодействия выглядят одинаково.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-115">After a user redeems an invitation, hello experiences look alike.</span></span>

- <span data-ttu-id="1c2c5-116">Пользователей, приглашенных в службу совместной работы Azure AD B2B, можно выбирать в диалоговых окнах общего доступа OneDrive и SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-116">Azure AD B2B collaboration invited users can be picked from OneDrive/SharePoint Online sharing dialog boxes.</span></span> <span data-ttu-id="1c2c5-117">Приглашенные пользователи OneDrive и SharePoint Online также отображаются в Azure AD после того, как они активируют свои приглашения.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-117">OneDrive/SharePoint Online invited users also show up in Azure AD after they redeem their invitations.</span></span>

- <span data-ttu-id="1c2c5-118">toomanage внешнего совместного использования в OneDrive или SharePoint Online с Azure AD B2B совместной работы, задайте hello OneDrive или SharePoint Online внешнего совместного использования задание слишком**только открыть доступ для внешних пользователей уже в каталоге hello**.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-118">toomanage external sharing in OneDrive/SharePoint Online with Azure AD B2B collaboration, set hello OneDrive/SharePoint Online external sharing setting too**Only allow sharing with external users already in hello directory**.</span></span> <span data-ttu-id="1c2c5-119">Пользователи могут перейти tooexternally общих сайтов и выбора с внешними участниками, Здравствуйте, администратор добавил.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-119">Users can go tooexternally shared sites and pick from external collaborators that hello admin has added.</span></span> <span data-ttu-id="1c2c5-120">Здравствуйте, администратор может добавить hello внешними участниками через hello приглашения совместной работы B2B API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="1c2c5-120">hello admin can add hello external collaborators through hello B2B collaboration invitation APIs.</span></span>

![OneDrive или SharePoint Online настройки общего доступа к внешней Hello](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a><span data-ttu-id="1c2c5-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c2c5-122">Next steps</span></span>

<span data-ttu-id="1c2c5-123">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="1c2c5-123">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1c2c5-124">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="1c2c5-124">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1c2c5-125">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1c2c5-125">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="1c2c5-126">Добавление роли пользователя tooa B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="1c2c5-126">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="1c2c5-127">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1c2c5-127">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="1c2c5-128">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1c2c5-128">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="1c2c5-129">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1c2c5-129">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="1c2c5-130">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="1c2c5-130">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="1c2c5-131">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1c2c5-131">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="1c2c5-132">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c2c5-132">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="1c2c5-133">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1c2c5-133">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
