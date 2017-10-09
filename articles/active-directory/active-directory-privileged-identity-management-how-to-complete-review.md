---
title: "aaaHow toocomplete доступе | Документы Microsoft"
description: "После запуска проверки доступа в Azure AD Privileged Identity Management, узнайте, как toocomplete его и просмотрите hello результатов"
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
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="806c9-103">Как toocomplete доступа просмотрите в Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="806c9-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="806c9-104">После [запуска функции проверки безопасности](active-directory-privileged-identity-management-how-to-start-security-review.md)администраторы привилегированных ролей могут проверить привилегированный доступ.</span><span class="sxs-lookup"><span data-stu-id="806c9-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="806c9-105">Azure AD Privileged Identity Management (PIM) автоматически отправляет сообщение электронной почты, запросы пользователей tooreview свой доступ.</span><span class="sxs-lookup"><span data-stu-id="806c9-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="806c9-106">Если пользователь не получает сообщение электронной почты, можно отправить им инструкции hello [как tooperform безопасности просмотрите](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="806c9-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="806c9-107">После период проверки безопасности hello, или все пользователи hello закончена, просмотрите их самостоятельно, выполните действия hello в этой статье toomanage hello проверки и просмотреть результаты hello.</span><span class="sxs-lookup"><span data-stu-id="806c9-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="806c9-108">Управление проверкой безопасности</span><span class="sxs-lookup"><span data-stu-id="806c9-108">Manage security reviews</span></span>
1. <span data-ttu-id="806c9-109">Go toohello [портал Azure](https://portal.azure.com/) и выберите hello **Azure AD Privileged Identity Management** приложения в панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="806c9-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="806c9-110">Выберите hello **проверки доступа к** hello панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="806c9-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="806c9-111">Выберите требуемый toomanage hello доступе.</span><span class="sxs-lookup"><span data-stu-id="806c9-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="806c9-112">В колонке сведений проверки доступа hello существует число параметров для управления этой проверки.</span><span class="sxs-lookup"><span data-stu-id="806c9-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![Кнопки проверки доступа PIM — снимок экрана][1]

### <a name="remind"></a><span data-ttu-id="806c9-114">Напомнить</span><span class="sxs-lookup"><span data-stu-id="806c9-114">Remind</span></span>
<span data-ttu-id="806c9-115">При доступе настройки, чтобы просмотреть hello пользователи сами hello **напоминать** кнопка отправляет уведомление.</span><span class="sxs-lookup"><span data-stu-id="806c9-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="806c9-116">Остановить</span><span class="sxs-lookup"><span data-stu-id="806c9-116">Stop</span></span>
<span data-ttu-id="806c9-117">Все отзывы доступ имеют срок действия, но можно использовать hello **остановить** toofinish кнопку раньше его.</span><span class="sxs-lookup"><span data-stu-id="806c9-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="806c9-118">Если к этому времени еще не были проверены все пользователи, они не будет возможности tooafter остановить проверку hello.</span><span class="sxs-lookup"><span data-stu-id="806c9-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="806c9-119">Нельзя перезапустить проверку после ее остановки.</span><span class="sxs-lookup"><span data-stu-id="806c9-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="806c9-120">Применить</span><span class="sxs-lookup"><span data-stu-id="806c9-120">Apply</span></span>
<span data-ttu-id="806c9-121">После завершения проверки доступа, либо из-за достижения Дата окончания hello или остановить его вручную, hello **применить** реализовывать hello результат проверки hello.</span><span class="sxs-lookup"><span data-stu-id="806c9-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="806c9-122">Если при проверке hello запрещен доступ пользователя, это hello, приведет к удалению назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="806c9-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="806c9-123">экспорт.</span><span class="sxs-lookup"><span data-stu-id="806c9-123">Export</span></span>
<span data-ttu-id="806c9-124">Если требуется tooapply hello результатов проверки безопасности hello вручную, можно экспортировать hello проверки.</span><span class="sxs-lookup"><span data-stu-id="806c9-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="806c9-125">Hello **Экспорт** кнопку начнется загрузка CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="806c9-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="806c9-126">Вы можете управлять hello результаты в Excel или другие программы, откройте CSV-файлы.</span><span class="sxs-lookup"><span data-stu-id="806c9-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="806c9-127">Удалить</span><span class="sxs-lookup"><span data-stu-id="806c9-127">Delete</span></span>
<span data-ttu-id="806c9-128">Если вы не заинтересованы в hello просматривать любые дополнительные, удалите его.</span><span class="sxs-lookup"><span data-stu-id="806c9-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="806c9-129">Hello **удалить** кнопка удаляет hello проверки из hello PIM приложения.</span><span class="sxs-lookup"><span data-stu-id="806c9-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="806c9-130">Будет не появляется предупреждение, прежде чем произойдет удаление, поэтому убедитесь, что требуется toodelete, просмотрите.</span><span class="sxs-lookup"><span data-stu-id="806c9-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="806c9-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="806c9-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
