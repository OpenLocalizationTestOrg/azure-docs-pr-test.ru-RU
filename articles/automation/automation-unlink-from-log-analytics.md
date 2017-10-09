---
title: "Учетная запись службы автоматизации Azure из службы анализа журналов aaaUnlink | Документы Microsoft"
description: "В этой статье предоставляет общие сведения о том, как toounlink автоматизации Azure учетной записи из рабочей области OMS."
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
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a><span data-ttu-id="36fe1-103">Toounlink автоматической учетной записи из рабочей области аналитики журналов</span><span class="sxs-lookup"><span data-stu-id="36fe1-103">How toounlink your Automation account from a Log Analytics workspace</span></span>

<span data-ttu-id="36fe1-104">Служба автоматизации Azure интегрируется с анализа журналов toonot только поддержка упреждающего мониторинга заданий runbook для всех учетных записей автоматизации, но требуется также при импорте hello следующие решения, которые зависят от службы анализа журналов:</span><span class="sxs-lookup"><span data-stu-id="36fe1-104">Azure Automation integrates with Log Analytics toonot only support proactive monitoring of your runbook jobs across all of your Automation accounts, but is also required when you import hello following solutions that are dependent on Log Analytics:</span></span>

* [<span data-ttu-id="36fe1-105">Управление обновлениями</span><span class="sxs-lookup"><span data-stu-id="36fe1-105">Update Management</span></span>](../operations-management-suite/oms-solution-update-management.md)
* [<span data-ttu-id="36fe1-106">Отслеживание изменений</span><span class="sxs-lookup"><span data-stu-id="36fe1-106">Change Tracking</span></span>](../log-analytics/log-analytics-change-tracking.md)
* [<span data-ttu-id="36fe1-107">Запуск и остановка виртуальных машин в нерабочее время</span><span class="sxs-lookup"><span data-stu-id="36fe1-107">Start/Stop VMs during off-hours</span></span>](automation-solution-vm-management.md)
 
<span data-ttu-id="36fe1-108">Если вы решили, что необходимо прекратить toointegrate ваша учетная запись автоматизации с помощью аналитики журналов, можно разорвать связь учетной записи непосредственно из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="36fe1-108">If you decide you no longer wish toointegrate your Automation account with Log Analytics, you can unlink your account directly from hello Azure portal.</span></span>  <span data-ttu-id="36fe1-109">Прежде чем продолжить, необходимо сначала tooremove hello решения, приведенные выше, в противном случае этот процесс сможет продолжить.</span><span class="sxs-lookup"><span data-stu-id="36fe1-109">Before you proceed, you will first need tooremove hello solutions mentioned earlier, otherwise this process will be prevented from proceeding.</span></span>  <span data-ttu-id="36fe1-110">Просмотрите раздел hello для конкретного решения hello импорта toounderstand hello шаги tooremove его.</span><span class="sxs-lookup"><span data-stu-id="36fe1-110">Review hello topic for hello particular solution you have imported toounderstand hello steps required tooremove it.</span></span>  

<span data-ttu-id="36fe1-111">После удаления этих решений можно выполнить следующие шаги toounlink hello ваша учетная запись автоматизации.</span><span class="sxs-lookup"><span data-stu-id="36fe1-111">After you remove these solutions you can perform hello following steps toounlink your Automation account.</span></span>

## <a name="unlink-workspace"></a><span data-ttu-id="36fe1-112">Удаление связи с рабочей областью</span><span class="sxs-lookup"><span data-stu-id="36fe1-112">Unlink workspace</span></span>

1. <span data-ttu-id="36fe1-113">Hello портал Azure, откройте учетную запись автоматизации и в колонке учетной записи автоматизации hello в колонке hello учетной записи, выберите **разорвать связь рабочей**.</span><span class="sxs-lookup"><span data-stu-id="36fe1-113">From hello Azure portal, open your Automation account, and in hello Automation account blade, in hello account blade, select **Unlink workspace**.</span></span><br><br> <span data-ttu-id="36fe1-114">![Параметр удаления связи с рабочей областью](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span><span class="sxs-lookup"><span data-stu-id="36fe1-114">![Unlink workspace option](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)</span></span><br><br>  
2. <span data-ttu-id="36fe1-115">В колонке рабочей hello отменить связь, нажмите кнопку **разорвать связь worksapce**.</span><span class="sxs-lookup"><span data-stu-id="36fe1-115">On hello Unlink workspace blade, click **Unlink worksapce**.</span></span><br><br> <span data-ttu-id="36fe1-116">![Колонка удаления связи с рабочей областью](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span><span class="sxs-lookup"><span data-stu-id="36fe1-116">![Unlink workspace blade](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).</span></span><br><br>  <span data-ttu-id="36fe1-117">Вы получите приглашение проверка того, что вы хотите tooproceed.</span><span class="sxs-lookup"><span data-stu-id="36fe1-117">You will receive a prompt verifying you wish tooproceed.</span></span><br><br>
3. <span data-ttu-id="36fe1-118">Хотя Azure Automation пытается учетной записи hello toounlink рабочей области аналитики журналов, отслеживания хода hello в **уведомления** меню "hello".</span><span class="sxs-lookup"><span data-stu-id="36fe1-118">While Azure Automation attempts toounlink hello account your Log Analytics workspace, you can track hello progress under **Notifications** from hello menu.</span></span>

<span data-ttu-id="36fe1-119">При использовании решения управления обновлениями hello, при необходимости вы можете hello tooremove следующих элементов, которые больше не нужны после удаления решения hello.</span><span class="sxs-lookup"><span data-stu-id="36fe1-119">If you used hello Update Management solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="36fe1-120">Обновление расписаний.</span><span class="sxs-lookup"><span data-stu-id="36fe1-120">Update schedules.</span></span>  <span data-ttu-id="36fe1-121">Каждый будет иметь имена, которые соответствуют hello развертываний обновлений, созданный)</span><span class="sxs-lookup"><span data-stu-id="36fe1-121">Each will have names that match hello update deployments you created)</span></span>

* <span data-ttu-id="36fe1-122">Гибридной рабочей группы, создаваемые для решения hello.</span><span class="sxs-lookup"><span data-stu-id="36fe1-122">Hybrid worker groups created for hello solution.</span></span>  <span data-ttu-id="36fe1-123">Каждая будет называться аналогично слишком machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).</span><span class="sxs-lookup"><span data-stu-id="36fe1-123">Each will be named similarly too machine1.contoso.com_9ceb8108-26c9-4051-b6b3-227600d715c8).</span></span>

<span data-ttu-id="36fe1-124">При использовании виртуальных машин для запуска и остановки hello во время решения нерабочие часы, при необходимости вы можете hello tooremove следующих элементов, которые больше не нужны после удаления решения hello.</span><span class="sxs-lookup"><span data-stu-id="36fe1-124">If you used hello Start/Stop VMs during off-hours solution, optionally you may want tooremove hello following items that are no longer needed after you remove hello solution.</span></span>

* <span data-ttu-id="36fe1-125">Расписание запуска и остановки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="36fe1-125">Start and stop VM runbook schedules</span></span> 
* <span data-ttu-id="36fe1-126">Рабочие роли Runbook запуска и остановки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="36fe1-126">Start and stop VM runbooks</span></span>
* <span data-ttu-id="36fe1-127">Переменные</span><span class="sxs-lookup"><span data-stu-id="36fe1-127">Variables</span></span>   

## <a name="next-steps"></a><span data-ttu-id="36fe1-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36fe1-128">Next steps</span></span>

<span data-ttu-id="36fe1-129">tooreconfigure вашей toointegrate учетной записи автоматизации с помощью аналитики журналов OMS, в разделе [вперед от tooLog автоматизации Analytics (OMS) состояние задания и задания потоки](automation-manage-send-joblogs-log-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="36fe1-129">tooreconfigure your Automation account toointegrate with OMS Log Analytics, see [Forward job status and job streams from Automation tooLog Analytics (OMS)](automation-manage-send-joblogs-log-analytics.md).</span></span> 
