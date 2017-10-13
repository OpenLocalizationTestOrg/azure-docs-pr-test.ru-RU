---
title: "Создать сеть сеть VPN-подключение между двумя виртуальными сетями в разных средах Azure стека Development Kit | Документы Microsoft"
description: "Пошаговая процедура, администратору облака для создания VPN-подключения сеть сеть между двумя средами пакет средств разработки Azure стека одного узла."
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 3f1b4e02-dbab-46a3-8e11-a777722120ec
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: fa2a940620e06521fa110fa13dcbc3050635a502
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-site-to-site-vpn-connection-between-two-virtual-networks-in-different-azure-stack-development-kit-environments"></a><span data-ttu-id="dbb00-103">Создать сеть сеть VPN-подключение между двумя виртуальными сетями в разных средах пакет средств разработки стек Azure</span><span class="sxs-lookup"><span data-stu-id="dbb00-103">Create a site-to-site VPN connection between two virtual networks in different Azure Stack Development Kit environments</span></span>
## <a name="overview"></a><span data-ttu-id="dbb00-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="dbb00-104">Overview</span></span>
<span data-ttu-id="dbb00-105">В этой статье показано, как создать сеть сеть VPN-подключение между двумя виртуальными сетями в двух отдельных средах Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="dbb00-105">This article shows you how to create a site-to-site VPN connection between two virtual networks in two separate Azure Stack Development Kit environments.</span></span> <span data-ttu-id="dbb00-106">Во время настройки соединения, вы узнаете, как работают VPN-шлюзы Azure стека.</span><span class="sxs-lookup"><span data-stu-id="dbb00-106">While you configure the connections, you learn how VPN gateways in Azure Stack work.</span></span>

### <a name="connection-diagram"></a><span data-ttu-id="dbb00-107">Схема подключения</span><span class="sxs-lookup"><span data-stu-id="dbb00-107">Connection diagram</span></span>
<span data-ttu-id="dbb00-108">В примере ниже показан конфигурации соединения должны выглядеть после завершения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-108">The following diagram shows what the connection configuration should look like when you’re done.</span></span>

![Сайт сайт конфигурации VPN-подключения](media/azure-stack-create-vpn-connection-one-node-tp2/OneNodeS2SVPN.png)

### <a name="before-you-begin"></a><span data-ttu-id="dbb00-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="dbb00-110">Before you begin</span></span>
<span data-ttu-id="dbb00-111">Чтобы завершить настройку подключения, убедитесь, что следующие элементы перед началом:</span><span class="sxs-lookup"><span data-stu-id="dbb00-111">To complete the connection configuration, ensure that you have the following items before you begin:</span></span>

* <span data-ttu-id="dbb00-112">Два сервера, которые удовлетворяют требованиям к оборудованию пакет средств разработки Azure стека, которые определены по [необходимые условия для развертывания Azure стека](azure-stack-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="dbb00-112">Two servers that meet the Azure Stack Development Kit hardware requirements, which are defined by the [Azure Stack deployment prerequisites](azure-stack-deploy.md).</span></span> <span data-ttu-id="dbb00-113">Убедитесь, что другие необходимые компоненты, отображаемые в [статьи](azure-stack-deploy.md) слишком будут выполнены.</span><span class="sxs-lookup"><span data-stu-id="dbb00-113">Ensure that the other prerequisites that appear in the [article](azure-stack-deploy.md) are fulfilled too.</span></span>
* <span data-ttu-id="dbb00-114">[Пакет средств разработки Azure стека](https://azure.microsoft.com/en-us/overview/azure-stack/try/) пакет развертывания.</span><span class="sxs-lookup"><span data-stu-id="dbb00-114">The [Azure Stack Development Kit](https://azure.microsoft.com/en-us/overview/azure-stack/try/) deployment package.</span></span>

## <a name="deploy-the-azure-stack-development-kit-environments"></a><span data-ttu-id="dbb00-115">Развертывание сред пакет средств разработки стек Azure</span><span class="sxs-lookup"><span data-stu-id="dbb00-115">Deploy the Azure Stack Development Kit environments</span></span>
<span data-ttu-id="dbb00-116">Чтобы завершить настройку подключения, необходимо развернуть двумя средами Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="dbb00-116">To complete the connection configuration, you must deploy two Azure Stack Development Kit environments.</span></span>
> [!NOTE] 
> <span data-ttu-id="dbb00-117">Для каждого Azure стека пакета средств разработки, развертывания, выполните [инструкции по развертыванию](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="dbb00-117">For each Azure Stack Development Kit that you deploy, follow the [deployment instructions](azure-stack-run-powershell-script.md).</span></span> <span data-ttu-id="dbb00-118">В этой статье, называются средах Azure стека Development Kit *POC1* и *POC2*.</span><span class="sxs-lookup"><span data-stu-id="dbb00-118">In this article, the Azure Stack Development Kit environments are called *POC1* and *POC2*.</span></span>


## <a name="prepare-an-offer-on-poc1-and-poc2"></a><span data-ttu-id="dbb00-119">Подготовка предложение на POC1 и POC2</span><span class="sxs-lookup"><span data-stu-id="dbb00-119">Prepare an offer on POC1 and POC2</span></span>
<span data-ttu-id="dbb00-120">На POC1 и POC2 Подготовьте предложение, чтобы пользователь мог подписаться на предложение и развертывание виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="dbb00-120">On both POC1 and POC2, prepare an offer so that a user can subscribe to the offer and deploy the virtual machines.</span></span> <span data-ttu-id="dbb00-121">Сведения о том, как создать предложение см [доступность виртуальных машин для пользователей Azure стека](azure-stack-tutorial-tenant-vm.md).</span><span class="sxs-lookup"><span data-stu-id="dbb00-121">For information on how to create an offer, see [Make virtual machines available to your Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span></span>

## <a name="review-and-complete-the-network-configuration-table"></a><span data-ttu-id="dbb00-122">Изучите и выполните в таблице конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="dbb00-122">Review and complete the network configuration table</span></span>
<span data-ttu-id="dbb00-123">В следующей таблице перечислены параметры сети для обеих сред пакет средств разработки стек Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb00-123">The following table summarizes the network configuration for both Azure Stack Development Kit environments.</span></span> <span data-ttu-id="dbb00-124">Используйте процедуру, которая появляется после таблицы для добавления внешних BGPNAT адреса, подходящую для вашей сети.</span><span class="sxs-lookup"><span data-stu-id="dbb00-124">Use the procedure that appears after the table to add the External BGPNAT address that is specific for your network.</span></span>

<span data-ttu-id="dbb00-125">**Таблица конфигурации сети**</span><span class="sxs-lookup"><span data-stu-id="dbb00-125">**Network configuration table**</span></span>
|   |<span data-ttu-id="dbb00-126">POC1</span><span class="sxs-lookup"><span data-stu-id="dbb00-126">POC1</span></span>|<span data-ttu-id="dbb00-127">POC2</span><span class="sxs-lookup"><span data-stu-id="dbb00-127">POC2</span></span>|
|---------|---------|---------|
|<span data-ttu-id="dbb00-128">Имя виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="dbb00-128">Virtual network name</span></span>     |<span data-ttu-id="dbb00-129">01 ВИРТУАЛЬНОЙ СЕТИ</span><span class="sxs-lookup"><span data-stu-id="dbb00-129">VNET-01</span></span>|<span data-ttu-id="dbb00-130">02 ВИРТУАЛЬНОЙ СЕТИ</span><span class="sxs-lookup"><span data-stu-id="dbb00-130">VNET-02</span></span> |
|<span data-ttu-id="dbb00-131">Адресное пространство виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="dbb00-131">Virtual network address space</span></span> |<span data-ttu-id="dbb00-132">10.0.10.0/23</span><span class="sxs-lookup"><span data-stu-id="dbb00-132">10.0.10.0/23</span></span>|<span data-ttu-id="dbb00-133">10.0.20.0/23</span><span class="sxs-lookup"><span data-stu-id="dbb00-133">10.0.20.0/23</span></span>|
|<span data-ttu-id="dbb00-134">Имя подсети</span><span class="sxs-lookup"><span data-stu-id="dbb00-134">Subnet name</span></span>     |<span data-ttu-id="dbb00-135">Подсети-01</span><span class="sxs-lookup"><span data-stu-id="dbb00-135">Subnet-01</span></span>|<span data-ttu-id="dbb00-136">Подсеть — 02</span><span class="sxs-lookup"><span data-stu-id="dbb00-136">Subnet-02</span></span>|
|<span data-ttu-id="dbb00-137">Диапазон адресов подсети</span><span class="sxs-lookup"><span data-stu-id="dbb00-137">Subnet address range</span></span>|<span data-ttu-id="dbb00-138">10.0.10.0/24</span><span class="sxs-lookup"><span data-stu-id="dbb00-138">10.0.10.0/24</span></span> |<span data-ttu-id="dbb00-139">10.0.20.0/24</span><span class="sxs-lookup"><span data-stu-id="dbb00-139">10.0.20.0/24</span></span> |
|<span data-ttu-id="dbb00-140">Подсеть шлюза</span><span class="sxs-lookup"><span data-stu-id="dbb00-140">Gateway subnet</span></span>     |<span data-ttu-id="dbb00-141">10.0.11.0/24</span><span class="sxs-lookup"><span data-stu-id="dbb00-141">10.0.11.0/24</span></span>|<span data-ttu-id="dbb00-142">10.0.21.0/24</span><span class="sxs-lookup"><span data-stu-id="dbb00-142">10.0.21.0/24</span></span>|
|<span data-ttu-id="dbb00-143">Внешний адрес BGPNAT</span><span class="sxs-lookup"><span data-stu-id="dbb00-143">External BGPNAT address</span></span>     |         |         |

> [!NOTE]
> <span data-ttu-id="dbb00-144">Внешние BGPNAT IP-адреса в примере среде являются 10.16.167.195 для POC1 и 10.16.169.131 для POC2.</span><span class="sxs-lookup"><span data-stu-id="dbb00-144">The external BGPNAT IP addresses in the example environment are 10.16.167.195 for POC1, and 10.16.169.131 for POC2.</span></span> <span data-ttu-id="dbb00-145">Используйте следующую процедуру для определения внешних BGPNAT IP-адреса для узлов Azure стека Development Kit, а затем добавьте их к предыдущей таблице конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="dbb00-145">Use the following procedure to determine the external BGPNAT IP addresses for your Azure Stack Development Kit hosts, and then add them to the previous network configuration table.</span></span>


### <a name="get-the-ip-address-of-the-external-adapter-of-the-nat-vm"></a><span data-ttu-id="dbb00-146">Получение IP-адреса внешнего адаптера виртуальной машины NAT</span><span class="sxs-lookup"><span data-stu-id="dbb00-146">Get the IP address of the external adapter of the NAT VM</span></span>
1. <span data-ttu-id="dbb00-147">Войдите на физическом компьютере Azure стека для POC1.</span><span class="sxs-lookup"><span data-stu-id="dbb00-147">Sign in to the Azure Stack physical machine for POC1.</span></span>
2. <span data-ttu-id="dbb00-148">Изменить следующий код Powershell, чтобы заменить пароль администратора, а затем запустите код подтверждения Концепции узла:</span><span class="sxs-lookup"><span data-stu-id="dbb00-148">Edit the following Powershell code to replace your administrator password, and then run the code on the POC host:</span></span>

   ```powershell
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "AzS-bgpnat01" `
    -Password $Password
   ```
3. <span data-ttu-id="dbb00-149">Добавьте IP-адрес таблицы конфигурации сети, которая отображается в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="dbb00-149">Add the IP address to the network configuration table that appears in the previous section.</span></span>

4. <span data-ttu-id="dbb00-150">Повторите эту процедуру на POC2.</span><span class="sxs-lookup"><span data-stu-id="dbb00-150">Repeat this procedure on POC2.</span></span>

## <a name="create-the-network-resources-in-poc1"></a><span data-ttu-id="dbb00-151">Создание сетевого ресурса в POC1</span><span class="sxs-lookup"><span data-stu-id="dbb00-151">Create the network resources in POC1</span></span>
<span data-ttu-id="dbb00-152">Теперь можно создать POC1 сетевые ресурсы, необходимых для настройки шлюзов.</span><span class="sxs-lookup"><span data-stu-id="dbb00-152">Now you create the POC1 network resources that you need to set up your gateways.</span></span> <span data-ttu-id="dbb00-153">Приведенные ниже инструкции показывают, как создать ресурсы с помощью пользовательского портала.</span><span class="sxs-lookup"><span data-stu-id="dbb00-153">The following instructions show you how to create the resources by using the user portal.</span></span> <span data-ttu-id="dbb00-154">Можно также использовать код PowerShell для создания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dbb00-154">You can also use PowerShell code to create the resources.</span></span>

![Рабочий процесс, который используется для создания ресурсов](media/azure-stack-create-vpn-connection-one-node-tp2/image2.png)

### <a name="sign-in-as-a-tenant"></a><span data-ttu-id="dbb00-156">Войдите в качестве клиента</span><span class="sxs-lookup"><span data-stu-id="dbb00-156">Sign in as a tenant</span></span>
<span data-ttu-id="dbb00-157">Администратором службы сможете войти как клиента для тестирования планов, предложения и подписки, которые могут использовать их клиентов.</span><span class="sxs-lookup"><span data-stu-id="dbb00-157">A service administrator can sign in as a tenant to test the plans, offers, and subscriptions that their tenants might use.</span></span> <span data-ttu-id="dbb00-158">Если вы уже нет, [создать учетную запись](azure-stack-add-new-user-aad.md) перед входом.</span><span class="sxs-lookup"><span data-stu-id="dbb00-158">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="dbb00-159">Создание виртуальной сети и подсети виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="dbb00-159">Create the virtual network and VM subnet</span></span>
1. <span data-ttu-id="dbb00-160">Выполнять вход на пользовательский портал учетной записи клиента.</span><span class="sxs-lookup"><span data-stu-id="dbb00-160">Use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="dbb00-161">На портале пользователей выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-161">In the user portal, select **New**.</span></span>

    ![Создайте новую виртуальную сеть](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. <span data-ttu-id="dbb00-163">Последовательно выберите пункты **Marketplace**, а затем выберите **сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-163">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="dbb00-164">Выберите **виртуальная сеть**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-164">Select **Virtual network**.</span></span>
5. <span data-ttu-id="dbb00-165">Для **имя**, **адресное пространство**, **имя подсети**, и **диапазон адресов подсети**, используйте значения, отображаемые в сети Таблица конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dbb00-165">For **Name**, **Address space**, **Subnet name**, and **Subnet address range**, use the values that appear earlier in the network configuration table.</span></span>
6. <span data-ttu-id="dbb00-166">В **подписки**, отображается подписки, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="dbb00-166">In **Subscription**, the subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="dbb00-167">Для **группы ресурсов**, можно создать группу ресурсов или если это уже сделано, установите **использовать существующие**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-167">For **Resource Group**, you can either create a resource group or if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="dbb00-168">Проверьте значение расположения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dbb00-168">Verify the default location.</span></span>
9. <span data-ttu-id="dbb00-169">Кроме того, установите флажок **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-169">Select **Pin to dashboard**.</span></span>
10. <span data-ttu-id="dbb00-170">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-170">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="dbb00-171">Создание подсети шлюза</span><span class="sxs-lookup"><span data-stu-id="dbb00-171">Create the gateway subnet</span></span>
1. <span data-ttu-id="dbb00-172">На панели мониторинга откройте ресурс виртуальной сети VNET-01, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="dbb00-172">On the dashboard, open the VNET-01 virtual network resource that you created earlier.</span></span>
2. <span data-ttu-id="dbb00-173">В колонке **Параметры** выберите **Подсети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-173">On the **Settings** blade, select **Subnets**.</span></span>
3. <span data-ttu-id="dbb00-174">Чтобы добавить подсеть шлюза виртуальной сети, выберите **подсеть шлюза**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-174">To add a gateway subnet to the virtual network, select **Gateway Subnet**.</span></span>
   
    ![Добавить подсеть шлюза](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. <span data-ttu-id="dbb00-176">По умолчанию присвоено имя подсети **GatewaySubnet**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-176">By default, the subnet name is set to **GatewaySubnet**.</span></span>
   <span data-ttu-id="dbb00-177">Шлюз подсети имеют специальное назначение.</span><span class="sxs-lookup"><span data-stu-id="dbb00-177">Gateway subnets are special.</span></span> <span data-ttu-id="dbb00-178">Для правильной работы функций, они должны использовать *GatewaySubnet* имя.</span><span class="sxs-lookup"><span data-stu-id="dbb00-178">To function properly, they must use the *GatewaySubnet* name.</span></span>
5. <span data-ttu-id="dbb00-179">В **диапазона адресов**, убедитесь, что адрес **10.0.11.0/24**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-179">In **Address range**, verify that the address is **10.0.11.0/24**.</span></span>
6. <span data-ttu-id="dbb00-180">Выберите **ОК** Создание подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="dbb00-180">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="dbb00-181">Создание шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="dbb00-181">Create the virtual network gateway</span></span>
1. <span data-ttu-id="dbb00-182">На портале Azure выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-182">In the Azure portal, select **New**.</span></span> 
2. <span data-ttu-id="dbb00-183">Последовательно выберите пункты **Marketplace**, а затем выберите **сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-183">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="dbb00-184">В списке сетевых ресурсов, выберите **шлюз виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-184">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="dbb00-185">В **имя**, введите **GW1**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-185">In **Name**, enter **GW1**.</span></span>
5. <span data-ttu-id="dbb00-186">Выберите **виртуальная сеть** элемент, чтобы выбрать виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="dbb00-186">Select the **Virtual network** item to choose a virtual network.</span></span>
   <span data-ttu-id="dbb00-187">Выберите **VNET-01** из списка.</span><span class="sxs-lookup"><span data-stu-id="dbb00-187">Select **VNET-01** from the list.</span></span>
6. <span data-ttu-id="dbb00-188">Выберите **общедоступный IP-адрес** элемента меню.</span><span class="sxs-lookup"><span data-stu-id="dbb00-188">Select the **Public IP address** menu item.</span></span> <span data-ttu-id="dbb00-189">Когда **выберите общедоступный IP-адрес** открывается колонка, выберите **создать новый**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-189">When the **Choose public IP address** blade opens, select **Create new**.</span></span>
7. <span data-ttu-id="dbb00-190">В **имя**, введите **GW1 PiP**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-190">In **Name**, enter **GW1-PiP**, and then select **OK**.</span></span>
8.  <span data-ttu-id="dbb00-191">По умолчанию для **тип VPN**, **на основе маршрутов** выбран.</span><span class="sxs-lookup"><span data-stu-id="dbb00-191">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="dbb00-192">Сохранить **на основе маршрутов** тип VPN.</span><span class="sxs-lookup"><span data-stu-id="dbb00-192">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="dbb00-193">Убедитесь, что для параметров **Подписка** и **Расположение** выбраны правильные значения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-193">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="dbb00-194">Вы можете закрепить ресурсов на панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="dbb00-194">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="dbb00-195">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-195">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway"></a><span data-ttu-id="dbb00-196">Создание шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="dbb00-196">Create the local network gateway</span></span>
<span data-ttu-id="dbb00-197">Реализация *шлюза локальной сети* в оценочном развертывании Azure Stack немного отличается от реализации в фактическом развертывании Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb00-197">The implementation of a *local network gateway* in this Azure Stack evaluation deployment is a bit different than in an actual Azure deployment.</span></span>

<span data-ttu-id="dbb00-198">При развертывании Azure шлюза локальной сети представляет локально (на клиенте) физического устройства, которое используется для подключения к шлюзу виртуальной сети в Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb00-198">In an Azure deployment, a local network gateway represents an on-premises (at the tenant) physical device, that you use to connect to a virtual network gateway in Azure.</span></span> <span data-ttu-id="dbb00-199">В таком сценарии вычислений Azure стека обоих концах соединения являются шлюзами виртуальной сети!</span><span class="sxs-lookup"><span data-stu-id="dbb00-199">In this Azure Stack evaluation deployment, both ends of the connection are virtual network gateways!</span></span>

<span data-ttu-id="dbb00-200">Представьте себе ситуацию, общем можно выполнить, ресурс шлюза локальной сети всегда указывает удаленный шлюз на другом конце соединения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-200">A way to think about this more generically is that the local network gateway resource always indicates the remote gateway at the other end of the connection.</span></span> <span data-ttu-id="dbb00-201">Из-за того, который был разработан пакет средств разработки Azure стека необходимо указать IP-адрес внешнего сетевого адаптера с преобразованием сетевых адресов (NAT) виртуальной Машины других Azure стека разработки набора как общедоступный IP-адрес шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="dbb00-201">Because of the way the Azure Stack Development Kit was designed, you need to provide the IP address of the external network adapter on the network address translation (NAT) VM of the other Azure Stack Development Kit as the Public IP Address of the local network gateway.</span></span> <span data-ttu-id="dbb00-202">Затем создайте сопоставление NAT на виртуальной Машине NAT, чтобы убедиться в том, что правильно подключены обеих сторон.</span><span class="sxs-lookup"><span data-stu-id="dbb00-202">You then create NAT mappings on the NAT VM to make sure that both ends are connected properly.</span></span>


### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="dbb00-203">Создать ресурс шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="dbb00-203">Create the local network gateway resource</span></span>
1. <span data-ttu-id="dbb00-204">Войдите на физическом компьютере Azure стека для POC1.</span><span class="sxs-lookup"><span data-stu-id="dbb00-204">Sign in to the Azure Stack physical machine for POC1.</span></span>
2. <span data-ttu-id="dbb00-205">На портале пользователей выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-205">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="dbb00-206">Последовательно выберите пункты **Marketplace**, а затем выберите **сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-206">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="dbb00-207">В списке ресурсов выберите **шлюз локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-207">From the list of resources, select **local network gateway**.</span></span>
5. <span data-ttu-id="dbb00-208">В **имя**, введите **POC2-GW**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-208">In **Name**, enter **POC2-GW**.</span></span>
6. <span data-ttu-id="dbb00-209">В **IP-адрес**, введите адрес внешнего BGPNAT POC2.</span><span class="sxs-lookup"><span data-stu-id="dbb00-209">In **IP address**, enter the External BGPNAT address for POC2.</span></span> <span data-ttu-id="dbb00-210">Этот адрес появляется в таблице конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="dbb00-210">This address appears earlier in the network configuration table.</span></span>
7. <span data-ttu-id="dbb00-211">В **адресное пространство**, адресное пространство виртуальной сети POC2, создаваемых в дальнейшем, введите **10.0.20.0/23**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-211">In **Address Space**, for the address space of the POC2 VNET that you create later, enter **10.0.20.0/23**.</span></span>
8. <span data-ttu-id="dbb00-212">Убедитесь, что ваш **подписки**, **группы ресурсов**, и **расположение** верны, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-212">Verify that your **Subscription**, **Resource Group**, and **location** are correct, and then select **Create**.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="dbb00-213">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="dbb00-213">Create the connection</span></span>
1. <span data-ttu-id="dbb00-214">На портале пользователей выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-214">In the user portal, select **New**.</span></span>
2. <span data-ttu-id="dbb00-215">Последовательно выберите пункты **Marketplace**, а затем выберите **сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-215">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="dbb00-216">В списке ресурсов выберите **соединения**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-216">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="dbb00-217">На **основы** колонку параметров для **тип подключения**выберите **-сайтами (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-217">On the **Basics** settings blade, for the **Connection type**, select **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="dbb00-218">Выберите **подписки**, **группы ресурсов**, и **расположение**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-218">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="dbb00-219">На **параметры** колонке выберите **шлюз виртуальной сети**, а затем выберите **GW1**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-219">On the **Settings** blade,  select **Virtual network gateway**, and then select **GW1**.</span></span>
7. <span data-ttu-id="dbb00-220">Выберите **шлюз локальной сети**, а затем выберите **POC2-GW**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-220">Select **Local network gateway**, and then select **POC2-GW**.</span></span>
8. <span data-ttu-id="dbb00-221">В **имя подключения**, введите **POC1 POC2**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-221">In **Connection Name**, enter **POC1-POC2**.</span></span>
9. <span data-ttu-id="dbb00-222">В **общий ключ (PSK)**, введите **12345**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-222">In **Shared key (PSK)**, enter **12345**, and then select **OK**.</span></span>
10. <span data-ttu-id="dbb00-223">На **Сводка** колонке выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-223">On the **Summary** blade, select **OK**.</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="dbb00-224">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="dbb00-224">Create a VM</span></span>
<span data-ttu-id="dbb00-225">Для проверки данных, проходящий через VPN-подключение, необходимо, чтобы виртуальные машины для отправки и получения данных в каждом пакете средств разработки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="dbb00-225">To validate the data that travels through the VPN connection, you need the virtual machines to send and receive data in each Azure Stack Development Kit.</span></span> <span data-ttu-id="dbb00-226">Создание виртуальной машины в POC1 теперь и в виртуальной сети, поместите его в вашей подсети виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="dbb00-226">Create a virtual machine in POC1 now, and then in your virtual network, put it on your VM subnet.</span></span>

1. <span data-ttu-id="dbb00-227">На портале Azure выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-227">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="dbb00-228">Последовательно выберите пункты **Marketplace**, а затем выберите **вычислений**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-228">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="dbb00-229">В списке образов виртуальных машин, выберите **Eval центра обработки данных Windows Server 2016** изображения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-229">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="dbb00-230">На **основы** колонки в **имя**, введите **VM01**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-230">On the **Basics** blade, in **Name**, enter **VM01**.</span></span>
5. <span data-ttu-id="dbb00-231">Введите допустимое имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="dbb00-231">Enter a valid username and password.</span></span> <span data-ttu-id="dbb00-232">Используйте эту учетную запись для входа в виртуальную Машину после ее создания.</span><span class="sxs-lookup"><span data-stu-id="dbb00-232">You use this account to sign in to the VM after it's created.</span></span>
6. <span data-ttu-id="dbb00-233">Предоставляют **подписки**, **группы ресурсов**, и **расположение**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-233">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="dbb00-234">На **размер** колонке для данного экземпляра, выберите размер виртуальной машины, а затем выберите **выберите**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-234">On the **Size** blade, for this instance, select a virtual machine size, and then select **Select**.</span></span>
8. <span data-ttu-id="dbb00-235">На **параметры** колонки, примите параметры по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dbb00-235">On the **Settings** blade, accept the defaults.</span></span> <span data-ttu-id="dbb00-236">Убедитесь, что **VNET-01** выбранной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="dbb00-236">Ensure that the **VNET-01** virtual network is selected.</span></span> <span data-ttu-id="dbb00-237">Убедитесь, что подсеть **10.0.10.0/24**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-237">Verify that the subnet is set to **10.0.10.0/24**.</span></span> <span data-ttu-id="dbb00-238">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-238">Then select **OK**.</span></span>
9. <span data-ttu-id="dbb00-239">На **Сводка** колонки, проверьте параметры, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-239">On the **Summary** blade, review the settings, and then select **OK**.</span></span>



## <a name="create-the-network-resources-in-poc2"></a><span data-ttu-id="dbb00-240">Создание сетевого ресурса в POC2</span><span class="sxs-lookup"><span data-stu-id="dbb00-240">Create the network resources in POC2</span></span>

<span data-ttu-id="dbb00-241">Следующим шагом является создание сетевого ресурса для POC2.</span><span class="sxs-lookup"><span data-stu-id="dbb00-241">The next step is to create the network resources for POC2.</span></span> <span data-ttu-id="dbb00-242">Ниже показано, как создать ресурсы с помощью пользовательского портала.</span><span class="sxs-lookup"><span data-stu-id="dbb00-242">The following instructions show how to create the resources by using the user portal.</span></span>

### <a name="sign-in-as-a-tenant"></a><span data-ttu-id="dbb00-243">Войдите в качестве клиента</span><span class="sxs-lookup"><span data-stu-id="dbb00-243">Sign in as a tenant</span></span>
<span data-ttu-id="dbb00-244">Администратором службы сможете войти как клиента для тестирования планов, предложения и подписки, которые могут использовать их клиентов.</span><span class="sxs-lookup"><span data-stu-id="dbb00-244">A service administrator can sign in as a tenant to test the plans, offers, and subscriptions that their tenants might use.</span></span> <span data-ttu-id="dbb00-245">Если вы уже нет, [создать учетную запись](azure-stack-add-new-user-aad.md) перед входом.</span><span class="sxs-lookup"><span data-stu-id="dbb00-245">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="dbb00-246">Создание виртуальной сети и подсети виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="dbb00-246">Create the virtual network and VM subnet</span></span>

1. <span data-ttu-id="dbb00-247">Войдите в систему с учетной записью клиента.</span><span class="sxs-lookup"><span data-stu-id="dbb00-247">Sign in by using a tenant account.</span></span>
2. <span data-ttu-id="dbb00-248">На портале пользователей выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-248">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="dbb00-249">Последовательно выберите пункты **Marketplace**, а затем выберите **сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-249">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="dbb00-250">Выберите **виртуальная сеть**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-250">Select **Virtual network**.</span></span>
5. <span data-ttu-id="dbb00-251">Используйте сведения, ранее в таблице конфигурации сети для определения значения для POC2 **имя**, **адресное пространство**, **имя подсети**и **Диапазон адресов подсети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-251">Use the information appearing earlier in the network configuration table to identify the values for the POC2 **Name**, **Address space**, **Subnet name**, and **Subnet address range**.</span></span>
6. <span data-ttu-id="dbb00-252">В **подписки**, отображается подписки, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="dbb00-252">In **Subscription**, the subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="dbb00-253">Для **группы ресурсов**, создать новую группу ресурсов или, если это уже сделано, установите **использовать существующие**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-253">For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="dbb00-254">Проверка стандартного **расположение**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-254">Verify the default **Location**.</span></span>
9. <span data-ttu-id="dbb00-255">Кроме того, установите флажок **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-255">Select **Pin to dashboard**.</span></span>
10. <span data-ttu-id="dbb00-256">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-256">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="dbb00-257">Создание подсети шлюза</span><span class="sxs-lookup"><span data-stu-id="dbb00-257">Create the Gateway Subnet</span></span>
1. <span data-ttu-id="dbb00-258">Открытие ресурса виртуальной сети, вы создали (**02 виртуальной сети**) с помощью панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="dbb00-258">Open the Virtual network resource you created (**VNET-02**) from the dashboard.</span></span>
2. <span data-ttu-id="dbb00-259">В колонке **Параметры** выберите **Подсети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-259">On the **Settings** blade, select **Subnets**.</span></span>
3. <span data-ttu-id="dbb00-260">Выберите **подсеть шлюза** Чтобы добавить подсеть шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="dbb00-260">Select  **Gateway subnet** to add a gateway subnet to the virtual network.</span></span>
4. <span data-ttu-id="dbb00-261">Подсети присвоено имя **GatewaySubnet** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dbb00-261">The name of the subnet is set to **GatewaySubnet** by default.</span></span>
   <span data-ttu-id="dbb00-262">Подсети шлюза являются специальными, и для правильной работы им должно быть присвоено конкретное имя.</span><span class="sxs-lookup"><span data-stu-id="dbb00-262">Gateway subnets are special and must have this specific name to function properly.</span></span>
5. <span data-ttu-id="dbb00-263">В **диапазона адресов** поле, убедитесь, что адрес **10.0.21.0/24**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-263">In the **Address range** field, verify the address is **10.0.21.0/24**.</span></span>
6. <span data-ttu-id="dbb00-264">Выберите **ОК** Создание подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="dbb00-264">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="dbb00-265">Создание шлюза виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="dbb00-265">Create the virtual network gateway</span></span>
1. <span data-ttu-id="dbb00-266">На портале Azure выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-266">In the Azure portal, select **New**.</span></span>  
2. <span data-ttu-id="dbb00-267">Последовательно выберите пункты **Marketplace**, а затем выберите **сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-267">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="dbb00-268">В списке сетевых ресурсов, выберите **шлюз виртуальной сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-268">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="dbb00-269">В **имя**, введите **GW2**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-269">In **Name**, enter **GW2**.</span></span>
5. <span data-ttu-id="dbb00-270">Чтобы выбрать виртуальную сеть, выберите **виртуальная сеть**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-270">To choose a virtual network, select **Virtual network**.</span></span> <span data-ttu-id="dbb00-271">Выберите **02 виртуальной сети** из списка.</span><span class="sxs-lookup"><span data-stu-id="dbb00-271">Then select **VNET-02** from the list.</span></span>
6. <span data-ttu-id="dbb00-272">Выберите **общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-272">Select **Public IP address**.</span></span> <span data-ttu-id="dbb00-273">Когда **выберите общедоступный IP-адрес** открывается колонка, выберите **создать новый**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-273">When the **Choose public IP address** blade opens, select **Create new**.</span></span>
7. <span data-ttu-id="dbb00-274">В **имя**, введите **GW2 PiP**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-274">In **Name**, enter **GW2-PiP**, and then select **OK**.</span></span>
8. <span data-ttu-id="dbb00-275">По умолчанию для **тип VPN**, **на основе маршрутов** выбран.</span><span class="sxs-lookup"><span data-stu-id="dbb00-275">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="dbb00-276">Сохранить **на основе маршрутов** тип VPN.</span><span class="sxs-lookup"><span data-stu-id="dbb00-276">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="dbb00-277">Убедитесь, что для параметров **Подписка** и **Расположение** выбраны правильные значения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-277">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="dbb00-278">Вы можете закрепить ресурсов на панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="dbb00-278">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="dbb00-279">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-279">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="dbb00-280">Создать ресурс шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="dbb00-280">Create the local network gateway resource</span></span>

1. <span data-ttu-id="dbb00-281">На портале пользователей POC2 выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-281">In the POC2 user portal, select **New**.</span></span> 
4. <span data-ttu-id="dbb00-282">Последовательно выберите пункты **Marketplace**, а затем выберите **сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-282">Go to **Marketplace**, and then select **Networking**.</span></span>
5. <span data-ttu-id="dbb00-283">В списке ресурсов выберите **шлюз локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-283">From the list of resources, select **Local network gateway**.</span></span>
6. <span data-ttu-id="dbb00-284">В **имя**, введите **POC1-GW**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-284">In **Name**, enter **POC1-GW**.</span></span>
7. <span data-ttu-id="dbb00-285">В **IP-адрес**, введите адрес внешнего BGPNAT POC1, перечисленные выше в таблице конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="dbb00-285">In **IP address**, enter the External BGPNAT address for POC1 that is listed earlier in the network configuration table.</span></span>
8. <span data-ttu-id="dbb00-286">В **адресное пространство**, POC1, введите следующую команду **10.0.10.0/23** адресное пространство **VNET-01**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-286">In **Address Space**, from POC1, enter the **10.0.10.0/23** address space of **VNET-01**.</span></span>
9. <span data-ttu-id="dbb00-287">Убедитесь, что ваш **подписки**, **группы ресурсов**, и **расположение** верны, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-287">Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="dbb00-288">Создание подключения</span><span class="sxs-lookup"><span data-stu-id="dbb00-288">Create the connection</span></span>
1. <span data-ttu-id="dbb00-289">На портале пользователей выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-289">In the user portal, select **New**.</span></span> 
2. <span data-ttu-id="dbb00-290">Последовательно выберите пункты **Marketplace**, а затем выберите **сети**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-290">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="dbb00-291">В списке ресурсов выберите **соединения**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-291">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="dbb00-292">На **основные** колонку параметров для **тип подключения**, выберите **-сайтами (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-292">On the **Basic** settings blade, for the **Connection type**, choose **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="dbb00-293">Выберите **подписки**, **группы ресурсов**, и **расположение**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-293">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="dbb00-294">На **параметры** колонке выберите **шлюз виртуальной сети**, а затем выберите **GW2**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-294">On the **Settings** blade, select **Virtual network gateway**, and then select **GW2**.</span></span>
7. <span data-ttu-id="dbb00-295">Выберите **шлюз локальной сети**, а затем выберите **POC1-GW**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-295">Select **Local network gateway**, and then select **POC1-GW**.</span></span>
8. <span data-ttu-id="dbb00-296">В **имя подключения**, введите **POC2 POC1**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-296">In **Connection name**, enter **POC2-POC1**.</span></span>
9. <span data-ttu-id="dbb00-297">В **общий ключ (PSK)**, введите **12345**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-297">In **Shared key (PSK)**, enter **12345**.</span></span> <span data-ttu-id="dbb00-298">Если выбрать другое значение, помните, что он *должен* соответствует значению для общий ключ, созданный на POC1.</span><span class="sxs-lookup"><span data-stu-id="dbb00-298">If you choose a different value, remember that it *must* match the value for the shared key that you created on POC1.</span></span> <span data-ttu-id="dbb00-299">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-299">Select **OK**.</span></span>
10. <span data-ttu-id="dbb00-300">Просмотрите **Сводка** колонки, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-300">Review the **Summary** blade, and then select **OK**.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="dbb00-301">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="dbb00-301">Create a virtual machine</span></span>
<span data-ttu-id="dbb00-302">Создание виртуальной машины в POC2 теперь и поместить его в вашей подсети виртуальной Машины в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="dbb00-302">Create a virtual machine in POC2 now, and put it on your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="dbb00-303">На портале Azure выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-303">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="dbb00-304">Последовательно выберите пункты **Marketplace**, а затем выберите **вычислений**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-304">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="dbb00-305">В списке образов виртуальных машин, выберите **Eval центра обработки данных Windows Server 2016** изображения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-305">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="dbb00-306">На **основы** колонке для **имя**, введите **VM02**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-306">On the **Basics** blade, for **Name**, enter **VM02**.</span></span>
5. <span data-ttu-id="dbb00-307">Введите допустимое имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="dbb00-307">Enter a valid username and password.</span></span> <span data-ttu-id="dbb00-308">Используйте эту учетную запись для входа в виртуальную машину после ее создания.</span><span class="sxs-lookup"><span data-stu-id="dbb00-308">You use this account to sign in to the virtual machine after it's created.</span></span>
6. <span data-ttu-id="dbb00-309">Предоставляют **подписки**, **группы ресурсов**, и **расположение**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-309">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="dbb00-310">На **размер** колонке выберите виртуальную машину, размер данного экземпляра, а затем выберите **выберите**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-310">On the **Size** blade, select a virtual machine size for this instance, and then select **Select**.</span></span>
8. <span data-ttu-id="dbb00-311">На **параметры** колонки, можно принять значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dbb00-311">On the **Settings** blade, you can accept the defaults.</span></span> <span data-ttu-id="dbb00-312">Убедитесь, что **02 виртуальной сети** выбран виртуальной сети и убедитесь, что подсеть **10.0.20.0/24**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-312">Ensure that the **VNET-02** virtual network is selected, and verify that the subnet is set to **10.0.20.0/24**.</span></span> <span data-ttu-id="dbb00-313">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-313">Select **OK**.</span></span>
9. <span data-ttu-id="dbb00-314">Проверьте параметры на **Сводка** колонки, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-314">Review the settings on the **Summary** blade, and then select **OK**.</span></span>

## <a name="configure-the-nat-virtual-machine-on-each-azure-stack-development-kit-for-gateway-traversal"></a><span data-ttu-id="dbb00-315">Настройте виртуальную машину NAT на каждый пакет средств разработки Azure стека для обхода шлюза</span><span class="sxs-lookup"><span data-stu-id="dbb00-315">Configure the NAT virtual machine on each Azure Stack Development Kit for gateway traversal</span></span>
<span data-ttu-id="dbb00-316">Так как пакет средств разработки Azure стека самодостаточны и изолированы от сети, на котором развертывается физического узла, *внешних* виртуальных IP-адресов сети, шлюзы, подключенные к не является фактически внешним.</span><span class="sxs-lookup"><span data-stu-id="dbb00-316">Because the Azure Stack Development Kit is self-contained and isolated from the network on which the physical host is deployed, the *external* VIP network that the gateways are connected to is not actually external.</span></span> <span data-ttu-id="dbb00-317">Вместо этого виртуальный IP-адрес сети скрыто вне маршрутизатора, который выполняет преобразование сетевых адресов.</span><span class="sxs-lookup"><span data-stu-id="dbb00-317">Instead, the VIP network is hidden behind a router that performs network address translation.</span></span> 

<span data-ttu-id="dbb00-318">Этот маршрутизатор является виртуальная машина Windows Server, с именем *AzS bgpnat01*, роли маршрутизации и удаленного доступа (RRAS), работающий в инфраструктуре Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="dbb00-318">The router is a Windows Server virtual machine, called *AzS-bgpnat01*, that runs the Routing and Remote Access Services (RRAS) role in the Azure Stack Development Kit infrastructure.</span></span> <span data-ttu-id="dbb00-319">Необходимо настроить NAT на виртуальной машине AzS bgpnat01, чтобы разрешить VPN-подключения сеть сеть для подключения на обоих концах.</span><span class="sxs-lookup"><span data-stu-id="dbb00-319">You must configure NAT on the AzS-bgpnat01 virtual machine to allow the site-to-site VPN connection to connect on both ends.</span></span> 

<span data-ttu-id="dbb00-320">Чтобы настроить VPN-подключение, необходимо создать статических маршрутов карты NAT, который сопоставляется внешний интерфейс на виртуальной машине BGPNAT виртуальный IP-адрес шлюза пула ребер.</span><span class="sxs-lookup"><span data-stu-id="dbb00-320">To configure the VPN connection, you must create a static NAT map route that maps the external interface on the BGPNAT virtual machine to the VIP of the Edge Gateway Pool.</span></span> <span data-ttu-id="dbb00-321">Статический маршрут NAT карты является обязательным для каждого порта в VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-321">A static NAT map route is required for each port in a VPN connection.</span></span>

> [!NOTE]
> <span data-ttu-id="dbb00-322">Эта конфигурация требуется пакет средств разработки Azure стека только для сред.</span><span class="sxs-lookup"><span data-stu-id="dbb00-322">This configuration is required for Azure Stack Development Kit environments only.</span></span>
> 
> 

### <a name="configure-the-nat"></a><span data-ttu-id="dbb00-323">Настройка преобразования сетевых адресов</span><span class="sxs-lookup"><span data-stu-id="dbb00-323">Configure the NAT</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dbb00-324">Необходимо выполнить эту процедуру для *оба* средах Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="dbb00-324">You must complete this procedure for *both* Azure Stack Development Kit environments.</span></span>

1. <span data-ttu-id="dbb00-325">Определить **внутренний IP-адрес** для использования в следующий сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dbb00-325">Determine the **Internal IP address** to use in the following PowerShell script.</span></span> <span data-ttu-id="dbb00-326">Откройте шлюз виртуальной сети (GW1 и GW2), а затем на **Общие сведения о** колонке сохранить значение для **общедоступный IP-адрес** для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="dbb00-326">Open the virtual network gateway (GW1 and GW2), and then on the **Overview** blade, save the value for the **Public IP address** for later use.</span></span>
<span data-ttu-id="dbb00-327">![Внутренний IP-адрес](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)</span><span class="sxs-lookup"><span data-stu-id="dbb00-327">![Internal IP address](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)</span></span>
2. <span data-ttu-id="dbb00-328">Войдите на физическом компьютере Azure стека для POC1.</span><span class="sxs-lookup"><span data-stu-id="dbb00-328">Sign in to the Azure Stack physical machine for POC1.</span></span>
3. <span data-ttu-id="dbb00-329">Скопируйте и измените следующий сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dbb00-329">Copy and edit the following PowerShell script.</span></span> <span data-ttu-id="dbb00-330">Настройка NAT на каждый пакет средств разработки Azure стек, запустите сценарий в с повышенными привилегиями Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="dbb00-330">To configure the NAT on each Azure Stack Development Kit, run the script in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="dbb00-331">В скрипте, добавив значения *BGPNAT внешний адрес* и *внутренний IP-адрес* заполнители:</span><span class="sxs-lookup"><span data-stu-id="dbb00-331">In the script, add values to the *External BGPNAT address* and *Internal IP address* placeholders:</span></span>

   ```powershell
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
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
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

4. <span data-ttu-id="dbb00-332">Повторите эту процедуру на POC2.</span><span class="sxs-lookup"><span data-stu-id="dbb00-332">Repeat this procedure on POC2.</span></span>

## <a name="test-the-connection"></a><span data-ttu-id="dbb00-333">Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="dbb00-333">Test the connection</span></span>
<span data-ttu-id="dbb00-334">Теперь, когда устанавливается соединение сайт сайт, следует проверить, что может получить трафик через него.</span><span class="sxs-lookup"><span data-stu-id="dbb00-334">Now that the site-to-site connection is established, you should validate that you can get traffic flowing through it.</span></span> <span data-ttu-id="dbb00-335">Чтобы проверить, войдите в одной из виртуальных машин, созданных в среде Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="dbb00-335">To validate, sign in to one of the virtual machines that you created in either Azure Stack Development Kit environment.</span></span> <span data-ttu-id="dbb00-336">Затем проверьте связь виртуальной машины, созданной в другой среде.</span><span class="sxs-lookup"><span data-stu-id="dbb00-336">Then, ping the virtual machine that you created in the other environment.</span></span> 

<span data-ttu-id="dbb00-337">Чтобы убедиться, что отправляется трафик через подключение сайт сайт, убедитесь, выполнить команду ping адрес прямой IP-адрес (DIP) виртуальной машины на удаленной подсети не виртуальных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="dbb00-337">To ensure that you send the traffic through the site-to-site connection, ensure that you ping the Direct IP (DIP) address of the virtual machine on the remote subnet, not the VIP.</span></span> <span data-ttu-id="dbb00-338">Для этого найдите DIP-адрес на другой стороне соединения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-338">To do this, find the DIP address on the other end of the connection.</span></span> <span data-ttu-id="dbb00-339">Сохраните адрес для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="dbb00-339">Save the address for later use.</span></span>

### <a name="sign-in-to-the-tenant-vm-in-poc1"></a><span data-ttu-id="dbb00-340">Войдите в клиент виртуальной Машины в POC1</span><span class="sxs-lookup"><span data-stu-id="dbb00-340">Sign in to the tenant VM in POC1</span></span>
1. <span data-ttu-id="dbb00-341">Войдите на физическом компьютере Azure стека для POC1 и затем выполнять вход на пользовательский портал учетной записи клиента.</span><span class="sxs-lookup"><span data-stu-id="dbb00-341">Sign in to the Azure Stack physical machine for POC1, and then use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="dbb00-342">На панели навигации слева выберите **вычислений**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-342">In the left navigation bar, select **Compute**.</span></span>
3. <span data-ttu-id="dbb00-343">В списке виртуальных машин, найдите **VM01** , созданного ранее и выберите его.</span><span class="sxs-lookup"><span data-stu-id="dbb00-343">In the list of VMs, find **VM01** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="dbb00-344">В колонке виртуальной машины, нажмите кнопку **Connect**, а затем откройте файл VM01.rdp.</span><span class="sxs-lookup"><span data-stu-id="dbb00-344">On the blade for the virtual machine, click **Connect**, and then open the VM01.rdp file.</span></span>
   
     ![Кнопка "Подключить"](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. <span data-ttu-id="dbb00-346">Войдите с помощью учетной записи, настроенной при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dbb00-346">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="dbb00-347">Откройте повышенными **Windows PowerShell** окна.</span><span class="sxs-lookup"><span data-stu-id="dbb00-347">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="dbb00-348">Введите **ipconfig/all**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-348">Enter **ipconfig /all**.</span></span>
8. <span data-ttu-id="dbb00-349">Найдите в выходных данных, **IPv4-адрес**, а затем сохраните адрес для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="dbb00-349">In the output, find the **IPv4 Address**, and then save the address for later use.</span></span> <span data-ttu-id="dbb00-350">Это адрес, который будет проверять связь с POC2.</span><span class="sxs-lookup"><span data-stu-id="dbb00-350">This is the address that you will ping from POC2.</span></span> <span data-ttu-id="dbb00-351">В примере среды этот адрес — **10.0.10.4**, но в вашей среде он может быть другим.</span><span class="sxs-lookup"><span data-stu-id="dbb00-351">In the example environment, the address is **10.0.10.4**, but in your environment it might be different.</span></span> <span data-ttu-id="dbb00-352">Он должен находиться в **10.0.10.0/24** подсети, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="dbb00-352">It should fall within the **10.0.10.0/24** subnet that you created previously.</span></span>
9. <span data-ttu-id="dbb00-353">Чтобы создать правило брандмауэра, которое позволяет реагировать на запросы проверки связи виртуальную машину, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dbb00-353">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-to-the-tenant-vm-in-poc2"></a><span data-ttu-id="dbb00-354">Войдите в клиент виртуальной Машины в POC2</span><span class="sxs-lookup"><span data-stu-id="dbb00-354">Sign in to the tenant VM in POC2</span></span>
1. <span data-ttu-id="dbb00-355">Войдите на физическом компьютере Azure стека для POC2 и затем выполнять вход на пользовательский портал учетной записи клиента.</span><span class="sxs-lookup"><span data-stu-id="dbb00-355">Sign in to the Azure Stack physical machine for POC2, and then use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="dbb00-356">На панели навигации слева щелкните **вычислений**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-356">In the left navigation bar, click **Compute**.</span></span>
3. <span data-ttu-id="dbb00-357">В списке виртуальных машин, найти **VM02** , созданного ранее и выберите его.</span><span class="sxs-lookup"><span data-stu-id="dbb00-357">From the list of virtual machines, find **VM02** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="dbb00-358">В колонке виртуальной машины щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-358">On the blade for the virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="dbb00-359">Войдите с помощью учетной записи, настроенной при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dbb00-359">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="dbb00-360">Откройте повышенными **Windows PowerShell** окна.</span><span class="sxs-lookup"><span data-stu-id="dbb00-360">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="dbb00-361">Введите **ipconfig/all**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-361">Enter **ipconfig /all**.</span></span>
8. <span data-ttu-id="dbb00-362">Вы увидите IPv4-адрес, который попадает в **10.0.20.0/24**.</span><span class="sxs-lookup"><span data-stu-id="dbb00-362">You should see an IPv4 address that falls within **10.0.20.0/24**.</span></span> <span data-ttu-id="dbb00-363">В среде примере является адрес **10.0.20.4**, но ваш адрес может различаться.</span><span class="sxs-lookup"><span data-stu-id="dbb00-363">In the example environment, the address is **10.0.20.4**, but your address might be different.</span></span>
9. <span data-ttu-id="dbb00-364">Чтобы создать правило брандмауэра, которое позволяет реагировать на запросы проверки связи виртуальную машину, выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dbb00-364">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. <span data-ttu-id="dbb00-365">На виртуальной машине POC2 проверьте связь с виртуальной машины на POC1, через туннель.</span><span class="sxs-lookup"><span data-stu-id="dbb00-365">From the virtual machine on POC2, ping the virtual machine on POC1, through the tunnel.</span></span> <span data-ttu-id="dbb00-366">Чтобы сделать это, проверьте связь DIP, записанное на VM01.</span><span class="sxs-lookup"><span data-stu-id="dbb00-366">To do this, you ping the DIP that you recorded from VM01.</span></span>
   <span data-ttu-id="dbb00-367">В среде примере это **10.0.10.4**, но необходимо обязательно обратитесь по адресу, записанное в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="dbb00-367">In the example environment, this is **10.0.10.4**, but be sure to ping the address you noted in your lab.</span></span> <span data-ttu-id="dbb00-368">Вы увидите результат, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dbb00-368">You should see a result that looks like the following:</span></span>
   
    ![Успешная проверка связи](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. <span data-ttu-id="dbb00-370">Ответ от удаленной виртуальной машины указывает успешного завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="dbb00-370">A reply from the remote virtual machine indicates a successful test!</span></span> <span data-ttu-id="dbb00-371">Можно закрыть окна виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dbb00-371">You can close the virtual machine window.</span></span> <span data-ttu-id="dbb00-372">Можно проверить подключение, можно попробовать другие виды передачах данных, таких как копирование файлов.</span><span class="sxs-lookup"><span data-stu-id="dbb00-372">To test your connection, you can try other kinds of data transfers like a file copy.</span></span>

### <a name="viewing-data-transfer-statistics-through-the-gateway-connection"></a><span data-ttu-id="dbb00-373">Просмотр статистики передачи данных через подключение шлюза</span><span class="sxs-lookup"><span data-stu-id="dbb00-373">Viewing data transfer statistics through the gateway connection</span></span>
<span data-ttu-id="dbb00-374">Если вы хотите знать, сколько данных проходит через сайт сайт подключения, эта информация доступна на **подключения** колонку.</span><span class="sxs-lookup"><span data-stu-id="dbb00-374">If you want to know how much data passes through your site-to-site connection, this information is available on the **Connection** blade.</span></span> <span data-ttu-id="dbb00-375">Этот тест также является другим способом, чтобы убедиться, что ping, который вы только что отправлен на самом деле пошло через VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="dbb00-375">This test is also another way to verify that the ping you just sent actually went through the VPN connection.</span></span>

1. <span data-ttu-id="dbb00-376">Во время выполнен вход на виртуальную машину клиента в POC2, выполнять вход на пользовательский портал учетной записи клиента.</span><span class="sxs-lookup"><span data-stu-id="dbb00-376">While you're signed in to the tenant virtual machine in POC2, use your tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="dbb00-377">Последовательно выберите пункты **все ресурсы**, а затем выберите **POC2 POC1** соединения.</span><span class="sxs-lookup"><span data-stu-id="dbb00-377">Go to **All resources**, and then select the **POC2-POC1** connection.</span></span> <span data-ttu-id="dbb00-378">**Подключения** отображается.</span><span class="sxs-lookup"><span data-stu-id="dbb00-378">**Connections** appears.</span></span>
4. <span data-ttu-id="dbb00-379">На **подключения** колонки, статистика для **данные в** и **исходящие данные** отображаются.</span><span class="sxs-lookup"><span data-stu-id="dbb00-379">On the **Connection** blade, the statistics for **Data in** and **Data out** appear.</span></span> <span data-ttu-id="dbb00-380">На следующем снимке экрана больших чисел достигается за счет передачи дополнительных файлов.</span><span class="sxs-lookup"><span data-stu-id="dbb00-380">In the following screenshot, the large numbers are attributed to additional file transfer.</span></span> <span data-ttu-id="dbb00-381">Вы увидите некоторые ненулевых значений.</span><span class="sxs-lookup"><span data-stu-id="dbb00-381">You should see some nonzero values there.</span></span>
   
    ![Данные, in и out](media/azure-stack-create-vpn-connection-one-node-tp2/image20.png)
