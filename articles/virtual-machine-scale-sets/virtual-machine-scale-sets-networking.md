---
title: "aaaNetworking для набора масштабирования виртуальной машины Azure | Документы Microsoft"
description: "Конфигурация свойств сети для масштабируемых наборов виртуальных машин Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Сеть для масштабируемых наборов виртуальных машин Azure

При развертывании Azure масштабирования виртуальной машины через портал hello задать определенные свойства сети, используемое по умолчанию, например правил NAT для входящего трафика подсистемы балансировки нагрузки Azure с. В этой статье описывается, каким образом задает toouse некоторые hello дополнительные сетевые возможности, которые можно настроить с масштабом.

Можно настроить все функции hello, описанные в этой статье, используя шаблоны Azure Resource Manager. Кроме того, будут добавлены примеры Azure CLI и PowerShell для выбранных компонентов. Используйте интерфейс командной строки версии 2.10 и PowerShell 4.2.0 или более поздней версии.

## <a name="accelerated-networking"></a>Ускорение работы в сети
Azure [Accelerated сети](../virtual-network/virtual-network-create-vm-accelerated-networking.md) позволяет повысить производительность сети путем включения SR-iov виртуализацию SR-IOV tooa виртуальной машины. toouse accelerated сетью с помощью набора масштабирования, задайте enableAcceleratedNetworking слишком**true** в параметрах набора масштабирования конфигураций сетевого интерфейса. Например:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>Создание набора масштабирования, который ссылается на существующую службу Azure Load Balancer
При создании набора масштабирования с помощью портала Azure hello новую подсистему балансировки загрузки создается для большинства параметров конфигурации. При создании набора масштабирования, которая должна tooreference существующей подсистемы балансировки нагрузки, это можно сделать с помощью CLI. Следующий пример скрипта Hello создается подсистемы балансировки нагрузки, а затем создается набора масштабирования, который ссылается на нее:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Настраиваемые параметры DNS
По умолчанию наборы масштабирования отключить на определенные параметры DNS hello hello виртуальной сети и подсети, в котором они были созданы. Однако вы можете настроить параметры DNS hello шкалы, задавать напрямую.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Создание масштабируемого набора с настраиваемыми DNS-серверами
в наборе с пользовательской конфигурацией DNS с помощью CLI 2.0 toocreate добавить hello **--dns-серверы** toohello аргумент **vmss создания** команды, за которыми следует пробел запятыми IP-адреса сервера. Например:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
tooconfigure пользовательские DNS-серверы в шаблоне Azure, добавить шкалу dnsSettings свойства toohello задать раздел конфигураций сетевого интерфейса. Например:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Создание масштабируемого набора с настраиваемыми именами доменов виртуальных машин
toocreate в наборе с пользовательским именем DNS для виртуальных машин с помощью CLI версии 2.0, добавить hello **виртуальной машины — доменное имя** toohello аргумент **vmss создания** команды, за которым следует строка, представляющая hello доменное имя.

добавить имя домена tooset hello в шаблон Azure **dnsSettings** набор масштабирования toohello свойство **конфигураций сетевого интерфейса** раздела. Например:

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

выходные данные Hello, для отдельных виртуальных машин DNS-имя может быть в hello следующие формы: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>Общедоступный IPv4 на каждую виртуальную машину
Как правило, виртуальным машинам в масштабируемом наборе Azure не требуются собственные общедоступные IP-адреса. В большинстве случаев это безопасное и экономичное tooassociate открытый IP адрес tooa нагрузки балансировки или tooan отдельных виртуальной машины (также называемого jumpbox), который затем направляет входящие соединения tooscale набор виртуальных машин, при необходимости (например, с помощью Входящие правила NAT).

Однако в некоторых сценариях требуется набор масштабирования виртуальных машин toohave собственные общедоступный IP-адрес адреса. Игры пример, где консоли требуется наличие toomake прямое подключение tooa облака виртуальной машины, которой выполняется обработка игры физических. Еще один пример — где виртуальные машины должны tooone внешних соединений toomake другой по регионам в распределенной базы данных.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Создание масштабируемого набора с общедоступным IP-адресом на виртуальную машину
toocreate набор масштабирования, которая назначает открытый IP адрес tooeach виртуальную машину с CLI 2.0, добавить hello **--public-ip каждой виртуальной машине** toohello параметр **vmss создания** команды. 

toocreate масштабирования, заданные с помощью шаблона Azure, убедитесь, что версия hello API hello Microsoft.Compute/virtualMachineScaleSets ресурсов по крайней мере **2017 г-03-30**и добавьте **publicIpAddressConfiguration**JSON свойство toohello в наборе раздел IP-конфигурации. Например:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Пример шаблона: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>Выполнение запроса hello общедоступный IP-адрес набора адресов hello виртуальных машин на шкале
общедоступные IP-адреса toolist hello назначенный tooscale набор виртуальных машин с помощью CLI 2.0, используйте hello **az vmss списка экземпляр public-IP-адреса** команды.

задать масштаб toolist общих IP-адресов с помощью PowerShell, используйте hello _Get AzureRmPublicIpAddress_ команды. Например:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

Вы также можете запроса hello общих IP-адресов с помощью ссылки на идентификатор ресурса hello hello открытый IP-адрес конфигурации напрямую. Например:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

общедоступные IP-адреса tooquery hello назначенный tooscale набор виртуальных машин с помощью hello [обозревателя ресурсов Azure](https://resources.azure.com), или hello Azure REST API с версией **2017 г-03-30** или более поздней версии.

tooview общих IP-адресов для масштабирования, заданные с помощью обозревателя ресурсов hello просмотрите hello **общедоступных** раздел находится в наборе масштабирования. Например, https://resources.azure.com/subscriptions/_ИД_подсистемы_/resourceGroups/_ваша_группа_ресурсов_/providers/Microsoft.Compute/virtualMachineScaleSets/_ваша_vmss_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

Выходные данные примера:
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>Несколько IP-адресов на сетевой адаптер
Каждый сетевой Адаптер подключен tooa виртуальной Машины в наборе масштабирования может иметь один или несколько IP-конфигурации, связанные с ним. Каждая конфигурация получает один частный IP-адрес. Кроме того, каждой конфигурации также может быть присвоен один ресурс общедоступного IP-адреса. toounderstand, сколько IP-адреса могут назначаться tooa сетевого Адаптера, и сколько общедоступных IP-адресов, можно использовать в подписку Azure, см. слишком[ограничения Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Несколько сетевых адаптеров на виртуальную машину
Можно создать до too8 сетевые адаптеры на каждую виртуальную машину, в зависимости от размера машины. Hello максимальное количество сетевых адаптеров на один компьютер доступен в hello [статье размер виртуальной Машины](../virtual-machines/windows/sizes.md). Hello следующий пример — сетевой профиль, показывающий несколько записей сетевого Адаптера и несколько общих IP-адресов на каждую виртуальную машину в наборе масштабирования:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>Группа безопасности сети на масштабируемый набор
Сетевые группы безопасности можно применить непосредственно tooa набор масштабирования, добавив toohello сетевой интерфейс конфигурации Справочник шкалы hello задать свойства виртуальной машины.

Например: 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о виртуальных сетях Azure см. в разделе слишком[этой документации](../virtual-network/virtual-networks-overview.md).
