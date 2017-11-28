---
title: "Завершение выполнения проверки доступа | Документация Майкрософт"
description: "После запуска проверки доступа в управлении привилегированными пользователями Azure AD узнайте, как ее завершить и просмотреть результаты."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="84f94-103">Как завершить выполнение проверки доступа в управлении привилегированными пользователями Azure AD</span><span class="sxs-lookup"><span data-stu-id="84f94-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="84f94-104">После [запуска функции проверки безопасности](active-directory-privileged-identity-management-how-to-start-security-review.md)администраторы привилегированных ролей могут проверить привилегированный доступ.</span><span class="sxs-lookup"><span data-stu-id="84f94-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="84f94-105">Компонент управления привилегированными пользователями (PIM) Azure AD автоматически отправит пользователям электронное письмо с предложением проверить доступ.</span><span class="sxs-lookup"><span data-stu-id="84f94-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="84f94-106">Если пользователь не получил электронное письмо, ему можно отправить [инструкции по выполнению проверки безопасности](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="84f94-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="84f94-107">После окончания периода проверки безопасности или после завершения всеми пользователями самостоятельной проверки выполните шаги, описанные в этой статье, для управления проверкой и просмотра результатов.</span><span class="sxs-lookup"><span data-stu-id="84f94-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="84f94-108">Управление проверкой безопасности</span><span class="sxs-lookup"><span data-stu-id="84f94-108">Manage security reviews</span></span>
1. <span data-ttu-id="84f94-109">Войдите на [портал Azure](https://portal.azure.com/) и выберите приложение **Управление привилегированными пользователями Azure AD** на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="84f94-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="84f94-110">Выберите раздел **Проверки доступа** на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="84f94-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="84f94-111">Выберите необходимую проверку доступа.</span><span class="sxs-lookup"><span data-stu-id="84f94-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="84f94-112">В колонке со сведениями о проверке доступа отображается ряд вариантов действий для этой проверки.</span><span class="sxs-lookup"><span data-stu-id="84f94-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![Кнопки проверки доступа PIM — снимок экрана][1]

### <a name="remind"></a><span data-ttu-id="84f94-114">Напомнить</span><span class="sxs-lookup"><span data-stu-id="84f94-114">Remind</span></span>
<span data-ttu-id="84f94-115">Если проверка доступа настроена таким образом, что пользователи проверяют сами себя, то кнопка **Напомнить** отправляет уведомление.</span><span class="sxs-lookup"><span data-stu-id="84f94-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="84f94-116">Остановить</span><span class="sxs-lookup"><span data-stu-id="84f94-116">Stop</span></span>
<span data-ttu-id="84f94-117">Все проверки доступа имеют дату окончания, но можно воспользоваться кнопкой **Остановить** , чтобы завершить их выполнение раньше.</span><span class="sxs-lookup"><span data-stu-id="84f94-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="84f94-118">Если к этому моменту еще не все пользователи были проверены, то они уже не смогут пройти проверку после ее остановки.</span><span class="sxs-lookup"><span data-stu-id="84f94-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="84f94-119">Нельзя перезапустить проверку после ее остановки.</span><span class="sxs-lookup"><span data-stu-id="84f94-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="84f94-120">Применить</span><span class="sxs-lookup"><span data-stu-id="84f94-120">Apply</span></span>
<span data-ttu-id="84f94-121">После того, как проверка доступа завершается из-за достижения даты окончания или из-за остановки вручную, реализовать результат проверки можно с помощью кнопки **Применить** .</span><span class="sxs-lookup"><span data-stu-id="84f94-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="84f94-122">Если в процессе проверки пользователю было отказано в доступе, то этот шаг приведет к удалению назначенной пользователю роли.</span><span class="sxs-lookup"><span data-stu-id="84f94-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="84f94-123">экспорт.</span><span class="sxs-lookup"><span data-stu-id="84f94-123">Export</span></span>
<span data-ttu-id="84f94-124">Если вы хотите применить результаты проверки безопасности вручную, можно экспортировать проверку.</span><span class="sxs-lookup"><span data-stu-id="84f94-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="84f94-125">При нажатии кнопки **Экспорт** будет скачан CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="84f94-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="84f94-126">Открыть этот файл можно в Excel или в других программах, поддерживающих CSV-файлы.</span><span class="sxs-lookup"><span data-stu-id="84f94-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="84f94-127">Удалить</span><span class="sxs-lookup"><span data-stu-id="84f94-127">Delete</span></span>
<span data-ttu-id="84f94-128">Если проверка вам больше не нужна, удалите ее.</span><span class="sxs-lookup"><span data-stu-id="84f94-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="84f94-129">При нажатии кнопки **Удалить** проверка будет удалена из приложения PIM.</span><span class="sxs-lookup"><span data-stu-id="84f94-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84f94-130">Учтите, что при удалении проверки предупреждение не выдается. Поэтому убедитесь, что выбрана нужная проверка.</span><span class="sxs-lookup"><span data-stu-id="84f94-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="84f94-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84f94-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
