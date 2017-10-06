---
title: "Пользователи tooapplications aaaHow tooAssign | Документы Microsoft"
description: "Понять, как пользователи получить назначения tooan приложения в клиенте"
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="e081e-103">Как tooapplications tooassign пользователей</span><span class="sxs-lookup"><span data-stu-id="e081e-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="e081e-104">В этой статье помогут toounderstand получить назначение пользователей tooan приложения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="e081e-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="e081e-105">Как пользователей получить назначения tooan приложения в Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e081e-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="e081e-106">Для tooaccess пользователя приложения их необходимо назначить tooit иным образом.</span><span class="sxs-lookup"><span data-stu-id="e081e-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="e081e-107">Назначение может выполнять администратор, business делегата или в некоторых случаях пользователь hello сами.</span><span class="sxs-lookup"><span data-stu-id="e081e-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="e081e-108">Ниже описываются способы hello, которые пользователи могут получить назначения tooapplications:</span><span class="sxs-lookup"><span data-stu-id="e081e-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="e081e-109">Администратор [назначает пользователя](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello приложению напрямую</span><span class="sxs-lookup"><span data-stu-id="e081e-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="e081e-110">Администратор [Назначение группы](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) hello пользователя является членом toohello приложения, включая:</span><span class="sxs-lookup"><span data-stu-id="e081e-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="e081e-111">Группа, синхронизированная из локальной среды.</span><span class="sxs-lookup"><span data-stu-id="e081e-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="e081e-112">Безопасность статической группы в облаке hello</span><span class="sxs-lookup"><span data-stu-id="e081e-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="e081e-113">Объект [динамической безопасности группы](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) в облаке hello</span><span class="sxs-lookup"><span data-stu-id="e081e-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="e081e-114">Группы Office 365, созданной в облаке hello</span><span class="sxs-lookup"><span data-stu-id="e081e-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="e081e-115">Hello [всех пользователей](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) группы</span><span class="sxs-lookup"><span data-stu-id="e081e-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="e081e-116">Администратор включает [самообслуживания доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd пользователя приложения с помощью hello [панели доступа приложения](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **добавить приложение** функция **без утверждения бизнеса**</span><span class="sxs-lookup"><span data-stu-id="e081e-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="e081e-117">Администратор включает [самообслуживания доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd пользователя приложения с помощью hello [панели доступа приложения](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **добавить приложение** компонент, но только w **i-ой предварительного разрешения из выбранного набора утверждающих бизнеса**</span><span class="sxs-lookup"><span data-stu-id="e081e-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="e081e-118">Администратор включает [Самостоятельное управление группами](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin пользователем группы, назначенный приложению слишком**без утверждения бизнеса**</span><span class="sxs-lookup"><span data-stu-id="e081e-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="e081e-119">Администратор включает [Самостоятельное управление группами](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin пользователя, назначенный приложению в, но только группы **с предварительного разрешения из выбранного набора утверждающих бизнеса**</span><span class="sxs-lookup"><span data-stu-id="e081e-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="e081e-120">Администратор назначает лицензии пользователя tooa непосредственно для первой стороной приложения, таких как [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="e081e-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="e081e-121">Администратор назначает, tooa лицензионную группу, hello пользователь является членом tooa первой стороной приложения, как [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="e081e-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="e081e-122">[Администратора согласии приложения tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe использовать все пользователи, а затем пользователь входит в приложении toohello</span><span class="sxs-lookup"><span data-stu-id="e081e-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="e081e-123">Пользователь [согласии приложения tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) сами при входе в приложение toohello</span><span class="sxs-lookup"><span data-stu-id="e081e-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="e081e-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e081e-124">Next steps</span></span>
[<span data-ttu-id="e081e-125">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e081e-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
