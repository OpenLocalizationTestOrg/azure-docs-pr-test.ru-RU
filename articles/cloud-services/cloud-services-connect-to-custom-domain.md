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
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="e83c1-103">Подключение ролей облачных служб Azure к контроллеру личного домена AD, размещенному в Azure</span><span class="sxs-lookup"><span data-stu-id="e83c1-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="e83c1-104">Сначала настройте виртуальную сеть в Azure.</span><span class="sxs-lookup"><span data-stu-id="e83c1-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="e83c1-105">Затем добавьте к ней контроллер домена Active Directory (размещенный на виртуальной машине Azure).</span><span class="sxs-lookup"><span data-stu-id="e83c1-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="e83c1-106">После этого добавьте имеющиеся роли облачных служб в заранее созданную виртуальную сеть и подключите их к контроллеру домена.</span><span class="sxs-lookup"><span data-stu-id="e83c1-106">Next, we will add existing cloud service roles to the pre-created VNet, then connect them to the Domain Controller.</span></span>

<span data-ttu-id="e83c1-107">Прежде чем начать, пара моментов, которые стоит запомнить:</span><span class="sxs-lookup"><span data-stu-id="e83c1-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="e83c1-108">В этом руководстве используется Azure PowerShell. Поэтому убедитесь, что это средство установлено и готово к использованию.</span><span class="sxs-lookup"><span data-stu-id="e83c1-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="e83c1-109">Справку об установке Azure PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e83c1-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="e83c1-110">Экземпляры контроллера домена AD и веб-ролей или рабочих ролей должны быть в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e83c1-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="e83c1-111">Следуйте этому пошаговому руководству и, если возникнут проблемы, оставьте нам комментарий в конце статьи.</span><span class="sxs-lookup"><span data-stu-id="e83c1-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at the end of the article.</span></span> <span data-ttu-id="e83c1-112">Кто-нибудь из наших сотрудников вам ответит (да, мы читаем ваши комментарии).</span><span class="sxs-lookup"><span data-stu-id="e83c1-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="e83c1-113">Сеть, на которую ссылается облачная служба, должна быть **классической виртуальной сетью**.</span><span class="sxs-lookup"><span data-stu-id="e83c1-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="e83c1-114">Создайте виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="e83c1-114">Create a Virtual Network</span></span>
<span data-ttu-id="e83c1-115">Создать виртуальную сеть в Azure можно с помощью портала Azure или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e83c1-115">You can create a Virtual Network in Azure using the Azure portal or PowerShell.</span></span> <span data-ttu-id="e83c1-116">В этом руководстве используется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e83c1-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="e83c1-117">Сведения о создании виртуальной сети с помощью портала Azure см. в статье [Создание виртуальной сети с несколькими подсетями](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="e83c1-117">To create a Virtual Network using the Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="e83c1-118">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e83c1-118">Create a Virtual Machine</span></span>
<span data-ttu-id="e83c1-119">Выполнив настройку виртуальной сети, необходимо будет создать контроллер домена AD.</span><span class="sxs-lookup"><span data-stu-id="e83c1-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="e83c1-120">В этом учебнике выполняется настройка контроллера домена AD на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="e83c1-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="e83c1-121">Для этого создайте виртуальную машину с помощью PowerShell, используя следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e83c1-121">To do this, create a virtual machine through PowerShell using the following commands:</span></span>

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

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="e83c1-122">Повысьте уровень виртуальной машины до контроллера домена</span><span class="sxs-lookup"><span data-stu-id="e83c1-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="e83c1-123">Чтобы настроить виртуальную машину в качестве контроллера домена AD, необходимо войти в нее и настроить.</span><span class="sxs-lookup"><span data-stu-id="e83c1-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="e83c1-124">Для входа в виртуальную машину можно получить RDP-файл через PowerShell, используя следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e83c1-124">To log in to the VM, you can get the RDP file through PowerShell, use the following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="e83c1-125">Войдя в виртуальную машину, настройте ее в качестве контроллера домена AD, следуя указаниям пошагового руководства [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx) (Настройка личного контроллера домена AD).</span><span class="sxs-lookup"><span data-stu-id="e83c1-125">Once you are signed in to the VM, set up your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="e83c1-126">Добавление облачной службы в виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="e83c1-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="e83c1-127">Затем необходимо добавить развертывание облачной службы в новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="e83c1-127">Next, you need to add your cloud service deployment to the new VNet.</span></span> <span data-ttu-id="e83c1-128">Для этого измените файл CSCFG облачной службы, добавив в него соответствующие разделы с помощью Visual Studio или другого редактора.</span><span class="sxs-lookup"><span data-stu-id="e83c1-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

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

<span data-ttu-id="e83c1-129">Затем создайте проект облачной службы и выполните его развертывание в Azure.</span><span class="sxs-lookup"><span data-stu-id="e83c1-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="e83c1-130">Справку о развертывании пакета облачных служб в Azure см. в статье [Создание и развертывание облачной службы](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="e83c1-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="e83c1-131">Подключение веб- и рабочих ролей к домену</span><span class="sxs-lookup"><span data-stu-id="e83c1-131">Connect your web/worker roles to the domain</span></span>
<span data-ttu-id="e83c1-132">Выполнив развертывание проекта облачной службы в Azure, подключите экземпляры ролей к личному домену AD с помощью расширения доменов AD.</span><span class="sxs-lookup"><span data-stu-id="e83c1-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="e83c1-133">Чтобы добавить расширение доменов AD к существующему развертыванию облачной службы и присоединить личный домен, выполните в PowerShell следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e83c1-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

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

<span data-ttu-id="e83c1-134">И это все.</span><span class="sxs-lookup"><span data-stu-id="e83c1-134">And that's it.</span></span>

<span data-ttu-id="e83c1-135">Облачные службы должны быть присоединены к контроллеру личного домена.</span><span class="sxs-lookup"><span data-stu-id="e83c1-135">Your cloud services should be joined to your custom domain controller.</span></span> <span data-ttu-id="e83c1-136">Дополнительные сведения о различных параметрах для настройки расширения домена AD см. в справке PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e83c1-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help.</span></span> <span data-ttu-id="e83c1-137">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="e83c1-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
