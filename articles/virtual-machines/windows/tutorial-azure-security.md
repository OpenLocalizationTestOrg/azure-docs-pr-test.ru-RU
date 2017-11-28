---
title: "Центр безопасности Azure и виртуальные машины Windows в Azure | Документация Майкрософт"
description: "Дополнительные сведения о контроле безопасности виртуальных машин Windows в Azure с помощью центра безопасности Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: adb00e28b0b204858a763f83836ee2ac96f8f9e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="d6c94-103">Контроль безопасности виртуальных машин с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="d6c94-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="d6c94-104">Центр безопасности Azure поможет получить рекомендации по безопасности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c94-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="d6c94-105">Центр безопасности предлагает встроенный мониторинг безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6c94-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="d6c94-106">Это позволяет распознавать угрозы, которые в противном случае могли быть не замечены.</span><span class="sxs-lookup"><span data-stu-id="d6c94-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="d6c94-107">В этом руководстве вы узнаете о центре безопасности Azure и научитесь:</span><span class="sxs-lookup"><span data-stu-id="d6c94-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="d6c94-108">Настраивать сбор данных.</span><span class="sxs-lookup"><span data-stu-id="d6c94-108">Set up data collection</span></span>
> * <span data-ttu-id="d6c94-109">Устанавливать политики безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6c94-109">Set up security policies</span></span>
> * <span data-ttu-id="d6c94-110">Просматривать и устранять неполадки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d6c94-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="d6c94-111">Просматривать обнаруженные угрозы.</span><span class="sxs-lookup"><span data-stu-id="d6c94-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="d6c94-112">Обзор центра безопасности</span><span class="sxs-lookup"><span data-stu-id="d6c94-112">Security Center overview</span></span>

<span data-ttu-id="d6c94-113">Центр безопасности выявляет потенциальные проблемы в конфигурации виртуальных машины и целевые угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6c94-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="d6c94-114">Это могут быть виртуальные машины, которые отсутствуют в группах безопасности сети, незашифрованные диски и атаки методом подбора по протоколу удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="d6c94-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="d6c94-115">Эти сведения отображаются на панели мониторинга центра безопасности в виде удобных диаграмм.</span><span class="sxs-lookup"><span data-stu-id="d6c94-115">The information is shown on the Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="d6c94-116">Чтобы получить доступ к панели мониторинга центра безопасности, на портале Azure в меню выберите **Центр безопасности**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-116">To access the Security Center dashboard, in the Azure portal, on the menu, select  **Security Center**.</span></span> <span data-ttu-id="d6c94-117">На панели мониторинга можно просмотреть работоспособность системы безопасности среды Azure, узнать количество текущих рекомендаций и изучить текущее состояние оповещений об угрозах.</span><span class="sxs-lookup"><span data-stu-id="d6c94-117">On the dashboard, you can see the security health of your Azure environment, find a count of current recommendations, and view the current state of threat alerts.</span></span> <span data-ttu-id="d6c94-118">Вы можете развернуть каждую детальную диаграмму, чтобы просмотреть подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="d6c94-118">You can expand each high-level chart to see more detail.</span></span>

![Панель мониторинга центра безопасности](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="d6c94-120">Возможности центра безопасности Azure выходят за пределы обнаружения данных, так как он предоставляет рекомендации для выявленных проблем.</span><span class="sxs-lookup"><span data-stu-id="d6c94-120">Security Center goes beyond data discovery to provide recommendations for issues that it detects.</span></span> <span data-ttu-id="d6c94-121">Например, если виртуальная машина была развернута без группы безопасности сети, будет создана рекомендация, содержащая необходимые действия по исправлению.</span><span class="sxs-lookup"><span data-stu-id="d6c94-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="d6c94-122">Эти рекомендации также дают возможность автоматизировать исправления, не покидая контекст центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c94-122">You get automated remediation without leaving the context of Security Center.</span></span>  

![Рекомендации](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="d6c94-124">Настройка сбора данных</span><span class="sxs-lookup"><span data-stu-id="d6c94-124">Set up data collection</span></span>

<span data-ttu-id="d6c94-125">Прежде чем вы сможете просмотреть конфигурации безопасности виртуальных машин, в центре безопасности нужно настроить сбор данных.</span><span class="sxs-lookup"><span data-stu-id="d6c94-125">Before you can get visibility into VM security configurations, you need to set up Security Center data collection.</span></span> <span data-ttu-id="d6c94-126">Для этого следует включить сбор данных и создать учетную запись хранения Azure, чтобы хранить в ней собранные данные.</span><span class="sxs-lookup"><span data-stu-id="d6c94-126">This involves turning on data collection and creating an Azure storage account to hold collected data.</span></span> 

1. <span data-ttu-id="d6c94-127">На панели мониторинга центра безопасности щелкните **Политика безопасности** и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="d6c94-127">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="d6c94-128">Выберите **Вкл.** для параметра **Сбор данных**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="d6c94-129">Чтобы создать учетную запись хранения, щелкните **Выберите учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-129">To create a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="d6c94-130">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="d6c94-131">В колонке **Политика безопасности** выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-131">On the **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="d6c94-132">После этого на всех виртуальных машинах будет установлен агент сбора данных центра безопасности Azure, который начнет сбор данных.</span><span class="sxs-lookup"><span data-stu-id="d6c94-132">The Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="d6c94-133">Настройка политики безопасности</span><span class="sxs-lookup"><span data-stu-id="d6c94-133">Set up a security policy</span></span>

<span data-ttu-id="d6c94-134">Политика безопасности определяет элементы центра безопасности, для которых собираются данные и предоставляются рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d6c94-134">Security policies are used to define the items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="d6c94-135">Вы можете применять различные политики безопасности к разным наборам ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c94-135">You can apply different security policies to different sets of Azure resources.</span></span> <span data-ttu-id="d6c94-136">Несмотря на то, что по умолчанию ресурсы Azure вычисляются для всех элементов политики, отдельные элементы политики можно отключать для всех ресурсов Azure или для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d6c94-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="d6c94-137">Подробные сведения о настройке политик безопасности в центре безопасности Azure см. в [этой статье](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d6c94-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="d6c94-138">Чтобы настроить политику безопасности для всех ресурсов Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d6c94-138">To set up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="d6c94-139">На панели мониторинга центра безопасности щелкните **Политика безопасности** и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="d6c94-139">On the Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="d6c94-140">Щелкните **Prevention policy** (Политика предотвращения).</span><span class="sxs-lookup"><span data-stu-id="d6c94-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="d6c94-141">Включите или отключите элементы политики, которые должны применяться ко всем ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c94-141">Turn on or turn off policy items that you want to apply to all Azure resources.</span></span>
4. <span data-ttu-id="d6c94-142">Когда закончите выбирать параметры, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="d6c94-143">В колонке **Политика безопасности** выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-143">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="d6c94-144">Чтобы настроить политику для определенной группы ресурсов, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d6c94-144">To set up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="d6c94-145">На панели мониторинга центра безопасности щелкните **Политика безопасности** и выберите группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d6c94-145">On the Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="d6c94-146">Щелкните **Prevention policy** (Политика предотвращения).</span><span class="sxs-lookup"><span data-stu-id="d6c94-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="d6c94-147">Включите или отключите элементы политики, которые должны применяться к группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d6c94-147">Turn on or turn off policy items that you want to apply to the resource group.</span></span>
4. <span data-ttu-id="d6c94-148">В разделе **Наследование** выберите **Уникальный**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="d6c94-149">Когда закончите выбирать параметры, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="d6c94-150">В колонке **Политика безопасности** выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-150">On the **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="d6c94-151">Вы также можете отключить сбор данных для определенной группы ресурсов на этой странице.</span><span class="sxs-lookup"><span data-stu-id="d6c94-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="d6c94-152">В следующем примере для группы ресурсов *myResoureGroup* создается уникальная политика.</span><span class="sxs-lookup"><span data-stu-id="d6c94-152">In the following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="d6c94-153">В этой политике отключены рекомендации для шифрования дисков и брандмауэра веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d6c94-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Уникальная политика](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="d6c94-155">Просмотр состояния работоспособности конфигурации виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d6c94-155">View VM configuration health</span></span>

<span data-ttu-id="d6c94-156">После включения сбора данных и настройки политики безопасности центр безопасности начинает отображать оповещения и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d6c94-156">After you've turned on data collection and set a security policy, Security Center begins to provide alerts and recommendations.</span></span> <span data-ttu-id="d6c94-157">На развертываемые виртуальные машины устанавливается агент сбора данных.</span><span class="sxs-lookup"><span data-stu-id="d6c94-157">As VMs are deployed, the data collection agent is installed.</span></span> <span data-ttu-id="d6c94-158">Центр безопасности Azure заполняется данными для этих новых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d6c94-158">Security Center is then populated with data for the new VMs.</span></span> <span data-ttu-id="d6c94-159">Подробные сведения о работоспособности конфигурации виртуальных машин см. в статье [Защита виртуальных машин в центре безопасности Azure](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="d6c94-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="d6c94-160">По мере сбора данных сведения о работоспособности ресурсов для каждой виртуальной машины и связанного ресурса Azure объединяются.</span><span class="sxs-lookup"><span data-stu-id="d6c94-160">As data is collected, the resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="d6c94-161">Сведения отображаются на удобной для чтения диаграмме.</span><span class="sxs-lookup"><span data-stu-id="d6c94-161">The information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="d6c94-162">Чтобы просмотреть состояние работоспособности ресурса:</span><span class="sxs-lookup"><span data-stu-id="d6c94-162">To view resource health:</span></span>

1.  <span data-ttu-id="d6c94-163">На панели мониторинга центра безопасности в разделе **Resource security health** (Работоспособность системы безопасности ресурсов) выберите **Вычислить**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-163">On the Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="d6c94-164">В колонке **Вычисления** щелкните **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-164">On the **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="d6c94-165">Это представление содержит сводку состояния конфигурации для всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d6c94-165">This view provides a summary of the configuration status for all your VMs.</span></span>

![Вычисление работоспособности](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="d6c94-167">Выберите определенную виртуальную машину, чтобы увидеть все рекомендации для нее.</span><span class="sxs-lookup"><span data-stu-id="d6c94-167">To see all recommendations for a VM, select the VM.</span></span> <span data-ttu-id="d6c94-168">Эти рекомендации подробно описываются в следующем разделе данного руководства.</span><span class="sxs-lookup"><span data-stu-id="d6c94-168">Recommendations and remediation are covered in more detail in the next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="d6c94-169">Исправление проблем конфигурации</span><span class="sxs-lookup"><span data-stu-id="d6c94-169">Remediate configuration issues</span></span>

<span data-ttu-id="d6c94-170">После того, как центр безопасности Azure начинает получать данные конфигурации, на основе настроенной политики безопасности создаются рекомендации.</span><span class="sxs-lookup"><span data-stu-id="d6c94-170">After Security Center begins to populate with configuration data, recommendations are made based on the security policy you set up.</span></span> <span data-ttu-id="d6c94-171">Например, если для виртуальной машины не была настроена связанная группа безопасности сети, создается рекомендация для ее создания.</span><span class="sxs-lookup"><span data-stu-id="d6c94-171">For instance, if a VM was set up without an associated network security group, a recommendation is made to create one.</span></span> 

<span data-ttu-id="d6c94-172">Вот как можно просмотреть список всех рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="d6c94-172">To see a list of all recommendations:</span></span> 

1. <span data-ttu-id="d6c94-173">Щелкните элемент **Рекомендации** на панели мониторинга центра безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6c94-173">On the Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="d6c94-174">Выберите конкретную рекомендацию.</span><span class="sxs-lookup"><span data-stu-id="d6c94-174">Select a specific recommendation.</span></span> <span data-ttu-id="d6c94-175">Откроется колонка со списком всех ресурсов, к которым относится эта рекомендация.</span><span class="sxs-lookup"><span data-stu-id="d6c94-175">A list of all resources for which the recommendation applies appears.</span></span>
3. <span data-ttu-id="d6c94-176">Чтобы применить рекомендацию, выберите конкретный ресурс.</span><span class="sxs-lookup"><span data-stu-id="d6c94-176">To apply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="d6c94-177">Следуйте инструкциям по исправлению.</span><span class="sxs-lookup"><span data-stu-id="d6c94-177">Follow the instructions for remediation steps.</span></span> 

<span data-ttu-id="d6c94-178">Во многих случаях центр безопасности предоставляет практические инструкции, позволяющие выполнить рекомендацию, не покидая центр безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6c94-178">In many cases, Security Center provides actionable steps you can take to address a recommendation without leaving Security Center.</span></span> <span data-ttu-id="d6c94-179">В следующем примере центр безопасности обнаруживает группу безопасности сети с правилом входящего трафика без ограничений.</span><span class="sxs-lookup"><span data-stu-id="d6c94-179">In the following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="d6c94-180">В этой рекомендации можно нажать кнопку **Изменить правила для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-180">On the recommendation page, you can select the **Edit inbound rules** button.</span></span> <span data-ttu-id="d6c94-181">Отобразится пользовательский интерфейс, необходимый для изменения правила.</span><span class="sxs-lookup"><span data-stu-id="d6c94-181">The UI that is needed to modify the rule appears.</span></span> 

![Рекомендации](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="d6c94-183">После исправления проблем относящиеся к ним рекомендации помечаются как выполненные.</span><span class="sxs-lookup"><span data-stu-id="d6c94-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="d6c94-184">Просмотр обнаруженных угроз</span><span class="sxs-lookup"><span data-stu-id="d6c94-184">View detected threats</span></span>

<span data-ttu-id="d6c94-185">Помимо рекомендаций по настройке ресурсов центр безопасности также отображает оповещения об обнаружении угроз.</span><span class="sxs-lookup"><span data-stu-id="d6c94-185">In addition to resource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="d6c94-186">Функция оповещения системы безопасности объединяет данные, полученные с каждой виртуальной машины, из сетевых журналов Azure и подключенных партнерских решений, для обнаружения угроз безопасности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c94-186">The security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions to detect security threats against Azure resources.</span></span> <span data-ttu-id="d6c94-187">Подробные сведения о возможностях обнаружения угроз центра безопасности Azure см. в [этой статье](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="d6c94-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="d6c94-188">Для использования функции оповещения системы безопасности требуется повысить ценовую категорию центра безопасности с *Бесплатный* до *Стандартный*.</span><span class="sxs-lookup"><span data-stu-id="d6c94-188">The security alerts feature requires the Security Center pricing tier to be increased from *Free* to *Standard*.</span></span> <span data-ttu-id="d6c94-189">При переходе на более высокую ценовую категорию предоставляется 30-дневная **бесплатная пробная версия**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-189">A 30-day **free trial** is available when you move to this higher pricing tier.</span></span> 

<span data-ttu-id="d6c94-190">Вот как можно изменить ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="d6c94-190">To change the pricing tier:</span></span>  

1. <span data-ttu-id="d6c94-191">На панели мониторинга центра безопасности щелкните **Политика безопасности** и выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="d6c94-191">On the Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="d6c94-192">Выберите **ценовую категорию**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="d6c94-193">Выберите новую ценовую категорию и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-193">Select the new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="d6c94-194">В колонке **Политика безопасности** выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d6c94-194">On the **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="d6c94-195">После изменения ценовой категории диаграмма оповещений системы безопасности начнет заполняться выявленными угрозами безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6c94-195">After you've changed the pricing tier, the security alerts graph begins to populate as security threats are detected.</span></span>

![Оповещения безопасности](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="d6c94-197">Щелкните оповещение, чтобы увидеть дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="d6c94-197">Select an alert to view information.</span></span> <span data-ttu-id="d6c94-198">Например, можно просмотреть такие сведения об угрозе, как ее описание, время обнаружения, число попыток и рекомендуемые действия по исправлению.</span><span class="sxs-lookup"><span data-stu-id="d6c94-198">For example, you can see a description of the threat, the detection time, all threat attempts, and the recommended remediation.</span></span> <span data-ttu-id="d6c94-199">В следующем примере была обнаружена атака методом подбора по протоколу RDP, которая безуспешно предпринималась 294 раза.</span><span class="sxs-lookup"><span data-stu-id="d6c94-199">In the following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="d6c94-200">Рекомендуемое решение также указано.</span><span class="sxs-lookup"><span data-stu-id="d6c94-200">A recommended resolution is provided.</span></span>

![Атака по протоколу RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="d6c94-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6c94-202">Next steps</span></span>
<span data-ttu-id="d6c94-203">В этом руководстве вы настроили центр безопасности Azure, а затем проверили в нем виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="d6c94-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="d6c94-204">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d6c94-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d6c94-205">Настраивать сбор данных.</span><span class="sxs-lookup"><span data-stu-id="d6c94-205">Set up data collection</span></span>
> * <span data-ttu-id="d6c94-206">Устанавливать политики безопасности.</span><span class="sxs-lookup"><span data-stu-id="d6c94-206">Set up security policies</span></span>
> * <span data-ttu-id="d6c94-207">Просматривать и устранять неполадки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d6c94-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="d6c94-208">Просматривать обнаруженные угрозы.</span><span class="sxs-lookup"><span data-stu-id="d6c94-208">Review detected threats</span></span>

<span data-ttu-id="d6c94-209">Перейдите к следующему руководству, чтобы научиться создавать конвейер CI/CD с помощью Visual Studio Team Services и виртуальной машины Windows под управлением IIS.</span><span class="sxs-lookup"><span data-stu-id="d6c94-209">Advance to the next tutorial to learn how to create a CI/CD pipeline with Visual Studio Team Services and a Windows VM running IIS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6c94-210">Создание конвейера для непрерывной интеграции с помощью Visual Studio Team Services и IIS</span><span class="sxs-lookup"><span data-stu-id="d6c94-210">Visual Studio Team Services CI/CD pipeline</span></span>](./tutorial-vsts-iis-cicd.md)
