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
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="c745b-103">Подключение пользовательского tooa Azure облачной службы роли контроллера домена AD размещено в Azure</span><span class="sxs-lookup"><span data-stu-id="c745b-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="c745b-104">Сначала настройте виртуальную сеть в Azure.</span><span class="sxs-lookup"><span data-stu-id="c745b-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="c745b-105">Затем мы добавим toohello (размещенный на виртуальных машинах Azure) контроллер домена Active Directory виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c745b-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="c745b-106">Далее мы будет toohello роли службы для существующей облачной ранее созданной виртуальной сети, а затем подключите их toohello контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="c745b-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="c745b-107">Прежде чем начать, пару из tookeep действия в виду:</span><span class="sxs-lookup"><span data-stu-id="c745b-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="c745b-108">В этом учебнике используется PowerShell, поэтому проверьте, есть Azure PowerShell установлена и готова toogo.</span><span class="sxs-lookup"><span data-stu-id="c745b-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="c745b-109">tooget справку по настройке Azure PowerShell, в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c745b-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="c745b-110">Контроллер домена AD и рабочих и веб-роли экземпляры должны toobe в hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c745b-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="c745b-111">Выполните в этом пошаговом руководстве и если возникнут проблемы, отправьте нам комментарий в конце hello hello статьи.</span><span class="sxs-lookup"><span data-stu-id="c745b-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="c745b-112">Свяжется tooyou (Да, мы чтения комментариев).</span><span class="sxs-lookup"><span data-stu-id="c745b-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="c745b-113">Hello сеть, на который ссылается hello облачная служба должна быть **классической виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="c745b-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="c745b-114">Создайте виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="c745b-114">Create a Virtual Network</span></span>
<span data-ttu-id="c745b-115">Можно создать виртуальную сеть в Azure с помощью портала Azure hello или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c745b-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="c745b-116">В этом руководстве используется PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c745b-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="c745b-117">в виртуальной сети с помощью toocreate hello Azure портала, см. в разделе [Создание виртуальной сети](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c745b-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="c745b-118">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c745b-118">Create a Virtual Machine</span></span>
<span data-ttu-id="c745b-119">После завершения настройки hello виртуальной сети, необходимо будет toocreate контроллер домена AD.</span><span class="sxs-lookup"><span data-stu-id="c745b-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="c745b-120">В этом учебнике выполняется настройка контроллера домена AD на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="c745b-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="c745b-121">toodo, создание виртуальной машины с помощью PowerShell, с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c745b-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

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

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="c745b-122">Повышение уровня tooa вашей виртуальной машины контроллера домена</span><span class="sxs-lookup"><span data-stu-id="c745b-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="c745b-123">hello tooconfigure виртуальную машину как контроллер домена AD, может потребоваться toolog в toohello виртуальной Машины и настроить его.</span><span class="sxs-lookup"><span data-stu-id="c745b-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="c745b-124">toolog в toohello виртуальной Машины hello RDP-файл можно получить с помощью PowerShell hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c745b-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="c745b-125">После входа в toohello виртуальной Машины, настроить виртуальную машину как контроллер домена AD, следующие пошаговые руководства hello на [как tooset вашего клиента контроллера домена AD](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="c745b-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="c745b-126">Добавить toohello вашей облачной службе виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c745b-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="c745b-127">Далее необходимо tooadd вашей облачной службы развертывания toohello новой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c745b-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="c745b-128">toodo, изменить облака службы cscfg, добавив tooyour cscfg hello соответствующие разделы, с помощью Visual Studio или hello редактора по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="c745b-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

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

<span data-ttu-id="c745b-129">После построения проекта облачной службы и развернуть ее tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c745b-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="c745b-130">tooget сведения о развертывании вашей tooAzure пакета облачной службы в разделе [как tooCreate и развертывание облачной службы](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="c745b-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="c745b-131">Подключение домена toohello рабочих и веб-роли</span><span class="sxs-lookup"><span data-stu-id="c745b-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="c745b-132">После развертывания проекта облачной службы в Azure подключаться домена toohello пользовательские AD экземпляров роли с помощью hello расширение домена AD.</span><span class="sxs-lookup"><span data-stu-id="c745b-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="c745b-133">hello tooadd развертывания существующей облачной службы для расширения домена AD tooyour и присоединение к домену пользовательские "hello", выполните следующие команды в PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="c745b-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

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

<span data-ttu-id="c745b-134">И это все.</span><span class="sxs-lookup"><span data-stu-id="c745b-134">And that's it.</span></span>

<span data-ttu-id="c745b-135">Облачные службы должно быть присоединены к домену tooyour пользовательского домена контроллера.</span><span class="sxs-lookup"><span data-stu-id="c745b-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="c745b-136">Если вы хотите toolearn Здравствуйте, Дополнительные сведения о различных функций, доступных для помощь tooconfigure расширение домена AD, используйте hello PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c745b-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="c745b-137">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="c745b-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```
