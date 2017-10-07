---
title: "aaaApply системных обновлений в центре безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** применения обновлений системы ** и ** перезагрузки после обновления системы **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="30cc0-103">Применение обновлений системы в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="30cc0-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="30cc0-104">Центр безопасности Azure ежедневно проверяет наличие обновлений операционной системы виртуальных машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="30cc0-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="30cc0-105">Центр безопасности получает список доступных критических обновлений и обновлений для системы безопасности из Центра обновления Windows или служб Windows Server Update Services в зависимости от того, какая служба настроена для виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="30cc0-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="30cc0-106">Центр обеспечения безопасности также проверяет наличие последних обновлений hello в системах Linux.</span><span class="sxs-lookup"><span data-stu-id="30cc0-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="30cc0-107">Если на виртуальной машине отсутствует обновление системы, центр безопасности порекомендует его применить.</span><span class="sxs-lookup"><span data-stu-id="30cc0-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="30cc0-108">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="30cc0-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="30cc0-109">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="30cc0-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="30cc0-110">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="30cc0-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="30cc0-111">В hello **рекомендации** колонке выберите **применения обновлений системы**.</span><span class="sxs-lookup"><span data-stu-id="30cc0-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Применение обновлений системы][1]
2. <span data-ttu-id="30cc0-113">Hello **применения обновлений системы** открывается колонка, отображающая список виртуальных машин отсутствуют обновления для системы.</span><span class="sxs-lookup"><span data-stu-id="30cc0-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="30cc0-114">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="30cc0-114">Select a VM.</span></span>

   ![Выбор виртуальной машины][2]
3. <span data-ttu-id="30cc0-116">Откроется колонка со списком отсутствующих обновлений для этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="30cc0-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="30cc0-117">Выберите обновление системы.</span><span class="sxs-lookup"><span data-stu-id="30cc0-117">Select a system update.</span></span> <span data-ttu-id="30cc0-118">В этом примере выберем обновление KB3156016.</span><span class="sxs-lookup"><span data-stu-id="30cc0-118">In this example, let’s select KB3156016.</span></span>

   ![Отсутствующие обновления безопасности][3]

4. <span data-ttu-id="30cc0-120">Следуйте указаниям hello hello **обновление системы безопасности** tooapply колонке hello отсутствующие обновления.</span><span class="sxs-lookup"><span data-stu-id="30cc0-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Обновление для системы безопасности][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="30cc0-122">Перезагрузка после завершения обновлений системы</span><span class="sxs-lookup"><span data-stu-id="30cc0-122">Reboot after system updates</span></span>
1. <span data-ttu-id="30cc0-123">Вернуть toohello **рекомендации** колонку.</span><span class="sxs-lookup"><span data-stu-id="30cc0-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="30cc0-124">После применения обновлений системы будет создана запись с названием **Перезагрузить после завершения обновлений системы**.</span><span class="sxs-lookup"><span data-stu-id="30cc0-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="30cc0-125">Эта запись позволяет узнать необходимые tooreboot hello ВМ toocomplete hello процесс применения обновлений системы.</span><span class="sxs-lookup"><span data-stu-id="30cc0-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Перезагрузка после завершения обновлений системы][5]
2. <span data-ttu-id="30cc0-127">Выберите **Перезагрузить после завершения обновлений системы**.</span><span class="sxs-lookup"><span data-stu-id="30cc0-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="30cc0-128">При этом откроется **это ожидание toocomplete системных обновлений** колонки, отображается список виртуальных машин, необходимо toorestart toocomplete hello применить процесс обновления системы.</span><span class="sxs-lookup"><span data-stu-id="30cc0-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Ожидание перезагрузки][6]

<span data-ttu-id="30cc0-130">Перезапустите hello ВМ из Azure toocomplete hello процесса.</span><span class="sxs-lookup"><span data-stu-id="30cc0-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="30cc0-131">См. также</span><span class="sxs-lookup"><span data-stu-id="30cc0-131">See also</span></span>
<span data-ttu-id="30cc0-132">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="30cc0-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="30cc0-133">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="30cc0-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="30cc0-134">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="30cc0-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="30cc0-135">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="30cc0-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="30cc0-136">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="30cc0-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="30cc0-137">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="30cc0-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="30cc0-138">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="30cc0-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="30cc0-139">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="30cc0-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
