---
title: "aaaDedicated группы в Azure Active Directory | Документы Microsoft"
description: "Обзор работы выделенных групп в Azure Active Directory и способов их создания."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a><span data-ttu-id="25d34-103">Выделенные группы в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25d34-103">Dedicated groups in Azure Active Directory</span></span>
<span data-ttu-id="25d34-104">В Azure Active Directory (Azure AD) функция выделенные группы hello автоматически создает и заполняет членство группы Azure AD предопределенные.</span><span class="sxs-lookup"><span data-stu-id="25d34-104">In Azure Active Directory (Azure AD), hello dedicated groups feature automatically creates and populates membership for Azure AD predefined groups.</span></span> <span data-ttu-id="25d34-105">Не удается добавить элементы выделенных групп или удален с помощью hello Azure классического портала, командлеты Windows PowerShell или программно.</span><span class="sxs-lookup"><span data-stu-id="25d34-105">Members of dedicated groups cannot be added or removed using hello Azure classic portal, Windows PowerShell cmdlets, or programmatically.</span></span>

> [!NOTE]
> <span data-ttu-id="25d34-106">Выделенные группы требуют назначения лицензии Azure AD Premium:</span><span class="sxs-lookup"><span data-stu-id="25d34-106">Dedicated groups require that an Azure AD Premium license is assigned to</span></span>
>
> * <span data-ttu-id="25d34-107">Здравствуйте, администратор, ответственный за управление hello правила в группе</span><span class="sxs-lookup"><span data-stu-id="25d34-107">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="25d34-108">все пользователи, которые выбираются hello правило toobe является членом группы hello</span><span class="sxs-lookup"><span data-stu-id="25d34-108">all users who are selected by hello rule toobe a member of hello group</span></span>
>
>

<span data-ttu-id="25d34-109">**tooenable выделенной группы**</span><span class="sxs-lookup"><span data-stu-id="25d34-109">**tooenable dedicated groups**</span></span>

1. <span data-ttu-id="25d34-110">В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем откройте каталог вашей организации.</span><span class="sxs-lookup"><span data-stu-id="25d34-110">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.</span></span>
2. <span data-ttu-id="25d34-111">Выберите hello **группы** вкладку и откройте hello группу tooedit.</span><span class="sxs-lookup"><span data-stu-id="25d34-111">Select hello **Groups** tab, and then open hello group you want tooedit.</span></span>
3. <span data-ttu-id="25d34-112">Выберите hello **Настройка** и затем задайте **Включить выделенные группы** слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="25d34-112">Select hello **Configure** tab, and then set **Enable Dedicated Groups** too**Yes**.</span></span>

<span data-ttu-id="25d34-113">После переключения включить целевые группы hello слишком**Да**, можно дополнительно включить hello directory tooautomatically создать hello всех пользователей, отдельная группа, задание hello **«Все пользователи» включить группы** Переключение слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="25d34-113">Once hello Enable Dedicated Groups switch is set too**Yes**, you can further enable hello directory tooautomatically create hello All Users dedicated group by setting hello **Enable “All Users” Group** switch too**Yes**.</span></span> <span data-ttu-id="25d34-114">Вы также можно отредактировать имя этой целевой группы hello, введя его в hello **отображаемое имя для «Все пользователи» группа** поля.</span><span class="sxs-lookup"><span data-stu-id="25d34-114">You can then also edit hello name of this dedicated group by typing it in hello **Display Name for “All Users” Group** field.</span></span>

<span data-ttu-id="25d34-115">можно использовать группы все пользователи Hello tooassign hello и те же разрешения tooall hello пользователи в вашем каталоге.</span><span class="sxs-lookup"><span data-stu-id="25d34-115">hello All Users group can be used tooassign hello same permissions tooall hello users in your directory.</span></span> <span data-ttu-id="25d34-116">Например можно предоставить всем пользователям в ваш каталог доступа tooa приложения SaaS, назначив доступ для всех пользователей отдельная группа toothis приложения hello.</span><span class="sxs-lookup"><span data-stu-id="25d34-116">For example, you can grant all users in your directory access tooa SaaS application by assigning access for hello All Users dedicated group toothis application.</span></span>

<span data-ttu-id="25d34-117">Hello выделенной группы все пользователи входят все пользователи в каталоге hello, включая гостей и внешних пользователей.</span><span class="sxs-lookup"><span data-stu-id="25d34-117">hello dedicated All Users group includes all users in hello directory, including guests and external users.</span></span> <span data-ttu-id="25d34-118">Если требуется группа, исключает внешних пользователей, то это можно сделать, создав группу с основанное на атрибутах динамическое правило hello ниже:</span><span class="sxs-lookup"><span data-stu-id="25d34-118">If you need a group that excludes external users, then you can accomplish this by creating a group with an attribute-based dynamic rule such as hello following:</span></span>

                (user.userPrincipalName -notContains "#EXT#@")

<span data-ttu-id="25d34-119">Группы, который исключает всем гостевым системам используйте правило, например hello следующее:</span><span class="sxs-lookup"><span data-stu-id="25d34-119">For a group that excludes all Guests, use a rule such as hello following:</span></span>

                (user.userType -ne "Guest")

<span data-ttu-id="25d34-120">toolearn о том, как toocreate *Дополнительно* правил (правил, которые может содержать несколько сравнения) динамическое членство в группе, в разделе [с помощью атрибутов toocreate расширенные правила](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="25d34-120">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="25d34-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25d34-121">Next steps</span></span>
<span data-ttu-id="25d34-122">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="25d34-122">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="25d34-123">Управление tooresources доступ с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25d34-123">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="25d34-124">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25d34-124">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="25d34-125">Что такое Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25d34-125">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="25d34-126">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25d34-126">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
