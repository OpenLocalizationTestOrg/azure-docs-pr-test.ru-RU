---
title: "Размещение зон обратного просмотра DNS в Azure DNS | Документация Майкрософт"
description: "Узнайте, как использовать Azure DNS, чтобы разместить зоны обратного просмотра DNS для диапазонов IP-адресов"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="0ff97-103">Размещение зон обратного просмотра DNS в Azure DNS</span><span class="sxs-lookup"><span data-stu-id="0ff97-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="0ff97-104">В этой статье описано размещение зон обратного просмотра DNS для назначенных диапазонов IP-адресов в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="0ff97-105">Диапазоны IP-адресов, представленные зоной обратного просмотра, должны быть назначены организации (как правило, поставщиком услуг Интернета).</span><span class="sxs-lookup"><span data-stu-id="0ff97-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="0ff97-106">Чтобы настроить обратные зоны DNS для принадлежащего Azure IP-адреса, назначенного службе Azure, см. раздел о [настройке обратного просмотра для IP-адресов, выделенных службе Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="0ff97-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="0ff97-107">Перед прочтением этой статьи ознакомьтесь со статьей [Основные сведения об обратной зоне DNS и ее поддержке в Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0ff97-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="0ff97-108">Эта статья поможет вам создать свою первую зону обратного просмотра и обратную запись DNS с помощью портала Azure, Azure PowerShell, Azure CLI 1.0 или Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0ff97-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="0ff97-109">Создание зоны обратного просмотра DNS</span><span class="sxs-lookup"><span data-stu-id="0ff97-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="0ff97-110">Войдите на [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="0ff97-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="0ff97-111">В главном меню последовательно выберите **Создать** > **Сети**, а затем щелкните **Зона DNS**, чтобы открыть колонку **Создание зоны DNS**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![Зона DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="0ff97-113">В колонке **Создание зоны DNS** укажите имя зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="0ff97-114">Для префиксов IPv4 и IPv6 имя зоны формируется по-разному.</span><span class="sxs-lookup"><span data-stu-id="0ff97-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="0ff97-115">Чтобы указать имя зоны, выполните инструкции для [IPv4](#ipv4) или [IPv6](#ipv6).</span><span class="sxs-lookup"><span data-stu-id="0ff97-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="0ff97-116">По завершении нажмите кнопку **Создать**, чтобы создать зону.</span><span class="sxs-lookup"><span data-stu-id="0ff97-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="0ff97-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="0ff97-117">IPv4</span></span>

<span data-ttu-id="0ff97-118">Имя зоны обратного просмотра IPv4 формируется на основе диапазона IP-адресов, который она представляет.</span><span class="sxs-lookup"><span data-stu-id="0ff97-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="0ff97-119">Имя должно быть указано в формате `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="0ff97-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="0ff97-120">Примеры см. в [обзоре записей в обратной зоне DNS и поддержки в Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="0ff97-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="0ff97-121">Создавая бесклассовую зону обратного просмотра DNS в Azure DNS, в имени зоны необходимо использовать дефис (`-`) вместо косой черты (/).</span><span class="sxs-lookup"><span data-stu-id="0ff97-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="0ff97-122">Например, для диапазона IP-адресов 192.0.2.128/26 в качестве имени зоны нужно использовать `128-26.2.0.192.in-addr.arpa`, а не `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="0ff97-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="0ff97-123">Стандарты DNS поддерживают оба варианта, но имена зон DNS, содержащие символ косой черты (`/`), не поддерживаются в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="0ff97-124">В примере ниже показано, как создать зону обратного просмотра DNS класса C с именем `2.0.192.in-addr.arpa` в Azure DNS при помощи портала Azure:</span><span class="sxs-lookup"><span data-stu-id="0ff97-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Создание зоны DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="0ff97-126">Параметр "Расположение группы ресурсов" относится к расположению группы ресурсов и никак не влияет на расположение зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="0ff97-127">Расположение зоны DNS всегда является глобальным и не отображается.</span><span class="sxs-lookup"><span data-stu-id="0ff97-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="0ff97-128">Ниже приведены примеры выполнения этой задачи с помощью Azure PowerShell и Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="0ff97-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0ff97-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff97-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0ff97-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0ff97-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="0ff97-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="0ff97-132">IPv6</span></span>

<span data-ttu-id="0ff97-133">Имя зоны обратного просмотра IPv6 должно быть указано в формате `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="0ff97-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="0ff97-134">Примеры см. в [обзоре записей в обратной зоне DNS и поддержки в Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="0ff97-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="0ff97-135">В примере ниже показано, как создать зону обратного просмотра DNS IPv6 с именем `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` в Azure DNS при помощи портала Azure:</span><span class="sxs-lookup"><span data-stu-id="0ff97-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Создание зоны DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="0ff97-137">Параметр "Расположение группы ресурсов" относится к расположению группы ресурсов и никак не влияет на расположение зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="0ff97-138">Расположение зоны DNS всегда является глобальным и не отображается.</span><span class="sxs-lookup"><span data-stu-id="0ff97-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="0ff97-139">Ниже приведены примеры выполнения этой задачи с помощью Azure PowerShell и Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="0ff97-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0ff97-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff97-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="0ff97-141">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="0ff97-142">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="0ff97-143">Делегирование зоны обратного просмотра DNS</span><span class="sxs-lookup"><span data-stu-id="0ff97-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="0ff97-144">Создав зону обратного просмотра DNS, убедитесь, что она делегирована из родительской зоны.</span><span class="sxs-lookup"><span data-stu-id="0ff97-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="0ff97-145">Делегирование DNS позволяет процессу разрешения имен DNS находить серверы имен, на которых размещена зона обратного просмотра DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="0ff97-146">После этого серверы имен могут отвечать на обратные запросы DNS для IP-адресов в указанном диапазоне.</span><span class="sxs-lookup"><span data-stu-id="0ff97-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="0ff97-147">Для зон прямого просмотра делегирование зоны DNS описано в разделе [Делегирование домена в Azure DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="0ff97-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="0ff97-148">Делегирование для зон обратного просмотра выполняется аналогичным образом.</span><span class="sxs-lookup"><span data-stu-id="0ff97-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="0ff97-149">Единственное различие — серверы имен настраиваются с помощью поставщика услуг Интернета, предоставившим вам диапазон IP-адресов, а не с помощью регистратора доменных имен.</span><span class="sxs-lookup"><span data-stu-id="0ff97-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="0ff97-150">Создание записи DNS типа PTR</span><span class="sxs-lookup"><span data-stu-id="0ff97-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="0ff97-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="0ff97-151">IPv4</span></span>

<span data-ttu-id="0ff97-152">Следующий пример демонстрирует создание записи типа PTR для зоны обратного просмотра DNS в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="0ff97-153">Сведения о других типах записей и об изменении существующих записей см. в статье [Управление записями и наборами записей DNS с помощью портала Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ff97-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="0ff97-154">В верхней части этой колонки **Зона DNS** щелкните **Набор записей**, чтобы открыть колонку **Добавление набора записей**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![Зона DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="0ff97-156">Откройте колонку **Добавление набора записей**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="0ff97-157">Выберите **PTR** в меню **Тип**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="0ff97-158">Имя набора записей для записи типа PTR должно представлять собой оставшуюся часть адреса IPv4 в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="0ff97-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="0ff97-159">В этом примере первые три октета уже указаны как часть имени зоны (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="0ff97-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="0ff97-160">Таким образом, в поле имени содержится только последний октет.</span><span class="sxs-lookup"><span data-stu-id="0ff97-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="0ff97-161">Например, для ресурса с IP-адресом 192.0.2.15 можно назвать набор записей **15**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="0ff97-162">В поле **Доменное имя** введите полное доменное имя (FQDN) ресурса, использующего IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0ff97-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="0ff97-163">В нижней части колонки нажмите кнопку **ОК**, чтобы создать запись DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![Добавление набора записей](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="0ff97-165">Ниже приведены примеры выполнения этой задачи с помощью PowerShell и Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0ff97-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0ff97-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff97-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="0ff97-167">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="0ff97-168">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="0ff97-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="0ff97-169">IPv6</span></span>

<span data-ttu-id="0ff97-170">Следующий пример демонстрирует процесс создания записи типа PTR.</span><span class="sxs-lookup"><span data-stu-id="0ff97-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="0ff97-171">Сведения о других типах записей и об изменении существующих записей см. в статье [Управление записями и наборами записей DNS с помощью портала Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ff97-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="0ff97-172">В верхней части колонки **Зона DNS** щелкните **Набор записей**, чтобы открыть колонку **Добавление набора записей**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="0ff97-174">Откройте колонку **Добавление набора записей**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="0ff97-175">Выберите **PTR** в меню **Тип**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="0ff97-176">Имя набора записей для записи типа PTR должно представлять собой оставшуюся часть адреса IPv6 в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="0ff97-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="0ff97-177">Сжатие за счет нулей не должно использоваться.</span><span class="sxs-lookup"><span data-stu-id="0ff97-177">It must not include any zero compression.</span></span> <span data-ttu-id="0ff97-178">В этом примере первые 64 бита IPv6 уже указаны как часть имени зоны (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="0ff97-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="0ff97-179">Таким образом, в поле имени содержатся только последние 64 бита.</span><span class="sxs-lookup"><span data-stu-id="0ff97-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="0ff97-180">Последние 64 бита IP-адреса вводятся в обратном порядке, в качестве разделителя между каждым шестнадцатеричным числом используется точка.</span><span class="sxs-lookup"><span data-stu-id="0ff97-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="0ff97-181">Например, для ресурса с IP-адресом 2001:0db8:abdc:0000:f524:10bc:1af9:405e набор записей можно назвать **e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**.</span><span class="sxs-lookup"><span data-stu-id="0ff97-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="0ff97-182">В поле **Доменное имя** введите полное доменное имя (FQDN) ресурса, использующего IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0ff97-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="0ff97-183">В нижней части колонки нажмите кнопку **ОК**, чтобы создать запись DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![Колонка добавления набора записей](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="0ff97-185">Ниже приведены примеры выполнения этой задачи с помощью PowerShell и Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0ff97-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0ff97-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff97-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="0ff97-187">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="0ff97-188">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="0ff97-189">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="0ff97-189">View Records</span></span>

<span data-ttu-id="0ff97-190">Чтобы просмотреть созданные записи, перейдите к зоне DNS на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff97-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="0ff97-191">В нижней части колонки **Зона DNS** отображаются записи для зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="0ff97-192">Должны отобразиться записи типа NS и SOA по умолчанию, которые создаются в каждой зоне, а также все новые записи, созданные вами.</span><span class="sxs-lookup"><span data-stu-id="0ff97-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="0ff97-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="0ff97-193">IPv4</span></span>

<span data-ttu-id="0ff97-194">Колонка зоны DNS с записями IPv4 типа PTR:</span><span class="sxs-lookup"><span data-stu-id="0ff97-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="0ff97-196">В примерах ниже показано, как просмотреть записи типа PTR с помощью PowerShell или Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="0ff97-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0ff97-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff97-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0ff97-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0ff97-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="0ff97-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="0ff97-200">IPv6</span></span>

<span data-ttu-id="0ff97-201">Колонка зоны DNS с записями IPv6 типа PTR:</span><span class="sxs-lookup"><span data-stu-id="0ff97-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="0ff97-203">В примерах ниже показано, как просмотреть записи с помощью PowerShell и Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0ff97-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0ff97-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff97-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0ff97-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0ff97-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0ff97-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="0ff97-207">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="0ff97-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="0ff97-208">Можно ли разместить зоны обратного просмотра DNS для блоков IP-адресов, назначенных поставщиком услуг Интернета, в DNS Azure?</span><span class="sxs-lookup"><span data-stu-id="0ff97-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="0ff97-209">Да.</span><span class="sxs-lookup"><span data-stu-id="0ff97-209">Yes.</span></span> <span data-ttu-id="0ff97-210">Размещение зон обратного просмотра DNS для пользовательских диапазонов IP-адресов в Azure DNS полностью поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0ff97-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="0ff97-211">Создайте зону обратного просмотра в Azure DNS, как описано в этой статье, а затем [делегируйте ее](dns-domain-delegation.md) с помощью поставщика услуг Интернета.</span><span class="sxs-lookup"><span data-stu-id="0ff97-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="0ff97-212">Вы можете управлять записями типа PTR для каждого обратного просмотра точно так же, как и другими записями другого типа.</span><span class="sxs-lookup"><span data-stu-id="0ff97-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="0ff97-213">Сколько стоит размещение зоны обратного просмотра DNS?</span><span class="sxs-lookup"><span data-stu-id="0ff97-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="0ff97-214">Размещение зоны обратного просмотра DNS в Azure DNS для блока IP-адресов, назначенного поставщиком услуг Интернета, оплачивается по [стандартным тарифам Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="0ff97-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="0ff97-215">Можно ли разместить в Azure DNS зоны обратного просмотра DNS для адресов IPv4 и IPv6?</span><span class="sxs-lookup"><span data-stu-id="0ff97-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="0ff97-216">Да.</span><span class="sxs-lookup"><span data-stu-id="0ff97-216">Yes.</span></span> <span data-ttu-id="0ff97-217">В этой статье объясняется, как создать зоны обратного просмотра DNS для адресов IPv4 и IPv6 в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0ff97-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="0ff97-218">Можно ли импортировать существующую зону обратного просмотра DNS?</span><span class="sxs-lookup"><span data-stu-id="0ff97-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="0ff97-219">Да.</span><span class="sxs-lookup"><span data-stu-id="0ff97-219">Yes.</span></span> <span data-ttu-id="0ff97-220">Вы можете импортировать существующие зоны DNS в Azure DNS при помощи интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff97-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="0ff97-221">Он работает как с зонами прямого просмотра, так и с зонами обратного просмотра.</span><span class="sxs-lookup"><span data-stu-id="0ff97-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="0ff97-222">Дополнительные сведения см. в разделе [Импорт и экспорт файла зоны DNS с помощью Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="0ff97-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ff97-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ff97-223">Next steps</span></span>

<span data-ttu-id="0ff97-224">Дополнительные сведения см. [в статье Википедии об обратном просмотре DNS](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="0ff97-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="0ff97-225">Узнайте, как [управлять записями обратной зоны DNS для служб Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="0ff97-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
