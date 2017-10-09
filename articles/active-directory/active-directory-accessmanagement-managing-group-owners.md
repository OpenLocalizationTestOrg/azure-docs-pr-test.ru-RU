---
title: "aaaNext действия для управления доступом с помощью групп | Документы Microsoft"
description: "Как расширенный-руководства по управлению группами безопасности и как toouse эти группы доступа toomanage tooa ресурсов."
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
ms.openlocfilehash: 4fd55f893290fac3551a130f29bd12709cf551e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-owners-for-a-group"></a><span data-ttu-id="a34a8-103">Управление владельцами группы</span><span class="sxs-lookup"><span data-stu-id="a34a8-103">Managing owners for a group</span></span>
<span data-ttu-id="a34a8-104">Уже присвоенное владельцем ресурса группы ресурсов tooan Azure AD для доступа к tooa hello членства группы hello управляется hello владелец группы.</span><span class="sxs-lookup"><span data-stu-id="a34a8-104">Once a resource owner has assigned access tooa resource tooan Azure AD group, hello membership of hello group is managed by hello group owner.</span></span> <span data-ttu-id="a34a8-105">владелец ресурса Hello фактически передает hello разрешение tooassign пользователей toohello toohello владелец ресурса группы hello.</span><span class="sxs-lookup"><span data-stu-id="a34a8-105">hello resource owner effectively delegates hello permission tooassign users toohello resource toohello owner of hello group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a34a8-106">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a34a8-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

## <a name="assigning-group-ownership"></a><span data-ttu-id="a34a8-107">Назначение владельца группы</span><span class="sxs-lookup"><span data-stu-id="a34a8-107">Assigning group ownership</span></span>
<span data-ttu-id="a34a8-108">**tooadd tooa владельца группы**</span><span class="sxs-lookup"><span data-stu-id="a34a8-108">**tooadd an owner tooa group**</span></span>

1. <span data-ttu-id="a34a8-109">В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем откройте каталог вашей организации.</span><span class="sxs-lookup"><span data-stu-id="a34a8-109">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="a34a8-110">Выберите hello **группы** вкладки и группы последовательно откройте hello tooadd владельцам.</span><span class="sxs-lookup"><span data-stu-id="a34a8-110">Select hello **Groups** tab, and then open hello group that you want tooadd owners to.</span></span>
3. <span data-ttu-id="a34a8-111">Щелкните **Добавить владельцев**.</span><span class="sxs-lookup"><span data-stu-id="a34a8-111">Select **Add Owners**.</span></span>
4. <span data-ttu-id="a34a8-112">На hello **добавить владельцев** страницу, выберите hello пользователь должен быть tooadd hello владельца этой группы и убедитесь, что это имя добавлено toohello **выбранные** области.</span><span class="sxs-lookup"><span data-stu-id="a34a8-112">On hello **Add owners** page, select hello user that you want tooadd as hello owner of this group, and make sure this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="a34a8-113">**tooremove владельца из группы**</span><span class="sxs-lookup"><span data-stu-id="a34a8-113">**tooremove an owner from a group**</span></span>

1. <span data-ttu-id="a34a8-114">В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем откройте каталог вашей организации.</span><span class="sxs-lookup"><span data-stu-id="a34a8-114">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="a34a8-115">Выберите hello **группы** табуляции, а затем откройте hello группу, которой необходимо tooremove владельца.</span><span class="sxs-lookup"><span data-stu-id="a34a8-115">Select hello **Groups** tab, and then open hello group that you want tooremove an owner from.</span></span>
3. <span data-ttu-id="a34a8-116">Выберите hello **владельцев** вкладки.</span><span class="sxs-lookup"><span data-stu-id="a34a8-116">Select hello **Owners** tab.</span></span>
4. <span data-ttu-id="a34a8-117">Выберите hello владелец должен tooremove из этой группы, а затем выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a34a8-117">Select hello owner that you want tooremove from this group, and then select **Remove**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="a34a8-118">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="a34a8-118">Additional information</span></span>
<span data-ttu-id="a34a8-119">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a34a8-119">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="a34a8-120">Управление tooresources доступ с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a34a8-120">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="a34a8-121">Настройка параметров групп с помощью командлетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a34a8-121">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="a34a8-122">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a34a8-122">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="a34a8-123">Что такое Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a34a8-123">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="a34a8-124">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a34a8-124">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
