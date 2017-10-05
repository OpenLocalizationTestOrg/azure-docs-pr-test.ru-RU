---
title: "Добавление новых пользователей в Azure Active Directory | Документация Майкрософт"
description: "Инструкции по добавлению новых пользователей в Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="9e69d-103">Краткое руководство по добавлению новых пользователей в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e69d-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="9e69d-104">В этой статье объясняется, как добавлять новых пользователей в вашей организации в Azure Active Directory (Azure AD) одновременно с помощью портала Azure или синхронизации данных учетной записи пользователя Windows Server AD в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="9e69d-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="9e69d-105">Добавление облачных пользователей</span><span class="sxs-lookup"><span data-stu-id="9e69d-105">Add cloud-based users</span></span>
1. <span data-ttu-id="9e69d-106">Войдите в [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="9e69d-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="9e69d-107">Выберите **Azure Active Directory**, а затем щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9e69d-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="9e69d-108">В колонке **Пользователи и группы** выберите **Все пользователи** и щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="9e69d-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="9e69d-109">![Выбор команды "Добавить"](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="9e69d-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="9e69d-110">Введите сведения о пользователе в соответствующих полях, например **Имя** и **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="9e69d-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="9e69d-111">Частью имени пользователя, представляющей собой доменное имя, должно быть доменное имя по умолчанию, [domain name].onmicrosoft.com, или проверенное доменное имя, не являющееся федеративным, например [настроить доменное имя](add-custom-domain.md) contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9e69d-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="9e69d-112">Скопируйте или иным способом запишите созданный пароль пользователя, чтобы после завершения этого процесса его можно было предоставить пользователю.</span><span class="sxs-lookup"><span data-stu-id="9e69d-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="9e69d-113">При необходимости можно заполнить сведения, открыв колонку **Профиль**, **Группы** или **Роль каталога** для пользователя.</span><span class="sxs-lookup"><span data-stu-id="9e69d-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="9e69d-114">Дополнительные сведения о ролях пользователей и администраторов см. в статье [Назначение ролей администратора в Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9e69d-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="9e69d-115">В колонке **Пользователь** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9e69d-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="9e69d-116">Безопасным способом передайте созданный пароль новому пользователю, чтобы он мог войти в систему.</span><span class="sxs-lookup"><span data-stu-id="9e69d-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="9e69d-117">Вы также можете синхронизировать данные учетной записи пользователя из локальной среды Windows Server AD.</span><span class="sxs-lookup"><span data-stu-id="9e69d-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="9e69d-118">Решения для идентификации Майкрософт обладают локальными и облачными возможностями, создавая единое удостоверение пользователя для проверки подлинности и авторизации для всех ресурсов, независимо от их расположения.</span><span class="sxs-lookup"><span data-stu-id="9e69d-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="9e69d-119">Мы называем это гибридной идентификацией.</span><span class="sxs-lookup"><span data-stu-id="9e69d-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="9e69d-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) можно использовать для интеграции локальных каталогов с Azure Active Directory для сценариев гибридной идентификации.</span><span class="sxs-lookup"><span data-stu-id="9e69d-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="9e69d-121">Таким образом вы сможете предоставить пользователям возможность получать доступ с использованием одного удостоверения для приложений Office 365, Azure и программного обеспечения как услуги (SaaS), интегрированных с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e69d-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="9e69d-122">Удалить пользователей из Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e69d-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="9e69d-123">Войдите в [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с помощью учетной записи глобального администратора каталога.</span><span class="sxs-lookup"><span data-stu-id="9e69d-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="9e69d-124">Выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9e69d-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="9e69d-125">В колонке **Пользователи и группы** выберите пользователя, которого необходимо удалить из списка.</span><span class="sxs-lookup"><span data-stu-id="9e69d-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="9e69d-126">В колонке для выбранного пользователя щелкните **Обзор**, а затем на панели команд щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="9e69d-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="9e69d-127">![Выбор команды "Добавить"](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="9e69d-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="9e69d-128">Подробнее</span><span class="sxs-lookup"><span data-stu-id="9e69d-128">Learn more</span></span> 
* [<span data-ttu-id="9e69d-129">Добавление внешнего пользователя</span><span class="sxs-lookup"><span data-stu-id="9e69d-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="9e69d-130">Назначение пользователей в предварительной версии Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e69d-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="9e69d-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e69d-131">Next steps</span></span>
<span data-ttu-id="9e69d-132">В этом кратком руководстве описано, как добавить личный домен в Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="9e69d-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="9e69d-133">Чтобы создать личный домен в Azure AD с портала Azure, воспользуйтесь следующей ссылкой.</span><span class="sxs-lookup"><span data-stu-id="9e69d-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e69d-134">Добавление пользователей в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e69d-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 