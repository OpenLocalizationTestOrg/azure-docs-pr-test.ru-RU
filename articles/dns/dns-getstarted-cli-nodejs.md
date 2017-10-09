---
title: "aaaGet работы с Azure DNS, с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate DNS зоны и записи в Azure DNS. Это toocreate Пошаговое руководство и управлять первый DNS-зоны и записи с помощью hello Azure CLI 1.0."
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
ms.openlocfilehash: e200c848ad261160e593306dbb8a1d92bf26880b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="b1b95-104">Начало работы со службой DNS Azure с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b1b95-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1b95-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="b1b95-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="b1b95-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1b95-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="b1b95-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b1b95-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="b1b95-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b1b95-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="b1b95-109">В этой статье поможет выполнить шаги toocreate hello вашей первой зоны DNS и записи с помощью hello Azure CLI кросс платформенных 1.0, которая доступна для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="b1b95-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="b1b95-110">Также можно выполнить следующие действия с помощью hello портал Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1b95-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="b1b95-111">Зоны DNS-записей DNS используется toohost hello для определенного домена.</span><span class="sxs-lookup"><span data-stu-id="b1b95-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="b1b95-112">toostart размещение домена в Azure DNS необходимо toocreate зону DNS для этого имени домена.</span><span class="sxs-lookup"><span data-stu-id="b1b95-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="b1b95-113">Каждая запись DNS для вашего домена создается внутри этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="b1b95-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="b1b95-114">Наконец, toopublish toohello Интернета, зоны DNS-сервера требуется tooconfigure hello имя серверов для домена hello.</span><span class="sxs-lookup"><span data-stu-id="b1b95-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="b1b95-115">Каждый из этих шагов описан ниже.</span><span class="sxs-lookup"><span data-stu-id="b1b95-115">Each of these steps is described below.</span></span>

<span data-ttu-id="b1b95-116">Эти инструкции предполагают, вы уже установили и вход выполнен tooAzure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="b1b95-116">These instructions assume you have already installed and signed in tooAzure CLI 1.0.</span></span> <span data-ttu-id="b1b95-117">Справочные сведения см. в разделе [как toomanage DNS-зоны с помощью Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b1b95-117">For help, see [How toomanage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="b1b95-118">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="b1b95-118">Create hello resource group</span></span>

<span data-ttu-id="b1b95-119">Перед созданием hello зоны DNS, зоны DNS hello toocontain создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b1b95-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="b1b95-120">Hello ниже показана команда hello.</span><span class="sxs-lookup"><span data-stu-id="b1b95-120">hello following shows hello command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="b1b95-121">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="b1b95-121">Create a DNS zone</span></span>

<span data-ttu-id="b1b95-122">Зоны DNS создается с помощью hello `azure network dns zone create` команды.</span><span class="sxs-lookup"><span data-stu-id="b1b95-122">A DNS zone is created using hello `azure network dns zone create` command.</span></span> <span data-ttu-id="b1b95-123">toosee справку для этой команды, введите `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="b1b95-123">toosee help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="b1b95-124">Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello вызывается *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b1b95-124">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="b1b95-125">Используйте toocreate пример hello зону DNS, подставив собственные значения hello.</span><span class="sxs-lookup"><span data-stu-id="b1b95-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="b1b95-126">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="b1b95-126">Create a DNS record</span></span>

<span data-ttu-id="b1b95-127">запись DNS toocreate использовать hello `azure network dns record-set add-record` команды.</span><span class="sxs-lookup"><span data-stu-id="b1b95-127">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="b1b95-128">Чтобы получить справку, см. `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="b1b95-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="b1b95-129">Hello в примере создается запись с hello относительное имя «www» в зону DNS «contoso.com» в группе ресурсов «MyResourceGroup» hello.</span><span class="sxs-lookup"><span data-stu-id="b1b95-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="b1b95-130">Hello полное имя набора записей hello — «www.contoso.com».</span><span class="sxs-lookup"><span data-stu-id="b1b95-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="b1b95-131">Тип записи Hello — «A» с IP-адресом «1.2.3.4», и используется значение по умолчанию срок ЖИЗНИ 3600 секунд (1 час).</span><span class="sxs-lookup"><span data-stu-id="b1b95-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="b1b95-132">Для других типов записей для наборов записей с более одной записи для альтернативных значений срока ЖИЗНИ и toomodify существующие записи, в разделе [Управление DNS-записи и с помощью наборов записей hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b1b95-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="b1b95-133">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="b1b95-133">View records</span></span>

<span data-ttu-id="b1b95-134">toolist hello DNS-записи в зоне, используйте:</span><span class="sxs-lookup"><span data-stu-id="b1b95-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="b1b95-135">Обновление серверов доменных имен</span><span class="sxs-lookup"><span data-stu-id="b1b95-135">Update name servers</span></span>

<span data-ttu-id="b1b95-136">Как только будут выполнены, что DNS-зоны и записи были настроены правильно, необходимо tooconfigure домена имя toouse hello Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="b1b95-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="b1b95-137">Это позволяет другим пользователям на hello Internet toofind DNS-записей.</span><span class="sxs-lookup"><span data-stu-id="b1b95-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="b1b95-138">Hello серверы имен для зоны определяются hello `azure network dns zone show` команды:</span><span class="sxs-lookup"><span data-stu-id="b1b95-138">hello name servers for your zone are given by hello `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up hello dns zone "contoso.com"
data:    Id                              : /subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com
data:    Name                            : contoso.com
data:    Type                            : Microsoft.Network/dnszones
data:    Location                        : global
data:    Number of record sets           : 3
data:    Max number of record sets       : 5000
data:    Name servers:
data:        ns1-01.azure-dns.com.
data:        ns2-01.azure-dns.net.
data:        ns3-01.azure-dns.org.
data:        ns4-01.azure-dns.info.
data:    Tags                            :
info:    network dns zone show command OK
```

<span data-ttu-id="b1b95-139">Эти серверы имен должны быть настроены с помощью регистратора доменных имен hello (которого вы приобрели hello доменное имя).</span><span class="sxs-lookup"><span data-stu-id="b1b95-139">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="b1b95-140">Регистратор предлагают tooset параметр hello hello серверов имя домена hello.</span><span class="sxs-lookup"><span data-stu-id="b1b95-140">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="b1b95-141">Дополнительные сведения см. в разделе [делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="b1b95-141">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="b1b95-142">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="b1b95-142">Delete all resources</span></span>
 
<span data-ttu-id="b1b95-143">toodelete все ресурсы созданы в этой статье hello выполните следующий шаг:</span><span class="sxs-lookup"><span data-stu-id="b1b95-143">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b1b95-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1b95-144">Next steps</span></span>

<span data-ttu-id="b1b95-145">toolearn Дополнительные сведения о Azure DNS в разделе [Обзор Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1b95-145">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="b1b95-146">toolearn Дополнительные сведения об управлении зонами DNS в Azure DNS, в разделе [зоны DNS, управление в Azure DNS, с помощью Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b1b95-146">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="b1b95-147">toolearn Дополнительные сведения об управлении DNS-записи в Azure DNS, в разделе [Управление DNS-записи и записи задает в Azure DNS, с помощью Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b1b95-147">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

