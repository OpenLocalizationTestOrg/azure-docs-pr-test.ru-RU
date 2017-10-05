---
title: "Управление зарезервированными IP-адресами Azure (классическая модель) с помощью PowerShell | Документация Майкрософт"
description: "Сведения о зарезервированных IP-адресах (классическая модель) и управлении ими с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 5e9c83cebec96c6bc8afd53b0c637d7af899746f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="c65fc-103">Зарезервированные IP-адреса (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="c65fc-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c65fc-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c65fc-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="c65fc-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c65fc-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="c65fc-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="c65fc-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="c65fc-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="c65fc-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="c65fc-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="c65fc-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="c65fc-109">IP-адреса в Azure делятся на две категории: динамические и зарезервированные.</span><span class="sxs-lookup"><span data-stu-id="c65fc-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="c65fc-110">Общедоступные IP-адреса, управляемые Azure, являются динамическими по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c65fc-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="c65fc-111">Это означает, что IP-адрес, используемый для указанной облачной службы (VIP) или для прямого доступа к виртуальной машине или экземпляру роли (ILPIP), время от времени может изменяться, при отключении или остановке (высвобождении) ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c65fc-111">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="c65fc-112">Чтобы предотвратить изменение IP-адресов, можно зарезервировать IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c65fc-112">To prevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="c65fc-113">Зарезервированные IP-адреса можно использовать только в качестве виртуального IP-адреса (VIP). В этом случае IP-адрес облачной службы будет сохраняться даже при отключении или остановке (высвобождении) ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c65fc-113">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="c65fc-114">Кроме того, можно преобразовать существующие динамические IP-адреса, используемые в качестве виртуального IP-адреса, в зарезервированный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c65fc-114">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c65fc-115">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c65fc-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c65fc-116">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="c65fc-116">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c65fc-117">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c65fc-117">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c65fc-118">Сведения о том, как зарезервировать статический общедоступный IP-адрес, используя модель развертывания с помощью Resource Manager, см. [здесь](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c65fc-118">Learn how to reserve a static public IP address using the [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="c65fc-119">Дополнительные сведения об IP-адресах в Azure см. в [этой статье](virtual-network-ip-addresses-overview-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c65fc-119">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="c65fc-120">Когда требуется зарезервированный IP-адрес?</span><span class="sxs-lookup"><span data-stu-id="c65fc-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="c65fc-121">**Необходимо обеспечить резервирование IP-адреса в подписке**.</span><span class="sxs-lookup"><span data-stu-id="c65fc-121">**You want to ensure that the IP is reserved in your subscription**.</span></span> <span data-ttu-id="c65fc-122">Если вам нужен постоянный IP-адрес, который будет в любых обстоятельствах связан с подпиской, следует использовать зарезервированный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c65fc-122">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="c65fc-123">**Необходимо сохранять IP-адрес облачной службы даже в случае остановленного или высвобожденного состояния (виртуальных машин)**.</span><span class="sxs-lookup"><span data-stu-id="c65fc-123">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="c65fc-124">Если требуется доступ к службе по IP-адресу, который не изменится, даже если виртуальные машины в облачной службе будут отключены или остановлены (высвобождены).</span><span class="sxs-lookup"><span data-stu-id="c65fc-124">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="c65fc-125">**Необходимо обеспечить предсказуемый IP-адрес для исходящего трафика из Azure**.</span><span class="sxs-lookup"><span data-stu-id="c65fc-125">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="c65fc-126">Возможно, настройки локального брандмауэра разрешают трафик только с определенных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c65fc-126">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span></span> <span data-ttu-id="c65fc-127">Резервирование IP-адреса позволяет всегда знать IP-адрес источника и избавляет от необходимости изменять правила брандмауэра из-за смены адреса.</span><span class="sxs-lookup"><span data-stu-id="c65fc-127">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="c65fc-128">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="c65fc-128">FAQ</span></span>
1. <span data-ttu-id="c65fc-129">Можно ли использовать зарезервированный IP-адрес для всех служб Azure?</span><span class="sxs-lookup"><span data-stu-id="c65fc-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="c65fc-130">Нет.</span><span class="sxs-lookup"><span data-stu-id="c65fc-130">No.</span></span> <span data-ttu-id="c65fc-131">Зарезервированные IP-адреса можно использовать только для виртуальных машин и экземпляров ролей облачных служб, представляемых через виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c65fc-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="c65fc-132">Сколько зарезервированных IP-адресов можно установить?</span><span class="sxs-lookup"><span data-stu-id="c65fc-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="c65fc-133">Дополнительные сведения см. в разделе [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.</span><span class="sxs-lookup"><span data-stu-id="c65fc-133">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="c65fc-134">Взимается ли плата за зарезервированные IP-адреса?</span><span class="sxs-lookup"><span data-stu-id="c65fc-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="c65fc-135">Иногда.</span><span class="sxs-lookup"><span data-stu-id="c65fc-135">Sometimes.</span></span> <span data-ttu-id="c65fc-136">Сведения о ценах на зарезервированные IP-адреса см. на [этой странице](http://go.microsoft.com/fwlink/?LinkID=398482).</span><span class="sxs-lookup"><span data-stu-id="c65fc-136">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="c65fc-137">Как зарезервировать IP-адрес?</span><span class="sxs-lookup"><span data-stu-id="c65fc-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="c65fc-138">Можно использовать PowerShell, [API REST управления Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), или [портал Azure](https://portal.azure.com) зарезервировать IP-адрес в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="c65fc-138">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span></span> <span data-ttu-id="c65fc-139">Зарезервированный IP-адрес связывается с подпиской.</span><span class="sxs-lookup"><span data-stu-id="c65fc-139">A reserved IP address is associated to your subscription.</span></span>
5. <span data-ttu-id="c65fc-140">Можно ли использовать зарезервированный IP-адрес с виртуальными сетями на основе территориальной группы?</span><span class="sxs-lookup"><span data-stu-id="c65fc-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="c65fc-141">Нет.</span><span class="sxs-lookup"><span data-stu-id="c65fc-141">No.</span></span> <span data-ttu-id="c65fc-142">Зарезервированные IP-адреса поддерживаются только в региональных виртуальных сетях.</span><span class="sxs-lookup"><span data-stu-id="c65fc-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="c65fc-143">Зарезервированные IP-адреса не поддерживаются для виртуальных сетей, которые связаны с территориальными группами.</span><span class="sxs-lookup"><span data-stu-id="c65fc-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="c65fc-144">Дополнительные сведения о связывании виртуальной сети с регионом или территориальной группой см. в статье [Переход от территориальных групп к региональной виртуальной сети](virtual-networks-migrate-to-regional-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="c65fc-144">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="c65fc-145">Управление зарезервированными виртуальными IP-адресами</span><span class="sxs-lookup"><span data-stu-id="c65fc-145">Manage reserved VIPs</span></span>

<span data-ttu-id="c65fc-146">Установите и настройте PowerShell, выполнив действия, описанные в [этой статье](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c65fc-146">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="c65fc-147">Прежде чем можно будет использовать зарезервированные IP-адреса, их необходимо добавить в подписку.</span><span class="sxs-lookup"><span data-stu-id="c65fc-147">Before you can use reserved IPs, you must add it to your subscription.</span></span> <span data-ttu-id="c65fc-148">Чтобы создать зарезервированный IP-адрес из пула общедоступных IP-адресов в *центральной части США*, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c65fc-148">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="c65fc-149">Обратите внимание, однако, что нельзя указать, какой IP-адрес будет зарезервирован.</span><span class="sxs-lookup"><span data-stu-id="c65fc-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="c65fc-150">Чтобы просмотреть, какие IP-адреса зарезервированы в подписке, выполните следующую команду PowerShell и обратите внимание на значения *ReservedIPName* и *Address*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-150">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="c65fc-151">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c65fc-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="c65fc-152">Если вы создаете зарезервированный IP-адрес с помощью PowerShell, вы не можете указать группу ресурсов, в которой нужно создать зарезервированный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c65fc-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group to create the reserved IP in.</span></span> <span data-ttu-id="c65fc-153">Azure по умолчанию помещает его в группу ресурсов с именем *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="c65fc-154">Если вы создаете зарезервированный IP-адрес с помощью [портала Azure](http://portal.azure.com), вы можете указать для него любую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c65fc-154">If you create the reserved IP using the [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="c65fc-155">Но если зарезервированный IP-адрес создается в любой другой группе ресурсов, кроме *Default-Networking*, все обращения к этому зарезервированному IP-адресу в любых командах, например `Get-AzureReservedIP` или `Remove-AzureReservedIP`, должны выполняться по полному имени *группа_имя_группы_ресурсов имя_зарезервированного_IP-адреса*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-155">If you create the reserved IP in a resource group other than *Default-Networking* however, whenever you reference the reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference the name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="c65fc-156">Например, если вы создадите зарезервированный IP-адрес с именем *myReservedIP* в группе ресурсов с именем *myResourceGroup*, ссылки на него должны иметь такой вид: *Group myResourceGroup myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference the name of the reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="c65fc-157">После того как IP-адрес будет зарезервирован, он останется связан с подпиской до тех пор, пока вы ее не удалите.</span><span class="sxs-lookup"><span data-stu-id="c65fc-157">Once an IP is reserved, it remains associated to your subscription until you delete it.</span></span> <span data-ttu-id="c65fc-158">Чтобы удалить зарезервированный IP-адрес, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c65fc-158">To delete a reserved IP, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-the-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="c65fc-159">Резервирование IP-адреса существующей облачной службы</span><span class="sxs-lookup"><span data-stu-id="c65fc-159">Reserve the IP address of an existing cloud service</span></span>
<span data-ttu-id="c65fc-160">Можно зарезервировать IP-адрес существующей облачной службы, добавив параметр `-ServiceName`.</span><span class="sxs-lookup"><span data-stu-id="c65fc-160">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span></span> <span data-ttu-id="c65fc-161">Чтобы зарезервировать IP-адрес облачной службы *TestService* в расположении *центральная часть США*, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c65fc-161">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-to-a-new-cloud-service"></a><span data-ttu-id="c65fc-162">Связывание зарезервированного IP-адреса с новой облачной службой</span><span class="sxs-lookup"><span data-stu-id="c65fc-162">Associate a reserved IP to a new cloud service</span></span>
<span data-ttu-id="c65fc-163">Приведенный ниже скрипт создает новый зарезервированный IP-адрес и связывает его с новой облачной службой с именем *TestService*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-163">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="c65fc-164">Если вы создадите зарезервированный IP-адрес для облачной службы, обращения к виртуальной машине для входящей связи по-прежнему выполняются в формате *виртуальный_IP-адрес:&lt;номер порта>*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-164">When you create a reserved IP to use with a cloud service, you still refer to the VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="c65fc-165">Резервирование IP-адреса не означает возможность прямого подключения к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c65fc-165">Reserving an IP does not mean you can connect to the VM directly.</span></span> <span data-ttu-id="c65fc-166">Зарезервированный IP-адрес назначается облачной службе, в которой развернута виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="c65fc-166">The reserved IP is assigned to the cloud service that the VM has been deployed to.</span></span> <span data-ttu-id="c65fc-167">Если требуется подключиться непосредственно к виртуальной машине по IP-адресу, следует настроить общедоступный IP-адрес уровня экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c65fc-167">If you want to connect to a VM by IP directly, you have to configure an instance-level public IP.</span></span> <span data-ttu-id="c65fc-168">Общедоступный IP-адрес уровня экземпляра — это тип общедоступного IP-адреса (называемый ILPIP), который назначается непосредственно виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c65fc-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly to your VM.</span></span> <span data-ttu-id="c65fc-169">Его нельзя зарезервировать.</span><span class="sxs-lookup"><span data-stu-id="c65fc-169">It cannot be reserved.</span></span> <span data-ttu-id="c65fc-170">Дополнительные сведения см. в статье [Общие сведения об общедоступных IP-адресах уровня экземпляра (классическая модель развертывания)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c65fc-170">For more information, read the [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="c65fc-171">Удаление зарезервированного IP-адреса из работающей развернутой системы</span><span class="sxs-lookup"><span data-stu-id="c65fc-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="c65fc-172">Чтобы удалить зарезервированный IP-адрес, добавленный в облачную службу, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c65fc-172">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="c65fc-173">При удалении зарезервированного IP-адреса из работающей развернутой системы резервирование не удаляется из вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="c65fc-173">Removing a reserved IP from a running deployment does not remove the reservation from your subscription.</span></span> <span data-ttu-id="c65fc-174">IP-адрес просто освобождается для использования другим ресурсом в подписке.</span><span class="sxs-lookup"><span data-stu-id="c65fc-174">It simply frees the IP to be used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-to-a-running-deployment"></a><span data-ttu-id="c65fc-175">Связывание зарезервированного IP-адреса с работающей развернутой системой</span><span class="sxs-lookup"><span data-stu-id="c65fc-175">Associate a reserved IP to a running deployment</span></span>
<span data-ttu-id="c65fc-176">Следующие команды создают облачную службу с именем *TestService2*, к которой прикреплена новая виртуальная машина с именем *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-176">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="c65fc-177">Затем с этой облачной службой связывается существующий зарезервированный IP-адрес с именем *MyReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-177">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="c65fc-178">Связывание зарезервированного IP-адреса с облачной службой с помощью файла конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="c65fc-178">Associate a reserved IP to a cloud service by using a service configuration file</span></span>
<span data-ttu-id="c65fc-179">Зарезервированный IP-адрес можно также связать с облачной службой с помощью файла конфигурации службы (CSCFG).</span><span class="sxs-lookup"><span data-stu-id="c65fc-179">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="c65fc-180">В приведенном ниже XML-коде показано, как настроить облачную службу для использования зарезервированного виртуального IP-адреса с именем *MyReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="c65fc-180">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="c65fc-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c65fc-181">Next steps</span></span>
* <span data-ttu-id="c65fc-182">Общие сведения об IP-адресах в классической модели развертывания см. в [этой статье](virtual-network-ip-addresses-overview-classic.md).</span><span class="sxs-lookup"><span data-stu-id="c65fc-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="c65fc-183">Ознакомьтесь с информацией о [зарезервированных частных IP-адресах](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c65fc-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="c65fc-184">Ознакомьтесь с информацией об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="c65fc-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

