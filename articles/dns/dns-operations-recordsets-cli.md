---
title: "Здравствуйте, aaaManage DNS-записей в Azure DNS с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Управляйте наборами записей и записями DNS в службе Azure DNS при размещении вашего домена в Azure DNS. Все команды CLI 2.0 для операций с наборами записей и записями."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="0a404-104">Управление DNS-записи и наборов записей в Azure DNS, с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="0a404-104">Manage DNS records and recordsets in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a404-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="0a404-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="0a404-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0a404-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="0a404-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0a404-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="0a404-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a404-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="0a404-109">В этой статье показано, как toomanage записи DNS для зоны DNS с помощью hello кросс платформенных Azure командной строки (CLI) 2.0, которое доступно для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="0a404-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="0a404-110">Также можно управлять с помощью DNS-записей [Azure PowerShell](dns-operations-recordsets.md) или hello [портал Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0a404-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0a404-111">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="0a404-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="0a404-112">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="0a404-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="0a404-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.</span><span class="sxs-lookup"><span data-stu-id="0a404-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="0a404-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурса управления.</span><span class="sxs-lookup"><span data-stu-id="0a404-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="0a404-115">Hello в этой статье примерах уже имеется [hello Azure CLI 2.0, вход и создали зоны DNS](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0a404-115">hello examples in this article assume you have already [installed hello Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="0a404-116">Введение</span><span class="sxs-lookup"><span data-stu-id="0a404-116">Introduction</span></span>

<span data-ttu-id="0a404-117">Прежде чем создавать DNS-записи в Azure DNS, необходимо сначала toounderstand как Azure DNS организует DNS-записей в наборы записей DNS.</span><span class="sxs-lookup"><span data-stu-id="0a404-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="0a404-118">Дополнительные сведения о записях DNS в Azure DNS см. в статье [Зоны и записи DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0a404-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="0a404-119">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="0a404-119">Create a DNS record</span></span>

<span data-ttu-id="0a404-120">toocreate запись DNS использовать hello `az network dns record-set <record-type> set-record` команду (где `<record-type>` является hello типа записи, т. е.</span><span class="sxs-lookup"><span data-stu-id="0a404-120">toocreate a DNS record, use hello `az network dns record-set <record-type> set-record` command (where `<record-type>` is hello type of record, i.e</span></span> <span data-ttu-id="0a404-121">a, srv, txt и т. д.). Чтобы получить справку, см. `az network dns record-set --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="0a404-122">При создании записи, необходимо, чтобы имя группы ресурсов hello toospecify имя зоны, имя, тип записи hello и hello подробные сведения о записи hello набор записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="0a404-123">Hello имя набора записей должно быть *относительный* имя, то есть его необходимо исключить hello имя зоны.</span><span class="sxs-lookup"><span data-stu-id="0a404-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="0a404-124">Набор записей hello еще не существует, эта команда создает для вас.</span><span class="sxs-lookup"><span data-stu-id="0a404-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="0a404-125">Если существует запись hello уже настроено, эта команда добавляет запись hello, укажите toohello существующего набора записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-125">If hello record set already exists, this command adds hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="0a404-126">При создании набора записей используется срок жизни (TTL) по умолчанию — 3600.</span><span class="sxs-lookup"><span data-stu-id="0a404-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="0a404-127">Инструкции по toouse различных TTLs статье [создать набор записей DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="0a404-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="0a404-128">Hello следующий пример создает запись называется *www* в зоне hello *contoso.com* в группе ресурсов hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0a404-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="0a404-129">Здравствуйте, IP-адрес hello запись — *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="0a404-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="0a404-130">задать toocreate запись в вершине зоны hello hello (в этом случае «contoso.com»), используйте имя записи hello, «@», кавычками hello:</span><span class="sxs-lookup"><span data-stu-id="0a404-130">toocreate a record set in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="0a404-131">Создание набора записей DNS</span><span class="sxs-lookup"><span data-stu-id="0a404-131">Create a DNS record set</span></span>

<span data-ttu-id="0a404-132">В hello выше примеры hello DNS-запись была либо добавлены tooan существующего набора записей или был создан набор записей hello *неявно*.</span><span class="sxs-lookup"><span data-stu-id="0a404-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="0a404-133">Также можно создать набор записей hello *явно* до добавления записывает tooit.</span><span class="sxs-lookup"><span data-stu-id="0a404-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="0a404-134">Azure DNS поддерживает «empty» наборы записей, которые может выступать в качестве tooreserve заполнитель DNS-имя перед созданием записи DNS.</span><span class="sxs-lookup"><span data-stu-id="0a404-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="0a404-135">Пустые наборы записей, отображаются в hello Azure DNS панели управления, но не отображаются в hello Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="0a404-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="0a404-136">Наборы записей создаются с помощью hello `az network dns record-set <record-type> create` команды.</span><span class="sxs-lookup"><span data-stu-id="0a404-136">Record sets are created using hello `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="0a404-137">Чтобы получить справку, см. `az network dns record-set <record-type> create --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="0a404-138">Создание записи hello задано явным образом позволяет toospecify свойства набора записей, такие как hello [срока жизни (TTL)](dns-zones-records.md#time-to-live) и метаданные.</span><span class="sxs-lookup"><span data-stu-id="0a404-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="0a404-139">[Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение".</span><span class="sxs-lookup"><span data-stu-id="0a404-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="0a404-140">Hello следующем примере создается пустой набор записей типа «A» со сроком ЖИЗНИ 60 секунд, с помощью hello `--ttl` параметра (Краткая форма `-l`):</span><span class="sxs-lookup"><span data-stu-id="0a404-140">hello following example creates an empty record set of type 'A' with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="0a404-141">Hello следующий пример создает записей с две записи метаданных» dept = finance» и «среды = рабочей», с помощью hello `--metadata` параметр:</span><span class="sxs-lookup"><span data-stu-id="0a404-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="0a404-142">После создания пустого набора записей в него можно добавить записи с помощью команды `azure network dns record-set <record-type> set-record`, как описано в разделе [Создание записи DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="0a404-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="0a404-143">Создание записей других типов</span><span class="sxs-lookup"><span data-stu-id="0a404-143">Create records of other types</span></span>

<span data-ttu-id="0a404-144">Рассматривать подробно порядок записей toocreate «A» hello, в следующих примерах показано, как запись toocreate других типов записи поддерживается службой Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0a404-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="0a404-145">использовать параметры Hello toospecify hello записи данных зависит от типа hello hello записи.</span><span class="sxs-lookup"><span data-stu-id="0a404-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="0a404-146">Например, для записи типа «A», можно указать hello IPv4-адрес с параметром hello `--ipv4-address <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="0a404-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="0a404-147">Здравствуйте параметров для каждого типа записи могут быть перечислены с помощью `az network dns record-set <record-type> set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-147">hello parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="0a404-148">В каждом случае показано, как toocreate отдельную запись.</span><span class="sxs-lookup"><span data-stu-id="0a404-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="0a404-149">Hello запись будет добавлена toohello существующего набора записей или неявно создан набор записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="0a404-150">Дополнительные сведения о создании наборов записей и явной настройке параметра набора см. в разделе [Создание набора записей DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="0a404-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="0a404-151">Мы не предоставляем toocreate примере SOA набор записей, так как создаются SOA и удалены вместе с каждой зоны DNS и не удается создать или удалить отдельно.</span><span class="sxs-lookup"><span data-stu-id="0a404-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="0a404-152">Тем не менее [SOA могут быть изменены, как показано в пример hello](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="0a404-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="0a404-153">Создание записи типа AAAA</span><span class="sxs-lookup"><span data-stu-id="0a404-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="0a404-154">Создание записи CNAME</span><span class="sxs-lookup"><span data-stu-id="0a404-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="0a404-155">Hello стандартах DNS не допускают записи CNAME на вершине hello зоны (`--Name "@"`), и не следует разрешать или запрещать наборы записей, содержащая более одной записи.</span><span class="sxs-lookup"><span data-stu-id="0a404-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="0a404-156">Дополнительные сведения см. в разделе [Записи типа CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="0a404-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="0a404-157">Создание записи типа MX</span><span class="sxs-lookup"><span data-stu-id="0a404-157">Create an MX record</span></span>

<span data-ttu-id="0a404-158">В этом примере мы используем имя набора записей hello «@» hello toocreate MX-записи на вершине зоны hello (в данном случае «contoso.com»).</span><span class="sxs-lookup"><span data-stu-id="0a404-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="0a404-159">Создание записи типа NS</span><span class="sxs-lookup"><span data-stu-id="0a404-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="0a404-160">Создание записи типа PTR</span><span class="sxs-lookup"><span data-stu-id="0a404-160">Create a PTR record</span></span>

<span data-ttu-id="0a404-161">В этом случае "my-arpa-zone.com" представляет hello зоны ARPA, представляющий ваш диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="0a404-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="0a404-162">Каждая запись PTR в этой зоне соответствует tooan IP-адрес в этот диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="0a404-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="0a404-163">Имя записи Hello "10" представляет hello последний октет hello IP-адрес в этот диапазон IP-адресов, представленного данной записью.</span><span class="sxs-lookup"><span data-stu-id="0a404-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="0a404-164">Создание записи типа SRV</span><span class="sxs-lookup"><span data-stu-id="0a404-164">Create an SRV record</span></span>

<span data-ttu-id="0a404-165">При создании [набор записей типа SRV](dns-zones-records.md#srv-records), укажите hello  *\_службы* и  *\_протокола* в hello имя набора записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="0a404-166">Нет нет необходимости tooinclude «@» в hello запись имя набора при создании записи SRV набора в вершине зоны hello.</span><span class="sxs-lookup"><span data-stu-id="0a404-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="0a404-167">Создание записи типа TXT</span><span class="sxs-lookup"><span data-stu-id="0a404-167">Create a TXT record</span></span>

<span data-ttu-id="0a404-168">Hello следующем примере показано, как записать toocreate TXT.</span><span class="sxs-lookup"><span data-stu-id="0a404-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="0a404-169">Дополнительные сведения о hello Максимальная длина строки поддерживается в записи TXT в разделе [записи TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="0a404-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="0a404-170">Получение набора записей</span><span class="sxs-lookup"><span data-stu-id="0a404-170">Get a record set</span></span>

<span data-ttu-id="0a404-171">использовать существующий набор записей, tooretrieve `az network dns record-set <record-type> show`.</span><span class="sxs-lookup"><span data-stu-id="0a404-171">tooretrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="0a404-172">Чтобы получить справку, см. `az network dns record-set <record-type> show --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="0a404-173">При создании записи или набора записей записи hello задать имя, присвоенное должен быть *относительный* имя, то есть его необходимо исключить hello имя зоны.</span><span class="sxs-lookup"><span data-stu-id="0a404-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="0a404-174">Требуется тип записи toospecify hello, hello зоны, содержащей записи hello задать и hello группы ресурсов, содержащую зону hello.</span><span class="sxs-lookup"><span data-stu-id="0a404-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="0a404-175">Hello следующий пример извлекает записи hello *www* типа a из зоны *contoso.com* в группе ресурсов *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0a404-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="0a404-176">Перечисление наборов записей</span><span class="sxs-lookup"><span data-stu-id="0a404-176">List record sets</span></span>

<span data-ttu-id="0a404-177">Список всех записей в зоне DNS можно с помощью hello `az network dns record-set list` команды.</span><span class="sxs-lookup"><span data-stu-id="0a404-177">You can list all records in a DNS zone by using hello `az network dns record-set list` command.</span></span> <span data-ttu-id="0a404-178">Чтобы получить справку, см. `az network dns record-set list --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="0a404-179">Этот пример возвращает задает все записи в зоне hello *contoso.com*, в группе ресурсов *MyResourceGroup*, независимо от того, имя или тип записи:</span><span class="sxs-lookup"><span data-stu-id="0a404-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="0a404-180">Этот пример возвращает все наборы записей, которые соответствуют hello данного типа записи (в данном случае записи 'A'):</span><span class="sxs-lookup"><span data-stu-id="0a404-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="0a404-181">Добавление записей tooan существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="0a404-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="0a404-182">Можно использовать `az network dns record-set <record-type> set-record` как toocreate записи в новой записи или tooadd существующую запись tooan записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-182">You can use `az network dns record-set <record-type> set-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="0a404-183">Дополнительные сведения см. в разделах [Создание записи DNS](#create-a-dns-record) и [Создание записей других типов](#create-records-of-other-types) выше.</span><span class="sxs-lookup"><span data-stu-id="0a404-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="0a404-184">Удаление записи из существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="0a404-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="0a404-185">запись tooremove DNS из существующего набора записей, используйте `az network dns record-set <record-type> remove-record`.</span><span class="sxs-lookup"><span data-stu-id="0a404-185">tooremove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="0a404-186">Чтобы получить справку, см. `az network dns record-set <record-type> remove-record -h`.</span><span class="sxs-lookup"><span data-stu-id="0a404-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="0a404-187">Эта команда удаляет запись DNS из набора записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="0a404-188">При удалении hello последней записи в наборе записей набора сам записей hello также удаляется.</span><span class="sxs-lookup"><span data-stu-id="0a404-188">If hello last record in a record set is deleted, hello record set itself is also deleted.</span></span> <span data-ttu-id="0a404-189">набор пустой записей hello tookeep используйте hello `--keep-empty-record-set` параметр.</span><span class="sxs-lookup"><span data-stu-id="0a404-189">tookeep hello empty record set instead, use hello `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="0a404-190">Требуется toospecify записей toobe hello удален и hello зоны, он должен быть удален из, с помощью hello такими же параметрами, при создании записи с помощью `az network dns record-set <record-type> set-record`.</span><span class="sxs-lookup"><span data-stu-id="0a404-190">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="0a404-191">Эти параметры описаны в предыдущих разделах [Создание записи DNS](#create-a-dns-record) и [Создание записей других типов](#create-records-of-other-types).</span><span class="sxs-lookup"><span data-stu-id="0a404-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="0a404-192">Следующий пример удаляет Hello hello запись со значением "1.2.3.4» из записи hello набор *www* в зоне hello *contoso.com*, в группе ресурсов hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0a404-192">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="0a404-193">Обновление существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="0a404-193">Modify an existing record set</span></span>

<span data-ttu-id="0a404-194">В каждом наборе записей указан [срок жизни](dns-zones-records.md#time-to-live), [метаданные](dns-zones-records.md#tags-and-metadata) и записи DNS.</span><span class="sxs-lookup"><span data-stu-id="0a404-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="0a404-195">Hello следующих разделах объясняется, как toomodify каждого из этих свойств.</span><span class="sxs-lookup"><span data-stu-id="0a404-195">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="0a404-196">toomodify запись A, AAAA, MX, NS, SRV, PTR или TXT</span><span class="sxs-lookup"><span data-stu-id="0a404-196">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="0a404-197">toomodify существующую запись типа A, AAAA, MX, NS, SRV, PTR или TXT, сначала следует добавить новую запись и удаление существующей записи hello.</span><span class="sxs-lookup"><span data-stu-id="0a404-197">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="0a404-198">Подробные инструкции о том, как toodelete и добавьте записи см. в разделе hello в предыдущих разделах данной статьи.</span><span class="sxs-lookup"><span data-stu-id="0a404-198">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="0a404-199">Hello в следующем примере показано, как запись «A» из tooIP IP адрес 1.2.3.4 toomodify устранить 5.6.7.8:</span><span class="sxs-lookup"><span data-stu-id="0a404-199">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="0a404-200">Нельзя добавлять, удалять или изменять hello записи автоматически создается набор на вершине зоны hello записей NS hello (`--Name "@"`, включая кавычки).</span><span class="sxs-lookup"><span data-stu-id="0a404-200">You cannot add, remove, or modify hello records in hello automatically created NS record set at hello zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="0a404-201">Для этого набора записей hello допускается могут только запись hello toomodify набор TTL, а также метаданные.</span><span class="sxs-lookup"><span data-stu-id="0a404-201">For this record set, hello only changes permitted are toomodify hello record set TTL and metadata.</span></span>

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="0a404-202">toomodify запись CNAME</span><span class="sxs-lookup"><span data-stu-id="0a404-202">toomodify a CNAME record</span></span>

<span data-ttu-id="0a404-203">В отличие от большинства других типов записей, набор записей CNAME может содержать только одну запись.</span><span class="sxs-lookup"><span data-stu-id="0a404-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="0a404-204">Таким образом невозможно заменить текущее значение hello, добавив новую запись и удаление существующей записи hello, как и для других типов записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-204">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="0a404-205">Вместо этого используйте toomodify запись CNAME `az network dns record-set cname set-record`.</span><span class="sxs-lookup"><span data-stu-id="0a404-205">Instead, toomodify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="0a404-206">Чтобы получить справку, см. `az network dns record-set cname set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="0a404-207">Hello пример изменяет набор записей типа CNAME hello *www* в зоне hello *contoso.com*, в группе ресурсов *MyResourceGroup*, toopoint слишком «www.fabrikam.net» вместо его существующее значение:</span><span class="sxs-lookup"><span data-stu-id="0a404-207">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="0a404-208">toomodify записи SOA</span><span class="sxs-lookup"><span data-stu-id="0a404-208">toomodify an SOA record</span></span>

<span data-ttu-id="0a404-209">В отличие от большинства других типов записей, набор записей CNAME может содержать только одну запись.</span><span class="sxs-lookup"><span data-stu-id="0a404-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="0a404-210">Таким образом невозможно заменить текущее значение hello, добавив новую запись и удаление существующей записи hello, как и для других типов записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-210">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="0a404-211">Вместо этого используйте toomodify hello начальной записи `az network dns record-set soa update`.</span><span class="sxs-lookup"><span data-stu-id="0a404-211">Instead, toomodify hello SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="0a404-212">Чтобы получить справку, см. `az network dns record-set soa update --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="0a404-213">Hello следующем примере показано, как свойство tooset hello «электронная почта» hello начальной записи зоны hello *contoso.com* в группе ресурсов hello *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0a404-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="0a404-214">записей toomodify NS на вершине зоны hello</span><span class="sxs-lookup"><span data-stu-id="0a404-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="0a404-215">запись NS Hello на вершине зоны hello создается автоматически с каждой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="0a404-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="0a404-216">Она содержит имена hello hello Azure имя серверов назначенного toohello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="0a404-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="0a404-217">Можно добавить дополнительное имя серверов toothis NS: набор записей, toosupport совместное размещение домены с более чем одного поставщика DNS.</span><span class="sxs-lookup"><span data-stu-id="0a404-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="0a404-218">Можно также изменить hello TTL и метаданные для этого набора записей.</span><span class="sxs-lookup"><span data-stu-id="0a404-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="0a404-219">Тем не менее нельзя удалять или изменять hello предварительно заполненных Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="0a404-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="0a404-220">Обратите внимание, что это применимо только toohello NS набора записей на вершине зоны hello.</span><span class="sxs-lookup"><span data-stu-id="0a404-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="0a404-221">Другие NS наборов записей в зоне (как в дочерних зонах используется toodelegate) можно изменять без ограничений.</span><span class="sxs-lookup"><span data-stu-id="0a404-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="0a404-222">Привет, в следующем примере показано, как tooadd запись NS toohello дополнительное имя сервера задать на вершине зоны hello:</span><span class="sxs-lookup"><span data-stu-id="0a404-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="0a404-223">задать hello toomodify TTL существующей записи</span><span class="sxs-lookup"><span data-stu-id="0a404-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="0a404-224">задать hello toomodify TTL существующей записи, используйте `azure network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="0a404-224">toomodify hello TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="0a404-225">Чтобы получить справку, см. `azure network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="0a404-226">Hello в следующем примере показано, как toomodify набора записей TTL, в этом случае too60 секунд:</span><span class="sxs-lookup"><span data-stu-id="0a404-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="0a404-227">toomodify hello метаданных из существующего набора записей</span><span class="sxs-lookup"><span data-stu-id="0a404-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="0a404-228">[Набор записей метаданных](dns-zones-records.md#tags-and-metadata) может быть используется tooassociate данных приложения с каждым набором записей, как пары "ключ значение".</span><span class="sxs-lookup"><span data-stu-id="0a404-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="0a404-229">задать toomodify hello метаданных из существующей записи, используйте `az network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="0a404-229">toomodify hello metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="0a404-230">Чтобы получить справку, см. `az network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="0a404-231">Hello следующем примере показано, как toomodify набор записей с две записи метаданных «dept = процент» и «среды = производства».</span><span class="sxs-lookup"><span data-stu-id="0a404-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="0a404-232">Обратите внимание, что все существующие метаданные *заменить* по заданным значениям hello.</span><span class="sxs-lookup"><span data-stu-id="0a404-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="0a404-233">Удаление набора записей</span><span class="sxs-lookup"><span data-stu-id="0a404-233">Delete a record set</span></span>

<span data-ttu-id="0a404-234">Наборы записей можно удалить с помощью hello `az network dns record-set <record-type> delete` команды.</span><span class="sxs-lookup"><span data-stu-id="0a404-234">Record sets can be deleted by using hello `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="0a404-235">Чтобы получить справку, см. `azure network dns record-set <record-type> delete --help`.</span><span class="sxs-lookup"><span data-stu-id="0a404-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="0a404-236">При удалении набора записей также удаляются все записи в наборе записей hello.</span><span class="sxs-lookup"><span data-stu-id="0a404-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="0a404-237">Не удается удалить hello SOA и NS наборов записей в вершине зоны hello (`--name "@"`).</span><span class="sxs-lookup"><span data-stu-id="0a404-237">You cannot delete hello SOA and NS record sets at hello zone apex (`--name "@"`).</span></span>  <span data-ttu-id="0a404-238">Эти отчеты создаются автоматически при hello зона была создана и автоматически удаляются при удалении hello зоны.</span><span class="sxs-lookup"><span data-stu-id="0a404-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="0a404-239">Hello следующий пример удаляет набор именованных записей hello *www* типа a из зоны hello *contoso.com* в группе ресурсов *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0a404-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="0a404-240">Все операции удаления запрашиваемые tooconfirm hello.</span><span class="sxs-lookup"><span data-stu-id="0a404-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="0a404-241">Этот запрос toosuppress использовать hello `--yes` переключения.</span><span class="sxs-lookup"><span data-stu-id="0a404-241">toosuppress this prompt, use hello `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a404-242">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a404-242">Next steps</span></span>

<span data-ttu-id="0a404-243">См. дополнительные сведения о [зонах и записях в Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0a404-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="0a404-244">Узнайте, каким образом слишком[защиты зоны и записи](dns-protect-zones-recordsets.md) при использовании Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0a404-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
