---
title: "aaaHow toocreate образов виртуальных Машин Windows Azure с Packer | Документы Microsoft"
description: "Узнайте, как toouse Packer toocreate образы виртуальных машинах в Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: d310fae3becb453b52d21281cb8ac53fa14a3fc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="08179-103">Как на виртуальной машине Windows toouse Packer toocreate образы в Azure</span><span class="sxs-lookup"><span data-stu-id="08179-103">How toouse Packer toocreate Windows virtual machine images in Azure</span></span>
<span data-ttu-id="08179-104">Каждой виртуальной машины (VM) в Azure создается из образа, определяющего распространения Windows hello и версию операционной системы.</span><span class="sxs-lookup"><span data-stu-id="08179-104">Each virtual machine (VM) in Azure is created from an image that defines hello Windows distribution and OS version.</span></span> <span data-ttu-id="08179-105">Образы могут содержать предварительно установленные приложения и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="08179-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="08179-106">Hello Azure Marketplace предоставляет большое количество изображений первый и сторонних разработчиков для наиболее распространенных операционной системы и приложений, или можно создать потребностями tooyour специально созданных пользовательских образов.</span><span class="sxs-lookup"><span data-stu-id="08179-106">hello Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="08179-107">В этой статье описаны как toouse Привет открыть инструмент источника [Packer](https://www.packer.io/) toodefine и построения пользовательских образов в Azure.</span><span class="sxs-lookup"><span data-stu-id="08179-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="08179-108">Создание группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="08179-108">Create Azure resource group</span></span>
<span data-ttu-id="08179-109">Во время сборки hello Packer создает временные ресурсы Azure, при построении hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08179-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="08179-110">toocapture, исходной виртуальной Машины для использования в качестве образа, необходимо определить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="08179-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="08179-111">Hello выходные данные процесса сборки hello Packer хранится в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="08179-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="08179-112">Создайте группу ресурсов с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="08179-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="08179-113">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="08179-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="08179-114">Создание учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="08179-114">Create Azure credentials</span></span>
<span data-ttu-id="08179-115">Packer выполняет проверку подлинности с помощью субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="08179-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="08179-116">Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Packer.</span><span class="sxs-lookup"><span data-stu-id="08179-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="08179-117">Управление и определить hello разрешения участника службы hello toowhat операции можно выполнять в Azure.</span><span class="sxs-lookup"><span data-stu-id="08179-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="08179-118">Создание службы с основной [New AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) и назначьте разрешения для участника toocreate hello службы и управление ресурсами с помощью [New AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="08179-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for hello service principal toocreate and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="08179-119">tooauthenticate tooAzure, необходимо также tooobtain вашей Azure ИД клиента и подписки с [Get AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="08179-119">tooauthenticate tooAzure, you also need tooobtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="08179-120">Эти два ИД используется в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="08179-120">You use these two IDs in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="08179-121">Определение шаблона Packer</span><span class="sxs-lookup"><span data-stu-id="08179-121">Define Packer template</span></span>
<span data-ttu-id="08179-122">toobuild изображения, нужно создать шаблон в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="08179-122">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="08179-123">В шаблоне hello определения построители и provisioners, выполняющих hello фактический процесс построения.</span><span class="sxs-lookup"><span data-stu-id="08179-123">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="08179-124">Имеет packer [средство подготовки для Azure](https://www.packer.io/docs/builders/azure.html) , позволяющий toodefine Azure ресурсы, такие как службы основной hello учетных данных, созданных в предыдущих шага hello.</span><span class="sxs-lookup"><span data-stu-id="08179-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="08179-125">Создайте файл с именем *windows.json* и вставить hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="08179-125">Create a file named *windows.json* and paste hello following content.</span></span> <span data-ttu-id="08179-126">Ввести собственные значения для следующего hello:</span><span class="sxs-lookup"><span data-stu-id="08179-126">Enter your own values for hello following:</span></span>

| <span data-ttu-id="08179-127">Параметр</span><span class="sxs-lookup"><span data-stu-id="08179-127">Parameter</span></span>                           | <span data-ttu-id="08179-128">Где tooobtain</span><span class="sxs-lookup"><span data-stu-id="08179-128">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="08179-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="08179-129">*client_id*</span></span>                         | <span data-ttu-id="08179-130">Просмотрите идентификатор субъекта-службы с помощью `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="08179-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="08179-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="08179-131">*client_secret*</span></span>                     | <span data-ttu-id="08179-132">Пароль, указанный в `$securePassword`</span><span class="sxs-lookup"><span data-stu-id="08179-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="08179-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="08179-133">*tenant_id*</span></span>                         | <span data-ttu-id="08179-134">Выходные данные команды `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="08179-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="08179-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="08179-135">*subscription_id*</span></span>                   | <span data-ttu-id="08179-136">Выходные данные команды `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="08179-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="08179-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="08179-137">*object_id*</span></span>                         | <span data-ttu-id="08179-138">Просмотрите идентификатор объекта субъекта-службы с помощью `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="08179-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="08179-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="08179-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="08179-140">Имя группы ресурсов, созданный на первом шаге hello</span><span class="sxs-lookup"><span data-stu-id="08179-140">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="08179-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="08179-141">*managed_image_name*</span></span>                | <span data-ttu-id="08179-142">Имя образа hello управляемого диска, который создается</span><span class="sxs-lookup"><span data-stu-id="08179-142">Name for hello managed disk image that is created</span></span> |

```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "0831b578-8ab6-40b9-a581-9a880a94aab1",
    "client_secret": "P@ssw0rd!",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
    "object_id": "a7dfb070-0d5b-47ac-b9a5-cf214fff0ae2",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Windows",
    "image_publisher": "MicrosoftWindowsServer",
    "image_offer": "WindowsServer",
    "image_sku": "2016-Datacenter",

    "communicator": "winrm",
    "winrm_use_ssl": "true",
    "winrm_insecure": "true",
    "winrm_timeout": "3m",
    "winrm_username": "packer",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "type": "powershell",
    "inline": [
      "Add-WindowsFeature Web-Server",
      "if( Test-Path $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml ){ rm $Env:SystemRoot\\windows\\system32\\Sysprep\\unattend.xml -Force}",
      "& $Env:SystemRoot\\System32\\Sysprep\\Sysprep.exe /oobe /generalize /shutdown /quiet"
    ]
  }]
}
```

<span data-ttu-id="08179-143">Этот шаблон создает виртуальную Машину Windows Server 2016, установка служб IIS, а затем обобщает hello виртуальной Машины с помощью средства Sysprep.</span><span class="sxs-lookup"><span data-stu-id="08179-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes hello VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="08179-144">Создание образа Packer</span><span class="sxs-lookup"><span data-stu-id="08179-144">Build Packer image</span></span>
<span data-ttu-id="08179-145">Если у вас еще нет Packer установлен на локальном компьютере, [следуйте инструкциям по установке hello Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="08179-145">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="08179-146">Для создания образа hello задайте вашей Packer файл шаблона следующим образом:</span><span class="sxs-lookup"><span data-stu-id="08179-146">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="08179-147">Пример выходных данных hello hello предшествующий команды выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="08179-147">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> task : Image deployment
==> azure-arm:  ->> dept : Engineering
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting hello certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM toobecome available...
==> azure-arm: Connected tooWinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-pq0mthtbtt/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> ComputeName       : ‘pkrvmpq0mthtbtt’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> Compute Name              : ‘pkrvmpq0mthtbtt’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="08179-148">Он занимает несколько минут для выполнения hello provisioners hello Packer toobuild виртуальной Машины и очистки hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="08179-148">It takes a few minutes for Packer toobuild hello VM, run hello provisioners, and clean up hello deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="08179-149">Создание виртуальной машины на основе образа Azure</span><span class="sxs-lookup"><span data-stu-id="08179-149">Create VM from Azure Image</span></span>
<span data-ttu-id="08179-150">Набор администратору имя пользователя и пароль для виртуальных машин hello с [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="08179-150">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="08179-151">Теперь можно создать виртуальную машину из образа с помощью командлета [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="08179-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="08179-152">Hello следующий пример создает Виртуальную машину с именем *myVM* из *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="08179-152">hello following example creates a VM named *myVM* from *myPackerImage*.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod "Static" `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Define hello image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="08179-153">Занимает несколько минут toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08179-153">It takes a few minutes toocreate hello VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="08179-154">Тестирование виртуальной машины и служб IIS</span><span class="sxs-lookup"><span data-stu-id="08179-154">Test VM and IIS</span></span>
<span data-ttu-id="08179-155">Получить hello общедоступный IP-адрес виртуальной Машины с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="08179-155">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="08179-156">Hello следующий пример извлекает hello IP-адрес для *myPublicIP* созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="08179-156">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="08179-157">После этого можно вводить hello общедоступный IP-адрес в tooa веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="08179-157">You can then enter hello public IP address in tooa web browser.</span></span>

![Сайт IIS по умолчанию](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="08179-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="08179-159">Next steps</span></span>
<span data-ttu-id="08179-160">В этом примере используется Packer toocreate образ виртуальной Машины с уже установленными службами IIS.</span><span class="sxs-lookup"><span data-stu-id="08179-160">In this example, you used Packer toocreate a VM image with IIS already installed.</span></span> <span data-ttu-id="08179-161">Можно использовать этот образ виртуальной Машины наряду с существующие рабочие процессы развертывания, например toodeploy tooVMs вашего приложения, созданные на основе hello изображение с Team Services, Ansible, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="08179-161">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="08179-162">Дополнительный пример шаблонов Packer для других дистрибутивов Windows см. в этом [репозитории GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="08179-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>