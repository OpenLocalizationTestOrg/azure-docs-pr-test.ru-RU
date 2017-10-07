---
title: "aaaGet работы с DNS Azure с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate DNS зоны и записи в Azure DNS. Это toocreate Пошаговое руководство и управлять вашей первой зоны DNS и записи с помощью PowerShell."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 0f9dead1e4b44fcc74c84a024c41cdfaeb02b5d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="cc8bc-104">Приступая к работе со службой DNS Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc8bc-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc8bc-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="cc8bc-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="cc8bc-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc8bc-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="cc8bc-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="cc8bc-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="cc8bc-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cc8bc-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="cc8bc-109">В этой статье описывается toocreate действия hello вашей первой зоны DNS и запись с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-109">This article walks you through hello steps toocreate your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="cc8bc-110">Также можно выполнить следующие действия с помощью портала Azure hello или hello кросс платформенных Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-110">You can also perform these steps using hello Azure portal or hello cross-platform Azure CLI.</span></span>

<span data-ttu-id="cc8bc-111">Зоны DNS-записей DNS используется toohost hello для определенного домена.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="cc8bc-112">toostart размещение домена в Azure DNS необходимо toocreate зону DNS для этого имени домена.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="cc8bc-113">Каждая запись DNS для вашего домена создается внутри этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="cc8bc-114">Наконец, toopublish toohello Интернета, зоны DNS-сервера требуется tooconfigure hello имя серверов для домена hello.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="cc8bc-115">Каждый из этих шагов описан ниже.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-115">Each of these steps is described below.</span></span>

<span data-ttu-id="cc8bc-116">Эти инструкции предполагают, вы уже установили и вход выполнен tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-116">These instructions assume you have already installed and signed in tooAzure PowerShell.</span></span> <span data-ttu-id="cc8bc-117">Справочные сведения см. в разделе [как toomanage DNS-зоны с помощью PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="cc8bc-117">For help, see [How toomanage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="cc8bc-118">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="cc8bc-118">Create hello resource group</span></span>

<span data-ttu-id="cc8bc-119">Перед созданием hello зоны DNS, зоны DNS hello toocontain создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="cc8bc-120">Hello ниже показана команда hello.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-120">hello following shows hello command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="cc8bc-121">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="cc8bc-121">Create a DNS zone</span></span>

<span data-ttu-id="cc8bc-122">Зоны DNS создается с помощью hello `New-AzureRmDnsZone` командлета.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-122">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="cc8bc-123">Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-123">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="cc8bc-124">Используйте toocreate пример hello зону DNS, подставив собственные значения hello.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-124">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="cc8bc-125">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="cc8bc-125">Create a DNS record</span></span>

<span data-ttu-id="cc8bc-126">Создание наборов записей с помощью hello `New-AzureRmDnsRecordSet` командлета.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-126">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="cc8bc-127">Hello в примере создается запись с hello относительное имя «www» в зону DNS «contoso.com» в группе ресурсов «MyResourceGroup» hello.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-127">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="cc8bc-128">Hello полное имя набора записей hello — «www.contoso.com».</span><span class="sxs-lookup"><span data-stu-id="cc8bc-128">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="cc8bc-129">Тип записи Hello «A» с IP-адресом «1.2.3.4», который hello TTL 3600 секунд.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-129">hello record type is "A", with IP address "1.2.3.4", and hello TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="cc8bc-130">Для других типов записей для наборов записей с более чем одной записи и toomodify существующие записи, в разделе [Управление DNS-записи и наборы записей с помощью Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="cc8bc-130">For other record types, for record sets with more than one record, and toomodify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="cc8bc-131">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="cc8bc-131">View records</span></span>

<span data-ttu-id="cc8bc-132">toolist hello DNS-записи в зоне, используйте:</span><span class="sxs-lookup"><span data-stu-id="cc8bc-132">toolist hello DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="cc8bc-133">Обновление серверов доменных имен</span><span class="sxs-lookup"><span data-stu-id="cc8bc-133">Update name servers</span></span>

<span data-ttu-id="cc8bc-134">Как только будут выполнены, что DNS-зоны и записи были настроены правильно, необходимо tooconfigure домена имя toouse hello Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="cc8bc-135">Это позволяет другим пользователям на hello Internet toofind DNS-записей.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-135">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="cc8bc-136">Hello серверы имен для зоны определяются hello `Get-AzureRmDnsZone` командлета:</span><span class="sxs-lookup"><span data-stu-id="cc8bc-136">hello name servers for your zone are given by hello `Get-AzureRmDnsZone` cmdlet:</span></span>

```powershell
Get-AzureRmDnsZone -ZoneName contoso.com -ResourceGroupName MyResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-b40d-0996b97ed101
Tags                  : {}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org., ns4-01.azure-dns.info.}
NumberOfRecordSets    : 3
MaxNumberOfRecordSets : 5000
```

<span data-ttu-id="cc8bc-137">Эти серверы имен должны быть настроены с помощью регистратора доменных имен hello (которого вы приобрели hello доменное имя).</span><span class="sxs-lookup"><span data-stu-id="cc8bc-137">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="cc8bc-138">Регистратор предлагают tooset параметр hello hello серверов имя домена hello.</span><span class="sxs-lookup"><span data-stu-id="cc8bc-138">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="cc8bc-139">Дополнительные сведения см. в разделе [делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="cc8bc-139">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="cc8bc-140">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="cc8bc-140">Delete all resources</span></span>

<span data-ttu-id="cc8bc-141">toodelete все ресурсы созданы в этой статье hello выполните следующий шаг:</span><span class="sxs-lookup"><span data-stu-id="cc8bc-141">toodelete all resources created in this article, take hello following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cc8bc-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc8bc-142">Next steps</span></span>

<span data-ttu-id="cc8bc-143">toolearn Дополнительные сведения о Azure DNS в разделе [Обзор Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc8bc-143">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="cc8bc-144">toolearn Дополнительные сведения об управлении зонами DNS в Azure DNS, в разделе [Управление DNS зоны в DNS Azure с помощью PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="cc8bc-144">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="cc8bc-145">toolearn Дополнительные сведения об управлении DNS-записи в Azure DNS, в разделе [Управление DNS-записи и записи задает в Azure DNS с помощью PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="cc8bc-145">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

