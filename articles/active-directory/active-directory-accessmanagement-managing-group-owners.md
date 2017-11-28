---
title: "Дополнительные возможности управления доступом с помощью групп | Документация Майкрософт"
description: "Расширенные указания по управлению группами безопасности и использованию этих групп для управления доступом к ресурсу."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="1ce4e-103">Управление владельцами группы</span><span class="sxs-lookup"><span data-stu-id="1ce4e-103">Managing owners for a group</span></span>
<span data-ttu-id="1ce4e-104">После того как владелец ресурса предоставил доступ к ресурсу группе Azure Active Directory, управление членством в группе осуществляется владельцем группы.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-104">Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner.</span></span> <span data-ttu-id="1ce4e-105">Владелец ресурса фактически делегирует владельцу группы разрешение предоставлять пользователям доступ к ресурсу.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-105">The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ce4e-106">Для управления службой Azure AD мы рекомендуем использовать [Центр администрирования Azure AD](https://aad.portal.azure.com) на портале Azure, а не классический портал Azure, который упоминается в этой статье.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-106">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="1ce4e-107">Назначение владельца группы</span><span class="sxs-lookup"><span data-stu-id="1ce4e-107">Assigning group ownership</span></span>
<span data-ttu-id="1ce4e-108">**Добавление владельца в группу**</span><span class="sxs-lookup"><span data-stu-id="1ce4e-108">**To add an owner to a group**</span></span>

1. <span data-ttu-id="1ce4e-109">На [классическом портале Azure](https://manage.windowsazure.com)щелкните **Active Directory**, а затем откройте каталог своей организации.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-109">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="1ce4e-110">Откройте вкладку **Группы** , а затем группу, в которую нужно добавить владельцев.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-110">Select the **Groups** tab, and then open the group that you want to add owners to.</span></span>
3. <span data-ttu-id="1ce4e-111">Щелкните **Добавить владельцев**.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="1ce4e-112">На странице **Добавление владельцев** выберите пользователя, которого нужно добавить в качестве владельца этой группы, и убедитесь в том, что его имя появилось в области **Выбранные**.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-112">On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="1ce4e-113">**Удаление владельца из группы**</span><span class="sxs-lookup"><span data-stu-id="1ce4e-113">**To remove an owner from a group**</span></span>

1. <span data-ttu-id="1ce4e-114">На [классическом портале Azure](https://manage.windowsazure.com)щелкните **Active Directory**, а затем откройте каталог своей организации.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-114">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="1ce4e-115">Откройте вкладку **Группы** , а затем группу, из которой нужно удалить владельца.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-115">Select the **Groups** tab, and then open the group that you want to remove an owner from.</span></span>
3. <span data-ttu-id="1ce4e-116">Откройте вкладку **Владельцы** .</span><span class="sxs-lookup"><span data-stu-id="1ce4e-116">Select the **Owners** tab.</span></span>
4. <span data-ttu-id="1ce4e-117">Выберите владельца, которого нужно удалить из группы, а затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-117">Select the owner that you want to remove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="1ce4e-118">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="1ce4e-118">Additional information</span></span>
<span data-ttu-id="1ce4e-119">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1ce4e-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="1ce4e-120">Управление доступом к ресурсам с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ce4e-120">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="1ce4e-121">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="1ce4e-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="1ce4e-122">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ce4e-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="1ce4e-123">Что такое Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ce4e-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="1ce4e-124">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ce4e-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
