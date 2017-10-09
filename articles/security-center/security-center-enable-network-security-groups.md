---
title: "aaaEnable группами безопасности сети в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить сетевой безопасности групп **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="7b674-103">Включение групп безопасности сети в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="7b674-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="7b674-104">Центр безопасности Azure порекомендует вам включить группы безопасности сети (NSG), если они еще не включены.</span><span class="sxs-lookup"><span data-stu-id="7b674-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="7b674-105">Nsg содержит список правил список управления доступом (ACL), которые разрешают или запрещают трафик tooyour экземпляров виртуальных Машин в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7b674-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="7b674-106">Группы безопасности сети можно связать с подсетями или отдельными экземплярами виртуальных машин в одной из подсетей.</span><span class="sxs-lookup"><span data-stu-id="7b674-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="7b674-107">Когда NSG связана с подсетью, правила ACL hello применяются tooall экземпляров виртуальных Машин hello в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="7b674-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="7b674-108">Кроме того, tooan трафик отдельных виртуальных Машин может быть ограничен продолжается связывание NSG непосредственно toothat виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7b674-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="7b674-109">более разделе toolearn [что такое группа безопасности сети (NSG)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="7b674-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="7b674-110">Если у вас Nsg включен, центр обеспечения безопасности представляется двумя tooyou рекомендации: включить Сетевые группы безопасности в подсети и включить группы безопасности сети на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="7b674-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="7b674-111">Можно выбрать, какой уровень, подсети или виртуальной Машины, tooapply Nsg.</span><span class="sxs-lookup"><span data-stu-id="7b674-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="7b674-112">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="7b674-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="7b674-113">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="7b674-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="7b674-114">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="7b674-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="7b674-115">В hello **рекомендации** колонке выберите **включить группы безопасности сети** подсетей или виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="7b674-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="7b674-116">![Включение групп безопасности сети][1]</span><span class="sxs-lookup"><span data-stu-id="7b674-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="7b674-117">Это открывает колонку hello **настройки отсутствуют сетевые группы безопасности** для подсетей или виртуальных машин, в зависимости от рекомендаций hello выбранного.</span><span class="sxs-lookup"><span data-stu-id="7b674-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="7b674-118">Установите в подсети или виртуальной машины tooconfigure NSG.</span><span class="sxs-lookup"><span data-stu-id="7b674-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![Настройка группы безопасности сети для подсети][2]

   ![Настройка группы безопасности сети для виртуальной машины][3]
3. <span data-ttu-id="7b674-121">На hello **выберите сетевую группу безопасности** колонке выберите существующей NSG или **создать новый** toocreate NSG.</span><span class="sxs-lookup"><span data-stu-id="7b674-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![Выбрать группу безопасности сети][4]

<span data-ttu-id="7b674-123">При создании NSG, следуйте указаниям hello [как с помощью Nsg toomanage hello портал Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate NSG и набор правил безопасности.</span><span class="sxs-lookup"><span data-stu-id="7b674-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="7b674-124">См. также</span><span class="sxs-lookup"><span data-stu-id="7b674-124">See also</span></span>
<span data-ttu-id="7b674-125">В этой статье показано, как tooimplement hello центра обеспечения безопасности, рекомендации «включить Сетевые группы безопасности» для подсетей или виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7b674-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="7b674-126">toolearn Дополнительные сведения о включении Nsg, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="7b674-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="7b674-127">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="7b674-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="7b674-128">Как с помощью Nsg toomanage hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7b674-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="7b674-129">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="7b674-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="7b674-130">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7b674-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="7b674-131">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="7b674-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="7b674-132">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="7b674-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="7b674-133">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="7b674-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="7b674-134">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="7b674-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="7b674-135">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="7b674-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="7b674-136">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) --получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="7b674-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
