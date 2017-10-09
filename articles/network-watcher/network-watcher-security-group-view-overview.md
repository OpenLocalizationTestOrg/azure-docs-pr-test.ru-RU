---
title: "представление группы toosecurity aaaIntroduction в Наблюдатель сети Azure | Документы Microsoft"
description: "Эта страница содержит краткую hello возможность представления безопасности Наблюдатель сети"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="834c2-103">Представление группы безопасности toonetwork введение в инспектор сети Azure</span><span class="sxs-lookup"><span data-stu-id="834c2-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="834c2-104">Группы безопасности сети (NSG) связаны на уровне подсети или сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="834c2-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="834c2-105">При наличии связи на уровне подсети, оно применяется экземпляров виртуальных Машин tooall hello в подсети hello.</span><span class="sxs-lookup"><span data-stu-id="834c2-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="834c2-106">Сетевая группа безопасности представление возвращает все hello настроен Nsg и правилах, которые связаны на уровне сетевого Адаптера и подсеть для виртуальной машины, предоставляя понимания конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="834c2-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="834c2-107">Кроме того правила безопасности hello возвращаются для каждого hello сетевых адаптеров на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="834c2-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="834c2-108">С помощью представления групп безопасности сети можно оценить сетевые уязвимости виртуальной машины, например открытые порты.</span><span class="sxs-lookup"><span data-stu-id="834c2-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="834c2-109">Можно также проверить, если вашей группе безопасности сети работает должным образом на основе [сравнение hello настроен и hello правила безопасности](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="834c2-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="834c2-110">Более расширенный вариант использования относится к области соответствия требованиям безопасности и аудита.</span><span class="sxs-lookup"><span data-stu-id="834c2-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="834c2-111">Можно определить предписываемый набор правил безопасности, используемый в качестве модели для контроля безопасности в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="834c2-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="834c2-112">Аудита периодических соответствия может осуществляться программным образом, сравнивая hello конкретные правила с hello действующие правила для каждой из виртуальных машин hello в сети.</span><span class="sxs-lookup"><span data-stu-id="834c2-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="834c2-113">В hello портала правила разделены действующим, подсети, сетевого интерфейса и по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="834c2-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="834c2-114">Это обеспечивает простое представление hello правил, применяемых tooa виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="834c2-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="834c2-115">Кнопку загрузки предоставляется tooeasily загрузить все правила безопасности hello независимо от того, вкладка «hello» в CSV-файл.</span><span class="sxs-lookup"><span data-stu-id="834c2-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![Представление групп безопасности][1]

<span data-ttu-id="834c2-117">Правила могут быть выбраны и открывается новая колонка tooshow hello сетевой группы безопасности, исходный и целевой префиксы.</span><span class="sxs-lookup"><span data-stu-id="834c2-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="834c2-118">Из этой колонки можно перейти непосредственно toohello ресурсов группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="834c2-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![Детализация][2]

### <a name="next-steps"></a><span data-ttu-id="834c2-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="834c2-120">Next steps</span></span>

<span data-ttu-id="834c2-121">Узнайте, как tooaudit сетевой безопасности группы параметров, посетив [параметров аудита сетевой группы безопасности с помощью PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="834c2-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









