## <a name="virtual-network"></a><span data-ttu-id="84d3e-101">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="84d3e-101">Virtual Network</span></span>
<span data-ttu-id="84d3e-102">Ресурсы виртуальных сетей (VNET) и подсетей позволяют определить периметр безопасности для рабочих нагрузок, выполняемых в Azure.</span><span class="sxs-lookup"><span data-stu-id="84d3e-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="84d3e-103">Виртуальная сеть характеризуется набором адресных пространств, которые также называются блоками CIDR.</span><span class="sxs-lookup"><span data-stu-id="84d3e-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="84d3e-104">Сетевым администраторам знакомы нотации CIDR.</span><span class="sxs-lookup"><span data-stu-id="84d3e-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="84d3e-105">Если вы не знакомы с методом CIDR, [узнайте больше о нем](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="84d3e-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Виртуальная сеть с несколькими подсетями](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="84d3e-107">Виртуальные сети содержать hello следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="84d3e-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="84d3e-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="84d3e-108">Property</span></span> | <span data-ttu-id="84d3e-109">Описание</span><span class="sxs-lookup"><span data-stu-id="84d3e-109">Description</span></span> | <span data-ttu-id="84d3e-110">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="84d3e-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84d3e-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="84d3e-111">**addressSpace**</span></span> |<span data-ttu-id="84d3e-112">Коллекция префиксов адресов, составляющих hello виртуальной сети в нотации CIDR</span><span class="sxs-lookup"><span data-stu-id="84d3e-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="84d3e-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="84d3e-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="84d3e-114">**Подсети**</span><span class="sxs-lookup"><span data-stu-id="84d3e-114">**subnets**</span></span> |<span data-ttu-id="84d3e-115">Коллекция подсетей, составляющих hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="84d3e-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="84d3e-116">См. раздел [Подсети](#Subnets) ниже.</span><span class="sxs-lookup"><span data-stu-id="84d3e-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="84d3e-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="84d3e-117">**ipAddress**</span></span> |<span data-ttu-id="84d3e-118">Tooobject назначить IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="84d3e-118">IP address assigned tooobject.</span></span> <span data-ttu-id="84d3e-119">Это свойство доступно только для чтения.</span><span class="sxs-lookup"><span data-stu-id="84d3e-119">This is a read-only property.</span></span> |<span data-ttu-id="84d3e-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="84d3e-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="84d3e-121">Подсети</span><span class="sxs-lookup"><span data-stu-id="84d3e-121">Subnets</span></span>
<span data-ttu-id="84d3e-122">Подсеть является дочерним ресурсом виртуальной сети, который помогает определить сегменты адресных пространств в пределах блока CIDR на основе префиксов IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="84d3e-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="84d3e-123">Сетевые адаптеры могут добавляться toosubnets и подключенных tooVMs, предоставляя возможность подключения к для различных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="84d3e-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="84d3e-124">Подсети содержат hello следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="84d3e-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="84d3e-125">Свойство</span><span class="sxs-lookup"><span data-stu-id="84d3e-125">Property</span></span> | <span data-ttu-id="84d3e-126">Описание</span><span class="sxs-lookup"><span data-stu-id="84d3e-126">Description</span></span> | <span data-ttu-id="84d3e-127">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="84d3e-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84d3e-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="84d3e-128">**addressPrefix**</span></span> |<span data-ttu-id="84d3e-129">Один префикс адреса, которые образуют hello подсети в нотации CIDR</span><span class="sxs-lookup"><span data-stu-id="84d3e-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="84d3e-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="84d3e-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="84d3e-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="84d3e-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="84d3e-132">NSG применяется toohello подсети</span><span class="sxs-lookup"><span data-stu-id="84d3e-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="84d3e-133">См. раздел [Группы безопасности сети](#Network-Security-Group).</span><span class="sxs-lookup"><span data-stu-id="84d3e-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="84d3e-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="84d3e-134">**routeTable**</span></span> |<span data-ttu-id="84d3e-135">Таблица маршрутов применяется toohello подсети</span><span class="sxs-lookup"><span data-stu-id="84d3e-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="84d3e-136">См. раздел [Определяемые пользователем маршруты](#Route-table).</span><span class="sxs-lookup"><span data-stu-id="84d3e-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="84d3e-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="84d3e-137">**ipConfigurations**</span></span> |<span data-ttu-id="84d3e-138">Коллекция объектов конфигурации IP, используемые подсети toohello подключенных сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="84d3e-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="84d3e-139">См. раздел [Определяемые пользователем маршруты](#Route-table).</span><span class="sxs-lookup"><span data-stu-id="84d3e-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="84d3e-140">Пример виртуальной сети в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="84d3e-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="84d3e-141">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="84d3e-141">Additional resources</span></span>
* <span data-ttu-id="84d3e-142">Более подробная информация о [виртуальной сети](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84d3e-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="84d3e-143">Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163650.aspx) для виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="84d3e-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="84d3e-144">Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163618.aspx) для подсетей.</span><span class="sxs-lookup"><span data-stu-id="84d3e-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

