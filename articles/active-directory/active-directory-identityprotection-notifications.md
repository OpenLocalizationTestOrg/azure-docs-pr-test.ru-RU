---
title: "уведомления Active Directory Identity Protection aaaAzure | Документы Microsoft"
description: "Узнайте, как уведомления помогают в изучении проблем."
services: active-directory
keywords: "защита удостоверений Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="28183-104">Уведомления защиты идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28183-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="28183-105">Azure AD Identity Protection отправляет два типа автоматических уведомлений отправляется сообщение электронной почты toohelp, которыми вы управляете пользователя риска и событиях риска:</span><span class="sxs-lookup"><span data-stu-id="28183-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="28183-106">оповещение электронной почты о том, что пользователь скомпрометирован;</span><span class="sxs-lookup"><span data-stu-id="28183-106">User compromised alert email</span></span>
* <span data-ttu-id="28183-107">сообщение электронной почты еженедельного дайджеста.</span><span class="sxs-lookup"><span data-stu-id="28183-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="28183-108">оповещение электронной почты о том, что пользователь скомпрометирован;</span><span class="sxs-lookup"><span data-stu-id="28183-108">User compromised alert email</span></span>
<span data-ttu-id="28183-109">Электронное оповещение о том, что пользователь скомпрометирован, создается, если служба защиты идентификации Azure AD определяет, что учетная запись скомпрометирована.</span><span class="sxs-lookup"><span data-stu-id="28183-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="28183-110">Hello электронной почты включает toohello связи, в которой пользователи отмечен для риска отчета на панели мониторинга hello защиту учетных данных.</span><span class="sxs-lookup"><span data-stu-id="28183-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="28183-111">Мы рекомендуем безотлагательно проверить уведомления о скомпрометированных учетных записях.</span><span class="sxs-lookup"><span data-stu-id="28183-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="28183-112">сообщение электронной почты еженедельного дайджеста.</span><span class="sxs-lookup"><span data-stu-id="28183-112">Weekly digest email</span></span>
<span data-ttu-id="28183-113">Hello еженедельная хэш-кода по электронной почте содержит сводку новых событий риска.</span><span class="sxs-lookup"><span data-stu-id="28183-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="28183-114">Сюда входят:</span><span class="sxs-lookup"><span data-stu-id="28183-114">It includes:</span></span>

* <span data-ttu-id="28183-115">пользователи под угрозой;</span><span class="sxs-lookup"><span data-stu-id="28183-115">Users at risk</span></span>
* <span data-ttu-id="28183-116">подозрительные действия;</span><span class="sxs-lookup"><span data-stu-id="28183-116">Suspicious activities</span></span>
* <span data-ttu-id="28183-117">обнаруженные уязвимости;</span><span class="sxs-lookup"><span data-stu-id="28183-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="28183-118">Toohello ссылки, связанные с отчетами в защиту учетных данных</span><span class="sxs-lookup"><span data-stu-id="28183-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="28183-119">
![Исправления](./media/active-directory-identityprotection-notifications/400.png "исправления")
</span><span class="sxs-lookup"><span data-stu-id="28183-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="28183-120">Можно отключить отправку еженедельных дайджестов по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="28183-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="28183-121">
![Рисков для пользователя](./media/active-directory-identityprotection-notifications/62.png "рисков для пользователя")
</span><span class="sxs-lookup"><span data-stu-id="28183-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="28183-122">**диалоговое окно конфигурации hello tooopen**:</span><span class="sxs-lookup"><span data-stu-id="28183-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="28183-123">На hello **Azure AD Identity Protection** колонка, щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="28183-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="28183-124">
   ![Политика пользователя риск](./media/active-directory-identityprotection-notifications/401.png "риск политика пользователя")
   </span><span class="sxs-lookup"><span data-stu-id="28183-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="28183-125">В hello **Общие** щелкните **уведомления**.</span><span class="sxs-lookup"><span data-stu-id="28183-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="28183-126">
   ![Политика пользователя риск](./media/active-directory-identityprotection-notifications/405.png "риск политика пользователя")
   </span><span class="sxs-lookup"><span data-stu-id="28183-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="28183-127">См. также</span><span class="sxs-lookup"><span data-stu-id="28183-127">See also</span></span>
* [<span data-ttu-id="28183-128">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28183-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
