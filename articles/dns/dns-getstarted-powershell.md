---
title: "Приступая к работе со службой DNS Azure с помощью PowerShell | Документация Майкрософт"
description: "Узнайте, как создать зону и запись DNS в службе DNS Azure. Это пошаговое руководство описывает создание первых зоны и записи DNS, а также управление ими с помощью PowerShell."
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
ms.openlocfilehash: 48f7ba325f61b4a91c0208b4c99058da801bee19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-powershell"></a><span data-ttu-id="7b712-104">Приступая к работе со службой DNS Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b712-104">Get Started with Azure DNS using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b712-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7b712-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="7b712-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b712-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="7b712-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7b712-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="7b712-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7b712-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="7b712-109">Эта статья поможет вам создать свою первую зону и первую запись DNS с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b712-109">This article walks you through the steps to create your first DNS zone and record using Azure PowerShell.</span></span> <span data-ttu-id="7b712-110">Эти действия также можно выполнить с помощью портала Azure или кроссплатформенного интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="7b712-110">You can also perform these steps using the Azure portal or the cross-platform Azure CLI.</span></span>

<span data-ttu-id="7b712-111">Зона DNS используется для размещения DNS-записей определенного домена.</span><span class="sxs-lookup"><span data-stu-id="7b712-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="7b712-112">Чтобы разместить свой домен в Azure DNS, необходимо создать зону DNS для этого доменного имени.</span><span class="sxs-lookup"><span data-stu-id="7b712-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="7b712-113">Каждая запись DNS для вашего домена создается внутри этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="7b712-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="7b712-114">Наконец, чтобы опубликовать зону DNS в Интернете, необходимо настроить серверы доменных имен для домена.</span><span class="sxs-lookup"><span data-stu-id="7b712-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="7b712-115">Каждый из этих шагов описан ниже.</span><span class="sxs-lookup"><span data-stu-id="7b712-115">Each of these steps is described below.</span></span>

<span data-ttu-id="7b712-116">При выполнении этих инструкций предполагается, что вы уже установили Azure PowerShell и выполнили вход.</span><span class="sxs-lookup"><span data-stu-id="7b712-116">These instructions assume you have already installed and signed in to Azure PowerShell.</span></span> <span data-ttu-id="7b712-117">Чтобы получить справку, см. статью [Как управлять зонами DNS с помощью PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="7b712-117">For help, see [How to manage DNS zones using PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="7b712-118">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7b712-118">Create the resource group</span></span>

<span data-ttu-id="7b712-119">Перед созданием зоны DNS создается группа ресурсов, которая будет включать эту зону DNS.</span><span class="sxs-lookup"><span data-stu-id="7b712-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="7b712-120">Ниже показана команда для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7b712-120">The following shows the command.</span></span>

```powershell
New-AzureRMResourceGroup -name MyResourceGroup -location "westus"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="7b712-121">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7b712-121">Create a DNS zone</span></span>

<span data-ttu-id="7b712-122">Зона DNS создается с помощью командлета `New-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="7b712-122">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="7b712-123">В следующем примере будет создана зона DNS *contoso.com* в группе ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="7b712-123">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="7b712-124">Пример можно использовать для создания зоны DNS, заменив соответствующие значения собственными.</span><span class="sxs-lookup"><span data-stu-id="7b712-124">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyResourceGroup
```

## <a name="create-a-dns-record"></a><span data-ttu-id="7b712-125">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="7b712-125">Create a DNS record</span></span>

<span data-ttu-id="7b712-126">Для создания наборов записей используется командлет `New-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="7b712-126">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="7b712-127">В следующем примере создается запись с относительным именем www в зоне DNS contoso.com, в группе ресурсов MyResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="7b712-127">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="7b712-128">Полное доменное имя набора записей — www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7b712-128">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="7b712-129">Тип записи — A, IP-адрес — 1.2.3.4, а срок жизни составляет 3600 секунд.</span><span class="sxs-lookup"><span data-stu-id="7b712-129">The record type is "A", with IP address "1.2.3.4", and the TTL is 3600 seconds.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName contoso.com -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4")
```

<span data-ttu-id="7b712-130">Сведения о других типах записей, наборах записей с несколькими записями, а также об изменении существующих записей см. в статье [Управление записями DNS в службе DNS Azure с помощью Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="7b712-130">For other record types, for record sets with more than one record, and to modify existing records, see [Manage DNS records and record sets using Azure PowerShell](dns-operations-recordsets.md).</span></span> 


## <a name="view-records"></a><span data-ttu-id="7b712-131">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="7b712-131">View records</span></span>

<span data-ttu-id="7b712-132">Чтобы просмотреть список записей DNS в зоне, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7b712-132">To list the DNS records in your zone, use:</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName contoso.com -ResourceGroupName MyResourceGroup
```


## <a name="update-name-servers"></a><span data-ttu-id="7b712-133">Обновление серверов доменных имен</span><span class="sxs-lookup"><span data-stu-id="7b712-133">Update name servers</span></span>

<span data-ttu-id="7b712-134">Когда вы убедитесь, что зона и записи DNS настроены правильно, необходимо настроить доменное имя для использования серверов доменных имен службы DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="7b712-134">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="7b712-135">Это позволит другим пользователям в Интернете находить ваши записи DNS.</span><span class="sxs-lookup"><span data-stu-id="7b712-135">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="7b712-136">Для получения списка серверов доменных имен для определенной зоны используется командлет `Get-AzureRmDnsZone`:</span><span class="sxs-lookup"><span data-stu-id="7b712-136">The name servers for your zone are given by the `Get-AzureRmDnsZone` cmdlet:</span></span>

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

<span data-ttu-id="7b712-137">Эти серверы доменных имен необходимо настроить с помощью регистратора доменных имен (у которого было приобретено доменное имя).</span><span class="sxs-lookup"><span data-stu-id="7b712-137">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="7b712-138">Регистратор предложит вам вариант настройки серверов доменных имен для домена.</span><span class="sxs-lookup"><span data-stu-id="7b712-138">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="7b712-139">Дополнительные сведения см. в статье [Делегирование домена в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="7b712-139">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="7b712-140">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="7b712-140">Delete all resources</span></span>

<span data-ttu-id="7b712-141">Чтобы удалить все ресурсы, созданные при работе с этой статьей, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="7b712-141">To delete all resources created in this article, take the following step:</span></span>

```powershell
Remove-AzureRMResourceGroup -Name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7b712-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b712-142">Next steps</span></span>

<span data-ttu-id="7b712-143">Дополнительные сведения о службе DNS Azure см. в статье [Обзор Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7b712-143">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="7b712-144">Дополнительные сведения об управлении зонами DNS в службе DNS Azure см. в статье [Как управлять зонами DNS с помощью PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="7b712-144">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using PowerShell](dns-operations-dnszones.md).</span></span>

<span data-ttu-id="7b712-145">Дополнительные сведения об управлении записями DNS в службе DNS Azure см. в статье [Управление записями DNS в службе DNS Azure с помощью Azure PowerShell](dns-operations-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="7b712-145">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using PowerShell](dns-operations-recordsets.md).</span></span>

