---
title: "Устранение неполадок: Отсутствующие данные в hello загрузить журналы действий Azure Active Directory | Документы Microsoft"
description: "Предоставляет данные toomissing разрешения в загруженный журналы действий Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="1de33-103">Данные не найдены в журналы действий hello Azure Active Directory, я загрузил</span><span class="sxs-lookup"><span data-stu-id="1de33-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="1de33-104">Симптомы</span><span class="sxs-lookup"><span data-stu-id="1de33-104">Symptoms</span></span>

<span data-ttu-id="1de33-105">Я загрузил журналы действий hello (аудита или входа в систему), и я не вижу все записи hello для hello раз, когда я выбрал.</span><span class="sxs-lookup"><span data-stu-id="1de33-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="1de33-106">Почему?</span><span class="sxs-lookup"><span data-stu-id="1de33-106">Why?</span></span> 

 ![Отчеты](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="1de33-108">Причина:</span><span class="sxs-lookup"><span data-stu-id="1de33-108">Cause</span></span>

<span data-ttu-id="1de33-109">При загрузке журналы действий в hello портал Azure ограничена hello шкалы too120K записей, отсортированных по дате последней.</span><span class="sxs-lookup"><span data-stu-id="1de33-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="1de33-110">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="1de33-110">Resolution</span></span>

<span data-ttu-id="1de33-111">Можно использовать [Azure AD API-интерфейсы отчетов](active-directory-reporting-api-getting-started.md) toofetch tooa миллионов записей в любой момент.</span><span class="sxs-lookup"><span data-stu-id="1de33-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="1de33-112">Наш рекомендуется toorun сценария в соответствии с расписанием, вызывающий hello отчетов API-интерфейсы toofetch записывает в реальному за период времени (например, ежедневно или еженедельно).</span><span class="sxs-lookup"><span data-stu-id="1de33-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1de33-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1de33-113">Next steps</span></span>
<span data-ttu-id="1de33-114">В разделе hello [отчетов часто задаваемые вопросы об Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="1de33-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

