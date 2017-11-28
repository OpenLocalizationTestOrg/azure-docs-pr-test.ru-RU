---
title: "адреса aaaAzure уровне экземпляра общедоступный IP-адрес (классические) | Документы Microsoft"
description: "Понимать экземпляра уровня общедоступных адресов IP (ILPIP) и как toomanage их с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="5ed91-103">Общие сведения об общедоступных IP-адресах уровня экземпляра (классическая модель развертывания)</span><span class="sxs-lookup"><span data-stu-id="5ed91-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="5ed91-104">Экземпляр уровня открытый IP (ILPIP) — общедоступный IP-адрес, который можно назначить непосредственно tooa экземпляра роли виртуальной Машины или облачные службы, а не toohello облачной службы, в котором экземпляр виртуальной Машины или роли.</span><span class="sxs-lookup"><span data-stu-id="5ed91-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="5ed91-105">ILPIP не принимает hello вместо hello виртуальный IP-адрес (VIP), назначенный tooyour облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5ed91-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="5ed91-106">Скорее, это дополнительный IP-адрес, что можно использовать tooconnect непосредственно tooyour ВМ или экземпляру роли.</span><span class="sxs-lookup"><span data-stu-id="5ed91-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ed91-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ed91-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="5ed91-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="5ed91-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="5ed91-109">Корпорация Майкрософт рекомендует создавать виртуальные машины с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5ed91-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="5ed91-110">Убедитесь, что вы понимаете как работают в Azure [IP-адреса](virtual-network-ip-addresses-overview-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="5ed91-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Разница между ILPIP-адресом и виртуальным IP-адресом](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="5ed91-112">Как показано на рисунке 1 hello облачной службе осуществляется с использованием VIP, при hello отдельные виртуальные машины обычно осуществляется с помощью виртуального IP-адреса:&lt;номер порта&gt;.</span><span class="sxs-lookup"><span data-stu-id="5ed91-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="5ed91-113">Назначив tooa ILPIP определенную виртуальную Машину, что виртуальная машина может быть доступ непосредственно с помощью этого IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="5ed91-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="5ed91-114">При создании облачной службы в Azure, соответствующие записи DNS создаются автоматически службы toohello tooallow доступа через полное доменное имя (FQDN), вместо использования hello фактических виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="5ed91-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="5ed91-115">Hello для ILPIP, позволяя доступа toohello ВМ или экземпляру роли по полному доменному ИМЕНИ вместо hello ILPIP может произойти одного процесса.</span><span class="sxs-lookup"><span data-stu-id="5ed91-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="5ed91-116">Для экземпляра при создании облачной службы с именем *contosoadservice*, и настройте веб-роль с именем *contosoweb* с двумя экземплярами hello Azure регистрирует следующие A записей для hello экземпляров:</span><span class="sxs-lookup"><span data-stu-id="5ed91-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="5ed91-117">contosoweb\_IN_0.contosoadservice.cloudapp.net;</span><span class="sxs-lookup"><span data-stu-id="5ed91-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="5ed91-118">contosoweb\_IN_1.contosoadservice.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="5ed91-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="5ed91-119">Каждой виртуальной машине или экземпляру роли можно назначить только один ILPIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5ed91-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="5ed91-120">Воспользуйтесь ILPIPs too5 на подписку.</span><span class="sxs-lookup"><span data-stu-id="5ed91-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="5ed91-121">ILPIP-адреса не поддерживаются для виртуальных машин с несколькими сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="5ed91-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="5ed91-122">Зачем запрашивать ILPIP-адрес?</span><span class="sxs-lookup"><span data-stu-id="5ed91-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="5ed91-123">Tooyour может tooconnect toobe виртуальной Машины или экземпляра роли по IP-адреса назначаются напрямую tooit, вместо использования hello облачной службы VIP:&lt;номер порта&gt;, запрос ILPIP для виртуальной Машины или экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="5ed91-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="5ed91-124">**Активный режим FTP** -назначая ILPIP tooa виртуальной Машины, она может получать трафик через любой порт.</span><span class="sxs-lookup"><span data-stu-id="5ed91-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="5ed91-125">Конечные точки не являются обязательными для hello tooreceive трафика виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="5ed91-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="5ed91-126">Дополнительные сведения по протоколу hello FTP. в разделе (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Обзор протокола FTP].</span><span class="sxs-lookup"><span data-stu-id="5ed91-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="5ed91-127">**Исходящий IP-адрес** - исходящий трафик от ВМ hello сопоставлен toohello ILPIP в качестве источника hello и hello ILPIP однозначно определяет объекты tooexternal hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5ed91-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="5ed91-128">В прошлом hello адрес ILPIP была ссылка tooas общедоступному IP (PIP).</span><span class="sxs-lookup"><span data-stu-id="5ed91-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="5ed91-129">Управление ILPIP-адресом виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5ed91-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="5ed91-130">следующие задачи Hello позволяют toocreate, назначение и удаление ILPIPs из виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="5ed91-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="5ed91-131">Как toorequest ILPIP во время создания виртуальной Машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ed91-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="5ed91-132">Следующий сценарий PowerShell Hello создает облачную службу с именем *FTP-Служба\всего*, извлекает изображение из Azure, создает Виртуальную машину с именем *FTPInstance* с помощью образа hello получить задает hello ВМ toouse ILPIP и добавляет новую службу hello ВМ toohello:</span><span class="sxs-lookup"><span data-stu-id="5ed91-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="5ed91-133">Как tooretrieve ILPIP сведения для виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5ed91-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="5ed91-134">hello tooview ILPIP сведения для hello создания ВМ и для предыдущего сценария hello, запустите следующую команду PowerShell hello и просмотрите значения hello *PublicIPAddress* и *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="5ed91-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="5ed91-135">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5ed91-135">Expected output:</span></span>
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="5ed91-136">Как tooremove ILPIP из виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5ed91-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="5ed91-137">в предыдущий сценарий hello, запустите следующую команду PowerShell hello tooremove hello ILPIP добавлены toohello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="5ed91-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="5ed91-138">Как tooadd tooan ILPIP существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5ed91-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="5ed91-139">tooadd ILPIP toohello виртуальной Машины, созданной с помощью скрипта hello предыдущей, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="5ed91-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="5ed91-140">Управление ILPIP-адресом экземпляра роли облачных служб</span><span class="sxs-lookup"><span data-stu-id="5ed91-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="5ed91-141">tooadd экземпляр роли облачных служб ILPIP tooa завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="5ed91-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="5ed91-142">Загрузите файл cscfg hello hello облачную службу, выполнив hello шагов в hello [как tooConfigure облачных служб](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) статьи.</span><span class="sxs-lookup"><span data-stu-id="5ed91-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="5ed91-143">Обновление hello cscfg-файле, добавив hello `InstanceAddress` элемента.</span><span class="sxs-lookup"><span data-stu-id="5ed91-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="5ed91-144">Hello следующий пример добавляет ILPIP с именем *MyPublicIP* с именем экземпляра роли tooa *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="5ed91-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. <span data-ttu-id="5ed91-145">Отправить файл cscfg hello hello облачную службу, выполнив hello шагов в hello [как tooConfigure облачных служб](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) статьи.</span><span class="sxs-lookup"><span data-stu-id="5ed91-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ed91-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ed91-146">Next steps</span></span>
* <span data-ttu-id="5ed91-147">Понять, как [IP-адресация](virtual-network-ip-addresses-overview-classic.md) работает в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="5ed91-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="5ed91-148">Общие сведения о зарезервированных IP-адресах см. в [этой статье](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="5ed91-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
