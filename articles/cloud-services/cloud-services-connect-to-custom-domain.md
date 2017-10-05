---
title: "Подключение облачной службы к пользовательскому контроллеру домена | Документация Майкрософт"
description: "Сведения о подключении веб-ролей и рабочих ролей к личному домену AD с помощью PowerShell и расширения домена AD"
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
ms.openlocfilehash: 17f6918371678ac849198bff4e3b3eea8678c660
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a>Подключение ролей облачных служб Azure к контроллеру личного домена AD, размещенному в Azure
Сначала настройте виртуальную сеть в Azure. Затем добавьте к ней контроллер домена Active Directory (размещенный на виртуальной машине Azure). После этого добавьте имеющиеся роли облачных служб в заранее созданную виртуальную сеть и подключите их к контроллеру домена.

Прежде чем начать, пара моментов, которые стоит запомнить:

1. В этом руководстве используется Azure PowerShell. Поэтому убедитесь, что это средство установлено и готово к использованию. Справку об установке Azure PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).
2. Экземпляры контроллера домена AD и веб-ролей или рабочих ролей должны быть в виртуальной сети.

Следуйте этому пошаговому руководству и, если возникнут проблемы, оставьте нам комментарий в конце статьи. Кто-нибудь из наших сотрудников вам ответит (да, мы читаем ваши комментарии).

Сеть, на которую ссылается облачная служба, должна быть **классической виртуальной сетью**.

## <a name="create-a-virtual-network"></a>Создайте виртуальную сеть
Создать виртуальную сеть в Azure можно с помощью портала Azure или PowerShell. В этом руководстве используется PowerShell. Сведения о создании виртуальной сети с помощью портала Azure см. в статье [Создание виртуальной сети с несколькими подсетями](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

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
Выполнив настройку виртуальной сети, необходимо будет создать контроллер домена AD. В этом учебнике выполняется настройка контроллера домена AD на виртуальной машине Azure.

Для этого создайте виртуальную машину с помощью PowerShell, используя следующие команды.

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

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a>Повысьте уровень виртуальной машины до контроллера домена
Чтобы настроить виртуальную машину в качестве контроллера домена AD, необходимо войти в нее и настроить.

Для входа в виртуальную машину можно получить RDP-файл через PowerShell, используя следующие команды.

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

Войдя в виртуальную машину, настройте ее в качестве контроллера домена AD, следуя указаниям пошагового руководства [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx) (Настройка личного контроллера домена AD).

## <a name="add-your-cloud-service-to-the-virtual-network"></a>Добавление облачной службы в виртуальную сеть
Затем необходимо добавить развертывание облачной службы в новую виртуальную сеть. Для этого измените файл CSCFG облачной службы, добавив в него соответствующие разделы с помощью Visual Studio или другого редактора.

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

Затем создайте проект облачной службы и выполните его развертывание в Azure. Справку о развертывании пакета облачных служб в Azure см. в статье [Создание и развертывание облачной службы](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service).

## <a name="connect-your-webworker-roles-to-the-domain"></a>Подключение веб- и рабочих ролей к домену
Выполнив развертывание проекта облачной службы в Azure, подключите экземпляры ролей к личному домену AD с помощью расширения доменов AD. Чтобы добавить расширение доменов AD к существующему развертыванию облачной службы и присоединить личный домен, выполните в PowerShell следующие команды:

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

И это все.

Облачные службы должны быть присоединены к контроллеру личного домена. Дополнительные сведения о различных параметрах для настройки расширения домена AD см. в справке PowerShell. Вот несколько примеров.

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
