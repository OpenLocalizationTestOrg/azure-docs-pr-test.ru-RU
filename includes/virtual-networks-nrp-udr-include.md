## <a name="route-tables"></a><span data-ttu-id="5b400-101">Таблицы маршрутов</span><span class="sxs-lookup"><span data-stu-id="5b400-101">Route tables</span></span>
<span data-ttu-id="5b400-102">Ресурсы таблиц маршрутов содержат маршруты, используемые для направления трафика в рамках инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="5b400-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="5b400-103">Вы можете использовать определяемые пользователем маршруты (UDR) для отправки всего трафика из определенной подсети в виртуальный модуль, например брандмауэр или систему обнаружения атак (IDS).</span><span class="sxs-lookup"><span data-stu-id="5b400-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="5b400-104">Таблицу маршрутизации можно связать с подсетью.</span><span class="sxs-lookup"><span data-stu-id="5b400-104">You can associate a route table to subnets.</span></span> 

<span data-ttu-id="5b400-105">Таблицы маршрутизации обладают следующими свойствами.</span><span class="sxs-lookup"><span data-stu-id="5b400-105">Route tables contain the following properties.</span></span>

| <span data-ttu-id="5b400-106">Свойство</span><span class="sxs-lookup"><span data-stu-id="5b400-106">Property</span></span> | <span data-ttu-id="5b400-107">Описание</span><span class="sxs-lookup"><span data-stu-id="5b400-107">Description</span></span> | <span data-ttu-id="5b400-108">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="5b400-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b400-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="5b400-109">**routes**</span></span> |<span data-ttu-id="5b400-110">Коллекция определяемых пользователем маршрутов в таблице маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="5b400-110">Collection of user defined routes in the route table</span></span> |<span data-ttu-id="5b400-111">См. раздел [Определяемые пользователем маршруты](#User-defined-routes).</span><span class="sxs-lookup"><span data-stu-id="5b400-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="5b400-112">**Подсети**</span><span class="sxs-lookup"><span data-stu-id="5b400-112">**subnets**</span></span> |<span data-ttu-id="5b400-113">Коллекция подсетей, к которым применяется таблица маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="5b400-113">Collection of subnets the route table is applied to</span></span> |<span data-ttu-id="5b400-114">См. раздел [Подсети](#Subnets).</span><span class="sxs-lookup"><span data-stu-id="5b400-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="5b400-115">Определяемые пользователем маршруты</span><span class="sxs-lookup"><span data-stu-id="5b400-115">User defined routes</span></span>
<span data-ttu-id="5b400-116">Вы можете создать определяемые пользователем маршруты, чтобы указать, куда следует отправлять трафик, по его адресу назначения.</span><span class="sxs-lookup"><span data-stu-id="5b400-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="5b400-117">Маршрут можно считать определением шлюза по умолчанию, построенным на основе адреса назначения сетевого пакета.</span><span class="sxs-lookup"><span data-stu-id="5b400-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span></span>

<span data-ttu-id="5b400-118">Определяемые пользователем маршруты содержат следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="5b400-118">UDRs contain the following properties.</span></span> 

| <span data-ttu-id="5b400-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="5b400-119">Property</span></span> | <span data-ttu-id="5b400-120">Описание</span><span class="sxs-lookup"><span data-stu-id="5b400-120">Description</span></span> | <span data-ttu-id="5b400-121">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="5b400-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b400-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="5b400-122">**addressPrefix**</span></span> |<span data-ttu-id="5b400-123">Префикс адреса или полный IP-адрес назначения.</span><span class="sxs-lookup"><span data-stu-id="5b400-123">Address prefix, or full IP address for the destination</span></span> |<span data-ttu-id="5b400-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="5b400-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="5b400-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="5b400-125">**nextHopType**</span></span> |<span data-ttu-id="5b400-126">Тип устройства, на которое будет отправляться трафик.</span><span class="sxs-lookup"><span data-stu-id="5b400-126">Type of device the traffic will be sent to</span></span> |<span data-ttu-id="5b400-127">VirtualAppliance, VPN-шлюз, Интернет</span><span class="sxs-lookup"><span data-stu-id="5b400-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="5b400-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="5b400-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="5b400-129">IP-адрес следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="5b400-129">IP address for the next hop</span></span> |<span data-ttu-id="5b400-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="5b400-130">192.168.1.4</span></span> |

<span data-ttu-id="5b400-131">Пример таблицы маршрутов в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="5b400-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="5b400-132">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5b400-132">Additional resources</span></span>
* <span data-ttu-id="5b400-133">Более подробная информация об [определяемых пользователем маршрутах](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5b400-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="5b400-134">Прочитайте [справочную документацию по REST API](https://msdn.microsoft.com/library/azure/mt502549.aspx) для таблиц маршрутов.</span><span class="sxs-lookup"><span data-stu-id="5b400-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="5b400-135">Прочитайте [справочную документацию по REST API](https://msdn.microsoft.com/library/azure/mt502539.aspx) для определяемых пользователем маршрутов (UDR).</span><span class="sxs-lookup"><span data-stu-id="5b400-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

