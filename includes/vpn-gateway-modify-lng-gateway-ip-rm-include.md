### <span data-ttu-id="ac450-101"><a name="gwipnoconnection"></a> Изменение шлюза локальной сети с использованием GatewayIpAddress при отсутствии подключения к шлюзу</span><span class="sxs-lookup"><span data-stu-id="ac450-101"><a name="gwipnoconnection"></a> To modify the local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="ac450-102">Если общедоступный IP-адрес VPN-устройства, к которому вы хотите подключиться, изменился, измените шлюз локальной сети в соответствии с изменениями.</span><span class="sxs-lookup"><span data-stu-id="ac450-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="ac450-103">Используйте пример ниже, чтобы изменить шлюз локальной сети, к которому нет подключения.</span><span class="sxs-lookup"><span data-stu-id="ac450-103">Use the example to modify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="ac450-104">При изменении этого значения вы также можете изменить префиксы адресов.</span><span class="sxs-lookup"><span data-stu-id="ac450-104">When modifying this value, you can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="ac450-105">Не забудьте указать имеющееся имя шлюза локальной сети для перезаписи текущих параметров.</span><span class="sxs-lookup"><span data-stu-id="ac450-105">Be sure to use the existing name of your local network gateway in order to overwrite the current settings.</span></span> <span data-ttu-id="ac450-106">Если используется другое имя, необходимо создать новый шлюз локальной сети вместо перезаписи существующего.</span><span class="sxs-lookup"><span data-stu-id="ac450-106">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="ac450-107"><a name="gwipwithconnection"></a> Изменение шлюза локальной сети с использованием GatewayIpAddress, если подключение к шлюзу установлено</span><span class="sxs-lookup"><span data-stu-id="ac450-107"><a name="gwipwithconnection"></a>To modify the local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="ac450-108">Если общедоступный IP-адрес VPN-устройства, к которому вы хотите подключиться, изменился, измените шлюз локальной сети в соответствии с изменениями.</span><span class="sxs-lookup"><span data-stu-id="ac450-108">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="ac450-109">Если шлюз уже подключен, сначала вам нужно удалить подключение.</span><span class="sxs-lookup"><span data-stu-id="ac450-109">If a gateway connection already exists, you first need to remove the connection.</span></span> <span data-ttu-id="ac450-110">Затем вы сможете изменить IP-адрес шлюза и создать новое подключение.</span><span class="sxs-lookup"><span data-stu-id="ac450-110">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="ac450-111">При этом вы также можете изменить префиксы адресов.</span><span class="sxs-lookup"><span data-stu-id="ac450-111">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="ac450-112">После этого VPN-подключение будет некоторое время недоступно.</span><span class="sxs-lookup"><span data-stu-id="ac450-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="ac450-113">Не удаляйте VPN-шлюз при изменении IP-адреса шлюза.</span><span class="sxs-lookup"><span data-stu-id="ac450-113">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="ac450-114">Необходимо удалить только подключение.</span><span class="sxs-lookup"><span data-stu-id="ac450-114">You only need to remove the connection.</span></span>
 

1. <span data-ttu-id="ac450-115">Удалите подключение.</span><span class="sxs-lookup"><span data-stu-id="ac450-115">Remove the connection.</span></span> <span data-ttu-id="ac450-116">Вы можете найти имя своего подключения с помощью командлета Get-AzureRmVirtualNetworkGatewayConnection.</span><span class="sxs-lookup"><span data-stu-id="ac450-116">You can find the name of your connection by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="ac450-117">Измените значение GatewayIpAddress.</span><span class="sxs-lookup"><span data-stu-id="ac450-117">Modify the 'GatewayIpAddress' value.</span></span> <span data-ttu-id="ac450-118">При этом вы также можете изменить префиксы адресов.</span><span class="sxs-lookup"><span data-stu-id="ac450-118">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="ac450-119">Не забудьте указать существующее имя шлюза локальной сети для перезаписи текущих параметров.</span><span class="sxs-lookup"><span data-stu-id="ac450-119">Be sure to use the existing name of your local network gateway to overwrite the current settings.</span></span> <span data-ttu-id="ac450-120">Иначе вы создадите новый шлюз локальной сети, а не перезапишете существующий.</span><span class="sxs-lookup"><span data-stu-id="ac450-120">If you don't, you create a new local network gateway, instead of overwriting the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="ac450-121">Создайте подключение.</span><span class="sxs-lookup"><span data-stu-id="ac450-121">Create the connection.</span></span> <span data-ttu-id="ac450-122">В этом примере мы настраиваем тип подключения IPsec.</span><span class="sxs-lookup"><span data-stu-id="ac450-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="ac450-123">При повторном создании подключения используйте тип соединения, указанный для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ac450-123">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="ac450-124">Дополнительные типы подключений см. на странице с [командлетами PowerShell](https://msdn.microsoft.com/library/mt603611.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac450-124">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="ac450-125">Чтобы получить имя VirtualNetworkGateway, запустите командлет Get-AzureRmVirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="ac450-125">To obtain the VirtualNetworkGateway name, you can run the 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="ac450-126">Задайте переменные.</span><span class="sxs-lookup"><span data-stu-id="ac450-126">Set the variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="ac450-127">Создайте подключение.</span><span class="sxs-lookup"><span data-stu-id="ac450-127">Create the connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```