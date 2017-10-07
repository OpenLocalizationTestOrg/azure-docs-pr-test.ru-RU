---
title: "aaaUnderstanding DNS-сервер в стек Azure | Документы Microsoft"
description: "Основные сведения о DNS функций и возможностей в стек Azure"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: f60128cf98af8e98ac2bc87172b54132ed06cd8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="9ddc8-103">Общие сведения о имена IDN для стек Azure</span><span class="sxs-lookup"><span data-stu-id="9ddc8-103">Introducing iDNS for Azure Stack</span></span>
================================

<span data-ttu-id="9ddc8-104">имена IDN — это функция Azure стека, который позволяет вам tooresolve внешних DNS-имен (например, http://www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="9ddc8-104">iDNS is a feature in Azure Stack that allows you tooresolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="9ddc8-105">Она также позволяет имена tooregister внутреннюю виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-105">It also allows you tooregister internal virtual network names.</span></span> <span data-ttu-id="9ddc8-106">Таким образом, можно разрешить виртуальных машин на hello одной виртуальной сети по имени, а не IP-адресов, без необходимости tooprovide пользовательские записи DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-106">By doing so, you can resolve VMs on hello same virtual network by name rather than IP address, without having tooprovide custom DNS server entries.</span></span>

<span data-ttu-id="9ddc8-107">Это то, что всегда было существует в Azure, но она доступна в Windows Server 2016 и стек Azure слишком.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-107">It’s something that’s always been there in Azure, but it's available in Windows Server 2016 and Azure Stack too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="9ddc8-108">Каково предназначение IDN.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-108">What does iDNS do?</span></span>
<span data-ttu-id="9ddc8-109">Имена IDN в стек Azure позволяет получить hello следующие возможности, без необходимости toospecify пользовательские записи DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-109">With iDNS in Azure Stack, you get hello following capabilities, without having toospecify custom DNS server entries.</span></span>

* <span data-ttu-id="9ddc8-110">Общие службы разрешения имен DNS для рабочих нагрузок клиентов.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-110">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="9ddc8-111">Принудительное службы DNS для разрешения имен и регистрация DNS в виртуальную сеть клиента hello.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-111">Authoritative DNS service for name resolution and DNS registration within hello tenant virtual network.</span></span>
* <span data-ttu-id="9ddc8-112">Служба рекурсивный DNS для разрешения имен Интернета из виртуальных машин клиентов.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-112">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="9ddc8-113">Клиенты больше не нужна toospecify пользовательские DNS записи tooresolve имен Интернета (например, www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="9ddc8-113">Tenants no longer need toospecify custom DNS entries tooresolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="9ddc8-114">По-прежнему можно подключить собственный DNS-сервера и использовать пользовательские DNS-серверы, если необходимо.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-114">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="9ddc8-115">Но теперь только имена DNS Интернета могут tooresolve toobe и сможете Здравствуйте, tooconnect tooother виртуальных машин в одной виртуальной сети, не требуется toospecify ничего, и он будет работать.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-115">But now, if you just want toobe able tooresolve Internet DNS names and be able tooconnect tooother virtual machines in hello same virtual network, you don’t need toospecify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="9ddc8-116">Что делает имена IDN не?</span><span class="sxs-lookup"><span data-stu-id="9ddc8-116">What does iDNS not do?</span></span>
<span data-ttu-id="9ddc8-117">Какие имена IDN не позволит toodo является создание записи DNS для имени, которое можно привести вне hello в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-117">What iDNS does not allow you toodo is create a DNS record for a name that can be resolved from outside hello virtual network.</span></span>

<span data-ttu-id="9ddc8-118">В Azure у вас hello указания метка DNS-имени, которое может быть связано с общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-118">In Azure, you have hello option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="9ddc8-119">Можно выбрать метки hello (префикс), но Azure выбирает hello суффикс, который основан на hello регион, в котором можно создавать hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-119">You can choose hello label (prefix), but Azure chooses hello suffix, which is based on hello region in which you create hello public IP address.</span></span>

![Метка снимок экрана DNS-имени](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="9ddc8-121">Hello рисунке выше Azure создаст» «запись в DNS для метка DNS-имени hello, указанные в разделе зоны hello **westus.cloudapp.azure.com**. Суффикс префикс и hello вместе образуют полное доменное имя (FQDN), можно разрешить в любом месте на hello общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-121">In hello image above, Azure will create an “A” record in DNS for hello DNS name label specified under hello zone **westus.cloudapp.azure.com**. The prefix and hello suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on hello public Internet.</span></span>

<span data-ttu-id="9ddc8-122">Azure стека только поддерживает имена IDN регистрация внутреннее имя, поэтому его нельзя hello следующие.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-122">Azure Stack only supports iDNS for internal name registration, so it cannot do hello following.</span></span>

* <span data-ttu-id="9ddc8-123">Создание записи DNS в существующей размещенной зоны DNS (например, local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="9ddc8-123">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="9ddc8-124">Создайте зону DNS (например, Contoso.com).</span><span class="sxs-lookup"><span data-stu-id="9ddc8-124">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="9ddc8-125">Создайте запись в создаваемую зону DNS.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-125">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="9ddc8-126">Поддерживает покупку hello доменных имен.</span><span class="sxs-lookup"><span data-stu-id="9ddc8-126">Support hello purchase of domain names.</span></span>

