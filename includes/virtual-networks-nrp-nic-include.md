## <a name="nic"></a><span data-ttu-id="ad84d-101">Сетевая карта</span><span class="sxs-lookup"><span data-stu-id="ad84d-101">NIC</span></span>
<span data-ttu-id="ad84d-102">Ресурс сетевого интерфейса адаптер (NIC) обеспечивает подключение tooan существующей подсети в виртуальной сети ресурс.</span><span class="sxs-lookup"><span data-stu-id="ad84d-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="ad84d-103">Несмотря на то, что вы сможете создать сетевой Адаптер в виде отдельного объекта, необходимо tooassociate его tooactually объекта tooanother обеспечить подключение.</span><span class="sxs-lookup"><span data-stu-id="ad84d-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="ad84d-104">Сетевой Адаптер может быть используется tooconnect tooa подсеть виртуальной Машины, общедоступный IP-адрес или подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ad84d-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="ad84d-105">Свойство</span><span class="sxs-lookup"><span data-stu-id="ad84d-105">Property</span></span> | <span data-ttu-id="ad84d-106">Описание</span><span class="sxs-lookup"><span data-stu-id="ad84d-106">Description</span></span> | <span data-ttu-id="ad84d-107">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="ad84d-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad84d-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="ad84d-108">**virtualMachine**</span></span> |<span data-ttu-id="ad84d-109">С которым связан hello виртуальной Машины сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="ad84d-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="ad84d-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="ad84d-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="ad84d-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="ad84d-111">**macAddress**</span></span> |<span data-ttu-id="ad84d-112">MAC-адрес для сетевого Адаптера hello</span><span class="sxs-lookup"><span data-stu-id="ad84d-112">MAC address for hello NIC</span></span> |<span data-ttu-id="ad84d-113">любое значение от 4 до 30</span><span class="sxs-lookup"><span data-stu-id="ad84d-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="ad84d-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="ad84d-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="ad84d-115">NSG связанные toohello сетевого Адаптера</span><span class="sxs-lookup"><span data-stu-id="ad84d-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="ad84d-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="ad84d-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="ad84d-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="ad84d-117">**dnsSettings**</span></span> |<span data-ttu-id="ad84d-118">Параметры DNS для сетевого Адаптера hello</span><span class="sxs-lookup"><span data-stu-id="ad84d-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="ad84d-119">См. раздел [Общедоступный IP-адрес](#Public-IP-address).</span><span class="sxs-lookup"><span data-stu-id="ad84d-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="ad84d-120">Сетевой адаптер или сетевой Адаптер, представляет сетевого интерфейса, который может быть связан tooa виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="ad84d-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="ad84d-121">У виртуальной машины может быть одна или несколько сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="ad84d-121">A VM can have one or more NICs.</span></span>

![Сетевая карта на одной виртуальной машине](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="ad84d-123">Конфигурации IP</span><span class="sxs-lookup"><span data-stu-id="ad84d-123">IP configurations</span></span>
<span data-ttu-id="ad84d-124">Сетевые адаптеры имеют дочерний объект с именем **IP-конфигураций** содержащий hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="ad84d-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="ad84d-125">Свойство</span><span class="sxs-lookup"><span data-stu-id="ad84d-125">Property</span></span> | <span data-ttu-id="ad84d-126">Описание</span><span class="sxs-lookup"><span data-stu-id="ad84d-126">Description</span></span> | <span data-ttu-id="ad84d-127">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="ad84d-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ad84d-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="ad84d-128">**subnet**</span></span> |<span data-ttu-id="ad84d-129">Подсети hello сетевого Адаптера — подключенного к.</span><span class="sxs-lookup"><span data-stu-id="ad84d-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="ad84d-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="ad84d-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="ad84d-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="ad84d-131">**privateIPAddress**</span></span> |<span data-ttu-id="ad84d-132">IP-адрес для hello сетевых Адаптеров в подсети hello</span><span class="sxs-lookup"><span data-stu-id="ad84d-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="ad84d-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="ad84d-133">10.0.0.8</span></span> |
| <span data-ttu-id="ad84d-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="ad84d-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="ad84d-135">Метод выделения IP-адресов</span><span class="sxs-lookup"><span data-stu-id="ad84d-135">IP allocation method</span></span> |<span data-ttu-id="ad84d-136">Динамический или статический</span><span class="sxs-lookup"><span data-stu-id="ad84d-136">Dynamic or Static</span></span> |
| <span data-ttu-id="ad84d-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="ad84d-137">**enableIPForwarding**</span></span> |<span data-ttu-id="ad84d-138">Hello сетевой Адаптер может использоваться для маршрутизации</span><span class="sxs-lookup"><span data-stu-id="ad84d-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="ad84d-139">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="ad84d-139">true or false</span></span> |
| <span data-ttu-id="ad84d-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="ad84d-140">**primary**</span></span> |<span data-ttu-id="ad84d-141">Является ли сетевой Адаптер hello hello первичный сетевой Адаптер для виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="ad84d-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="ad84d-142">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="ad84d-142">true or false</span></span> |
| <span data-ttu-id="ad84d-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="ad84d-143">**publicIPAddress**</span></span> |<span data-ttu-id="ad84d-144">PIP-адрес, связанный с hello сетевого Адаптера</span><span class="sxs-lookup"><span data-stu-id="ad84d-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="ad84d-145">См. раздел [Параметры DNS](#DNS-settings).</span><span class="sxs-lookup"><span data-stu-id="ad84d-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="ad84d-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="ad84d-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="ad84d-147">Резервное hello пулов адресов конечного сетевого Адаптера, которое связано с</span><span class="sxs-lookup"><span data-stu-id="ad84d-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="ad84d-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="ad84d-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="ad84d-149">Входящий hello правил NAT подсистемы балансировки нагрузки сетевого Адаптера, которое связано с</span><span class="sxs-lookup"><span data-stu-id="ad84d-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="ad84d-150">Пример общедоступного IP-адреса в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="ad84d-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="ad84d-151">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ad84d-151">Additional resources</span></span>
* <span data-ttu-id="ad84d-152">Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163579.aspx) для сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="ad84d-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

