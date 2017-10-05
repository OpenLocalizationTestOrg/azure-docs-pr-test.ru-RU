---
title: "Устранение неполадок, связанных с отсутствием данных в скачанных журналах действий Azure Active Directory | Документация Майкрософт"
description: "В этой статье описаны способы устранения неполадок, связанных с отсутствием данных в скачанных журналах действий."
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
ms.openlocfilehash: 3d56f89035da4d1a0074256b165663f81fc2b01e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="56cce-103">Не удается найти данные в скачанном журнале действий Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56cce-103">I can’t find any data in the Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="56cce-104">Симптомы</span><span class="sxs-lookup"><span data-stu-id="56cce-104">Symptoms</span></span>

<span data-ttu-id="56cce-105">В скачанном журнале действий (аудита или входа) нет всех записей за выбранный период времени.</span><span class="sxs-lookup"><span data-stu-id="56cce-105">I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose.</span></span> <span data-ttu-id="56cce-106">Почему?</span><span class="sxs-lookup"><span data-stu-id="56cce-106">Why?</span></span> 

 ![Отчеты](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="56cce-108">Причина:</span><span class="sxs-lookup"><span data-stu-id="56cce-108">Cause</span></span>

<span data-ttu-id="56cce-109">К журналам действий, скачиваемым на портале Azure, применяется ограничение в 120 тыс. последних записей.</span><span class="sxs-lookup"><span data-stu-id="56cce-109">When you download activity logs in the Azure portal, we limit the scale to 120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="56cce-110">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="56cce-110">Resolution</span></span>

<span data-ttu-id="56cce-111">Вы можете в любой момент использовать [интерфейсы API отчетов Azure AD](active-directory-reporting-api-getting-started.md), чтобы извлечь до миллиона записей.</span><span class="sxs-lookup"><span data-stu-id="56cce-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) to fetch up to a million records at any given point.</span></span> <span data-ttu-id="56cce-112">Мы рекомендуем настроить расписание выполнения скрипта, который вызывает интерфейсы API отчетов для получения данных за определенный период времени (например, ежедневно или еженедельно).</span><span class="sxs-lookup"><span data-stu-id="56cce-112">Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="56cce-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56cce-113">Next steps</span></span>
<span data-ttu-id="56cce-114">См. сведения в статье [Часто задаваемые вопросы об отчетах Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="56cce-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

