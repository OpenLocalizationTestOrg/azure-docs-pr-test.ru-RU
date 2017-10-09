### <a name="noconnection"></a>toomodify локальной сети шлюза префиксов IP-адресов — подключение к шлюзу

префиксы tooadd дополнительный адрес:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

tooremove префиксы адресов:<br>
Оставьте hello префиксов, которые больше не нужны. В этом примере мы больше не требуется префикс 20.0.0.0/24 (из предыдущего примера hello), поэтому мы обновление шлюза локальной сети hello, за исключением этого префикса.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify локальной сети шлюза префиксов IP-адресов — существующие подключения шлюза

Если после подключения шлюза и хотите tooadd или префиксов IP-адресов hello, содержащихся в шлюз локальной сети, необходимо hello toodo следующие шаги в порядке. После этого VPN-подключение будет некоторое время недоступно. При изменении префиксов IP-адресов, не требуется toodelete hello VPN-шлюз. Необходимо только подключение tooremove hello.


1. Удалите подключение hello.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Измените префиксы адресов hello шлюза локальной сети.
   
  Задайте переменную hello для hello LocalNetworkGateway.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Измените префиксы hello.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Создание подключения hello. В этом примере мы настраиваем тип подключения IPsec. При повторном создании подключения, используйте hello тип соединения, указанный для вашей конфигурации. Для подключения дополнительных типов, в разделе hello [командлета PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) страницы.
   
  Задайте переменную hello для hello задана как.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Создание подключения hello. В этом примере используется переменная hello $local, установленное на шаге 2.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```