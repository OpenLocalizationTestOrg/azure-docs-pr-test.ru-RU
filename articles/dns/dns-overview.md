---
title: "aaaOverview из Azure DNS | Документы Microsoft"
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
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="c4870-104">Обзор Azure DNS</span><span class="sxs-lookup"><span data-stu-id="c4870-104">Azure DNS overview</span></span>

<span data-ttu-id="c4870-105">Hello доменных имен или DNS, отвечает за преобразование (или разрешение) веб-сайта или службы имя tooits IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c4870-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="c4870-106">Azure DNS является службой размещения для доменов DNS, предоставляющей разрешение имен с помощью инфраструктуры Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c4870-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="c4870-107">При размещении ваших доменов в Azure, вы можете управлять DNS hello записей с помощью учетных данных, API-интерфейсы, средства и выставление счетов как других служб Azure.</span><span class="sxs-lookup"><span data-stu-id="c4870-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Общие сведения о DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="c4870-109">Функции</span><span class="sxs-lookup"><span data-stu-id="c4870-109">Features</span></span>

* <span data-ttu-id="c4870-110">**Надежность и производительность**: домены DNS в Azure DNS размещаются в глобальной сети DNS-серверов Azure.</span><span class="sxs-lookup"><span data-stu-id="c4870-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="c4870-111">Мы используем произвольной рассылки к сети, чтобы каждый запрос DNS будет отвечать на ближайший доступный сервер DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c4870-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="c4870-112">Это обеспечивает высокую производительность и высокий уровень доступности для вашего домена.</span><span class="sxs-lookup"><span data-stu-id="c4870-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="c4870-113">**Полная интеграция** -hello служба Azure DNS может быть toomanage используется DNS-записи для служб Azure, а используемые tooprovide DNS для внешних ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c4870-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="c4870-114">Azure DNS интегрирован в портал Azure hello и hello использует такие же учетные данные, выставления счетов и контрактом на поддержку как других служб Azure.</span><span class="sxs-lookup"><span data-stu-id="c4870-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="c4870-115">**Безопасность** -hello служба Azure DNS основан на Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4870-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="c4870-116">Таким образом она использует преимущества Resource Manager, такие как управление доступом на основе ролей, журналы аудита и блокировка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c4870-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="c4870-117">Ваших доменов и записей можно управлять с помощью hello портал Azure, командлеты Azure PowerShell и hello кросс платформенных Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c4870-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="c4870-118">Приложений, которым требуется автоматическое управление DNS можно интегрировать со службой hello через hello REST API и пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="c4870-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="c4870-119">Azure DNS в настоящее время не поддерживает приобретение доменных имен.</span><span class="sxs-lookup"><span data-stu-id="c4870-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="c4870-120">Если вы хотите toopurchase доменов, необходимо toouse регистратора сторонних доменных имен.</span><span class="sxs-lookup"><span data-stu-id="c4870-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="c4870-121">как правило, Hello регистратора оплата годовой небольшую плату.</span><span class="sxs-lookup"><span data-stu-id="c4870-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="c4870-122">Hello доменов может размещаться в Azure DNS для управления DNS-записей.</span><span class="sxs-lookup"><span data-stu-id="c4870-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="c4870-123">В разделе [делегировать tooAzure домена DNS](dns-domain-delegation.md) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="c4870-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="c4870-124">Цены</span><span class="sxs-lookup"><span data-stu-id="c4870-124">Pricing</span></span>

<span data-ttu-id="c4870-125">DNS выставление счетов основано на hello число зон DNS, размещенных в Azure и hello число запросов DNS.</span><span class="sxs-lookup"><span data-stu-id="c4870-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="c4870-126">Дополнительные сведения о ценах, посетите toolearn [цены на Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="c4870-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="c4870-127">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="c4870-127">FAQ</span></span>

<span data-ttu-id="c4870-128">Часто задаваемые вопросы о Azure DNS. в разделе hello [DNS Azure часто задаваемые вопросы о](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="c4870-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4870-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c4870-129">Next steps</span></span>

<span data-ttu-id="c4870-130">Дополнительные сведения о записях и зонах DNS см. в [обзоре зон и записей DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="c4870-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="c4870-131">Узнайте, каким образом слишком[создать зону DNS](./dns-getstarted-create-dnszone-portal.md) в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="c4870-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="c4870-132">Дополнительные сведения о некоторых hello другой ключ [сетевые возможности](../networking/networking-overview.md) платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="c4870-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

