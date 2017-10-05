---
title: "Уведомления защиты идентификации Azure Active Directory | Документация Майкрософт"
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
ms.openlocfilehash: 079d16bbf75cd2b3b94269d684e1ae1a0e6aa967
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="7266e-104">Уведомления защиты идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7266e-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="7266e-105">Служба защиты идентификации Azure AD отправляет по электронной почте два типа автоматических уведомлений, что упрощает управление рисками для пользователей и событиями риска:</span><span class="sxs-lookup"><span data-stu-id="7266e-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span></span>

* <span data-ttu-id="7266e-106">оповещение электронной почты о том, что пользователь скомпрометирован;</span><span class="sxs-lookup"><span data-stu-id="7266e-106">User compromised alert email</span></span>
* <span data-ttu-id="7266e-107">сообщение электронной почты еженедельного дайджеста.</span><span class="sxs-lookup"><span data-stu-id="7266e-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="7266e-108">оповещение электронной почты о том, что пользователь скомпрометирован;</span><span class="sxs-lookup"><span data-stu-id="7266e-108">User compromised alert email</span></span>
<span data-ttu-id="7266e-109">Электронное оповещение о том, что пользователь скомпрометирован, создается, если служба защиты идентификации Azure AD определяет, что учетная запись скомпрометирована.</span><span class="sxs-lookup"><span data-stu-id="7266e-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="7266e-110">В таком электронном сообщении содержится ссылка на отчет о пользователях, помеченных для события риска, на панели мониторинга защиты идентификации.</span><span class="sxs-lookup"><span data-stu-id="7266e-110">The email includes a link to the Users flagged for risk report in the Identity Protection dashboard.</span></span> <span data-ttu-id="7266e-111">Мы рекомендуем безотлагательно проверить уведомления о скомпрометированных учетных записях.</span><span class="sxs-lookup"><span data-stu-id="7266e-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="7266e-112">сообщение электронной почты еженедельного дайджеста.</span><span class="sxs-lookup"><span data-stu-id="7266e-112">Weekly digest email</span></span>
<span data-ttu-id="7266e-113">В электронном сообщении еженедельного дайджеста содержится сводка новых событий риска.</span><span class="sxs-lookup"><span data-stu-id="7266e-113">The weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="7266e-114">Сюда входят:</span><span class="sxs-lookup"><span data-stu-id="7266e-114">It includes:</span></span>

* <span data-ttu-id="7266e-115">пользователи под угрозой;</span><span class="sxs-lookup"><span data-stu-id="7266e-115">Users at risk</span></span>
* <span data-ttu-id="7266e-116">подозрительные действия;</span><span class="sxs-lookup"><span data-stu-id="7266e-116">Suspicious activities</span></span>
* <span data-ttu-id="7266e-117">обнаруженные уязвимости;</span><span class="sxs-lookup"><span data-stu-id="7266e-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="7266e-118">ссылки на связанные отчеты в службе защиты идентификации.</span><span class="sxs-lookup"><span data-stu-id="7266e-118">Links to the related reports in Identity Protection</span></span>

<br><span data-ttu-id="7266e-119">
![Исправления](./media/active-directory-identityprotection-notifications/400.png "исправления")
</span><span class="sxs-lookup"><span data-stu-id="7266e-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="7266e-120">Можно отключить отправку еженедельных дайджестов по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="7266e-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="7266e-121">
![Рисков для пользователя](./media/active-directory-identityprotection-notifications/62.png "рисков для пользователя")
</span><span class="sxs-lookup"><span data-stu-id="7266e-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="7266e-122">**Вот как можно открыть диалоговое окно настройки**.</span><span class="sxs-lookup"><span data-stu-id="7266e-122">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="7266e-123">В колонке **Защита идентификации Azure AD** щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="7266e-123">On the **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="7266e-124">
   ![Политика пользователя риск](./media/active-directory-identityprotection-notifications/401.png "риск политика пользователя")
   </span><span class="sxs-lookup"><span data-stu-id="7266e-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="7266e-125">В разделе **Общие** щелкните **Уведомления**.</span><span class="sxs-lookup"><span data-stu-id="7266e-125">In the **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="7266e-126">
   ![Политика пользователя риск](./media/active-directory-identityprotection-notifications/405.png "риск политика пользователя")
   </span><span class="sxs-lookup"><span data-stu-id="7266e-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="7266e-127">См. также</span><span class="sxs-lookup"><span data-stu-id="7266e-127">See also</span></span>
* [<span data-ttu-id="7266e-128">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7266e-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
