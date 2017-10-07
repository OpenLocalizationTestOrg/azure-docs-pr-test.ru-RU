---
title: "aaaConnect tooa облачной службы настраиваемый контроллер домена | Документы Microsoft"
description: "Узнайте, как tooconnect tooa пользовательских рабочих и веб-роли домена AD с помощью PowerShell и расширение домена AD"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a>Подключение пользовательского tooa Azure облачной службы роли контроллера домена AD размещено в Azure
Сначала настройте виртуальную сеть в Azure. Затем мы добавим toohello (размещенный на виртуальных машинах Azure) контроллер домена Active Directory виртуальной сети. Далее мы будет toohello роли службы для существующей облачной ранее созданной виртуальной сети, а затем подключите их toohello контроллера домена.

Прежде чем начать, пару из tookeep действия в виду:

1. В этом учебнике используется PowerShell, поэтому проверьте, есть Azure PowerShell установлена и готова toogo. tooget справку по настройке Azure PowerShell, в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).
2. Контроллер домена AD и рабочих и веб-роли экземпляры должны toobe в hello виртуальной сети.

Выполните в этом пошаговом руководстве и если возникнут проблемы, отправьте нам комментарий в конце hello hello статьи. Свяжется tooyou (Да, мы чтения комментариев).

Hello сеть, на который ссылается hello облачная служба должна быть **классической виртуальной сети**.

## <a name="create-a-virtual-network"></a>Создайте виртуальную сеть
Можно создать виртуальную сеть в Azure с помощью портала Azure hello или PowerShell. В этом руководстве используется PowerShell. в виртуальной сети с помощью toocreate hello Azure портала, см. в разделе [Создание виртуальной сети](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a>Создание виртуальной машины
После завершения настройки hello виртуальной сети, необходимо будет toocreate контроллер домена AD. В этом учебнике выполняется настройка контроллера домена AD на виртуальной машине Azure.

toodo, создание виртуальной машины с помощью PowerShell, с помощью hello, следующие команды:

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a>Повышение уровня tooa вашей виртуальной машины контроллера домена
hello tooconfigure виртуальную машину как контроллер домена AD, может потребоваться toolog в toohello виртуальной Машины и настроить его.

toolog в toohello виртуальной Машины hello RDP-файл можно получить с помощью PowerShell hello используйте следующие команды:

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

После входа в toohello виртуальной Машины, настроить виртуальную машину как контроллер домена AD, следующие пошаговые руководства hello на [как tooset вашего клиента контроллера домена AD](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).

## <a name="add-your-cloud-service-toohello-virtual-network"></a>Добавить toohello вашей облачной службе виртуальной сети
Далее необходимо tooadd вашей облачной службы развертывания toohello новой виртуальной сети. toodo, изменить облака службы cscfg, добавив tooyour cscfg hello соответствующие разделы, с помощью Visual Studio или hello редактора по своему усмотрению.

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

После построения проекта облачной службы и развернуть ее tooAzure. tooget сведения о развертывании вашей tooAzure пакета облачной службы в разделе [как tooCreate и развертывание облачной службы](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)

## <a name="connect-your-webworker-roles-toohello-domain"></a>Подключение домена toohello рабочих и веб-роли
После развертывания проекта облачной службы в Azure подключаться домена toohello пользовательские AD экземпляров роли с помощью hello расширение домена AD. hello tooadd развертывания существующей облачной службы для расширения домена AD tooyour и присоединение к домену пользовательские "hello", выполните следующие команды в PowerShell hello:

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

И это все.

Облачные службы должно быть присоединены к домену tooyour пользовательского домена контроллера. Если вы хотите toolearn Здравствуйте, Дополнительные сведения о различных функций, доступных для помощь tooconfigure расширение домена AD, используйте hello PowerShell. Вот несколько примеров.

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
