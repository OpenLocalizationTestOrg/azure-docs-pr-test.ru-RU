---
title: "aaaAccess и безопасности в Azure шаблоны виртуальных машин Linux | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 07e47189-680e-4102-a8d4-5a8eb9c00213
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88fedc8287c1f8ab8397a03ddefe1e60a686815e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a>Доступ и безопасность в шаблонах Azure Resource Manager для виртуальных машин Linux

Приложения размещенных в Azure скорее всего, необходимость toobe доступ через hello Интернета или VPN-подключения Express Route с Azure. С образцом приложения hello Music Store, hello веб-сайта доступны на hello Интернета с общедоступный IP-адрес. С уровнем доступа установления подключений toohello доступа к приложениям и toohello ресурсы виртуальной машины сами должны быть защищены. Защиту доступа обеспечивает группа безопасности сети. 

В этом документе описаны как обеспечивается безопасность hello приложение Music Store в hello образец шаблона диспетчера ресурсов Azure. Здесь будут описаны все зависимости и уникальные настройки. Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure. Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания на Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="public-ip-address"></a>Общедоступный IP-адрес
можно использовать общий доступ tooprovide tooan ресурсов Azure, открытого ресурса IP-адреса. Общедоступный IP-адрес может быть статическим или динамическим. Если используется динамический адрес и останавливается и освобождается hello виртуальной машины, удаляется адреса hello. При запуске машины hello снова, ее можно назначить другой общедоступный IP-адрес. tooprevent объект IP адрес изменять, можно использовать зарезервированный IP-адрес. 

Общедоступный IP-адрес можно добавить hello Visual Studio новый мастер добавления ресурсов, с помощью шаблона Azure Resource Manager tooan или путем вставки допустимых данных JSON в шаблон. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [общедоступный IP-адрес](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicipaddressName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "public-ip-front"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Общедоступный IP-адрес может быть связан с виртуальным сетевым адаптером или с балансировщиком нагрузки. В этом примере, поскольку hello Music Store веб-сайта является Балансировка нагрузки для нескольких виртуальных машин hello общедоступный IP-адрес является вложенного toohello подсистемы балансировки нагрузки.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [ассоциации общедоступный IP-адрес с подсистемой балансировки нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Hello общедоступный IP-адрес, как просматривать hello портал Azure. Обратите внимание, что hello общедоступный IP-адрес связанного tooa балансировки нагрузки и не на виртуальной машине. В следующий документ hello этой серии приводится подробное описание подсистем балансировки нагрузки сети.

![Общедоступный IP-адрес](./media/dotnet-core-3-access-security/pubip.png)

Дополнительные сведения об общедоступных IP-адресах Azure см. в статье [IP-адреса в Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Группа безопасности сети
После доступа к установленным tooAzure ресурсы, должны быть ограничены такой доступ. Для виртуальных машин Azure безопасный доступ гарантирует группа безопасности сети. С образцом приложения hello Music Store все доступа toohello виртуальная машина является ограниченным доступом, за исключением через порт 80 для доступа по протоколу http и порт 22 для доступа по протоколу SSH. Tooan шаблона диспетчера ресурсов Azure, с использованием hello Visual Studio новый мастер добавления ресурсов, можно добавить сетевую группу безопасности или путем вставки допустимых данных JSON в шаблон.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [сетевой группы безопасности](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('nsgfront')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "nsg-front"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
}
```

В этом примере hello сетевая группа безопасности является, связанных с hello объекта подсети, объявленные в виртуальной сети ресурс hello. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [связь группы безопасности сети с помощью виртуальной сети](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
```

Вот какие группы безопасности сети hello как выглядит из hello портал Azure. Обратите внимание, что группу безопасности сети можно связать с подсетью и (или) с сетевым интерфейсом. В этом случае hello NSG — связанные tooa подсети. В этой конфигурации hello правила для входящих подключений применяются tooall виртуальными машинами, подключенными toohello подсети.

![Группа безопасности сети](./media/dotnet-core-3-access-security/nsg.png)

Дополнительные сведения о группах безопасности сети см. в статье [Группа безопасности сети](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Дальнейшие действия
<hr>

[Шаг 3. Доступность и масштабирование в шаблонах Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

