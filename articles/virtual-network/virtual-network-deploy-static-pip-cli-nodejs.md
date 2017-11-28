---
title: "aaaCreate виртуальную Машину с статический общедоступный IP-адрес - Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate ВМ с статических открытый IP адрес с помощью hello Azure командной строки (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3ee906b65735830757b455df00f9f8d4373be3dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-10"></a><span data-ttu-id="85e3c-103">Создайте виртуальную Машину с помощью hello Azure CLI 1.0 статический общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="85e3c-103">Create a VM with a static public IP address using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="85e3c-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="85e3c-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="85e3c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85e3c-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="85e3c-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="85e3c-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="85e3c-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="85e3c-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="85e3c-108">Шаблон</span><span class="sxs-lookup"><span data-stu-id="85e3c-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="85e3c-109">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="85e3c-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="85e3c-110">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="85e3c-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="85e3c-111">В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="85e3c-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

<span data-ttu-id="85e3c-112">Выполнить эту задачу с помощью hello Azure CLI 1.0 (Эта статья) или hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="85e3c-112">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> 

## <span data-ttu-id="85e3c-113"><a name = "create"></a>Шаг 1. Запуск скрипта</span><span class="sxs-lookup"><span data-stu-id="85e3c-113"><a name = "create"></a>Step 1 - Start your script</span></span>
<span data-ttu-id="85e3c-114">Вы можете загрузить hello bash полный сценарий [здесь](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="85e3c-114">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-cli.sh).</span></span> <span data-ttu-id="85e3c-115">Выполните следующие toowork действия toochange hello скрипта в среде hello.</span><span class="sxs-lookup"><span data-stu-id="85e3c-115">Complete hello following steps toochange hello script toowork in your environment:</span></span>

<span data-ttu-id="85e3c-116">Изменить значения hello hello следующих переменных на основе значений hello нужно toouse для развертывания.</span><span class="sxs-lookup"><span data-stu-id="85e3c-116">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="85e3c-117">Привет, выполнив сценарий toohello карты значения, используемые в этой статье:</span><span class="sxs-lookup"><span data-stu-id="85e3c-117">hello following values map toohello scenario used in this article:</span></span>

```azurecli
# Set variables for hello new resource group
rgName="IaaSStory"
location="westus"

# Set variables for VNet
vnetName="TestVNet"
vnetPrefix="192.168.0.0/16"
subnetName="FrontEnd"
subnetPrefix="192.168.1.0/24"

# Set variables for storage
stdStorageAccountName="iaasstorystorage"

# Set variables for VM
vmSize="Standard_A1"
diskSize=127
publisher="Canonical"
offer="UbuntuServer"
sku="14.04.2-LTS"
version="latest"
vmName="WEB1"
osDiskName="osdisk"
nicName="NICWEB1"
privateIPAddress="192.168.1.101"
username='adminuser'
password='adminP@ssw0rd'
pipName="PIPWEB1"
dnsName="iaasstoryws1"
```

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="85e3c-118">Шаг 2 — Создание hello необходимые ресурсы для виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="85e3c-118">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="85e3c-119">Перед созданием виртуальной Машины, необходимо группы ресурсов, виртуальной сети, открытый IP и Сетевых toobe используемые hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="85e3c-119">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="85e3c-120">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="85e3c-120">Create a new resource group.</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="85e3c-121">Создание hello виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="85e3c-121">Create hello VNet and subnet.</span></span>

    ```azurecli
    azure network vnet create --resource-group $rgName \
        --name $vnetName \
        --address-prefixes $vnetPrefix \
        --location $location
    azure network vnet subnet create --resource-group $rgName \
        --vnet-name $vnetName \
        --name $subnetName \
        --address-prefix $subnetPrefix
    ```

3. <span data-ttu-id="85e3c-122">Создайте открытый IP-ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="85e3c-122">Create hello public IP resource.</span></span>

    ```azurecli
    azure network public-ip create --resource-group $rgName \
        --name $pipName \
        --location $location \
        --allocation-method Static \
        --domain-name-label $dnsName
    ```

4. <span data-ttu-id="85e3c-123">Создайте hello сетевого интерфейса (NIC) для hello ВМ в подсети hello, созданная выше, с hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="85e3c-123">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="85e3c-124">Обратите внимание hello первый набор команд, используемых tooretrieve hello **идентификатор** hello подсети, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="85e3c-124">Notice hello first set of commands are used tooretrieve hello **Id** of hello subnet created above.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $rgName \
        --vnet-name $vnetName \
        --name $subnetName|grep Id)"

    subnetId=${subnetId#*/}

    azure network nic create --name $nicName \
        --resource-group $rgName \
        --location $location \
        --private-ip-address $privateIPAddress \
        --subnet-id $subnetId \
        --public-ip-name $pipName
    ```

   > [!TIP]
   > <span data-ttu-id="85e3c-125">Здравствуйте, первая команда выше используется [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) и [строка манипуляции](http://tldp.org/LDP/abs/html/string-manipulation.html) (в частности, подстроки удаления).</span><span class="sxs-lookup"><span data-stu-id="85e3c-125">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

5. <span data-ttu-id="85e3c-126">Создайте hello toohost учетной записи хранения диска ОС виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="85e3c-126">Create a storage account toohost hello VM OS drive.</span></span>

    ```azurecli
    azure storage account create $stdStorageAccountName \
        --resource-group $rgName \
        --location $location --type LRS
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="85e3c-127">Шаг 3 — Создание hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="85e3c-127">Step 3 - Create hello VM</span></span>
<span data-ttu-id="85e3c-128">Теперь, когда имеются все необходимые ресурсы, можно создать новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="85e3c-128">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="85e3c-129">Создайте hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="85e3c-129">Create hello VM.</span></span>

    ```azurecli
    azure vm create --resource-group $rgName \
        --name $vmName \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --nic-names $nicName \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $stdStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName.vhd \
        --admin-username $username \
        --admin-password $password
    ```
2. <span data-ttu-id="85e3c-130">Сохраните файл скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="85e3c-130">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="85e3c-131">Шаг 4. выполнение сценариев hello</span><span class="sxs-lookup"><span data-stu-id="85e3c-131">Step 4 - Run hello script</span></span>
<span data-ttu-id="85e3c-132">После внесения необходимых изменений и основные сведения о скрипте hello Показать выше, запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="85e3c-132">After making any necessary changes, and understanding hello script show above, run hello script.</span></span>

1. <span data-ttu-id="85e3c-133">С помощью консоли bash скрипт hello выше.</span><span class="sxs-lookup"><span data-stu-id="85e3c-133">From a bash console, run hello script above.</span></span>

    ```azurecli
    sh myscript.sh
    ```

2. <span data-ttu-id="85e3c-134">ниже Hello вывода должны отображаться через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="85e3c-134">hello output below should be displayed after a few minutes.</span></span>

        info:    Executing command group create
        info:    Getting resource group IaaSStory
        info:    Creating resource group IaaSStory
        info:    Created resource group IaaSStory
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
        data:    Name:                IaaSStory
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command network vnet create
        info:    Looking up virtual network "TestVNet"
        info:    Creating virtual network "TestVNet"
        info:    Loading virtual network state
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/TestVNet
        data:    Name                            : TestVNet
        data:    Type                            : Microsoft.Network/virtualNetworks
        data:    Location                        : westus
        data:    ProvisioningState               : Succeeded
        data:    Address prefixes:
        data:      192.168.0.0/16
        info:    network vnet create command OK
        info:    Executing command network vnet subnet create
        info:    Looking up hello subnet "FrontEnd"
        info:    Creating subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:
        info:    network vnet subnet create command OK
        info:    Executing command network public-ip create
        info:    Looking up hello public ip "PIPWEB1"
        info:    Creating public ip address "PIPWEB1"
        info:    Looking up hello public ip "PIPWEB1"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
        data:    Name                            : PIPWEB1
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Static
        data:    Idle timeout                    : 4
        data:    IP Address                      : 40.78.63.253
        data:    Domain name label               : iaasstoryws1
        data:    FQDN                            : iaasstoryws1.westus.cloudapp.azure.com
        info:    network public-ip create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICWEB1"
        info:    Looking up hello public ip "PIPWEB1"
        info:    Creating network interface "NICWEB1"
        info:    Looking up hello network interface "NICWEB1"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkInterfaces/NICWEB1
        data:    Name                            : NICWEB1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory2/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "WEB1"
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account iaasstorystorage
        info:    Looking up hello NIC "NICWEB1"
        info:    Creating VM "WEB1"
        info:    vm create command OK
