<span data-ttu-id="5ea26-101">Hello действия для этой задачи используйте виртуальную сеть на основе hello значений в следующий список ссылок на конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="5ea26-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="5ea26-102">В этом списке также приведены дополнительные параметры и имена.</span><span class="sxs-lookup"><span data-stu-id="5ea26-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="5ea26-103">Мы не используем этот список непосредственно в любом из этапов hello, несмотря на то, что мы добавляем переменных, основанных на значениях hello в этот список.</span><span class="sxs-lookup"><span data-stu-id="5ea26-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="5ea26-104">Можно скопировать toouse список hello как ссылка, заменив значения hello собственные.</span><span class="sxs-lookup"><span data-stu-id="5ea26-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="5ea26-105">**Справочный список для конфигурации**</span><span class="sxs-lookup"><span data-stu-id="5ea26-105">**Configuration reference list**</span></span>

* <span data-ttu-id="5ea26-106">Имя виртуальной сети: TestVNet.</span><span class="sxs-lookup"><span data-stu-id="5ea26-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="5ea26-107">Адресное пространство виртуальной сети: 192.168.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="5ea26-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="5ea26-108">Группа ресурсов — TestRG.</span><span class="sxs-lookup"><span data-stu-id="5ea26-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="5ea26-109">Имя подсети Subnet1: FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="5ea26-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="5ea26-110">Адресное пространство Subnet1: 192.168.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="5ea26-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="5ea26-111">Имя подсети шлюза: GatewaySubnet; подсеть шлюза всегда необходимо называть *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="5ea26-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="5ea26-112">Адресное пространство шлюза подсети: 192.168.200.0/26.</span><span class="sxs-lookup"><span data-stu-id="5ea26-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="5ea26-113">Расположение — East US.</span><span class="sxs-lookup"><span data-stu-id="5ea26-113">Region = "East US"</span></span>
* <span data-ttu-id="5ea26-114">Имя шлюза: GW.</span><span class="sxs-lookup"><span data-stu-id="5ea26-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="5ea26-115">IP-имя шлюза: GWIP.</span><span class="sxs-lookup"><span data-stu-id="5ea26-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="5ea26-116">Имя конфигурации IP-адресов шлюза: gwipconf.</span><span class="sxs-lookup"><span data-stu-id="5ea26-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="5ea26-117">Type = "ExpressRoute". Для настройки ExpressRoute требуется этот тип.</span><span class="sxs-lookup"><span data-stu-id="5ea26-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="5ea26-118">Общедоступное IP-имя шлюза: gwpip.</span><span class="sxs-lookup"><span data-stu-id="5ea26-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="5ea26-119">Добавление шлюза</span><span class="sxs-lookup"><span data-stu-id="5ea26-119">Add a gateway</span></span>
1. <span data-ttu-id="5ea26-120">Подключите tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea26-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="5ea26-121">Объявите переменные для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="5ea26-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="5ea26-122">Быть убедиться, что tooedit hello tooreflect образец hello параметры, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="5ea26-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="5ea26-123">Хранится в переменной hello объекта виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5ea26-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="5ea26-124">Добавьте tooyour подсети шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5ea26-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="5ea26-125">подсеть шлюза Hello должен называться «GatewaySubnet».</span><span class="sxs-lookup"><span data-stu-id="5ea26-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="5ea26-126">Потребуется создать шлюз с префиксом /27 или больше (26, 25 и т. д.).</span><span class="sxs-lookup"><span data-stu-id="5ea26-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="5ea26-127">Задание конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="5ea26-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="5ea26-128">Подсеть шлюза hello хранится в переменной.</span><span class="sxs-lookup"><span data-stu-id="5ea26-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="5ea26-129">Запросите общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5ea26-129">Request a public IP address.</span></span> <span data-ttu-id="5ea26-130">Перед созданием шлюза hello запрашивается Hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="5ea26-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="5ea26-131">Нельзя указать hello IP-адреса, которые должны toouse; он выделяется динамически.</span><span class="sxs-lookup"><span data-stu-id="5ea26-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="5ea26-132">Этот IP-адрес будет использоваться в следующем разделе конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="5ea26-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="5ea26-133">Hello AllocationMethod должны быть динамическими.</span><span class="sxs-lookup"><span data-stu-id="5ea26-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="5ea26-134">Создайте конфигурацию hello для шлюза.</span><span class="sxs-lookup"><span data-stu-id="5ea26-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="5ea26-135">Конфигурация шлюза Hello определяет подсеть hello и hello открытый IP адрес toouse.</span><span class="sxs-lookup"><span data-stu-id="5ea26-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="5ea26-136">На этом шаге вы указываете hello конфигурации, который будет использоваться при создании шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="5ea26-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="5ea26-137">Этот шаг не создает hello объекта шлюза.</span><span class="sxs-lookup"><span data-stu-id="5ea26-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="5ea26-138">Использование образца hello ниже toocreate конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="5ea26-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="5ea26-139">Создайте шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="5ea26-139">Create hello gateway.</span></span> <span data-ttu-id="5ea26-140">На этом шаге hello **- тип шлюза** особенно важна.</span><span class="sxs-lookup"><span data-stu-id="5ea26-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="5ea26-141">Необходимо использовать значение hello **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="5ea26-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="5ea26-142">После выполнения этих командлетов, hello шлюза может занять 45 минут или более toocreate.</span><span class="sxs-lookup"><span data-stu-id="5ea26-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="5ea26-143">Убедитесь, что был создан шлюз hello</span><span class="sxs-lookup"><span data-stu-id="5ea26-143">Verify hello gateway was created</span></span>
<span data-ttu-id="5ea26-144">Используйте следующие команды, созданных tooverify, hello шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="5ea26-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="5ea26-145">Изменение размера шлюза</span><span class="sxs-lookup"><span data-stu-id="5ea26-145">Resize a gateway</span></span>
<span data-ttu-id="5ea26-146">Существует несколько [номеров SKU шлюзов](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="5ea26-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="5ea26-147">Можно использовать hello, следующая команда toochange hello номер SKU шлюза в любое время.</span><span class="sxs-lookup"><span data-stu-id="5ea26-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ea26-148">Эта команда не работает для шлюза UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="5ea26-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="5ea26-149">toochange tooan UltraPerformance шлюз шлюз, сначала удалите существующий шлюз ExpressRoute hello и создайте новый шлюз UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="5ea26-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="5ea26-150">удалите шлюз с шлюзом UltraPerformance toodowngrade hello UltraPerformance шлюза, а затем создайте новый шлюз.</span><span class="sxs-lookup"><span data-stu-id="5ea26-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="5ea26-151">Удаление шлюза</span><span class="sxs-lookup"><span data-stu-id="5ea26-151">Remove a gateway</span></span>
<span data-ttu-id="5ea26-152">Используйте следующие команды tooremove шлюз hello:</span><span class="sxs-lookup"><span data-stu-id="5ea26-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```