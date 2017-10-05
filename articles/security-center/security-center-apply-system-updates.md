---
title: "Применение обновлений системы в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе показано, как реализовать рекомендации центра безопасности Azure **Применить обновления системы** и **Перезагрузить после обновления системы**."
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="f2f10-103">Применение обновлений системы в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="f2f10-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="f2f10-104">Центр безопасности Azure ежедневно проверяет наличие обновлений операционной системы виртуальных машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="f2f10-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="f2f10-105">Центр безопасности получает список доступных критических обновлений и обновлений для системы безопасности из Центра обновления Windows или служб Windows Server Update Services в зависимости от того, какая служба настроена для виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="f2f10-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="f2f10-106">Центр безопасности также проверяет наличие последних обновлений для систем Linux.</span><span class="sxs-lookup"><span data-stu-id="f2f10-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="f2f10-107">Если на виртуальной машине отсутствует обновление системы, центр безопасности порекомендует его применить.</span><span class="sxs-lookup"><span data-stu-id="f2f10-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="f2f10-108">В документе приводится обзор службы с помощью примера развертывания.</span><span class="sxs-lookup"><span data-stu-id="f2f10-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="f2f10-109">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="f2f10-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="f2f10-110">Выполнение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="f2f10-110">Implement the recommendation</span></span>
1. <span data-ttu-id="f2f10-111">В колонке **Рекомендации** выберите **Применить обновления системы**.</span><span class="sxs-lookup"><span data-stu-id="f2f10-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Применение обновлений системы][1]
2. <span data-ttu-id="f2f10-113">В открывшейся колонке **Применить обновления системы** отобразится список обновлений системы, которые отсутствуют на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="f2f10-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="f2f10-114">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f2f10-114">Select a VM.</span></span>

   ![Выбор виртуальной машины][2]
3. <span data-ttu-id="f2f10-116">Откроется колонка со списком отсутствующих обновлений для этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f2f10-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="f2f10-117">Выберите обновление системы.</span><span class="sxs-lookup"><span data-stu-id="f2f10-117">Select a system update.</span></span> <span data-ttu-id="f2f10-118">В этом примере выберем обновление KB3156016.</span><span class="sxs-lookup"><span data-stu-id="f2f10-118">In this example, let’s select KB3156016.</span></span>

   ![Отсутствующие обновления безопасности][3]

4. <span data-ttu-id="f2f10-120">Следуйте указаниям в колонке **обновления для системы безопасности** , чтобы применить отсутствующее обновление.</span><span class="sxs-lookup"><span data-stu-id="f2f10-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Обновление для системы безопасности][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="f2f10-122">Перезагрузка после завершения обновлений системы</span><span class="sxs-lookup"><span data-stu-id="f2f10-122">Reboot after system updates</span></span>
1. <span data-ttu-id="f2f10-123">Вернитесь в колонку **Рекомендации** .</span><span class="sxs-lookup"><span data-stu-id="f2f10-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="f2f10-124">После применения обновлений системы будет создана запись с названием **Перезагрузить после завершения обновлений системы**.</span><span class="sxs-lookup"><span data-stu-id="f2f10-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="f2f10-125">Эта запись свидетельствует о том, что вам нужно перезагрузить виртуальную машину, чтобы завершить применение обновлений системы.</span><span class="sxs-lookup"><span data-stu-id="f2f10-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Перезагрузка после завершения обновлений системы][5]
2. <span data-ttu-id="f2f10-127">Выберите **Перезагрузить после завершения обновлений системы**.</span><span class="sxs-lookup"><span data-stu-id="f2f10-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="f2f10-128">Откроется колонка **Ожидается перезапуск для завершения обновлений системы** со списком виртуальных машин, которые необходимо перезагрузить, чтобы завершить применение обновлений системы.</span><span class="sxs-lookup"><span data-stu-id="f2f10-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Ожидание перезагрузки][6]

<span data-ttu-id="f2f10-130">Перезапустите виртуальную машину из Azure, чтобы завершить процесс.</span><span class="sxs-lookup"><span data-stu-id="f2f10-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="f2f10-131">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="f2f10-131">See also</span></span>
<span data-ttu-id="f2f10-132">Дополнительные сведения о Центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="f2f10-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="f2f10-133">[Настройка политик безопасности в Центре безопасности Azure](security-center-policies.md) — узнайте, как настроить политики безопасности для подписок и групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f10-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f2f10-134">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f10-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f2f10-135">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md) — узнайте, как наблюдать за работоспособностью ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f10-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="f2f10-136">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md) — узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="f2f10-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f2f10-137">[Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md) — узнайте, как отслеживать состояние работоспособности решений партнеров.</span><span class="sxs-lookup"><span data-stu-id="f2f10-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="f2f10-138">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="f2f10-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="f2f10-139">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f10-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
