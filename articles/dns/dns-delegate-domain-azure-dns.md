---
title: "aaaDelegate tooAzure вашего домена DNS | Документы Microsoft"
description: "Понять, как toochange делегирования домена и Azure DNS используйте имя размещение домена tooprovide серверов."
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
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="7459a-103">Делегат tooAzure домена DNS</span><span class="sxs-lookup"><span data-stu-id="7459a-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="7459a-104">Azure DNS позволяет toohost зоны DNS и управлять hello записей DNS для домена в Azure.</span><span class="sxs-lookup"><span data-stu-id="7459a-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="7459a-105">Чтобы запросы DNS для домена tooreach Azure DNS, hello домен имеет toobe делегировать tooAzure DNS из родительского домена hello.</span><span class="sxs-lookup"><span data-stu-id="7459a-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="7459a-106">Имейте в виду Azure DNS не hello регистратора домена.</span><span class="sxs-lookup"><span data-stu-id="7459a-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="7459a-107">В этой статье объясняется, как toodelegate tooAzure вашего домена DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="7459a-108">Для доменов, приобретенных у регистратора регистратор предлагает tooset параметр hello этих записей NS.</span><span class="sxs-lookup"><span data-stu-id="7459a-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="7459a-109">У вас tooown домена toocreate зоны DNS с помощью этого доменного имени в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="7459a-110">Тем не менее следует соблюдать tooset домена hello tooown копирование tooAzure hello делегирование DNS у регистратора hello.</span><span class="sxs-lookup"><span data-stu-id="7459a-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="7459a-111">Например предположим, вы приобрели hello домена «contoso.net» и создать зону с именем hello «contoso.net» в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="7459a-112">Как владелец домена hello hello регистратор предлагает hello параметр tooconfigure hello имя адреса сервера (то есть записи hello NS) для своего домена.</span><span class="sxs-lookup"><span data-stu-id="7459a-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="7459a-113">Эти записи NS сохраняет регистратора Hello в hello родительский домен, в данном случае «.net».</span><span class="sxs-lookup"><span data-stu-id="7459a-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="7459a-114">Затем клиенты вокруг Здравствуй, мир! можно направленной tooyour домена в зоне Azure DNS при попытке tooresolve DNS-записи в «contoso.net».</span><span class="sxs-lookup"><span data-stu-id="7459a-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="7459a-115">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7459a-115">Create a DNS zone</span></span>

1. <span data-ttu-id="7459a-116">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7459a-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="7459a-117">Hello концентратора меню и нажмите кнопку **Создать > Сетевые подключения >** и нажмите кнопку **зоны DNS** tooopen hello создать DNS-зоны колонку.</span><span class="sxs-lookup"><span data-stu-id="7459a-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Зона DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="7459a-119">На hello **создать DNS-зоны** колонки введите следующие значения hello, затем щелкните **создать**:</span><span class="sxs-lookup"><span data-stu-id="7459a-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="7459a-120">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="7459a-120">**Setting**</span></span> | <span data-ttu-id="7459a-121">**Значение**</span><span class="sxs-lookup"><span data-stu-id="7459a-121">**Value**</span></span> | <span data-ttu-id="7459a-122">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="7459a-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7459a-123">**Имя**</span><span class="sxs-lookup"><span data-stu-id="7459a-123">**Name**</span></span>|<span data-ttu-id="7459a-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="7459a-124">contoso.net</span></span>|<span data-ttu-id="7459a-125">Имя зоны DNS hello Hello</span><span class="sxs-lookup"><span data-stu-id="7459a-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="7459a-126">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="7459a-126">**Subscription**</span></span>|<span data-ttu-id="7459a-127">[Ваша подписка]</span><span class="sxs-lookup"><span data-stu-id="7459a-127">[Your subscription]</span></span>|<span data-ttu-id="7459a-128">Выберите шлюз приложения hello toocreate подписки в.</span><span class="sxs-lookup"><span data-stu-id="7459a-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="7459a-129">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="7459a-129">**Resource group**</span></span>|<span data-ttu-id="7459a-130">**Создать:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="7459a-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="7459a-131">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7459a-131">Create a resource group.</span></span> <span data-ttu-id="7459a-132">Имя группы ресурсов Hello должно быть уникальным в пределах hello подписки, выбранной.</span><span class="sxs-lookup"><span data-stu-id="7459a-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="7459a-133">Дополнительные сведения о группах ресурсов, чтение hello toolearn [диспетчера ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) обзорную статью.</span><span class="sxs-lookup"><span data-stu-id="7459a-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="7459a-134">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="7459a-134">**Location**</span></span>|<span data-ttu-id="7459a-135">Запад США</span><span class="sxs-lookup"><span data-stu-id="7459a-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="7459a-136">Группа ресурсов Hello относится toohello расположение группы ресурсов hello, а не оказывает влияния на hello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="7459a-137">расположение зоны DNS Hello всегда «глобальные» и не отображается.</span><span class="sxs-lookup"><span data-stu-id="7459a-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="7459a-138">Получение серверов имен</span><span class="sxs-lookup"><span data-stu-id="7459a-138">Retrieve name servers</span></span>

<span data-ttu-id="7459a-139">Прежде чем делегировать вашей tooAzure зоны DNS DNS, необходимо сначала tooknow hello имя сервера имен для зоны.</span><span class="sxs-lookup"><span data-stu-id="7459a-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="7459a-140">Когда создается зона, служба DNS Azure выделяет серверы имен из пула.</span><span class="sxs-lookup"><span data-stu-id="7459a-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="7459a-141">С помощью зоны DNS hello, созданные в hello портал Azure **Избранное** области, нажмите кнопку **все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="7459a-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="7459a-142">Нажмите кнопку hello **contoso.net** зоны DNS в hello **все ресурсы** колонку.</span><span class="sxs-lookup"><span data-stu-id="7459a-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="7459a-143">Если подписка hello, уже содержит несколько ресурсов, можно ввести **contoso.net** в hello фильтр по имени...</span><span class="sxs-lookup"><span data-stu-id="7459a-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="7459a-144">шлюз приложения hello доступа tooeasily поле.</span><span class="sxs-lookup"><span data-stu-id="7459a-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="7459a-145">Получить серверы имен hello из колонки зоны DNS hello.</span><span class="sxs-lookup"><span data-stu-id="7459a-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="7459a-146">В этом примере hello зоны «contoso.net» назначаемые серверы имен "ns1-01.azure-dns.com", «ns2-01.azure dns .net», "ns3-01.azure-dns.org", и "ns4-01.azure-dns.info":</span><span class="sxs-lookup"><span data-stu-id="7459a-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Сервер имен DNS](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="7459a-148">Azure DNS автоматически создает записи заслуживающих доверия NS в зоне содержащий hello, назначаемые серверы имен.</span><span class="sxs-lookup"><span data-stu-id="7459a-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="7459a-149">Имя сервера toosee hello имена через Azure PowerShell или Azure CLI, необходимо просто tooretrieve этих записей.</span><span class="sxs-lookup"><span data-stu-id="7459a-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="7459a-150">Hello следующие примеры также предоставляют действия hello серверы имен hello tooretrieve для зоны DNS Azure с помощью PowerShell и Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7459a-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="7459a-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7459a-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="7459a-152">Следующий пример Hello — ответ hello.</span><span class="sxs-lookup"><span data-stu-id="7459a-152">hello following example is hello response.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="7459a-153">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7459a-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="7459a-154">Следующий пример Hello — ответ hello.</span><span class="sxs-lookup"><span data-stu-id="7459a-154">hello following example is hello response.</span></span>

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

## <a name="delegate-hello-domain"></a><span data-ttu-id="7459a-155">Делегат hello домена</span><span class="sxs-lookup"><span data-stu-id="7459a-155">Delegate hello domain</span></span>

<span data-ttu-id="7459a-156">Теперь, когда создается зона DNS hello и у вас есть серверы имен hello, hello родительский домен должен toobe обновляется hello Azure DNS-серверами.</span><span class="sxs-lookup"><span data-stu-id="7459a-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="7459a-157">Каждый регистратор имеет свои собственные управления средств toochange hello имя сервера записи DNS для домена.</span><span class="sxs-lookup"><span data-stu-id="7459a-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="7459a-158">На странице управления hello регистратора DNS редактирования записей NS hello и замените записей NS hello hello из них созданы Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="7459a-159">При делегировании tooAzure домена DNS, необходимо использовать имена серверов имя hello, предоставляемые Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="7459a-160">Рекомендуется toouse все четыре имен сервера имен, независимо от того, hello имя вашего домена.</span><span class="sxs-lookup"><span data-stu-id="7459a-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="7459a-161">Делегирование доменов не требует hello имя сервера имя toouse hello домену верхнего уровня, в домене.</span><span class="sxs-lookup"><span data-stu-id="7459a-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="7459a-162">Не следует использовать «делегирование» toopoint toohello Azure DNS имя сервера IP-адресов, так как эти IP-адреса может измениться в будущем.</span><span class="sxs-lookup"><span data-stu-id="7459a-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="7459a-163">Делегирование с использованием имен серверов доменных имен в собственной зоне (также известны как серверы личных имен) в настоящее время не поддерживается в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="7459a-164">Проверка работы разрешения имен</span><span class="sxs-lookup"><span data-stu-id="7459a-164">Verify name resolution is working</span></span>

<span data-ttu-id="7459a-165">После завершения hello делегирование, можно проверить, что разрешение имен работает с помощью такого средства, как «nslookup» tooquery hello начальной записи для зоны (который также создается автоматически при создании зоны hello).</span><span class="sxs-lookup"><span data-stu-id="7459a-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="7459a-166">Нет toospecify hello Azure DNS-серверами, если делегирование hello была настроена неправильно, hello обычный DNS процесс разрешения находит серверы приветствия имен автоматически.</span><span class="sxs-lookup"><span data-stu-id="7459a-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="7459a-167">Hello ниже приведен пример ответа от предшествующих команда hello.</span><span class="sxs-lookup"><span data-stu-id="7459a-167">hello following is an example response from hello preceding command:</span></span>

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

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="7459a-168">Делегирование поддоменов в Azure DNS</span><span class="sxs-lookup"><span data-stu-id="7459a-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="7459a-169">Если вы хотите tooset копирование отдельной дочерней зоне, вы можете делегировать дочерний домен в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="7459a-170">Например, Настройка и делегированные «contoso.net» в Azure DNS, предположим, что хотелось бы tooset копирование отдельной дочерней зоне, «partners.contoso.net».</span><span class="sxs-lookup"><span data-stu-id="7459a-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="7459a-171">Создайте дочерние зоны hello «partners.contoso.net» в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="7459a-172">Поиск записей заслуживающих доверия NS hello в hello дочерние зоны tooobtain hello серверы имен размещение hello дочерней зоны в Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="7459a-173">Настройка записей NS в родительской зоне hello, указывающий toohello дочерней зоны делегировать hello дочерней зоны.</span><span class="sxs-lookup"><span data-stu-id="7459a-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="7459a-174">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7459a-174">Create a DNS zone</span></span>

1. <span data-ttu-id="7459a-175">Войдите в toohello портал Azure</span><span class="sxs-lookup"><span data-stu-id="7459a-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="7459a-176">Hello концентратора меню и нажмите кнопку **Создать > Сетевые подключения >** и нажмите кнопку **зоны DNS** tooopen hello создать DNS-зоны колонку.</span><span class="sxs-lookup"><span data-stu-id="7459a-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Зона DNS](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="7459a-178">На hello **создать DNS-зоны** колонки введите следующие значения hello, затем щелкните **создать**:</span><span class="sxs-lookup"><span data-stu-id="7459a-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="7459a-179">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="7459a-179">**Setting**</span></span> | <span data-ttu-id="7459a-180">**Значение**</span><span class="sxs-lookup"><span data-stu-id="7459a-180">**Value**</span></span> | <span data-ttu-id="7459a-181">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="7459a-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7459a-182">**Имя**</span><span class="sxs-lookup"><span data-stu-id="7459a-182">**Name**</span></span>|<span data-ttu-id="7459a-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="7459a-183">partners.contoso.net</span></span>|<span data-ttu-id="7459a-184">Имя зоны DNS hello Hello</span><span class="sxs-lookup"><span data-stu-id="7459a-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="7459a-185">**Подписка**</span><span class="sxs-lookup"><span data-stu-id="7459a-185">**Subscription**</span></span>|<span data-ttu-id="7459a-186">[Ваша подписка]</span><span class="sxs-lookup"><span data-stu-id="7459a-186">[Your subscription]</span></span>|<span data-ttu-id="7459a-187">Выберите шлюз приложения hello toocreate подписки в.</span><span class="sxs-lookup"><span data-stu-id="7459a-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="7459a-188">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="7459a-188">**Resource group**</span></span>|<span data-ttu-id="7459a-189">**Использовать существующий:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="7459a-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="7459a-190">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7459a-190">Create a resource group.</span></span> <span data-ttu-id="7459a-191">Имя группы ресурсов Hello должно быть уникальным в пределах hello подписки, выбранной.</span><span class="sxs-lookup"><span data-stu-id="7459a-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="7459a-192">Дополнительные сведения о группах ресурсов, чтение hello toolearn [диспетчера ресурсов](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) обзорную статью.</span><span class="sxs-lookup"><span data-stu-id="7459a-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="7459a-193">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="7459a-193">**Location**</span></span>|<span data-ttu-id="7459a-194">Запад США</span><span class="sxs-lookup"><span data-stu-id="7459a-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="7459a-195">Группа ресурсов Hello относится toohello расположение группы ресурсов hello, а не оказывает влияния на hello зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="7459a-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="7459a-196">расположение зоны DNS Hello всегда «глобальные» и не отображается.</span><span class="sxs-lookup"><span data-stu-id="7459a-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="7459a-197">Получение серверов имен</span><span class="sxs-lookup"><span data-stu-id="7459a-197">Retrieve name servers</span></span>

1. <span data-ttu-id="7459a-198">С помощью зоны DNS hello, созданные в hello портал Azure **Избранное** области, нажмите кнопку **все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="7459a-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="7459a-199">Нажмите кнопку hello **partners.contoso.net** зоны DNS в hello **все ресурсы** колонку.</span><span class="sxs-lookup"><span data-stu-id="7459a-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="7459a-200">Если подписка hello, уже содержит несколько ресурсов, можно ввести **partners.contoso.net** в hello фильтр по имени...</span><span class="sxs-lookup"><span data-stu-id="7459a-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="7459a-201">зона DNS hello доступа tooeasily поле.</span><span class="sxs-lookup"><span data-stu-id="7459a-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="7459a-202">Получить серверы имен hello из колонки зоны DNS hello.</span><span class="sxs-lookup"><span data-stu-id="7459a-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="7459a-203">В этом примере hello зоны «contoso.net» назначаемые серверы имен "ns1-01.azure-dns.com", «ns2-01.azure dns .net», "ns3-01.azure-dns.org", и "ns4-01.azure-dns.info":</span><span class="sxs-lookup"><span data-stu-id="7459a-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Сервер имен DNS](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="7459a-205">Azure DNS автоматически создает записи заслуживающих доверия NS в зоне содержащий hello, назначаемые серверы имен.</span><span class="sxs-lookup"><span data-stu-id="7459a-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="7459a-206">Имя сервера toosee hello имена через Azure PowerShell или Azure CLI, необходимо просто tooretrieve этих записей.</span><span class="sxs-lookup"><span data-stu-id="7459a-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="7459a-207">Создание записи сервера имен в родительской зоне</span><span class="sxs-lookup"><span data-stu-id="7459a-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="7459a-208">Перейдите toohello **contoso.net** зоны DNS в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7459a-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="7459a-209">Щелкните **+ Record set** (+ Набор записей).</span><span class="sxs-lookup"><span data-stu-id="7459a-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="7459a-210">На hello **добавить набор записей** колонки, введите следующие значения hello, затем щелкните **ОК**:</span><span class="sxs-lookup"><span data-stu-id="7459a-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="7459a-211">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="7459a-211">**Setting**</span></span> | <span data-ttu-id="7459a-212">**Значение**</span><span class="sxs-lookup"><span data-stu-id="7459a-212">**Value**</span></span> | <span data-ttu-id="7459a-213">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="7459a-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="7459a-214">**Имя**</span><span class="sxs-lookup"><span data-stu-id="7459a-214">**Name**</span></span>|<span data-ttu-id="7459a-215">partners</span><span class="sxs-lookup"><span data-stu-id="7459a-215">partners</span></span>|<span data-ttu-id="7459a-216">Имя Hello hello дочерней зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7459a-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="7459a-217">**Тип**</span><span class="sxs-lookup"><span data-stu-id="7459a-217">**Type**</span></span>|<span data-ttu-id="7459a-218">NS</span><span class="sxs-lookup"><span data-stu-id="7459a-218">NS</span></span>|<span data-ttu-id="7459a-219">Используйте NS для записей серверов имен.</span><span class="sxs-lookup"><span data-stu-id="7459a-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="7459a-220">**Срок жизни**</span><span class="sxs-lookup"><span data-stu-id="7459a-220">**TTL**</span></span>|<span data-ttu-id="7459a-221">1</span><span class="sxs-lookup"><span data-stu-id="7459a-221">1</span></span>|<span data-ttu-id="7459a-222">Время toolive.</span><span class="sxs-lookup"><span data-stu-id="7459a-222">Time toolive.</span></span>|
   |<span data-ttu-id="7459a-223">**Единица срока жизни**</span><span class="sxs-lookup"><span data-stu-id="7459a-223">**TTL unit**</span></span>|<span data-ttu-id="7459a-224">Часы</span><span class="sxs-lookup"><span data-stu-id="7459a-224">Hours</span></span>|<span data-ttu-id="7459a-225">Задает toohours toolive единица времени</span><span class="sxs-lookup"><span data-stu-id="7459a-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="7459a-226">**Сервер доменных имен**</span><span class="sxs-lookup"><span data-stu-id="7459a-226">**NAME SERVER**</span></span>|<span data-ttu-id="7459a-227">{серверы доменных имен из зоны partners.contoso.net}</span><span class="sxs-lookup"><span data-stu-id="7459a-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="7459a-228">Введите все 4 hello серверы имен из partners.contoso.net зоны.</span><span class="sxs-lookup"><span data-stu-id="7459a-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Сервер имен DNS](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="7459a-230">Делегирование поддоменов в Azure DNS с помощью других средств</span><span class="sxs-lookup"><span data-stu-id="7459a-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="7459a-231">Hello ниже приведены примеры hello действия toodelegate поддоменов в Azure DNS с помощью PowerShell и интерфейс командной строки:</span><span class="sxs-lookup"><span data-stu-id="7459a-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="7459a-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7459a-232">PowerShell</span></span>

<span data-ttu-id="7459a-233">Следующий пример PowerShell Hello показано, как это работает.</span><span class="sxs-lookup"><span data-stu-id="7459a-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="7459a-234">Здравствуйте, одну последовательность шагов может быть выполнен через портал Azure hello, или через hello кросс платформенных Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7459a-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="7459a-235">Используйте `nslookup` tooverify, все настроено правильно, произведя поиск hello начальной записи зоны дочерних hello.</span><span class="sxs-lookup"><span data-stu-id="7459a-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

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

#### <a name="azure-cli"></a><span data-ttu-id="7459a-236">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7459a-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="7459a-237">Получить hello серверы доменных имен для hello `partners.contoso.net` зоны hello в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="7459a-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

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

<span data-ttu-id="7459a-238">Создайте набор записей hello и записи NS для каждого имени сервера.</span><span class="sxs-lookup"><span data-stu-id="7459a-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="7459a-239">Удаление всех ресурсов</span><span class="sxs-lookup"><span data-stu-id="7459a-239">Delete all resources</span></span>

<span data-ttu-id="7459a-240">toodelete все ресурсы, которые созданы в этой статье завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7459a-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="7459a-241">В hello портал Azure **Избранное** области, нажмите кнопку **все ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="7459a-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="7459a-242">Нажмите кнопку hello **contosorg** группа ресурсов в hello все колонки ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7459a-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="7459a-243">Если подписка hello, уже содержит несколько ресурсов, можно ввести **contosorg** в hello **фильтрация по имени...**</span><span class="sxs-lookup"><span data-stu-id="7459a-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="7459a-244">Группа ресурсов hello доступа tooeasily поле.</span><span class="sxs-lookup"><span data-stu-id="7459a-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="7459a-245">В hello **contosorg** колонка, щелкните hello **удалить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7459a-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="7459a-246">Hello портала требуется имя hello tootype tooconfirm группы ресурсов hello, что требуется toodelete его.</span><span class="sxs-lookup"><span data-stu-id="7459a-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="7459a-247">Тип *contosorg* hello имя группы ресурсов, нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="7459a-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="7459a-248">При удалении группы ресурсов будут удалены все ресурсы в группе ресурсов hello, поэтому всегда tooconfirm убедиться, что содержимое hello группу ресурсов перед его удалением.</span><span class="sxs-lookup"><span data-stu-id="7459a-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="7459a-249">портал Hello удаляет все ресурсы, содержащиеся в группе ресурсов hello, а затем удаляет hello самой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7459a-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="7459a-250">Этот процесс занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7459a-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7459a-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7459a-251">Next steps</span></span>

[<span data-ttu-id="7459a-252">Управление зонами DNS</span><span class="sxs-lookup"><span data-stu-id="7459a-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="7459a-253">Управление зонами DNS</span><span class="sxs-lookup"><span data-stu-id="7459a-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
