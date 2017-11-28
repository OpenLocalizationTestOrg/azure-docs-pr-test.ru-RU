---
title: "Отмена привязки учетной записи службы автоматизации Azure к Log Analytics | Документация Майкрософт"
description: "В этой статье объясняется, как отменить связь между учетной записью службы автоматизации Azure и рабочей областью OMS."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 56b09c2cfc14813b5efcb364c580787fec1bf639
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-unlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="6c422-103">Отмена привязки учетной записи службы автоматизации Azure к рабочей области Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6c422-103">How to unlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="6c422-104">Служба автоматизации Azure интегрируется с Log Analytics не только для поддержки упреждающего мониторинга заданий рабочей роли Runbook во всех учетных записях автоматизации. Эта связь также необходима для импорта следующих решений, которые зависят от Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6c422-104">Azure Automation integrates with Log Analytics to not only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import the following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="6c422-105">Управление обновлениями</span><span class="sxs-lookup"><span data-stu-id="6c422-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="6c422-106">Отслеживание изменений</span><span class="sxs-lookup"><span data-stu-id="6c422-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="6c422-107">Запуск и остановка виртуальных машин в нерабочее время</span><span class="sxs-lookup"><span data-stu-id="6c422-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="6c422-108">Если вам больше не требуется интеграция учетной записи службы автоматизации с Log Analytics, вы можете отменить привязку учетной записи непосредственно на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6c422-108">If you decide you no longer wish to integrate your Automation account with Log Analytics, you can unlink your account directly from the Azure portal.</span></span>  <span data-ttu-id="6c422-109">Прежде чем продолжить, необходимо сначала удалить решения, которые упоминались ранее. Иначе вы не сможете выполнить эту процедуру.</span><span class="sxs-lookup"><span data-stu-id="6c422-109">Before you proceed, you will first need to remove the solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="6c422-110">Найдите в статье решение, которое вы импортировали, чтобы узнать, как его удалить.</span><span class="sxs-lookup"><span data-stu-id="6c422-110">Review the topic for the particular solution you have imported to understand the steps required to remove it.</span></span>  

<span data-ttu-id="6c422-111">Удалив эти решения, выполните следующие действия, чтобы отменить привязку учетной записи службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="6c422-111">After you remove these solutions you can perform the following steps to unlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="6c422-112">Удаление связи с рабочей областью</span><span class="sxs-lookup"><span data-stu-id="6c422-112">Unlink workspace</span></span>

1. <span data-ttu-id="6c422-113">На портале Azure откройте свою учетную запись службы автоматизации, а в колонке учетной записи службы автоматизации выберите **Удалить связь с рабочей областью**.</span><span class="sxs-lookup"><span data-stu-id="6c422-113">From the Azure portal, open your Automation account, and in the Automation account blade, in the account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="6c422-114">![Параметр удаления связи с рабочей областью](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="6c422-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="6c422-115">В колонке удаления связи с рабочей областью нажмите кнопку **Удалить связь с рабочей областью**.</span><span class="sxs-lookup"><span data-stu-id="6c422-115">On the Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="6c422-116">![Колонка удаления связи с рабочей областью](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="6c422-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="6c422-117">Появится запрос на подтверждение удаления.</span><span class="sxs-lookup"><span data-stu-id="6c422-117">You will receive a prompt verifying you wish to proceed.</span></span><br><br>
3. <span data-ttu-id="6c422-118">Пока служба автоматизации Azure пытается отменить привязку учетной записи к рабочей области Log Analytics, вы можете отслеживать ход выполнения этой задачи в меню **Уведомления**.</span><span class="sxs-lookup"><span data-stu-id="6c422-118">While Azure Automation attempts to unlink the account your Log Analytics workspace, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="6c422-119">Если вы используете решение управления обновлениями, при необходимости можно удалить следующие элементы, которые больше не нужны после удаления решения.</span><span class="sxs-lookup"><span data-stu-id="6c422-119">If you used the Update Management solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="6c422-120">Обновление расписаний.</span><span class="sxs-lookup"><span data-stu-id="6c422-120">Update schedules.</span></span>  <span data-ttu-id="6c422-121">Каждый элемент имеет имя, которое соответствуют развертыванию обновления, которое вы создали.</span><span class="sxs-lookup"><span data-stu-id="6c422-121">Each will have names that match the update deployments you created)</span></span>

* <span data-ttu-id="6c422-122">Группы гибридных рабочих ролей, созданные для решения.</span><span class="sxs-lookup"><span data-stu-id="6c422-122">Hybrid worker groups created for the solution.</span></span>  <span data-ttu-id="6c422-123">Каждая группа будет иметь приблизительно такое имя: machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8.</span><span class="sxs-lookup"><span data-stu-id="6c422-123">Each will be named similarly to  machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="6c422-124">Если вы используете решение запуска и остановки виртуальных машин в нерабочее время, при необходимости можно удалить следующие элементы, которые больше не нужны после удаления решения.</span><span class="sxs-lookup"><span data-stu-id="6c422-124">If you used the Start/Stop VMs during off-hours solution, optionally you may want to remove the following items that are no longer needed after you remove the solution.</span></span>

* <span data-ttu-id="6c422-125">Расписание запуска и остановки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6c422-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="6c422-126">Рабочие роли Runbook запуска и остановки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6c422-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="6c422-127">Переменные</span><span class="sxs-lookup"><span data-stu-id="6c422-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="6c422-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c422-128">Next steps</span></span>

<span data-ttu-id="6c422-129">Чтобы повторно настроить интеграцию учетной записи службы автоматизации с Log Analytics (OMS), см. инструкции в статье [Пересылка состояния задания и потоков заданий из службы автоматизации в Log Analytics (OMS](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="6c422-129">To reconfigure your Automation account to integrate with OMS Log Analytics, see [Forward job status and job streams from Automation to Log Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 