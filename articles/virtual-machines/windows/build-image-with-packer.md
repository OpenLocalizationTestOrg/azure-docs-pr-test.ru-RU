---
title: "Создание образов виртуальных машин Windows в Azure с помощью Packer | Документация Майкрософт"
description: "Сведения об использовании Packer для создания образов виртуальных машин Windows в Azure"
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
ms.openlocfilehash: 11a4a4d65be09e6c518836c25bb455a6df738dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-packer-to-create-windows-virtual-machine-images-in-azure"></a><span data-ttu-id="7cb8a-103">Использование Packer для создания образов виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="7cb8a-103">How to use Packer to create Windows virtual machine images in Azure</span></span>
<span data-ttu-id="7cb8a-104">Каждая виртуальная машина в Azure создается из образа, который определяет дистрибутив Windows и версию операционной системы.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-104">Each virtual machine (VM) in Azure is created from an image that defines the Windows distribution and OS version.</span></span> <span data-ttu-id="7cb8a-105">Образы могут содержать предварительно установленные приложения и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="7cb8a-106">Azure Marketplace предоставляет большое количество образов Майкрософт и сторонних разработчиков для наиболее распространенных операционных систем и приложений. Кроме того, вы можете создать собственные настраиваемые образы, отвечающие конкретным потребностям.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-106">The Azure Marketplace provides many first and third-party images for most common OS' and application environments, or you can create your own custom images tailored to your needs.</span></span> <span data-ttu-id="7cb8a-107">В этой статье описывается определение и создание пользовательских образов в Azure с использованием средства с открытым кодом [Packer](https://www.packer.io/).</span><span class="sxs-lookup"><span data-stu-id="7cb8a-107">This article details how to use the open source tool [Packer](https://www.packer.io/) to define and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="7cb8a-108">Создание группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="7cb8a-108">Create Azure resource group</span></span>
<span data-ttu-id="7cb8a-109">В процессе сборки исходной виртуальной машины Packer создает временные ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-109">During the build process, Packer creates temporary Azure resources as it builds the source VM.</span></span> <span data-ttu-id="7cb8a-110">Чтобы сохранить эту исходную виртуальную машину для использования в качестве образа, необходимо определить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-110">To capture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="7cb8a-111">Выходные данные процесса сборки Packer хранятся в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-111">The output from the Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="7cb8a-112">Создайте группу ресурсов с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="7cb8a-112">Create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="7cb8a-113">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a><span data-ttu-id="7cb8a-114">Создание учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="7cb8a-114">Create Azure credentials</span></span>
<span data-ttu-id="7cb8a-115">Packer выполняет проверку подлинности с помощью субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="7cb8a-116">Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Packer.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="7cb8a-117">Вы можете определять разрешения на то, какие операции может выполнять субъект-служба в Azure, и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-117">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span>

<span data-ttu-id="7cb8a-118">Создайте субъект-службу с помощью команды [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) и назначьте ей разрешения на создание и управление ресурсами с помощью [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span><span class="sxs-lookup"><span data-stu-id="7cb8a-118">Create a service principal with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) and assign permissions for the service principal to create and manage resources with [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):</span></span>

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

<span data-ttu-id="7cb8a-119">Для выполнения проверки подлинности в Azure вам также необходимо получить идентификаторы вашего клиента и подписки Azure с помощью команды [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span><span class="sxs-lookup"><span data-stu-id="7cb8a-119">To authenticate to Azure, you also need to obtain your Azure tenant and subscription IDs with [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):</span></span>

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

<span data-ttu-id="7cb8a-120">Эти идентификаторы используются в следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-120">You use these two IDs in the next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="7cb8a-121">Определение шаблона Packer</span><span class="sxs-lookup"><span data-stu-id="7cb8a-121">Define Packer template</span></span>
<span data-ttu-id="7cb8a-122">Чтобы собрать образы, создайте шаблон в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-122">To build images, you create a template as a JSON file.</span></span> <span data-ttu-id="7cb8a-123">В шаблоне определите средства разработки и подготовки, выполняющие процесс сборки.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-123">In the template, you define builders and provisioners that carry out the actual build process.</span></span> <span data-ttu-id="7cb8a-124">Packer использует [средство подготовки для Azure](https://www.packer.io/docs/builders/azure.html), которое позволяет определить ресурсы Azure, такие как учетные данные субъекта-службы, созданные на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-124">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you to define Azure resources, such as the service principal credentials created in the preceding step.</span></span>

<span data-ttu-id="7cb8a-125">Создайте файл с именем *windows.json* и вставьте следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-125">Create a file named *windows.json* and paste the following content.</span></span> <span data-ttu-id="7cb8a-126">Введите свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7cb8a-126">Enter your own values for the following:</span></span>

| <span data-ttu-id="7cb8a-127">Параметр</span><span class="sxs-lookup"><span data-stu-id="7cb8a-127">Parameter</span></span>                           | <span data-ttu-id="7cb8a-128">Где можно получить</span><span class="sxs-lookup"><span data-stu-id="7cb8a-128">Where to obtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="7cb8a-129">*client_id*</span><span class="sxs-lookup"><span data-stu-id="7cb8a-129">*client_id*</span></span>                         | <span data-ttu-id="7cb8a-130">Просмотрите идентификатор субъекта-службы с помощью `$sp.applicationId`</span><span class="sxs-lookup"><span data-stu-id="7cb8a-130">View service principal ID with `$sp.applicationId`</span></span> |
| <span data-ttu-id="7cb8a-131">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="7cb8a-131">*client_secret*</span></span>                     | <span data-ttu-id="7cb8a-132">Пароль, указанный в `$securePassword`</span><span class="sxs-lookup"><span data-stu-id="7cb8a-132">Password you specified in `$securePassword`</span></span> |
| <span data-ttu-id="7cb8a-133">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="7cb8a-133">*tenant_id*</span></span>                         | <span data-ttu-id="7cb8a-134">Выходные данные команды `$sub.TenantId`</span><span class="sxs-lookup"><span data-stu-id="7cb8a-134">Output from `$sub.TenantId` command</span></span> |
| <span data-ttu-id="7cb8a-135">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="7cb8a-135">*subscription_id*</span></span>                   | <span data-ttu-id="7cb8a-136">Выходные данные команды `$sub.SubscriptionId`</span><span class="sxs-lookup"><span data-stu-id="7cb8a-136">Output from `$sub.SubscriptionId` command</span></span> |
| <span data-ttu-id="7cb8a-137">*object_id*</span><span class="sxs-lookup"><span data-stu-id="7cb8a-137">*object_id*</span></span>                         | <span data-ttu-id="7cb8a-138">Просмотрите идентификатор объекта субъекта-службы с помощью `$sp.Id`</span><span class="sxs-lookup"><span data-stu-id="7cb8a-138">View service principal object ID with `$sp.Id`</span></span> |
| <span data-ttu-id="7cb8a-139">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="7cb8a-139">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="7cb8a-140">Имя группы ресурсов, созданной на первом шаге</span><span class="sxs-lookup"><span data-stu-id="7cb8a-140">Name of resource group you created in the first step</span></span> |
| <span data-ttu-id="7cb8a-141">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="7cb8a-141">*managed_image_name*</span></span>                | <span data-ttu-id="7cb8a-142">Имя создаваемого образа управляемого диска</span><span class="sxs-lookup"><span data-stu-id="7cb8a-142">Name for the managed disk image that is created</span></span> |

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

<span data-ttu-id="7cb8a-143">Этот шаблон создает виртуальную машину Windows Server 2016, устанавливает службы IIS, а затем подготавливает виртуальную машину с помощью средства Sysprep.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-143">This template builds a Windows Server 2016 VM, installs IIS, then generalizes the VM with Sysprep.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="7cb8a-144">Создание образа Packer</span><span class="sxs-lookup"><span data-stu-id="7cb8a-144">Build Packer image</span></span>
<span data-ttu-id="7cb8a-145">Если средство Packer еще не установлено на локальном компьютере, [следуйте инструкциям по его установке](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="7cb8a-145">If you don't already have Packer installed on your local machine, [follow the Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="7cb8a-146">Создайте образ, указав файл шаблона Packer следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7cb8a-146">Build the image by specifying your Packer template file as follows:</span></span>

```bash
./packer build windows.json
```

<span data-ttu-id="7cb8a-147">Ниже приведен пример выходных данных предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="7cb8a-147">An example of the output from the preceding commands is as follows:</span></span>

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
==> azure-arm: Getting the certificate’s URL ...
==> azure-arm:  -> Key Vault Name        : ‘pkrkvpq0mthtbtt’
==> azure-arm:  -> Key Vault Secret Name : ‘packerKeyVaultSecret’
==> azure-arm:  -> Certificate URL       : ‘https://pkrkvpq0mthtbtt.vault.azure.net/secrets/packerKeyVaultSecret/8c7bd823e4fa44e1abb747636128adbb'
==> azure-arm: Setting the certificate’s URL ...
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> DeploymentName    : ‘pkrdppq0mthtbtt’
==> azure-arm: Getting the VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-pq0mthtbtt’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.55.35’
==> azure-arm: Waiting for WinRM to become available...
==> azure-arm: Connected to WinRM!
==> azure-arm: Provisioning with Powershell...
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-powershell-provisioner902510110
    azure-arm: #< CLIXML
    azure-arm:
    azure-arm: Success Restart Needed Exit Code      Feature Result
    azure-arm: ------- -------------- ---------      --------------
    azure-arm: True    No             Success        {Common HTTP Features, Default Document, D...
    azure-arm: <Objs Version=“1.1.0.1” xmlns=“http://schemas.microsoft.com/powershell/2004/04"><Obj S=“progress” RefId=“0"><TN RefId=“0”><T>System.Management.Automation.PSCustomObject</T><T>System.Object</T></TN><MS><I64 N=“SourceId”>1</I64><PR N=“Record”><AV>Preparing modules for first use.</AV><AI>0</AI><Nil /><PI>-1</PI><PC>-1</PC><T>Completed</T><SR>-1</SR><SD> </SD></PR></MS></Obj></Objs>
==> azure-arm: Querying the machine’s properties ...
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
==> azure-arm: Deleting the temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. The artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```

<span data-ttu-id="7cb8a-148">Через несколько минут Packer создаст виртуальную машину, запустит средства подготовки и очистит развертывание.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-148">It takes a few minutes for Packer to build the VM, run the provisioners, and clean up the deployment.</span></span>


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="7cb8a-149">Создание виртуальной машины на основе образа Azure</span><span class="sxs-lookup"><span data-stu-id="7cb8a-149">Create VM from Azure Image</span></span>
<span data-ttu-id="7cb8a-150">Укажите имя и пароль администратора для виртуальной машины с помощью командлета [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span><span class="sxs-lookup"><span data-stu-id="7cb8a-150">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="7cb8a-151">Теперь можно создать виртуальную машину из образа с помощью командлета [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="7cb8a-151">You can now create a VM from your Image with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="7cb8a-152">В следующем примере создается виртуальная машина с именем *myVM* из образа *myPackerImage*.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-152">The following example creates a VM named *myVM* from *myPackerImage*.</span></span>

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

# Define the image created by Packer
$image = Get-AzureRMImage -ImageName myPackerImage -ResourceGroupName $rgName

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -Id $image.Id | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```

<span data-ttu-id="7cb8a-153">Создание виртуальной машины занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-153">It takes a few minutes to create the VM.</span></span>


## <a name="test-vm-and-iis"></a><span data-ttu-id="7cb8a-154">Тестирование виртуальной машины и служб IIS</span><span class="sxs-lookup"><span data-stu-id="7cb8a-154">Test VM and IIS</span></span>
<span data-ttu-id="7cb8a-155">Получите общедоступный IP-адрес своей виртуальной машины с помощью командлета [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="7cb8a-155">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="7cb8a-156">Следующий пример позволяет получить IP-адрес для созданного ранее *myPublicIP*.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-156">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="7cb8a-157">После этого можно ввести общедоступный IP-адрес в веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-157">You can then enter the public IP address in to a web browser.</span></span>

![Сайт IIS по умолчанию](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a><span data-ttu-id="7cb8a-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7cb8a-159">Next steps</span></span>
<span data-ttu-id="7cb8a-160">В этом примере вы создали образ виртуальной машины с уже установленными службами IIS с помощью Packer.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-160">In this example, you used Packer to create a VM image with IIS already installed.</span></span> <span data-ttu-id="7cb8a-161">Этот образ виртуальной машины можно использовать наряду с имеющимися рабочими процессами развертывания, как например развертывание приложений на виртуальных машинах, созданных из образа с помощью Team Services, Ansible, Chef или Puppet.</span><span class="sxs-lookup"><span data-stu-id="7cb8a-161">You can use this VM image alongside existing deployment workflows, such as to deploy your app to VMs created from the Image with Team Services, Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="7cb8a-162">Дополнительный пример шаблонов Packer для других дистрибутивов Windows см. в этом [репозитории GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="7cb8a-162">For additional example Packer templates for other Windows distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>