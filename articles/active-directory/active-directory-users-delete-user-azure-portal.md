---
title: "Удаление пользователя из каталога в Azure Active Directory | Документы Майкрософт"
description: "В этом разделе объясняется, как удалить пользователя и все его данные из Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bd1c9ccc-2d80-42bf-82cc-db37bb1a1d67
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: 19a4d2c37c785b3b56a2e0e1b6797ec56dad9835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-user-from-a-directory-in-azure-active-directory"></a><span data-ttu-id="d6e63-103">Удаление пользователя из каталога в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6e63-103">Delete a user from a directory in Azure Active Directory</span></span>
<span data-ttu-id="d6e63-104">В этой статье объясняется, как удалить пользователя из каталога в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6e63-104">This article explains how to delete a user from a directory in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="d6e63-105">Сведения о добавлении новых пользователей в организации см. в статье [Добавление новых пользователей или пользователей с учетными записями Майкрософт в Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6e63-105">For information about adding new users to your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="to-delete-a-user"></a><span data-ttu-id="d6e63-106">Удаление пользователя</span><span class="sxs-lookup"><span data-stu-id="d6e63-106">To delete a user</span></span>
1. <span data-ttu-id="d6e63-107">Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="d6e63-107">Sign in to [the Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="d6e63-108">Выберите **Больше служб**, введите **Пользователи и группы** в текстовое поле, а затем нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="d6e63-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Открытие страницы "Управление пользователями"](./media/active-directory-users-delete-user-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="d6e63-110">В колонке **Пользователи и группы** выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d6e63-110">On the **Users and groups** blade, select **Users**.</span></span>

   ![Открытие колонки "Пользователи"](./media/active-directory-users-delete-user-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="d6e63-112">В колонке **Пользователи и группы — Пользователи** выберите пользователя из списка.</span><span class="sxs-lookup"><span data-stu-id="d6e63-112">On the **Users and groups - Users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="d6e63-113">В колонке для выбранного пользователя щелкните **Обзор**, а затем на панели команд щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="d6e63-113">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![Выбор команды "Удалить"](./media/active-directory-users-delete-user-azure-portal/create-users-delete-command.png)

## <a name="next-steps"></a><span data-ttu-id="d6e63-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6e63-115">Next steps</span></span>
* [<span data-ttu-id="d6e63-116">Добавление новых пользователей в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6e63-116">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="d6e63-117">Сброс пароля пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6e63-117">Reset the password for a user in Azure Active Directory</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="d6e63-118">Назначение пользователю ролей администратора в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6e63-118">Assign a user to administrator roles in Azure Active Directory</span></span>](active-directory-users-assign-role-azure-portal.md)
* [<span data-ttu-id="d6e63-119">Добавление или изменение данных профиля пользователя в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6e63-119">Add or change profile information for a user in Azure Active Directory</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="d6e63-120">Удаление пользователя из каталога в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6e63-120">Delete a user from a directory in Azure Active Directory</span></span>](active-directory-users-profile-azure-portal.md)
