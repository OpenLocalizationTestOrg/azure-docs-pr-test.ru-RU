## <a name="application-gateway"></a><span data-ttu-id="4e731-101">Шлюз приложений</span><span class="sxs-lookup"><span data-stu-id="4e731-101">Application Gateway</span></span>
<span data-ttu-id="4e731-102">Шлюз приложений обеспечивает управляемое Azure решение по балансировке нагрузки HTTP на основе технологии балансировки нагрузки на 7 уровне.</span><span class="sxs-lookup"><span data-stu-id="4e731-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="4e731-103">Балансировка нагрузки приложения позволяет использовать правила маршрутизации для сетевого трафика в зависимости от HTTP.</span><span class="sxs-lookup"><span data-stu-id="4e731-103">Application load balancing allows the use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="4e731-104">Свойство</span><span class="sxs-lookup"><span data-stu-id="4e731-104">Property</span></span> | <span data-ttu-id="4e731-105">Описание</span><span class="sxs-lookup"><span data-stu-id="4e731-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e731-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="4e731-106">**backendAddressPools**</span></span> |<span data-ttu-id="4e731-107">Список IP-адресов внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="4e731-107">The list of IP addresses of the back end servers.</span></span> <span data-ttu-id="4e731-108">Указанные IP-адреса должны относиться к подсети виртуальной сети либо представлять собой общедоступные, виртуальные либо частные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="4e731-108">The IP addresses listed should either belong to the virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="4e731-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="4e731-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="4e731-110">У каждого пула есть такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="4e731-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="4e731-111">Эти параметры привязываются к пулу и применяются ко всем серверам в этом пуле.</span><span class="sxs-lookup"><span data-stu-id="4e731-111">These settings are tied to a pool and are applied to all servers within the pool</span></span> |
| <span data-ttu-id="4e731-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="4e731-112">**frontendPorts**</span></span> |<span data-ttu-id="4e731-113">Общий порт, открытый в шлюзе приложений.</span><span class="sxs-lookup"><span data-stu-id="4e731-113">This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="4e731-114">Трафик поступает в этот порт, а затем перенаправляется на один из внутренних серверов.</span><span class="sxs-lookup"><span data-stu-id="4e731-114">Traffic hits this port, and then gets redirected to one of the back end servers</span></span> |
| <span data-ttu-id="4e731-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="4e731-115">**httpListeners**</span></span> |<span data-ttu-id="4e731-116">Прослушиватель имеет внешний порт, протокол (HTTP или HTTPS, с учетом регистра) и имя SSL-сертификата (если настраивается разгрузка SSL).</span><span class="sxs-lookup"><span data-stu-id="4e731-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="4e731-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="4e731-117">**requestRoutingRules**</span></span> |<span data-ttu-id="4e731-118">Связывает прослушиватель и пул внутренних серверов, а также определяет, в какой пул внутренних серверов следует направлять трафик.</span><span class="sxs-lookup"><span data-stu-id="4e731-118">The rule binds the listener and the back end server pool and defines which back end server pool the traffic should be directed.</span></span> <span data-ttu-id="4e731-119">В настоящее время работает только по принципу циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="4e731-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="4e731-120">Пример шаблона шлюза приложений в формате Json:</span><span class="sxs-lookup"><span data-stu-id="4e731-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location to deploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for the Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
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
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="4e731-121">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4e731-121">Additional resources</span></span>
<span data-ttu-id="4e731-122">Подробнее об этом см. в описании [REST API шлюза приложений](https://msdn.microsoft.com/library/azure/mt299388.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e731-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

