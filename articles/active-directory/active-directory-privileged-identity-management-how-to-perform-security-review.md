---
title: "Выполнение проверки доступа | Документация Майкрософт"
description: "Сведения о выполнении проверки с помощью приложения для управления привилегированными пользователями Azure."
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
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="dd992-103">Как выполнить проверку доступа в управлении привилегированными пользователями Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd992-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="dd992-104">Компонент Azure Active Directory (AD) Privileged Identity Management упрощает управление привилегированным доступом пользователей к ресурсам в Azure AD и других веб-службах Майкрософт, включая Office 365 и Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="dd992-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="dd992-105">Если вам назначена роль администратора, администратор привилегированных ролей вашей организации может попросить вас регулярно подтверждать, что эта роль по-прежнему требуется вам для работы.</span><span class="sxs-lookup"><span data-stu-id="dd992-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="dd992-106">Вы можете получить сообщение электронной почты, содержащее ссылку для подтверждения, или перейти непосредственно на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd992-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dd992-107">Следуйте указаниям в этой статье, чтобы выполнить самостоятельную проверку назначенных вам ролей.</span><span class="sxs-lookup"><span data-stu-id="dd992-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="dd992-108">Если вы администратор привилегированных ролей и вас интересуют функции проверки доступа, дополнительные сведения см. в статье [Как запустить проверку доступа в управлении привилегированными пользователями Azure AD](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="dd992-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="dd992-109">Добавление приложения для управления привилегированными пользователями</span><span class="sxs-lookup"><span data-stu-id="dd992-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="dd992-110">Для выполнения проверки можно использовать приложение "Управление привилегированными пользователями" (PIM) Azure AD на [портале Azure](https://portal.azure.com/) .</span><span class="sxs-lookup"><span data-stu-id="dd992-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="dd992-111">Если приложение Azure AD PIM еще не установлено на портале, выполните следующие действия, чтобы приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="dd992-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="dd992-112">Выполните вход на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dd992-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dd992-113">Щелкните свое имя пользователя в правом верхнем углу портала Azure и выберите каталог, с которым будете работать.</span><span class="sxs-lookup"><span data-stu-id="dd992-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="dd992-114">Выберите **Другие службы** и в текстовое поле "Фильтр" введите **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="dd992-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="dd992-115">Установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd992-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="dd992-116">Откроется приложение "Управление привилегированными пользователями".</span><span class="sxs-lookup"><span data-stu-id="dd992-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="dd992-117">Утверждение или отклонение доступа</span><span class="sxs-lookup"><span data-stu-id="dd992-117">Approve or deny access</span></span>
<span data-ttu-id="dd992-118">При утверждении или отклонении доступа вы просто сообщаете проверяющему, используете ли вы еще эту роль.</span><span class="sxs-lookup"><span data-stu-id="dd992-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="dd992-119">Чтобы оставаться в этой роли, выберите **Утвердить**, а когда доступ вам больше не требуется — **Запретить**.</span><span class="sxs-lookup"><span data-stu-id="dd992-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="dd992-120">Состояние роли изменится лишь тогда, когда проверяющий применит результаты.</span><span class="sxs-lookup"><span data-stu-id="dd992-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="dd992-121">Выполните следующие действия, чтобы найти проверку доступа и завершить ее.</span><span class="sxs-lookup"><span data-stu-id="dd992-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="dd992-122">В приложении PIM выберите **Просмотр привилегированного доступа**.</span><span class="sxs-lookup"><span data-stu-id="dd992-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="dd992-123">Если у вас есть незавершенные проверки доступа, то они отображаются в колонке "Проверки доступа" в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd992-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="dd992-124">Выберите проверку, которую необходимо завершить.</span><span class="sxs-lookup"><span data-stu-id="dd992-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="dd992-125">Если эта проверка создана не вами, вы должны быть единственным пользователем, отображаемым при проверке.</span><span class="sxs-lookup"><span data-stu-id="dd992-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="dd992-126">Установите флажок рядом со своим именем.</span><span class="sxs-lookup"><span data-stu-id="dd992-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="dd992-127">Выберите **Утвердить** или **Запретить**.</span><span class="sxs-lookup"><span data-stu-id="dd992-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="dd992-128">Возможно, в текстовом поле **Указание причины** потребуется ввести причину своего решения.</span><span class="sxs-lookup"><span data-stu-id="dd992-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="dd992-129">Закройте колонку **Проверка ролей Azure AD** .</span><span class="sxs-lookup"><span data-stu-id="dd992-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="dd992-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd992-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
