---
title: "шаблоны aaaNetworking для Azure Service Fabric | Документы Microsoft"
description: "Описывает общих сетевых шаблонов для службы структуры и как toocreate кластера с помощью Azure сетевые возможности."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="7ebab-103">Схемы сетевых подключений Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ebab-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="7ebab-104">Кластер Azure Service Fabric можно интегрировать с другими сетевыми компонентами Azure.</span><span class="sxs-lookup"><span data-stu-id="7ebab-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="7ebab-105">В этой статье мы покажем, как toocreate кластеры, hello используйте следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="7ebab-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- <span data-ttu-id="7ebab-106">[существующая виртуальная сеть или подсеть](#existingvnet);</span><span class="sxs-lookup"><span data-stu-id="7ebab-106">[Existing virtual network or subnet](#existingvnet)</span></span>
- <span data-ttu-id="7ebab-107">[статический общедоступный IP-адрес](#staticpublicip);</span><span class="sxs-lookup"><span data-stu-id="7ebab-107">[Static public IP address](#staticpublicip)</span></span>
- <span data-ttu-id="7ebab-108">[подсистема балансировки нагрузки только для внутреннего использования](#internallb);</span><span class="sxs-lookup"><span data-stu-id="7ebab-108">[Internal-only load balancer](#internallb)</span></span>
- <span data-ttu-id="7ebab-109">[внутренняя и внешняя подсистемы балансировки нагрузки](#internalexternallb).</span><span class="sxs-lookup"><span data-stu-id="7ebab-109">[Internal and external load balancer](#internalexternallb)</span></span>

<span data-ttu-id="7ebab-110">Service Fabric выполняется в стандартном масштабируемом наборе виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7ebab-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="7ebab-111">Любые функции, которые можно использовать в масштабируемом наборе виртуальных машин, можно также использовать и в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ebab-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="7ebab-112">разделы сети Hello hello шаблонов диспетчера ресурсов Azure для набора масштабирования виртуальной машины и службы структуры являются идентичными.</span><span class="sxs-lookup"><span data-stu-id="7ebab-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="7ebab-113">После развертывания tooan существующей виртуальной сети, он будет легко tooincorporate другие сетевые функции, такие как Azure ExpressRoute, шлюз VPN Azure, группы безопасности сети и виртуальную сеть пиринга.</span><span class="sxs-lookup"><span data-stu-id="7ebab-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="7ebab-114">Служба Service Fabric является уникальной среди других сетевых компонентов в одном аспекте.</span><span class="sxs-lookup"><span data-stu-id="7ebab-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="7ebab-115">Hello [портал Azure](https://portal.azure.com) внутренним образом использует hello Service Fabric toocall tooa кластера tooget информация о поставщике ресурсов о узлы и приложения.</span><span class="sxs-lookup"><span data-stu-id="7ebab-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="7ebab-116">поставщик ресурсов Hello Service Fabric требуется порт шлюза общедоступный входящий доступ toohello HTTP (порт 19080, по умолчанию) в конечной точке управления hello.</span><span class="sxs-lookup"><span data-stu-id="7ebab-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="7ebab-117">[Обозреватель Service Fabric](service-fabric-visualizing-your-cluster.md) использует hello toomanage конечной точки управления кластера.</span><span class="sxs-lookup"><span data-stu-id="7ebab-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="7ebab-118">поставщик ресурсов Hello Service Fabric также использует порт tooquery информация о кластере toodisplay в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7ebab-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="7ebab-119">Если порт 19080 не доступен из поставщика ресурсов Service Fabric hello, сообщение, например *узлы не найдены* появится на портала hello и отображается пустой список узла и приложения.</span><span class="sxs-lookup"><span data-stu-id="7ebab-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="7ebab-120">Если вы хотите toosee кластера в hello портал Azure, подсистема балансировки нагрузки, должен предоставлять общий IP-адрес и вашей группе безопасности сети должны разрешать входящий трафик порта 19080.</span><span class="sxs-lookup"><span data-stu-id="7ebab-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="7ebab-121">Если настройки не удовлетворяет этим требованиям, hello портал Azure не отображает hello состояния кластера.</span><span class="sxs-lookup"><span data-stu-id="7ebab-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="7ebab-122">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="7ebab-122">Templates</span></span>

<span data-ttu-id="7ebab-123">Все шаблоны Service Fabric находятся в [одном загружаемом файле](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="7ebab-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="7ebab-124">Должен быть доступ toodeploy hello шаблоны в качестве-с помощью следующих команд PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7ebab-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="7ebab-125">Если вы развертываете hello существующий шаблон виртуальной сети Azure или hello статического открытого шаблон IP-адреса, сначала прочтите hello [начальной установки](#initialsetup) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="7ebab-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="7ebab-126">Начальная настройка</span><span class="sxs-lookup"><span data-stu-id="7ebab-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="7ebab-127">Существующая виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="7ebab-127">Existing virtual network</span></span>

<span data-ttu-id="7ebab-128">В следующем примере hello, мы начнем с существующей виртуальной сети с именем ExistingRG виртуальной сети, в hello **ExistingRG** группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ebab-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="7ebab-129">подсети Hello совпадает с именем по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7ebab-129">hello subnet is named default.</span></span> <span data-ttu-id="7ebab-130">Эти ресурсы по умолчанию создаются при использовании hello Azure портала toocreate стандартной виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="7ebab-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="7ebab-131">Hello виртуальной сети и подсети можно создать без создания hello виртуальной Машины, но основной целью hello Добавление кластера tooan существующей виртуальной сети является tooother подключения tooprovide сети виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7ebab-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="7ebab-132">Создание hello виртуальной Машины дает хороший пример как обычно используется существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="7ebab-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="7ebab-133">Если кластер Service Fabric использует только внутренняя Подсистема балансировки нагрузки, без общедоступный IP-адрес можно использовать hello виртуальной Машины и ее общедоступный IP-адрес как безопасный *перехода поле*.</span><span class="sxs-lookup"><span data-stu-id="7ebab-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="7ebab-134">Статический общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="7ebab-134">Static public IP address</span></span>

<span data-ttu-id="7ebab-135">Как правило, статический общедоступный IP-адрес, выделенный ресурс, который управляется отдельно от hello виртуальных Машин или виртуальных машин, он назначен.</span><span class="sxs-lookup"><span data-stu-id="7ebab-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="7ebab-136">Он предоставляется в отдельная группа сетевых ресурсов (как противоположность tooin hello Service Fabric группы ресурсов кластера сам).</span><span class="sxs-lookup"><span data-stu-id="7ebab-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="7ebab-137">Создайте статический общедоступный IP-адрес, с именем staticIP1 в hello ExistingRG группе ресурсов, в hello портал Azure или с помощью PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7ebab-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="7ebab-138">Шаблон Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ebab-138">Service Fabric template</span></span>

<span data-ttu-id="7ebab-139">В примерах hello в этой статье мы используем template.json Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="7ebab-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="7ebab-140">Перед созданием кластера можно использовать шаблон hello toodownload hello стандартный мастер портала с портала hello.</span><span class="sxs-lookup"><span data-stu-id="7ebab-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="7ebab-141">Также можно использовать один из шаблонов hello в hello [коллекции шаблонов](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), такие как hello [пяти узел кластера Service Fabric](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="7ebab-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="7ebab-142">Существующая виртуальная сеть или подсеть</span><span class="sxs-lookup"><span data-stu-id="7ebab-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="7ebab-143">Измените имя параметра toohello hello подсети hello существующей подсети, а затем добавьте две новые параметры tooreference hello существующей виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="7ebab-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="7ebab-144">Изменение hello `vnetID` переменной toopoint toohello существующей виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="7ebab-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="7ebab-145">Удалите `Microsoft.Network/virtualNetworks` из ресурсов, чтобы платформа Azure не создала виртуальную сеть:</span><span class="sxs-lookup"><span data-stu-id="7ebab-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="7ebab-146">Закомментируйте hello виртуальной сети из hello `dependsOn` атрибут `Microsoft.Compute/virtualMachineScaleSets`, поэтому вы не зависят от создания новой виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="7ebab-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="7ebab-147">Развертывание шаблона hello:</span><span class="sxs-lookup"><span data-stu-id="7ebab-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="7ebab-148">После развертывания виртуальной сети должен включать набор hello новый масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7ebab-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="7ebab-149">Тип узла набора масштабирования виртуальной машины Hello должны показывать hello существующую виртуальную сеть и подсети.</span><span class="sxs-lookup"><span data-stu-id="7ebab-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="7ebab-150">Также можно использовать удаленного рабочего стола (RDP) tooaccess hello виртуальной Машины, которые была записаны в виртуальной сети hello и tooping hello новый профиль в наборе виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="7ebab-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="7ebab-151">Еще один пример см. в разделе [, не определенных tooService структуры](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="7ebab-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="7ebab-152">Статический общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="7ebab-152">Static public IP address</span></span>

1. <span data-ttu-id="7ebab-153">Добавьте параметры для hello имя hello существующие группы ресурсов статического IP, имя и полное доменное имя (FQDN):</span><span class="sxs-lookup"><span data-stu-id="7ebab-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="7ebab-154">Удалите hello `dnsName` параметра.</span><span class="sxs-lookup"><span data-stu-id="7ebab-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="7ebab-155">(hello статический IP-адрес уже имеется.)</span><span class="sxs-lookup"><span data-stu-id="7ebab-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="7ebab-156">Добавьте переменную tooreference hello существующий статический IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="7ebab-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="7ebab-157">Удалите `Microsoft.Network/publicIPAddresses` из ресурсов, чтобы платформа Azure не создала IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="7ebab-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="7ebab-158">Закомментируйте hello IP-адрес из hello `dependsOn` атрибут `Microsoft.Network/loadBalancers`, поэтому оно не зависит от создается новый IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="7ebab-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="7ebab-159">В hello `Microsoft.Network/loadBalancers` ресурсов, изменение hello `publicIPAddress` элемент `frontendIPConfigurations` tooreference hello существующий статический IP-адрес вместо только что созданной:</span><span class="sxs-lookup"><span data-stu-id="7ebab-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="7ebab-160">В hello `Microsoft.ServiceFabric/clusters` ресурсов, изменение `managementEndpoint` toohello полное доменное имя DNS hello статического IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7ebab-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="7ebab-161">При использовании безопасного кластера убедитесь, что вы изменили *http://* слишком*https://*.</span><span class="sxs-lookup"><span data-stu-id="7ebab-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="7ebab-162">(Обратите внимание, что этот шаг применяется только кластеры tooService структуры.</span><span class="sxs-lookup"><span data-stu-id="7ebab-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="7ebab-163">Если вы используете масштабируемый набор виртуальных машин, то пропустите этот шаг.)</span><span class="sxs-lookup"><span data-stu-id="7ebab-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="7ebab-164">Развертывание шаблона hello:</span><span class="sxs-lookup"><span data-stu-id="7ebab-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="7ebab-165">После развертывания, можно видеть, что Подсистема балансировки нагрузки привязанного toohello открытый статический IP-адрес из hello другой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7ebab-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="7ebab-166">Здравствуйте, конечная точка подключения клиента Service Fabric и [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) конечной точки toohello полное доменное имя DNS hello статического IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7ebab-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="7ebab-167">Подсистема балансировки нагрузки только для внутреннего использования</span><span class="sxs-lookup"><span data-stu-id="7ebab-167">Internal-only load balancer</span></span>

<span data-ttu-id="7ebab-168">Этот сценарий заменяет hello внешней подсистемы балансировки нагрузки в шаблоне Service Fabric по умолчанию hello подсистемы балансировки нагрузки только для внутреннего использования.</span><span class="sxs-lookup"><span data-stu-id="7ebab-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="7ebab-169">Влияет на hello портал Azure, для поставщика ресурсов Service Fabric hello предшествующий раздел hello см.</span><span class="sxs-lookup"><span data-stu-id="7ebab-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="7ebab-170">Удалите hello `dnsName` параметра.</span><span class="sxs-lookup"><span data-stu-id="7ebab-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="7ebab-171">(он не требуется).</span><span class="sxs-lookup"><span data-stu-id="7ebab-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="7ebab-172">При необходимости, если используется метод статического выделения, можно добавить параметр статического IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7ebab-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="7ebab-173">Если вы используете метод динамическое выделение, необязательно toodo этот шаг.</span><span class="sxs-lookup"><span data-stu-id="7ebab-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="7ebab-174">Удалите `Microsoft.Network/publicIPAddresses` из ресурсов, чтобы платформа Azure не создала IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="7ebab-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="7ebab-175">Удалите IP-адрес hello `dependsOn` атрибут `Microsoft.Network/loadBalancers`, поэтому оно не зависит от создается новый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="7ebab-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="7ebab-176">Добавить виртуальную сеть hello `dependsOn` атрибут, так как Подсистема балансировки нагрузки hello теперь зависит от подсети hello hello в виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="7ebab-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="7ebab-177">Изменить подсистему балансировки нагрузки hello `frontendIPConfigurations` настройки параметров с помощью `publicIPAddress`, toousing подсети и `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="7ebab-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="7ebab-178">`privateIPAddress` использует предварительно определенный статический внутренний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="7ebab-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="7ebab-179">toouse динамический IP-адрес, удалите hello `privateIPAddress` элемент, а затем измените `privateIPAllocationMethod` слишком**динамическое**.</span><span class="sxs-lookup"><span data-stu-id="7ebab-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="7ebab-180">В hello `Microsoft.ServiceFabric/clusters` ресурсов, изменение `managementEndpoint` адрес подсистемы балансировки нагрузки внутренней toohello toopoint.</span><span class="sxs-lookup"><span data-stu-id="7ebab-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="7ebab-181">При использовании безопасного кластера, убедитесь, что вы изменили *http://* слишком*https://*.</span><span class="sxs-lookup"><span data-stu-id="7ebab-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="7ebab-182">(Обратите внимание, что этот шаг применяется только кластеры tooService структуры.</span><span class="sxs-lookup"><span data-stu-id="7ebab-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="7ebab-183">Если вы используете масштабируемый набор виртуальных машин, то пропустите этот шаг.)</span><span class="sxs-lookup"><span data-stu-id="7ebab-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="7ebab-184">Развертывание шаблона hello:</span><span class="sxs-lookup"><span data-stu-id="7ebab-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="7ebab-185">После развертывания поддерживаемый подсистемой балансировки нагрузки использует hello 10.0.0.250 частного статического IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="7ebab-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="7ebab-186">Если имеется другой компьютер в этой же виртуальной сети, можно перейти toohello внутренней [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) конечной точки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="7ebab-187">Обратите внимание, что подключение выполняется tooone hello узлов за подсистемой балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="7ebab-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="7ebab-188">Внутренняя и внешняя подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="7ebab-188">Internal and external load balancer</span></span>

<span data-ttu-id="7ebab-189">В этом сценарии с hello существующих одним узлом тип внешней подсистемы балансировки нагрузки и добавить внутренний балансировщик нагрузки для hello того же типа узла.</span><span class="sxs-lookup"><span data-stu-id="7ebab-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="7ebab-190">Пул адресов серверной части tooa порту внутренней могут назначаться только балансировки нагрузки одного tooa.</span><span class="sxs-lookup"><span data-stu-id="7ebab-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="7ebab-191">Выберите, какая подсистема балансировки нагрузки будет управлять портами вашего приложения, а какая — конечными точками управления (порты 19000 и 19080).</span><span class="sxs-lookup"><span data-stu-id="7ebab-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="7ebab-192">Если конечные точки управления hello разместить на hello внутренней подсистемы балансировки нагрузки, имейте в виду hello ресурса службы фабрики поставщика ограничения, описанные в статье hello.</span><span class="sxs-lookup"><span data-stu-id="7ebab-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="7ebab-193">В примере hello мы используем конечные точки управления hello остаются на hello внешней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="7ebab-194">Можно также добавить порт 80 приложения порт и поместите его на hello внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="7ebab-195">В кластере типа узла двух один узел является на hello внешней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="7ebab-196">Hello узле такого типа является hello внутренний балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="7ebab-197">toouse типа узла два кластера, hello создать портал два узла типа в шаблоне (который поставляется с двумя подсистемы балансировки нагрузки), переключение hello второй нагрузки балансировки tooan внутренней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="7ebab-198">Дополнительные сведения см. в разделе hello [балансировки нагрузки только для внутреннего использования](#internallb) раздела.</span><span class="sxs-lookup"><span data-stu-id="7ebab-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="7ebab-199">Добавьте параметром IP-адреса подсистемы балансировки нагрузки статический внутренний hello.</span><span class="sxs-lookup"><span data-stu-id="7ebab-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="7ebab-200">(Заметки о связанных toousing динамический IP-адрес, см. в предыдущих разделах этой статьи.)</span><span class="sxs-lookup"><span data-stu-id="7ebab-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="7ebab-201">Добавьте параметр порта приложения 80.</span><span class="sxs-lookup"><span data-stu-id="7ebab-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="7ebab-202">tooadd внутренней версии существующих hello сети переменные, скопируйте и вставьте их и добавьте «-Int» toohello имя:</span><span class="sxs-lookup"><span data-stu-id="7ebab-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="7ebab-203">Если начать с шаблона создается портал hello, который использует приложение порт 80, шаблон портала по умолчанию hello добавляет AppPort1 (порт 80) на hello внешней подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="7ebab-204">В этом случае удалите AppPort1 из hello внешней подсистемы балансировки нагрузки `loadBalancingRules` и зондов, поэтому ее можно добавить toohello внутренняя Подсистема балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="7ebab-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="7ebab-205">Добавьте второй ресурс `Microsoft.Network/loadBalancers`.</span><span class="sxs-lookup"><span data-stu-id="7ebab-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="7ebab-206">Выглядит аналогично toohello внутренняя Подсистема балансировки нагрузки в hello [балансировки нагрузки только для внутреннего использования](#internallb) раздела, но использует hello «-Int» загрузить балансировки переменных и реализует только hello приложения порт 80.</span><span class="sxs-lookup"><span data-stu-id="7ebab-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="7ebab-207">При этом также удаляются `inboundNatPools`, конечные точки протокола удаленного рабочего СТОЛА tookeep на hello внешняя Подсистема балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="7ebab-208">Если вы хотите протокола удаленного рабочего СТОЛА на hello внутренней подсистемы балансировки нагрузки, переместите `inboundNatPools` из toothis подсистемы балансировки нагрузки hello внутренняя Подсистема балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="7ebab-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="7ebab-209">В `networkProfile` для hello `Microsoft.Compute/virtualMachineScaleSets` ресурсов, добавить пул внутренних адресов серверной части hello:</span><span class="sxs-lookup"><span data-stu-id="7ebab-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="7ebab-210">Развертывание шаблона hello:</span><span class="sxs-lookup"><span data-stu-id="7ebab-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="7ebab-211">После развертывания можно увидеть два подсистемы балансировки нагрузки в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7ebab-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="7ebab-212">При просмотре hello подсистемы балансировки нагрузки, вы увидите hello общедоступный IP-адрес и управления конечными точками (порты 19000 и 19080), назначенными toohello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="7ebab-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="7ebab-213">Также видно hello статического внутреннего IP адрес и приложения назначен конечной точки (порт 80) toohello внутренняя Подсистема балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="7ebab-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="7ebab-214">Использование подсистемы балансировки нагрузки hello того же набора масштабирования виртуальных машин пула серверной части.</span><span class="sxs-lookup"><span data-stu-id="7ebab-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ebab-215">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ebab-215">Next steps</span></span>
[<span data-ttu-id="7ebab-216">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="7ebab-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
