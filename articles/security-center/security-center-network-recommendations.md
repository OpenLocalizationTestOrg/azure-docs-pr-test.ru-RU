---
title: "aaaProtecting сети в центр безопасности Azure | Документы Microsoft"
description: "В этом документе рассматриваются рекомендации из центра безопасности Azure, которые помогают защитить вашу сеть Azure и обеспечить соответствие политикам безопасности."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="5597c-103">Защита сети в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="5597c-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="5597c-104">Центр безопасности Azure анализирует состояние безопасности hello ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="5597c-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="5597c-105">Когда центр обеспечения безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации, которые hello процесс настройки hello необходимые элементы управления.</span><span class="sxs-lookup"><span data-stu-id="5597c-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="5597c-106">Рекомендации относятся типы ресурсов tooAzure: виртуальных машин (ВМ), сети, SQL и приложениями.</span><span class="sxs-lookup"><span data-stu-id="5597c-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="5597c-107">В этой статье рассматриваются рекомендации, которые применяются tooyour сети.</span><span class="sxs-lookup"><span data-stu-id="5597c-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="5597c-108">Основное внимание в рекомендациях для сети уделено брандмауэрам следующего поколения, группам безопасности сети, настройке правил входящего трафика и другим аспектам.</span><span class="sxs-lookup"><span data-stu-id="5597c-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="5597c-109">Использовать таблицу hello ниже как toohelp ссылку, вы понимаете рекомендации доступную сеть hello и назначение каждого из них при его применении.</span><span class="sxs-lookup"><span data-stu-id="5597c-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="5597c-110">Доступные рекомендации для сети</span><span class="sxs-lookup"><span data-stu-id="5597c-110">Available network recommendations</span></span>
| <span data-ttu-id="5597c-111">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="5597c-111">Recommendation</span></span> | <span data-ttu-id="5597c-112">Описание</span><span class="sxs-lookup"><span data-stu-id="5597c-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="5597c-113">Добавить брандмауэр следующего поколения</span><span class="sxs-lookup"><span data-stu-id="5597c-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="5597c-114">Рекомендует добавить брандмауэра следующего поколения (NGFW) от партнера Майкрософт tooincrease мер по обеспечению безопасности.</span><span class="sxs-lookup"><span data-stu-id="5597c-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="5597c-115">Route traffic through NGFW only (Маршрутизировать трафик только через NGFW)</span><span class="sxs-lookup"><span data-stu-id="5597c-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="5597c-116">Рекомендует настраивать группы (NSG) правила сетевой безопасности, заставляющие tooyour входящий трафик ВМ с помощью вашей NGFW.</span><span class="sxs-lookup"><span data-stu-id="5597c-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="5597c-117">Enable Network Security Groups on subnets or virtual machines (Включить группы безопасности сети для подсетей или виртуальных машин)</span><span class="sxs-lookup"><span data-stu-id="5597c-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="5597c-118">Рекомендует включить группы безопасности сети для подсетей или виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5597c-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="5597c-119">Restrict access through Internet facing endpoint (Ограничить доступ через подключенную к Интернету конечную точку)</span><span class="sxs-lookup"><span data-stu-id="5597c-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="5597c-120">Рекомендует настроить правила входящего трафика для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="5597c-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="5597c-121">См. также</span><span class="sxs-lookup"><span data-stu-id="5597c-121">See also</span></span>
<span data-ttu-id="5597c-122">Дополнительные сведения о рекомендации, которые применяются tooother типы ресурсов Azure см. в разделе ниже hello toolearn:</span><span class="sxs-lookup"><span data-stu-id="5597c-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="5597c-123">Защита виртуальных машин в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="5597c-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="5597c-124">Защита приложений в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="5597c-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="5597c-125">Защита службы SQL Azure в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="5597c-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="5597c-126">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="5597c-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="5597c-127">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5597c-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="5597c-128">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="5597c-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="5597c-129">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="5597c-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
