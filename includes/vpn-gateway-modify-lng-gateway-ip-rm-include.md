### <a name="gwipnoconnection"></a>шлюз локальной сети toomodify hello «GatewayIpAddress» - нет подключение к шлюзу

Если hello VPN-устройства, которые должны tooconnect toohas изменено его общедоступный IP-адрес, необходимо tooreflect шлюза локальной сети hello toomodify, изменяется. Используйте пример hello toomodify шлюза локальной сети, у которого нет подключения шлюза.

При изменении этого значения, также можно изменить префиксы адресов hello в hello то же время. Быть убедиться, что существующее имя toouse hello в порядке toooverwrite hello текущие параметры шлюза локальной сети. Если используется другое имя, можно создать новый шлюз локальной сети, вместо переопределения Здравствуйте существующий.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>шлюз локальной сети toomodify hello «GatewayIpAddress» - существующее подключение шлюза

Если hello VPN-устройства, которые должны tooconnect toohas изменено его общедоступный IP-адрес, необходимо tooreflect шлюза локальной сети hello toomodify, изменяется. Если подключение шлюза уже существует, необходимо сначала tooremove hello соединения. После удаления hello подключения, можно изменить IP-адрес шлюза hello и заново создайте новое соединение. Можно также изменить префиксы адресов hello в hello то же время. После этого VPN-подключение будет некоторое время недоступно. При изменении IP-адрес шлюза hello, не требуется toodelete hello VPN-шлюз. Необходимо только подключение tooremove hello.
 

1. Удалите подключение hello. Имя hello подключения можно найти с помощью командлета hello «Get-AzureRmVirtualNetworkGatewayConnection».

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Измените значение «GatewayIpAddress» hello. Можно также изменить префиксы адресов hello в hello то же время. Быть убедиться, что toouse hello существующее имя локальной сети шлюза toooverwrite hello текущие настройки. Если этого не сделать, можно создать новый шлюз локальной сети, вместо переопределения Здравствуйте существующий.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Создание подключения hello. В этом примере мы настраиваем тип подключения IPsec. При повторном создании подключения, используйте hello тип соединения, указанный для вашей конфигурации. Для подключения дополнительных типов, в разделе hello [командлета PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) страницы.  tooobtain hello задана как имя, можно запустить командлет «Get-AzureRmVirtualNetworkGateway» hello.
   
    Установка переменных hello.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Создание подключения hello.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```