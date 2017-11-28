---
title: "aaaAdd tooAzure новых пользователей Active Directory | Документы Microsoft"
description: "Объясняет, как tooadd новых пользователей или изменение сведений о пользователе в Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="cfa65-103">Добавление новых пользователей или пользователей с учетными записями Microsoft tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfa65-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="cfa65-104">Добавьте каталог toopopulate пользователей.</span><span class="sxs-lookup"><span data-stu-id="cfa65-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="cfa65-105">В этой статье объясняется, как tooadd новых пользователей в вашей организации и как tooadd пользователей, имеющих учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cfa65-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="cfa65-106">Дополнительные сведения о добавлении пользователей из других каталогов в Azure Active Directory или пользователей из компаний-партнеров см. в статье [Добавление пользователей из других каталогов или компаний-партнеров в Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="cfa65-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="cfa65-107">Добавленные пользователи нет прав администратора по умолчанию, но можно назначить роли toothem в любое время.</span><span class="sxs-lookup"><span data-stu-id="cfa65-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfa65-108">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cfa65-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="cfa65-109">Для tooadd пользователей в центре администрирования hello Azure AD, в статье [добавлять новых пользователей tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cfa65-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="cfa65-110">Добавление пользователя</span><span class="sxs-lookup"><span data-stu-id="cfa65-110">Add a user</span></span>
1. <span data-ttu-id="cfa65-111">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="cfa65-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="cfa65-112">Выберите **Active Directory**, а затем выберите hello имя каталога вашей организации.</span><span class="sxs-lookup"><span data-stu-id="cfa65-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="cfa65-113">Выберите hello **пользователей** вкладку и выберите на панели команд hello, **добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="cfa65-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="cfa65-114">На hello **сообщите нам об этом пользователе** в разделе **тип пользователя**, выберите пункт:</span><span class="sxs-lookup"><span data-stu-id="cfa65-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="cfa65-115">**Новый пользователь в вашей организации** — создает новую учетную запись пользователя в каталоге.</span><span class="sxs-lookup"><span data-stu-id="cfa65-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="cfa65-116">**Пользователь с существующей учетной записью Майкрософт** — Добавляет существующий Microsoft потребителей учетной записи tooyour каталог (например, учетная запись Outlook)</span><span class="sxs-lookup"><span data-stu-id="cfa65-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="cfa65-117">В зависимости от **типа пользователя**введите имя пользователя (для нового пользователя) или адрес электронной почты (для пользователей с учетной записью Майкрософт).</span><span class="sxs-lookup"><span data-stu-id="cfa65-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="cfa65-118">На пользователя hello **профиль** укажите имя и фамилия, понятное имя и роль пользователя из hello **ролей** списка.</span><span class="sxs-lookup"><span data-stu-id="cfa65-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="cfa65-119">Дополнительные сведения о ролях пользователей и администраторов см. в статье [Назначение ролей администратора в Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="cfa65-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="cfa65-120">Укажите ли слишком**включить многофакторную проверку подлинности** для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="cfa65-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="cfa65-121">На hello **получение временного пароля** выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="cfa65-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cfa65-122">Если ваша организация использует несколько доменов, необходимо знать о hello, при добавлении учетной записи пользователя, следующие проблемы:</span><span class="sxs-lookup"><span data-stu-id="cfa65-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="cfa65-123">учетные записи пользователей tooadd с hello того же основного имени пользователя (UPN) в доменах, **первый** добавить, например, geoffgrisso@contoso.onmicrosoft.com, **следуют** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="cfa65-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="cfa65-124">**Не** добавляйте geoffgrisso@contoso.com, пока не добавите geoffgrisso@contoso.onmicrosoft.com. Этот порядок важен, может быть сложно tooundo.</span><span class="sxs-lookup"><span data-stu-id="cfa65-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="cfa65-125">Изменение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="cfa65-125">Change user information</span></span>
<span data-ttu-id="cfa65-126">Вы можете изменить любой атрибут пользователя, за исключением идентификатор hello объекта.</span><span class="sxs-lookup"><span data-stu-id="cfa65-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="cfa65-127">Откройте свой каталог.</span><span class="sxs-lookup"><span data-stu-id="cfa65-127">Open your directory.</span></span>
2. <span data-ttu-id="cfa65-128">Выберите hello **пользователей** вкладку и выберите hello отображаемым именем hello нужного toochange пользователя.</span><span class="sxs-lookup"><span data-stu-id="cfa65-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="cfa65-129">Внесите необходимые изменения и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cfa65-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="cfa65-130">Если hello пользователя, который происходит изменение синхронизируется с локальной службой Active Directory, нельзя изменить сведения о пользователе hello, выполнив следующую процедуру.</span><span class="sxs-lookup"><span data-stu-id="cfa65-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="cfa65-131">пользователь toochange hello, используйте средства управления Active Directory в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="cfa65-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="cfa65-132">Управление гостевыми пользователями и ограничения</span><span class="sxs-lookup"><span data-stu-id="cfa65-132">Guest user management and limitations</span></span>
<span data-ttu-id="cfa65-133">Гостевой учетной записи — это пользователи из других каталогов, являвшиеся приглашенных tooyour directory tooaccess SharePoint документы, приложения или другим ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="cfa65-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="cfa65-134">Учетная запись гостя в каталоге его базового UserType атрибут имеет значение слишком «Guest.»</span><span class="sxs-lookup"><span data-stu-id="cfa65-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="cfa65-135">Обычные пользователи (в частности, члены своего каталога) атрибутом hello UserType «Member».</span><span class="sxs-lookup"><span data-stu-id="cfa65-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="cfa65-136">Гости обладают ограниченным набором прав в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="cfa65-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="cfa65-137">Эти права ограничивают возможность гостей toodiscover сведения о других пользователях в каталоге hello hello.</span><span class="sxs-lookup"><span data-stu-id="cfa65-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="cfa65-138">Однако гостевые пользователи по-прежнему могут взаимодействовать с hello пользователей и групп, связанных с hello ресурсы, которые они выполняют.</span><span class="sxs-lookup"><span data-stu-id="cfa65-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="cfa65-139">Гости могут:</span><span class="sxs-lookup"><span data-stu-id="cfa65-139">Guest users can:</span></span>

* <span data-ttu-id="cfa65-140">Видеть других пользователей и групп, связанных с toowhich подписки Azure, которому они предназначены</span><span class="sxs-lookup"><span data-stu-id="cfa65-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="cfa65-141">Просмотреть элементы hello объекта toowhich групп, которые они входят</span><span class="sxs-lookup"><span data-stu-id="cfa65-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="cfa65-142">Поиск пользователей в каталоге hello, если они знают hello полный адрес электронной почты пользователя hello</span><span class="sxs-lookup"><span data-stu-id="cfa65-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="cfa65-143">Видеть только ограниченный набор атрибутов hello пользователей, которым они поиска — ограниченный toodisplay имя, адрес электронной почты, имя участника-пользователя (UPN) и эскиз фотографии</span><span class="sxs-lookup"><span data-stu-id="cfa65-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="cfa65-144">Получить список проверенных доменов в каталоге hello</span><span class="sxs-lookup"><span data-stu-id="cfa65-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="cfa65-145">Здравствуйте, tooapplications согласия, предоставляя им доступа к тому же, в каталоге есть члены</span><span class="sxs-lookup"><span data-stu-id="cfa65-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="cfa65-146">Настройка политик доступа гостевых пользователей</span><span class="sxs-lookup"><span data-stu-id="cfa65-146">Set guest user access policies</span></span>
<span data-ttu-id="cfa65-147">Hello **Настройка** каталога включает параметры toocontrol доступ для гостевых пользователей.</span><span class="sxs-lookup"><span data-stu-id="cfa65-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="cfa65-148">Эти параметры может изменить только глобальный администратор каталога на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="cfa65-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="cfa65-149">Сейчас это нельзя сделать с помощью PowerShell или API.</span><span class="sxs-lookup"><span data-stu-id="cfa65-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="cfa65-150">tooopen hello **Настройка** вкладке hello Azure классического портала, выберите **Active Directory**, а затем выберите имя каталога, hello hello.</span><span class="sxs-lookup"><span data-stu-id="cfa65-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Вкладка "Настройка" в Azure Active Directory][1]

<span data-ttu-id="cfa65-152">Затем можно изменить доступ toocontrol hello параметры для гостевых пользователей.</span><span class="sxs-lookup"><span data-stu-id="cfa65-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![параметры контроля доступа для гостевых пользователей][2]

## <a name="whats-next"></a><span data-ttu-id="cfa65-154">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="cfa65-154">What's next</span></span>
* [<span data-ttu-id="cfa65-155">Добавление пользователей из других каталогов или компаний-партнеров в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfa65-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="cfa65-156">Администрирование Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfa65-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="cfa65-157">Управление паролями в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfa65-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="cfa65-158">Управление группами в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfa65-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
