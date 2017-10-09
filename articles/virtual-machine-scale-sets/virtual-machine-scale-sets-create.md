---
title: "набор масштабирования виртуальной машины Azure aaaCreate | Документы Microsoft"
description: "Создание и развертывание масштабируемого набора виртуальных машин Linux или Windows в Azure с помощью Azure CLI, PowerShell, шаблона или Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="d4ce7-103">Создание и развертывание масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d4ce7-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="d4ce7-104">Наборы масштабирования виртуальных машин упростить для вас toodeploy идентичные виртуальных машин и управление как набор.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="d4ce7-105">Масштабируемые наборы обеспечивают высокую степень масштабируемости и персонализацию уровня вычислений для гипермасштабируемых приложений. Кроме того, они поддерживают образы платформ Windows и Linux, а также пользовательские образы и расширения.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="d4ce7-106">Дополнительные сведения о масштабируемых наборах см. в разделе [Общие сведения о масштабируемых наборах виртуальных машин в Azure](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="d4ce7-107">В этом учебнике показано, как toocreate набора масштабирования виртуальных машин **без** с помощью портала Azure "hello".</span><span class="sxs-lookup"><span data-stu-id="d4ce7-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="d4ce7-108">Сведения о как toouse hello портала Azure см. в разделе [как toocreate набора масштабирования виртуальных машин с портала Azure hello](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="d4ce7-109">Дополнительные сведения о ресурсах Azure Resource Manager см. в статье [Развертывание с помощью Azure Resource Manager и классическое развертывание: сведения о моделях развертывания и состоянии ресурсов](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="d4ce7-110">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="d4ce7-110">Sign in tooAzure</span></span>

<span data-ttu-id="d4ce7-111">Если вы используете Azure CLI 2.0 или Azure PowerShell toocreate шкалу задано, необходимо сначала toosign в tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="d4ce7-112">Дополнительные сведения о статье tooinstall, настроить и войдите в tooAzure с помощью Azure CLI или PowerShell, [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) или [приступить к работе с помощью командлетов Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="d4ce7-113">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4ce7-113">Create a resource group</span></span>

<span data-ttu-id="d4ce7-114">Необходимо сначала toocreate группы ресурсов, набора масштабирования виртуальных машин hello с которым связан.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="d4ce7-115">Создание с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d4ce7-115">Create from Azure CLI</span></span>

<span data-ttu-id="d4ce7-116">Создать масштабируемый набор виртуальных машин с помощью Azure CLI достаточно просто.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="d4ce7-117">Если не указать значения по умолчанию, они будут заданы автоматически.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="d4ce7-118">Например, если не указать данные виртуальной сети, она будет создана автоматически.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="d4ce7-119">При отсутствии hello следующие элементы, они создаются:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="d4ce7-120">подсистема балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="d4ce7-120">A load balancer</span></span>
- <span data-ttu-id="d4ce7-121">виртуальную сеть;</span><span class="sxs-lookup"><span data-stu-id="d4ce7-121">A virtual network</span></span>
- <span data-ttu-id="d4ce7-122">общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-122">A public IP address</span></span>

<span data-ttu-id="d4ce7-123">При выборе hello образ виртуальной машины, которые должны toouse на hello набора масштабирования виртуальных машин, у вас есть несколько вариантов:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="d4ce7-124">URN</span><span class="sxs-lookup"><span data-stu-id="d4ce7-124">URN</span></span>  
<span data-ttu-id="d4ce7-125">Идентификатор ресурса Hello:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="d4ce7-126">**Win2012R2Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="d4ce7-127">Псевдоним URN</span><span class="sxs-lookup"><span data-stu-id="d4ce7-127">URN alias</span></span>  
<span data-ttu-id="d4ce7-128">Hello понятное имя универсального имени ресурса:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="d4ce7-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="d4ce7-130">Идентификатор настраиваемого ресурса</span><span class="sxs-lookup"><span data-stu-id="d4ce7-130">Custom resource id</span></span>  
<span data-ttu-id="d4ce7-131">tooan путь Hello ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="d4ce7-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="d4ce7-133">Веб-ресурс</span><span class="sxs-lookup"><span data-stu-id="d4ce7-133">Web resource</span></span>  
<span data-ttu-id="d4ce7-134">Hello tooan пути HTTP URI:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="d4ce7-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="d4ce7-136">Список доступных образов можно получить с помощью команды `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="d4ce7-137">набор масштабирования виртуальных машин toocreate, необходимо указать следующие hello:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="d4ce7-138">Группа ресурсов</span><span class="sxs-lookup"><span data-stu-id="d4ce7-138">Resource group</span></span> 
- <span data-ttu-id="d4ce7-139">Имя</span><span class="sxs-lookup"><span data-stu-id="d4ce7-139">Name</span></span>
- <span data-ttu-id="d4ce7-140">образ операционной системы;</span><span class="sxs-lookup"><span data-stu-id="d4ce7-140">Operating system image</span></span>
- <span data-ttu-id="d4ce7-141">данные аутентификации.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-141">Authentication information</span></span> 
 
<span data-ttu-id="d4ce7-142">Следующий пример Hello создает базовый набор масштабирования виртуальной машины (этот шаг может занять несколько минут).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="d4ce7-143">После завершения выполнения команды hello теперь имеется шкала созданной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="d4ce7-144">IP-адрес tooget hello hello виртуальной машины может понадобиться, чтобы вы могли подключаться tooit.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="d4ce7-145">Вы можете получить множество различных сведений о виртуальной машине hello (включая hello IP-адрес) с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="d4ce7-146">Создание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4ce7-146">Create from PowerShell</span></span>

<span data-ttu-id="d4ce7-147">PowerShell — toouse сложнее, чем Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="d4ce7-148">Azure CLI предоставляет значения по умолчанию для сетевых ресурсов (таких как подсистемы балансировки нагрузки, IP-адреса и виртуальные сети), а PowerShell — нет.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="d4ce7-149">Также с помощью PowerShell немного сложнее указать образ.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="d4ce7-150">Изображения можно получать с hello следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="d4ce7-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="d4ce7-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="d4ce7-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="d4ce7-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="d4ce7-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="d4ce7-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="d4ce7-154">командлеты работают Hello можно направить в последовательности.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="d4ce7-155">Ниже приведен пример как tooget все образы для hello **Западная часть США 2** область с издателем с именем hello **microsoft** в нем.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="d4ce7-156">Hello рабочий процесс для создания набора масштабирования виртуальных машин выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="d4ce7-157">Создайте объект конфигурации, который содержит сведения о наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="d4ce7-158">Справочник по hello базовый образ ОС.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="d4ce7-159">Настройте параметры операционной системы hello: проверка подлинности, префикс имени виртуальной Машины и передача/пользователя.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="d4ce7-160">Настройте сеть.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-160">Configure networking.</span></span>
5. <span data-ttu-id="d4ce7-161">Создайте набор масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-161">Create hello scale set.</span></span>

<span data-ttu-id="d4ce7-162">В этом примере создается простой масштабируемый набор с двумя экземплярами для компьютера под управлением Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="d4ce7-163">Использование образов настраиваемой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d4ce7-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="d4ce7-164">При создании набора из собственного пользовательского изображения вместо ссылки на образ виртуальной машины из коллекции hello шкалы hello _AzureRmVmssStorageProfile набор_ команда будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d4ce7-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="d4ce7-165">Создание с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="d4ce7-165">Create from a template</span></span>

<span data-ttu-id="d4ce7-166">Вы можете развернуть масштабируемый набор виртуальных машин с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="d4ce7-167">Можно создать собственный шаблон или использовать один из hello [шаблон репозитория](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="d4ce7-168">Эти шаблоны можно развернуть напрямую tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="d4ce7-169">toocreate собственный шаблон, создайте файл JSON.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="d4ce7-170">Общие сведения о том, как toocreate и настройки шаблона см. в разделе [шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d4ce7-171">Пример шаблона доступен на [сайте GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="d4ce7-172">Дополнительные сведения о том, как отображается toocreate и использовать этот пример, [минимальный набор реальную масштабирования](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="d4ce7-173">Создание с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4ce7-173">Create from Visual Studio</span></span>

<span data-ttu-id="d4ce7-174">С помощью Visual Studio можно создать проект группы ресурсов Azure и добавить шаблон tooit набор масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="d4ce7-175">Можно выбрать, следует ли tooimport из GitHub или hello Azure коллекции веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="d4ce7-176">Кроме того, автоматически создается сценарий PowerShell для развертывания.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="d4ce7-177">Дополнительные сведения см. в разделе [как toocreate набора масштабирования виртуальных машин с помощью Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="d4ce7-178">Создать из hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d4ce7-178">Create from hello Azure portal</span></span>

<span data-ttu-id="d4ce7-179">Hello портал Azure предоставляет удобный способ tooquickly создания набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d4ce7-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="d4ce7-180">Дополнительные сведения см. в разделе [как toocreate набора масштабирования виртуальных машин с портала Azure hello](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4ce7-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4ce7-181">Next steps</span></span>

<span data-ttu-id="d4ce7-182">Узнайте больше о [дисках данных](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="d4ce7-183">Узнайте, каким образом слишком[управлять приложениями](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="d4ce7-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
