---
title: "Защита сети в центре безопасности Azure | Документация Майкрософт"
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
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="8a338-103">Защита сети в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="8a338-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="8a338-104">Центр безопасности Azure анализирует состояние безопасности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8a338-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="8a338-105">Когда центр безопасности выявляет потенциальные уязвимости в системе безопасности, он создает рекомендации по настройке необходимых элементов управления.</span><span class="sxs-lookup"><span data-stu-id="8a338-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="8a338-106">Рекомендации относятся к следующим типам ресурсов Azure: виртуальные машины (ВМ), сети, SQL и приложения.</span><span class="sxs-lookup"><span data-stu-id="8a338-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="8a338-107">В этой статье рассматриваются рекомендации, которые касаются сети.</span><span class="sxs-lookup"><span data-stu-id="8a338-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="8a338-108">Основное внимание в рекомендациях для сети уделено брандмауэрам следующего поколения, группам безопасности сети, настройке правил входящего трафика и другим аспектам.</span><span class="sxs-lookup"><span data-stu-id="8a338-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="8a338-109">В таблице ниже приведена справочная информация о доступных рекомендациях, включая действия, выполняемые при применении этих рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="8a338-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="8a338-110">Доступные рекомендации для сети</span><span class="sxs-lookup"><span data-stu-id="8a338-110">Available network recommendations</span></span>
| <span data-ttu-id="8a338-111">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="8a338-111">Recommendation</span></span> | <span data-ttu-id="8a338-112">Описание</span><span class="sxs-lookup"><span data-stu-id="8a338-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="8a338-113">Добавить брандмауэр следующего поколения</span><span class="sxs-lookup"><span data-stu-id="8a338-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="8a338-114">Рекомендует добавить брандмауэр следующего поколения (NGFW) от партнера корпорации Майкрософт для повышения безопасности.</span><span class="sxs-lookup"><span data-stu-id="8a338-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="8a338-115">Route traffic through NGFW only (Маршрутизировать трафик только через NGFW)</span><span class="sxs-lookup"><span data-stu-id="8a338-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="8a338-116">Рекомендует настроить правила группы безопасности сети, которые принудительно передают входящий трафик к виртуальной машине через ваш NGFW.</span><span class="sxs-lookup"><span data-stu-id="8a338-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="8a338-117">Enable Network Security Groups on subnets or virtual machines (Включить группы безопасности сети для подсетей или виртуальных машин)</span><span class="sxs-lookup"><span data-stu-id="8a338-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="8a338-118">Рекомендует включить группы безопасности сети для подсетей или виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8a338-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="8a338-119">Restrict access through Internet facing endpoint (Ограничить доступ через подключенную к Интернету конечную точку)</span><span class="sxs-lookup"><span data-stu-id="8a338-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="8a338-120">Рекомендует настроить правила входящего трафика для групп безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="8a338-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="8a338-121">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="8a338-121">See also</span></span>
<span data-ttu-id="8a338-122">Дополнительные сведения о рекомендациях, которые относятся к другим типам ресурсов Azure, см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="8a338-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="8a338-123">Защита виртуальных машин в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="8a338-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="8a338-124">Защита приложений в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="8a338-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="8a338-125">Защита службы SQL Azure в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="8a338-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="8a338-126">Дополнительные сведения о Центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="8a338-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="8a338-127">[Настройка политик безопасности в Центре безопасности Azure](security-center-policies.md) — узнайте, как настроить политики безопасности для подписок и групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8a338-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8a338-128">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md) — узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="8a338-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="8a338-129">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="8a338-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
