### <span data-ttu-id="a5fed-101"><a name="noconnection"></a>toomodify локальной сети шлюза префиксов IP-адресов — подключение к шлюзу</span><span class="sxs-lookup"><span data-stu-id="a5fed-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="a5fed-102">префиксы tooadd дополнительный адрес:</span><span class="sxs-lookup"><span data-stu-id="a5fed-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="a5fed-103">tooremove префиксы адресов:</span><span class="sxs-lookup"><span data-stu-id="a5fed-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="a5fed-104">Оставьте hello префиксов, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="a5fed-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="a5fed-105">В этом примере мы больше не требуется префикс 20.0.0.0/24 (из предыдущего примера hello), поэтому мы обновление шлюза локальной сети hello, за исключением этого префикса.</span><span class="sxs-lookup"><span data-stu-id="a5fed-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="a5fed-106"><a name="withconnection"></a>toomodify локальной сети шлюза префиксов IP-адресов — существующие подключения шлюза</span><span class="sxs-lookup"><span data-stu-id="a5fed-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="a5fed-107">Если после подключения шлюза и хотите tooadd или префиксов IP-адресов hello, содержащихся в шлюз локальной сети, необходимо hello toodo следующие шаги в порядке.</span><span class="sxs-lookup"><span data-stu-id="a5fed-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="a5fed-108">После этого VPN-подключение будет некоторое время недоступно.</span><span class="sxs-lookup"><span data-stu-id="a5fed-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="a5fed-109">При изменении префиксов IP-адресов, не требуется toodelete hello VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="a5fed-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="a5fed-110">Необходимо только подключение tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="a5fed-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="a5fed-111">Удалите подключение hello.</span><span class="sxs-lookup"><span data-stu-id="a5fed-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="a5fed-112">Измените префиксы адресов hello шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="a5fed-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="a5fed-113">Задайте переменную hello для hello LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="a5fed-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="a5fed-114">Измените префиксы hello.</span><span class="sxs-lookup"><span data-stu-id="a5fed-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="a5fed-115">Создание подключения hello.</span><span class="sxs-lookup"><span data-stu-id="a5fed-115">Create hello connection.</span></span> <span data-ttu-id="a5fed-116">В этом примере мы настраиваем тип подключения IPsec.</span><span class="sxs-lookup"><span data-stu-id="a5fed-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="a5fed-117">При повторном создании подключения, используйте hello тип соединения, указанный для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a5fed-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="a5fed-118">Для подключения дополнительных типов, в разделе hello [командлета PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="a5fed-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="a5fed-119">Задайте переменную hello для hello задана как.</span><span class="sxs-lookup"><span data-stu-id="a5fed-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="a5fed-120">Создание подключения hello.</span><span class="sxs-lookup"><span data-stu-id="a5fed-120">Create hello connection.</span></span> <span data-ttu-id="a5fed-121">В этом примере используется переменная hello $local, установленное на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="a5fed-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```