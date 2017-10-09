## <a name="application-gateway"></a><span data-ttu-id="531aa-101">Шлюз приложений</span><span class="sxs-lookup"><span data-stu-id="531aa-101">Application Gateway</span></span>
<span data-ttu-id="531aa-102">Шлюз приложений обеспечивает управляемое Azure решение по балансировке нагрузки HTTP на основе технологии балансировки нагрузки на 7 уровне.</span><span class="sxs-lookup"><span data-stu-id="531aa-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="531aa-103">Балансировка нагрузки приложения позволяет использовать hello правила маршрутизации для сетевого трафика в зависимости от HTTP.</span><span class="sxs-lookup"><span data-stu-id="531aa-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="531aa-104">Свойство</span><span class="sxs-lookup"><span data-stu-id="531aa-104">Property</span></span> | <span data-ttu-id="531aa-105">Описание</span><span class="sxs-lookup"><span data-stu-id="531aa-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="531aa-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="531aa-106">**backendAddressPools**</span></span> |<span data-ttu-id="531aa-107">Список IP-адресов серверов серверной части hello Hello.</span><span class="sxs-lookup"><span data-stu-id="531aa-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="531aa-108">Hello IP-адресов либо должен принадлежать подсети виртуальной сети toohello или должен быть открытый IP-адрес или VIP или частного IP</span><span class="sxs-lookup"><span data-stu-id="531aa-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="531aa-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="531aa-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="531aa-110">У каждого пула есть такие параметры, как порт, протокол и сходство на основе файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="531aa-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="531aa-111">Эти параметры являются связанные tooa пул, а также примененные tooall серверы в пуле hello</span><span class="sxs-lookup"><span data-stu-id="531aa-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="531aa-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="531aa-112">**frontendPorts**</span></span> |<span data-ttu-id="531aa-113">Этот порт является hello открытый порт открыт для шлюза приложения hello.</span><span class="sxs-lookup"><span data-stu-id="531aa-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="531aa-114">Трафик обращений к этому порту, а затем возвращает перенаправляется tooone hello серверной части серверов</span><span class="sxs-lookup"><span data-stu-id="531aa-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="531aa-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="531aa-115">**httpListeners**</span></span> |<span data-ttu-id="531aa-116">Прослушиватель имеет интерфейсный порт, протокол (Http или Https, они зависят от регистра) и имя сертификата SSL hello (при настройке протокола SSL разгрузки)</span><span class="sxs-lookup"><span data-stu-id="531aa-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="531aa-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="531aa-117">**requestRoutingRules**</span></span> |<span data-ttu-id="531aa-118">правило Hello привязывает hello hello и прослушивателя внутренний пул серверов и определяет, какой трафик hello серверной части пула серверов должны быть направлены.</span><span class="sxs-lookup"><span data-stu-id="531aa-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="531aa-119">В настоящее время работает только по принципу циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="531aa-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="531aa-120">Пример шаблона шлюза приложений в формате Json:</span><span class="sxs-lookup"><span data-stu-id="531aa-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
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


### <a name="additional-resources"></a><span data-ttu-id="531aa-121">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="531aa-121">Additional resources</span></span>
<span data-ttu-id="531aa-122">Подробнее об этом см. в описании [REST API шлюза приложений](https://msdn.microsoft.com/library/azure/mt299388.aspx).</span><span class="sxs-lookup"><span data-stu-id="531aa-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

