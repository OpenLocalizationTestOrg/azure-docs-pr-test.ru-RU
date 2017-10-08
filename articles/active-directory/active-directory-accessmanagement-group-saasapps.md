---
title: "aaaUsing tooSaaS доступа toomanage группы приложений | Документы Microsoft"
description: "Как toouse группы в Azure Active Directory Premium или Basic tooassign доступ к tooSaaS приложения, интегрированные с Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a><span data-ttu-id="4b722-103">С помощью приложения tooSaaS для доступа к toomanage группы</span><span class="sxs-lookup"><span data-stu-id="4b722-103">Using a group toomanage access tooSaaS applications</span></span>
<span data-ttu-id="4b722-104">С помощью Azure Active Directory (Azure AD) с лицензией Azure AD Premium или Azure AD Basic, можно использовать группы tooassign доступа tooa приложению SaaS, которое интегрировано с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b722-104">Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups tooassign access tooa SaaS application that's integrated with Azure AD.</span></span> <span data-ttu-id="4b722-105">Например если вы хотите получить доступ tooassign для hello маркетинговый отдел toouse пяти разным приложениям SaaS, можно создать группу, содержащую пользователей hello в отделе маркетинга hello и назначьте этой группе toothese пять приложений SaaS, которые являются требуемые hello отдела маркетинга.</span><span class="sxs-lookup"><span data-stu-id="4b722-105">For example, if you want tooassign access for hello marketing department toouse five different SaaS applications, you can create a group that contains hello users in hello marketing department, and then assign that group toothese five SaaS applications that are needed by hello marketing department.</span></span> <span data-ttu-id="4b722-106">Таким образом можно сэкономить время, управление членством hello объекта hello маркетинг отдела в одном месте.</span><span class="sxs-lookup"><span data-stu-id="4b722-106">This way you can save time by managing hello membership of hello marketing department in one place.</span></span> <span data-ttu-id="4b722-107">Пользователи затем назначаются toohello приложения во время их добавления в качестве членов группы marketing hello и назначениях удалены из приложения hello после их удаления из маркетингового hello.</span><span class="sxs-lookup"><span data-stu-id="4b722-107">Users then are assigned toohello application when they are added as members of hello marketing group, and have their assignments removed from hello application when they are removed from hello marketing group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b722-108">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4b722-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 

<span data-ttu-id="4b722-109">Эту возможность можно использовать с сотнями приложений, которые можно добавить из в hello коллекции приложений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b722-109">This capability can be used with hundreds of applications that you can add from within hello Azure AD Application Gallery.</span></span>

<span data-ttu-id="4b722-110">**tooassign доступ для группы tooa приложения SaaS**</span><span class="sxs-lookup"><span data-stu-id="4b722-110">**tooassign access for a group tooa SaaS application**</span></span>

1. <span data-ttu-id="4b722-111">В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory** на панели навигации hello hello левой стороны.</span><span class="sxs-lookup"><span data-stu-id="4b722-111">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory** on hello navigation bar on hello left hand side.</span></span>
2. <span data-ttu-id="4b722-112">Выберите hello **каталога** вкладку и откройте hello каталог, в котором нужно tooassign доступ для группы tooa приложения SaaS.</span><span class="sxs-lookup"><span data-stu-id="4b722-112">Select hello **Directory** tab, and then open hello directory in which you want tooassign access for a group tooa SaaS application.</span></span>
3. <span data-ttu-id="4b722-113">Выберите hello **приложений** вкладки. Выберите приложение, которое вы добавили из коллекции приложений hello и нажмите кнопку hello **пользователей и групп** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4b722-113">Select hello **Applications** tab. Select an application that you added from hello Application Gallery, and then click  hello **Users and Groups** tab.</span></span>
4. <span data-ttu-id="4b722-114">На hello **пользователей и групп** hello на вкладке **начиная с** введите имя hello hello группы toowhich нужно tooassign доступ, а затем выберите hello флажок в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="4b722-114">On hello **Users and Groups** tab, in hello **Starting with** field, enter hello name of hello group toowhich you want tooassign access, and then select hello check mark in hello upper right.</span></span> <span data-ttu-id="4b722-115">Требуется только tootype hello первую часть имени группы.</span><span class="sxs-lookup"><span data-stu-id="4b722-115">You only need tootype hello first part of a group's name.</span></span>
5. <span data-ttu-id="4b722-116">Выберите группу hello, а затем выберите hello **назначать доступ к** кнопки.</span><span class="sxs-lookup"><span data-stu-id="4b722-116">Select hello group, then then select hello **Assign Access** button.</span></span> <span data-ttu-id="4b722-117">Выберите **Да** при появлении сообщения о подтверждении hello.</span><span class="sxs-lookup"><span data-stu-id="4b722-117">Select **Yes** when you see hello confirmation message.</span></span> <span data-ttu-id="4b722-118">В данный момент вложенных группах не поддерживаются для tooapplications назначения на основе группы.</span><span class="sxs-lookup"><span data-stu-id="4b722-118">Nested group memberships are not supported for group-based assignment tooapplications at this time.</span></span>
6. <span data-ttu-id="4b722-119">Также вы увидите, какие пользователи назначаются приложения toohello напрямую или через членство в группе.</span><span class="sxs-lookup"><span data-stu-id="4b722-119">You can also see which users are assigned toohello application, either directly or by membership in a group.</span></span> <span data-ttu-id="4b722-120">toodo это, измените hello **показывать раскрывающийся список с «Группы»** слишком**«Все пользователи»**.</span><span class="sxs-lookup"><span data-stu-id="4b722-120">toodo this, change hello **Show dropdown from 'Groups'** too**'All Users'**.</span></span> <span data-ttu-id="4b722-121">Hello список пользователей в каталоге hello и ли каждому пользователю назначается toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="4b722-121">hello list shows users in hello directory and whether or not each user is assigned toohello application.</span></span> <span data-ttu-id="4b722-122">Hello также перечислены ли hello назначенных пользователей, назначенных toohello приложению напрямую (тип Inherited «Direct»), или посредством членства в группе (тип Inherited «Inherited.»)</span><span class="sxs-lookup"><span data-stu-id="4b722-122">hello list also shows whether hello assigned users are assigned toohello application directly (assignment type shown as 'Direct'), or by virtue of group membership (assignment type shown as 'Inherited.')</span></span>

> [!NOTE]
> <span data-ttu-id="4b722-123">Вы увидите hello пользователей и группы только после включения Azure AD Premium или Azure AD Basic.</span><span class="sxs-lookup"><span data-stu-id="4b722-123">You can see hello Users and Groups tab only after you have enabled Azure AD Premium or Azure AD Basic.</span></span>
>
>

### <a name="next-steps"></a><span data-ttu-id="4b722-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4b722-124">Next steps</span></span>
<span data-ttu-id="4b722-125">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b722-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="4b722-126">Управление tooresources доступ с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b722-126">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="4b722-127">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b722-127">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="4b722-128">Настройка параметров групп с помощью командлетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b722-128">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="4b722-129">Что такое Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b722-129">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="4b722-130">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b722-130">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
