---
title: "Приступая к работе с управлением привилегированными пользователями Azure AD | Документация Майкрософт"
description: "Сведения о том, как управлять привилегированными удостоверениями с помощью приложения для управления привилегированными пользователями Azure Active Directory на портале Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="faab0-103">Приступая к использованию Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="faab0-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="faab0-104">С помощью управления привилегированными пользователями в Azure Active Directory (AD) можно администрировать, контролировать и отслеживать доступ в пределах организации,</span><span class="sxs-lookup"><span data-stu-id="faab0-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="faab0-105">в том числе доступ к ресурсам в Azure AD и остальным веб-службам Microsoft, таким как Office 365 или Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="faab0-105">This scope includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="faab0-106">В этой статье рассказывается, как добавить приложение Azure AD PIM на панель мониторинга портала Azure.</span><span class="sxs-lookup"><span data-stu-id="faab0-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="faab0-107">Добавление приложения для управления привилегированными пользователями</span><span class="sxs-lookup"><span data-stu-id="faab0-107">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="faab0-108">Прежде чем вы сможете работать с приложением для управления привилегированными пользователями Azure AD, его необходимо добавить на панель мониторинга портала Azure.</span><span class="sxs-lookup"><span data-stu-id="faab0-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="faab0-109">Войдите на [портал Azure](https://portal.azure.com/) как глобальный администратор нужного каталога.</span><span class="sxs-lookup"><span data-stu-id="faab0-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="faab0-110">Если в организации имеется несколько каталогов, выберите свое имя пользователя в правом верхнем углу на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="faab0-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="faab0-111">Выберите каталог, где необходимо использовать PIM.</span><span class="sxs-lookup"><span data-stu-id="faab0-111">Select the directory where you want to use PIM.</span></span>
3. <span data-ttu-id="faab0-112">Выберите **Другие службы** и в текстовое поле "Фильтр" введите **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="faab0-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="faab0-113">Установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="faab0-113">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="faab0-114">Откроется приложение Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="faab0-114">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="faab0-115">Если вы первый пользователь, использующий Azure Active Directory Privileged Identity Management в каталоге, вам автоматически назначаются роли **Администратор безопасности** и **Администратор привилегированных ролей** в этом каталоге.</span><span class="sxs-lookup"><span data-stu-id="faab0-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, you are automatically assigned the **Security administrator** and **Privileged role administrator** roles in the directory.</span></span> <span data-ttu-id="faab0-116">Только администраторы привилегированных ролей могут управлять назначением ролей пользователей.</span><span class="sxs-lookup"><span data-stu-id="faab0-116">Only privileged role administrators can manage role assignments of users.</span></span> <span data-ttu-id="faab0-117">Кроме того, вы можете запустить [мастер защиты](active-directory-privileged-identity-management-security-wizard.md),</span><span class="sxs-lookup"><span data-stu-id="faab0-117">In addition, you may choose to run the [security wizard.](active-directory-privileged-identity-management-security-wizard.md)</span></span> <span data-ttu-id="faab0-118">который поможет вам выполнить первое обнаружение и назначение.</span><span class="sxs-lookup"><span data-stu-id="faab0-118">that walks you through the initial discovery and assignment experience.</span></span>

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="faab0-119">Переход к задачам</span><span class="sxs-lookup"><span data-stu-id="faab0-119">Navigate to your tasks</span></span>
<span data-ttu-id="faab0-120">После настройки приложения Azure AD Privileged Identity Management при каждом его запуске будет отображаться колонка навигации.</span><span class="sxs-lookup"><span data-stu-id="faab0-120">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span> <span data-ttu-id="faab0-121">Ее можно использовать для выполнения задач по управлению пользователями.</span><span class="sxs-lookup"><span data-stu-id="faab0-121">Use this blade to accomplish your identity management tasks.</span></span>

![Задачи верхнего уровня для управления привилегированными пользователями — снимок экрана](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* <span data-ttu-id="faab0-123">В разделе **Мои роли** приведен список назначенных вам ролей.</span><span class="sxs-lookup"><span data-stu-id="faab0-123">**My Roles** takes you to a list of roles that are assigned to you.</span></span> <span data-ttu-id="faab0-124">Здесь можно активировать любую назначенную вам роль.</span><span class="sxs-lookup"><span data-stu-id="faab0-124">This section is where you activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="faab0-125">В разделе **Approve Requests (Preview)** (Утверждение запросов (предварительная версия)) приведен список ожидающих запросов на активацию от пользователей в каталоге.</span><span class="sxs-lookup"><span data-stu-id="faab0-125">**Approve Requests (Preview)** displays a list of pending activation requests from users in your directory.</span></span> [<span data-ttu-id="faab0-126">Подробнее.</span><span class="sxs-lookup"><span data-stu-id="faab0-126">Learn more.</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* <span data-ttu-id="faab0-127">В разделе **Pending Requests (Preview)** (Запросы в ожидании (предварительная версия)) отображаются все запросы, ожидающие активации.</span><span class="sxs-lookup"><span data-stu-id="faab0-127">**Pending Requests (Preview)** displays any current requests to have made to activate.</span></span>
* <span data-ttu-id="faab0-128">Раздел **Проверка доступа** перенаправляет вас к незавершенным проверкам доступа (для себя или для кого-то другого), которые нужно завершить.</span><span class="sxs-lookup"><span data-stu-id="faab0-128">**Review Access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span></span>
* <span data-ttu-id="faab0-129">Параметр **Роли каталога Azure AD** расположен в разделе "Управление". Это панель мониторинга, где администраторы привилегированных ролей могут управлять назначением ролей, изменять параметры активации роли, выполнять проверки доступа и многое другое.</span><span class="sxs-lookup"><span data-stu-id="faab0-129">**Azure AD Directory Roles** located under the 'Manage' section is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="faab0-130">Параметры на этой панели мониторинга отключены для всех, кто не является администратором привилегированных ролей.</span><span class="sxs-lookup"><span data-stu-id="faab0-130">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="faab0-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="faab0-131">Next steps</span></span>
<span data-ttu-id="faab0-132">В разделе, посвященном [обзору управления привилегированными пользователями Azure AD](active-directory-privileged-identity-management-configure.md) , содержатся дополнительные сведения об управлении административным доступом в организации.</span><span class="sxs-lookup"><span data-stu-id="faab0-132">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
