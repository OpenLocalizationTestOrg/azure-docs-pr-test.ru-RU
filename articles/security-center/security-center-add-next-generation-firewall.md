---
title: "aaaAdd следующего поколения брандмауэра в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** добавьте следующего поколения брандмауэра ** и ** маршрута анализировать трафик через NGFW только **."
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
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="c33a4-103">Добавление брандмауэра следующего поколения в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="c33a4-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="c33a4-104">Центр безопасности Azure может рекомендуем добавить брандмауэром следующего поколения (NGFW) от партнера Майкрософт tooincrease мер по обеспечению безопасности.</span><span class="sxs-lookup"><span data-stu-id="c33a4-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> <span data-ttu-id="c33a4-105">В этом документе описан процесс пример toodo это.</span><span class="sxs-lookup"><span data-stu-id="c33a4-105">This document walks you through an example of how toodo this.</span></span>

> [!NOTE]
> <span data-ttu-id="c33a4-106">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="c33a4-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="c33a4-107">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="c33a4-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="c33a4-108">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="c33a4-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="c33a4-109">В hello **рекомендации** колонке выберите **Добавление следующего поколения брандмауэр**.</span><span class="sxs-lookup"><span data-stu-id="c33a4-109">In hello **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="c33a4-110">![Добавить брандмауэр следующего поколения][1]</span><span class="sxs-lookup"><span data-stu-id="c33a4-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="c33a4-111">В hello **Добавление следующего поколения брандмауэр** колонке выберите конечную точку.</span><span class="sxs-lookup"><span data-stu-id="c33a4-111">In hello **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="c33a4-112">![Выбор конечной точки][2]</span><span class="sxs-lookup"><span data-stu-id="c33a4-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="c33a4-113">Откроется вторая колонка **Добавить брандмауэр следующего поколения** .</span><span class="sxs-lookup"><span data-stu-id="c33a4-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="c33a4-114">Вы можете toouse существующее решение при наличии или можно создать новую.</span><span class="sxs-lookup"><span data-stu-id="c33a4-114">You can choose toouse an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="c33a4-115">В этом примере нет доступных решений, поэтому мы создадим NGFW.</span><span class="sxs-lookup"><span data-stu-id="c33a4-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="c33a4-116">![Создание брандмауэра следующего поколения][3]</span><span class="sxs-lookup"><span data-stu-id="c33a4-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="c33a4-117">toocreate NGFW выберите решение из списка hello интеграции партнеров.</span><span class="sxs-lookup"><span data-stu-id="c33a4-117">toocreate an NGFW, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="c33a4-118">В нашем примере мы выберем **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="c33a4-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="c33a4-119">![Выбор решения брандмауэра следующего поколения][4]</span><span class="sxs-lookup"><span data-stu-id="c33a4-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="c33a4-120">Hello **Check Point** открывает колонку обеспечивает сведения о решении hello партнера.</span><span class="sxs-lookup"><span data-stu-id="c33a4-120">hello **Check Point** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="c33a4-121">Выберите **создать** в колонке сведения hello.</span><span class="sxs-lookup"><span data-stu-id="c33a4-121">Select **Create** in hello information blade.</span></span>
   <span data-ttu-id="c33a4-122">![Колонка со сведениями о брандмауэре][5]</span><span class="sxs-lookup"><span data-stu-id="c33a4-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="c33a4-123">Hello **создать виртуальную машину** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="c33a4-123">hello **Create virtual machine** blade opens.</span></span> <span data-ttu-id="c33a4-124">Здесь можно ввести сведения, необходимые toospin виртуальную машину (VM) под управлением hello NGFW.</span><span class="sxs-lookup"><span data-stu-id="c33a4-124">Here you can enter information required toospin up a virtual machine (VM) that runs hello NGFW.</span></span> <span data-ttu-id="c33a4-125">Выполните действия hello и укажите необходимые сведения NGFW hello.</span><span class="sxs-lookup"><span data-stu-id="c33a4-125">Follow hello steps and provide hello NGFW information required.</span></span> <span data-ttu-id="c33a4-126">Выберите ОК tooapply.</span><span class="sxs-lookup"><span data-stu-id="c33a4-126">Select OK tooapply.</span></span>
   <span data-ttu-id="c33a4-127">![Создание виртуальной машины toorun NGFW][6]</span><span class="sxs-lookup"><span data-stu-id="c33a4-127">![Create virtual machine toorun NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="c33a4-128">Маршрутизация трафика только через NGFW</span><span class="sxs-lookup"><span data-stu-id="c33a4-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="c33a4-129">Вернуть toohello **рекомендации** колонку.</span><span class="sxs-lookup"><span data-stu-id="c33a4-129">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="c33a4-130">Когда вы добавите добавления NGFW с помощью центра безопасности, будет создана запись **Маршрутизировать трафик только через NGFW**.</span><span class="sxs-lookup"><span data-stu-id="c33a4-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="c33a4-131">Эта рекомендация создается только в том случае, если вы установили NGFW с помощью центра безопасности.</span><span class="sxs-lookup"><span data-stu-id="c33a4-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="c33a4-132">При наличии конечных точек с выходом в Интернет, центр обеспечения безопасности рекомендует настраивать правил сетевой группы безопасности, принудительно tooyour входящий трафик ВМ с помощью вашей NGFW.</span><span class="sxs-lookup"><span data-stu-id="c33a4-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic tooyour VM through your NGFW.</span></span>

1. <span data-ttu-id="c33a4-133">В hello **колонке рекомендации**выберите **направить трафик только через NGFW**.</span><span class="sxs-lookup"><span data-stu-id="c33a4-133">In hello **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="c33a4-134">![Route traffic through NGFW only (Маршрутизировать трафик только через NGFW)][7]</span><span class="sxs-lookup"><span data-stu-id="c33a4-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="c33a4-135">Это открывает колонку hello **направить трафик только через NGFW**, в котором перечислены виртуальные машины, которые может направлять трафик.</span><span class="sxs-lookup"><span data-stu-id="c33a4-135">This opens hello blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="c33a4-136">Выберите виртуальную Машину из списка hello.</span><span class="sxs-lookup"><span data-stu-id="c33a4-136">Select a VM from hello list.</span></span>
   <span data-ttu-id="c33a4-137">![Выбор виртуальной машины][8]</span><span class="sxs-lookup"><span data-stu-id="c33a4-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="c33a4-138">Стоечный модуль для hello выбрать ВМ откроется связанные правила для входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="c33a4-138">A blade for hello selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="c33a4-139">Отображенное описание будет содержать дополнительные сведения о возможных дальнейших действиях.</span><span class="sxs-lookup"><span data-stu-id="c33a4-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="c33a4-140">Выберите **изменить правила для входящих подключений** tooproceed с изменением правила входящего подключения.</span><span class="sxs-lookup"><span data-stu-id="c33a4-140">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span> <span data-ttu-id="c33a4-141">Hello ожидается, что **источника** не задано слишком**любой** для конечных точек с выходом в Интернет hello связанных с hello NGFW.</span><span class="sxs-lookup"><span data-stu-id="c33a4-141">hello expectation is that **Source** is not set too**Any** for hello Internet-facing endpoints linked with hello NGFW.</span></span> <span data-ttu-id="c33a4-142">toolearn больше о свойствах hello hello правило для входящего трафика, в разделе [правила NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="c33a4-142">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="c33a4-143">![Настройка правил доступа toolimit][9]
   ![изменить правила для входящего трафика][10]</span><span class="sxs-lookup"><span data-stu-id="c33a4-143">![Configure rules toolimit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="c33a4-144">См. также</span><span class="sxs-lookup"><span data-stu-id="c33a4-144">See also</span></span>
<span data-ttu-id="c33a4-145">В этом документе вы узнали, как tooimplement hello рекомендации центра обеспечения безопасности «Добавить следующего поколения брандмауэр».</span><span class="sxs-lookup"><span data-stu-id="c33a4-145">This document showed you how tooimplement hello Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="c33a4-146">toolearn Дополнительные сведения о NGFWs и hello решение партнера Check Point, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="c33a4-146">toolearn more about NGFWs and hello Check Point partner solution, see hello following:</span></span>

* [<span data-ttu-id="c33a4-147">Next-Generation Firewall</span><span class="sxs-lookup"><span data-stu-id="c33a4-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="c33a4-148">Check Point vSEC</span><span class="sxs-lookup"><span data-stu-id="c33a4-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="c33a4-149">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="c33a4-149">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="c33a4-150">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности.</span><span class="sxs-lookup"><span data-stu-id="c33a4-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="c33a4-151">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="c33a4-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c33a4-152">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c33a4-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="c33a4-153">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="c33a4-153">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c33a4-154">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="c33a4-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="c33a4-155">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="c33a4-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c33a4-156">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="c33a4-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

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
