---
title: "aaaAdd tooAzure новых пользователей Active Directory | Документы Microsoft"
description: "Объясняет, как tooadd новых пользователей в Azure Active Directory."
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
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="95e16-103">Краткое руководство: Добавление новых пользователей tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="95e16-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="95e16-104">В этой статье объясняется, как tooadd новых пользователей в вашей организации в Azure Active Directory (Azure AD) hello один одновременно с помощью hello портал Azure или путем синхронизации локальных пользователей Windows Server AD учетной записи данных.</span><span class="sxs-lookup"><span data-stu-id="95e16-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="95e16-105">Добавление облачных пользователей</span><span class="sxs-lookup"><span data-stu-id="95e16-105">Add cloud-based users</span></span>
1. <span data-ttu-id="95e16-106">Войдите в toohello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="95e16-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="95e16-107">Выберите **Azure Active Directory**, а затем щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="95e16-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="95e16-108">На hello **пользователей и групп** колонке выберите **всех пользователей**, а затем выберите **нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="95e16-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="95e16-109">![При выборе команды Добавить hello](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="95e16-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="95e16-110">Введите сведения для пользователя hello, таких как **имя** и **имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="95e16-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="95e16-111">Hello часть имени домена имя пользователя hello должны быть hello начальное значение по умолчанию домена имя «[домен].onmicrosoft.com» или проверенных, не являющихся федеративными [пользовательское имя домена](add-custom-domain.md) например «contoso.com».</span><span class="sxs-lookup"><span data-stu-id="95e16-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="95e16-112">Копирование или в противном случае Примечание hello создать пароль пользователя, таким образом, чтобы можно предоставить его toohello пользователя после завершения этого процесса.</span><span class="sxs-lookup"><span data-stu-id="95e16-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="95e16-113">При необходимости можно открыть и заполните сведения hello в hello **профиль** колонки, hello **группы** колонке или hello **роли каталога** колонку для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="95e16-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="95e16-114">Дополнительные сведения о ролях пользователей и администраторов см. в статье [Назначение ролей администратора в Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="95e16-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="95e16-115">На hello **пользователя** колонке выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="95e16-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="95e16-116">Безопасно распространите hello созданный пароль toohello нового пользователя, чтобы hello пользователь сможет войти в.</span><span class="sxs-lookup"><span data-stu-id="95e16-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="95e16-117">Вы также можете синхронизировать данные учетной записи пользователя из локальной среды Windows Server AD.</span><span class="sxs-lookup"><span data-stu-id="95e16-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="95e16-118">Решения по управлению удостоверениями корпорации Майкрософт используют локальных и облачных, возможности создания удостоверения одного пользователя для проверки подлинности и авторизации tooall ресурсов, независимо от расположения.</span><span class="sxs-lookup"><span data-stu-id="95e16-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="95e16-119">Мы называем это гибридной идентификацией.</span><span class="sxs-lookup"><span data-stu-id="95e16-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="95e16-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) может быть используется toointegrate локальных каталогов с Azure Active Directory для гибридных удостоверений сценариев.</span><span class="sxs-lookup"><span data-stu-id="95e16-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="95e16-121">Это позволяет tooprovide общего удостоверения для пользователей для приложений Office 365, Azure и SaaS интегрированы с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="95e16-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="95e16-122">Удалить пользователей из Azure AD</span><span class="sxs-lookup"><span data-stu-id="95e16-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="95e16-123">Войдите в toohello [Центр администрирования Azure Active Directory](https://aad.portal.azure.com) с помощью учетной записи глобального администратора каталога hello.</span><span class="sxs-lookup"><span data-stu-id="95e16-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="95e16-124">Выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="95e16-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="95e16-125">На hello **пользователей и групп** колонки, toodelete hello выберите пользователя из списка hello.</span><span class="sxs-lookup"><span data-stu-id="95e16-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="95e16-126">В колонке hello для выбранного пользователя hello, выберите **Обзор**и выберите в панели команд hello, **удалить**.</span><span class="sxs-lookup"><span data-stu-id="95e16-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="95e16-127">![При выборе команды Добавить hello](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="95e16-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="95e16-128">Подробнее</span><span class="sxs-lookup"><span data-stu-id="95e16-128">Learn more</span></span> 
* [<span data-ttu-id="95e16-129">Добавление внешнего пользователя</span><span class="sxs-lookup"><span data-stu-id="95e16-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="95e16-130">Назначьте роль tooa пользователя в Azure AD</span><span class="sxs-lookup"><span data-stu-id="95e16-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="95e16-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="95e16-131">Next steps</span></span>
<span data-ttu-id="95e16-132">В этом кратком руководстве вы узнали, как новый tooadd tooAzure пользователей AD Premium.</span><span class="sxs-lookup"><span data-stu-id="95e16-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="95e16-133">Можно использовать следующую ссылку toocreate нового пользователя в Azure AD из портала Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="95e16-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="95e16-134">Добавление пользователей tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="95e16-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
