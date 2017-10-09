---
title: "aaaGet работы с Azure DNS, с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как toocreate DNS зоны и записи в Azure DNS. Это toocreate Пошаговое руководство и управлять первый DNS-зоны и записи с помощью Azure CLI 2.0 hello."
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fb0aa0a6-d096-4d6a-b2f6-eda1c64f6182
ms.service: dns
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: jonatul
ms.openlocfilehash: 8a894941e9910d5cc35394a1be9dbca9792613f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="11627-104">Начало работы со службой DNS Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="11627-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="11627-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="11627-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="11627-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="11627-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="11627-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="11627-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="11627-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="11627-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="11627-109">В этой статье поможет выполнить шаги toocreate hello вашей первой зоны DNS и записи с помощью hello Azure CLI кросс платформенных 2.0, которая доступна для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="11627-109">This article walks you through hello steps toocreate your first DNS zone and record using hello cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="11627-110">Также можно выполнить следующие действия с помощью hello портал Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11627-110">You can also perform these steps using hello Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="11627-111">Зоны DNS-записей DNS используется toohost hello для определенного домена.</span><span class="sxs-lookup"><span data-stu-id="11627-111">A DNS zone is used toohost hello DNS records for a particular domain.</span></span> <span data-ttu-id="11627-112">toostart размещение домена в Azure DNS необходимо toocreate зону DNS для этого имени домена.</span><span class="sxs-lookup"><span data-stu-id="11627-112">toostart hosting your domain in Azure DNS, you need toocreate a DNS zone for that domain name.</span></span> <span data-ttu-id="11627-113">Каждая запись DNS для вашего домена создается внутри этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="11627-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="11627-114">Наконец, toopublish toohello Интернета, зоны DNS-сервера требуется tooconfigure hello имя серверов для домена hello.</span><span class="sxs-lookup"><span data-stu-id="11627-114">Finally, toopublish your DNS zone toohello Internet, you need tooconfigure hello name servers for hello domain.</span></span> <span data-ttu-id="11627-115">Каждый из этих шагов описан ниже.</span><span class="sxs-lookup"><span data-stu-id="11627-115">Each of these steps is described below.</span></span>

<span data-ttu-id="11627-116">Эти инструкции предполагают, вы уже установили и вход выполнен tooAzure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="11627-116">These instructions assume you have already installed and signed in tooAzure CLI 2.0.</span></span> <span data-ttu-id="11627-117">Справочные сведения см. в разделе [как toomanage DNS-зоны с помощью Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="11627-117">For help, see [How toomanage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="11627-118">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="11627-118">Create hello resource group</span></span>

<span data-ttu-id="11627-119">Перед созданием hello зоны DNS, зоны DNS hello toocontain создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="11627-119">Before creating hello DNS zone, a resource group is created toocontain hello DNS Zone.</span></span> <span data-ttu-id="11627-120">Hello ниже показана команда hello.</span><span class="sxs-lookup"><span data-stu-id="11627-120">hello following shows hello command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="11627-121">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="11627-121">Create a DNS zone</span></span>

<span data-ttu-id="11627-122">Зоны DNS создается с помощью hello `az network dns zone create` команды.</span><span class="sxs-lookup"><span data-stu-id="11627-122">A DNS zone is created using hello `az network dns zone create` command.</span></span> <span data-ttu-id="11627-123">toosee справку для этой команды, введите `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="11627-123">toosee help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="11627-124">Hello следующий пример создает зоны DNS, которая называется *contoso.com* в группе ресурсов hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="11627-124">hello following example creates a DNS zone called *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="11627-125">Используйте toocreate пример hello зону DNS, подставив собственные значения hello.</span><span class="sxs-lookup"><span data-stu-id="11627-125">Use hello example toocreate a DNS zone, substituting hello values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="11627-126">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="11627-126">Create a DNS record</span></span>

<span data-ttu-id="11627-127">запись DNS toocreate использовать hello `az network dns record-set [record type] add-record` команды.</span><span class="sxs-lookup"><span data-stu-id="11627-127">toocreate a DNS record, use hello `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="11627-128">Чтобы получить справку, например по записям типа A, см. `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="11627-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="11627-129">Hello в примере создается запись с hello относительное имя «www» в зону DNS «contoso.com» в группе ресурсов «MyResourceGroup» hello.</span><span class="sxs-lookup"><span data-stu-id="11627-129">hello following example creates a record with hello relative name "www" in hello DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="11627-130">Hello полное имя набора записей hello — «www.contoso.com».</span><span class="sxs-lookup"><span data-stu-id="11627-130">hello fully-qualified name of hello record set is "www.contoso.com".</span></span> <span data-ttu-id="11627-131">Тип записи Hello — «A» с IP-адресом «1.2.3.4», и используется значение по умолчанию срок ЖИЗНИ 3600 секунд (1 час).</span><span class="sxs-lookup"><span data-stu-id="11627-131">hello record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="11627-132">Для других типов записей для наборов записей с более одной записи для альтернативных значений срока ЖИЗНИ и toomodify существующие записи, в разделе [Управление DNS-записи и с помощью наборов записей hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="11627-132">For other record types, for record sets with more than one record, for alternative TTL values, and toomodify existing records, see [Manage DNS records and record sets using hello Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="11627-133">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="11627-133">View records</span></span>

<span data-ttu-id="11627-134">toolist hello DNS-записи в зоне, используйте:</span><span class="sxs-lookup"><span data-stu-id="11627-134">toolist hello DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="11627-135">Обновление серверов доменных имен</span><span class="sxs-lookup"><span data-stu-id="11627-135">Update name servers</span></span>

<span data-ttu-id="11627-136">Как только будут выполнены, что DNS-зоны и записи были настроены правильно, необходимо tooconfigure домена имя toouse hello Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="11627-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need tooconfigure your domain name toouse hello Azure DNS name servers.</span></span> <span data-ttu-id="11627-137">Это позволяет другим пользователям на hello Internet toofind DNS-записей.</span><span class="sxs-lookup"><span data-stu-id="11627-137">This enables other users on hello Internet toofind your DNS records.</span></span>

<span data-ttu-id="11627-138">Hello серверы имен для зоны определяются hello `az network dns zone show` команды.</span><span class="sxs-lookup"><span data-stu-id="11627-138">hello name servers for your zone are given by hello `az network dns zone show` command.</span></span> <span data-ttu-id="11627-139">имена серверов имя toosee hello, используйте выходных данных, JSON, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="11627-139">toosee hello name server names, use JSON output, as shown in hello following example.</span></span>

```azurecli
az network dns zone show -g MyResourceGroup -n contoso.com -o json

{
  "etag": "00000003-0000-0000-b40d-0996b97ed101",
  "id": "/subscriptions/a385a691-bd93-41b0-8084-8213ebc5bff7/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-01.azure-dns.com.",
    "ns2-01.azure-dns.net.",
    "ns3-01.azure-dns.org.",
    "ns4-01.azure-dns.info."
  ],
  "numberOfRecordSets": 3,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="11627-140">Эти серверы имен должны быть настроены с помощью регистратора доменных имен hello (которого вы приобрели hello доменное имя).</span><span class="sxs-lookup"><span data-stu-id="11627-140">These name servers should be configured with hello domain name registrar (where you purchased hello domain name).</span></span> <span data-ttu-id="11627-141">Регистратор предлагают tooset параметр hello hello серверов имя домена hello.</span><span class="sxs-lookup"><span data-stu-id="11627-141">Your registrar will offer hello option tooset up hello name servers for hello domain.</span></span> <span data-ttu-id="11627-142">Дополнительные сведения см. в разделе [делегировать tooAzure вашего домена DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="11627-142">For more information, see [Delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="11627-143">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="11627-143">Delete all resources</span></span>
 
<span data-ttu-id="11627-144">toodelete все ресурсы созданы в этой статье hello выполните следующий шаг:</span><span class="sxs-lookup"><span data-stu-id="11627-144">toodelete all resources created in this article, take hello following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="11627-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11627-145">Next steps</span></span>

<span data-ttu-id="11627-146">toolearn Дополнительные сведения о Azure DNS в разделе [Обзор Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11627-146">toolearn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="11627-147">toolearn Дополнительные сведения об управлении зонами DNS в Azure DNS, в разделе [зоны DNS, управление в Azure DNS, с помощью Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="11627-147">toolearn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="11627-148">toolearn Дополнительные сведения об управлении DNS-записи в Azure DNS, в разделе [Управление DNS-записи и записи задает в Azure DNS, с помощью Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="11627-148">toolearn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
