---
title: "Назначение групп для приложений Azure AD | Документация Майкрософт"
description: "Как реализовать назначение групп для приложений Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="7da16-103">Назначение групп Azure Active Directory для приложения</span><span class="sxs-lookup"><span data-stu-id="7da16-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="7da16-104">Прежде чем назначить пользователей и группы для приложения, необходимо настроить требование назначения пользователей.</span><span class="sxs-lookup"><span data-stu-id="7da16-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="7da16-105">Чтобы узнать, как настроить требование назначения пользователей, см. статью [Azure AD и приложения: требование назначения пользователей](active-directory-applications-guiding-developers-requiring-user-assignment.md).</span><span class="sxs-lookup"><span data-stu-id="7da16-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="7da16-106">В этой статье предполагается, что вы уже создали в Active Directory группу, которая используется для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="7da16-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="7da16-107">Назначение групп для приложения</span><span class="sxs-lookup"><span data-stu-id="7da16-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="7da16-108">Войдите на портал Azure с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="7da16-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="7da16-109">В главном меню выберите пункт **Все элементы** .</span><span class="sxs-lookup"><span data-stu-id="7da16-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="7da16-110">Выберите каталог, который используете для приложения.</span><span class="sxs-lookup"><span data-stu-id="7da16-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="7da16-111">Откройте вкладку **ПРИЛОЖЕНИЯ** .</span><span class="sxs-lookup"><span data-stu-id="7da16-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="7da16-112">Выберите приложение из списка приложений, связанных с данным каталогом.</span><span class="sxs-lookup"><span data-stu-id="7da16-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="7da16-113">Откройте вкладку **ПОЛЬЗОВАТЕЛИ И ГРУППЫ** .</span><span class="sxs-lookup"><span data-stu-id="7da16-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="7da16-114">Отфильтруйте список групп в Active Directory с помощью раскрывающегося списка **Группы** .</span><span class="sxs-lookup"><span data-stu-id="7da16-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="7da16-115">Выберите группу.</span><span class="sxs-lookup"><span data-stu-id="7da16-115">Select the group.</span></span>
9. <span data-ttu-id="7da16-116">Щелкните **НАЗНАЧИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="7da16-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="7da16-117">Щелкните **Да** при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="7da16-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7da16-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7da16-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
