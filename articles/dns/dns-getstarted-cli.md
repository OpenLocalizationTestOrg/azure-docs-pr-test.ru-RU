---
title: "Приступая к работе со службой DNS Azure с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "Узнайте, как создать зону и запись DNS в службе DNS Azure. Это пошаговое руководство описывает создание первых зоны и записи DNS, а также управление ими с помощью интерфейса командной строки Azure CLI 2.0."
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
ms.openlocfilehash: 6958d61b29961f59cb22f62bec55f2d467e7e7cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-20"></a><span data-ttu-id="4c095-104">Начало работы со службой DNS Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4c095-104">Get started with Azure DNS using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c095-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4c095-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="4c095-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c095-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="4c095-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4c095-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="4c095-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4c095-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="4c095-109">В этой статье описано, как создать первую зону DNS и первую запись DNS, используя кроссплатформенный интерфейс командной строки Azure CLI 2.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="4c095-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="4c095-110">Эти действия также можно выполнить с помощью портала Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4c095-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="4c095-111">Зона DNS используется для размещения DNS-записей определенного домена.</span><span class="sxs-lookup"><span data-stu-id="4c095-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="4c095-112">Чтобы разместить свой домен в Azure DNS, необходимо создать зону DNS для этого доменного имени.</span><span class="sxs-lookup"><span data-stu-id="4c095-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="4c095-113">Каждая запись DNS для вашего домена создается внутри этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="4c095-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="4c095-114">Наконец, чтобы опубликовать зону DNS в Интернете, необходимо настроить серверы доменных имен для домена.</span><span class="sxs-lookup"><span data-stu-id="4c095-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="4c095-115">Каждый из этих шагов описан ниже.</span><span class="sxs-lookup"><span data-stu-id="4c095-115">Each of these steps is described below.</span></span>

<span data-ttu-id="4c095-116">При выполнении этих инструкций предполагается, что вы уже установили Azure CLI 2.0 и выполнили вход.</span><span class="sxs-lookup"><span data-stu-id="4c095-116">These instructions assume you have already installed and signed in to Azure CLI 2.0.</span></span> <span data-ttu-id="4c095-117">Чтобы получить справку, см. статью [Как управлять зонами DNS в службе DNS Azure с помощью Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4c095-117">For help, see [How to manage DNS zones using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="4c095-118">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="4c095-118">Create the resource group</span></span>

<span data-ttu-id="4c095-119">Перед созданием зоны DNS создается группа ресурсов, которая будет включать эту зону DNS.</span><span class="sxs-lookup"><span data-stu-id="4c095-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="4c095-120">Ниже показана команда для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4c095-120">The following shows the command.</span></span>

```azurecli
az group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="4c095-121">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="4c095-121">Create a DNS zone</span></span>

<span data-ttu-id="4c095-122">Зона DNS создается с помощью команды `az network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="4c095-122">A DNS zone is created using the `az network dns zone create` command.</span></span> <span data-ttu-id="4c095-123">Чтобы просмотреть справку для этой команды, введите `az network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="4c095-123">To see help for this command, type `az network dns zone create -h`.</span></span>

<span data-ttu-id="4c095-124">В следующем примере будет создана зона DNS *contoso.com* в группе ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="4c095-124">The following example creates a DNS zone called *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="4c095-125">Пример можно использовать для создания зоны DNS, заменив соответствующие значения собственными.</span><span class="sxs-lookup"><span data-stu-id="4c095-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="4c095-126">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="4c095-126">Create a DNS record</span></span>

<span data-ttu-id="4c095-127">Чтобы создать запись DNS, используйте команду `az network dns record-set [record type] add-record`.</span><span class="sxs-lookup"><span data-stu-id="4c095-127">To create a DNS record, use the `az network dns record-set [record type] add-record` command.</span></span> <span data-ttu-id="4c095-128">Чтобы получить справку, например по записям типа A, см. `azure network dns record-set A add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="4c095-128">For help, for A records for example, see `azure network dns record-set A add-record -h`.</span></span>

<span data-ttu-id="4c095-129">В следующем примере создается запись с относительным именем www в зоне DNS contoso.com, в группе ресурсов MyResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="4c095-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="4c095-130">Полное доменное имя набора записей — www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4c095-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="4c095-131">Используется тип записи A с IP-адресом 1.2.3.4 и сроком жизни по умолчанию 3600 секунд (1 час).</span><span class="sxs-lookup"><span data-stu-id="4c095-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
az network dns record-set a add-record -g MyResourceGroup -z contoso.com -n www -a 1.2.3.4
```

<span data-ttu-id="4c095-132">Сведения о других типах записей, наборах записей с несколькими записями, других значениях срока жизни, а также об изменении существующих записей см. в статье [Управление записями и наборами записей DNS в Azure DNS с помощью Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4c095-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="4c095-133">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="4c095-133">View records</span></span>

<span data-ttu-id="4c095-134">Чтобы просмотреть список записей DNS в зоне, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4c095-134">To list the DNS records in your zone, use:</span></span>

```azurecli
az network dns record-set list -g MyResourceGroup -z contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="4c095-135">Обновление серверов доменных имен</span><span class="sxs-lookup"><span data-stu-id="4c095-135">Update name servers</span></span>

<span data-ttu-id="4c095-136">Когда вы убедитесь, что зона и записи DNS настроены правильно, необходимо настроить доменное имя для использования серверов доменных имен службы DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="4c095-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="4c095-137">Это позволит другим пользователям в Интернете находить ваши записи DNS.</span><span class="sxs-lookup"><span data-stu-id="4c095-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="4c095-138">Для получения списка серверов доменных имен для определенной зоны используется команда `az network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="4c095-138">The name servers for your zone are given by the `az network dns zone show` command.</span></span> <span data-ttu-id="4c095-139">Чтобы просмотреть имена серверов доменных имен, используйте выходные данные JSON, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4c095-139">To see the name server names, use JSON output, as shown in the following example.</span></span>

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

<span data-ttu-id="4c095-140">Эти серверы доменных имен необходимо настроить с помощью регистратора доменных имен (у которого было приобретено доменное имя).</span><span class="sxs-lookup"><span data-stu-id="4c095-140">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="4c095-141">Регистратор предложит вам вариант настройки серверов доменных имен для домена.</span><span class="sxs-lookup"><span data-stu-id="4c095-141">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="4c095-142">Дополнительные сведения см. в статье [Делегирование домена в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="4c095-142">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="4c095-143">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="4c095-143">Delete all resources</span></span>
 
<span data-ttu-id="4c095-144">Чтобы удалить все ресурсы, созданные при работе с этой статьей, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4c095-144">To delete all resources created in this article, take the following step:</span></span>

```azurecli
az group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4c095-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c095-145">Next steps</span></span>

<span data-ttu-id="4c095-146">Дополнительные сведения о службе DNS Azure см. в статье [Обзор Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c095-146">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="4c095-147">Дополнительные сведения об управлении зонами DNS в службе DNS Azure см. в статье [Как управлять зонами DNS в службе DNS Azure с помощью Azure CLI 2.0](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4c095-147">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 2.0](dns-operations-dnszones-cli.md).</span></span>

<span data-ttu-id="4c095-148">Дополнительные сведения об управлении записями DNS в службе DNS Azure см. в статье [Управление записями и наборами записей DNS в Azure DNS с помощью Azure CLI 2.0](dns-operations-recordsets-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4c095-148">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 2.0](dns-operations-recordsets-cli.md).</span></span>
