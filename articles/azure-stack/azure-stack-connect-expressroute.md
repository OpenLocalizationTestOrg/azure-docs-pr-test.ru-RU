---
title: "Подключиться к Azure с помощью ExpressRoute стек Azure"
description: "Способ подключения виртуальных сетей в Azure стека виртуальных сетей в Azure с помощью ExpressRoute."
services: azure-stack
documentationcenter: 
author: victorar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: victorh
ms.openlocfilehash: aa6973939c6cfe0688f5781fdcea5d39670249df
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="connect-azure-stack-to-azure-using-expressroute"></a><span data-ttu-id="c9ea7-103">Подключиться к Azure с помощью ExpressRoute стек Azure</span><span class="sxs-lookup"><span data-stu-id="c9ea7-103">Connect Azure Stack to Azure using ExpressRoute</span></span>

<span data-ttu-id="c9ea7-104">*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*</span><span class="sxs-lookup"><span data-stu-id="c9ea7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="c9ea7-105">Существует два поддерживаемых методов для подключения к виртуальной сети в Azure виртуальные сети в Azure стека:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-105">There are two supported methods to connect virtual networks in Azure Stack to virtual networks in Azure:</span></span>
   * <span data-ttu-id="c9ea7-106">**Сеть-сеть**</span><span class="sxs-lookup"><span data-stu-id="c9ea7-106">**Site-to-Site**</span></span>

     <span data-ttu-id="c9ea7-107">VPN-подключение по IPsec (IKE v1 и IKE v2).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-107">A VPN connection over IPsec (IKE v1 and IKE v2).</span></span> <span data-ttu-id="c9ea7-108">Для этого типа подключения требуется VPN-устройство или RRAS.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-108">This type of connection requires a VPN device or RRAS.</span></span> <span data-ttu-id="c9ea7-109">Дополнительные сведения см. в разделе [подключения стек Azure в Azure с помощью VPN](azure-stack-connect-vpn.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-109">For more information, see [Connect Azure Stack to Azure using VPN](azure-stack-connect-vpn.md).</span></span>
   * <span data-ttu-id="c9ea7-110">**ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="c9ea7-110">**ExpressRoute**</span></span>

     <span data-ttu-id="c9ea7-111">Прямое подключение к Azure из развертывания Azure стека.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-111">A direct connection to Azure from your Azure Stack deployment.</span></span> <span data-ttu-id="c9ea7-112">ExpressRoute — **не** VPN-подключения через общедоступный Интернет.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-112">ExpressRoute is **not** a VPN connection over the public Internet.</span></span> <span data-ttu-id="c9ea7-113">Дополнительные сведения об Azure ExpressRoute см. в разделе [Обзор ExpressRoute](../expressroute/expressroute-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-113">For more information about Azure ExpressRoute, see [ExpressRoute overview](../expressroute/expressroute-introduction.md).</span></span>

<span data-ttu-id="c9ea7-114">В этой статье показан пример использования ExpressRoute для подключения к Azure Azure стека.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-114">This article shows an example using ExpressRoute to connect Azure Stack to Azure.</span></span>
## <a name="requirements"></a><span data-ttu-id="c9ea7-115">Требования</span><span class="sxs-lookup"><span data-stu-id="c9ea7-115">Requirements</span></span>
<span data-ttu-id="c9ea7-116">Ниже приведены особые требования для подключения стек Azure и Azure с помощью ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-116">The following are specific requirements to connect Azure Stack and Azure using ExpressRoute:</span></span>
* <span data-ttu-id="c9ea7-117">Подписка Azure для создания каналов expressroute и виртуальных сетей в Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-117">An Azure subscription to create an ExpressRoute circuit and VNets in Azure.</span></span>
* <span data-ttu-id="c9ea7-118">Объект подготовить канал ExpressRoute через [поставщика услуг подключения](../expressroute/expressroute-locations.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-118">A provisioned ExpressRoute circuit through a [connectivity provider](../expressroute/expressroute-locations.md).</span></span>
* <span data-ttu-id="c9ea7-119">Маршрутизатор, который был подключен к его WAN портов канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-119">A router that has the ExpressRoute circuit connected to its WAN ports.</span></span>
* <span data-ttu-id="c9ea7-120">Мультитенантный шлюз стек Azure связан стороне маршрутизатора локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-120">The LAN side of the router is linked to the Azure Stack Multitenant Gateway.</span></span>
* <span data-ttu-id="c9ea7-121">Маршрутизатор должен поддерживать через виртуальную Частную сеть для подключений между его интерфейса локальной сети и мультитенантный шлюз Azure стека.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-121">The router must support Site-to-Site VPN connections between its LAN interface and Azure Stack Multitenant Gateway.</span></span>
* <span data-ttu-id="c9ea7-122">Если более чем одного клиента добавляется в развертывании Azure стека, маршрутизатор необходима для создания нескольких Vrf (виртуальный маршрутизации и пересылки).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-122">If more than one tenant is added in your Azure Stack deployment, the router must be able to create multiple VRFs (Virtual Routing and Forwarding).</span></span>

<span data-ttu-id="c9ea7-123">На следующей диаграмме показан концептуальное представление сети после завершения настройки:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-123">The following diagram shows a conceptual networking view after you complete the configuration:</span></span>

![Концептуальная схема](media/azure-stack-connect-expressroute/Conceptual.png)

<span data-ttu-id="c9ea7-125">**На рис. 1**</span><span class="sxs-lookup"><span data-stu-id="c9ea7-125">**Diagram 1**</span></span>

<span data-ttu-id="c9ea7-126">В примере ниже показан архитектура как несколько клиентов соединиться с инфраструктурой Azure стека через маршрутизатор ExpressRoute Azure на границе Microsoft:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-126">The following architecture diagram shows how multiple tenants connect from the Azure Stack infrastructure through the ExpressRoute router to Azure at the Microsoft edge:</span></span>

![Схема архитектуры](media/azure-stack-connect-expressroute/Architecture.png)

<span data-ttu-id="c9ea7-128">**Схема 2**</span><span class="sxs-lookup"><span data-stu-id="c9ea7-128">**Diagram 2**</span></span>

<span data-ttu-id="c9ea7-129">Пример, приведенный в этом разделе использует ту же архитектуру для подключения к Azure через частного пиринга ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-129">The example shown in this article uses the same architecture to connect to Azure via ExpressRoute private peering.</span></span> <span data-ttu-id="c9ea7-130">Это можно сделать с помощью через виртуальную Частную сеть для подключения через шлюз виртуальной сети Azure стека маршрутизатор ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-130">It is done using a Site-to-Site VPN connection from the virtual network gateway in Azure Stack to an ExpressRoute router.</span></span> <span data-ttu-id="c9ea7-131">Следующие шаги в этой статье показано, как создание конца в конец соединения между двумя виртуальных сетей от двух разных клиентов в стек Azure для их соответствующих виртуальных сетей в Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-131">The following steps in this article show how to create an end-to-end connection between two VNets from two different tenants in Azure Stack to their respective VNets in Azure.</span></span> <span data-ttu-id="c9ea7-132">Можно добавить как многие клиента виртуальных сетей и реплицировать шаги для каждого клиента или использовать этот пример развертывание только одного клиента виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-132">You can choose to add as many tenant VNets and replicate the steps for each tenant or use this example to deploy just a single tenant VNet.</span></span>

## <a name="configure-azure-stack"></a><span data-ttu-id="c9ea7-133">Настройка стек Azure</span><span class="sxs-lookup"><span data-stu-id="c9ea7-133">Configure Azure Stack</span></span>
<span data-ttu-id="c9ea7-134">Теперь можно создать ресурсов, необходимых для настройки среды Azure стека как клиента.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-134">Now you create the resources you need to set up your Azure Stack environment as a tenant.</span></span> <span data-ttu-id="c9ea7-135">Следующие шаги иллюстрируют, вам нужно.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-135">The following steps illustrate what you need to do.</span></span> <span data-ttu-id="c9ea7-136">Эти инструкции показано, как создать ресурсы с помощью портала Azure стека, но можно также использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-136">These instructions show how to create resources using the Azure Stack portal, but you can also use PowerShell.</span></span>

![Действия сетевых ресурсов](media/azure-stack-connect-expressroute/image2.png)
### <a name="before-you-begin"></a><span data-ttu-id="c9ea7-138">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c9ea7-138">Before you begin</span></span>
<span data-ttu-id="c9ea7-139">Перед началом настройки необходимо:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-139">Before you start the configuration, you need:</span></span>
* <span data-ttu-id="c9ea7-140">Развертывания служб Azure стека.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-140">An Azure Stack deployment.</span></span>

   <span data-ttu-id="c9ea7-141">Сведения о развертывании пакета средств разработки стек Azure см. в разделе [краткое руководство для развертывания пакета средств разработки Azure стека](azure-stack-deploy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-141">For information about deploying Azure Stack Development Kit, see [Azure Stack Development Kit deployment quickstart](azure-stack-deploy-overview.md).</span></span>
* <span data-ttu-id="c9ea7-142">Стек Azure, пользователь может подписаться на предложение.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-142">An offer on Azure Stack that your user can subscribe to.</span></span>

  <span data-ttu-id="c9ea7-143">Инструкции см. в разделе [доступность виртуальных машин для пользователей Azure стека](azure-stack-tutorial-tenant-vm.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-143">For instructions, see [Make virtual machines available to your Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span></span>

### <a name="create-network-resources-in-azure-stack"></a><span data-ttu-id="c9ea7-144">Создание сетевых ресурсов в стек Azure</span><span class="sxs-lookup"><span data-stu-id="c9ea7-144">Create network resources in Azure Stack</span></span>

<span data-ttu-id="c9ea7-145">Используйте следующие процедуры для создания требуемым сетевым ресурсам в Azure стека для каждого клиента:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-145">Use the following procedures to create the required network resources in Azure Stack for each tenant:</span></span>

#### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="c9ea7-146">Создание виртуальной сети и подсети виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c9ea7-146">Create the virtual network and VM subnet</span></span>
1. <span data-ttu-id="c9ea7-147">Войдите в портал пользователей с учетной записью пользователя (клиента).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-147">Sign in the user portal with a user (tenant) account.</span></span>

2. <span data-ttu-id="c9ea7-148">На портале щелкните **New**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-148">In the portal, click **New**.</span></span>

   ![](media/azure-stack-connect-expressroute/MAS-new.png)

3. <span data-ttu-id="c9ea7-149">В меню Marketplace выберите **Сети**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-149">Select **Networking** from the Marketplace menu.</span></span>

4. <span data-ttu-id="c9ea7-150">В меню щелкните **Виртуальная сеть**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-150">Click **Virtual network** on the menu.</span></span>

5. <span data-ttu-id="c9ea7-151">Введите значения в соответствующие поля, используйте следующую таблицу:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-151">Type the values into the appropriate fields using the following table:</span></span>

   |<span data-ttu-id="c9ea7-152">Поле</span><span class="sxs-lookup"><span data-stu-id="c9ea7-152">Field</span></span>  |<span data-ttu-id="c9ea7-153">Значение</span><span class="sxs-lookup"><span data-stu-id="c9ea7-153">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="c9ea7-154">Имя</span><span class="sxs-lookup"><span data-stu-id="c9ea7-154">Name</span></span>     |<span data-ttu-id="c9ea7-155">Tenant1VNet1</span><span class="sxs-lookup"><span data-stu-id="c9ea7-155">Tenant1VNet1</span></span>         |
   |<span data-ttu-id="c9ea7-156">Пространство адресов</span><span class="sxs-lookup"><span data-stu-id="c9ea7-156">Address space</span></span>     |<span data-ttu-id="c9ea7-157">10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c9ea7-157">10.1.0.0/16</span></span>|
   |<span data-ttu-id="c9ea7-158">Имя подсети</span><span class="sxs-lookup"><span data-stu-id="c9ea7-158">Subnet name</span></span>     |<span data-ttu-id="c9ea7-159">Sub1 клиента (1)</span><span class="sxs-lookup"><span data-stu-id="c9ea7-159">Tenant1-Sub1</span></span>|
   |<span data-ttu-id="c9ea7-160">Диапазон адресов подсети</span><span class="sxs-lookup"><span data-stu-id="c9ea7-160">Subnet address range</span></span>     |<span data-ttu-id="c9ea7-161">10.1.1.0/24</span><span class="sxs-lookup"><span data-stu-id="c9ea7-161">10.1.1.0/24</span></span>|

6. <span data-ttu-id="c9ea7-162">В поле **Подписка** должна появиться созданная ранее подписка.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-162">You should see the Subscription you created earlier populated in the **Subscription** field.</span></span>

    <span data-ttu-id="c9ea7-163">а.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-163">a.</span></span> <span data-ttu-id="c9ea7-164">Для группы ресурсов, можно создать группу ресурсов или если это уже сделано, установите **использовать существующие**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-164">For Resource Group, you can either create a Resource Group or if you already have one, select **Use existing**.</span></span>

    <span data-ttu-id="c9ea7-165">b.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-165">b.</span></span> <span data-ttu-id="c9ea7-166">Проверьте значение расположения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-166">Verify the default location.</span></span>

    <span data-ttu-id="c9ea7-167">c.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-167">c.</span></span> <span data-ttu-id="c9ea7-168">Щелкните **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-168">Click **Pin to dashboard**.</span></span>

    <span data-ttu-id="c9ea7-169">d.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-169">d.</span></span> <span data-ttu-id="c9ea7-170">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-170">Click **Create**.</span></span>



#### <a name="create-the-gateway-subnet"></a><span data-ttu-id="c9ea7-171">Создание подсети шлюза</span><span class="sxs-lookup"><span data-stu-id="c9ea7-171">Create the gateway subnet</span></span>
1. <span data-ttu-id="c9ea7-172">Откройте ресурс виртуальной сети, вы создали (Tenant1VNet1) на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-172">Open the Virtual Network resource you created (Tenant1VNet1) from the dashboard.</span></span>
2. <span data-ttu-id="c9ea7-173">В разделе «Параметры» выберите **подсети**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-173">On the Settings section, select **Subnets**.</span></span>
3. <span data-ttu-id="c9ea7-174">Щелкните **Подсеть шлюза**, чтобы добавить подсеть шлюза в виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-174">Click **Gateway Subnet** to add a gateway subnet to the virtual network.</span></span>
   
    ![](media/azure-stack-connect-expressroute/gatewaysubnet.png)
4. <span data-ttu-id="c9ea7-175">Подсети присвоено имя **GatewaySubnet** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-175">The name of the subnet is set to **GatewaySubnet** by default.</span></span>
   <span data-ttu-id="c9ea7-176">Подсети шлюза являются специальными, и для правильной работы им должно быть присвоено конкретное имя.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-176">Gateway subnets are special and must have this specific name to function properly.</span></span>
5. <span data-ttu-id="c9ea7-177">В **диапазона адресов** поле, убедитесь, что адрес **10.1.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-177">In the **Address range** field, verify the address is **10.1.0.0/24**.</span></span>
6. <span data-ttu-id="c9ea7-178">Нажмите кнопку **ОК**, чтобы создать подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-178">Click **OK** to create the gateway subnet.</span></span>

#### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="c9ea7-179">Создание шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c9ea7-179">Create the virtual network gateway</span></span>
1. <span data-ttu-id="c9ea7-180">На портале Azure стека пользователя щелкните **New**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-180">In the Azure Stack user portal, click **New**.</span></span>
   
2. <span data-ttu-id="c9ea7-181">В меню Marketplace выберите **Сети**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-181">Select **Networking** from the Marketplace menu.</span></span>
3. <span data-ttu-id="c9ea7-182">В списке сетевых ресурсов выберите **Шлюз виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-182">Select **Virtual network gateway** from the list of network resources.</span></span>
4. <span data-ttu-id="c9ea7-183">В поле **Имя** введите **GW1**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-183">In the **Name** field type **GW1**.</span></span>
5. <span data-ttu-id="c9ea7-184">Щелкните пункт **Виртуальная сеть**, чтобы выбрать виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-184">Click the **Virtual network** item to choose a virtual network.</span></span>
   <span data-ttu-id="c9ea7-185">Выберите **Tenant1VNet1** из списка.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-185">Select **Tenant1VNet1** from the list.</span></span>
6. <span data-ttu-id="c9ea7-186">Щелкните пункт меню **Общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-186">Click the **Public IP address** menu item.</span></span> <span data-ttu-id="c9ea7-187">Когда **выберите общедоступный IP-адрес** раздел откроется щелкните **создать новый**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-187">When the **Choose public IP address** section opens click **Create new**.</span></span>
7. <span data-ttu-id="c9ea7-188">В поле **Имя** введите **GW1-PiP** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-188">In the **Name** field, type **GW1-PiP** and click **OK**.</span></span>
8. <span data-ttu-id="c9ea7-189">Для параметра **Тип VPN** должно быть установлено значение **Route-based** (На основе маршрутов) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-189">The **VPN type** should have **Route-based** selected by default.</span></span>
    <span data-ttu-id="c9ea7-190">Не изменяйте значение этого параметра.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-190">Keep this setting.</span></span>
9. <span data-ttu-id="c9ea7-191">Убедитесь, что для параметров **Подписка** и **Расположение** выбраны правильные значения.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-191">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="c9ea7-192">Если требуется, вы можете закрепить ресурсов на панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-192">You can pin the resource to the Dashboard if you want.</span></span> <span data-ttu-id="c9ea7-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-193">Click **Create**.</span></span>

#### <a name="create-the-local-network-gateway"></a><span data-ttu-id="c9ea7-194">Создание шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="c9ea7-194">Create the local network gateway</span></span>

<span data-ttu-id="c9ea7-195">Ресурс шлюза локальной сети предназначена для указания удаленного шлюза на другом конце VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-195">The purpose of the Local network gateway resource is to indicate the remote gateway at the other end of the VPN connection.</span></span> <span data-ttu-id="c9ea7-196">Например удаленная сторона является подчиненный локальной сети, интерфейс маршрутизатора ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-196">For this example, the remote side is the LAN subinterface of the ExpressRoute router.</span></span> <span data-ttu-id="c9ea7-197">Для клиента 1 в этом примере удаленный адрес — 10.60.3.255, как показано на рис. 2.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-197">For Tenant 1 in this example, the remote address is 10.60.3.255 as shown in Diagram 2.</span></span>

1. <span data-ttu-id="c9ea7-198">Войдите в систему физического компьютера Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-198">Log in to the Azure Stack physical machine.</span></span>
2. <span data-ttu-id="c9ea7-199">Войдите на пользовательский портал с помощью учетной записи пользователя и нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-199">Sign in to the user portal with your user account and click **New**.</span></span>
3. <span data-ttu-id="c9ea7-200">В меню Marketplace выберите **Сети**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-200">Select **Networking** from the Marketplace menu.</span></span>
4. <span data-ttu-id="c9ea7-201">В списке сетевых ресурсов выберите **шлюз локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-201">Select **local network gateway** from the list of resources.</span></span>
5. <span data-ttu-id="c9ea7-202">В **имя** тип поля **ER-маршрутизатор-GW**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-202">In the **Name** field type **ER-Router-GW**.</span></span>
6. <span data-ttu-id="c9ea7-203">Для **IP-адрес** полей см. рис. 2.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-203">For the **IP address** field, refer to Diagram 2.</span></span> <span data-ttu-id="c9ea7-204">IP-адрес подчиненный интерфейс локальной сети маршрутизатор ExpressRoute для клиента 1 — 10.60.3.255.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-204">The IP address of the ExpressRoute router's LAN subinterface for Tenant 1 is 10.60.3.255.</span></span> <span data-ttu-id="c9ea7-205">Для среды введите IP-адрес маршрутизатора соответствующий интерфейс.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-205">For your own environment, type the IP address of your router's corresponding interface.</span></span>
7. <span data-ttu-id="c9ea7-206">В **адресное пространство** введите адресное пространство виртуальных сетей, который требуется подключить к Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-206">In the **Address Space** field, type the address space of the VNets that you want to connect to in Azure.</span></span> <span data-ttu-id="c9ea7-207">Для этого примера см. рис. 2.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-207">For this example, refer to Diagram 2.</span></span> <span data-ttu-id="c9ea7-208">Для клиента 1, обратите внимание, что необходимые подсетей **192.168.2.0/24** (это концентратора виртуальной сети в Azure) и **10.100.0.0/16** (это резервный виртуальной сети в Azure).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-208">For Tenant 1, notice that the required subnets are **192.168.2.0/24** (this is the Hub Vnet in Azure) and **10.100.0.0/16** (this is the Spoke VNet in Azure).</span></span> <span data-ttu-id="c9ea7-209">Введите соответствующие подсети для вашей рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-209">Type the corresponding subnets for your own environment.</span></span>
   > [!IMPORTANT]
   > <span data-ttu-id="c9ea7-210">В этом примере предполагается, что вы используете статические маршруты для сеть-сеть VPN-подключение между шлюзом стек Azure и маршрутизатор ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-210">This example assumes you are using static routes for the Site-to-Site VPN connection between the Azure Stack gateway and the ExpressRoute router.</span></span>

8. <span data-ttu-id="c9ea7-211">Убедитесь, что ваш **подписки**, **группы ресурсов**, и **расположение** заданы правильно и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-211">Verify that your **Subscription**, **Resource Group**, and **Location** are all correct and click **Create**.</span></span>

#### <a name="create-the-connection"></a><span data-ttu-id="c9ea7-212">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="c9ea7-212">Create the connection</span></span>
1. <span data-ttu-id="c9ea7-213">На портале Azure стека пользователя щелкните **New**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-213">In the Azure Stack user portal, click **New**.</span></span>
2. <span data-ttu-id="c9ea7-214">В меню Marketplace выберите **Сети**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-214">Select **Networking** from the Marketplace menu.</span></span>
3. <span data-ttu-id="c9ea7-215">В списке сетевых ресурсов выберите **Подключение**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-215">Select **Connection** from the list of resources.</span></span>
4. <span data-ttu-id="c9ea7-216">В **основы** разделе "Параметры" выберите **-сайтами (IPSec)** как **тип соединения**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-216">In the **Basics** settings section, choose **Site-to-site (IPSec)** as the **Connection type**.</span></span>
5. <span data-ttu-id="c9ea7-217">Выберите **подписки**, **группы ресурсов**, и **расположение** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-217">Select the **Subscription**, **Resource Group**, and **Location** and click **OK**.</span></span>
6. <span data-ttu-id="c9ea7-218">В **параметры** щелкните **шлюз виртуальной сети** щелкните **GW1**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-218">In the **Settings** section,  click **Virtual network gateway** click **GW1**.</span></span>
7. <span data-ttu-id="c9ea7-219">Нажмите кнопку **шлюз локальной сети**и нажмите кнопку **ER маршрутизатора GW**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-219">Click **Local network gateway**, and click **ER Router GW**.</span></span>
8. <span data-ttu-id="c9ea7-220">В **имя подключения** введите **ConnectToAzure**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-220">In the **Connection Name** field, type **ConnectToAzure**.</span></span>
9. <span data-ttu-id="c9ea7-221">В **общий ключ (PSK)** введите **abc123** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-221">In the **Shared key (PSK)** field, type **abc123** and click **OK**.</span></span>
10. <span data-ttu-id="c9ea7-222">На **Сводка** щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-222">On the **Summary** section, click **OK**.</span></span>

    <span data-ttu-id="c9ea7-223">После создания соединения, можно увидеть общедоступный IP-адрес, используемый шлюзом виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-223">After the connection is created, you can see the public IP address used by the virtual network gateway.</span></span> <span data-ttu-id="c9ea7-224">Чтобы найти адрес на портале Azure стека, перейдите на шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-224">To find the address in the Azure Stack portal, browse to your Virtual network gateway.</span></span> <span data-ttu-id="c9ea7-225">В **Обзор**, найти **общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-225">In **Overview**, find the **Public IP address**.</span></span> <span data-ttu-id="c9ea7-226">Запишите этот адрес; используется в качестве *внутренний IP-адрес* в следующем разделе (если применимо, для развертывания).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-226">Note this address; you will use it as the *Internal IP address* in the next section (if applicable for your deployment).</span></span>

    ![](media/azure-stack-connect-expressroute/GWPublicIP.png)

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="c9ea7-227">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c9ea7-227">Create a virtual machine</span></span>
<span data-ttu-id="c9ea7-228">Для проверки данных, проходящих через VPN-подключение, необходимо, чтобы виртуальные машины для отправки и получения данных в стек виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-228">To validate data traveling through the VPN Connection, you need virtual machines to send and receive data in the Azure Stack Vnet.</span></span> <span data-ttu-id="c9ea7-229">Теперь создайте виртуальную машину и поместить его в вашей подсети виртуальной Машины в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-229">Create a virtual machine now and put it in your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="c9ea7-230">На портале Azure стека пользователя щелкните **New**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-230">In the Azure Stack user portal, click **New**.</span></span>
2. <span data-ttu-id="c9ea7-231">В меню Marketplace выберите **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-231">Select **Virtual Machines** from the Marketplace menu.</span></span>
3. <span data-ttu-id="c9ea7-232">В списке образов виртуальных машин, выберите **Eval центра обработки данных Windows Server 2016** образ и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-232">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image and click **Create**.</span></span>
4. <span data-ttu-id="c9ea7-233">На **основы** раздела **имя** тип поля **VM01**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-233">On the **Basics** section, in the **Name** field type **VM01**.</span></span>
5. <span data-ttu-id="c9ea7-234">Введите допустимое имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-234">Type a valid user name and password.</span></span> <span data-ttu-id="c9ea7-235">Эта учетная запись будет использоваться для входа в виртуальную машину после ее создания.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-235">You’ll use this account to log in to the VM after it has been created.</span></span>
6. <span data-ttu-id="c9ea7-236">Укажите **подписки**, **группы ресурсов**, и **расположение** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-236">Provide a **Subscription**, **Resource Group**, and **Location** and then click **OK**.</span></span>
7. <span data-ttu-id="c9ea7-237">На **размер** щелкните размер виртуальной машины для этого экземпляра и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-237">On the **Size** section, click a virtual machine size for this instance and then click **Select**.</span></span>
8. <span data-ttu-id="c9ea7-238">На **параметры** раздела, можно принять значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-238">On the **Settings** section, you can accept the defaults.</span></span> <span data-ttu-id="c9ea7-239">Но это гарантирует выбранной виртуальной сети **Tenant1VNet1** и подсети **10.1.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-239">But ensure the virtual network selected is **Tenant1VNet1** and the subnet is set to **10.1.1.0/24**.</span></span> <span data-ttu-id="c9ea7-240">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-240">Click **OK**.</span></span>
9. <span data-ttu-id="c9ea7-241">Проверьте параметры на **Сводка** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-241">Review the settings on the **Summary** section and click **OK**.</span></span>

<span data-ttu-id="c9ea7-242">Для каждого клиента для подключения виртуальной сети, повторите предыдущие шаги из **создать виртуальную сеть и подсеть виртуальной Машины** через **Создание виртуальной машины** разделы.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-242">For each tenant VNet you want to connect, repeat the previous steps from **Create the virtual network and VM subnet** through **Create a virtual machine** sections.</span></span>

### <a name="configure-the-nat-virtual-machine-for-gateway-traversal"></a><span data-ttu-id="c9ea7-243">Настройте виртуальную машину NAT для обхода шлюза</span><span class="sxs-lookup"><span data-stu-id="c9ea7-243">Configure the NAT virtual machine for gateway traversal</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c9ea7-244">Этот раздел предназначен для развертывания пакета средств разработки Azure стека только.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-244">This section is for Azure Stack Development Kit deployments only.</span></span> <span data-ttu-id="c9ea7-245">NAT не требуется для развертываний с несколькими узлами.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-245">The NAT is not needed for multi-node deployments.</span></span>

<span data-ttu-id="c9ea7-246">Пакет средств разработки Azure стека самодостаточны и изолированы от сети, на котором развернута физического узла.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-246">The Azure Stack Development Kit is self-contained and isolated from the network on which the physical host is deployed.</span></span> <span data-ttu-id="c9ea7-247">Таким образом не является внешним, шлюзы, подключенные к сети «External» виртуальный IP-адрес, но скрыто за маршрутизатором, выполнив сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-247">So, the “External” VIP network that the gateways are connected to is not external, but instead is hidden behind a router doing Network Address Translation (NAT).</span></span>
 
<span data-ttu-id="c9ea7-248">Маршрутизатор — это виртуальная машина Windows Server (**AzS BGPNAT01**) под управлением роли маршрутизации и удаленного доступа (RRAS) в инфраструктуре Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-248">The router is a Windows Server virtual machine (**AzS-BGPNAT01**) running the Routing and Remote Access Services (RRAS) role in the Azure Stack Development Kit infrastructure.</span></span> <span data-ttu-id="c9ea7-249">Необходимо настроить NAT на виртуальной машине AzS BGPNAT01, чтобы разрешить VPN-подключения сеть-сеть для подключения на обоих концах.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-249">You must configure NAT on the AzS-BGPNAT01 virtual machine to allow the Site-to-Site VPN Connection to connect on both ends.</span></span>

#### <a name="configure-the-nat"></a><span data-ttu-id="c9ea7-250">Настройка преобразования сетевых адресов</span><span class="sxs-lookup"><span data-stu-id="c9ea7-250">Configure the NAT</span></span>

1. <span data-ttu-id="c9ea7-251">Войдите в Azure стека физического компьютера с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-251">Log in to the Azure Stack physical machine with your administrator account.</span></span>
2. <span data-ttu-id="c9ea7-252">Скопируйте и измените следующий сценарий PowerShell и выполните в с повышенными привилегиями Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-252">Copy and edit the following PowerShell script and run in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="c9ea7-253">Замените пароль администратора.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-253">Replace your administrator password.</span></span> <span data-ttu-id="c9ea7-254">Возвращается адрес вашей *BGPNAT внешний адрес*.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-254">The address returned is your *External BGPNAT address*.</span></span>

   ```
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "azs-bgpnat01" `
    -Password $Password
   ```
4. <span data-ttu-id="c9ea7-255">Настройка преобразования сетевых адресов, скопируйте и измените следующий сценарий PowerShell и выполняются в с повышенными привилегиями Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-255">To configure the NAT, copy and edit the following PowerShell script and run in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="c9ea7-256">Измените скрипт, чтобы заменить *BGPNAT внешний адрес* и *внутренний IP-адрес* (ранее определенных на **создания подключения** раздел).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-256">Edit the script to replace the *External BGPNAT address* and *Internal IP address* (which you noted previously in the **Create the Connection** section).</span></span>

   <span data-ttu-id="c9ea7-257">На примере диаграммах *BGPNAT внешний адрес* — 10.10.0.62 и *внутренний IP-адрес* — 192.168.102.1.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-257">In the example diagrams, the *External BGPNAT address* is 10.10.0.62 and the *Internal IP address* is 192.168.102.1.</span></span>

   ```
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish the complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

## <a name="configure-azure"></a><span data-ttu-id="c9ea7-258">Настройка Azure</span><span class="sxs-lookup"><span data-stu-id="c9ea7-258">Configure Azure</span></span>
<span data-ttu-id="c9ea7-259">Теперь, после завершения настройки стека Azure, можно развернуть некоторые ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-259">Now that you have completed the Azure Stack configuration, you can deploy some Azure resources.</span></span> <span data-ttu-id="c9ea7-260">На следующей диаграмме показан пример клиента виртуальной сети в Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-260">The following diagram shows a sample tenant virtual network in Azure.</span></span> <span data-ttu-id="c9ea7-261">Можно использовать любое имя и схему адресации для виртуальной сети в Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-261">You can use any name and addressing scheme for your VNet in Azure.</span></span> <span data-ttu-id="c9ea7-262">Однако диапазон адресов для виртуальных сетей в стеке Azure и Azure должны быть уникальными и не перекрываются.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-262">However, the address range of the VNets in Azure and Azure Stack must be unique and not overlap.</span></span>

![Виртуальные сети Azure](media/azure-stack-connect-expressroute/AzureArchitecture.png)

<span data-ttu-id="c9ea7-264">**Схема 3**</span><span class="sxs-lookup"><span data-stu-id="c9ea7-264">**Diagram 3**</span></span>

<span data-ttu-id="c9ea7-265">Ресурсы, развертываемые в Azure похожи на ресурсы, которые развернуты в стек Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-265">The resources you deploy in Azure are similar to the resources you deployed in Azure Stack.</span></span> <span data-ttu-id="c9ea7-266">Аналогичным образом можно развернуть:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-266">Similarly, you deploy:</span></span>
* <span data-ttu-id="c9ea7-267">Виртуальные сети и подсети</span><span class="sxs-lookup"><span data-stu-id="c9ea7-267">Virtual networks and subnets</span></span>
* <span data-ttu-id="c9ea7-268">Подсеть шлюза</span><span class="sxs-lookup"><span data-stu-id="c9ea7-268">A gateway subnet</span></span>
* <span data-ttu-id="c9ea7-269">шлюз виртуальной сети;</span><span class="sxs-lookup"><span data-stu-id="c9ea7-269">A virtual network gateway</span></span>
* <span data-ttu-id="c9ea7-270">Соединение</span><span class="sxs-lookup"><span data-stu-id="c9ea7-270">A connection</span></span>
* <span data-ttu-id="c9ea7-271">Канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c9ea7-271">An ExpressRoute circuit</span></span>

<span data-ttu-id="c9ea7-272">Пример сетевой инфраструктуры Azure настраивается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-272">The example Azure network infrastructure is configured in the following way:</span></span>
* <span data-ttu-id="c9ea7-273">Используется стандартный (192.168.2.0/24) звездообразной (10.100.0.0./16) модели виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-273">A standard hub (192.168.2.0/24) and spoke (10.100.0.0./16) VNet model is used.</span></span>
* <span data-ttu-id="c9ea7-274">Рабочие нагрузки развертываются в резервный виртуальной сети и канал ExpressRoute подключен к концентратору виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-274">The workloads are deployed in the spoke Vnet and the ExpressRoute circuit is connected to the hub VNet.</span></span>
* <span data-ttu-id="c9ea7-275">Два виртуальных сетей связаны с помощью функции пиринга виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-275">The two VNets are linked using the VNet peering feature.</span></span>

### <a name="configure-vnets"></a><span data-ttu-id="c9ea7-276">Настройка виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="c9ea7-276">Configure Vnets</span></span>
1. <span data-ttu-id="c9ea7-277">Войдите на портал Azure, используя свои учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-277">Sign in to the Azure portal with your Azure credentials.</span></span>
2. <span data-ttu-id="c9ea7-278">Создание концентратора виртуальной сети с помощью адресное пространство 192.168.2.0/24.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-278">Create the hub VNet using the 192.168.2.0/24 address space.</span></span> <span data-ttu-id="c9ea7-279">Создание с помощью 192.168.2.0/25 диапазон адресов подсети и добавить подсеть шлюза, используя диапазон адресов 192.168.2.128/27.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-279">Create a subnet using the 192.168.2.0/25 address range, and add a gateway subnet using the 192.168.2.128/27 address range.</span></span>
3. <span data-ttu-id="c9ea7-280">Создание резервного диапазон адресов виртуальной сети и подсети с помощью 10.100.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-280">Create the spoke VNet and subnet using the 10.100.0.0/16 address range.</span></span>


<span data-ttu-id="c9ea7-281">Дополнительные сведения о создании виртуальных сетей в Azure см. в разделе [создать виртуальную сеть с несколькими подсетями](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-281">For more information about creating virtual networks in Azure, see [Create a virtual network with multiple subnets](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

### <a name="configure-an-expressroute-circuit"></a><span data-ttu-id="c9ea7-282">Настроить канал ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="c9ea7-282">Configure an ExpressRoute circuit</span></span>

1. <span data-ttu-id="c9ea7-283">Изучите необходимые компоненты ExpressRoute в [ExpressRoute необходимые компоненты и контрольный список](../expressroute/expressroute-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-283">Review the ExpressRoute prerequisites in [ExpressRoute prerequisites & checklist](../expressroute/expressroute-prerequisites.md).</span></span>
2. <span data-ttu-id="c9ea7-284">Следуйте указаниям в [Создание и изменение канал ExpressRoute](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) для создания канала ExpressRoute с помощью вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-284">Follow the steps in [Create and modify an ExpressRoute circuit](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) to create an ExpressRoute circuit using your Azure subscription.</span></span>
3. <span data-ttu-id="c9ea7-285">С помощью поставщика услуг размещения или поставщика для подготовки к каналу ExpressRoute со своей стороны совместно использовать ключ службы из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-285">Share the service key from the previous step with your hoster/provider to provision your ExpressRoute circuit at their end.</span></span>
4. <span data-ttu-id="c9ea7-286">Следуйте указаниям в [создания и изменения пиринга за канал ExpressRoute](../expressroute/expressroute-howto-routing-portal-resource-manager.md) настройка частного пиринга на канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-286">Follow the steps in [Create and modify peering for an ExpressRoute circuit](../expressroute/expressroute-howto-routing-portal-resource-manager.md) to configure private peering on the ExpressRoute circuit.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="c9ea7-287">Создание шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c9ea7-287">Create the virtual network gateway</span></span>

* <span data-ttu-id="c9ea7-288">Следуйте указаниям в [настроить шлюз виртуальной сети для ExpressRoute с помощью PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) Создание шлюза виртуальной сети для ExpressRoute в концентраторе виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-288">Follow the steps in [Configure a virtual network gateway for ExpressRoute using PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) to create a virtual network gateway for ExpressRoute in the hub VNet.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="c9ea7-289">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="c9ea7-289">Create the connection</span></span>

* <span data-ttu-id="c9ea7-290">Чтобы связать с expressroute концентратора виртуальной сети, следуйте инструкциям [подключить виртуальную сеть к каналу ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-290">To link the ExpressRoute circuit to the hub VNet, follow the steps in [Connect a virtual network to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>

### <a name="peer-the-vnets"></a><span data-ttu-id="c9ea7-291">Одноранговая виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="c9ea7-291">Peer the Vnets</span></span>

* <span data-ttu-id="c9ea7-292">Одноранговая основной и резервный виртуальных сетей с помощью действия, описанные в [создать виртуальную сеть пиринга с помощью портала Azure](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9ea7-292">Peer the Hub and Spoke VNets using the steps in [Create a virtual network peering using the Azure portal](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span></span> <span data-ttu-id="c9ea7-293">При настройке пиринговой виртуальной сети убедитесь, что выбраны следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-293">When configuring VNet peering, ensure you select the following options:</span></span>
   * <span data-ttu-id="c9ea7-294">От концентратора для типа «звезда»: **разрешить транспорте шлюза**</span><span class="sxs-lookup"><span data-stu-id="c9ea7-294">From hub to spoke: **Allow gateway transit**</span></span>
   * <span data-ttu-id="c9ea7-295">Из типа «звезда» к концентратору: **использовать удаленный шлюз**</span><span class="sxs-lookup"><span data-stu-id="c9ea7-295">From spoke to hub: **Use remote gateway**</span></span>

### <a name="create-a-virtual-machine"></a><span data-ttu-id="c9ea7-296">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c9ea7-296">Create a virtual machine</span></span>

* <span data-ttu-id="c9ea7-297">Развертывание рабочей нагрузки виртуальных машин в резервный виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-297">Deploy your workload virtual machines into the spoke VNet.</span></span>

<span data-ttu-id="c9ea7-298">Повторите эти действия для всех дополнительных пользователей виртуальных сетей для подключения в Azure через их соответствующие каналы ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-298">Repeat these steps for any additional tenant VNets you want to connect in Azure through their respective ExpressRoute circuits.</span></span>

## <a name="configure-the-router"></a><span data-ttu-id="c9ea7-299">Настройка маршрутизатора</span><span class="sxs-lookup"><span data-stu-id="c9ea7-299">Configure the router</span></span>

<span data-ttu-id="c9ea7-300">На следующей диаграмме инфраструктуры в целом можно использовать для задач настройки маршрутизатора ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-300">You can use the following end-to-end infrastructure diagram to guide the configuration of your ExpressRoute Router.</span></span> <span data-ttu-id="c9ea7-301">На этой диаграмме показаны двух клиентов (клиента 1 и 2 клиента) их соответствующих цепи Express Route.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-301">This diagram shows two tenants (Tenant 1 and Tenant 2) with their respective Express Route circuits.</span></span> <span data-ttu-id="c9ea7-302">Каждый связанный для своих собственных VRF (виртуальный маршрутизации и пересылки) в локальной и глобальной сети на стороне ExpressRoute маршрутизатора, чтобы обеспечить изоляцию конца в конец между двух клиентов.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-302">Each is linked to their own VRF (Virtual Routing and Forwarding) in the LAN and WAN side of the ExpressRoute router to ensure end-to-end isolation between the two tenants.</span></span> <span data-ttu-id="c9ea7-303">Обратите внимание, IP-адреса, используемые в интерфейсах маршрутизатора, как выполните пример конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-303">Note the IP addresses used in the router interfaces as you follow the sample configuration.</span></span>

![Полнофункциональный схемы](media/azure-stack-connect-expressroute/EndToEnd.png)

<span data-ttu-id="c9ea7-305">**На рис. 4**</span><span class="sxs-lookup"><span data-stu-id="c9ea7-305">**Diagram 4**</span></span>

<span data-ttu-id="c9ea7-306">Можно использовать любой маршрутизатор, который поддерживает IKEv2 VPN и BGP разорвать соединение через виртуальную Частную сеть для из стека Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-306">You can use any router that supports IKEv2 VPN and BGP to terminate the Site-to-Site VPN connection from Azure Stack.</span></span> <span data-ttu-id="c9ea7-307">Тому же маршрутизатору используется для подключения к Azure, используя канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-307">The same router is used to connect to Azure using an ExpressRoute circuit.</span></span> 

<span data-ttu-id="c9ea7-308">Ниже приведен пример конфигурации из 1000 Cisco ASR, который поддерживает инфраструктуру сети, показанный на диаграмме. 4.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-308">Here is a sample configuration from a Cisco ASR 1000 that supports the network infrastructure shown in Diagram 4:</span></span>

```
ip vrf Tenant 1
 description Routing Domain for PRIVATE peering to Azure for Tenant 1
 rd 1:1
!
ip vrf Tenant 2
 description Routing Domain for PRIVATE peering to Azure for Tenant 2
 rd 1:5
!
crypto ikev2 proposal V2-PROPOSAL2 
description IKEv2 proposal for Tenant 1 
encryption aes-cbc-256
 integrity sha256
 group 2
crypto ikev2 proposal V4-PROPOSAL2 
description IKEv2 proposal for Tenant 2 
encryption aes-cbc-256
 integrity sha256
 group 2
!
crypto ikev2 policy V2-POLICY2 
description IKEv2 Policy for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 proposal V2-PROPOSAL2
description IKEv2 Policy for Tenant 2
crypto ikev2 policy V4-POLICY2 
 match fvrf Tenant 2
 match address local 10.60.3.251
 proposal V4-PROPOSAL2
!
crypto ikev2 profile V2-PROFILE
description IKEv2 profile for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 1
!
crypto ikev2 profile V4-PROFILE
description IKEv2 profile for Tenant 2
 match fvrf Tenant 2
 match address local 10.60.3.251
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 2
!
crypto ipsec transform-set V2-TRANSFORM2 esp-gcm 256 
 mode tunnel
crypto ipsec transform-set V4-TRANSFORM2 esp-gcm 256 
 mode tunnel
!
crypto ipsec profile V2-PROFILE
 set transform-set V2-TRANSFORM2 
 set ikev2-profile V2-PROFILE
!
crypto ipsec profile V4-PROFILE
 set transform-set V4-TRANSFORM2 
 set ikev2-profile V4-PROFILE
!
interface Tunnel10
description S2S VPN Tunnel for Tenant 1
 ip vrf forwarding Tenant 1
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.211
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf Tenant 1
 tunnel protection ipsec profile V2-PROFILE
!
interface Tunnel20
description S2S VPN Tunnel for Tenant 2
 ip vrf forwarding Tenant 2
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.213
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf VNET3
 tunnel protection ipsec profile V4-PROFILE
!
interface GigabitEthernet0/0/1
 description PRIMARY Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/1.100
description Primary WAN interface of Tenant 1
 description PRIMARY ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.1 255.255.255.252
!
interface GigabitEthernet0/0/1.102
description Primary WAN interface of Tenant 2
 description PRIMARY ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.17 255.255.255.252
!
interface GigabitEthernet0/0/2
 description BACKUP Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/2.100
description Secondary WAN interface of Tenant 1
 description BACKUP ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.5 255.255.255.252
!
interface GigabitEthernet0/0/2.102
description Secondary WAN interface of Tenant 2 
description BACKUP ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.21 255.255.255.252
!
interface TenGigabitEthernet0/1/0
 description Downlink to ---Port 1/47
 no ip address
!
interface TenGigabitEthernet0/1/0.211
 description LAN interface of Tenant 1
description Downlink to --- Port 1/47.211
 encapsulation dot1Q 211
 ip vrf forwarding Tenant 1
 ip address 10.60.3.255 255.255.255.254
!
interface TenGigabitEthernet0/1/0.213
description LAN interface of Tenant 2
 description Downlink to --- Port 1/47.213
 encapsulation dot1Q 213
 ip vrf forwarding Tenant 2
 ip address 10.60.3.251 255.255.255.254
!
router bgp 65530
 bgp router-id <removed>
 bgp log-neighbor-changes
 description BGP neighbor config and route advertisement for Tenant 1 VRF 
 address-family ipv4 vrf Tenant 1
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.254 mask 255.255.255.254
  network 192.168.1.0 mask 255.255.255.252
  network 192.168.1.4 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65100
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 1
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.254 remote-as 4232570301
  neighbor 10.60.3.254 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.254 activate
  neighbor 10.60.3.254 route-map BLOCK-ALL out
  neighbor 192.168.1.2 remote-as 12076
  neighbor 192.168.1.2 description PRIMARY ER peer for Tenant 1 to Azure
  neighbor 192.168.1.2 ebgp-multihop 5
  neighbor 192.168.1.2 activate
  neighbor 192.168.1.2 soft-reconfiguration inbound
  neighbor 192.168.1.2 route-map Tenant 1-ONLY out
  neighbor 192.168.1.6 remote-as 12076
  neighbor 192.168.1.6 description BACKUP ER peer for Tenant 1 to Azure
  neighbor 192.168.1.6 ebgp-multihop 5
  neighbor 192.168.1.6 activate
  neighbor 192.168.1.6 soft-reconfiguration inbound
  neighbor 192.168.1.6 route-map Tenant 1-ONLY out
  maximum-paths 8
 exit-address-family
 !
description BGP neighbor config and route advertisement for Tenant 2 VRF 
address-family ipv4 vrf Tenant 2
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.250 mask 255.255.255.254
  network 192.168.1.16 mask 255.255.255.252
  network 192.168.1.20 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65300
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 2
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.250 remote-as 4232570301
  neighbor 10.60.3.250 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.250 activate
  neighbor 10.60.3.250 route-map BLOCK-ALL out
  neighbor 192.168.1.18 remote-as 12076
  neighbor 192.168.1.18 description PRIMARY ER peer for Tenant 2 to Azure
  neighbor 192.168.1.18 ebgp-multihop 5
  neighbor 192.168.1.18 activate
  neighbor 192.168.1.18 soft-reconfiguration inbound
  neighbor 192.168.1.18 route-map VNET-ONLY out
  neighbor 192.168.1.22 remote-as 12076
  neighbor 192.168.1.22 description BACKUP ER peer for Tenant 2 to Azure
  neighbor 192.168.1.22 ebgp-multihop 5
  neighbor 192.168.1.22 activate
  neighbor 192.168.1.22 soft-reconfiguration inbound
  neighbor 192.168.1.22 route-map VNET-ONLY out
  maximum-paths 8
 exit-address-family
!
ip forward-protocol nd
!
ip as-path access-list 1 permit ^$
ip route vrf Tenant 1 10.1.0.0 255.255.0.0 Tunnel10
ip route vrf Tenant 2 10.1.0.0 255.255.0.0 Tunnel20
!
ip prefix-list BLOCK-ALL seq 5 deny 0.0.0.0/0 le 32
!
route-map BLOCK-ALL permit 10
 match ip address prefix-list BLOCK-ALL
!
route-map VNET-ONLY permit 10
 match as-path 1
!
```

## <a name="test-the-connection"></a><span data-ttu-id="c9ea7-309">Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="c9ea7-309">Test the connection</span></span>

<span data-ttu-id="c9ea7-310">Проверьте подключение после установления подключения сеть-сеть и канал ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-310">Test your connection after establishing the Site-to-Site connection and the ExpressRoute circuit.</span></span> <span data-ttu-id="c9ea7-311">Эта задача является простой.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-311">This task is simple.</span></span>  <span data-ttu-id="c9ea7-312">Выполните вход на одной из виртуальных машин, созданных в виртуальной сети Azure и проверить связь с виртуальной машины, созданной в среде Azure стека, или наоборот.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-312">Log on to one of the virtual machines you created in your Azure VNet and ping the virtual machine you created in the Azure Stack environment, or vice versa.</span></span> 

<span data-ttu-id="c9ea7-313">Чтобы убедиться, что при отправке трафика через сеть-сеть и подключения ExpressRoute, необходимо проверить связь выделенный адрес IP-адрес (DIP) виртуальной машины на концах одновременно, а не адрес виртуального IP-адреса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-313">To ensure you are sending the traffic through the Site-to-Site and ExpressRoute connections, you must ping the dedicated IP (DIP) address of the virtual machine at both ends and not the VIP address of the virtual machine.</span></span> <span data-ttu-id="c9ea7-314">Таким образом необходимо найти и запишите адрес, на другой стороне соединения.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-314">So, you must find and note the address on the other end of the connection.</span></span>

### <a name="allow-icmp-in-through-the-firewall"></a><span data-ttu-id="c9ea7-315">Разрешить ICMP в через брандмауэр</span><span class="sxs-lookup"><span data-stu-id="c9ea7-315">Allow ICMP in through the firewall</span></span>
<span data-ttu-id="c9ea7-316">По умолчанию Windows Server 2016 не разрешают ICMP-пакеты через брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-316">By default, Windows Server 2016 does not allow ICMP packets in through the firewall.</span></span> <span data-ttu-id="c9ea7-317">Таким образом для каждой виртуальной машины, используемого в тест, в окне PowerShell с повышенными привилегиями выполните следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="c9ea7-317">So, for every virtual machine you use in the test, run the following cmdlet in an elevated PowerShell window:</span></span>


   ```
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="ping-the-azure-stack-virtual-machine"></a><span data-ttu-id="c9ea7-318">Проверить связь с виртуальной машины Azure стека</span><span class="sxs-lookup"><span data-stu-id="c9ea7-318">Ping the Azure Stack virtual machine</span></span>

1. <span data-ttu-id="c9ea7-319">Войдите на пользовательский портал Azure стека с помощью учетной записи клиента.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-319">Sign in to the Azure Stack user portal using a tenant account.</span></span>
2. <span data-ttu-id="c9ea7-320">В области навигации слева щелкните **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-320">Click **Virtual Machines** in the left navigation bar.</span></span>
3. <span data-ttu-id="c9ea7-321">Найти ранее созданную виртуальную машину и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-321">Find the virtual machine that you previously created and click it.</span></span>
4. <span data-ttu-id="c9ea7-322">В разделе для виртуальной машины, нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-322">On the section for the virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="c9ea7-323">Откройте PowerShell с повышенными правами окно и введите **ipconfig/all**.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-323">Open an elevated PowerShell window, and type **ipconfig /all**.</span></span>
6. <span data-ttu-id="c9ea7-324">Найти адрес IPv4 в выходных данных и запишите его.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-324">Find the IPv4 Address in the output and note it.</span></span> <span data-ttu-id="c9ea7-325">Проверьте связь этого адреса из виртуальной машины в виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-325">Ping this address from the virtual machine in the Azure VNet.</span></span> <span data-ttu-id="c9ea7-326">В среде примере адрес является из подсети 10.1.1.x/24.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-326">In the example environment, the address is from the 10.1.1.x/24 subnet.</span></span> <span data-ttu-id="c9ea7-327">В вашей среде адресе может отличаться.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-327">In your environment, the address might be different.</span></span> <span data-ttu-id="c9ea7-328">Тем не менее следует в подсети, созданной для подсети виртуальной сети клиента.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-328">However, it should be within the subnet you created for the Tenant VNet subnet.</span></span>


### <a name="view-data-transfer-statistics"></a><span data-ttu-id="c9ea7-329">Просмотр статистики передачи данных</span><span class="sxs-lookup"><span data-stu-id="c9ea7-329">View data transfer statistics</span></span>

<span data-ttu-id="c9ea7-330">Если вы хотите знать, какой объем трафика передается через подключение к, можно найти эти сведения в разделе "подключения" в пользовательском портале Azure стека.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-330">If you want to know how much traffic is passing through your connection, you can find this information on the Connection section in the Azure Stack user portal.</span></span> <span data-ttu-id="c9ea7-331">Эти сведения также является хороший способ проверить, что ping, который вы только что отправлен на самом деле пошло через подключения VPN и ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-331">This information is also another good way to verify that the ping you just sent actually went through the VPN and ExpressRoute connections.</span></span>

1. <span data-ttu-id="c9ea7-332">Войдите на пользовательский портал стека Microsoft Azure с помощью учетной записи клиента.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-332">Sign in to the Microsoft Azure Stack user portal using your tenant account.</span></span>
2. <span data-ttu-id="c9ea7-333">Перейдите к группе ресурсов, в которой был создан шлюза VPN и выберите **подключений** тип объекта.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-333">Navigate to the resource group where your VPN Gateway was created and select the **Connections** object type.</span></span>
3. <span data-ttu-id="c9ea7-334">Нажмите кнопку **ConnectToAzure** подключение в списке.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-334">Click the **ConnectToAzure** connection in the list.</span></span>
4. <span data-ttu-id="c9ea7-335">На **подключения** можно просмотреть статистику для **данные в** и **исходящие данные**. Там будут отображаться ненулевые значения.</span><span class="sxs-lookup"><span data-stu-id="c9ea7-335">On the **Connection** section, you can see statistics for **Data in** and **Data out**. You should see some non-zero values there.</span></span>

   ![Данные в исходящие данные](media/azure-stack-connect-expressroute/DataInDataOut.png)

## <a name="next-steps"></a><span data-ttu-id="c9ea7-337">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9ea7-337">Next steps</span></span>
[<span data-ttu-id="c9ea7-338">Развертывание приложений для Azure и Azure стека</span><span class="sxs-lookup"><span data-stu-id="c9ea7-338">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)