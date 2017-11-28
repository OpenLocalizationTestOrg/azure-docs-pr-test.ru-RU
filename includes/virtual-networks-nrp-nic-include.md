## <a name="nic"></a><span data-ttu-id="793e1-101">Сетевая карта</span><span class="sxs-lookup"><span data-stu-id="793e1-101">NIC</span></span>
<span data-ttu-id="793e1-102">Ресурс сетевой карты обеспечивает сетевое взаимодействие с существующей подсетью в ресурсе виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="793e1-102">A network interface card (NIC) resource provides network connectivity to an existing subnet in a VNet resource.</span></span> <span data-ttu-id="793e1-103">Хотя вы можете создать сетевую карту как отдельный объект, ее необходимо связать с другим объектом, чтобы обеспечить возможность связи.</span><span class="sxs-lookup"><span data-stu-id="793e1-103">Although you can create a NIC as a stand alone object, you need to associate it to another object to actually provide connectivity.</span></span> <span data-ttu-id="793e1-104">Сетевую карту можно использовать для подключения виртуальной машины к подсети, общему IP-адресу или балансировщику нагрузки.</span><span class="sxs-lookup"><span data-stu-id="793e1-104">A NIC can be used to connect a VM to a subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="793e1-105">Свойство</span><span class="sxs-lookup"><span data-stu-id="793e1-105">Property</span></span> | <span data-ttu-id="793e1-106">Описание</span><span class="sxs-lookup"><span data-stu-id="793e1-106">Description</span></span> | <span data-ttu-id="793e1-107">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="793e1-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="793e1-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="793e1-108">**virtualMachine**</span></span> |<span data-ttu-id="793e1-109">Виртуальная машина, с которой сопоставлена сетевая карта.</span><span class="sxs-lookup"><span data-stu-id="793e1-109">VM the NIC is associated with.</span></span> |<span data-ttu-id="793e1-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="793e1-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="793e1-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="793e1-111">**macAddress**</span></span> |<span data-ttu-id="793e1-112">MAC-адрес для сетевой карты</span><span class="sxs-lookup"><span data-stu-id="793e1-112">MAC address for the NIC</span></span> |<span data-ttu-id="793e1-113">любое значение от 4 до 30</span><span class="sxs-lookup"><span data-stu-id="793e1-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="793e1-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="793e1-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="793e1-115">Группа NSG, связанная с сетевой картой</span><span class="sxs-lookup"><span data-stu-id="793e1-115">NSG associated to the NIC</span></span> |<span data-ttu-id="793e1-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="793e1-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="793e1-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="793e1-117">**dnsSettings**</span></span> |<span data-ttu-id="793e1-118">Параметры DNS для сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="793e1-118">DNS settings for the NIC</span></span> |<span data-ttu-id="793e1-119">См. раздел [Общедоступный IP-адрес](#Public-IP-address).</span><span class="sxs-lookup"><span data-stu-id="793e1-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="793e1-120">Сетевая карта, или сетевой адаптер, представляет сетевой интерфейс, который может быть связан с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="793e1-120">A Network Interface Card, or NIC, represents a network interface that can be associated to a virtual machine (VM).</span></span> <span data-ttu-id="793e1-121">У виртуальной машины может быть одна или несколько сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="793e1-121">A VM can have one or more NICs.</span></span>

![Сетевая карта на одной виртуальной машине](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="793e1-123">Конфигурации IP</span><span class="sxs-lookup"><span data-stu-id="793e1-123">IP configurations</span></span>
<span data-ttu-id="793e1-124">У сетевых карт есть дочерний объект с именем **ipConfigurations** , содержащий следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="793e1-124">NICs have a child object named **ipConfigurations** containing the following properties:</span></span>

| <span data-ttu-id="793e1-125">Свойство</span><span class="sxs-lookup"><span data-stu-id="793e1-125">Property</span></span> | <span data-ttu-id="793e1-126">Описание</span><span class="sxs-lookup"><span data-stu-id="793e1-126">Description</span></span> | <span data-ttu-id="793e1-127">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="793e1-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="793e1-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="793e1-128">**subnet**</span></span> |<span data-ttu-id="793e1-129">Подсеть, к которой подключена сетевая карта.</span><span class="sxs-lookup"><span data-stu-id="793e1-129">Subnet the NIC is onnected to.</span></span> |<span data-ttu-id="793e1-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="793e1-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="793e1-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="793e1-131">**privateIPAddress**</span></span> |<span data-ttu-id="793e1-132">IP-адрес для сетевой карты в подсети</span><span class="sxs-lookup"><span data-stu-id="793e1-132">IP address for the NIC in the subnet</span></span> |<span data-ttu-id="793e1-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="793e1-133">10.0.0.8</span></span> |
| <span data-ttu-id="793e1-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="793e1-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="793e1-135">Метод выделения IP-адресов</span><span class="sxs-lookup"><span data-stu-id="793e1-135">IP allocation method</span></span> |<span data-ttu-id="793e1-136">Динамический или статический</span><span class="sxs-lookup"><span data-stu-id="793e1-136">Dynamic or Static</span></span> |
| <span data-ttu-id="793e1-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="793e1-137">**enableIPForwarding**</span></span> |<span data-ttu-id="793e1-138">Можно ли использовать сетевую карту для маршрутизации</span><span class="sxs-lookup"><span data-stu-id="793e1-138">Whether the NIC can be used for routing</span></span> |<span data-ttu-id="793e1-139">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="793e1-139">true or false</span></span> |
| <span data-ttu-id="793e1-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="793e1-140">**primary**</span></span> |<span data-ttu-id="793e1-141">Является ли эта сетевая карта основной для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="793e1-141">Whether the NIC is the primary NIC for the VM</span></span> |<span data-ttu-id="793e1-142">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="793e1-142">true or false</span></span> |
| <span data-ttu-id="793e1-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="793e1-143">**publicIPAddress**</span></span> |<span data-ttu-id="793e1-144">PIP, сопоставленный с сетевой картой</span><span class="sxs-lookup"><span data-stu-id="793e1-144">PIP associated with the NIC</span></span> |<span data-ttu-id="793e1-145">См. раздел [Параметры DNS](#DNS-settings).</span><span class="sxs-lookup"><span data-stu-id="793e1-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="793e1-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="793e1-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="793e1-147">Пулы адресов серверной части, с которыми сопоставлена сетевая карта</span><span class="sxs-lookup"><span data-stu-id="793e1-147">Back end address pools the NIC is associated with</span></span> | |
| <span data-ttu-id="793e1-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="793e1-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="793e1-149">Правила входящего трафика NAT для балансировщика нагрузки, с которыми сопоставлена сетевая карта</span><span class="sxs-lookup"><span data-stu-id="793e1-149">Inbound load balancer NAT rules the NIC is associated with</span></span> | |

<span data-ttu-id="793e1-150">Пример общедоступного IP-адреса в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="793e1-150">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="793e1-151">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="793e1-151">Additional resources</span></span>
* <span data-ttu-id="793e1-152">Прочитайте [справочную документацию по REST API](https://msdn.microsoft.com/library/azure/mt163579.aspx) для сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="793e1-152">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

