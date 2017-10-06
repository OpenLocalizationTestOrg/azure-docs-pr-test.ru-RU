---
title: "aaaHow tooperform доступе | Документы Microsoft"
description: "Узнайте, как tooperform отзыв с hello Azure управления привилегированными пользователями приложения."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="b31ae-103">Как tooperform доступа просмотрите в Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="b31ae-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="b31ae-104">Active Directory (AD) Управление привилегированными пользователями Azure упрощает, как управлять предприятий tooresources привилегированный доступ в Azure AD и других электронных услуг Microsoft, такие как Office 365 или Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="b31ae-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="b31ae-105">Если вам назначена роль администратора tooan, привилегированной роли Администратор организации может попросить вас tooregularly подтверждение по-прежнему требуется этой роли для данного задания.</span><span class="sxs-lookup"><span data-stu-id="b31ae-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="b31ae-106">Может появиться сообщение электронной почты, содержащее ссылку или переходе прямой toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b31ae-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b31ae-107">Выполните действия hello в этой статье tooperform, самостоятельно просмотрите назначенных ролей.</span><span class="sxs-lookup"><span data-stu-id="b31ae-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="b31ae-108">Если вы являетесь администратором привилегированной роли интересует проверки доступа, получить более подробные сведения в [как toostart доступа просмотрите](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="b31ae-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="b31ae-109">Добавить приложение hello Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="b31ae-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="b31ae-110">Можно использовать приложение hello Azure AD Privileged Identity управления (PIM) в hello [портал Azure](https://portal.azure.com/) tooperform проверки.</span><span class="sxs-lookup"><span data-stu-id="b31ae-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="b31ae-111">При отсутствии приложения hello Azure AD Privileged Identity Management на портале, выполните эти действия, tooget работы.</span><span class="sxs-lookup"><span data-stu-id="b31ae-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="b31ae-112">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b31ae-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b31ae-113">Выберите свое имя пользователя в верхнем правом углу hello hello портал Azure и выберите hello каталог, где можно будет работать.</span><span class="sxs-lookup"><span data-stu-id="b31ae-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="b31ae-114">Выберите **дополнительные службы** и использовать hello toosearch текстовое поле фильтра для **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="b31ae-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="b31ae-115">Проверьте **toodashboard ПИН-код** и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="b31ae-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="b31ae-116">Откроется Hello управления привилегированными пользователями приложения.</span><span class="sxs-lookup"><span data-stu-id="b31ae-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="b31ae-117">Утверждение или отклонение доступа</span><span class="sxs-lookup"><span data-stu-id="b31ae-117">Approve or deny access</span></span>
<span data-ttu-id="b31ae-118">При утверждении или запретить доступ, вы просто сообщают, что редактор hello ли вы по-прежнему использовать роль или нет.</span><span class="sxs-lookup"><span data-stu-id="b31ae-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="b31ae-119">Выберите **утвердить** Если toostay в роли hello или **Deny** Если вы не должны hello доступ больше.</span><span class="sxs-lookup"><span data-stu-id="b31ae-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="b31ae-120">Состояние не изменит прямо сейчас, пока редактор hello применяются hello результаты.</span><span class="sxs-lookup"><span data-stu-id="b31ae-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="b31ae-121">Выполните эти шаги toofind, выполните проверку доступа hello.</span><span class="sxs-lookup"><span data-stu-id="b31ae-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="b31ae-122">В hello PIM приложения, выберите **проверки привилегированный доступ**.</span><span class="sxs-lookup"><span data-stu-id="b31ae-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="b31ae-123">При наличии любой проверки ожидающих доступ, они отображаются в hello колонке проверок доступа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b31ae-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="b31ae-124">Выберите, требуется toocomplete проверки hello.</span><span class="sxs-lookup"><span data-stu-id="b31ae-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="b31ae-125">Если не был создан проверки hello, вы отображаются так, как только пользователь при проверке hello hello.</span><span class="sxs-lookup"><span data-stu-id="b31ae-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="b31ae-126">Выберите имя следующего tooyour hello флажок.</span><span class="sxs-lookup"><span data-stu-id="b31ae-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="b31ae-127">Выберите **Утвердить** или **Запретить**.</span><span class="sxs-lookup"><span data-stu-id="b31ae-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="b31ae-128">Может потребоваться tooinclude причина такого решения в hello **указать причину** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="b31ae-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="b31ae-129">Закрыть hello **роли проверки Azure AD** колонку.</span><span class="sxs-lookup"><span data-stu-id="b31ae-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="b31ae-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b31ae-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
