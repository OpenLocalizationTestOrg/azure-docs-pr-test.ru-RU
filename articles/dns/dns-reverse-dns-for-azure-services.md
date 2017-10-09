---
title: "aaaReverse DNS для служб Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure обратный просмотр DNS для служб, размещенных в Azure"
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="0451e-103">Настройка обратного просмотра DNS для размещенных в Azure служб</span><span class="sxs-lookup"><span data-stu-id="0451e-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="0451e-104">В этой статье объясняется, как tooconfigure обратный просмотр DNS для служб, размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="0451e-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="0451e-105">Службы в Azure используют IP-адреса, присвоенные им службой Azure и являющиеся собственностью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0451e-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="0451e-106">Эти обратной записи DNS (PTR-записей) должны создаваться в hello соответствующего корпорации Майкрософт зоны обратного просмотра DNS уточняющего запроса.</span><span class="sxs-lookup"><span data-stu-id="0451e-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="0451e-107">В этой статье объясняется, как toodo это.</span><span class="sxs-lookup"><span data-stu-id="0451e-107">This article explains how toodo this.</span></span>

<span data-ttu-id="0451e-108">Этот сценарий не следует путать с возможностью hello слишком[размещения hello зоны обратного просмотра DNS подстановки для назначенных диапазонов IP-в Azure DNS](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="0451e-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="0451e-109">В этом случае hello диапазоны IP-адресов, представленный зоны обратного просмотра hello должны быть назначены организации tooyour обычно поставщиком услуг Интернета.</span><span class="sxs-lookup"><span data-stu-id="0451e-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="0451e-110">Перед прочтением этой статьи ознакомьтесь со статьей [Основные сведения об обратной зоне DNS и ее поддержке в Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0451e-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="0451e-111">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0451e-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="0451e-112">В модели развертывания диспетчера ресурсов hello вычислительных ресурсов (например, виртуальные машины, наборы масштабирования виртуальных машин или кластеров Service Fabric) предоставляются через ресурсов PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="0451e-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="0451e-113">Обратный поиск DNS настраиваются с помощью свойства «ReverseFqdn» hello hello PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="0451e-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="0451e-114">В hello классической модели развертывания вычислительные ресурсы предоставляются с помощью облачных служб.</span><span class="sxs-lookup"><span data-stu-id="0451e-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="0451e-115">Обратный поиск DNS настраиваются с помощью свойства «ReverseDnsFqdn» hello hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="0451e-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="0451e-116">Обратного DNS для hello службе приложений Azure в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0451e-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="0451e-117">Проверка записей обратной зоны DNS</span><span class="sxs-lookup"><span data-stu-id="0451e-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="0451e-118">Сторонних производителей не должно быть возможности toocreate обратного DNS-записи для их доменов DNS tooyour сопоставления службы Azure.</span><span class="sxs-lookup"><span data-stu-id="0451e-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="0451e-119">tooprevent, Azure позволяет только создание hello обратную запись DNS, где — имя домена, указанное в записи DNS обратного hello hello таким же, как или автоматически преобразуется в hello DNS-имя или IP-адрес PublicIpAddress или облачной службы в hello же подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="0451e-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="0451e-120">Эта проверка выполняется только при установке или изменить hello обратную запись DNS.</span><span class="sxs-lookup"><span data-stu-id="0451e-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="0451e-121">Периодическая повторная проверка не выполняется.</span><span class="sxs-lookup"><span data-stu-id="0451e-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="0451e-122">Пример: предположим, что hello PublicIpAddress ресурсов имеет имя contosoapp1.northus.cloudapp.azure.com hello DNS и IP-адрес 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="0451e-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="0451e-123">Hello ReverseFqdn hello PublicIpAddress могут быть указаны как:</span><span class="sxs-lookup"><span data-stu-id="0451e-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="0451e-124">имя DNS Hello hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="0451e-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="0451e-125">Hello DNS-имен для разных PublicIpAddress в hello же подписку, такую как contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="0451e-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="0451e-126">Именного DNS-имен, например app1.contoso.com, при условии, что это имя является *первый* настроен в качестве CNAME toocontosoapp1.northus.cloudapp.azure.com или tooa другой PublicIpAddress в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="0451e-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="0451e-127">Именного DNS-имен, например app1.contoso.com, при условии, что это имя является *первый* настроен в качестве значения записи toohello IP-адрес 23.96.52.53 или toohello IP-адрес другой PublicIpAddress в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="0451e-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="0451e-128">Hello и те же ограничения применяются tooreverse DNS для облачных служб.</span><span class="sxs-lookup"><span data-stu-id="0451e-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="0451e-129">Обратная зона DNS для ресурсов PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0451e-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="0451e-130">В этом разделе приведены подробные инструкции как tooconfigure обратный поиск DNS для ресурсов PublicIpAddress в модели развертывания диспетчера ресурсов hello, с помощью Azure PowerShell, CLI Azure 1.0 или Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0451e-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="0451e-131">Настройка обратного DNS для ресурсов PublicIpAddress не поддерживается в настоящее время через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0451e-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="0451e-132">Сейчас Azure поддерживает обратную зону DNS только для IPv4-ресурсов PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="0451e-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="0451e-133">Для IPv6 эта возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0451e-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="0451e-134">Добавление обратного tooan DNS существующих общедоступных</span><span class="sxs-lookup"><span data-stu-id="0451e-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="0451e-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0451e-135">PowerShell</span></span>

<span data-ttu-id="0451e-136">tooadd существующие PublicIpAddress обратного tooan DNS:</span><span class="sxs-lookup"><span data-stu-id="0451e-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="0451e-137">tooadd обратную DNS tooan существующие PublicIpAddress, в котором еще нет DNS-имя, необходимо также указать DNS-имя:</span><span class="sxs-lookup"><span data-stu-id="0451e-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0451e-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0451e-138">Azure CLI 1.0</span></span>

<span data-ttu-id="0451e-139">tooadd существующие PublicIpAddress обратного tooan DNS:</span><span class="sxs-lookup"><span data-stu-id="0451e-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="0451e-140">tooadd обратную DNS tooan существующие PublicIpAddress, в котором еще нет DNS-имя, необходимо также указать DNS-имя:</span><span class="sxs-lookup"><span data-stu-id="0451e-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0451e-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0451e-141">Azure CLI 2.0</span></span>

<span data-ttu-id="0451e-142">tooadd существующие PublicIpAddress обратного tooan DNS:</span><span class="sxs-lookup"><span data-stu-id="0451e-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="0451e-143">tooadd обратную DNS tooan существующие PublicIpAddress, в котором еще нет DNS-имя, необходимо также указать DNS-имя:</span><span class="sxs-lookup"><span data-stu-id="0451e-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="0451e-144">Создание общедоступного IP-адреса с обратной зоной DNS</span><span class="sxs-lookup"><span data-stu-id="0451e-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="0451e-145">toocreate новый PublicIpAddress с hello свойство обратного DNS уже задан:</span><span class="sxs-lookup"><span data-stu-id="0451e-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0451e-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0451e-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0451e-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0451e-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0451e-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0451e-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="0451e-149">Просмотр обратной зоны DNS в существующем ресурсе PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0451e-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="0451e-150">tooview hello значение, настроенное для существующего PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="0451e-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0451e-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0451e-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0451e-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0451e-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0451e-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0451e-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="0451e-154">Удаление обратной зоны DNS из существующих общедоступных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="0451e-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="0451e-155">tooremove обратного DNS свойство из существующего PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="0451e-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="0451e-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0451e-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="0451e-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0451e-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="0451e-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0451e-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="0451e-159">Настройка обратной зоны DNS для облачных служб</span><span class="sxs-lookup"><span data-stu-id="0451e-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="0451e-160">В этом разделе приведены подробные инструкции как tooconfigure обратный поиск DNS для облачных служб в hello классической модели развертывания с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0451e-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="0451e-161">Настройка обратного DNS для облачных служб не поддерживается через hello портал Azure, Azure CLI 1.0 или Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0451e-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="0451e-162">Добавление обратного DNS tooexisting облачные службы</span><span class="sxs-lookup"><span data-stu-id="0451e-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="0451e-163">tooadd обратного DNS записи tooan существующей облачной службы:</span><span class="sxs-lookup"><span data-stu-id="0451e-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="0451e-164">Создание облачной службы с обратной зоной DNS</span><span class="sxs-lookup"><span data-stu-id="0451e-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="0451e-165">toocreate новую облачную службу с hello свойство обратного DNS уже задан:</span><span class="sxs-lookup"><span data-stu-id="0451e-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="0451e-166">Просмотр обратной зоны DNS в существующих облачных службах</span><span class="sxs-lookup"><span data-stu-id="0451e-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="0451e-167">tooview hello обратного DNS свойство для существующей облачной службы:</span><span class="sxs-lookup"><span data-stu-id="0451e-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="0451e-168">Удаление обратной зоны DNS из существующих облачных служб</span><span class="sxs-lookup"><span data-stu-id="0451e-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="0451e-169">tooremove обратного DNS свойства из существующей облачной службы:</span><span class="sxs-lookup"><span data-stu-id="0451e-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="0451e-170">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="0451e-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="0451e-171">Сколько стоит обратная зона DNS?</span><span class="sxs-lookup"><span data-stu-id="0451e-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="0451e-172">Она бесплатна!</span><span class="sxs-lookup"><span data-stu-id="0451e-172">They're free!</span></span>  <span data-ttu-id="0451e-173">Никакие дополнительные затраты на записи или запросы обратной зоны DNS не требуются.</span><span class="sxs-lookup"><span data-stu-id="0451e-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="0451e-174">Будет Мой обратной записи разрешения DNS из hello Интернет?</span><span class="sxs-lookup"><span data-stu-id="0451e-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="0451e-175">Да.</span><span class="sxs-lookup"><span data-stu-id="0451e-175">Yes.</span></span> <span data-ttu-id="0451e-176">После свойство hello обратного DNS для службы Azure, Azure управляет всем делегирования DNS hello и зон DNS требуемые разрешает tooensure, обратная запись DNS для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="0451e-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="0451e-177">Создаются ли для моих служб Azure какие-то стандартные записи обратной зоны DNS?</span><span class="sxs-lookup"><span data-stu-id="0451e-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="0451e-178">Нет.</span><span class="sxs-lookup"><span data-stu-id="0451e-178">No.</span></span> <span data-ttu-id="0451e-179">Обратная зона DNS — это подключаемая возможность.</span><span class="sxs-lookup"><span data-stu-id="0451e-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="0451e-180">По умолчанию создаются обратной записи DNS, при выборе не tooconfigure их.</span><span class="sxs-lookup"><span data-stu-id="0451e-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="0451e-181">Что такое формат hello hello полное доменное имя (FQDN)</span><span class="sxs-lookup"><span data-stu-id="0451e-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="0451e-182">Полные доменные имена указываются в прямом порядке и должны завершаться точкой (например, app1.contoso.com.).</span><span class="sxs-lookup"><span data-stu-id="0451e-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="0451e-183">Что произойдет, если проверка hello для hello обратный поиск DNS, я указал завершается ошибкой?</span><span class="sxs-lookup"><span data-stu-id="0451e-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="0451e-184">Где hello обратного DNS неудачной проверки hello операции tooconfigure hello обратную запись DNS не выполняется.</span><span class="sxs-lookup"><span data-stu-id="0451e-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="0451e-185">Исправьте значение обратного DNS hello при необходимости и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="0451e-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="0451e-186">Можно ли настроить обратную зону DNS для службы приложений Azure?</span><span class="sxs-lookup"><span data-stu-id="0451e-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="0451e-187">Нет.</span><span class="sxs-lookup"><span data-stu-id="0451e-187">No.</span></span> <span data-ttu-id="0451e-188">Обратного DNS не поддерживается для hello службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="0451e-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="0451e-189">Можно ли настроить несколько записей обратной зоны DNS для моей службы Azure?</span><span class="sxs-lookup"><span data-stu-id="0451e-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="0451e-190">Нет.</span><span class="sxs-lookup"><span data-stu-id="0451e-190">No.</span></span> <span data-ttu-id="0451e-191">В Azure поддерживается только одна запись обратной зоны DNS для каждой облачной службы Azure или каждого ресурса PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="0451e-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="0451e-192">Можно ли настроить обратную зону DNS для IPv6-ресурсов PublicIpAddress?</span><span class="sxs-lookup"><span data-stu-id="0451e-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="0451e-193">Нет.</span><span class="sxs-lookup"><span data-stu-id="0451e-193">No.</span></span> <span data-ttu-id="0451e-194">Сейчас Azure поддерживает обратную зону DNS только для облачных служб и IPv4-ресурсов PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="0451e-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="0451e-195">Можно отправлять сообщения электронной почты tooexternal домены из службы вычислений Azure?</span><span class="sxs-lookup"><span data-stu-id="0451e-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="0451e-196">Нет.</span><span class="sxs-lookup"><span data-stu-id="0451e-196">No.</span></span> [<span data-ttu-id="0451e-197">Службы вычислений Azure не поддерживают отправку сообщений электронной почты tooexternal доменов</span><span class="sxs-lookup"><span data-stu-id="0451e-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="0451e-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0451e-198">Next steps</span></span>

<span data-ttu-id="0451e-199">Дополнительные сведения см. [в статье Википедии об обратном просмотре DNS](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="0451e-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="0451e-200">Узнайте, каким образом слишком[зоны обратного просмотра hello узла для диапазона IP, назначенной поставщика услуг Интернета в Azure DNS](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="0451e-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

