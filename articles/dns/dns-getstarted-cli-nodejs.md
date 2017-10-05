---
title: "Приступая к работе со службой DNS Azure с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Узнайте, как создать зону и запись DNS в службе DNS Azure. Это пошаговое руководство описывает создание первых зоны и записи DNS, а также управление ими с помощью интерфейса командной строки Azure CLI 1.0."
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
ms.openlocfilehash: f7943b71bbd16c36df09436973d92539eb62b210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-dns-using-azure-cli-10"></a><span data-ttu-id="07543-104">Начало работы со службой DNS Azure с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="07543-104">Get started with Azure DNS using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="07543-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="07543-105">Azure portal</span></span>](dns-getstarted-portal.md)
> * [<span data-ttu-id="07543-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07543-106">PowerShell</span></span>](dns-getstarted-powershell.md)
> * [<span data-ttu-id="07543-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="07543-107">Azure CLI 1.0</span></span>](dns-getstarted-cli-nodejs.md)
> * [<span data-ttu-id="07543-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="07543-108">Azure CLI 2.0</span></span>](dns-getstarted-cli.md)

<span data-ttu-id="07543-109">В этой статье описано, как создать первую зону DNS и первую запись DNS, используя кроссплатформенный интерфейс командной строки Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="07543-109">This article walks you through the steps to create your first DNS zone and record using the cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="07543-110">Эти действия также можно выполнить с помощью портала Azure или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07543-110">You can also perform these steps using the Azure portal or Azure PowerShell.</span></span>

<span data-ttu-id="07543-111">Зона DNS используется для размещения DNS-записей определенного домена.</span><span class="sxs-lookup"><span data-stu-id="07543-111">A DNS zone is used to host the DNS records for a particular domain.</span></span> <span data-ttu-id="07543-112">Чтобы разместить свой домен в Azure DNS, необходимо создать зону DNS для этого доменного имени.</span><span class="sxs-lookup"><span data-stu-id="07543-112">To start hosting your domain in Azure DNS, you need to create a DNS zone for that domain name.</span></span> <span data-ttu-id="07543-113">Каждая запись DNS для вашего домена создается внутри этой зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="07543-113">Each DNS record for your domain is then created inside this DNS zone.</span></span> <span data-ttu-id="07543-114">Наконец, чтобы опубликовать зону DNS в Интернете, необходимо настроить серверы доменных имен для домена.</span><span class="sxs-lookup"><span data-stu-id="07543-114">Finally, to publish your DNS zone to the Internet, you need to configure the name servers for the domain.</span></span> <span data-ttu-id="07543-115">Каждый из этих шагов описан ниже.</span><span class="sxs-lookup"><span data-stu-id="07543-115">Each of these steps is described below.</span></span>

<span data-ttu-id="07543-116">При выполнении этих инструкций предполагается, что вы уже установили Azure CLI 1.0 и выполнили вход.</span><span class="sxs-lookup"><span data-stu-id="07543-116">These instructions assume you have already installed and signed in to Azure CLI 1.0.</span></span> <span data-ttu-id="07543-117">Чтобы получить справку, см. статью [Как управлять зонами DNS в службе DNS Azure с помощью Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="07543-117">For help, see [How to manage DNS zones using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="07543-118">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="07543-118">Create the resource group</span></span>

<span data-ttu-id="07543-119">Перед созданием зоны DNS создается группа ресурсов, которая будет включать эту зону DNS.</span><span class="sxs-lookup"><span data-stu-id="07543-119">Before creating the DNS zone, a resource group is created to contain the DNS Zone.</span></span> <span data-ttu-id="07543-120">Ниже показана команда для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="07543-120">The following shows the command.</span></span>

```azurecli
azure group create --name MyResourceGroup --location "West US"
```

## <a name="create-a-dns-zone"></a><span data-ttu-id="07543-121">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="07543-121">Create a DNS zone</span></span>

<span data-ttu-id="07543-122">Зона DNS создается с помощью команды `azure network dns zone create`.</span><span class="sxs-lookup"><span data-stu-id="07543-122">A DNS zone is created using the `azure network dns zone create` command.</span></span> <span data-ttu-id="07543-123">Чтобы просмотреть справку для этой команды, введите `azure network dns zone create -h`.</span><span class="sxs-lookup"><span data-stu-id="07543-123">To see help for this command, type `azure network dns zone create -h`.</span></span>

<span data-ttu-id="07543-124">В следующем примере будет создана зона DNS *contoso.com* в группе ресурсов *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="07543-124">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*.</span></span> <span data-ttu-id="07543-125">Пример можно использовать для создания зоны DNS, заменив соответствующие значения собственными.</span><span class="sxs-lookup"><span data-stu-id="07543-125">Use the example to create a DNS zone, substituting the values for your own.</span></span>

```azurecli
azure network dns zone create MyResourceGroup contoso.com
```


## <a name="create-a-dns-record"></a><span data-ttu-id="07543-126">Создание записи DNS</span><span class="sxs-lookup"><span data-stu-id="07543-126">Create a DNS record</span></span>

<span data-ttu-id="07543-127">Чтобы создать запись DNS, используйте команду `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="07543-127">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="07543-128">Чтобы получить справку, см. `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="07543-128">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="07543-129">В следующем примере создается запись с относительным именем www в зоне DNS contoso.com, в группе ресурсов MyResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="07543-129">The following example creates a record with the relative name "www" in the DNS Zone "contoso.com", in resource group "MyResourceGroup".</span></span> <span data-ttu-id="07543-130">Полное доменное имя набора записей — www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="07543-130">The fully-qualified name of the record set is "www.contoso.com".</span></span> <span data-ttu-id="07543-131">Используется тип записи A с IP-адресом 1.2.3.4 и сроком жизни по умолчанию 3600 секунд (1 час).</span><span class="sxs-lookup"><span data-stu-id="07543-131">The record type is "A", with IP address "1.2.3.4", and a default TTL of 3600 seconds (1 hour) is used.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="07543-132">Сведения о других типах записей, наборах записей с несколькими записями, других значениях срока жизни, а также об изменении существующих записей см. в статье [Управление записями DNS в Azure DNS с помощью Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="07543-132">For other record types, for record sets with more than one record, for alternative TTL values, and to modify existing records, see [Manage DNS records and record sets using the Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>


## <a name="view-records"></a><span data-ttu-id="07543-133">Просмотр записей</span><span class="sxs-lookup"><span data-stu-id="07543-133">View records</span></span>

<span data-ttu-id="07543-134">Чтобы просмотреть список записей DNS в зоне, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="07543-134">To list the DNS records in your zone, use:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```


## <a name="update-name-servers"></a><span data-ttu-id="07543-135">Обновление серверов доменных имен</span><span class="sxs-lookup"><span data-stu-id="07543-135">Update name servers</span></span>

<span data-ttu-id="07543-136">Когда вы убедитесь, что зона и записи DNS настроены правильно, необходимо настроить доменное имя для использования серверов доменных имен службы DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="07543-136">Once you are satisfied that your DNS zone and records have been set up correctly, you need to configure your domain name to use the Azure DNS name servers.</span></span> <span data-ttu-id="07543-137">Это позволит другим пользователям в Интернете находить ваши записи DNS.</span><span class="sxs-lookup"><span data-stu-id="07543-137">This enables other users on the Internet to find your DNS records.</span></span>

<span data-ttu-id="07543-138">Для получения списка серверов доменных имен для определенной зоны используется команда `azure network dns zone show`.</span><span class="sxs-lookup"><span data-stu-id="07543-138">The name servers for your zone are given by the `azure network dns zone show` command:</span></span>

```azurecli
azure network dns zone show MyResourceGroup contoso.com

info:    Executing command network dns zone show
+ Looking up the dns zone "contoso.com"
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

<span data-ttu-id="07543-139">Эти серверы доменных имен необходимо настроить с помощью регистратора доменных имен (у которого было приобретено доменное имя).</span><span class="sxs-lookup"><span data-stu-id="07543-139">These name servers should be configured with the domain name registrar (where you purchased the domain name).</span></span> <span data-ttu-id="07543-140">Регистратор предложит вам вариант настройки серверов доменных имен для домена.</span><span class="sxs-lookup"><span data-stu-id="07543-140">Your registrar will offer the option to set up the name servers for the domain.</span></span> <span data-ttu-id="07543-141">Дополнительные сведения см. в статье [Делегирование домена в Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="07543-141">For more information, see [Delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>

## <a name="delete-all-resources"></a><span data-ttu-id="07543-142">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="07543-142">Delete all resources</span></span>
 
<span data-ttu-id="07543-143">Чтобы удалить все ресурсы, созданные при работе с этой статьей, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="07543-143">To delete all resources created in this article, take the following step:</span></span>

```azurecli
azure group delete --name MyResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="07543-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07543-144">Next steps</span></span>

<span data-ttu-id="07543-145">Дополнительные сведения о службе DNS Azure см. в статье [Обзор Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="07543-145">To learn more about Azure DNS, see [Azure DNS overview](dns-overview.md).</span></span>

<span data-ttu-id="07543-146">Дополнительные сведения об управлении зонами DNS в службе DNS Azure см. в статье [Как управлять зонами DNS в службе DNS Azure с помощью Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="07543-146">To learn more about managing DNS zones in Azure DNS, see [Manage DNS zones in Azure DNS using Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md).</span></span>

<span data-ttu-id="07543-147">Дополнительные сведения об управлении записями DNS в службе DNS Azure см. в статье [Управление записями DNS в Azure DNS с помощью Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="07543-147">To learn more about managing DNS records in Azure DNS, see [Manage DNS records and record sets in Azure DNS using Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md).</span></span>

