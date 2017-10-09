---
title: "aaaHosting DNS зоны обратного просмотра в Azure DNS | Документы Microsoft"
description: "Узнайте, как hello toohost toouse Azure DNS DNS зоны обратного просмотра для диапазонов IP-"
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="ffeeb-103">Размещение зон обратного просмотра DNS в Azure DNS</span><span class="sxs-lookup"><span data-stu-id="ffeeb-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="ffeeb-104">В этой статье объясняется, как toohost hello DNS зоны обратного просмотра для назначенных диапазонов IP-в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="ffeeb-105">Hello диапазоны IP-адресов, представленный зоны обратного просмотра hello должны быть назначены организации tooyour обычно поставщиком услуг Интернета.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="ffeeb-106">tooconfigure обратного просмотра DNS для принадлежащие Azure IP-адреса, назначенного tooyour службы Azure см. в разделе [Настройка hello обратного просмотра для IP-адреса hello выделяются tooyour службы Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="ffeeb-107">Перед прочтением этой статьи ознакомьтесь со статьей [Основные сведения об обратной зоне DNS и ее поддержке в Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="ffeeb-108">В этой статье описывается toocreate действия hello вашей первой зоны обратного просмотра DNS и запись с помощью hello портал Azure, Azure PowerShell, CLI Azure 1.0 или Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="ffeeb-109">Создание зоны обратного просмотра DNS</span><span class="sxs-lookup"><span data-stu-id="ffeeb-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="ffeeb-110">Войдите в toohello [портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ffeeb-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="ffeeb-111">Hello концентратора меню и нажмите кнопку **New** > **сети** > и нажмите кнопку **зоны DNS** tooopen hello **создать DNS-зоны**колонку.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![Зона DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="ffeeb-113">На hello **создать DNS-зоны** колонке имя вашей зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="ffeeb-114">Имя зоны hello Hello сконструированных по-разному для IPv4 и IPv6 префиксов.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="ffeeb-115">Используйте либо hello инструкции для [IPV4](#ipv4) или [IPv6](#ipv6) tooname зоны.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="ffeeb-116">По завершении нажмите кнопку **создать** toocreate hello зоны.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="ffeeb-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="ffeeb-117">IPv4</span></span>

<span data-ttu-id="ffeeb-118">Имя зоны обратного просмотра IPv4 Hello основан на диапазон IP-адресов hello, которое он представляет.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="ffeeb-119">Он должен находиться в hello следующий формат: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="ffeeb-120">Примеры см. в [обзоре записей в обратной зоне DNS и поддержки в Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="ffeeb-121">При создании classless зоны обратного просмотра DNS в Azure DNS, необходимо использовать дефис (`-`) вместо косой черты («/») в имени зоны hello.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="ffeeb-122">Например, для 192.0.2.128/26 диапазон hello IP, необходимо использовать `128-26.2.0.192.in-addr.arpa` имени зоны hello вместо `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="ffeeb-123">Это происходит потому, что хотя оба поддерживаются стандартами DNS hello, зоны DNS, имена, содержащие hello косой черты (`/`) символ, не поддерживаются в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="ffeeb-124">Hello следующем примере показано, как toocreate «Класс C» обратная зона DNS с именем `2.0.192.in-addr.arpa` в Azure DNS через портал Azure hello:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![Создание зоны DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="ffeeb-126">Hello «Расположение группы ресурсов» определяет hello расположение группы ресурсов hello и не оказывает влияния на hello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="ffeeb-127">расположение зоны DNS Hello всегда «global» и не отображается.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="ffeeb-128">Hello следующих примерах показано, как toocomplete это задач с помощью Azure PowerShell и hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="ffeeb-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffeeb-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="ffeeb-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="ffeeb-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="ffeeb-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="ffeeb-132">IPv6</span></span>

<span data-ttu-id="ffeeb-133">Hello имя зоны обратного просмотра IPv6 должно быть в hello следующие формы: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="ffeeb-134">Примеры см. в [обзоре записей в обратной зоне DNS и поддержки в Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="ffeeb-135">Hello следующем примере показано, как toocreate зоне уточняющего запроса DNS обратного просмотра IPv6 именоваться `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` в Azure DNS через портал Azure hello:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![Создание зоны DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="ffeeb-137">Hello «Расположение группы ресурсов» определяет hello расположение группы ресурсов hello и не оказывает влияния на hello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="ffeeb-138">расположение зоны DNS Hello всегда «global» и не отображается.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="ffeeb-139">Hello следующих примерах показано, как toocomplete это задач с помощью Azure PowerShell и hello Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="ffeeb-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffeeb-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="ffeeb-141">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="ffeeb-142">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="ffeeb-143">Делегирование зоны обратного просмотра DNS</span><span class="sxs-lookup"><span data-stu-id="ffeeb-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="ffeeb-144">После создания вашего обратного просмотра зоны DNS, необходимо убедиться, что этой зоны hello делегирования в родительской зоне hello.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="ffeeb-145">Делегирование DNS позволяет hello DNS-имя разрешения процесса toofind hello серверами размещения вашего обратного просмотра зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="ffeeb-146">Это позволяет этих имя серверов tooanswer обратных запросов DNS для hello IP-адреса в диапазоне адресов.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="ffeeb-147">Для зоны прямого просмотра делегирование зоны DNS hello процесс описан в [делегировать tooAzure вашего домена DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="ffeeb-148">Делегирование для зоны обратного просмотра работает hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="ffeeb-149">Hello отличается только необходимость серверы имен hello tooconfigure с hello поставщика услуг Интернета, предоставившего вашей диапазон IP-адресов, вместо регистратора доменных имен.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="ffeeb-150">Создание записи DNS типа PTR</span><span class="sxs-lookup"><span data-stu-id="ffeeb-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="ffeeb-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="ffeeb-151">IPv4</span></span>

<span data-ttu-id="ffeeb-152">Hello в примере описывается процесс создания записи PTR в зону обратного просмотра DNS в Azure DNS hello.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="ffeeb-153">Для других типов записей и toomodify существующих записей в разделе [Управление DNS-записи и наборы записей с помощью hello портал Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="ffeeb-154">Вверху hello hello **зоны DNS** колонке выберите **+ запись набора** tooopen hello **добавить набор записей** колонку.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![Зона DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="ffeeb-156">На hello **добавить набор записей** колонку.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="ffeeb-157">Выберите **PTR** из записи hello»**тип**» меню.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="ffeeb-158">Hello имя набора записей hello для PTR-запись должна toobe hello остальной части hello IPv4-адрес в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="ffeeb-159">В этом примере hello первые три октета уже заполнены как часть имени зоны hello (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="ffeeb-160">Таким образом только последний октет hello содержится в поле имени hello.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="ffeeb-161">Например, для ресурса с IP-адресом 192.0.2.15 можно назвать набор записей **15**.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="ffeeb-162">В hello»**доменное имя**» введите hello полное доменное имя (FQDN) использует hello IP-адрес ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="ffeeb-163">Выберите **ОК** hello нижней части колонки toocreate hello hello-запись DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![Добавление набора записей](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="ffeeb-165">Hello ниже приведены примеры, демонстрирующие toocomplete этой задачи с помощью PowerShell и hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="ffeeb-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffeeb-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="ffeeb-167">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="ffeeb-168">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="ffeeb-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="ffeeb-169">IPv6</span></span>

<span data-ttu-id="ffeeb-170">Следующий пример Hello помогает выполнить процесс создания новой записи «PTR» hello.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="ffeeb-171">Для других типов записей и toomodify существующих записей в разделе [Управление DNS-записи и наборы записей с помощью hello портал Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="ffeeb-172">Вверху hello hello **колонке зоны DNS**выберите **+ запись набора** tooopen hello **добавить набор записей** колонку.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="ffeeb-174">На hello **добавить набор записей** колонку.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="ffeeb-175">Выберите **PTR** из записи hello»**тип**» меню.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="ffeeb-176">Hello имя набора записей hello для PTR-запись должна toobe hello остальной части hello IPv6-адрес в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="ffeeb-177">Сжатие за счет нулей не должно использоваться.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-177">It must not include any zero compression.</span></span> <span data-ttu-id="ffeeb-178">В этом примере hello первых 64 бит hello IPv6 уже заполнены как часть имени зоны hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="ffeeb-179">Таким образом в поле имя hello предоставляются только hello последние 64 бита.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="ffeeb-180">Hello последние 64 бита hello IP-адресов вводятся в обратном порядке, с помощью точки в качестве разделителя hello между каждое шестнадцатеричное число.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="ffeeb-181">Например, для ресурса с IP-адресом 2001:0db8:abdc:0000:f524:10bc:1af9:405e набор записей можно назвать **e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="ffeeb-182">В hello»**доменное имя**» введите hello полное доменное имя (FQDN) использует hello IP-адрес ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="ffeeb-183">Выберите **ОК** hello нижней части колонки toocreate hello hello-запись DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![Колонка добавления набора записей](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="ffeeb-185">Hello ниже приведены примеры, демонстрирующие toocomplete этой задачи с помощью PowerShell и hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="ffeeb-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffeeb-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="ffeeb-187">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="ffeeb-188">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="ffeeb-189">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="ffeeb-189">View Records</span></span>

<span data-ttu-id="ffeeb-190">tooview hello записи, которые вы создали перейдите tooyour зоны DNS в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="ffeeb-191">В hello понизить часть hello **зоны DNS** колонку, вы увидите hello записей для DNS-зоны hello.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="ffeeb-192">Вы увидите hello по умолчанию записи NS и SOA, которые создаются в каждой зоне, а также любые новые записи, который был создан.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="ffeeb-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="ffeeb-193">IPv4</span></span>

<span data-ttu-id="ffeeb-194">Колонка зоны DNS с записями IPv4 типа PTR:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="ffeeb-196">Hello следующие примеры Показать порядок tooview hello PTR записей с помощью PowerShell или Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="ffeeb-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffeeb-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="ffeeb-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="ffeeb-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="ffeeb-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="ffeeb-200">IPv6</span></span>

<span data-ttu-id="ffeeb-201">Колонка зоны DNS с записями IPv6 типа PTR:</span><span class="sxs-lookup"><span data-stu-id="ffeeb-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![Колонка зоны DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="ffeeb-203">Hello ниже приведены примеры на порядок tooview hello записей с помощью PowerShell и hello AzureCLI.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="ffeeb-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ffeeb-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="ffeeb-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="ffeeb-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffeeb-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="ffeeb-207">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="ffeeb-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="ffeeb-208">Можно ли разместить зоны обратного просмотра DNS для блоков IP-адресов, назначенных поставщиком услуг Интернета, в DNS Azure?</span><span class="sxs-lookup"><span data-stu-id="ffeeb-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="ffeeb-209">Да.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-209">Yes.</span></span> <span data-ttu-id="ffeeb-210">Полностью поддерживается размещение hello зоны обратного просмотра (ARPA) для диапазонов IP-в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="ffeeb-211">Создание зоны обратного просмотра hello в Azure DNS, как описано в этой статье, а затем работать с поставщиком услуг Интернета, слишком[зоны hello делегат](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="ffeeb-212">Затем можно будет управлять hello PTR-записей для каждого обратного просмотра в hello так же, как другие типов записей.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="ffeeb-213">Сколько стоит размещение зоны обратного просмотра DNS?</span><span class="sxs-lookup"><span data-stu-id="ffeeb-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="ffeeb-214">Размещение hello зоны обратного просмотра DNS для вашей услуг Интернета IP-блоков в Azure DNS оплачивается по [стандартные тарифы Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="ffeeb-215">Можно ли разместить в Azure DNS зоны обратного просмотра DNS для адресов IPv4 и IPv6?</span><span class="sxs-lookup"><span data-stu-id="ffeeb-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="ffeeb-216">Да.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-216">Yes.</span></span> <span data-ttu-id="ffeeb-217">В этой статье объясняется, как toocreate IPv4 и IPv6 DNS зоны обратного просмотра в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="ffeeb-218">Можно ли импортировать существующую зону обратного просмотра DNS?</span><span class="sxs-lookup"><span data-stu-id="ffeeb-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="ffeeb-219">Да.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-219">Yes.</span></span> <span data-ttu-id="ffeeb-220">Можно использовать существующие зон DNS hello Azure CLI tooimport в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="ffeeb-221">Он работает как с зонами прямого просмотра, так и с зонами обратного просмотра.</span><span class="sxs-lookup"><span data-stu-id="ffeeb-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="ffeeb-222">Дополнительные сведения см. в разделе [импорта и экспорта в файл зоны DNS с помощью hello Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffeeb-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffeeb-223">Next steps</span></span>

<span data-ttu-id="ffeeb-224">Дополнительные сведения см. [в статье Википедии об обратном просмотре DNS](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="ffeeb-225">Узнайте, каким образом слишком[управление обратного DNS-записи для служб Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="ffeeb-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
