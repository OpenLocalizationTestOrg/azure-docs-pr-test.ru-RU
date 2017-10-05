---
title: "Делегирование домена в Azure DNS | Документация Майкрософт"
description: "Узнайте, как изменить делегирование домена и использовать серверы имен Azure DNS для размещения домена."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: 33b3ec24432ff1268860b9a2e9d5098600a8dedc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-a-domain-to-azure-dns"></a><span data-ttu-id="d65a1-103">Делегирование домена в Azure DNS</span><span class="sxs-lookup"><span data-stu-id="d65a1-103">Delegate a domain to Azure DNS</span></span>

<span data-ttu-id="d65a1-104">Azure DNS позволяет размещать зону DNS и управлять записями DNS для домена в Azure.</span><span class="sxs-lookup"><span data-stu-id="d65a1-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="d65a1-105">Чтобы запросы DNS для домена достигали Azure DNS, домен должен быть делегирован в Azure DNS из родительского домена.</span><span class="sxs-lookup"><span data-stu-id="d65a1-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span></span> <span data-ttu-id="d65a1-106">Помните, что Azure DNS — это не регистратор доменных имен.</span><span class="sxs-lookup"><span data-stu-id="d65a1-106">Keep in mind Azure DNS is not the domain registrar.</span></span> <span data-ttu-id="d65a1-107">В этой статье описывается делегирование домена в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-107">This article explains how to delegate your domain to Azure DNS.</span></span>

<span data-ttu-id="d65a1-108">Для доменов, приобретенных у регистратора доменных имен, эти записи может настроить сам регистратор.</span><span class="sxs-lookup"><span data-stu-id="d65a1-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span></span> <span data-ttu-id="d65a1-109">Для создания зоны DNS с доменным именем в Azure DNS необязательно быть его владельцем.</span><span class="sxs-lookup"><span data-stu-id="d65a1-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="d65a1-110">Однако вам необходимо быть владельцем домена, чтобы настроить делегирование в Azure DNS у регистратора доменных имен.</span><span class="sxs-lookup"><span data-stu-id="d65a1-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span></span>

<span data-ttu-id="d65a1-111">Предположим, например, что вы приобрели домен contoso.net и создали зону с именем contoso.net в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="d65a1-112">Регистратор предоставляет вам как владельцу домена возможность настройки адресов серверов имен (то есть записи NS) для домена.</span><span class="sxs-lookup"><span data-stu-id="d65a1-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span></span> <span data-ttu-id="d65a1-113">Регистратор будет хранить эти записи NS в родительском домене, в данном случае это .net.</span><span class="sxs-lookup"><span data-stu-id="d65a1-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span></span> <span data-ttu-id="d65a1-114">Клиенты по всему миру будут направляться в ваш домен в зоне Azure DNS при попытке разрешить записи DNS в contoso.net.</span><span class="sxs-lookup"><span data-stu-id="d65a1-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="d65a1-115">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="d65a1-115">Create a DNS zone</span></span>

1. <span data-ttu-id="d65a1-116">Выполните вход на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d65a1-116">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="d65a1-117">В главном меню щелкните **Создать > Сети**, а затем щелкните **Зона DNS**, чтобы открыть колонку "Создать зону DNS".</span><span class="sxs-lookup"><span data-stu-id="d65a1-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Зона DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="d65a1-119">В колонке **Создание зоны DNS** введите следующие значения, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="d65a1-120">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="d65a1-120">**Setting**</span></span> | <span data-ttu-id="d65a1-121">**Значение**</span><span class="sxs-lookup"><span data-stu-id="d65a1-121">**Value**</span></span> | <span data-ttu-id="d65a1-122">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="d65a1-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="d65a1-123">**Имя**</span><span class="sxs-lookup"><span data-stu-id="d65a1-123">**Name**</span></span>|<span data-ttu-id="d65a1-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="d65a1-124">contoso.net</span></span>|<span data-ttu-id="d65a1-125">Имя зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-125">The name of the DNS zone</span></span>|
   |<span data-ttu-id="d65a1-126">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="d65a1-126">**Subscription**</span></span>|<span data-ttu-id="d65a1-127">[Ваша подписка]</span><span class="sxs-lookup"><span data-stu-id="d65a1-127">[Your subscription]</span></span>|<span data-ttu-id="d65a1-128">Выберите подписку для создания шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="d65a1-128">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="d65a1-129">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="d65a1-129">**Resource group**</span></span>|<span data-ttu-id="d65a1-130">**Создать:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="d65a1-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="d65a1-131">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d65a1-131">Create a resource group.</span></span> <span data-ttu-id="d65a1-132">Имя группы ресурсов должно быть уникальным в пределах выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="d65a1-132">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="d65a1-133">Дополнительные сведения о группах ресурсов см. в разделе [Группы ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) статьи "Общие сведения об Azure Resource Manager".</span><span class="sxs-lookup"><span data-stu-id="d65a1-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="d65a1-134">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="d65a1-134">**Location**</span></span>|<span data-ttu-id="d65a1-135">Запад США</span><span class="sxs-lookup"><span data-stu-id="d65a1-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="d65a1-136">Этот параметр относится к расположению группы ресурсов и никак не влияет на расположение зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="d65a1-137">Расположение зоны DNS всегда является "глобальным" и не отображается.</span><span class="sxs-lookup"><span data-stu-id="d65a1-137">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="d65a1-138">Получение серверов имен</span><span class="sxs-lookup"><span data-stu-id="d65a1-138">Retrieve name servers</span></span>

<span data-ttu-id="d65a1-139">Прежде чем делегировать зоны DNS в службу DNS Azure, сначала необходимо знать имена серверов имен зоны.</span><span class="sxs-lookup"><span data-stu-id="d65a1-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span></span> <span data-ttu-id="d65a1-140">Когда создается зона, служба DNS Azure выделяет серверы имен из пула.</span><span class="sxs-lookup"><span data-stu-id="d65a1-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="d65a1-141">Создав зону DNS, на портале Azure в области **Избранное** щелкните **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="d65a1-142">Щелкните зону DNS **contoso.net** в колонке **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="d65a1-143">Если выбранная подписка имеет несколько ресурсов, в поле "Фильтровать по имени..." введите **contoso.net**,</span><span class="sxs-lookup"><span data-stu-id="d65a1-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span></span> <span data-ttu-id="d65a1-144">чтобы быстро получить доступ к необходимому шлюзу приложений.</span><span class="sxs-lookup"><span data-stu-id="d65a1-144">box to easily access the application gateway.</span></span> 

1. <span data-ttu-id="d65a1-145">Получите серверы имен в колонке "Зона DNS".</span><span class="sxs-lookup"><span data-stu-id="d65a1-145">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="d65a1-146">В этом примере зоне contoso.net назначены серверы доменных имен ns1-01.azure-dns.com, ns2-01.azure-dns.net, ns3-01.azure-dns.org и ns4-01.azure-dns.info.</span><span class="sxs-lookup"><span data-stu-id="d65a1-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Сервер имен DNS](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="d65a1-148">Служба DNS Azure автоматически создает в вашей зоне заслуживающие доверия NS-записи, в которых указаны выделенные серверы имен.</span><span class="sxs-lookup"><span data-stu-id="d65a1-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="d65a1-149">Чтобы увидеть серверы имен через Azure PowerShell или интерфейс командной строки Azure, необходимо просто получить эти записи.</span><span class="sxs-lookup"><span data-stu-id="d65a1-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

<span data-ttu-id="d65a1-150">Ниже приведены примеры получения серверов имен для зоны в Azure DNS с помощью PowerShell и Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d65a1-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="d65a1-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d65a1-151">PowerShell</span></span>

```powershell
# The record name "@" is used to refer to records at the top of the zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="d65a1-152">Ниже приведен пример ответа.</span><span class="sxs-lookup"><span data-stu-id="d65a1-152">The following example is the response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="d65a1-153">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="d65a1-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="d65a1-154">Ниже приведен пример ответа.</span><span class="sxs-lookup"><span data-stu-id="d65a1-154">The following example is the response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-the-domain"></a><span data-ttu-id="d65a1-155">Делегирование домена</span><span class="sxs-lookup"><span data-stu-id="d65a1-155">Delegate the domain</span></span>

<span data-ttu-id="d65a1-156">Теперь, когда зона DNS создана и у вас есть серверы имен, необходимо обновить родительский домен с серверами имен Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span></span> <span data-ttu-id="d65a1-157">У каждого регистратора есть собственные средства управления DNS для изменения записей серверов имен домена.</span><span class="sxs-lookup"><span data-stu-id="d65a1-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="d65a1-158">На странице управления DNS регистратора замените записи NS на созданные службой Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span></span>

<span data-ttu-id="d65a1-159">При делегировании домена службе Azure DNS вам необходимо использовать имена серверов доменных имен, предоставленные службой Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span></span> <span data-ttu-id="d65a1-160">Рекомендуется всегда использовать все четыре имени серверов доменных имен независимо от имени домена.</span><span class="sxs-lookup"><span data-stu-id="d65a1-160">It is recommended to use all four name server names, regardless of the name of your domain.</span></span> <span data-ttu-id="d65a1-161">Для делегирования домена не требуется, чтобы в имени сервера доменных имен и вашем домене содержался один и тот же домен верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="d65a1-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span></span>

<span data-ttu-id="d65a1-162">Не используйте "связующие записи" для указания IP-адресов сервера доменных имен Azure DNS, поскольку эти IP-адреса в будущем могут измениться.</span><span class="sxs-lookup"><span data-stu-id="d65a1-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="d65a1-163">Делегирование с использованием имен серверов доменных имен в собственной зоне (также известны как серверы личных имен) в настоящее время не поддерживается в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="d65a1-164">Проверка работы разрешения имен</span><span class="sxs-lookup"><span data-stu-id="d65a1-164">Verify name resolution is working</span></span>

<span data-ttu-id="d65a1-165">По завершении делегирования можно проверить, работает ли разрешение имен. Это можно сделать с помощью такого средства, как nslookup, запросив запись типа SOA для своей зоны (также автоматически создается при создании зоны).</span><span class="sxs-lookup"><span data-stu-id="d65a1-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span></span>

<span data-ttu-id="d65a1-166">Вам не требуется указывать серверы имен Azure DNS, так как стандартный процесс разрешения DNS находит их автоматически, если делегирование настроено правильно.</span><span class="sxs-lookup"><span data-stu-id="d65a1-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="d65a1-167">Ниже приведен пример ответа из предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="d65a1-167">The following is an example response from the preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="d65a1-168">Делегирование поддоменов в Azure DNS</span><span class="sxs-lookup"><span data-stu-id="d65a1-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="d65a1-169">Если нужно настроить отдельную дочернюю зону, можно делегировать поддомен в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="d65a1-170">Предположим, что после настройки и делегирования contoso.net в Azure DNS требуется настроить отдельную дочернюю зону partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="d65a1-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="d65a1-171">Создайте в Azure DNS дочернюю зону partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="d65a1-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="d65a1-172">Поищите заслуживающие доверия записи сервера имен в дочерней зоне, чтобы получить список серверов имен, в которых в Azure DNS размещена дочерняя зона.</span><span class="sxs-lookup"><span data-stu-id="d65a1-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span></span>
3. <span data-ttu-id="d65a1-173">Выполните делегирование дочерней зоны. Для этого настройте записи сервера имен в родительской зоне, указывающей на дочернюю.</span><span class="sxs-lookup"><span data-stu-id="d65a1-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="d65a1-174">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="d65a1-174">Create a DNS zone</span></span>

1. <span data-ttu-id="d65a1-175">Выполните вход на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d65a1-175">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="d65a1-176">В главном меню щелкните **Создать > Сети**, а затем щелкните **Зона DNS**, чтобы открыть колонку "Создать зону DNS".</span><span class="sxs-lookup"><span data-stu-id="d65a1-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Зона DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="d65a1-178">В колонке **Создание зоны DNS** введите следующие значения, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="d65a1-179">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="d65a1-179">**Setting**</span></span> | <span data-ttu-id="d65a1-180">**Значение**</span><span class="sxs-lookup"><span data-stu-id="d65a1-180">**Value**</span></span> | <span data-ttu-id="d65a1-181">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="d65a1-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="d65a1-182">**Имя**</span><span class="sxs-lookup"><span data-stu-id="d65a1-182">**Name**</span></span>|<span data-ttu-id="d65a1-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="d65a1-183">partners.contoso.net</span></span>|<span data-ttu-id="d65a1-184">Имя зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-184">The name of the DNS zone</span></span>|
   |<span data-ttu-id="d65a1-185">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="d65a1-185">**Subscription**</span></span>|<span data-ttu-id="d65a1-186">[Ваша подписка]</span><span class="sxs-lookup"><span data-stu-id="d65a1-186">[Your subscription]</span></span>|<span data-ttu-id="d65a1-187">Выберите подписку для создания шлюза приложений.</span><span class="sxs-lookup"><span data-stu-id="d65a1-187">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="d65a1-188">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="d65a1-188">**Resource group**</span></span>|<span data-ttu-id="d65a1-189">**Использовать существующий:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="d65a1-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="d65a1-190">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d65a1-190">Create a resource group.</span></span> <span data-ttu-id="d65a1-191">Имя группы ресурсов должно быть уникальным в пределах выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="d65a1-191">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="d65a1-192">Дополнительные сведения о группах ресурсов см. в разделе [Группы ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) статьи "Общие сведения об Azure Resource Manager".</span><span class="sxs-lookup"><span data-stu-id="d65a1-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="d65a1-193">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="d65a1-193">**Location**</span></span>|<span data-ttu-id="d65a1-194">Запад США</span><span class="sxs-lookup"><span data-stu-id="d65a1-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="d65a1-195">Этот параметр относится к расположению группы ресурсов и никак не влияет на расположение зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="d65a1-196">Расположение зоны DNS всегда является "глобальным" и не отображается.</span><span class="sxs-lookup"><span data-stu-id="d65a1-196">The DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="d65a1-197">Получение серверов имен</span><span class="sxs-lookup"><span data-stu-id="d65a1-197">Retrieve name servers</span></span>

1. <span data-ttu-id="d65a1-198">Создав зону DNS, на портале Azure в области **Избранное** щелкните **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="d65a1-199">Щелкните зону DNS **partners.contoso.net** в колонке **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="d65a1-200">Если выбранная подписка имеет несколько ресурсов, в поле "Фильтровать по имени..." введите **partners.contoso.net**,</span><span class="sxs-lookup"><span data-stu-id="d65a1-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span></span> <span data-ttu-id="d65a1-201">чтобы быстро получить доступ к необходимой зоне DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-201">box to easily access the DNS zone.</span></span>

1. <span data-ttu-id="d65a1-202">Получите серверы имен в колонке "Зона DNS".</span><span class="sxs-lookup"><span data-stu-id="d65a1-202">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="d65a1-203">В этом примере зоне contoso.net назначены серверы доменных имен ns1-01.azure-dns.com, ns2-01.azure-dns.net, ns3-01.azure-dns.org и ns4-01.azure-dns.info.</span><span class="sxs-lookup"><span data-stu-id="d65a1-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Сервер имен DNS](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="d65a1-205">Служба DNS Azure автоматически создает в вашей зоне заслуживающие доверия NS-записи, в которых указаны выделенные серверы имен.</span><span class="sxs-lookup"><span data-stu-id="d65a1-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="d65a1-206">Чтобы увидеть серверы имен через Azure PowerShell или интерфейс командной строки Azure, необходимо просто получить эти записи.</span><span class="sxs-lookup"><span data-stu-id="d65a1-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="d65a1-207">Создание записи сервера имен в родительской зоне</span><span class="sxs-lookup"><span data-stu-id="d65a1-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="d65a1-208">На портале Azure перейдите к зоне DNS **contoso.net**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span></span>
1. <span data-ttu-id="d65a1-209">Щелкните **+ Record set** (+ Набор записей).</span><span class="sxs-lookup"><span data-stu-id="d65a1-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="d65a1-210">В колонке **Добавление набора записей** введите приведенные ниже значения и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-210">On the **Add record set** blade, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="d65a1-211">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="d65a1-211">**Setting**</span></span> | <span data-ttu-id="d65a1-212">**Значение**</span><span class="sxs-lookup"><span data-stu-id="d65a1-212">**Value**</span></span> | <span data-ttu-id="d65a1-213">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="d65a1-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="d65a1-214">**Имя**</span><span class="sxs-lookup"><span data-stu-id="d65a1-214">**Name**</span></span>|<span data-ttu-id="d65a1-215">partners</span><span class="sxs-lookup"><span data-stu-id="d65a1-215">partners</span></span>|<span data-ttu-id="d65a1-216">Имя дочерней зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="d65a1-216">The name of the child DNS zone</span></span>|
   |<span data-ttu-id="d65a1-217">**Тип**</span><span class="sxs-lookup"><span data-stu-id="d65a1-217">**Type**</span></span>|<span data-ttu-id="d65a1-218">NS</span><span class="sxs-lookup"><span data-stu-id="d65a1-218">NS</span></span>|<span data-ttu-id="d65a1-219">Используйте NS для записей серверов имен.</span><span class="sxs-lookup"><span data-stu-id="d65a1-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="d65a1-220">**Срок жизни**</span><span class="sxs-lookup"><span data-stu-id="d65a1-220">**TTL**</span></span>|<span data-ttu-id="d65a1-221">1</span><span class="sxs-lookup"><span data-stu-id="d65a1-221">1</span></span>|<span data-ttu-id="d65a1-222">Срок жизни.</span><span class="sxs-lookup"><span data-stu-id="d65a1-222">Time to live.</span></span>|
   |<span data-ttu-id="d65a1-223">**Единица срока жизни**</span><span class="sxs-lookup"><span data-stu-id="d65a1-223">**TTL unit**</span></span>|<span data-ttu-id="d65a1-224">Часы</span><span class="sxs-lookup"><span data-stu-id="d65a1-224">Hours</span></span>|<span data-ttu-id="d65a1-225">Указывает срок жизни в часах.</span><span class="sxs-lookup"><span data-stu-id="d65a1-225">sets time to live unit to hours</span></span>|
   |<span data-ttu-id="d65a1-226">**Сервер доменных имен**</span><span class="sxs-lookup"><span data-stu-id="d65a1-226">**NAME SERVER**</span></span>|<span data-ttu-id="d65a1-227">{серверы доменных имен из зоны partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="d65a1-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="d65a1-228">Введите все 4 сервера доменных имен из зоны partners.contoso.net.</span><span class="sxs-lookup"><span data-stu-id="d65a1-228">Enter all 4 of the name servers from partners.contoso.net zone.</span></span> |

   ![Сервер имен DNS](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="d65a1-230">Делегирование поддоменов в Azure DNS с помощью других средств</span><span class="sxs-lookup"><span data-stu-id="d65a1-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="d65a1-231">Ниже приведены примеры делегирования поддоменов в Azure DNS с помощью PowerShell и CLI:</span><span class="sxs-lookup"><span data-stu-id="d65a1-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="d65a1-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d65a1-232">PowerShell</span></span>

<span data-ttu-id="d65a1-233">Этот процесс продемонстрирован в приведенном ниже примере PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d65a1-233">The following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="d65a1-234">Эти же действия можно выполнить с помощью портала Azure или кроссплатформенного интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="d65a1-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span></span>

```powershell
# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve the authoritative NS records from the child zone as shown in the next example. This contains the name servers assigned to the child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create the corresponding NS record set in the parent zone to complete the delegation. The record set name in the parent zone matches the child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="d65a1-235">Используйте `nslookup`, чтобы убедиться в правильности настройки зоны, просмотрев запись типа SOA дочерней зоны.</span><span class="sxs-lookup"><span data-stu-id="d65a1-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="d65a1-236">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="d65a1-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="d65a1-237">Получите серверы доменных имен для зоны `partners.contoso.net` из выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d65a1-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="d65a1-238">Создайте набор записей и записи NS для каждого сервера доменных имен.</span><span class="sxs-lookup"><span data-stu-id="d65a1-238">Create the record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create the record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="d65a1-239">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="d65a1-239">Delete all resources</span></span>

<span data-ttu-id="d65a1-240">Чтобы удалить все ресурсы, созданные в этой статье, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d65a1-240">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="d65a1-241">На портале Azure в области **Избранное** щелкните **Все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-241">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="d65a1-242">Щелкните группу ресурсов **contosorg** в колонке "Все ресурсы".</span><span class="sxs-lookup"><span data-stu-id="d65a1-242">Click the **contosorg** resource group in the All resources blade.</span></span> <span data-ttu-id="d65a1-243">Если выбранная подписка имеет несколько ресурсов, в поле **Фильтровать по имени...** введите **contosorg**,</span><span class="sxs-lookup"><span data-stu-id="d65a1-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span></span> <span data-ttu-id="d65a1-244">чтобы быстро получить доступ к необходимой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d65a1-244">box to easily access the resource group.</span></span>
1. <span data-ttu-id="d65a1-245">В колонке **contosorg** нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-245">In the **contosorg** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="d65a1-246">На портале появится запрос на ввод имени группы ресурсов для подтверждения удаления.</span><span class="sxs-lookup"><span data-stu-id="d65a1-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="d65a1-247">Введите *contosorg* для имени группы ресурсов, а затем щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="d65a1-247">Type *contosorg* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="d65a1-248">При удалении группы ресурсов удаляются все расположенные в ней ресурсы. Поэтому перед удалением группы ресурсов всегда проверяйте ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="d65a1-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="d65a1-249">Сначала портал удаляет все ресурсы, содержащиеся в группе ресурсов, а затем удаляет и саму группу.</span><span class="sxs-lookup"><span data-stu-id="d65a1-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="d65a1-250">Этот процесс занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d65a1-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d65a1-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d65a1-251">Next steps</span></span>

[<span data-ttu-id="d65a1-252">Управление зонами DNS</span><span class="sxs-lookup"><span data-stu-id="d65a1-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="d65a1-253">Управление зонами DNS</span><span class="sxs-lookup"><span data-stu-id="d65a1-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
