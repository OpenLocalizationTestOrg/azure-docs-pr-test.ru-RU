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
# <a name="how-toouse-packer-toocreate-windows-virtual-machine-images-in-azure"></a>Как на виртуальной машине Windows toouse Packer toocreate образы в Azure
Каждой виртуальной машины (VM) в Azure создается из образа, определяющего распространения Windows hello и версию операционной системы. Образы могут содержать предварительно установленные приложения и конфигурации. Hello Azure Marketplace предоставляет большое количество изображений первый и сторонних разработчиков для наиболее распространенных операционной системы и приложений, или можно создать потребностями tooyour специально созданных пользовательских образов. В этой статье описаны как toouse Привет открыть инструмент источника [Packer](https://www.packer.io/) toodefine и построения пользовательских образов в Azure.


## <a name="create-azure-resource-group"></a>Создание группы ресурсов Azure
Во время сборки hello Packer создает временные ресурсы Azure, при построении hello исходной виртуальной Машины. toocapture, исходной виртуальной Машины для использования в качестве образа, необходимо определить группу ресурсов. Hello выходные данные процесса сборки hello Packer хранится в этой группе ресурсов.

Создайте группу ресурсов с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```powershell
$rgName = "myResourceGroup"
$location = "East US"
New-AzureRmResourceGroup -Name $rgName -Location $location
```

## <a name="create-azure-credentials"></a>Создание учетных данных Azure
Packer выполняет проверку подлинности с помощью субъекта-службы Azure. Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Packer. Управление и определить hello разрешения участника службы hello toowhat операции можно выполнять в Azure.

Создание службы с основной [New AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) и назначьте разрешения для участника toocreate hello службы и управление ресурсами с помощью [New AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment):

```powershell
$sp = New-AzureRmADServicePrincipal -DisplayName "Azure Packer IKF" -Password "P@ssw0rd!"
Sleep 20
New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $sp.ApplicationId
```

tooauthenticate tooAzure, необходимо также tooobtain вашей Azure ИД клиента и подписки с [Get AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription):

```powershell
$sub = Get-AzureRmSubscription
$sub.TenantId
$sub.SubscriptionId
```

Эти два ИД используется в следующем шаге hello.


## <a name="define-packer-template"></a>Определение шаблона Packer
toobuild изображения, нужно создать шаблон в формате JSON. В шаблоне hello определения построители и provisioners, выполняющих hello фактический процесс построения. Имеет packer [средство подготовки для Azure](https://www.packer.io/docs/builders/azure.html) , позволяющий toodefine Azure ресурсы, такие как службы основной hello учетных данных, созданных в предыдущих шага hello.

Создайте файл с именем *windows.json* и вставить hello после содержимого. Ввести собственные значения для следующего hello:

| Параметр                           | Где tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Просмотрите идентификатор субъекта-службы с помощью `$sp.applicationId` |
| *client_secret*                     | Пароль, указанный в `$securePassword` |
| *tenant_id*                         | Выходные данные команды `$sub.TenantId` |
| *subscription_id*                   | Выходные данные команды `$sub.SubscriptionId` |
| *object_id*                         | Просмотрите идентификатор объекта субъекта-службы с помощью `$sp.Id` |
| *managed_image_resource_group_name* | Имя группы ресурсов, созданный на первом шаге hello |
| *managed_image_name*                | Имя образа hello управляемого диска, который создается |

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

Этот шаблон создает виртуальную Машину Windows Server 2016, установка служб IIS, а затем обобщает hello виртуальной Машины с помощью средства Sysprep.


## <a name="build-packer-image"></a>Создание образа Packer
Если у вас еще нет Packer установлен на локальном компьютере, [следуйте инструкциям по установке hello Packer](https://www.packer.io/docs/install/index.html).

Для создания образа hello задайте вашей Packer файл шаблона следующим образом:

```bash
./packer build windows.json
```

Пример выходных данных hello hello предшествующий команды выглядит следующим образом:

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

Он занимает несколько минут для выполнения hello provisioners hello Packer toobuild виртуальной Машины и очистки hello развертывания.


## <a name="create-vm-from-azure-image"></a>Создание виртуальной машины на основе образа Azure
Набор администратору имя пользователя и пароль для виртуальных машин hello с [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential).

```powershell
$cred = Get-Credential
```

Теперь можно создать виртуальную машину из образа с помощью командлета [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Hello следующий пример создает Виртуальную машину с именем *myVM* из *myPackerImage*.

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

Занимает несколько минут toocreate hello виртуальной Машины.


## <a name="test-vm-and-iis"></a>Тестирование виртуальной машины и служб IIS
Получить hello общедоступный IP-адрес виртуальной Машины с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress). Hello следующий пример извлекает hello IP-адрес для *myPublicIP* созданную ранее:

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName $rgName `
    -Name "myPublicIP" | select "IpAddress"
```

После этого можно вводить hello общедоступный IP-адрес в tooa веб-браузере.

![Сайт IIS по умолчанию](./media/build-image-with-packer/iis.png) 


## <a name="next-steps"></a>Дальнейшие действия
В этом примере используется Packer toocreate образ виртуальной Машины с уже установленными службами IIS. Можно использовать этот образ виртуальной Машины наряду с существующие рабочие процессы развертывания, например toodeploy tooVMs вашего приложения, созданные на основе hello изображение с Team Services, Ansible, Chef или Puppet.

Дополнительный пример шаблонов Packer для других дистрибутивов Windows см. в этом [репозитории GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).