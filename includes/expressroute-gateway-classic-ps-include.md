<span data-ttu-id="6a42d-101">Необходимо создать виртуальную сеть и подсеть шлюза во-первых, прежде чем приступать к hello следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="6a42d-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="6a42d-102">См. в статье hello [Настройка виртуальной сети с помощью классического портала hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="6a42d-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="6a42d-103">Добавление шлюза</span><span class="sxs-lookup"><span data-stu-id="6a42d-103">Add a gateway</span></span>
<span data-ttu-id="6a42d-104">Команда hello ниже toocreate шлюз.</span><span class="sxs-lookup"><span data-stu-id="6a42d-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="6a42d-105">Быть toosubstitute убедиться, что все значения для себя.</span><span class="sxs-lookup"><span data-stu-id="6a42d-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="6a42d-106">Убедитесь, что был создан шлюз hello</span><span class="sxs-lookup"><span data-stu-id="6a42d-106">Verify hello gateway was created</span></span>
<span data-ttu-id="6a42d-107">Используйте команду hello ниже tooverify, hello шлюза был создан.</span><span class="sxs-lookup"><span data-stu-id="6a42d-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="6a42d-108">Эта команда также получает идентификатор hello шлюза, который требуется для других операций.</span><span class="sxs-lookup"><span data-stu-id="6a42d-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="6a42d-109">Изменение размера шлюза</span><span class="sxs-lookup"><span data-stu-id="6a42d-109">Resize a gateway</span></span>
<span data-ttu-id="6a42d-110">Существует несколько [номеров SKU шлюзов](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="6a42d-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="6a42d-111">Можно использовать hello, следующая команда toochange hello номер SKU шлюза в любое время.</span><span class="sxs-lookup"><span data-stu-id="6a42d-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a42d-112">Эта команда не работает для шлюза UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="6a42d-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="6a42d-113">toochange tooan UltraPerformance шлюз шлюз, сначала удалите существующий шлюз ExpressRoute hello и создайте новый шлюз UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="6a42d-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="6a42d-114">удалите шлюз с шлюзом UltraPerformance toodowngrade hello UltraPerformance шлюза, а затем создайте новый шлюз.</span><span class="sxs-lookup"><span data-stu-id="6a42d-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="6a42d-115">Удаление шлюза</span><span class="sxs-lookup"><span data-stu-id="6a42d-115">Remove a gateway</span></span>
<span data-ttu-id="6a42d-116">Команда hello ниже tooremove шлюза</span><span class="sxs-lookup"><span data-stu-id="6a42d-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>