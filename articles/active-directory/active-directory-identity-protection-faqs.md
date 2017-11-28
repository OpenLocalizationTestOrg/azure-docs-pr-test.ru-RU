---
title: "Вопросы и ответы о защите идентификации Azure Active Directory | Документация Майкрософт"
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
ms.openlocfilehash: 781f868c87cea3cd790d89c61e26eecf352babea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-faq"></a><span data-ttu-id="e82ac-103">Вопросы и ответы о защите идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e82ac-103">Azure Active Directory Identity Protection FAQ</span></span>


## <a name="why-do-some-risk-events-have-closed-system-status"></a><span data-ttu-id="e82ac-104">Почему для некоторых событий риска отображается состояние "Закрыто (системные)"?</span><span class="sxs-lookup"><span data-stu-id="e82ac-104">Why do some risk events have “Closed (system)” status?</span></span>

<span data-ttu-id="e82ac-105">**Ответ.** Это события, обнаруженные и затем закрытые службой защиты идентификации Azure Active Directory, так как они перестали считаться событиями, представляющими риск.</span><span class="sxs-lookup"><span data-stu-id="e82ac-105">**A:** These are events that Azure Active Directory Identity Protection detected and later closed because the events were no longer considered risky.</span></span> <span data-ttu-id="e82ac-106">Эти события не учитываются в уровне риска пользователя.</span><span class="sxs-lookup"><span data-stu-id="e82ac-106">These events do not count towards the user’s risk level.</span></span> 

---

## <a name="do-i-need-to-be-a-global-admin-to-use-identity-protection-in-the-azure-portal"></a><span data-ttu-id="e82ac-107">Требуется ли роль глобального администратора для использования защиты идентификации на портале Azure?</span><span class="sxs-lookup"><span data-stu-id="e82ac-107">Do I need to be a global admin to use Identity Protection in the Azure portal?</span></span>
<span data-ttu-id="e82ac-108">**Ответ.** **Нет**.</span><span class="sxs-lookup"><span data-stu-id="e82ac-108">**A:** **No**.</span></span> <span data-ttu-id="e82ac-109">Для использования защиты идентификации можно иметь роль читателя безопасности, администратора безопасности или глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="e82ac-109">You can either be a Security Reader, a Security Admin or a Global Admin to use Identity Protection.</span></span>

---

## <a name="how-do-i-get-identity-protection"></a><span data-ttu-id="e82ac-110">Как начать использовать защиту идентификации?</span><span class="sxs-lookup"><span data-stu-id="e82ac-110">How do I get Identity Protection?</span></span>
<span data-ttu-id="e82ac-111">**Ответ.** Ответ на этот вопрос есть в разделе [Приступая к работе с Azure Active Directory Premium](active-directory-get-started-premium.md).</span><span class="sxs-lookup"><span data-stu-id="e82ac-111">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

## <a name="what-happens-when-your-azure-active-directory-premium-2-trial-expires"></a><span data-ttu-id="e82ac-112">Что происходит после истечения срока действия пробной версии Azure Active Directory Premium 2?</span><span class="sxs-lookup"><span data-stu-id="e82ac-112">What happens when your Azure Active Directory Premium 2 trial expires?</span></span>

<span data-ttu-id="e82ac-113">**Ответ.** Если срок действия вашей пробной версии Azure Active Directory Premium 2 истек для выпуска Azure Active Directory Free, Basic или Premium 1 и у вас была включена защита идентификации, вы по-прежнему будете иметь к ней доступ, даже несмотря на несоблюдение условий лицензирования.</span><span class="sxs-lookup"><span data-stu-id="e82ac-113">**A:** If your Azure Active Directory Premium 2 trial edition has expired on your Azure Active Directory Free, Basic or Premium 1 edition, and you had Identity Protection enabled, you still have access to it even though you are not in compliance with licensing.</span></span>

---
