---
title: "aaaManaging группы в Azure Active Directory | Документы Microsoft"
description: "Как toocreate и управление группами toomanage Azure пользователей с помощью Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="8bbdd-103">Управление группами в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bbdd-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bbdd-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="8bbdd-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="8bbdd-105">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="8bbdd-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="8bbdd-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bbdd-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="8bbdd-107">Одна из функций hello управления пользователя Azure Active Directory (Azure AD) — hello возможность toocreate групп пользователей.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-107">One of hello features of Azure Active Directory (Azure AD) user management is hello ability toocreate groups of users.</span></span> <span data-ttu-id="8bbdd-108">Можно использовать задачи управления tooperform группы, например назначение лицензии или разрешения tooa число пользователей, одновременно.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-108">You use a group tooperform management tasks such as assigning licenses or permissions tooa number of users at once.</span></span> <span data-ttu-id="8bbdd-109">Можно также использовать разрешения на доступ к tooassign групп</span><span class="sxs-lookup"><span data-stu-id="8bbdd-109">You can also use groups tooassign access permission to</span></span>

* <span data-ttu-id="8bbdd-110">Ресурсы, такие как объекты в каталоге hello</span><span class="sxs-lookup"><span data-stu-id="8bbdd-110">Resources such as objects in hello directory</span></span>
* <span data-ttu-id="8bbdd-111">Каталог внешних toohello ресурсы, например приложений SaaS, служб Azure, сайтов SharePoint или локальных ресурсов</span><span class="sxs-lookup"><span data-stu-id="8bbdd-111">Resources external toohello directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="8bbdd-112">Кроме того владелец ресурса можно также назначить группу доступа tooa ресурсов tooan Azure AD с принадлежит другому пользователю.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-112">In addition, a resource owner can also assign access tooa resource tooan Azure AD group owned by someone else.</span></span> <span data-ttu-id="8bbdd-113">Это назначение предоставляет hello члены этой группы доступа toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-113">This assignment grants hello members of that group access toohello resource.</span></span> <span data-ttu-id="8bbdd-114">Затем hello владельца группы hello управляет членством в группе hello.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-114">Then, hello owner of hello group manages membership in hello group.</span></span> <span data-ttu-id="8bbdd-115">По сути hello ресурсов владельца делегаты toohello владелец hello группы hello разрешение tooassign пользователей tootheir ресурса.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-115">Effectively, hello resource owner delegates toohello owner of hello group hello permission tooassign users tootheir resource.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8bbdd-116">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-116">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="8bbdd-117">Сопоставление toomanage групп в центре администрирования hello Azure AD, в разделе [Создание группы и добавление членов в Azure Active Directory](active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8bbdd-117">For how toomanage groups in hello Azure AD admin center, see [Create a group and add members in Azure Active Directory](active-directory-groups-create-azure-portal.md).</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="8bbdd-118">Как создать группу?</span><span class="sxs-lookup"><span data-stu-id="8bbdd-118">How do I create a group?</span></span>
<span data-ttu-id="8bbdd-119">В зависимости от hello toowhich служб, которые подписана ваша организация можно создать группу, с помощью одного из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="8bbdd-119">Depending on hello services toowhich your organization has subscribed, you can create a group using one of hello following:</span></span>

* <span data-ttu-id="8bbdd-120">Hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="8bbdd-120">hello Azure classic portal</span></span>
* <span data-ttu-id="8bbdd-121">портал учетной записи Office 365 Hello</span><span class="sxs-lookup"><span data-stu-id="8bbdd-121">hello Office 365 account portal</span></span>
* <span data-ttu-id="8bbdd-122">портал учетных записей Windows Intune Hello</span><span class="sxs-lookup"><span data-stu-id="8bbdd-122">hello Windows Intune account portal</span></span>

<span data-ttu-id="8bbdd-123">Мы опишем задачи, как выполнять в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-123">We'll describe tasks as performed in hello Azure classic portal.</span></span> <span data-ttu-id="8bbdd-124">Дополнительные сведения об использовании toomanage порталы без использования Azure каталога Azure AD см. в разделе [администрирование каталога Azure AD](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="8bbdd-124">For more information about using non-Azure portals toomanage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="8bbdd-125">В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем выберите имя hello hello каталога для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-125">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="8bbdd-126">Выберите hello **группы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-126">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="8bbdd-127">Выберите **Добавить группу**.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-127">Select **Add Group**.</span></span>
4. <span data-ttu-id="8bbdd-128">В hello **добавить группу** окне укажите имя hello и hello описания группы.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-128">In hello **Add Group** window, specify hello name and hello description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="8bbdd-129">Как назначить пользователей в группу безопасности или удалить их из такой группы</span><span class="sxs-lookup"><span data-stu-id="8bbdd-129">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="8bbdd-130">**tooadd группы tooa отдельного пользователя**</span><span class="sxs-lookup"><span data-stu-id="8bbdd-130">**tooadd an individual user tooa group**</span></span>

1. <span data-ttu-id="8bbdd-131">В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем выберите имя hello hello каталога для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-131">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="8bbdd-132">Выберите hello **группы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-132">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="8bbdd-133">Откройте toowhich группы hello tooadd члены.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-133">Open hello group toowhich you want tooadd members.</span></span> <span data-ttu-id="8bbdd-134">Откройте hello **члены** вкладке hello выбранную группу, если он еще не отображается.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-134">Open hello **Members** tab of hello selected group if it not already displaying.</span></span>
4. <span data-ttu-id="8bbdd-135">Выберите **Добавить участников**.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-135">Select **Add Members**.</span></span>
5. <span data-ttu-id="8bbdd-136">На hello **добавить членов** страницу, выберите hello имя hello пользователю или группе, что tooadd должен быть членом этой группы.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-136">On hello **Add Members** page, select hello name of hello user or a group that you want tooadd as a member of this group.</span></span> <span data-ttu-id="8bbdd-137">Убедитесь, что это имя добавлено toohello **выбранные** области.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-137">Make sure that this name is added toohello **Selected** pane.</span></span>

<span data-ttu-id="8bbdd-138">**tooremove отдельного пользователя из группы**</span><span class="sxs-lookup"><span data-stu-id="8bbdd-138">**tooremove an individual user from a group**</span></span>

1. <span data-ttu-id="8bbdd-139">В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем выберите имя hello hello каталога для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-139">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="8bbdd-140">Выберите hello **группы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-140">Select hello **Groups** tab.</span></span>
3. <span data-ttu-id="8bbdd-141">Откройте группу hello, из которого нужно tooremove члены.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-141">Open hello group from which you want tooremove members.</span></span>
4. <span data-ttu-id="8bbdd-142">Выберите hello **элементы** вкладка, выберите hello имя члена hello требуется tooremove из этой группы и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-142">Select hello **Members** tab, select hello name of hello member that you want tooremove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="8bbdd-143">Подтвердите в строке приветствия tooremove этого члена из группы hello.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-143">Confirm at hello prompt that you want tooremove this member from hello group.</span></span>

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a><span data-ttu-id="8bbdd-144">Как управлять hello членство в группе динамически</span><span class="sxs-lookup"><span data-stu-id="8bbdd-144">How can I manage hello membership of a group dynamically?</span></span>
<span data-ttu-id="8bbdd-145">В Azure AD можно очень легко настроить toodetermine простое правило, какие пользователи являются членами toobe группы hello.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-145">In Azure AD, you can very easily set up a simple rule toodetermine which users are toobe members of hello group.</span></span> <span data-ttu-id="8bbdd-146">(правило, которое содержит только одно сравнение).</span><span class="sxs-lookup"><span data-stu-id="8bbdd-146">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="8bbdd-147">Например если группа назначается tooa приложения SaaS, настройкой правило tooadd пользователей, имеющих должность «Торговый представитель».</span><span class="sxs-lookup"><span data-stu-id="8bbdd-147">For example, if a group is assigned tooa SaaS application, you can set up a rule tooadd users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="8bbdd-148">Это правило затем предоставляет доступ пользователей tooall приложений SaaS toothis данной должности в вашем каталоге.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-148">This rule then grants access toothis SaaS application tooall users with that job title in your directory.</span></span>

<span data-ttu-id="8bbdd-149">Когда какие-либо атрибуты изменения пользователя hello система оценивает все правила динамическую группу в toosee каталог, если изменение атрибута hello hello пользователя приведет к запуску любую группу добавляет или удаляет.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-149">When any attributes of a user change, hello system evaluates all dynamic group rules in a directory toosee if hello attribute change of hello user would trigger any group adds or removes.</span></span> <span data-ttu-id="8bbdd-150">Если пользователь не соответствует правилу в группе, они добавляются в группу toothat член.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-150">If a user satisfies a rule on a group, they are added as a member toothat group.</span></span> <span data-ttu-id="8bbdd-151">Если они больше не удовлетворяют правилу hello, за которые она является членом группы, они удаляются как члены из этой группы.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-151">If they no longer satisfy hello rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> <span data-ttu-id="8bbdd-152">Вы можете настроить правило динамического членства для групп безопасности или групп Office 365.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-152">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="8bbdd-153">Вложенных группах сейчас не поддерживаются для tooapplications назначения на основе группы.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-153">Nested group memberships aren't currently supported for group-based assignment tooapplications.</span></span>
>
> <span data-ttu-id="8bbdd-154">Динамическое членство в группе требуется toobe лицензии Azure AD Premium, назначенные</span><span class="sxs-lookup"><span data-stu-id="8bbdd-154">Dynamic memberships for groups require an Azure AD Premium license toobe assigned to</span></span>
>
> * <span data-ttu-id="8bbdd-155">Здравствуйте, администратор, ответственный за управление hello правила в группе</span><span class="sxs-lookup"><span data-stu-id="8bbdd-155">hello administrator who manages hello rule on a group</span></span>
> * <span data-ttu-id="8bbdd-156">Все члены группы hello</span><span class="sxs-lookup"><span data-stu-id="8bbdd-156">All members of hello group</span></span>
>
>

<span data-ttu-id="8bbdd-157">**tooenable динамическое членство в группе**</span><span class="sxs-lookup"><span data-stu-id="8bbdd-157">**tooenable dynamic membership for a group**</span></span>

1. <span data-ttu-id="8bbdd-158">В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем выберите имя hello hello каталога для вашей организации.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-158">In hello [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select hello name of hello directory for your organization.</span></span>
2. <span data-ttu-id="8bbdd-159">Выберите hello **группы** вкладка и группа Привет открыть требуется tooedit.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-159">Select hello **Groups** tab, and open hello group you want tooedit.</span></span>
3. <span data-ttu-id="8bbdd-160">Выберите hello **Настройка** и затем задайте **включить динамическое членство** слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-160">Select hello **Configure** tab, and then set **Enable Dynamic Memberships** too**Yes**.</span></span>
4. <span data-ttu-id="8bbdd-161">Настроить простое единое правило для группы toocontrol hello динамического членства для этой группы функций.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-161">Set up a simple single rule for hello group toocontrol how dynamic membership for this group functions.</span></span> <span data-ttu-id="8bbdd-162">Убедитесь, что hello **добавить пользователей где** параметр выбран, затем выберите свойство пользователя из списка hello (например, отдел, должность, и т. д.)</span><span class="sxs-lookup"><span data-stu-id="8bbdd-162">Make sure hello **Add users where** option is selected, and then select a user property from hello list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="8bbdd-163">После этого выберите условие ("Не равно", "Равно", "Не начинается с", "Начинается с", "Не содержит", "Содержит", "Не соответствует", "Соответствует").</span><span class="sxs-lookup"><span data-stu-id="8bbdd-163">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="8bbdd-164">Укажите значение для сравнения для hello выбранного свойства пользователя.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-164">Specify a comparison value for hello selected user property.</span></span>

<span data-ttu-id="8bbdd-165">toolearn о том, как toocreate *Дополнительно* правил (правил, которые может содержать несколько сравнения) динамическое членство в группе, в разделе [с помощью атрибутов toocreate расширенные правила](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="8bbdd-165">toolearn about how toocreate *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes toocreate advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="8bbdd-166">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="8bbdd-166">Additional information</span></span>
<span data-ttu-id="8bbdd-167">В следующих статьях содержатся дополнительные сведения об Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8bbdd-167">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="8bbdd-168">Управление tooresources доступ с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bbdd-168">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="8bbdd-169">Настройка параметров групп с помощью командлетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bbdd-169">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="8bbdd-170">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bbdd-170">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="8bbdd-171">Что такое Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bbdd-171">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="8bbdd-172">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8bbdd-172">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
