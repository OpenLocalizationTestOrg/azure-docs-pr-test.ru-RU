---
title: "Назначение пользователей приложениям | Документация Майкрософт"
description: "Общие сведения о назначении пользователей для приложения в клиенте"
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="be5b0-103">Назначение пользователей для приложений</span><span class="sxs-lookup"><span data-stu-id="be5b0-103">How to assign users to applications</span></span>

<span data-ttu-id="be5b0-104">В этой статье представлены общие сведения о назначении пользователей для приложения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="be5b0-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="be5b0-105">Как пользователи назначаются для приложений в Azure AD?</span><span class="sxs-lookup"><span data-stu-id="be5b0-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="be5b0-106">Чтобы пользователь смог получить доступ к приложению, сначала его нужно любым образом назначить этому приложению.</span><span class="sxs-lookup"><span data-stu-id="be5b0-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="be5b0-107">Это может сделать администратор, бизнес-делегат или, в некоторых случаях, сам пользователь.</span><span class="sxs-lookup"><span data-stu-id="be5b0-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="be5b0-108">Ниже описаны способы назначения пользователя для приложения.</span><span class="sxs-lookup"><span data-stu-id="be5b0-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="be5b0-109">Администратор [назначает пользователей](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) непосредственно для приложения.</span><span class="sxs-lookup"><span data-stu-id="be5b0-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="be5b0-110">Администратор [назначает для приложения группу](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal), в которую входит пользователь. Ею может быть одна из следующих:</span><span class="sxs-lookup"><span data-stu-id="be5b0-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="be5b0-111">Группа, синхронизированная из локальной среды.</span><span class="sxs-lookup"><span data-stu-id="be5b0-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="be5b0-112">Статическая группа безопасности, созданная в облаке.</span><span class="sxs-lookup"><span data-stu-id="be5b0-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="be5b0-113">[Динамическая группа безопасности](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal), созданная в облаке.</span><span class="sxs-lookup"><span data-stu-id="be5b0-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="be5b0-114">Группа Office 365, созданная в облаке.</span><span class="sxs-lookup"><span data-stu-id="be5b0-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="be5b0-115">Группа ["Все пользователи"](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups).</span><span class="sxs-lookup"><span data-stu-id="be5b0-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="be5b0-116">Администратор включает [самостоятельный доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access), чтобы позволить пользователю добавлять приложения, используя возможность **добавления приложения** на [панели доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **без бизнес-утверждения**.</span><span class="sxs-lookup"><span data-stu-id="be5b0-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="be5b0-117">Администратор включает [самостоятельный доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access), чтобы позволить пользователю добавлять приложения, используя возможность **добавления приложения** на [панели доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **с предварительного разрешения выбранных утверждающих лиц**.</span><span class="sxs-lookup"><span data-stu-id="be5b0-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="be5b0-118">Администратор включает [самостоятельное управление группами](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), чтобы позволить пользователям присоединяться к группам, которым назначено приложение, **без бизнес-утверждения**.</span><span class="sxs-lookup"><span data-stu-id="be5b0-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="be5b0-119">Администратор включает [самостоятельное управление группами](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), чтобы позволить пользователям присоединяться к группам, которым назначено приложение, только **с предварительного разрешения выбранных утверждающих лиц**.</span><span class="sxs-lookup"><span data-stu-id="be5b0-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="be5b0-120">Администратор назначает пользователю лицензии напрямую для приложений Майкрософт, например [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="be5b0-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="be5b0-121">Администратор назначает группе, в которую входит пользователь, лицензию на приложение Майкрософт, например [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="be5b0-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="be5b0-122">[Администратор дает свое согласие на использование приложения](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) всеми пользователями, а затем пользователь входит в это приложение.</span><span class="sxs-lookup"><span data-stu-id="be5b0-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="be5b0-123">Пользователь сам [дает согласие на использование приложения](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) при входе в него.</span><span class="sxs-lookup"><span data-stu-id="be5b0-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="be5b0-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be5b0-124">Next steps</span></span>
[<span data-ttu-id="be5b0-125">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be5b0-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
