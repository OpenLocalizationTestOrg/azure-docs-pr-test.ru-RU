Необходимо создать виртуальную сеть и подсеть шлюза во-первых, прежде чем приступать к hello следующие задачи. См. в статье hello [Настройка виртуальной сети с помощью классического портала hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) для получения дополнительной информации.   

## <a name="add-a-gateway"></a>Добавление шлюза
Команда hello ниже toocreate шлюз. Быть toosubstitute убедиться, что все значения для себя.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Убедитесь, что был создан шлюз hello
Используйте команду hello ниже tooverify, hello шлюза был создан. Эта команда также получает идентификатор hello шлюза, который требуется для других операций.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Изменение размера шлюза
Существует несколько [номеров SKU шлюзов](../articles/expressroute/expressroute-about-virtual-network-gateways.md). Можно использовать hello, следующая команда toochange hello номер SKU шлюза в любое время.

> [!IMPORTANT]
> Эта команда не работает для шлюза UltraPerformance. toochange tooan UltraPerformance шлюз шлюз, сначала удалите существующий шлюз ExpressRoute hello и создайте новый шлюз UltraPerformance. удалите шлюз с шлюзом UltraPerformance toodowngrade hello UltraPerformance шлюза, а затем создайте новый шлюз. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Удаление шлюза
Команда hello ниже tooremove шлюза

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>