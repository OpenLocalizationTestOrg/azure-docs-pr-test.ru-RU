---
title: "Добавление брандмауэра следующего поколения в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе показано, как выполнить рекомендации центра безопасности **Добавить брандмауэр следующего поколения** и **Route traffic through NGFW only** (Маршрутизировать трафик только через NGFW)."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 30589d0a943517c03394a3aae7c03c8094e78c1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="28a3a-103">Добавление брандмауэра следующего поколения в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="28a3a-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="28a3a-104">Для повышения безопасности центр безопасности Azure может порекомендовать вам добавить брандмауэр следующего поколения (NGFW) от партнера корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="28a3a-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> <span data-ttu-id="28a3a-105">В этом документе вы найдете пример применения такой рекомендации.</span><span class="sxs-lookup"><span data-stu-id="28a3a-105">This document walks you through an example of how to do this.</span></span>

> [!NOTE]
> <span data-ttu-id="28a3a-106">В документе приводится обзор службы с помощью примера развертывания.</span><span class="sxs-lookup"><span data-stu-id="28a3a-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="28a3a-107">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="28a3a-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="28a3a-108">Выполнение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="28a3a-108">Implement the recommendation</span></span>
1. <span data-ttu-id="28a3a-109">В колонке **Рекомендации** выберите **Добавление брандмауэра следующего поколения**.</span><span class="sxs-lookup"><span data-stu-id="28a3a-109">In the **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="28a3a-110">![Добавить брандмауэр следующего поколения][1]</span><span class="sxs-lookup"><span data-stu-id="28a3a-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="28a3a-111">В колонке **Добавить брандмауэр следующего поколения** выберите конечную точку.</span><span class="sxs-lookup"><span data-stu-id="28a3a-111">In the **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="28a3a-112">![Выбор конечной точки][2]</span><span class="sxs-lookup"><span data-stu-id="28a3a-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="28a3a-113">Откроется вторая колонка **Добавить брандмауэр следующего поколения** .</span><span class="sxs-lookup"><span data-stu-id="28a3a-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="28a3a-114">Можно использовать существующее решение (если оно доступно) или создать новое.</span><span class="sxs-lookup"><span data-stu-id="28a3a-114">You can choose to use an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="28a3a-115">В этом примере нет доступных решений, поэтому мы создадим NGFW.</span><span class="sxs-lookup"><span data-stu-id="28a3a-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="28a3a-116">![Создание брандмауэра следующего поколения][3]</span><span class="sxs-lookup"><span data-stu-id="28a3a-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="28a3a-117">Чтобы создать NGFW, выберите решение из списка решений партнеров по интеграции.</span><span class="sxs-lookup"><span data-stu-id="28a3a-117">To create an NGFW, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="28a3a-118">В нашем примере мы выберем **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="28a3a-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="28a3a-119">![Выбор решения брандмауэра следующего поколения][4]</span><span class="sxs-lookup"><span data-stu-id="28a3a-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="28a3a-120">Откроется колонка **Check Point** , в которой содержатся сведения о решении партнера.</span><span class="sxs-lookup"><span data-stu-id="28a3a-120">The **Check Point** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="28a3a-121">В колонке сведений щелкните **Создать** .</span><span class="sxs-lookup"><span data-stu-id="28a3a-121">Select **Create** in the information blade.</span></span>
   <span data-ttu-id="28a3a-122">![Колонка со сведениями о брандмауэре][5]</span><span class="sxs-lookup"><span data-stu-id="28a3a-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="28a3a-123">Откроется колонка **Создание виртуальной машины** .</span><span class="sxs-lookup"><span data-stu-id="28a3a-123">The **Create virtual machine** blade opens.</span></span> <span data-ttu-id="28a3a-124">Здесь можно ввести сведения, необходимые для настройки виртуальной машины, на которой будет запущен NGFW.</span><span class="sxs-lookup"><span data-stu-id="28a3a-124">Here you can enter information required to spin up a virtual machine (VM) that runs the NGFW.</span></span> <span data-ttu-id="28a3a-125">Следуйте инструкциям и укажите требуемые данные NGFW.</span><span class="sxs-lookup"><span data-stu-id="28a3a-125">Follow the steps and provide the NGFW information required.</span></span> <span data-ttu-id="28a3a-126">Нажмите кнопку "ОК", чтобы применить введенные данные.</span><span class="sxs-lookup"><span data-stu-id="28a3a-126">Select OK to apply.</span></span>
   <span data-ttu-id="28a3a-127">![Создание виртуальной машины для выполнения NGFW][6]</span><span class="sxs-lookup"><span data-stu-id="28a3a-127">![Create virtual machine to run NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="28a3a-128">Маршрутизация трафика только через NGFW</span><span class="sxs-lookup"><span data-stu-id="28a3a-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="28a3a-129">Вернитесь в колонку **Рекомендации** .</span><span class="sxs-lookup"><span data-stu-id="28a3a-129">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="28a3a-130">Когда вы добавите добавления NGFW с помощью центра безопасности, будет создана запись **Маршрутизировать трафик только через NGFW**.</span><span class="sxs-lookup"><span data-stu-id="28a3a-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="28a3a-131">Эта рекомендация создается только в том случае, если вы установили NGFW с помощью центра безопасности.</span><span class="sxs-lookup"><span data-stu-id="28a3a-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="28a3a-132">При наличии подключенных к Интернету конечных точек центр безопасности порекомендует настроить правила группы безопасности сети, которые принудительно передают входящий трафик на виртуальную машину через NGFW.</span><span class="sxs-lookup"><span data-stu-id="28a3a-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic to your VM through your NGFW.</span></span>

1. <span data-ttu-id="28a3a-133">В колонке **Рекомендации** выберите **Маршрутизировать трафик только через NGFW**.</span><span class="sxs-lookup"><span data-stu-id="28a3a-133">In the **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="28a3a-134">![Route traffic through NGFW only (Маршрутизировать трафик только через NGFW)][7]</span><span class="sxs-lookup"><span data-stu-id="28a3a-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="28a3a-135">Откроется колонка **Маршрутизация трафика только через NGFW**, в которой перечислены виртуальные машины с возможностью перенаправления трафика.</span><span class="sxs-lookup"><span data-stu-id="28a3a-135">This opens the blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="28a3a-136">Выберите виртуальную машину из списка.</span><span class="sxs-lookup"><span data-stu-id="28a3a-136">Select a VM from the list.</span></span>
   <span data-ttu-id="28a3a-137">![Выбор виртуальной машины][8]</span><span class="sxs-lookup"><span data-stu-id="28a3a-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="28a3a-138">Откроется колонка для выбранной виртуальной машины, содержащая связанные правила входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="28a3a-138">A blade for the selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="28a3a-139">Отображенное описание будет содержать дополнительные сведения о возможных дальнейших действиях.</span><span class="sxs-lookup"><span data-stu-id="28a3a-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="28a3a-140">Выберите **Изменить правила для входящего трафика** , чтобы перейти к изменению правила входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="28a3a-140">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span> <span data-ttu-id="28a3a-141">Ожидается, что для параметра **Источник** конечных веб-точек, связанных с NGFW, не задано значение **Все**.</span><span class="sxs-lookup"><span data-stu-id="28a3a-141">The expectation is that **Source** is not set to **Any** for the Internet-facing endpoints linked with the NGFW.</span></span> <span data-ttu-id="28a3a-142">Чтобы узнать больше о свойствах правила входящего трафика, ознакомьтесь с [правилами группы безопасности сети](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="28a3a-142">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="28a3a-143">![Настройка правил ограничения доступа][9]
   ![Изменение правила входящего трафика][10]</span><span class="sxs-lookup"><span data-stu-id="28a3a-143">![Configure rules to limit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="28a3a-144">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="28a3a-144">See also</span></span>
<span data-ttu-id="28a3a-145">В этом документе показано, как выполнить рекомендацию центра безопасности "Добавить брандмауэр следующего поколения".</span><span class="sxs-lookup"><span data-stu-id="28a3a-145">This document showed you how to implement the Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="28a3a-146">Для получения дополнительных сведений о NGFW и решении партнера Check Point ознакомьтесь со статьями:</span><span class="sxs-lookup"><span data-stu-id="28a3a-146">To learn more about NGFWs and the Check Point partner solution, see the following:</span></span>

* [<span data-ttu-id="28a3a-147">Next-Generation Firewall</span><span class="sxs-lookup"><span data-stu-id="28a3a-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="28a3a-148">Check Point vSEC</span><span class="sxs-lookup"><span data-stu-id="28a3a-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="28a3a-149">Дополнительные сведения о Центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="28a3a-149">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="28a3a-150">[Настройка политик безопасности в Центре безопасности Azure](security-center-policies.md) — узнайте, как настраивать политики безопасности.</span><span class="sxs-lookup"><span data-stu-id="28a3a-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="28a3a-151">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="28a3a-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="28a3a-152">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md) — узнайте, как наблюдать за работоспособностью ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="28a3a-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="28a3a-153">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md) — узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="28a3a-153">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="28a3a-154">[Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md) — узнайте, как отслеживать состояние работоспособности решений партнеров.</span><span class="sxs-lookup"><span data-stu-id="28a3a-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="28a3a-155">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="28a3a-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="28a3a-156">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="28a3a-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
