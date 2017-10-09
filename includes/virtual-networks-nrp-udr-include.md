## <a name="route-tables"></a><span data-ttu-id="593c5-101">Таблицы маршрутов</span><span class="sxs-lookup"><span data-stu-id="593c5-101">Route tables</span></span>
<span data-ttu-id="593c5-102">Ресурсы таблицы маршрутизации содержит маршруты toodefine потоки трафика в рамках инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="593c5-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="593c5-103">Можно использовать определяемых пользователем маршрутов (UDR) toosend весь трафик с данной подсети tooa виртуального устройства, например брандмауэром или вторжений обнаружения системы (IDS).</span><span class="sxs-lookup"><span data-stu-id="593c5-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="593c5-104">Можно связать toosubnets таблицы маршрутов.</span><span class="sxs-lookup"><span data-stu-id="593c5-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="593c5-105">Таблицы маршрутов содержат hello следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="593c5-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="593c5-106">Свойство</span><span class="sxs-lookup"><span data-stu-id="593c5-106">Property</span></span> | <span data-ttu-id="593c5-107">Описание</span><span class="sxs-lookup"><span data-stu-id="593c5-107">Description</span></span> | <span data-ttu-id="593c5-108">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="593c5-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="593c5-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="593c5-109">**routes**</span></span> |<span data-ttu-id="593c5-110">Коллекция определяемых пользователем маршрутов в таблице маршрутов hello</span><span class="sxs-lookup"><span data-stu-id="593c5-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="593c5-111">См. раздел [Определяемые пользователем маршруты](#User-defined-routes).</span><span class="sxs-lookup"><span data-stu-id="593c5-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="593c5-112">**Подсети**</span><span class="sxs-lookup"><span data-stu-id="593c5-112">**subnets**</span></span> |<span data-ttu-id="593c5-113">Коллекция таблицы маршрутов для подсети hello применяется слишком</span><span class="sxs-lookup"><span data-stu-id="593c5-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="593c5-114">См. раздел [Подсети](#Subnets).</span><span class="sxs-lookup"><span data-stu-id="593c5-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="593c5-115">Определяемые пользователем маршруты</span><span class="sxs-lookup"><span data-stu-id="593c5-115">User defined routes</span></span>
<span data-ttu-id="593c5-116">Toospecify UDRs, где следует отправлять трафик, можно создать на основе его адреса назначения.</span><span class="sxs-lookup"><span data-stu-id="593c5-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="593c5-117">Маршрут можно считать определение шлюза по умолчанию hello, на основе адреса назначения hello сетевого пакета.</span><span class="sxs-lookup"><span data-stu-id="593c5-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="593c5-118">UDRs содержат hello следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="593c5-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="593c5-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="593c5-119">Property</span></span> | <span data-ttu-id="593c5-120">Описание</span><span class="sxs-lookup"><span data-stu-id="593c5-120">Description</span></span> | <span data-ttu-id="593c5-121">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="593c5-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="593c5-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="593c5-122">**addressPrefix**</span></span> |<span data-ttu-id="593c5-123">Префикс адреса или полного IP-адрес для назначения hello</span><span class="sxs-lookup"><span data-stu-id="593c5-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="593c5-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="593c5-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="593c5-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="593c5-125">**nextHopType**</span></span> |<span data-ttu-id="593c5-126">Тип трафика hello устройства будут отправляться слишком</span><span class="sxs-lookup"><span data-stu-id="593c5-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="593c5-127">VirtualAppliance, VPN-шлюз, Интернет</span><span class="sxs-lookup"><span data-stu-id="593c5-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="593c5-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="593c5-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="593c5-129">IP-адрес следующего прыжка hello</span><span class="sxs-lookup"><span data-stu-id="593c5-129">IP address for hello next hop</span></span> |<span data-ttu-id="593c5-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="593c5-130">192.168.1.4</span></span> |

<span data-ttu-id="593c5-131">Пример таблицы маршрутов в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="593c5-131">Sample route table in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="593c5-132">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="593c5-132">Additional resources</span></span>
* <span data-ttu-id="593c5-133">Более подробная информация об [определяемых пользователем маршрутах](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="593c5-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="593c5-134">Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt502549.aspx) для таблицы маршрутов.</span><span class="sxs-lookup"><span data-stu-id="593c5-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="593c5-135">Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt502539.aspx) для пользователя определено маршрутов (UDRs).</span><span class="sxs-lookup"><span data-stu-id="593c5-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

