<span data-ttu-id="8808b-101">Для выполнения этой задачи используйте виртуальную сеть со значениями, приведенными в справочном списке для настройки ниже.</span><span class="sxs-lookup"><span data-stu-id="8808b-101">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="8808b-102">В этом списке также приведены дополнительные параметры и имена.</span><span class="sxs-lookup"><span data-stu-id="8808b-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="8808b-103">Мы не используем этот список непосредственно ни на каком из шагов, несмотря на то, что добавляем переменные согласно значениям в этом списке.</span><span class="sxs-lookup"><span data-stu-id="8808b-103">We don't use this list directly in any of the steps, although we do add variables based on the values in this list.</span></span> <span data-ttu-id="8808b-104">Вы можете скопировать список для справки, заменив значения собственными.</span><span class="sxs-lookup"><span data-stu-id="8808b-104">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="8808b-105">**Справочный список для конфигурации**</span><span class="sxs-lookup"><span data-stu-id="8808b-105">**Configuration reference list**</span></span>

* <span data-ttu-id="8808b-106">Имя виртуальной сети: TestVNet.</span><span class="sxs-lookup"><span data-stu-id="8808b-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="8808b-107">Адресное пространство виртуальной сети: 192.168.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="8808b-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="8808b-108">Группа ресурсов — TestRG.</span><span class="sxs-lookup"><span data-stu-id="8808b-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="8808b-109">Имя подсети Subnet1: FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="8808b-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="8808b-110">Адресное пространство Subnet1: 192.168.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="8808b-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="8808b-111">Имя подсети шлюза: GatewaySubnet; подсеть шлюза всегда необходимо называть *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="8808b-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="8808b-112">Адресное пространство шлюза подсети: 192.168.200.0/26.</span><span class="sxs-lookup"><span data-stu-id="8808b-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="8808b-113">Расположение — East US.</span><span class="sxs-lookup"><span data-stu-id="8808b-113">Region = "East US"</span></span>
* <span data-ttu-id="8808b-114">Имя шлюза: GW.</span><span class="sxs-lookup"><span data-stu-id="8808b-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="8808b-115">IP-имя шлюза: GWIP.</span><span class="sxs-lookup"><span data-stu-id="8808b-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="8808b-116">Имя конфигурации IP-адресов шлюза: gwipconf.</span><span class="sxs-lookup"><span data-stu-id="8808b-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="8808b-117">Type = "ExpressRoute". Для настройки ExpressRoute требуется этот тип.</span><span class="sxs-lookup"><span data-stu-id="8808b-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="8808b-118">Общедоступное IP-имя шлюза: gwpip.</span><span class="sxs-lookup"><span data-stu-id="8808b-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="8808b-119">Добавление шлюза</span><span class="sxs-lookup"><span data-stu-id="8808b-119">Add a gateway</span></span>
1. <span data-ttu-id="8808b-120">Подключитесь к своей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="8808b-120">Connect to your Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="8808b-121">Объявите переменные для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="8808b-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="8808b-122">Не забудьте изменить пример в соответствии с параметрами, которые вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="8808b-122">Be sure to edit the sample to reflect the settings that you want to use.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="8808b-123">Сохраните объект виртуальной сети как переменную.</span><span class="sxs-lookup"><span data-stu-id="8808b-123">Store the virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="8808b-124">Создайте подсеть шлюза своей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="8808b-124">Add a gateway subnet to your Virtual Network.</span></span> <span data-ttu-id="8808b-125">Подсеть шлюза должна иметь имя GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="8808b-125">The gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="8808b-126">Потребуется создать шлюз с префиксом /27 или больше (26, 25 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="8808b-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="8808b-127">Теперь нужно настроить конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="8808b-127">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="8808b-128">Сохраните подсеть шлюза как переменную.</span><span class="sxs-lookup"><span data-stu-id="8808b-128">Store the gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="8808b-129">Запросите общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="8808b-129">Request a public IP address.</span></span> <span data-ttu-id="8808b-130">IP-адрес запрашивается перед созданием шлюза.</span><span class="sxs-lookup"><span data-stu-id="8808b-130">The IP address is requested before creating the gateway.</span></span> <span data-ttu-id="8808b-131">Указать необходимый IP-адрес нельзя, он выделяется динамически.</span><span class="sxs-lookup"><span data-stu-id="8808b-131">You cannot specify the IP address that you want to use; it’s dynamically allocated.</span></span> <span data-ttu-id="8808b-132">Этот IP-адрес будет использоваться на следующем этапе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8808b-132">You'll use this IP address in the next configuration section.</span></span> <span data-ttu-id="8808b-133">Параметр AllocationMethod должен иметь значение Dynamic.</span><span class="sxs-lookup"><span data-stu-id="8808b-133">The AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="8808b-134">Создайте конфигурацию для шлюза.</span><span class="sxs-lookup"><span data-stu-id="8808b-134">Create the configuration for your gateway.</span></span> <span data-ttu-id="8808b-135">Конфигурация шлюза определяет используемые подсеть и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="8808b-135">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="8808b-136">На этом шаге вы задаете конфигурацию, которая будет использоваться при создании шлюза.</span><span class="sxs-lookup"><span data-stu-id="8808b-136">In this step, you are specifying the configuration that will be used when you create the gateway.</span></span> <span data-ttu-id="8808b-137">Но пока объект шлюза не создается.</span><span class="sxs-lookup"><span data-stu-id="8808b-137">This step does not actually create the gateway object.</span></span> <span data-ttu-id="8808b-138">Используйте следующий пример, чтобы создать конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="8808b-138">Use the sample below to create your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="8808b-139">Создайте шлюз.</span><span class="sxs-lookup"><span data-stu-id="8808b-139">Create the gateway.</span></span> <span data-ttu-id="8808b-140">На этом шаге особенно важен параметр **-GatewayType** .</span><span class="sxs-lookup"><span data-stu-id="8808b-140">In this step, the **-GatewayType** is especially important.</span></span> <span data-ttu-id="8808b-141">Необходимо использовать значение **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="8808b-141">You must use the value **ExpressRoute**.</span></span> <span data-ttu-id="8808b-142">После выполнения этих командлетов на создание шлюза может потребоваться 45 минут или больше.</span><span class="sxs-lookup"><span data-stu-id="8808b-142">After running these cmdlets, the gateway can take 45 minutes or more to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="8808b-143">Проверка создания шлюза</span><span class="sxs-lookup"><span data-stu-id="8808b-143">Verify the gateway was created</span></span>
<span data-ttu-id="8808b-144">Используйте следующую команду, чтобы проверить, был ли создан шлюз:</span><span class="sxs-lookup"><span data-stu-id="8808b-144">Use the following commands to verify that the gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="8808b-145">Изменение размера шлюза</span><span class="sxs-lookup"><span data-stu-id="8808b-145">Resize a gateway</span></span>
<span data-ttu-id="8808b-146">Существует несколько [номеров SKU шлюзов](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="8808b-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="8808b-147">Чтобы изменить SKU шлюза в любое время, можно использовать следующую команду.</span><span class="sxs-lookup"><span data-stu-id="8808b-147">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8808b-148">Эта команда не работает для шлюза UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="8808b-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="8808b-149">Чтобы заменить шлюз на UltraPerformance, сначала удалите существующий шлюз ExpressRoute, а затем создайте шлюз UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="8808b-149">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="8808b-150">Чтобы заменить шлюз UltraPerformance обычным шлюзом, сначала удалите шлюз UltraPerformance, а затем создайте новый шлюз.</span><span class="sxs-lookup"><span data-stu-id="8808b-150">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="8808b-151">Удаление шлюза</span><span class="sxs-lookup"><span data-stu-id="8808b-151">Remove a gateway</span></span>
<span data-ttu-id="8808b-152">Чтобы удалить шлюз, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8808b-152">Use the following command to remove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```