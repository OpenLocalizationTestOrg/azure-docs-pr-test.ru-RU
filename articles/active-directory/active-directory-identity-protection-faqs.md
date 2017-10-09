---
title: "часто задаваемые вопросы защиты удостоверение Active Directory aaaAzure | Документы Microsoft"
description: "Часто задаваемые вопросы о защите идентификации Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6a053ce02bf7a248a284f482f20f96a312f1c204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="eed25-103">Вопросы и ответы о защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eed25-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="eed25-104">Почему для некоторых событий риска отображается состояние "Закрыто (системные)"?</span><span class="sxs-lookup"><span data-stu-id="eed25-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="eed25-105">**Ответ** это события, которые Azure Active Directory Identity Protection обнаружены и позже закрыт, потому что события hello рассматривались опасен.</span><span class="sxs-lookup"><span data-stu-id="eed25-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because hello events were no longer considered risky.</span></span> <span data-ttu-id="eed25-106">Эти события не считаются уровень риска hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="eed25-106">These events do not count towards hello user’s risk level.</span></span> 

---

## <a name="do-i-need-toobe-a-global-admin-toouse-identity-protection-in-hello-azure-portal"></a><span data-ttu-id="eed25-107">Требуется toobe toouse глобального администратора защиты идентификации в hello портал Azure?</span><span class="sxs-lookup"><span data-stu-id="eed25-107">Do I need toobe a global admin toouse Identity Protection in hello Azure portal?</span></span>
<span data-ttu-id="eed25-108">**Ответ.** **Нет**.</span><span class="sxs-lookup"><span data-stu-id="eed25-108">**A:** **No**.</span></span> <span data-ttu-id="eed25-109">Может представлять чтения безопасности, администратору безопасности или глобального администратора toouse защиту учетных данных.</span><span class="sxs-lookup"><span data-stu-id="eed25-109">You can either be a Security Reader, a Security Admin or a Global Admin toouse Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="eed25-110">Как начать использовать защиту идентификации?</span><span class="sxs-lookup"><span data-stu-id="eed25-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="eed25-111">**Ответ** разделе [Приступая к работе с Azure Active Directory Premium](active-directory-get-started-premium.md) для вопроса toothis ответов.</span><span class="sxs-lookup"><span data-stu-id="eed25-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="eed25-112">Что происходит после истечения срока действия пробной версии Azure Active Directory Premium 2?</span><span class="sxs-lookup"><span data-stu-id="eed25-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="eed25-113">**Ответ** при вашей пробной версии Azure Active Directory Premium 2 истек выпуска Azure Active Directory Free, Basic или Premium 1, с включенной защитой удостоверение, по-прежнему имеется доступ tooit даже если вы не compliance с Лицензирование.</span><span class="sxs-lookup"><span data-stu-id="eed25-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access tooit even though you are not in compliance with licensing.</span></span>

---
