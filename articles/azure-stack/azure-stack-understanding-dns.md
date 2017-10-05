---
title: "Основные сведения о DNS-сервер в стек Azure | Документы Microsoft"
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
ms.openlocfilehash: 2a19b435777ba848835dcd90a1ebb8a0cbcb0e9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="93e7f-103">Общие сведения о имена IDN для стек Azure</span><span class="sxs-lookup"><span data-stu-id="93e7f-103">Introducing iDNS for Azure Stack</span></span>
================================

<span data-ttu-id="93e7f-104">имена IDN — это функция Azure стека, который позволяет разрешать внешние имена DNS (например, http://www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="93e7f-104">iDNS is a feature in Azure Stack that allows you to resolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="93e7f-105">Он также позволяет зарегистрировать имена внутреннюю виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="93e7f-105">It also allows you to register internal virtual network names.</span></span> <span data-ttu-id="93e7f-106">Таким образом, можно без необходимости предоставляют пользовательские записи DNS-сервера, на той же виртуальной сети разрешить по имени, а не IP-адреса виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="93e7f-106">By doing so, you can resolve VMs on the same virtual network by name rather than IP address, without having to provide custom DNS server entries.</span></span>

<span data-ttu-id="93e7f-107">Это то, что всегда было существует в Azure, но она доступна в Windows Server 2016 и стек Azure слишком.</span><span class="sxs-lookup"><span data-stu-id="93e7f-107">It’s something that’s always been there in Azure, but it's available in Windows Server 2016 and Azure Stack too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="93e7f-108">Каково предназначение IDN.</span><span class="sxs-lookup"><span data-stu-id="93e7f-108">What does iDNS do?</span></span>
<span data-ttu-id="93e7f-109">Имена IDN в стек Azure позволяет получить следующие возможности без указания пользовательские записи DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="93e7f-109">With iDNS in Azure Stack, you get the following capabilities, without having to specify custom DNS server entries.</span></span>

* <span data-ttu-id="93e7f-110">Общие службы разрешения имен DNS для рабочих нагрузок клиентов.</span><span class="sxs-lookup"><span data-stu-id="93e7f-110">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="93e7f-111">Принудительное службы DNS для разрешения имен и регистрация DNS в виртуальной сети клиента.</span><span class="sxs-lookup"><span data-stu-id="93e7f-111">Authoritative DNS service for name resolution and DNS registration within the tenant virtual network.</span></span>
* <span data-ttu-id="93e7f-112">Служба рекурсивный DNS для разрешения имен Интернета из виртуальных машин клиентов.</span><span class="sxs-lookup"><span data-stu-id="93e7f-112">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="93e7f-113">Клиенты больше не требуется задать пользовательские записи DNS для разрешения имен Интернета (например, www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="93e7f-113">Tenants no longer need to specify custom DNS entries to resolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="93e7f-114">По-прежнему можно подключить собственный DNS-сервера и использовать пользовательские DNS-серверы, если необходимо.</span><span class="sxs-lookup"><span data-stu-id="93e7f-114">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="93e7f-115">Но теперь, если нужно иметь возможность разрешения имен DNS Интернета и подключаться к другим виртуальным машинам в той же виртуальной сети, не нужно указывать ничего, и он будет работать.</span><span class="sxs-lookup"><span data-stu-id="93e7f-115">But now, if you just want to be able to resolve Internet DNS names and be able to connect to other virtual machines in the same virtual network, you don’t need to specify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="93e7f-116">Что делает имена IDN не?</span><span class="sxs-lookup"><span data-stu-id="93e7f-116">What does iDNS not do?</span></span>
<span data-ttu-id="93e7f-117">Какие имена IDN не позволяет делать является создание записи DNS для имени, которое можно привести из вне виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="93e7f-117">What iDNS does not allow you to do is create a DNS record for a name that can be resolved from outside the virtual network.</span></span>

<span data-ttu-id="93e7f-118">В Azure у вас есть возможность указать метка DNS-имени, которое может быть связано с общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="93e7f-118">In Azure, you have the option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="93e7f-119">Можно выбрать метки (префикс), но Azure выбирает суффикс, который зависит от региона, в котором можно создавать общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="93e7f-119">You can choose the label (prefix), but Azure chooses the suffix, which is based on the region in which you create the public IP address.</span></span>

![Метка снимок экрана DNS-имени](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="93e7f-121">В приведенном выше рисунке Azure создаст» «запись в DNS для метка DNS-имени, указанному в зоне **westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="93e7f-121">In the image above, Azure will create an “A” record in DNS for the DNS name label specified under the zone **westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="93e7f-122">Префикс и суффикс вместе образуют полное доменное имя (FQDN), можно разрешить с в любом месте на общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="93e7f-122">The prefix and the suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on the public Internet.</span></span>

<span data-ttu-id="93e7f-123">Стек Azure только поддерживаются имена IDN регистрация внутреннее имя, поэтому его нельзя выполнить следующие.</span><span class="sxs-lookup"><span data-stu-id="93e7f-123">Azure Stack only supports iDNS for internal name registration, so it cannot do the following.</span></span>

* <span data-ttu-id="93e7f-124">Создание записи DNS в существующей размещенной зоны DNS (например, local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="93e7f-124">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="93e7f-125">Создайте зону DNS (например, Contoso.com).</span><span class="sxs-lookup"><span data-stu-id="93e7f-125">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="93e7f-126">Создайте запись в создаваемую зону DNS.</span><span class="sxs-lookup"><span data-stu-id="93e7f-126">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="93e7f-127">Поддерживает покупку доменных имен.</span><span class="sxs-lookup"><span data-stu-id="93e7f-127">Support the purchase of domain names.</span></span>

