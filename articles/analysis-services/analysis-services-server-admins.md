---
title: "Администраторы серверов aaaManage в Azure Analysis Services | Документы Microsoft"
description: "Узнайте, как администраторы серверов toomanage для сервера служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="723e0-103">Управление администраторами серверов</span><span class="sxs-lookup"><span data-stu-id="723e0-103">Manage server administrators</span></span>
<span data-ttu-id="723e0-104">Администраторы сервера необходимо быть допустимого пользователя или группы в Azure Active Directory (Azure AD) hello hello клиента, в которой hello находится сервер.</span><span class="sxs-lookup"><span data-stu-id="723e0-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="723e0-105">Можно использовать **Analysis Services Администраторы** в колонке управления hello для сервера на портале Azure или свойств сервера в SSMS toomanage администраторам.</span><span class="sxs-lookup"><span data-stu-id="723e0-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="723e0-106">Администраторы сервера tooadd с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="723e0-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="723e0-107">В колонке управления hello для сервера, щелкните **Analysis Services Администраторы**.</span><span class="sxs-lookup"><span data-stu-id="723e0-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="723e0-108">В hello  **\<имя_сервера >-Администраторы служб Analysis** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="723e0-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="723e0-109">В hello **добавления администраторов сервера** колонке выберите учетные записи пользователей из Azure AD или Пригласите внешних пользователей, адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="723e0-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Администраторы сервера на портале Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="723e0-111">Администраторы сервера tooadd с помощью среды SSMS</span><span class="sxs-lookup"><span data-stu-id="723e0-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="723e0-112">Щелкните правой кнопкой мыши сервер hello > **свойства**.</span><span class="sxs-lookup"><span data-stu-id="723e0-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="723e0-113">В разделе **Свойства сервера анализа данных** выберите **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="723e0-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="723e0-114">Нажмите кнопку **добавить**, а затем введите адрес электронной почты hello для пользователя или группы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="723e0-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Добавление администраторов сервера в SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="723e0-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="723e0-116">Next steps</span></span> 
[<span data-ttu-id="723e0-117">Аутентификация и пользовательские разрешения</span><span class="sxs-lookup"><span data-stu-id="723e0-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="723e0-118">Управление ролями и пользователями базы данных</span><span class="sxs-lookup"><span data-stu-id="723e0-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="723e0-119">Контроль доступа на основе ролей</span><span class="sxs-lookup"><span data-stu-id="723e0-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

