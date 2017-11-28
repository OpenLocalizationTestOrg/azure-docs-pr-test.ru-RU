---
title: "aaaManage Azure зарезервированные IP-адреса (обычная) — PowerShell | Документы Microsoft"
description: "Понимать зарезервированные IP-адреса (классические) и как toomanage их с помощью PowerShell."
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
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="f0afd-103">Зарезервированные IP-адреса (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="f0afd-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0afd-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="f0afd-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="f0afd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0afd-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="f0afd-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="f0afd-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="f0afd-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="f0afd-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="f0afd-108">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="f0afd-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="f0afd-109">IP-адреса в Azure делятся на две категории: динамические и зарезервированные.</span><span class="sxs-lookup"><span data-stu-id="f0afd-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="f0afd-110">Общедоступные IP-адреса, управляемые Azure, являются динамическими по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f0afd-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="f0afd-111">Что означает, что hello IP-адрес используется для данной облачной службы (VIP) или tooaccess виртуальной Машины или изменить непосредственно для экземпляра роли (ILPIP) из tootime времени при останове (освобождении) или завершение работы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f0afd-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="f0afd-112">tooprevent изменять IP-адреса, можно зарезервировать IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0afd-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="f0afd-113">Зарезервированные IP-адреса можно использовать только в качестве виртуального IP-адреса, обеспечивая этот hello IP-адрес для облачной службы hello останется hello таким же, даже если ресурсы, завершают работу или остановлена (освобождена).</span><span class="sxs-lookup"><span data-stu-id="f0afd-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="f0afd-114">Кроме того можно преобразовать существующие динамические IP-адреса, использовать в качестве виртуального IP-адреса tooa зарезервированные IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0afd-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0afd-115">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f0afd-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f0afd-116">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f0afd-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="f0afd-117">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f0afd-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f0afd-118">Узнайте, как статический открытый IP адрес с помощью tooreserve hello [модели развертывания диспетчера ресурсов](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f0afd-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="f0afd-119">toolearn более о IP-адреса в Azure, ознакомьтесь со статьей hello [IP-адреса](virtual-network-ip-addresses-overview-classic.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f0afd-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="f0afd-120">Когда требуется зарезервированный IP-адрес?</span><span class="sxs-lookup"><span data-stu-id="f0afd-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="f0afd-121">**Вы хотите tooensure, hello IP, зарезервированным в подписке**.</span><span class="sxs-lookup"><span data-stu-id="f0afd-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="f0afd-122">Если нужно tooreserve IP-адрес, не освобождается из вашей подписки ни при каких обстоятельствах следует использовать зарезервированный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0afd-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="f0afd-123">**Требуется toostay ваш IP в облачной службе даже через остановлена или освобождена состояние (ВМ)**.</span><span class="sxs-lookup"><span data-stu-id="f0afd-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="f0afd-124">Если вы хотите toobe вашей службы, обращаться с помощью IP-адрес, который не изменяется, даже в том случае, если облака виртуальных машин в hello службы завершение работы или остановки (освобождена).</span><span class="sxs-lookup"><span data-stu-id="f0afd-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="f0afd-125">**Вы хотите tooensure, что исходящий трафик из Azure использует предсказуемого IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="f0afd-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="f0afd-126">Возможно, вашей локальной брандмауэром tooallow трафик только от определенных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f0afd-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="f0afd-127">Резервируя IP-адреса, вы знаете hello исходный IP-адрес адрес и нет необходимости правила брандмауэра из-за изменения IP tooan tooupdate.</span><span class="sxs-lookup"><span data-stu-id="f0afd-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="f0afd-128">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="f0afd-128">FAQ</span></span>
1. <span data-ttu-id="f0afd-129">Можно ли использовать зарезервированный IP-адрес для всех служб Azure?</span><span class="sxs-lookup"><span data-stu-id="f0afd-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="f0afd-130">Нет.</span><span class="sxs-lookup"><span data-stu-id="f0afd-130">No.</span></span> <span data-ttu-id="f0afd-131">Зарезервированные IP-адреса можно использовать только для виртуальных машин и экземпляров ролей облачных служб, представляемых через виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0afd-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="f0afd-132">Сколько зарезервированных IP-адресов можно установить?</span><span class="sxs-lookup"><span data-stu-id="f0afd-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="f0afd-133">Дополнительные сведения см. в разделе hello [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.</span><span class="sxs-lookup"><span data-stu-id="f0afd-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="f0afd-134">Взимается ли плата за зарезервированные IP-адреса?</span><span class="sxs-lookup"><span data-stu-id="f0afd-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="f0afd-135">Иногда.</span><span class="sxs-lookup"><span data-stu-id="f0afd-135">Sometimes.</span></span> <span data-ttu-id="f0afd-136">Сведения о ценах см. в разделе hello [зарезервированные IP адрес сведения о ценах на](http://go.microsoft.com/fwlink/?LinkID=398482) страницы.</span><span class="sxs-lookup"><span data-stu-id="f0afd-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="f0afd-137">Как зарезервировать IP-адрес?</span><span class="sxs-lookup"><span data-stu-id="f0afd-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="f0afd-138">Можно использовать PowerShell, hello [API REST управления Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), или hello [портал Azure](https://portal.azure.com) tooreserve IP-адрес в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="f0afd-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="f0afd-139">Зарезервированный IP-адрес — это связанные tooyour подписка.</span><span class="sxs-lookup"><span data-stu-id="f0afd-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="f0afd-140">Можно ли использовать зарезервированный IP-адрес с виртуальными сетями на основе территориальной группы?</span><span class="sxs-lookup"><span data-stu-id="f0afd-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="f0afd-141">Нет.</span><span class="sxs-lookup"><span data-stu-id="f0afd-141">No.</span></span> <span data-ttu-id="f0afd-142">Зарезервированные IP-адреса поддерживаются только в региональных виртуальных сетях.</span><span class="sxs-lookup"><span data-stu-id="f0afd-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="f0afd-143">Зарезервированные IP-адреса не поддерживаются для виртуальных сетей, которые связаны с территориальными группами.</span><span class="sxs-lookup"><span data-stu-id="f0afd-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="f0afd-144">Дополнительные сведения о связывании виртуальной сети с регион или территориальная группа см. в разделе hello [о региональных виртуальных сетях и территориальных группах](virtual-networks-migrate-to-regional-vnet.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f0afd-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="f0afd-145">Управление зарезервированными виртуальными IP-адресами</span><span class="sxs-lookup"><span data-stu-id="f0afd-145">Manage reserved VIPs</span></span>

<span data-ttu-id="f0afd-146">Убедитесь в наличии установлен и настроен PowerShell, выполнив шаги hello в hello [установить и настроить PowerShell](/powershell/azure/overview) статьи.</span><span class="sxs-lookup"><span data-stu-id="f0afd-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="f0afd-147">Прежде чем использовать зарезервированные IP-адреса, необходимо добавить его tooyour подписки.</span><span class="sxs-lookup"><span data-stu-id="f0afd-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="f0afd-148">toocreate зарезервированный IP-адрес из пула hello общедоступных IP-адресов в hello *центральной части США* расположение, запускать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0afd-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="f0afd-149">Обратите внимание, однако, что нельзя указать, какой IP-адрес будет зарезервирован.</span><span class="sxs-lookup"><span data-stu-id="f0afd-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="f0afd-150">tooview какие IP-адреса зарезервированы в вашу подписку, запустите следующую команду PowerShell hello и обратите внимание, hello значения для *ReservedIPName* и *адрес*:</span><span class="sxs-lookup"><span data-stu-id="f0afd-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="f0afd-151">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f0afd-151">Expected output:</span></span>

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
><span data-ttu-id="f0afd-152">При создании зарезервированный IP-адрес с помощью PowerShell, нельзя указать ресурсов группы toocreate hello зарезервированные IP-адрес в.</span><span class="sxs-lookup"><span data-stu-id="f0afd-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="f0afd-153">Azure по умолчанию помещает его в группу ресурсов с именем *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="f0afd-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="f0afd-154">При создании hello зарезервированные IP с помощью hello [портал Azure](http://portal.azure.com), можно указать любой выбрать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f0afd-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="f0afd-155">При создании hello зарезервированные IP в группе ресурсов не *сети по умолчанию* тем не менее, при ссылках на hello зарезервированный IP-адрес с командами, таких как `Get-AzureReservedIP` и `Remove-AzureReservedIP`, необходимо сослаться на имя hello *Зарезервированное имя группы ресурсов — ip имя группы*.</span><span class="sxs-lookup"><span data-stu-id="f0afd-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="f0afd-156">Например, если создать зарезервированный IP-адрес с именем *myReservedIP* в группу ресурсов с именем *myResourceGroup*, должно ссылаться имя hello hello зарезервированные IP-адрес как *myResourceGroup группы myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="f0afd-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="f0afd-157">После зарезервированные IP-адреса, она остается tooyour связанные подписки, до момента ее удаления.</span><span class="sxs-lookup"><span data-stu-id="f0afd-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="f0afd-158">toodelete зарезервированный IP-адрес выполнения hello следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f0afd-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="f0afd-159">Зарезервировать IP-адрес hello существующей облачной службы</span><span class="sxs-lookup"><span data-stu-id="f0afd-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="f0afd-160">Можно зарезервировать IP-адрес hello существующей облачной службы, добавив hello `-ServiceName` параметра.</span><span class="sxs-lookup"><span data-stu-id="f0afd-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="f0afd-161">tooreserve hello IP-адрес облачной службы *TestService* в hello *центральной части США* расположение, запустите следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="f0afd-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="f0afd-162">Связать зарезервированный IP tooa новой облачной службы</span><span class="sxs-lookup"><span data-stu-id="f0afd-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="f0afd-163">Hello следующий скрипт создает новые зарезервированные IP, а затем связывает его tooa новой облачной службы с именем *TestService*.</span><span class="sxs-lookup"><span data-stu-id="f0afd-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="f0afd-164">При создании зарезервированные toouse IP для облачной службы, вы по-прежнему ссылаться toohello виртуальной Машины с помощью *виртуального IP-адреса:&lt;номер порта >* для входящих сообщений.</span><span class="sxs-lookup"><span data-stu-id="f0afd-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="f0afd-165">Резервирование IP-адреса не означает, что toohello виртуальной Машины можно подключаться напрямую.</span><span class="sxs-lookup"><span data-stu-id="f0afd-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="f0afd-166">Hello зарезервированный IP-адрес назначается toohello облачной службы, hello, в которой развернута виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="f0afd-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="f0afd-167">Если требуется напрямую tooconnect tooa ВМ по IP-Адресу tooconfigure имеется открытый IP-адрес уровня экземпляра.</span><span class="sxs-lookup"><span data-stu-id="f0afd-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="f0afd-168">Открытый IP-адрес уровня экземпляра — это тип общедоступный IP-адрес (называемых ILPIP), назначенный непосредственно tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f0afd-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="f0afd-169">Его нельзя зарезервировать.</span><span class="sxs-lookup"><span data-stu-id="f0afd-169">It cannot be reserved.</span></span> <span data-ttu-id="f0afd-170">Дополнительные сведения см. в статье hello [уровня экземпляра открытый IP (ILPIP)](virtual-networks-instance-level-public-ip.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f0afd-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="f0afd-171">Удаление зарезервированного IP-адреса из работающей развернутой системы</span><span class="sxs-lookup"><span data-stu-id="f0afd-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="f0afd-172">tooremove зарезервированный IP-адрес добавлен tooa новой облачной службы, запустите следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="f0afd-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="f0afd-173">Удаление зарезервированного IP-адреса из выполняющегося развертывания не удаляет резервирование hello из подписки.</span><span class="sxs-lookup"><span data-stu-id="f0afd-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="f0afd-174">Он просто освобождает hello IP toobe используется другим ресурсом в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="f0afd-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="f0afd-175">Связать зарезервированный tooa IP выполнение развертывания</span><span class="sxs-lookup"><span data-stu-id="f0afd-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="f0afd-176">Hello следующие команды создают облачная служба с именем *TestService2* с новой виртуальной Машины с именем *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="f0afd-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="f0afd-177">Hello существующий зарезервированный IP-адрес с именем *MyReservedIP* имеет связанный toohello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="f0afd-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="f0afd-178">Связать зарезервированный IP tooa облачной службы с помощью файла конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="f0afd-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="f0afd-179">Также можно связать зарезервированный IP tooa облачной службы с помощью файла конфигурации (CSCFG) службы.</span><span class="sxs-lookup"><span data-stu-id="f0afd-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="f0afd-180">Hello следующий образец xml показано как tooconfigure облачной службы toouse зарезервированного виртуального IP-адреса с именем *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="f0afd-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f0afd-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0afd-181">Next steps</span></span>
* <span data-ttu-id="f0afd-182">Понять, как [IP-адресация](virtual-network-ip-addresses-overview-classic.md) работает в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f0afd-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="f0afd-183">Ознакомьтесь с информацией о [зарезервированных частных IP-адресах](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="f0afd-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="f0afd-184">Ознакомьтесь с информацией об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="f0afd-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

