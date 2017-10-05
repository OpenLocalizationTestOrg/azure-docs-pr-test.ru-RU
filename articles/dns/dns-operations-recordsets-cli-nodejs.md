---
title: "Управление записями DNS в Azure DNS с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Управляйте наборами записей и записями DNS в службе Azure DNS при размещении вашего домена в Azure DNS. Все команды CLI 1.0 для операций с наборами записей и записями."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 307b327e4c04a0461e39930114eb193791cbda9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="1dd07-104">Управление записями DNS в Azure DNS с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1dd07-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1dd07-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1dd07-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="1dd07-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1dd07-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="1dd07-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1dd07-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="1dd07-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1dd07-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="1dd07-109">В этой статье описано, как управлять записями DNS для зоны DNS с помощью кроссплатформенного интерфейса командной строки (CLI) Azure, доступного для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="1dd07-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="1dd07-110">Записями DNS также можно управлять с помощью [Azure PowerShell](dns-operations-recordsets.md) или [портала Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1dd07-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="1dd07-111">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="1dd07-111">CLI versions to complete the task</span></span>

<span data-ttu-id="1dd07-112">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="1dd07-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="1dd07-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) — это интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1dd07-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="1dd07-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) — это интерфейс командной строки нового поколения для модели развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1dd07-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="1dd07-115">Для работы с этой статьей необходимо [установить Azure CLI 1.0, войти в учетную запись и создать зону DNS](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1dd07-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="1dd07-116">Введение</span><span class="sxs-lookup"><span data-stu-id="1dd07-116">Introduction</span></span>

<span data-ttu-id="1dd07-117">Чтобы создавать записи DNS в Azure DNS, нужно понимать, как Azure DNS организует записи DNS в соответствующие наборы записей.</span><span class="sxs-lookup"><span data-stu-id="1dd07-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="1dd07-118">Дополнительные сведения о записях DNS в Azure DNS см. в статье [Зоны и записи DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="1dd07-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="1dd07-119">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="1dd07-119">Create a DNS record</span></span>

<span data-ttu-id="1dd07-120">Чтобы создать запись DNS, используйте команду `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="1dd07-121">Чтобы получить справку, см. `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="1dd07-122">Создавая запись, вам нужно определить для нее имя группы ресурсов, имя зоны, имя набора записей, тип записей и сведения о создаваемой записи.</span><span class="sxs-lookup"><span data-stu-id="1dd07-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="1dd07-123">Имя набора записей должно быть *относительным*, т. е. оно не должно содержать имя зоны.</span><span class="sxs-lookup"><span data-stu-id="1dd07-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="1dd07-124">Если набора записей не существует, эта команда автоматически создаст его.</span><span class="sxs-lookup"><span data-stu-id="1dd07-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="1dd07-125">Если набор записей существует, эта команда добавляет в него указанную запись.</span><span class="sxs-lookup"><span data-stu-id="1dd07-125">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="1dd07-126">При создании набора записей используется срок жизни (TTL) по умолчанию — 3600.</span><span class="sxs-lookup"><span data-stu-id="1dd07-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="1dd07-127">Инструкции по использованию различных сроков жизни см. в разделе [Создание набора записей DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="1dd07-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="1dd07-128">В следующем примере будет создана запись A с именем *www* в зоне *contoso.com* в группе ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1dd07-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="1dd07-129">IP-адрес записи A — *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="1dd07-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="1dd07-130">Чтобы создать запись на вершине зоны (в нашем примере — contoso.com), используйте имя записи @, включая кавычки:</span><span class="sxs-lookup"><span data-stu-id="1dd07-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="1dd07-131">Создание набора записей DNS</span><span class="sxs-lookup"><span data-stu-id="1dd07-131">Create a DNS record set</span></span>

<span data-ttu-id="1dd07-132">В приведенных выше примерах запись DNS добавлялась к существующему набору записей, или набор записей создавался *неявно*.</span><span class="sxs-lookup"><span data-stu-id="1dd07-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="1dd07-133">Кроме того, можно *явно* создать набор записей, прежде чем добавлять в него записи.</span><span class="sxs-lookup"><span data-stu-id="1dd07-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="1dd07-134">В Azure DNS поддерживаются пустые наборы записей, которые могут использоваться как заполнители для резервирования имен DNS перед созданием записей DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="1dd07-135">Пустые наборы записей отображаются на панели управления Azure DNS, но не отображаются на серверах имен Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="1dd07-136">Наборы записей создаются с помощью команды `azure network dns record-set create`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-136">Record sets are created using the `azure network dns record-set create` command.</span></span> <span data-ttu-id="1dd07-137">Чтобы получить справку, см. `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="1dd07-138">При создании набора записей можно явно указать его свойства, например [срок жизни](dns-zones-records.md#time-to-live) и метаданные.</span><span class="sxs-lookup"><span data-stu-id="1dd07-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="1dd07-139">[Метаданные набора записей](dns-zones-records.md#tags-and-metadata) используются для связывания данных приложения с каждым набором записей в виде пар "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="1dd07-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="1dd07-140">В следующем примере показано, как создать пустой набор записей со сроком жизни 60 секунд. Для этого используется параметр `--ttl` (краткая форма `-l`).</span><span class="sxs-lookup"><span data-stu-id="1dd07-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="1dd07-141">В следующем примере показано, как создать набор с двумя записями метаданных: dept=finance и environment=production. Для этого используется параметр `--metadata` (краткая форма `-m`).</span><span class="sxs-lookup"><span data-stu-id="1dd07-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="1dd07-142">После создания пустого набора записей в него можно добавить записи с помощью команды `azure network dns record-set add-record`, как описано в разделе [Создание записи DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="1dd07-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="1dd07-143">Создание записей других типов</span><span class="sxs-lookup"><span data-stu-id="1dd07-143">Create records of other types</span></span>

<span data-ttu-id="1dd07-144">Вы уже узнали, как создавать записи типа А. В следующем примере показано, как создавать записи других типов, поддерживаемые в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="1dd07-145">Параметры, используемые для указания данных записи, различаются в зависимости от типа записи.</span><span class="sxs-lookup"><span data-stu-id="1dd07-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="1dd07-146">Например, для записи типа A необходимо указать адрес IPv4, используя параметр `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="1dd07-147">Параметры для каждого типа записи можно перечислить с помощью команды `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="1dd07-148">В каждом случае мы покажем, как создать одну запись.</span><span class="sxs-lookup"><span data-stu-id="1dd07-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="1dd07-149">Запись добавляется в существующий набор или набор, созданный неявно.</span><span class="sxs-lookup"><span data-stu-id="1dd07-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="1dd07-150">Дополнительные сведения о создании наборов записей и явной настройке параметра набора см. в разделе [Создание набора записей DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="1dd07-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="1dd07-151">Мы не включаем пример создания набора записей типа SOA, так как такие записи создаются и удаляются только вместе с соответствующей зоной DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="1dd07-152">Тем не менее [записи типа SOA можно изменять, как показано в примере ниже](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="1dd07-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="1dd07-153">Создание записи типа AAAA</span><span class="sxs-lookup"><span data-stu-id="1dd07-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="1dd07-154">Создание записи CNAME</span><span class="sxs-lookup"><span data-stu-id="1dd07-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="1dd07-155">Стандарты DNS не допускают использование записей типа CNAME на вершине зоны (`-Name "@"`), а также использование наборов записей, содержащих более одной записи.</span><span class="sxs-lookup"><span data-stu-id="1dd07-155">The DNS standards do not permit CNAME records at the apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="1dd07-156">Дополнительные сведения см. в разделе [Записи типа CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="1dd07-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="1dd07-157">Создание записи типа MX</span><span class="sxs-lookup"><span data-stu-id="1dd07-157">Create an MX record</span></span>

<span data-ttu-id="1dd07-158">Чтобы создать запись MX на вершине зоны (в данном случае "contoso.com"), в этом примере мы используем имя набора записей "@".</span><span class="sxs-lookup"><span data-stu-id="1dd07-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="1dd07-159">Создание записи типа NS</span><span class="sxs-lookup"><span data-stu-id="1dd07-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="1dd07-160">Создание записи типа PTR</span><span class="sxs-lookup"><span data-stu-id="1dd07-160">Create a PTR record</span></span>

<span data-ttu-id="1dd07-161">В этом случае my-arpa-zone.com представляет зону ARPA вашего диапазона IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1dd07-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="1dd07-162">Каждая запись PTR в этой зоне соответствует IP-адресу в этом диапазоне.</span><span class="sxs-lookup"><span data-stu-id="1dd07-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="1dd07-163">Имя записи 10 — это последний октет IP-адреса в этом диапазоне IP-адресов, представленном данной записью.</span><span class="sxs-lookup"><span data-stu-id="1dd07-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="1dd07-164">Создание записи типа SRV</span><span class="sxs-lookup"><span data-stu-id="1dd07-164">Create an SRV record</span></span>

<span data-ttu-id="1dd07-165">Создавая [набор записей SRV](dns-zones-records.md#srv-records), укажите в его имени *\_службу* и *\_протокол*.</span><span class="sxs-lookup"><span data-stu-id="1dd07-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="1dd07-166">Если набор записей SRV создается на вершине зоны, включать @ в имя набора записей не нужно.</span><span class="sxs-lookup"><span data-stu-id="1dd07-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="1dd07-167">Создание записи типа TXT</span><span class="sxs-lookup"><span data-stu-id="1dd07-167">Create a TXT record</span></span>

<span data-ttu-id="1dd07-168">В следующем примере показано, как создать запись типа ТХТ.</span><span class="sxs-lookup"><span data-stu-id="1dd07-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="1dd07-169">Дополнительные сведения о максимальной длине строки, поддерживаемой в записях типа TXT, см. в разделе [Записи типа TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="1dd07-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="1dd07-170">Получение набора записей</span><span class="sxs-lookup"><span data-stu-id="1dd07-170">Get a record set</span></span>

<span data-ttu-id="1dd07-171">Чтобы извлечь существующий набор записей, используйте команду `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-171">To retrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="1dd07-172">Чтобы получить справку, см. `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="1dd07-173">Как и при создании записи или набора записей, имя набора должно быть *относительным*, т. е. оно не должно содержать имя зоны.</span><span class="sxs-lookup"><span data-stu-id="1dd07-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="1dd07-174">Необходимо также указать тип записи, зону, содержащую набор записей, и группу ресурсов, содержащую зону.</span><span class="sxs-lookup"><span data-stu-id="1dd07-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="1dd07-175">В следующем примере показано получение записи *www* типа А из зоны *contoso.com* в группе ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1dd07-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="1dd07-176">Перечисление наборов записей</span><span class="sxs-lookup"><span data-stu-id="1dd07-176">List record sets</span></span>

<span data-ttu-id="1dd07-177">Команда `azure network dns record-set list` позволяет получить список всех записей в зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span></span> <span data-ttu-id="1dd07-178">Чтобы получить справку, см. `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="1dd07-179">В этом примере возвращаются все наборы записей в зоне *contoso.com* в группе ресурсов *MyResourceGroup* вне зависимости от имени и типа записи:</span><span class="sxs-lookup"><span data-stu-id="1dd07-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="1dd07-180">В этом примере возвращаются все наборы записей, соответствующие заданному типу записи (в данном случае это записи типа A).</span><span class="sxs-lookup"><span data-stu-id="1dd07-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="1dd07-181">Добавление записи в существующий набор записей</span><span class="sxs-lookup"><span data-stu-id="1dd07-181">Add a record to an existing record set</span></span>

<span data-ttu-id="1dd07-182">Команду `azure network dns record-set add-record` можно использовать как для создания записи в новом наборе записей, так и для добавления записи в существующий набор.</span><span class="sxs-lookup"><span data-stu-id="1dd07-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="1dd07-183">Дополнительные сведения см. в разделах [Создание записи DNS](#create-a-dns-record) и [Создание записей других типов](#create-records-of-other-types) выше.</span><span class="sxs-lookup"><span data-stu-id="1dd07-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="1dd07-184">Удаление записи из существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="1dd07-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="1dd07-185">Для удаления записи DNS из существующего набора используйте команду `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="1dd07-186">Чтобы получить справку, см. `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="1dd07-187">Эта команда удаляет запись DNS из набора записей.</span><span class="sxs-lookup"><span data-stu-id="1dd07-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="1dd07-188">Удаление последней записи в наборе **не** приводит к удалению самого набора.</span><span class="sxs-lookup"><span data-stu-id="1dd07-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="1dd07-189">В таком случае набор записей будет пустым.</span><span class="sxs-lookup"><span data-stu-id="1dd07-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="1dd07-190">Чтобы удалить набор, см. инструкции в разделе [Удаление набора записей](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="1dd07-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="1dd07-191">Необходимо указать удаляемую запись и зону, из которой ее следует удалить, используя те же параметры, что и при создании записи с помощью команды `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="1dd07-192">Эти параметры описаны в предыдущих разделах [Создание записи DNS](#create-a-dns-record) и [Создание записей других типов](#create-records-of-other-types).</span><span class="sxs-lookup"><span data-stu-id="1dd07-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="1dd07-193">Эта команда запрашивает подтверждение.</span><span class="sxs-lookup"><span data-stu-id="1dd07-193">This command prompts for confirmation.</span></span> <span data-ttu-id="1dd07-194">Этот запрос можно скрыть с помощью параметра `--quiet` (краткая форма `-q`).</span><span class="sxs-lookup"><span data-stu-id="1dd07-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="1dd07-195">В следующем примере показано удаление записи типа A со значением "1.2.3.4" из набора записей с именем *www* в зоне *contoso.com* в группе ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1dd07-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="1dd07-196">Запрос подтверждения скрыт.</span><span class="sxs-lookup"><span data-stu-id="1dd07-196">The confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="1dd07-197">Обновление существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="1dd07-197">Modify an existing record set</span></span>

<span data-ttu-id="1dd07-198">В каждом наборе записей указан [срок жизни](dns-zones-records.md#time-to-live), [метаданные](dns-zones-records.md#tags-and-metadata) и записи DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="1dd07-199">В следующих разделах описано, как изменять эти свойства.</span><span class="sxs-lookup"><span data-stu-id="1dd07-199">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="1dd07-200">Изменение записи типа A, AAAA, MX, NS, PTR, SRV или TXT</span><span class="sxs-lookup"><span data-stu-id="1dd07-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="1dd07-201">Чтобы изменить существующую запись типа A, AAAA, MX, NS, PTR, SRV или TXT, сначала следует добавить новую запись, а затем удалить существующую.</span><span class="sxs-lookup"><span data-stu-id="1dd07-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="1dd07-202">Подробные инструкции об удалении и добавлении записей см. в предыдущих разделах этой статьи.</span><span class="sxs-lookup"><span data-stu-id="1dd07-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="1dd07-203">В следующем примере показано, как в записи типа А изменить IP-адрес 1.2.3.4 на IP-адрес 5.6.7.8.</span><span class="sxs-lookup"><span data-stu-id="1dd07-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="1dd07-204">Изменение записи CNAME</span><span class="sxs-lookup"><span data-stu-id="1dd07-204">To modify a CNAME record</span></span>

<span data-ttu-id="1dd07-205">Чтобы изменить запись CNAME, используйте команду `azure network dns record-set add-record` для добавления нового значения записи.</span><span class="sxs-lookup"><span data-stu-id="1dd07-205">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span></span> <span data-ttu-id="1dd07-206">В отличие от других типов записей, набор записей CNAME может содержать только одну запись.</span><span class="sxs-lookup"><span data-stu-id="1dd07-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="1dd07-207">Таким образом, при добавлении новой записи существующая запись *заменяется*, и ее не нужно удалять отдельно.</span><span class="sxs-lookup"><span data-stu-id="1dd07-207">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span></span>  <span data-ttu-id="1dd07-208">Отобразится запрос на подтверждение этой замены.</span><span class="sxs-lookup"><span data-stu-id="1dd07-208">You will be prompted to accept this replacement.</span></span>

<span data-ttu-id="1dd07-209">В примере ниже показано изменение набора записей CNAME с именем *www* в зоне *contoso.com* в группе ресурсов *MyResourceGroup* таким образом, чтобы он указывал на www.fabrikam.net вместо существующего значения.</span><span class="sxs-lookup"><span data-stu-id="1dd07-209">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="1dd07-210">Изменение записи типа SOA</span><span class="sxs-lookup"><span data-stu-id="1dd07-210">To modify an SOA record</span></span>

<span data-ttu-id="1dd07-211">Чтобы изменить запись типа SOA для определенной зоны DNS, используйте команду `azure network dns record-set set-soa-record`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-211">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="1dd07-212">Чтобы получить справку, см. `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="1dd07-213">В примере ниже показано, как задать свойство email записи типа SOA для зоны *contoso.com* в группе ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1dd07-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="1dd07-214">Изменение записи NS на вершине зоны</span><span class="sxs-lookup"><span data-stu-id="1dd07-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="1dd07-215">Набор записей типа NS на вершине зоны автоматически создается вместе с каждой зоной DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="1dd07-216">Он содержит имена DNS-серверов Azure, назначенные зоне.</span><span class="sxs-lookup"><span data-stu-id="1dd07-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="1dd07-217">Вы можете добавить дополнительные имена серверов в этот набор записей NS, обеспечив поддержку совместного размещения доменов с использованием более чем одного поставщика DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="1dd07-218">Вы также можете изменить срок жизни и метаданные для этого набора записей.</span><span class="sxs-lookup"><span data-stu-id="1dd07-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="1dd07-219">При этом вы не можете удалить или изменить предварительно заполненные серверы доменных имен Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="1dd07-220">Обратите внимание, что это относится только к набору записей NS на вершине зоны.</span><span class="sxs-lookup"><span data-stu-id="1dd07-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="1dd07-221">Другие наборы записей NS в зоне (используемые для делегирования дочерних зон) можно изменять без ограничений.</span><span class="sxs-lookup"><span data-stu-id="1dd07-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="1dd07-222">В следующем примере показано, как добавить дополнительный сервер в набор записей NS на вершине зоны:</span><span class="sxs-lookup"><span data-stu-id="1dd07-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="1dd07-223">Изменение срока жизни существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="1dd07-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="1dd07-224">Для изменения срока жизни существующего набора записей используйте команду `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-224">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="1dd07-225">Чтобы получить справку, см. `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="1dd07-226">В примере ниже показано, как изменить срок жизни набора записей. В этом случае устанавливается срок в 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="1dd07-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="1dd07-227">Изменение метаданных существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="1dd07-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="1dd07-228">[Метаданные набора записей](dns-zones-records.md#tags-and-metadata) используются для связывания данных приложения с каждым набором записей в виде пар "ключ — значение".</span><span class="sxs-lookup"><span data-stu-id="1dd07-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="1dd07-229">Для изменения метаданных существующего набора записей используйте команду `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-229">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="1dd07-230">Чтобы получить справку, см. `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="1dd07-231">В следующем примере показано, как изменить набор данных с двумя записями метаданных: dept=finance и environment=production. Для этого используется параметр `--metadata` (краткая форма `-m`).</span><span class="sxs-lookup"><span data-stu-id="1dd07-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="1dd07-232">Обратите внимание, что все существующие метаданные *заменяются* заданными значениями.</span><span class="sxs-lookup"><span data-stu-id="1dd07-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="1dd07-233">Удаление набора записей</span><span class="sxs-lookup"><span data-stu-id="1dd07-233">Delete a record set</span></span>

<span data-ttu-id="1dd07-234">Наборы записей можно удалить с помощью команды `azure network dns record-set delete`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-234">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="1dd07-235">Чтобы получить справку, см. `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="1dd07-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="1dd07-236">При удалении набора записей также удаляются все содержащиеся в нем записи.</span><span class="sxs-lookup"><span data-stu-id="1dd07-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="1dd07-237">Удалить наборы записей типа SOA и NS на вершине зоны (`-Name "@"`) нельзя.</span><span class="sxs-lookup"><span data-stu-id="1dd07-237">You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="1dd07-238">Эти записи создаются и удаляются автоматически вместе с зоной.</span><span class="sxs-lookup"><span data-stu-id="1dd07-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="1dd07-239">В следующем примере показано удаление набора записей с именем *www* типа А из зоны *contoso.com* в группе ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1dd07-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="1dd07-240">Отобразится запрос на подтверждение операции удаления.</span><span class="sxs-lookup"><span data-stu-id="1dd07-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="1dd07-241">Чтобы скрыть этот запрос, используйте параметр `--quiet` (краткая форма `-q`).</span><span class="sxs-lookup"><span data-stu-id="1dd07-241">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dd07-242">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1dd07-242">Next steps</span></span>

<span data-ttu-id="1dd07-243">См. дополнительные сведения о [зонах и записях в Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="1dd07-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="1dd07-244">Узнайте, как [защитить зоны и записи](dns-protect-zones-recordsets.md) при использовании Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1dd07-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
