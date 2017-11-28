<span data-ttu-id="51d0d-101">Прежде чем приступить к работе над следующими задачами, необходимо создать виртуальную сеть и подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="51d0d-101">You must create a VNet and a gateway subnet first, before working on the following tasks.</span></span> <span data-ttu-id="51d0d-102">Дополнительные сведения см. в статье [Настройка виртуальной сети с помощью классического портала](../articles/expressroute/expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="51d0d-102">See the article [Configure a Virtual Network using the classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="51d0d-103">Добавление шлюза</span><span class="sxs-lookup"><span data-stu-id="51d0d-103">Add a gateway</span></span>
<span data-ttu-id="51d0d-104">Используйте следующую команду, чтобы создать шлюз.</span><span class="sxs-lookup"><span data-stu-id="51d0d-104">Use the command below to create a gateway.</span></span> <span data-ttu-id="51d0d-105">Не забудьте подставить собственные значения.</span><span class="sxs-lookup"><span data-stu-id="51d0d-105">Be sure to substitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="51d0d-106">Проверка создания шлюза</span><span class="sxs-lookup"><span data-stu-id="51d0d-106">Verify the gateway was created</span></span>
<span data-ttu-id="51d0d-107">Используйте следующую команду, чтобы проверить, был ли создан шлюз.</span><span class="sxs-lookup"><span data-stu-id="51d0d-107">Use the command below to verify that the gateway has been created.</span></span> <span data-ttu-id="51d0d-108">Эта команда также получает идентификатор шлюза, который нужен для других операций.</span><span class="sxs-lookup"><span data-stu-id="51d0d-108">This command also retrieves the gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="51d0d-109">Изменение размера шлюза</span><span class="sxs-lookup"><span data-stu-id="51d0d-109">Resize a gateway</span></span>
<span data-ttu-id="51d0d-110">Существует несколько [номеров SKU шлюзов](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="51d0d-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="51d0d-111">Чтобы изменить SKU шлюза в любое время, можно использовать следующую команду.</span><span class="sxs-lookup"><span data-stu-id="51d0d-111">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51d0d-112">Эта команда не работает для шлюза UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="51d0d-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="51d0d-113">Чтобы заменить шлюз на UltraPerformance, сначала удалите существующий шлюз ExpressRoute, а затем создайте шлюз UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="51d0d-113">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="51d0d-114">Чтобы заменить шлюз UltraPerformance обычным шлюзом, сначала удалите шлюз UltraPerformance, а затем создайте новый шлюз.</span><span class="sxs-lookup"><span data-stu-id="51d0d-114">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="51d0d-115">Удаление шлюза</span><span class="sxs-lookup"><span data-stu-id="51d0d-115">Remove a gateway</span></span>
<span data-ttu-id="51d0d-116">Используйте следующую команду, чтобы удалить шлюз.</span><span class="sxs-lookup"><span data-stu-id="51d0d-116">Use the command below to remove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>