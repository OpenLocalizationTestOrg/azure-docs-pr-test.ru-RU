---
title: "Обратная зона DNS для служб Azure | Документация Майкрософт"
description: "Узнайте, как настроить обратный просмотр DNS для размещенных в Azure служб."
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
ms.openlocfilehash: 63701e1ce0c1c6dcf2ce02ebce272b8280395e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="c868a-103">Настройка обратного просмотра DNS для размещенных в Azure служб</span><span class="sxs-lookup"><span data-stu-id="c868a-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="c868a-104">Из этой статьи вы узнаете, как настроить обратный просмотр DNS для размещенных в Azure служб.</span><span class="sxs-lookup"><span data-stu-id="c868a-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="c868a-105">Службы в Azure используют IP-адреса, присвоенные им службой Azure и являющиеся собственностью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c868a-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="c868a-106">Эти записи в обратной зоне DNS (записи типа PTR) должны создаваться в соответствующих зонах обратного просмотра DNS, принадлежащих корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c868a-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="c868a-107">В этой статье описано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="c868a-107">This article explains how to do this.</span></span>

<span data-ttu-id="c868a-108">Этот сценарий не следует путать с возможностью [размещать зоны обратного просмотра DNS для присвоенных диапазонов IP-адресов в службе Azure DNS](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="c868a-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="c868a-109">В этом случае диапазоны IP-адресов, представленные зоной обратного просмотра, должны быть присвоены организации (как правило, поставщиком услуг Интернета).</span><span class="sxs-lookup"><span data-stu-id="c868a-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="c868a-110">Перед прочтением этой статьи ознакомьтесь со статьей [Основные сведения об обратной зоне DNS и ее поддержке в Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c868a-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="c868a-111">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c868a-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="c868a-112">В модели развертывания Resource Manager вычислительные ресурсы (например, виртуальные машины, масштабируемые наборы виртуальных машин или кластеры Service Fabric) предоставляются с помощью ресурса PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="c868a-112">In the Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="c868a-113">Обратный просмотр DNS настраивается с помощью свойства ReverseFqdn ресурса PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="c868a-113">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>
* <span data-ttu-id="c868a-114">В классической модели развертывания вычислительные ресурсы предоставляются с помощью облачных служб.</span><span class="sxs-lookup"><span data-stu-id="c868a-114">In the Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="c868a-115">Обратный просмотр DNS настраивается с помощью свойства ReverseDnsFqdn облачной службы.</span><span class="sxs-lookup"><span data-stu-id="c868a-115">Reverse DNS lookups are configured using the 'ReverseDnsFqdn' property of the Cloud Service.</span></span>

<span data-ttu-id="c868a-116">Служба приложений Azure пока не поддерживает обратную зону DNS.</span><span class="sxs-lookup"><span data-stu-id="c868a-116">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="c868a-117">Проверка записей обратной зоны DNS</span><span class="sxs-lookup"><span data-stu-id="c868a-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="c868a-118">Чтобы сторонние лица не могли создавать записи обратной зоны DNS для сопоставления своих служб Azure с вашими доменами DNS, предусмотрен специальный механизм.</span><span class="sxs-lookup"><span data-stu-id="c868a-118">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="c868a-119">Azure позволяет создать запись обратной зоны DNS, только если доменное имя, указанное в такой записи, совпадает с DNS-именем либо IP-адресом (или разрешается в них) ресурса PublicIpAddress или облачной службы в той же подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="c868a-119">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="c868a-120">Эта проверка выполняется только при добавлении или изменении записи обратной зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="c868a-120">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="c868a-121">Периодическая повторная проверка не выполняется.</span><span class="sxs-lookup"><span data-stu-id="c868a-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="c868a-122">Предположим, ресурс PublicIpAddress имеет DNS-имя contosoapp1.northus.cloudapp.azure.com и IP-адрес 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="c868a-122">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="c868a-123">Свойство ReverseFqdn для ресурса PublicIpAddress можно указать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c868a-123">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="c868a-124">DNS-имя для ресурса PublicIpAddress — contosoapp1.northus.cloudapp.azure.com;</span><span class="sxs-lookup"><span data-stu-id="c868a-124">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="c868a-125">DNS-имя для другого ресурса PublicIpAddress в той же подписке — contosoapp2.westus.cloudapp.azure.com;</span><span class="sxs-lookup"><span data-stu-id="c868a-125">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="c868a-126">личное DNS-имя — app1.contoso.com при условии, что это имя *сначала* настроено как CNAME для contosoapp1.northus.cloudapp.azure.com или другого ресурса PublicIpAddress в той же подписке;</span><span class="sxs-lookup"><span data-stu-id="c868a-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="c868a-127">личное DNS-имя — app1.contoso.com при условии, что это имя *сначала* настроено как запись A для IP-адреса 23.96.52.53 или IP-адреса другого ресурса PublicIpAddress в той же подписке.</span><span class="sxs-lookup"><span data-stu-id="c868a-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="c868a-128">Те же ограничения применяются к обратной зоне DNS для облачных служб.</span><span class="sxs-lookup"><span data-stu-id="c868a-128">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="c868a-129">Обратная зона DNS для ресурсов PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c868a-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="c868a-130">Этот раздел содержит подробные инструкции по настройке обратной зоны DNS для ресурсов PublicIpAddress в модели развертывания Resource Manager с помощью Azure PowerShell, Azure CLI 1.0 или Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c868a-130">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="c868a-131">Настроить обратную зону DNS для ресурсов PublicIpAddres на портале Azure пока нельзя.</span><span class="sxs-lookup"><span data-stu-id="c868a-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="c868a-132">Сейчас Azure поддерживает обратную зону DNS только для IPv4-ресурсов PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="c868a-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="c868a-133">Для IPv6 эта возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c868a-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="c868a-134">Добавление обратной зоны DNS в существующий ресурс PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c868a-134">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="c868a-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c868a-135">PowerShell</span></span>

<span data-ttu-id="c868a-136">Чтобы добавить обратную зону DNS в существующий ресурс PublicIpAddress, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="c868a-137">Чтобы добавить обратную зону DNS в существующий ресурс PublicIpAddress, у которого еще нет DNS-имени, необходимо указать DNS-имя:</span><span class="sxs-lookup"><span data-stu-id="c868a-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="c868a-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c868a-138">Azure CLI 1.0</span></span>

<span data-ttu-id="c868a-139">Чтобы добавить обратную зону DNS в существующий ресурс PublicIpAddress, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="c868a-140">Чтобы добавить обратную зону DNS в существующий ресурс PublicIpAddress, у которого еще нет DNS-имени, необходимо указать DNS-имя:</span><span class="sxs-lookup"><span data-stu-id="c868a-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="c868a-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c868a-141">Azure CLI 2.0</span></span>

<span data-ttu-id="c868a-142">Чтобы добавить обратную зону DNS в существующий ресурс PublicIpAddress, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-142">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="c868a-143">Чтобы добавить обратную зону DNS в существующий ресурс PublicIpAddress, у которого еще нет DNS-имени, необходимо указать DNS-имя:</span><span class="sxs-lookup"><span data-stu-id="c868a-143">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="c868a-144">Создание общедоступного IP-адреса с обратной зоной DNS</span><span class="sxs-lookup"><span data-stu-id="c868a-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="c868a-145">Чтобы создать ресурс PublicIpAddress с уже указанным свойством обратной зоны DNS, выполните указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="c868a-145">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="c868a-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c868a-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="c868a-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c868a-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="c868a-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c868a-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="c868a-149">Просмотр обратной зоны DNS в существующем ресурсе PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="c868a-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="c868a-150">Чтобы просмотреть настроенное значение в существующем ресурсе PublicIpAddress, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-150">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="c868a-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c868a-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="c868a-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c868a-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="c868a-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c868a-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="c868a-154">Удаление обратной зоны DNS из существующих общедоступных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="c868a-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="c868a-155">Чтобы удалить свойство обратной зоны DNS из существующего ресурса PublicIpAddress, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-155">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="c868a-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c868a-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="c868a-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c868a-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="c868a-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c868a-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="c868a-159">Настройка обратной зоны DNS для облачных служб</span><span class="sxs-lookup"><span data-stu-id="c868a-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="c868a-160">Этот раздел содержит подробные инструкции по настройке обратной зоны DNS для облачных служб в классической модели развертывания с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c868a-160">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="c868a-161">Настройка обратной зоны DNS для облачных служб с помощью портала Azure, Azure CLI 1.0 и Azure CLI 2.0 не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c868a-161">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="c868a-162">Добавление обратной зоны DNS в существующие облачные службы</span><span class="sxs-lookup"><span data-stu-id="c868a-162">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="c868a-163">Чтобы добавить обратную зону DNS в существующую облачную службу, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-163">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="c868a-164">Создание облачной службы с обратной зоной DNS</span><span class="sxs-lookup"><span data-stu-id="c868a-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="c868a-165">Чтобы создать облачную службу с уже указанным свойством обратной зоны DNS, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-165">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="c868a-166">Просмотр обратной зоны DNS в существующих облачных службах</span><span class="sxs-lookup"><span data-stu-id="c868a-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="c868a-167">Чтобы просмотреть свойство обратной зоны DNS для существующей облачной службы, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-167">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="c868a-168">Удаление обратной зоны DNS из существующих облачных служб</span><span class="sxs-lookup"><span data-stu-id="c868a-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="c868a-169">Чтобы удалить свойство обратной зоны DNS из существующей облачной службы, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c868a-169">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="c868a-170">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="c868a-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="c868a-171">Сколько стоит обратная зона DNS?</span><span class="sxs-lookup"><span data-stu-id="c868a-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="c868a-172">Она бесплатна!</span><span class="sxs-lookup"><span data-stu-id="c868a-172">They're free!</span></span>  <span data-ttu-id="c868a-173">Никакие дополнительные затраты на записи или запросы обратной зоны DNS не требуются.</span><span class="sxs-lookup"><span data-stu-id="c868a-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="c868a-174">Будут ли мои записи обратной зоны DNS разрешаться из Интернета?</span><span class="sxs-lookup"><span data-stu-id="c868a-174">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="c868a-175">Да.</span><span class="sxs-lookup"><span data-stu-id="c868a-175">Yes.</span></span> <span data-ttu-id="c868a-176">После того, как вы укажете свойство обратной зоны DNS для своей службы Azure, облако Azure возьмет на себя управление зонами DNS и всеми операциями делегирования DNS, необходимыми для того, чтобы запись обратной зоны DNS разрешалась для всех интернет-пользователей.</span><span class="sxs-lookup"><span data-stu-id="c868a-176">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="c868a-177">Создаются ли для моих служб Azure какие-то стандартные записи обратной зоны DNS?</span><span class="sxs-lookup"><span data-stu-id="c868a-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="c868a-178">Нет.</span><span class="sxs-lookup"><span data-stu-id="c868a-178">No.</span></span> <span data-ttu-id="c868a-179">Обратная зона DNS — это подключаемая возможность.</span><span class="sxs-lookup"><span data-stu-id="c868a-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="c868a-180">Если вы не захотите настраивать записи обратной зоны DNS, они не будут создаваться по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c868a-180">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="c868a-181">Каков формат полного доменного имени (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="c868a-181">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="c868a-182">Полные доменные имена указываются в прямом порядке и должны завершаться точкой (например, app1.contoso.com.).</span><span class="sxs-lookup"><span data-stu-id="c868a-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="c868a-183">Что произойдет, если при проверке указанной мной записи обратной зоны DNS произойдет ошибка?</span><span class="sxs-lookup"><span data-stu-id="c868a-183">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="c868a-184">Если при проверке обратной зоны DNS происходит ошибка, настройка записи обратной зоны DNS завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="c868a-184">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="c868a-185">В этом случае исправьте значение обратной зоны DNS и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="c868a-185">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="c868a-186">Можно ли настроить обратную зону DNS для службы приложений Azure?</span><span class="sxs-lookup"><span data-stu-id="c868a-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="c868a-187">Нет.</span><span class="sxs-lookup"><span data-stu-id="c868a-187">No.</span></span> <span data-ttu-id="c868a-188">Служба приложений Azure не поддерживает обратную зону DNS.</span><span class="sxs-lookup"><span data-stu-id="c868a-188">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="c868a-189">Можно ли настроить несколько записей обратной зоны DNS для моей службы Azure?</span><span class="sxs-lookup"><span data-stu-id="c868a-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="c868a-190">Нет.</span><span class="sxs-lookup"><span data-stu-id="c868a-190">No.</span></span> <span data-ttu-id="c868a-191">В Azure поддерживается только одна запись обратной зоны DNS для каждой облачной службы Azure или каждого ресурса PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="c868a-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="c868a-192">Можно ли настроить обратную зону DNS для IPv6-ресурсов PublicIpAddress?</span><span class="sxs-lookup"><span data-stu-id="c868a-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="c868a-193">Нет.</span><span class="sxs-lookup"><span data-stu-id="c868a-193">No.</span></span> <span data-ttu-id="c868a-194">Сейчас Azure поддерживает обратную зону DNS только для облачных служб и IPv4-ресурсов PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="c868a-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="c868a-195">Можно ли отправлять электронные сообщения во внешние домены из служб вычислений Azure?</span><span class="sxs-lookup"><span data-stu-id="c868a-195">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="c868a-196">Нет.</span><span class="sxs-lookup"><span data-stu-id="c868a-196">No.</span></span> <span data-ttu-id="c868a-197">[Службы вычислений Azure не поддерживают отправку сообщений электронной почты на внешние домены](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/).</span><span class="sxs-lookup"><span data-stu-id="c868a-197">[Azure Compute services do not support sending emails to external domains](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c868a-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c868a-198">Next steps</span></span>

<span data-ttu-id="c868a-199">Дополнительные сведения см. [в статье Википедии об обратном просмотре DNS](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="c868a-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="c868a-200">Узнайте, как [разместить зону обратного просмотра для диапазона IP-адресов, присвоенного поставщиком услуг Интернета, в службе Azure DNS](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="c868a-200">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

