## <a name="load-balancer"></a><span data-ttu-id="04ca1-101">Подсистема балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="04ca1-101">Load Balancer</span></span>
<span data-ttu-id="04ca1-102">Подсистема балансировки нагрузки используется в том случае, если tooscale приложений.</span><span class="sxs-lookup"><span data-stu-id="04ca1-102">A load balancer is used when you want tooscale your applications.</span></span> <span data-ttu-id="04ca1-103">Типичные сценарии развертывания включают приложения, работающие на нескольких экземплярах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="04ca1-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="04ca1-104">Hello экземпляров виртуальных Машин аппаратные подсистемы балансировки нагрузки, помогающая toodistribute сетевой трафик toohello различных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="04ca1-104">hello VM instances are fronted by a load balancer that helps toodistribute network traffic toohello various instances.</span></span> 

![Сетевая карта на одной виртуальной машине](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="04ca1-106">Свойство</span><span class="sxs-lookup"><span data-stu-id="04ca1-106">Property</span></span> | <span data-ttu-id="04ca1-107">Описание</span><span class="sxs-lookup"><span data-stu-id="04ca1-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04ca1-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="04ca1-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="04ca1-109">Балансировщик нагрузки может включать в себя один или несколько внешних IP-адресов, которые также называются виртуальными IP-адресами.</span><span class="sxs-lookup"><span data-stu-id="04ca1-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="04ca1-110">Эти IP-адресов служат в качестве входящего трафика hello и может быть общедоступный IP-адрес или частного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="04ca1-110">These IP addresses serve as ingress for hello traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="04ca1-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="04ca1-111">*backendAddressPools*</span></span> |<span data-ttu-id="04ca1-112">Это IP-адреса, связанные с hello распределяются нагрузки toowhich сетевых адаптеров виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="04ca1-112">these are IP addresses associated with hello VM NICs toowhich load will be distributed</span></span> |
| <span data-ttu-id="04ca1-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="04ca1-113">*loadBalancingRules*</span></span> |<span data-ttu-id="04ca1-114">Свойство правила сопоставляется с IP-адресом данного внешнего интерфейса и порта набор tooa сочетания IP-адресов серверной части и комбинация порт.</span><span class="sxs-lookup"><span data-stu-id="04ca1-114">a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="04ca1-115">С помощью одного определения ресурса балансировщика нагрузки можно задать несколько правил балансировки нагрузки, каждое из которых отражает сочетание внешнего IP-адреса и порта с серверным IP-адресом и портом, связанными с виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="04ca1-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="04ca1-116">правило Hello — один порт в hello внешнего интерфейса пула toomany виртуальных машин в пуле hello серверной части</span><span class="sxs-lookup"><span data-stu-id="04ca1-116">hello rule is one port in hello front end pool toomany virtual machines in hello back end pool</span></span> |
| <span data-ttu-id="04ca1-117">*Пробы*</span><span class="sxs-lookup"><span data-stu-id="04ca1-117">*Probes*</span></span> |<span data-ttu-id="04ca1-118">зонды включить отслеживание tookeep hello работоспособности экземпляров виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="04ca1-118">probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="04ca1-119">Если происходит сбой проверки работоспособности, hello экземпляр виртуальной машины будет выполнено из ротации автоматически</span><span class="sxs-lookup"><span data-stu-id="04ca1-119">If a health probe fails, hello virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="04ca1-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="04ca1-120">*inboundNatRules*</span></span> |<span data-ttu-id="04ca1-121">Правила NAT, определяющие hello входящий трафик с IP-адреса внешнего интерфейса hello и распределенных экземпляр toohello серверной части IP tooa отдельную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="04ca1-121">NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP tooa specific virtual machine instance.</span></span> <span data-ttu-id="04ca1-122">Правило NAT имеет один порт hello обслуживающего пул tooone виртуальной машине в серверной части пула hello</span><span class="sxs-lookup"><span data-stu-id="04ca1-122">NAT rule is one port in hello front end pool tooone virtual machine in hello back end pool</span></span> |

<span data-ttu-id="04ca1-123">Пример шаблона балансировщика нагрузки в формате Json:</span><span class="sxs-lookup"><span data-stu-id="04ca1-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[parameters('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[parameters('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="04ca1-124">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="04ca1-124">Additional resources</span></span>
<span data-ttu-id="04ca1-125">Дополнительные сведения см. в описании [REST API балансировщика нагрузки](https://msdn.microsoft.com/library/azure/mt163651.aspx).</span><span class="sxs-lookup"><span data-stu-id="04ca1-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

