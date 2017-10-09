---
title: "aaaAzure центра обеспечения безопасности и Windows виртуальных машин в Azure | Документы Microsoft"
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
ms.openlocfilehash: 238bf4e266a24a536d35dd647db6056ab39a1f1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a><span data-ttu-id="fb8da-103">Контроль безопасности виртуальных машин с помощью центра безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="fb8da-103">Monitor virtual machine security by using Azure Security Center</span></span>

<span data-ttu-id="fb8da-104">Центр безопасности Azure поможет получить рекомендации по безопасности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8da-104">Azure Security Center can help you gain visibility into your Azure resource security practices.</span></span> <span data-ttu-id="fb8da-105">Центр безопасности предлагает встроенный мониторинг безопасности.</span><span class="sxs-lookup"><span data-stu-id="fb8da-105">Security Center offers integrated security monitoring.</span></span> <span data-ttu-id="fb8da-106">Это позволяет распознавать угрозы, которые в противном случае могли быть не замечены.</span><span class="sxs-lookup"><span data-stu-id="fb8da-106">It can detect threats that otherwise might go unnoticed.</span></span> <span data-ttu-id="fb8da-107">В этом руководстве вы узнаете о центре безопасности Azure и научитесь:</span><span class="sxs-lookup"><span data-stu-id="fb8da-107">In this tutorial, you learn about Azure Security Center, and how to:</span></span>
 
> [!div class="checklist"]
> * <span data-ttu-id="fb8da-108">Настраивать сбор данных.</span><span class="sxs-lookup"><span data-stu-id="fb8da-108">Set up data collection</span></span>
> * <span data-ttu-id="fb8da-109">Устанавливать политики безопасности.</span><span class="sxs-lookup"><span data-stu-id="fb8da-109">Set up security policies</span></span>
> * <span data-ttu-id="fb8da-110">Просматривать и устранять неполадки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fb8da-110">View and fix configuration health issues</span></span>
> * <span data-ttu-id="fb8da-111">Просматривать обнаруженные угрозы.</span><span class="sxs-lookup"><span data-stu-id="fb8da-111">Review detected threats</span></span>  

## <a name="security-center-overview"></a><span data-ttu-id="fb8da-112">Обзор центра безопасности</span><span class="sxs-lookup"><span data-stu-id="fb8da-112">Security Center overview</span></span>

<span data-ttu-id="fb8da-113">Центр безопасности выявляет потенциальные проблемы в конфигурации виртуальных машины и целевые угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="fb8da-113">Security Center identifies potential virtual machine (VM) configuration issues and targeted security threats.</span></span> <span data-ttu-id="fb8da-114">Это могут быть виртуальные машины, которые отсутствуют в группах безопасности сети, незашифрованные диски и атаки методом подбора по протоколу удаленного рабочего стола (RDP).</span><span class="sxs-lookup"><span data-stu-id="fb8da-114">These might include VMs that are missing network security groups, unencrypted disks, and brute-force Remote Desktop Protocol (RDP) attacks.</span></span> <span data-ttu-id="fb8da-115">Hello сведения отображаются на панели мониторинга центра обеспечения безопасности hello в виде диаграмм для чтения.</span><span class="sxs-lookup"><span data-stu-id="fb8da-115">hello information is shown on hello Security Center dashboard in easy-to-read graphs.</span></span>

<span data-ttu-id="fb8da-116">tooaccess hello панель мониторинга центра обеспечения безопасности, в hello портал Azure, в меню "hello", выберите **центра обеспечения безопасности**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-116">tooaccess hello Security Center dashboard, in hello Azure portal, on hello menu, select  **Security Center**.</span></span> <span data-ttu-id="fb8da-117">На панели мониторинга hello можно проверять работоспособность hello безопасности среды Azure, поиск число текущим рекомендациям и просмотр hello текущее состояние оповещения.</span><span class="sxs-lookup"><span data-stu-id="fb8da-117">On hello dashboard, you can see hello security health of your Azure environment, find a count of current recommendations, and view hello current state of threat alerts.</span></span> <span data-ttu-id="fb8da-118">Можно развернуть каждый toosee высокоуровневые диаграммы более подробно.</span><span class="sxs-lookup"><span data-stu-id="fb8da-118">You can expand each high-level chart toosee more detail.</span></span>

![Панель мониторинга центра безопасности](./media/tutorial-azure-security/asc-dash.png)

<span data-ttu-id="fb8da-120">Центр обеспечения безопасности выходит за рамки данных обнаружения tooprovide рекомендации о проблемах, которые он обнаруживает.</span><span class="sxs-lookup"><span data-stu-id="fb8da-120">Security Center goes beyond data discovery tooprovide recommendations for issues that it detects.</span></span> <span data-ttu-id="fb8da-121">Например, если виртуальная машина была развернута без группы безопасности сети, будет создана рекомендация, содержащая необходимые действия по исправлению.</span><span class="sxs-lookup"><span data-stu-id="fb8da-121">For example, if a VM was deployed without an attached network security group, Security Center displays a recommendation, with remediation steps you can take.</span></span> <span data-ttu-id="fb8da-122">Получение автоматических обновлений, не выходя из контекста hello центра обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="fb8da-122">You get automated remediation without leaving hello context of Security Center.</span></span>  

![Рекомендации](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a><span data-ttu-id="fb8da-124">Настраивать сбор данных.</span><span class="sxs-lookup"><span data-stu-id="fb8da-124">Set up data collection</span></span>

<span data-ttu-id="fb8da-125">Прежде чем видимость можно получить в настройках безопасности для виртуальной Машины, необходимо tooset коллекций центра обеспечения безопасности данных.</span><span class="sxs-lookup"><span data-stu-id="fb8da-125">Before you can get visibility into VM security configurations, you need tooset up Security Center data collection.</span></span> <span data-ttu-id="fb8da-126">Это подразумевает Включение сбора данных и создания данных собираются toohold учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8da-126">This involves turning on data collection and creating an Azure storage account toohold collected data.</span></span> 

1. <span data-ttu-id="fb8da-127">На панели мониторинга hello центра обеспечения безопасности, нажмите кнопку **политики безопасности**, а затем выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="fb8da-127">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span> 
2. <span data-ttu-id="fb8da-128">Выберите **Вкл.** для параметра **Сбор данных**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-128">For **Data collection**, select **On**.</span></span>
3. <span data-ttu-id="fb8da-129">Выберите учетную запись хранилища, toocreate **выберите учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-129">toocreate a storage account, select **Choose a storage account**.</span></span> <span data-ttu-id="fb8da-130">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-130">Then, select **OK**.</span></span>
4. <span data-ttu-id="fb8da-131">На hello **политики безопасности** колонке выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-131">On hello **Security Policy** blade, select **Save**.</span></span> 

<span data-ttu-id="fb8da-132">Hello центра обеспечения безопасности данных коллекции затем установлен агент на всех виртуальных машинах и начинает сбор данных.</span><span class="sxs-lookup"><span data-stu-id="fb8da-132">hello Security Center data collection agent is then installed on all VMs, and data collection begins.</span></span> 

## <a name="set-up-a-security-policy"></a><span data-ttu-id="fb8da-133">Настройка политики безопасности</span><span class="sxs-lookup"><span data-stu-id="fb8da-133">Set up a security policy</span></span>

<span data-ttu-id="fb8da-134">Политики безопасности — это элементы hello используется toodefine, для которых центра обеспечения безопасности, собирает данные и дает рекомендации.</span><span class="sxs-lookup"><span data-stu-id="fb8da-134">Security policies are used toodefine hello items for which Security Center collects data and makes recommendations.</span></span> <span data-ttu-id="fb8da-135">Можно применять наборы toodifferent политики безопасности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8da-135">You can apply different security policies toodifferent sets of Azure resources.</span></span> <span data-ttu-id="fb8da-136">Несмотря на то, что по умолчанию ресурсы Azure вычисляются для всех элементов политики, отдельные элементы политики можно отключать для всех ресурсов Azure или для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fb8da-136">Although by default Azure resources are evaluated against all policy items, you can turn off individual policy items for all Azure resources or for a resource group.</span></span> <span data-ttu-id="fb8da-137">Подробные сведения о настройке политик безопасности в центре безопасности Azure см. в [этой статье](../../security-center/security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="fb8da-137">For in-depth information about Security Center security policies, see [Set security policies in Azure Security Center](../../security-center/security-center-policies.md).</span></span> 

<span data-ttu-id="fb8da-138">tooset политику безопасности для всех ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="fb8da-138">tooset up a security policy for all Azure resources:</span></span>

1. <span data-ttu-id="fb8da-139">На панели мониторинга hello центра обеспечения безопасности, выберите **политики безопасности**и затем выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="fb8da-139">On hello Security Center dashboard, select **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="fb8da-140">Щелкните **Prevention policy** (Политика предотвращения).</span><span class="sxs-lookup"><span data-stu-id="fb8da-140">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="fb8da-141">Включить или отключить элементы политики, которые должны tooapply tooall ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8da-141">Turn on or turn off policy items that you want tooapply tooall Azure resources.</span></span>
4. <span data-ttu-id="fb8da-142">Когда закончите выбирать параметры, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-142">When you're finished selecting your settings, select **OK**.</span></span>
5. <span data-ttu-id="fb8da-143">На hello **политики безопасности** колонке выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-143">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="fb8da-144">tooset политику для определенной группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="fb8da-144">tooset up a policy for a specific resource group:</span></span>

1. <span data-ttu-id="fb8da-145">На панели мониторинга hello центра обеспечения безопасности, выберите **политики безопасности**, а затем выберите группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fb8da-145">On hello Security Center dashboard, select **Security policy**, and then select a resource group.</span></span>
2. <span data-ttu-id="fb8da-146">Щелкните **Prevention policy** (Политика предотвращения).</span><span class="sxs-lookup"><span data-stu-id="fb8da-146">Select **Prevention policy**.</span></span>
3. <span data-ttu-id="fb8da-147">Включить или отключить элементы политики, что требуется tooapply toohello ресурсов в группу.</span><span class="sxs-lookup"><span data-stu-id="fb8da-147">Turn on or turn off policy items that you want tooapply toohello resource group.</span></span>
4. <span data-ttu-id="fb8da-148">В разделе **Наследование** выберите **Уникальный**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-148">Under **INHERITANCE**, select **Unique**.</span></span>
5. <span data-ttu-id="fb8da-149">Когда закончите выбирать параметры, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-149">When you're finished selecting your settings, select **OK**.</span></span>
6. <span data-ttu-id="fb8da-150">На hello **политики безопасности** колонке выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-150">On hello **Security policy** blade, select **Save**.</span></span>  

<span data-ttu-id="fb8da-151">Вы также можете отключить сбор данных для определенной группы ресурсов на этой странице.</span><span class="sxs-lookup"><span data-stu-id="fb8da-151">You also can turn off data collection for a specific resource group on this page.</span></span>

<span data-ttu-id="fb8da-152">В следующем примере hello, уникальный политика была создана для группы ресурсов с именем *myResoureGroup*.</span><span class="sxs-lookup"><span data-stu-id="fb8da-152">In hello following example, a unique policy has been created for a resource group named *myResoureGroup*.</span></span> <span data-ttu-id="fb8da-153">В этой политике отключены рекомендации для шифрования дисков и брандмауэра веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="fb8da-153">In this policy, disk encryption and web application firewall recommendations are turned off.</span></span>

![Уникальная политика](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a><span data-ttu-id="fb8da-155">Просмотр состояния работоспособности конфигурации виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="fb8da-155">View VM configuration health</span></span>

<span data-ttu-id="fb8da-156">После включения сбора данных и задать политику безопасности, центр обеспечения безопасности начинает tooprovide предупреждения и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="fb8da-156">After you've turned on data collection and set a security policy, Security Center begins tooprovide alerts and recommendations.</span></span> <span data-ttu-id="fb8da-157">Как развернуты виртуальные машины, устанавливается hello агента сбора данных.</span><span class="sxs-lookup"><span data-stu-id="fb8da-157">As VMs are deployed, hello data collection agent is installed.</span></span> <span data-ttu-id="fb8da-158">Центр обеспечения безопасности затем заполняется данными для hello новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="fb8da-158">Security Center is then populated with data for hello new VMs.</span></span> <span data-ttu-id="fb8da-159">Подробные сведения о работоспособности конфигурации виртуальных машин см. в статье [Защита виртуальных машин в центре безопасности Azure](../../security-center/security-center-virtual-machine-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="fb8da-159">For in-depth information about VM configuration health, see [Protect your VMs in Security Center](../../security-center/security-center-virtual-machine-recommendations.md).</span></span> 

<span data-ttu-id="fb8da-160">Как данные собираются, группируются hello исправности ресурсов для каждой виртуальной Машины и связанных ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8da-160">As data is collected, hello resource health for each VM and related Azure resource is aggregated.</span></span> <span data-ttu-id="fb8da-161">Hello информация отображается на диаграмме для чтения.</span><span class="sxs-lookup"><span data-stu-id="fb8da-161">hello information is shown in an easy-to-read chart.</span></span> 

<span data-ttu-id="fb8da-162">работоспособность tooview ресурсов:</span><span class="sxs-lookup"><span data-stu-id="fb8da-162">tooview resource health:</span></span>

1.  <span data-ttu-id="fb8da-163">На панели мониторинга hello центра обеспечения безопасности в разделе **исправности ресурсов безопасности**выберите **вычислений**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-163">On hello Security Center dashboard, under **Resource security health**, select **Compute**.</span></span> 
2.  <span data-ttu-id="fb8da-164">На hello **вычислений** колонке выберите **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-164">On hello **Compute** blade, select **Virtual machines**.</span></span> <span data-ttu-id="fb8da-165">Это представление содержит сводку состояния конфигурации hello для всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fb8da-165">This view provides a summary of hello configuration status for all your VMs.</span></span>

![Вычисление работоспособности](./media/tutorial-azure-security/compute-health.png)

<span data-ttu-id="fb8da-167">toosee всех рекомендаций для виртуальной Машины, выберите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fb8da-167">toosee all recommendations for a VM, select hello VM.</span></span> <span data-ttu-id="fb8da-168">Рекомендации и исправления рассматриваются более подробно в следующем разделе hello этого учебника.</span><span class="sxs-lookup"><span data-stu-id="fb8da-168">Recommendations and remediation are covered in more detail in hello next section of this tutorial.</span></span>

## <a name="remediate-configuration-issues"></a><span data-ttu-id="fb8da-169">Исправление проблем конфигурации</span><span class="sxs-lookup"><span data-stu-id="fb8da-169">Remediate configuration issues</span></span>

<span data-ttu-id="fb8da-170">После начала toopopulate с данными конфигурации центра обеспечения безопасности рекомендаций на основе hello политикой безопасности, которые вы настроили.</span><span class="sxs-lookup"><span data-stu-id="fb8da-170">After Security Center begins toopopulate with configuration data, recommendations are made based on hello security policy you set up.</span></span> <span data-ttu-id="fb8da-171">Например если виртуальная машина была настроена без связанной сетевой группы безопасности, рекомендации toocreate один.</span><span class="sxs-lookup"><span data-stu-id="fb8da-171">For instance, if a VM was set up without an associated network security group, a recommendation is made toocreate one.</span></span> 

<span data-ttu-id="fb8da-172">toosee список всех рекомендаций:</span><span class="sxs-lookup"><span data-stu-id="fb8da-172">toosee a list of all recommendations:</span></span> 

1. <span data-ttu-id="fb8da-173">На панели мониторинга hello центра обеспечения безопасности, выберите **рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-173">On hello Security Center dashboard, select **Recommendations**.</span></span>
2. <span data-ttu-id="fb8da-174">Выберите конкретную рекомендацию.</span><span class="sxs-lookup"><span data-stu-id="fb8da-174">Select a specific recommendation.</span></span> <span data-ttu-id="fb8da-175">Отображается список всех ресурсов, для которого hello рекомендация применяется.</span><span class="sxs-lookup"><span data-stu-id="fb8da-175">A list of all resources for which hello recommendation applies appears.</span></span>
3. <span data-ttu-id="fb8da-176">tooapply рекомендации, выберите конкретный ресурс.</span><span class="sxs-lookup"><span data-stu-id="fb8da-176">tooapply a recommendation, select a specific resource.</span></span> 
4. <span data-ttu-id="fb8da-177">Следуйте инструкциям hello действия по исправлению.</span><span class="sxs-lookup"><span data-stu-id="fb8da-177">Follow hello instructions for remediation steps.</span></span> 

<span data-ttu-id="fb8da-178">Во многих случаях центра обеспечения безопасности шаги пригодных к использованию вы сможете tooaddress рекомендации, не выходя из центра обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="fb8da-178">In many cases, Security Center provides actionable steps you can take tooaddress a recommendation without leaving Security Center.</span></span> <span data-ttu-id="fb8da-179">В следующем примере hello центр обеспечения безопасности обнаруживает сетевую группу безопасности, имеет неограниченный правила входящего подключения.</span><span class="sxs-lookup"><span data-stu-id="fb8da-179">In hello following example, Security Center detects a network security group that has an unrestricted inbound rule.</span></span> <span data-ttu-id="fb8da-180">На странице приветствия рекомендаций, можно выбрать hello **изменить правила для входящих подключений** кнопки.</span><span class="sxs-lookup"><span data-stu-id="fb8da-180">On hello recommendation page, you can select hello **Edit inbound rules** button.</span></span> <span data-ttu-id="fb8da-181">Появится пользовательский Интерфейс, который требуется toomodify hello правило Hello.</span><span class="sxs-lookup"><span data-stu-id="fb8da-181">hello UI that is needed toomodify hello rule appears.</span></span> 

![Рекомендации](./media/tutorial-azure-security/remediation.png)

<span data-ttu-id="fb8da-183">После исправления проблем относящиеся к ним рекомендации помечаются как выполненные.</span><span class="sxs-lookup"><span data-stu-id="fb8da-183">As recommendations are remediated, they are marked as resolved.</span></span> 

## <a name="view-detected-threats"></a><span data-ttu-id="fb8da-184">Просмотр обнаруженных угроз</span><span class="sxs-lookup"><span data-stu-id="fb8da-184">View detected threats</span></span>

<span data-ttu-id="fb8da-185">Кроме tooresource рекомендации по конфигурации, центр обеспечения безопасности отображаются оповещения об обнаружении угроз.</span><span class="sxs-lookup"><span data-stu-id="fb8da-185">In addition tooresource configuration recommendations, Security Center displays threat detection alerts.</span></span> <span data-ttu-id="fb8da-186">функция предупреждения об изменении безопасности Hello статистически обрабатывает данные, собранные на каждой виртуальной Машины, журналы Azure сети и угроз безопасности решений toodetect подключенных партнера, к ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="fb8da-186">hello security alerts feature aggregates data collected from each VM, Azure networking logs, and connected partner solutions toodetect security threats against Azure resources.</span></span> <span data-ttu-id="fb8da-187">Подробные сведения о возможностях обнаружения угроз центра безопасности Azure см. в [этой статье](../../security-center/security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="fb8da-187">For in-depth information about Security Center threat detection capabilities, see [Azure Security Center detection capabilities](../../security-center/security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="fb8da-188">функция предупреждения об изменении безопасности Hello требует hello центра обеспечения безопасности, ценовой уровень toobe увеличено с *Free* слишком*Standard*.</span><span class="sxs-lookup"><span data-stu-id="fb8da-188">hello security alerts feature requires hello Security Center pricing tier toobe increased from *Free* too*Standard*.</span></span> <span data-ttu-id="fb8da-189">30-дневной **бесплатной пробной версии** доступен при перемещении toothis выше ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="fb8da-189">A 30-day **free trial** is available when you move toothis higher pricing tier.</span></span> 

<span data-ttu-id="fb8da-190">Ценовая категория hello toochange:</span><span class="sxs-lookup"><span data-stu-id="fb8da-190">toochange hello pricing tier:</span></span>  

1. <span data-ttu-id="fb8da-191">На панели мониторинга hello центра обеспечения безопасности, нажмите кнопку **политики безопасности**, а затем выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="fb8da-191">On hello Security Center dashboard, click **Security policy**, and then select your subscription.</span></span>
2. <span data-ttu-id="fb8da-192">Выберите **ценовую категорию**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-192">Select **Pricing tier**.</span></span>
3. <span data-ttu-id="fb8da-193">Выберите новый уровень hello, а затем выберите **выберите**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-193">Select hello new tier, and then select **Select**.</span></span>
4. <span data-ttu-id="fb8da-194">На hello **политики безопасности** колонке выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb8da-194">On hello **Security policy** blade, select **Save**.</span></span> 

<span data-ttu-id="fb8da-195">После изменения ценовой категории hello, график предупреждения безопасности hello начинает toopopulate в случае обнаружения угроз безопасности.</span><span class="sxs-lookup"><span data-stu-id="fb8da-195">After you've changed hello pricing tier, hello security alerts graph begins toopopulate as security threats are detected.</span></span>

![Оповещения безопасности](./media/tutorial-azure-security/security-alerts.png)

<span data-ttu-id="fb8da-197">Выберите сведения о tooview предупреждения.</span><span class="sxs-lookup"><span data-stu-id="fb8da-197">Select an alert tooview information.</span></span> <span data-ttu-id="fb8da-198">Например можно просмотреть описание hello угроз, время обнаружения hello, все попытки угроз и hello Рекомендуемые исправления.</span><span class="sxs-lookup"><span data-stu-id="fb8da-198">For example, you can see a description of hello threat, hello detection time, all threat attempts, and hello recommended remediation.</span></span> <span data-ttu-id="fb8da-199">В следующем примере hello RDP перебора обнаружен с 294 неудачных попыток протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="fb8da-199">In hello following example, an RDP brute-force attack was detected, with 294 failed RDP attempts.</span></span> <span data-ttu-id="fb8da-200">Рекомендуемое решение также указано.</span><span class="sxs-lookup"><span data-stu-id="fb8da-200">A recommended resolution is provided.</span></span>

![Атака по протоколу RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a><span data-ttu-id="fb8da-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb8da-202">Next steps</span></span>
<span data-ttu-id="fb8da-203">В этом руководстве вы настроили центр безопасности Azure, а затем проверили в нем виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="fb8da-203">In this tutorial, you set up Azure Security Center, and then reviewed VMs in Security Center.</span></span> <span data-ttu-id="fb8da-204">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fb8da-204">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb8da-205">Настраивать сбор данных.</span><span class="sxs-lookup"><span data-stu-id="fb8da-205">Set up data collection</span></span>
> * <span data-ttu-id="fb8da-206">Устанавливать политики безопасности.</span><span class="sxs-lookup"><span data-stu-id="fb8da-206">Set up security policies</span></span>
> * <span data-ttu-id="fb8da-207">Просматривать и устранять неполадки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fb8da-207">View and fix configuration health issues</span></span>
> * <span data-ttu-id="fb8da-208">Просматривать обнаруженные угрозы.</span><span class="sxs-lookup"><span data-stu-id="fb8da-208">Review detected threats</span></span>

<span data-ttu-id="fb8da-209">Переместить следующий учебник toolearn toohello toocreate CI/CD конвейера с Visual Studio Team Services, как виртуальная машина Windows под управлением служб IIS.</span><span class="sxs-lookup"><span data-stu-id="fb8da-209">Advance toohello next tutorial toolearn how toocreate a CI/CD pipeline with Visual Studio Team Services and a Windows VM running IIS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb8da-210">Создание конвейера для непрерывной интеграции с помощью Visual Studio Team Services и IIS</span><span class="sxs-lookup"><span data-stu-id="fb8da-210">Visual Studio Team Services CI/CD pipeline</span></span>](./tutorial-vsts-iis-cicd.md)
