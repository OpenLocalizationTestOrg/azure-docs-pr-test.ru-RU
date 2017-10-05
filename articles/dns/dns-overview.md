---
title: "Обзор Azure DNS | Документация Майкрософт"
description: "Обзор служб размещения DNS в Microsoft Azure. Размещение домена в Microsoft Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: 3705457e4c90f8869496f7f5177531bd128d1057
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="4af32-104">Обзор Azure DNS</span><span class="sxs-lookup"><span data-stu-id="4af32-104">Azure DNS overview</span></span>

<span data-ttu-id="4af32-105">Служба доменных имен, или DNS, отвечает за преобразование (или разрешение) имени веб-сайта или службы в IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4af32-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="4af32-106">Azure DNS является службой размещения для доменов DNS, предоставляющей разрешение имен с помощью инфраструктуры Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4af32-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="4af32-107">Размещая домены в Azure, вы можете управлять своими записями DNS с помощью тех же учетных данных, API и инструментов и оплачивать использование, как и другие службы Azure.</span><span class="sxs-lookup"><span data-stu-id="4af32-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Общие сведения о DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="4af32-109">Функции</span><span class="sxs-lookup"><span data-stu-id="4af32-109">Features</span></span>

* <span data-ttu-id="4af32-110">**Надежность и производительность**: домены DNS в Azure DNS размещаются в глобальной сети DNS-серверов Azure.</span><span class="sxs-lookup"><span data-stu-id="4af32-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="4af32-111">Мы используем адресацию любому устройству сети, чтобы на каждый запрос DNS отвечал ближайший доступный DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="4af32-111">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="4af32-112">Это обеспечивает высокую производительность и высокий уровень доступности для вашего домена.</span><span class="sxs-lookup"><span data-stu-id="4af32-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="4af32-113">**Простая интеграция** — службу Azure DNS можно использовать для управления DNS-записями служб Azure, а также для предоставления DNS для внешних ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4af32-113">**Seamless integration** - The Azure DNS service can be used to manage DNS records for your Azure services and can be used to provide DNS for your external resources as well.</span></span> <span data-ttu-id="4af32-114">Azure DNS интегрирована в портал Azure и использует те же учетные данные, данные для выставления счетов и контракты на поддержку, что и другие службы Azure.</span><span class="sxs-lookup"><span data-stu-id="4af32-114">Azure DNS is integrated in the Azure portal and uses the same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="4af32-115">**Безопасность**: работа службы Azure DNS основана на Azure Resource Manager (ARM).</span><span class="sxs-lookup"><span data-stu-id="4af32-115">**Security** - The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="4af32-116">Таким образом она использует преимущества Resource Manager, такие как управление доступом на основе ролей, журналы аудита и блокировка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4af32-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="4af32-117">Доменами и записями можно управлять с помощью портала Azure, командлетов Azure PowerShell и кроссплатформенного Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4af32-117">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="4af32-118">Приложения, для которых необходимо автоматическое управление DNS, можно интегрировать со службой с помощью REST API и пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="4af32-118">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="4af32-119">Azure DNS в настоящее время не поддерживает приобретение доменных имен.</span><span class="sxs-lookup"><span data-stu-id="4af32-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="4af32-120">Если вы хотите приобрести домены, вам потребуется использовать регистратор доменных имен стороннего поставщика.</span><span class="sxs-lookup"><span data-stu-id="4af32-120">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="4af32-121">Регистратор обычно взимает небольшую годовую плату.</span><span class="sxs-lookup"><span data-stu-id="4af32-121">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="4af32-122">Затем вы сможете разместить домены в Azure DNS, чтобы управлять записями DNS.</span><span class="sxs-lookup"><span data-stu-id="4af32-122">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="4af32-123">Дополнительные сведения см. в статье [Делегирование домена в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="4af32-123">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="4af32-124">Цены</span><span class="sxs-lookup"><span data-stu-id="4af32-124">Pricing</span></span>

<span data-ttu-id="4af32-125">Выставление счета за использование DNS выполняется на основании количества зон DNS, размещенных в Azure, и количества запросов DNS.</span><span class="sxs-lookup"><span data-stu-id="4af32-125">DNS billing is based on the number of DNS zones hosted in Azure and by the number of DNS queries.</span></span> <span data-ttu-id="4af32-126">Дополнительные сведения о ценах см. в статье [Цены на Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="4af32-126">To learn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="4af32-127">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="4af32-127">FAQ</span></span>

<span data-ttu-id="4af32-128">Часто задаваемые вопросы о DNS см. в статье [Вопросы и ответы о Azure DNS](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="4af32-128">For frequently asked questions about Azure DNS, see the [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4af32-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4af32-129">Next steps</span></span>

<span data-ttu-id="4af32-130">Дополнительные сведения о записях и зонах DNS см. в [обзоре зон и записей DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="4af32-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="4af32-131">Сведения о [создании зоны DNS](./dns-getstarted-create-dnszone-portal.md) в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="4af32-131">Learn how to [create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="4af32-132">Дополнительные сведения о некоторых других ключевых [сетевых возможностях](../networking/networking-overview.md) Azure.</span><span class="sxs-lookup"><span data-stu-id="4af32-132">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

