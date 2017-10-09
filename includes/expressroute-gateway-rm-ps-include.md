Hello действия для этой задачи используйте виртуальную сеть на основе hello значений в следующий список ссылок на конфигурации hello. В этом списке также приведены дополнительные параметры и имена. Мы не используем этот список непосредственно в любом из этапов hello, несмотря на то, что мы добавляем переменных, основанных на значениях hello в этот список. Можно скопировать toouse список hello как ссылка, заменив значения hello собственные.

**Справочный список для конфигурации**

* Имя виртуальной сети: TestVNet.
* Адресное пространство виртуальной сети: 192.168.0.0/16.
* Группа ресурсов — TestRG.
* Имя подсети Subnet1: FrontEnd. 
* Адресное пространство Subnet1: 192.168.1.0/24.
* Имя подсети шлюза: GatewaySubnet; подсеть шлюза всегда необходимо называть *GatewaySubnet*.
* Адресное пространство шлюза подсети: 192.168.200.0/26.
* Расположение — East US.
* Имя шлюза: GW.
* IP-имя шлюза: GWIP.
* Имя конфигурации IP-адресов шлюза: gwipconf.
* Type = "ExpressRoute". Для настройки ExpressRoute требуется этот тип.
* Общедоступное IP-имя шлюза: gwpip.

## <a name="add-a-gateway"></a>Добавление шлюза
1. Подключите tooyour подписки Azure.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Объявите переменные для этого упражнения. Быть убедиться, что tooedit hello tooreflect образец hello параметры, которые должны toouse.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Хранится в переменной hello объекта виртуальной сети.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Добавьте tooyour подсети шлюза виртуальной сети. подсеть шлюза Hello должен называться «GatewaySubnet». Потребуется создать шлюз с префиксом /27 или больше (26, 25 и т. д.).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Задание конфигурации hello.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Подсеть шлюза hello хранится в переменной.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Запросите общедоступный IP-адрес. Перед созданием шлюза hello запрашивается Hello IP-адрес. Нельзя указать hello IP-адреса, которые должны toouse; он выделяется динамически. Этот IP-адрес будет использоваться в следующем разделе конфигурации hello. Hello AllocationMethod должны быть динамическими.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Создайте конфигурацию hello для шлюза. Конфигурация шлюза Hello определяет подсеть hello и hello открытый IP адрес toouse. На этом шаге вы указываете hello конфигурации, который будет использоваться при создании шлюза hello. Этот шаг не создает hello объекта шлюза. Использование образца hello ниже toocreate конфигурацию шлюза.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Создайте шлюз hello. На этом шаге hello **- тип шлюза** особенно важна. Необходимо использовать значение hello **ExpressRoute**. После выполнения этих командлетов, hello шлюза может занять 45 минут или более toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Убедитесь, что был создан шлюз hello
Используйте следующие команды, созданных tooverify, hello шлюза hello.

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Изменение размера шлюза
Существует несколько [номеров SKU шлюзов](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Можно использовать hello, следующая команда toochange hello номер SKU шлюза в любое время.

> [!IMPORTANT]
> Эта команда не работает для шлюза UltraPerformance. toochange tooan UltraPerformance шлюз шлюз, сначала удалите существующий шлюз ExpressRoute hello и создайте новый шлюз UltraPerformance. удалите шлюз с шлюзом UltraPerformance toodowngrade hello UltraPerformance шлюза, а затем создайте новый шлюз.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Удаление шлюза
Используйте следующие команды tooremove шлюз hello:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```