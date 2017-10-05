---
title: "Общедоступные IP-адреса уровня экземпляра Azure (классическая модель) | Документация Майкрософт"
description: "Описание общедоступных IP-адресов уровня экземпляра (ILPIP-адресов) и инструкции по управлению ими с помощью PowerShell."
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
ms.openlocfilehash: 773043f2841ec7539b0d49357dec6bcb9f4f78a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="c10f4-103">Общие сведения об общедоступных IP-адресах уровня экземпляра (классическая модель развертывания)</span><span class="sxs-lookup"><span data-stu-id="c10f4-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="c10f4-104">Общедоступный IP-адрес уровня экземпляра (ILPIP) — это общедоступный IP-адрес, который можно назначить непосредственно виртуальной машине или экземпляру роли облачных служб, а не облачной службе, в которой они находятся.</span><span class="sxs-lookup"><span data-stu-id="c10f4-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly to a VM or Cloud Services role instance, rather than to the cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="c10f4-105">Он не заменяет виртуальный IP-адрес (VIP), назначенный облачной службе.</span><span class="sxs-lookup"><span data-stu-id="c10f4-105">An ILPIP doesn’t take the place of the virtual IP (VIP) that is assigned to your cloud service.</span></span> <span data-ttu-id="c10f4-106">а представляет собой дополнительный IP-адрес, с помощью которого можно подключаться непосредственно к виртуальной машине или экземпляру роли.</span><span class="sxs-lookup"><span data-stu-id="c10f4-106">Rather, it’s an additional IP address that you can use to connect directly to your VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c10f4-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c10f4-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="c10f4-108">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c10f4-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c10f4-109">Корпорация Майкрософт рекомендует создавать виртуальные машины с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c10f4-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="c10f4-110">Убедитесь, что вы понимаете как работают в Azure [IP-адреса](virtual-network-ip-addresses-overview-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="c10f4-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Разница между ILPIP-адресом и виртуальным IP-адресом](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="c10f4-112">Как показано на рис. 1, для доступа к облачной службе используется виртуальный IP-адрес, а для обращения к отдельным виртуальным машинам, как правило, применяется формат "виртуальный IP-адрес:&lt;номер_порта&gt;".</span><span class="sxs-lookup"><span data-stu-id="c10f4-112">As shown in Figure 1, the cloud service is accessed using a VIP, while the individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="c10f4-113">Назначив определенной виртуальной машине ILPIP-адрес, вы сможете обращаться к ней напрямую.</span><span class="sxs-lookup"><span data-stu-id="c10f4-113">By assigning an ILPIP to a specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="c10f4-114">При создании облачной службы в среде Azure автоматически создаются соответствующие записи A DNS, благодаря которым к службе можно обращаться по полному доменному имени вместо ее фактического виртуального IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c10f4-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically to allow access to the service through a fully qualified domain name (FQDN), instead of using the actual VIP.</span></span> <span data-ttu-id="c10f4-115">То же самое выполняется и для ILPIP-адресов, благодаря чему к виртуальным машинам и экземплярам ролей можно обращаться по полному доменному имени, не указывая ILPIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c10f4-115">The same process happens for an ILPIP, allowing access to the VM or role instance by FQDN instead of the ILPIP.</span></span> <span data-ttu-id="c10f4-116">Например, если при создании облачной службы *contosoadservice* вы настраиваете веб-роль *contosoweb* с двумя экземплярами, то платформа Azure регистрирует следующие записи A для этих экземпляров:</span><span class="sxs-lookup"><span data-stu-id="c10f4-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers the following A records for the instances:</span></span>

* <span data-ttu-id="c10f4-117">contosoweb\_IN_0.contosoadservice.cloudapp.net;</span><span class="sxs-lookup"><span data-stu-id="c10f4-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="c10f4-118">contosoweb\_IN_1.contosoadservice.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="c10f4-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="c10f4-119">Каждой виртуальной машине или экземпляру роли можно назначить только один ILPIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c10f4-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="c10f4-120">В одной подписке разрешается использовать до 5 ILPIP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c10f4-120">You can use up to 5 ILPIPs per subscription.</span></span> <span data-ttu-id="c10f4-121">ILPIP-адреса не поддерживаются для виртуальных машин с несколькими сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="c10f4-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="c10f4-122">Зачем запрашивать ILPIP-адрес?</span><span class="sxs-lookup"><span data-stu-id="c10f4-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="c10f4-123">Чтобы подключиться к виртуальной машине или экземпляру роли непосредственно по определенному IP-адресу, не используйте формат "виртуальный IP-адрес облачной службы:&lt;номер_порта&gt;", а вместо этого отправьте запрос на создание ILPIP-адреса для виртуальной машины или экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="c10f4-123">If you want to be able to connect to your VM or role instance by an IP address assigned directly to it, rather than using the cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="c10f4-124">**Активный FTP-сервер**. Если назначить ILPIP-адрес виртуальной машине, она сможет получать трафик через любой порт.</span><span class="sxs-lookup"><span data-stu-id="c10f4-124">**Active FTP** - By assigning an ILPIP to a VM, it can receive traffic on any port.</span></span> <span data-ttu-id="c10f4-125">Ей не понадобятся конечные точки, чтобы получать трафик.</span><span class="sxs-lookup"><span data-stu-id="c10f4-125">Endpoints are not required for the VM to receive traffic.</span></span>  <span data-ttu-id="c10f4-126">Дополнительные сведения о протоколе FTP см. в обзоре протокола FTP (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] .</span><span class="sxs-lookup"><span data-stu-id="c10f4-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on the FTP protocol.</span></span>
* <span data-ttu-id="c10f4-127">**Исходящий IP-трафик.** Исходящий трафик с виртуальной машины сопоставляется с ILPIP-адресом в качестве источника, который уникальным образом идентифицирует эту виртуальную машину для внешних сущностей.</span><span class="sxs-lookup"><span data-stu-id="c10f4-127">**Outbound IP** - Outbound traffic originating from the VM is mapped to the ILPIP as the source and the ILPIP uniquely identifies the VM to external entities.</span></span>

> [!NOTE]
> <span data-ttu-id="c10f4-128">Ранее ILPIP-адрес назывался общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="c10f4-128">In the past, an ILPIP address was referred to as a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="c10f4-129">Управление ILPIP-адресом виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c10f4-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="c10f4-130">Ниже описано, как создавать, назначать и удалять ILPIP-адреса виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c10f4-130">The following tasks enable you to create, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-to-request-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="c10f4-131">Как отправлять запрос на получение ILPIP-адреса на этапе создания виртуальной машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c10f4-131">How to request an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="c10f4-132">Приведенный ниже сценарий PowerShell создает облачную службу *FTPService*, получает образ из Azure, создает на его основе виртуальную машину *FTPInstance*, задает для нее ILPIP-адрес и добавляет эту виртуальную машину в новую службу.</span><span class="sxs-lookup"><span data-stu-id="c10f4-132">The following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using the retrieved image, sets the VM to use an ILPIP, and adds the VM to the new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-to-retrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="c10f4-133">Получение сведений об ILPIP-адресе виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c10f4-133">How to retrieve ILPIP information for a VM</span></span>
<span data-ttu-id="c10f4-134">Чтобы узнать ILPIP-адрес виртуальной машины, созданной с помощью приведенного выше сценария, выполните следующую команду PowerShell и обратите внимание на значения *PublicIPAddress* и *PublicIPName*.</span><span class="sxs-lookup"><span data-stu-id="c10f4-134">To view the ILPIP information for the VM created with the previous script, run the following PowerShell command and observe the values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="c10f4-135">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c10f4-135">Expected output:</span></span>
 
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

### <a name="how-to-remove-an-ilpip-from-a-vm"></a><span data-ttu-id="c10f4-136">Удаление ILPIP-адреса виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c10f4-136">How to remove an ILPIP from a VM</span></span>
<span data-ttu-id="c10f4-137">Чтобы удалить ILPIP-адрес, назначенный виртуальной машине в приведенном выше сценарии, выполните следующую команду PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c10f4-137">To remove the ILPIP added to the VM in the previous script, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-to-add-an-ilpip-to-an-existing-vm"></a><span data-ttu-id="c10f4-138">Назначение ILPIP-адреса существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="c10f4-138">How to add an ILPIP to an existing VM</span></span>
<span data-ttu-id="c10f4-139">Чтобы добавить ILPIP-адрес для виртуальной машины, созданной с помощью приведенного выше сценария, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c10f4-139">To add an ILPIP to the VM created using the script previous, run the following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="c10f4-140">Управление ILPIP-адресом экземпляра роли облачных служб</span><span class="sxs-lookup"><span data-stu-id="c10f4-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="c10f4-141">Чтобы добавить ILPIP-адрес для экземпляра роли облачных служб, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c10f4-141">To add an ILPIP to a Cloud Services role instance, complete the following steps:</span></span>

1. <span data-ttu-id="c10f4-142">Скачайте CSCFG-файл облачной службы, выполнив действия, описанные в статье [Настройка облачных служб](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg).</span><span class="sxs-lookup"><span data-stu-id="c10f4-142">Download the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="c10f4-143">Измените этот CSCFG-файл, добавив в него элемент `InstanceAddress`.</span><span class="sxs-lookup"><span data-stu-id="c10f4-143">Update the .cscfg file by adding the `InstanceAddress` element.</span></span> <span data-ttu-id="c10f4-144">Приведенный ниже пример добавляет ILPIP-адрес *MyPublicIP* для экземпляра роли *WebRole1*.</span><span class="sxs-lookup"><span data-stu-id="c10f4-144">The following sample adds an ILPIP named *MyPublicIP* to a role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="c10f4-145">Передайте CSCFG-файл облачной службы, выполнив действия, описанные в статье [Настройка облачных служб](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg).</span><span class="sxs-lookup"><span data-stu-id="c10f4-145">Upload the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c10f4-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c10f4-146">Next steps</span></span>
* <span data-ttu-id="c10f4-147">Общие сведения об IP-адресах в классической модели развертывания см. в статье [IP-адреса в Azure (классическая модель развертывания)](virtual-network-ip-addresses-overview-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c10f4-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="c10f4-148">Общие сведения о зарезервированных IP-адресах см. в [этой статье](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c10f4-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
