---
title: "шаблоны aaaNetworking для Azure Service Fabric | Документы Microsoft"
description: "Описывает общих сетевых шаблонов для службы структуры и как toocreate кластера с помощью Azure сетевые возможности."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Схемы сетевых подключений Service Fabric
Кластер Azure Service Fabric можно интегрировать с другими сетевыми компонентами Azure. В этой статье мы покажем, как toocreate кластеры, hello используйте следующие атрибуты:

- [существующая виртуальная сеть или подсеть](#existingvnet);
- [статический общедоступный IP-адрес](#staticpublicip);
- [подсистема балансировки нагрузки только для внутреннего использования](#internallb);
- [внутренняя и внешняя подсистемы балансировки нагрузки](#internalexternallb).

Service Fabric выполняется в стандартном масштабируемом наборе виртуальных машин. Любые функции, которые можно использовать в масштабируемом наборе виртуальных машин, можно также использовать и в кластере Service Fabric. разделы сети Hello hello шаблонов диспетчера ресурсов Azure для набора масштабирования виртуальной машины и службы структуры являются идентичными. После развертывания tooan существующей виртуальной сети, он будет легко tooincorporate другие сетевые функции, такие как Azure ExpressRoute, шлюз VPN Azure, группы безопасности сети и виртуальную сеть пиринга.

Служба Service Fabric является уникальной среди других сетевых компонентов в одном аспекте. Hello [портал Azure](https://portal.azure.com) внутренним образом использует hello Service Fabric toocall tooa кластера tooget информация о поставщике ресурсов о узлы и приложения. поставщик ресурсов Hello Service Fabric требуется порт шлюза общедоступный входящий доступ toohello HTTP (порт 19080, по умолчанию) в конечной точке управления hello. [Обозреватель Service Fabric](service-fabric-visualizing-your-cluster.md) использует hello toomanage конечной точки управления кластера. поставщик ресурсов Hello Service Fabric также использует порт tooquery информация о кластере toodisplay в hello портал Azure. 

Если порт 19080 не доступен из поставщика ресурсов Service Fabric hello, сообщение, например *узлы не найдены* появится на портала hello и отображается пустой список узла и приложения. Если вы хотите toosee кластера в hello портал Azure, подсистема балансировки нагрузки, должен предоставлять общий IP-адрес и вашей группе безопасности сети должны разрешать входящий трафик порта 19080. Если настройки не удовлетворяет этим требованиям, hello портал Azure не отображает hello состояния кластера.

## <a name="templates"></a>Шаблоны

Все шаблоны Service Fabric находятся в [одном загружаемом файле](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip). Должен быть доступ toodeploy hello шаблоны в качестве-с помощью следующих команд PowerShell hello. Если вы развертываете hello существующий шаблон виртуальной сети Azure или hello статического открытого шаблон IP-адреса, сначала прочтите hello [начальной установки](#initialsetup) этой статьи.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>Начальная настройка

### <a name="existing-virtual-network"></a>Существующая виртуальная сеть

В следующем примере hello, мы начнем с существующей виртуальной сети с именем ExistingRG виртуальной сети, в hello **ExistingRG** группы ресурсов. подсети Hello совпадает с именем по умолчанию. Эти ресурсы по умолчанию создаются при использовании hello Azure портала toocreate стандартной виртуальной машины (VM). Hello виртуальной сети и подсети можно создать без создания hello виртуальной Машины, но основной целью hello Добавление кластера tooan существующей виртуальной сети является tooother подключения tooprovide сети виртуальных машин. Создание hello виртуальной Машины дает хороший пример как обычно используется существующей виртуальной сети. Если кластер Service Fabric использует только внутренняя Подсистема балансировки нагрузки, без общедоступный IP-адрес можно использовать hello виртуальной Машины и ее общедоступный IP-адрес как безопасный *перехода поле*.

### <a name="static-public-ip-address"></a>Статический общедоступный IP-адрес

Как правило, статический общедоступный IP-адрес, выделенный ресурс, который управляется отдельно от hello виртуальных Машин или виртуальных машин, он назначен. Он предоставляется в отдельная группа сетевых ресурсов (как противоположность tooin hello Service Fabric группы ресурсов кластера сам). Создайте статический общедоступный IP-адрес, с именем staticIP1 в hello ExistingRG группе ресурсов, в hello портал Azure или с помощью PowerShell:

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Шаблон Service Fabric

В примерах hello в этой статье мы используем template.json Service Fabric hello. Перед созданием кластера можно использовать шаблон hello toodownload hello стандартный мастер портала с портала hello. Также можно использовать один из шаблонов hello в hello [коллекции шаблонов](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), такие как hello [пяти узел кластера Service Fabric](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>Существующая виртуальная сеть или подсеть

1. Измените имя параметра toohello hello подсети hello существующей подсети, а затем добавьте две новые параметры tooreference hello существующей виртуальной сети:

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. Изменение hello `vnetID` переменной toopoint toohello существующей виртуальной сети:

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Удалите `Microsoft.Network/virtualNetworks` из ресурсов, чтобы платформа Azure не создала виртуальную сеть:

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Закомментируйте hello виртуальной сети из hello `dependsOn` атрибут `Microsoft.Compute/virtualMachineScaleSets`, поэтому вы не зависят от создания новой виртуальной сети:

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Развертывание шаблона hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    После развертывания виртуальной сети должен включать набор hello новый масштабирования виртуальных машин. Тип узла набора масштабирования виртуальной машины Hello должны показывать hello существующую виртуальную сеть и подсети. Также можно использовать удаленного рабочего стола (RDP) tooaccess hello виртуальной Машины, которые была записаны в виртуальной сети hello и tooping hello новый профиль в наборе виртуальных машин:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

Еще один пример см. в разделе [, не определенных tooService структуры](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>Статический общедоступный IP-адрес

1. Добавьте параметры для hello имя hello существующие группы ресурсов статического IP, имя и полное доменное имя (FQDN):

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Удалите hello `dnsName` параметра. (hello статический IP-адрес уже имеется.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. Добавьте переменную tooreference hello существующий статический IP-адрес:

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Удалите `Microsoft.Network/publicIPAddresses` из ресурсов, чтобы платформа Azure не создала IP-адрес:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Закомментируйте hello IP-адрес из hello `dependsOn` атрибут `Microsoft.Network/loadBalancers`, поэтому оно не зависит от создается новый IP-адрес:

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. В hello `Microsoft.Network/loadBalancers` ресурсов, изменение hello `publicIPAddress` элемент `frontendIPConfigurations` tooreference hello существующий статический IP-адрес вместо только что созданной:

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. В hello `Microsoft.ServiceFabric/clusters` ресурсов, изменение `managementEndpoint` toohello полное доменное имя DNS hello статического IP-адреса. При использовании безопасного кластера убедитесь, что вы изменили *http://* слишком*https://*. (Обратите внимание, что этот шаг применяется только кластеры tooService структуры. Если вы используете масштабируемый набор виртуальных машин, то пропустите этот шаг.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Развертывание шаблона hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

После развертывания, можно видеть, что Подсистема балансировки нагрузки привязанного toohello открытый статический IP-адрес из hello другой группе ресурсов. Здравствуйте, конечная точка подключения клиента Service Fabric и [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) конечной точки toohello полное доменное имя DNS hello статического IP-адреса.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>Подсистема балансировки нагрузки только для внутреннего использования

Этот сценарий заменяет hello внешней подсистемы балансировки нагрузки в шаблоне Service Fabric по умолчанию hello подсистемы балансировки нагрузки только для внутреннего использования. Влияет на hello портал Azure, для поставщика ресурсов Service Fabric hello предшествующий раздел hello см.

1. Удалите hello `dnsName` параметра. (он не требуется).

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. При необходимости, если используется метод статического выделения, можно добавить параметр статического IP-адреса. Если вы используете метод динамическое выделение, необязательно toodo этот шаг.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Удалите `Microsoft.Network/publicIPAddresses` из ресурсов, чтобы платформа Azure не создала IP-адрес:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Удалите IP-адрес hello `dependsOn` атрибут `Microsoft.Network/loadBalancers`, поэтому оно не зависит от создается новый IP-адрес. Добавить виртуальную сеть hello `dependsOn` атрибут, так как Подсистема балансировки нагрузки hello теперь зависит от подсети hello hello в виртуальной сети:

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Изменить подсистему балансировки нагрузки hello `frontendIPConfigurations` настройки параметров с помощью `publicIPAddress`, toousing подсети и `privateIPAddress`. `privateIPAddress` использует предварительно определенный статический внутренний IP-адрес. toouse динамический IP-адрес, удалите hello `privateIPAddress` элемент, а затем измените `privateIPAllocationMethod` слишком**динамическое**.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. В hello `Microsoft.ServiceFabric/clusters` ресурсов, изменение `managementEndpoint` адрес подсистемы балансировки нагрузки внутренней toohello toopoint. При использовании безопасного кластера, убедитесь, что вы изменили *http://* слишком*https://*. (Обратите внимание, что этот шаг применяется только кластеры tooService структуры. Если вы используете масштабируемый набор виртуальных машин, то пропустите этот шаг.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Развертывание шаблона hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

После развертывания поддерживаемый подсистемой балансировки нагрузки использует hello 10.0.0.250 частного статического IP-адреса. Если имеется другой компьютер в этой же виртуальной сети, можно перейти toohello внутренней [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) конечной точки. Обратите внимание, что подключение выполняется tooone hello узлов за подсистемой балансировки нагрузки hello.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>Внутренняя и внешняя подсистемы балансировки нагрузки

В этом сценарии с hello существующих одним узлом тип внешней подсистемы балансировки нагрузки и добавить внутренний балансировщик нагрузки для hello того же типа узла. Пул адресов серверной части tooa порту внутренней могут назначаться только балансировки нагрузки одного tooa. Выберите, какая подсистема балансировки нагрузки будет управлять портами вашего приложения, а какая — конечными точками управления (порты 19000 и 19080). Если конечные точки управления hello разместить на hello внутренней подсистемы балансировки нагрузки, имейте в виду hello ресурса службы фабрики поставщика ограничения, описанные в статье hello. В примере hello мы используем конечные точки управления hello остаются на hello внешней подсистемы балансировки нагрузки. Можно также добавить порт 80 приложения порт и поместите его на hello внутренней подсистемы балансировки нагрузки.

В кластере типа узла двух один узел является на hello внешней подсистемы балансировки нагрузки. Hello узле такого типа является hello внутренний балансировщик нагрузки. toouse типа узла два кластера, hello создать портал два узла типа в шаблоне (который поставляется с двумя подсистемы балансировки нагрузки), переключение hello второй нагрузки балансировки tooan внутренней подсистемы балансировки нагрузки. Дополнительные сведения см. в разделе hello [балансировки нагрузки только для внутреннего использования](#internallb) раздела.

1. Добавьте параметром IP-адреса подсистемы балансировки нагрузки статический внутренний hello. (Заметки о связанных toousing динамический IP-адрес, см. в предыдущих разделах этой статьи.)

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. Добавьте параметр порта приложения 80.

3. tooadd внутренней версии существующих hello сети переменные, скопируйте и вставьте их и добавьте «-Int» toohello имя:

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. Если начать с шаблона создается портал hello, который использует приложение порт 80, шаблон портала по умолчанию hello добавляет AppPort1 (порт 80) на hello внешней подсистемы балансировки нагрузки. В этом случае удалите AppPort1 из hello внешней подсистемы балансировки нагрузки `loadBalancingRules` и зондов, поэтому ее можно добавить toohello внутренняя Подсистема балансировки нагрузки:

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. Добавьте второй ресурс `Microsoft.Network/loadBalancers`. Выглядит аналогично toohello внутренняя Подсистема балансировки нагрузки в hello [балансировки нагрузки только для внутреннего использования](#internallb) раздела, но использует hello «-Int» загрузить балансировки переменных и реализует только hello приложения порт 80. При этом также удаляются `inboundNatPools`, конечные точки протокола удаленного рабочего СТОЛА tookeep на hello внешняя Подсистема балансировки нагрузки. Если вы хотите протокола удаленного рабочего СТОЛА на hello внутренней подсистемы балансировки нагрузки, переместите `inboundNatPools` из toothis подсистемы балансировки нагрузки hello внутренняя Подсистема балансировки нагрузки:

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. В `networkProfile` для hello `Microsoft.Compute/virtualMachineScaleSets` ресурсов, добавить пул внутренних адресов серверной части hello:

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Развертывание шаблона hello:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

После развертывания можно увидеть два подсистемы балансировки нагрузки в группе ресурсов hello. При просмотре hello подсистемы балансировки нагрузки, вы увидите hello общедоступный IP-адрес и управления конечными точками (порты 19000 и 19080), назначенными toohello общедоступный IP-адрес. Также видно hello статического внутреннего IP адрес и приложения назначен конечной точки (порт 80) toohello внутренняя Подсистема балансировки нагрузки. Использование подсистемы балансировки нагрузки hello того же набора масштабирования виртуальных машин пула серверной части.

## <a name="next-steps"></a>Дальнейшие действия
[Создание кластера](service-fabric-cluster-creation-via-arm.md)
