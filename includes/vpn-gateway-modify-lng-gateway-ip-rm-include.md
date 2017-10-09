### <span data-ttu-id="9fc28-101"><a name="gwipnoconnection"></a>шлюз локальной сети toomodify hello «GatewayIpAddress» - нет подключение к шлюзу</span><span class="sxs-lookup"><span data-stu-id="9fc28-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="9fc28-102">Если hello VPN-устройства, которые должны tooconnect toohas изменено его общедоступный IP-адрес, необходимо tooreflect шлюза локальной сети hello toomodify, изменяется.</span><span class="sxs-lookup"><span data-stu-id="9fc28-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="9fc28-103">Используйте пример hello toomodify шлюза локальной сети, у которого нет подключения шлюза.</span><span class="sxs-lookup"><span data-stu-id="9fc28-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="9fc28-104">При изменении этого значения, также можно изменить префиксы адресов hello в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="9fc28-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="9fc28-105">Быть убедиться, что существующее имя toouse hello в порядке toooverwrite hello текущие параметры шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="9fc28-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="9fc28-106">Если используется другое имя, можно создать новый шлюз локальной сети, вместо переопределения Здравствуйте существующий.</span><span class="sxs-lookup"><span data-stu-id="9fc28-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="9fc28-107"><a name="gwipwithconnection"></a>шлюз локальной сети toomodify hello «GatewayIpAddress» - существующее подключение шлюза</span><span class="sxs-lookup"><span data-stu-id="9fc28-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="9fc28-108">Если hello VPN-устройства, которые должны tooconnect toohas изменено его общедоступный IP-адрес, необходимо tooreflect шлюза локальной сети hello toomodify, изменяется.</span><span class="sxs-lookup"><span data-stu-id="9fc28-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="9fc28-109">Если подключение шлюза уже существует, необходимо сначала tooremove hello соединения.</span><span class="sxs-lookup"><span data-stu-id="9fc28-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="9fc28-110">После удаления hello подключения, можно изменить IP-адрес шлюза hello и заново создайте новое соединение.</span><span class="sxs-lookup"><span data-stu-id="9fc28-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="9fc28-111">Можно также изменить префиксы адресов hello в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="9fc28-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="9fc28-112">После этого VPN-подключение будет некоторое время недоступно.</span><span class="sxs-lookup"><span data-stu-id="9fc28-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="9fc28-113">При изменении IP-адрес шлюза hello, не требуется toodelete hello VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="9fc28-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="9fc28-114">Необходимо только подключение tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="9fc28-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="9fc28-115">Удалите подключение hello.</span><span class="sxs-lookup"><span data-stu-id="9fc28-115">Remove hello connection.</span></span> <span data-ttu-id="9fc28-116">Имя hello подключения можно найти с помощью командлета hello «Get-AzureRmVirtualNetworkGatewayConnection».</span><span class="sxs-lookup"><span data-stu-id="9fc28-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="9fc28-117">Измените значение «GatewayIpAddress» hello.</span><span class="sxs-lookup"><span data-stu-id="9fc28-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="9fc28-118">Можно также изменить префиксы адресов hello в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="9fc28-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="9fc28-119">Быть убедиться, что toouse hello существующее имя локальной сети шлюза toooverwrite hello текущие настройки.</span><span class="sxs-lookup"><span data-stu-id="9fc28-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="9fc28-120">Если этого не сделать, можно создать новый шлюз локальной сети, вместо переопределения Здравствуйте существующий.</span><span class="sxs-lookup"><span data-stu-id="9fc28-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="9fc28-121">Создание подключения hello.</span><span class="sxs-lookup"><span data-stu-id="9fc28-121">Create hello connection.</span></span> <span data-ttu-id="9fc28-122">В этом примере мы настраиваем тип подключения IPsec.</span><span class="sxs-lookup"><span data-stu-id="9fc28-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="9fc28-123">При повторном создании подключения, используйте hello тип соединения, указанный для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9fc28-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="9fc28-124">Для подключения дополнительных типов, в разделе hello [командлета PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="9fc28-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="9fc28-125">tooobtain hello задана как имя, можно запустить командлет «Get-AzureRmVirtualNetworkGateway» hello.</span><span class="sxs-lookup"><span data-stu-id="9fc28-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="9fc28-126">Установка переменных hello.</span><span class="sxs-lookup"><span data-stu-id="9fc28-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="9fc28-127">Создание подключения hello.</span><span class="sxs-lookup"><span data-stu-id="9fc28-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```