---
title: "Требование назначения пользователей: Azure AD | Документация Майкрософт"
description: "Как требовать назначение пользователей для приложений Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a><span data-ttu-id="cac47-103">Azure AD и приложения: требование назначения пользователей</span><span class="sxs-lookup"><span data-stu-id="cac47-103">Azure AD and applications: Require user assignment</span></span>
## <a name="requiring-user-assignment"></a><span data-ttu-id="cac47-104">Требование назначения пользователей</span><span class="sxs-lookup"><span data-stu-id="cac47-104">Requiring User Assignment</span></span>
1. <span data-ttu-id="cac47-105">Войдите на портал Azure с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="cac47-105">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="cac47-106">В главном меню выберите пункт **Все элементы** .</span><span class="sxs-lookup"><span data-stu-id="cac47-106">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="cac47-107">Выберите каталог, который используете для приложения.</span><span class="sxs-lookup"><span data-stu-id="cac47-107">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="cac47-108">Откройте вкладку **ПРИЛОЖЕНИЯ** .</span><span class="sxs-lookup"><span data-stu-id="cac47-108">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="cac47-109">Выберите приложение из списка приложений, связанных с данным каталогом.</span><span class="sxs-lookup"><span data-stu-id="cac47-109">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="cac47-110">Выберите вкладку **НАСТРОЙКА** .</span><span class="sxs-lookup"><span data-stu-id="cac47-110">Click the **CONFIGURE** tab.</span></span>
7. <span data-ttu-id="cac47-111">Задайте для параметра **Для доступа к приложению требуется назначение пользователей** значение «Да».</span><span class="sxs-lookup"><span data-stu-id="cac47-111">Change the **User Assignment Required to Access App** toggle to Yes.</span></span>
8. <span data-ttu-id="cac47-112">Нажмите кнопку **Сохранить** , расположенную в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="cac47-112">Click the **Save** button at the bottom of the screen.</span></span>

<span data-ttu-id="cac47-113">Теперь будет необходимо назначить пользователей и (или) группы для приложения.</span><span class="sxs-lookup"><span data-stu-id="cac47-113">You will now have to assign users and/or groups to the application.</span></span> <span data-ttu-id="cac47-114">См. разделы [Назначение пользователей приложения](active-directory-applications-guiding-developers-assigning-users.md) и [Назначение групп для приложения](active-directory-applications-guiding-developers-assigning-groups.md).</span><span class="sxs-lookup"><span data-stu-id="cac47-114">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cac47-115">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cac47-115">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
