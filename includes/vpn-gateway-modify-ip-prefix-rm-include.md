### <span data-ttu-id="87059-101"><a name="noconnection"></a>Изменение префиксов IP-адресов для шлюза локальной сети при отсутствии подключения шлюза</span><span class="sxs-lookup"><span data-stu-id="87059-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="87059-102">Чтобы добавить дополнительные префиксы адресов:</span><span class="sxs-lookup"><span data-stu-id="87059-102">To add additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="87059-103">Чтобы удалить префиксы адресов, используйте фрагмент кода ниже.</span><span class="sxs-lookup"><span data-stu-id="87059-103">To remove address prefixes:</span></span><br>
<span data-ttu-id="87059-104">Не указывайте префиксы, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="87059-104">Leave out the prefixes that you no longer need.</span></span> <span data-ttu-id="87059-105">В этом примере нам больше не нужен префикс 20.0.0.0/24 (из предыдущего примера), поэтому мы обновим сетевой шлюз и исключим этот префикс.</span><span class="sxs-lookup"><span data-stu-id="87059-105">In this example, we no longer need prefix 20.0.0.0/24 (from the previous example), so we update the local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="87059-106"><a name="withconnection"></a>Изменение префиксов IP-адресов для шлюза локальной сети при наличии подключения шлюза</span><span class="sxs-lookup"><span data-stu-id="87059-106"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="87059-107">Если шлюз уже подключен и вам нужно добавить или удалить префиксы IP-адресов, указанные для локального сетевого шлюза, выполните приведенные ниже шаги именно в такой последовательности.</span><span class="sxs-lookup"><span data-stu-id="87059-107">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="87059-108">После этого VPN-подключение будет некоторое время недоступно.</span><span class="sxs-lookup"><span data-stu-id="87059-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="87059-109">При изменении префиксов IP-адресов не нужно удалять VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="87059-109">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="87059-110">Необходимо удалить только подключение.</span><span class="sxs-lookup"><span data-stu-id="87059-110">You only need to remove the connection.</span></span>


1. <span data-ttu-id="87059-111">Удалите подключение.</span><span class="sxs-lookup"><span data-stu-id="87059-111">Remove the connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="87059-112">Измените префиксы адресов для локального сетевого шлюза.</span><span class="sxs-lookup"><span data-stu-id="87059-112">Modify the address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="87059-113">Задайте переменную для локального сетевого шлюза.</span><span class="sxs-lookup"><span data-stu-id="87059-113">Set the variable for the LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="87059-114">Измените префиксы.</span><span class="sxs-lookup"><span data-stu-id="87059-114">Modify the prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="87059-115">Создайте подключение.</span><span class="sxs-lookup"><span data-stu-id="87059-115">Create the connection.</span></span> <span data-ttu-id="87059-116">В этом примере мы настраиваем тип подключения IPsec.</span><span class="sxs-lookup"><span data-stu-id="87059-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="87059-117">При повторном создании подключения используйте тип соединения, указанный для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="87059-117">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="87059-118">Дополнительные типы подключений см. на странице с [командлетами PowerShell](https://msdn.microsoft.com/library/mt603611.aspx).</span><span class="sxs-lookup"><span data-stu-id="87059-118">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="87059-119">Задайте переменную для шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="87059-119">Set the variable for the VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="87059-120">Создайте подключение.</span><span class="sxs-lookup"><span data-stu-id="87059-120">Create the connection.</span></span> <span data-ttu-id="87059-121">В этом примере используется переменная $local, присвоенная на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="87059-121">This example uses the variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```