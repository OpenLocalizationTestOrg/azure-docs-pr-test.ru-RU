---
title: "Назначение лицензий для Azure MFA | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как назначать лицензии для службы Microsoft Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a><span data-ttu-id="9aaa1-103">Назначение пользователям лицензии Azure MFA, Azure AD Premium или Enterprise Mobility</span><span class="sxs-lookup"><span data-stu-id="9aaa1-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span></span>
<span data-ttu-id="9aaa1-104">Если вы приобрели лицензии Azure MFA, Azure AD Premium или Enterprise Mobility Suite, поставщик Multi-Factor Authentication создавать не нужно.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span></span> <span data-ttu-id="9aaa1-105">Назначив эти лицензии пользователям, можно включить MFA.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span></span>

## <a name="to-assign-a-license"></a><span data-ttu-id="9aaa1-106">Назначение лицензии</span><span class="sxs-lookup"><span data-stu-id="9aaa1-106">To assign a license</span></span>
1. <span data-ttu-id="9aaa1-107">Войдите на [классический портал Azure](https://manage.windowsazure.com) с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="9aaa1-108">Выберите **Active Directory**слева.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-108">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="9aaa1-109">На странице "Active Directory" дважды щелкните каталог с пользователями для активации.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span></span>
4. <span data-ttu-id="9aaa1-110">В верхней части страницы каталога выберите **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-110">At the top of the directory page, select **Licenses**.</span></span>
   <span data-ttu-id="9aaa1-111">![Назначение лицензий](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="9aaa1-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="9aaa1-112">На странице "Лицензии" выберите **Многофакторная идентификация Azure**, **Active Directory Premium** или **Enterprise Mobility Suite**.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="9aaa1-113">Если у вас только одна лицензия, она будет выбрана автоматически.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="9aaa1-114">В нижней части страницы щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-114">At the bottom of the page, click **Assign**.</span></span>
   <span data-ttu-id="9aaa1-115">![Назначение лицензий](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="9aaa1-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="9aaa1-116">В открывшемся окне щелкните рядом с пользователями или группами, которым требуется назначить лицензии.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span></span>  <span data-ttu-id="9aaa1-117">Должна появиться зеленая галочка.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="9aaa1-118">Щелкните значок с галочкой, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-118">Click the check mark icon to save the changes.</span></span>
   <span data-ttu-id="9aaa1-119">![Назначение лицензий](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="9aaa1-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="9aaa1-120">Появится сообщение о том, сколько лицензий назначено и сколько не удалось назначить.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="9aaa1-121">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9aaa1-121">Click **Ok**.</span></span>
   <span data-ttu-id="9aaa1-122">![Назначение лицензий](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="9aaa1-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9aaa1-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9aaa1-123">Next steps</span></span>

- <span data-ttu-id="9aaa1-124">Дополнительные сведения см. в статье [Что такое лицензирование Microsoft Azure Active?](../active-directory/active-directory-licensing-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="9aaa1-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
