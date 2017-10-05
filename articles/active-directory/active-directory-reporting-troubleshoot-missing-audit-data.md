---
title: "Устранение неполадок, связанных с отсутствием данных в журнале действий Azure Active Directory | Документация Майкрософт"
description: "В этой статье описаны различные отчеты, доступные в Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a><span data-ttu-id="aaf68-103">Не удается найти некоторые выполненные действия в журнале действий Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aaf68-103">I can’t find some actions that I performed in the Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="aaf68-104">Симптомы</span><span class="sxs-lookup"><span data-stu-id="aaf68-104">Symptoms</span></span>

<span data-ttu-id="aaf68-105">Действия, выполненные на портале Azure, не отображаются в журнале аудита в колонке `Activity logs > Audit Logs`.</span><span class="sxs-lookup"><span data-stu-id="aaf68-105">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![Отчеты](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="aaf68-107">Причина:</span><span class="sxs-lookup"><span data-stu-id="aaf68-107">Cause</span></span>

<span data-ttu-id="aaf68-108">Действия отображаются в журнале аудита действий спустя некоторое время.</span><span class="sxs-lookup"><span data-stu-id="aaf68-108">Actions don’t appear immediately in the Activity Audit log.</span></span> <span data-ttu-id="aaf68-109">Чтобы действия отобразились в журнале аудита на портале, с момента выполнения операции может пройти от 15 минут до часа.</span><span class="sxs-lookup"><span data-stu-id="aaf68-109">It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="aaf68-110">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="aaf68-110">Resolution</span></span>

<span data-ttu-id="aaf68-111">Подождите от 15 минут до часа и проверьте, появились ли действия в журнале.</span><span class="sxs-lookup"><span data-stu-id="aaf68-111">Wait for 15 minutes to an hour and see if the actions appear in the log.</span></span> <span data-ttu-id="aaf68-112">Если они по-прежнему отсутствуют, отправьте запрос в службу поддержки, и мы рассмотрим вашу проблему.</span><span class="sxs-lookup"><span data-stu-id="aaf68-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="aaf68-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaf68-113">Next steps</span></span>
<span data-ttu-id="aaf68-114">См. сведения в статье [Часто задаваемые вопросы об отчетах Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="aaf68-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

