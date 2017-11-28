---
title: "aaaRestrict доступ с помощью конечных точек с выходом в Интернет в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** ограничение доступа через конечную точку **, подключенных к Интернету."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="ad512-103">Ограничение доступа через подключенную к Интернету конечную точку в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="ad512-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="ad512-104">Центр безопасности Azure будет рекомендовать ограничить доступ через подключенную к Интернету конечную точку, если в какой-либо группе безопасности сети есть одно или несколько правил входящего трафика, разрешающих доступ с "любого" исходного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="ad512-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="ad512-105">Открытие доступа слишком «any» могут включить злоумышленники tooaccess ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ad512-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="ad512-106">Центр безопасности Майкрософт рекомендует изменять эти правила для входящих подключений toorestrict доступа toosource IP-адресов, фактически требуется доступ.</span><span class="sxs-lookup"><span data-stu-id="ad512-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="ad512-107">Эта рекомендация создается для любого порта, не являющегося веб-портом, для которого в качестве источника указано значение "Любой".</span><span class="sxs-lookup"><span data-stu-id="ad512-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="ad512-108">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="ad512-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="ad512-109">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="ad512-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="ad512-110">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="ad512-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="ad512-111">В hello **колонке рекомендации**выберите **ограничить доступ через конечную точку сети Интернет**.</span><span class="sxs-lookup"><span data-stu-id="ad512-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Ограничение доступа через подключенную к Интернету конечную точку][1]
2. <span data-ttu-id="ad512-113">Это открывает колонку hello **ограничить доступ через конечную точку сети Интернет**.</span><span class="sxs-lookup"><span data-stu-id="ad512-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="ad512-114">Эта колонка список hello виртуальных машин (ВМ) с правила для входящих подключений, создать угрозу для безопасности.</span><span class="sxs-lookup"><span data-stu-id="ad512-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="ad512-115">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ad512-115">Select a VM.</span></span>

   ![Выбор виртуальной машины][2]
3. <span data-ttu-id="ad512-117">Hello **NSG** колонке отображаются данные сетевой группы безопасности, связанные правила для входящих подключений, и hello связанных виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="ad512-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="ad512-118">Выберите **изменить правила для входящих подключений** tooproceed с изменением правила входящего подключения.</span><span class="sxs-lookup"><span data-stu-id="ad512-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Колонка "Группа безопасности сети"][3]
4. <span data-ttu-id="ad512-120">На hello **безопасности правила для входящих подключений** колонке выберите hello tooedit правило для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="ad512-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="ad512-121">В этом примере выберем **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="ad512-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Правила безопасности для входящего трафика][4]

   <span data-ttu-id="ad512-123">Обратите внимание, что вы также можете выбрать **по умолчанию правила** toosee hello набор правил по умолчанию, содержащиеся в все Nsg.</span><span class="sxs-lookup"><span data-stu-id="ad512-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="ad512-124">правила по умолчанию Hello нельзя удалить, но, так как они будут назначены более низкий уровень приоритета, они могут быть переопределены созданных вами правил hello.</span><span class="sxs-lookup"><span data-stu-id="ad512-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="ad512-125">Узнайте больше о [правилах по умолчанию](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="ad512-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Правила по умолчанию][5]
5. <span data-ttu-id="ad512-127">На hello **AllowWeb** колонки, изменение свойств hello hello правило для входящего трафика, который hello **источника** — это IP-адрес или блок IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ad512-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="ad512-128">toolearn больше о свойствах hello hello правило для входящего трафика, в разделе [правила NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="ad512-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Изменение правила входящего трафика][6]

## <a name="see-also"></a><span data-ttu-id="ad512-130">См. также</span><span class="sxs-lookup"><span data-stu-id="ad512-130">See also</span></span>
<span data-ttu-id="ad512-131">В этой статье показано, как tooimplement hello центра обеспечения безопасности, рекомендации «ограничить доступ через конечную точку в Интернете».</span><span class="sxs-lookup"><span data-stu-id="ad512-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="ad512-132">toolearn Дополнительные сведения о включении Nsg и правилах, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="ad512-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="ad512-133">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="ad512-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="ad512-134">Как с помощью Nsg toomanage hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ad512-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="ad512-135">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="ad512-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="ad512-136">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md)— Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ad512-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ad512-137">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md)— узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="ad512-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ad512-138">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md)— Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ad512-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="ad512-139">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md)--Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="ad512-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="ad512-140">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="ad512-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="ad512-141">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md)— часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="ad512-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="ad512-142">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/)--получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="ad512-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
