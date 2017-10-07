---
title: "aaaDeploying ресурсов вычислений Linux с помощью шаблонов диспетчера ресурсов Azure | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 1c4d419e-ba0e-45e4-a9dd-7ee9975a86f9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0bc26805860fed47923d46fc84f357060f68a951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-linux-vms"></a>Архитектура приложений с использованием шаблонов Azure Resource Manager для виртуальных машин Linux

При разработке развертывания диспетчера ресурсов Azure, требования к вычислений должны toobe сопоставлен tooAzure ресурсы и службы. Если приложение содержит несколько конечных точек http, базы данных и службу кэширования данных, hello ресурсы Azure, на которых размещены каждого из этих компонентов должен toobe процессов оптимизации. Например приложение Music Store образец hello содержит веб-приложения, размещенного на виртуальной машине и базу данных SQL, которая размещается в базе данных Azure SQL. 

В этом документе описаны как hello Music Store вычислительные ресурсы настроены в шаблоне Azure Resource Manager образец hello. Здесь будут описаны все зависимости и уникальные настройки. Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure. Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания на Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="virtual-machine"></a>Виртуальная машина
Hello Music Store приложение включает веб-приложения, где можно просматривать и покупать музыка клиентов. Для размещения веб-приложений можно использовать несколько служб Azure. В нашем примере используется виртуальная машина. С помощью шаблона Music Store образец hello, развернута виртуальная машина, установить веб-сервер и веб-сайт Music Store hello установлен и настроен. Ради hello объекта в этой статье подробно только hello развертывания виртуальной машины. конфигурации Hello hello веб-сервера и приложения hello подробно описана в статье более поздней версии.

Виртуальные машины можно добавить tooa шаблон, с помощью Visual Studio добавьте новый ресурс мастер, или путем вставки допустимых данных JSON в шаблон развертывания hello hello. Для развертывания виртуальной машины также потребуются несколько связанных ресурсов. Если используется шаблон hello toocreate Visual Studio, эти ресурсы создаются автоматически. При ручном создании шаблона hello, эти ресурсы требуют toobe вставляется и настроен.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [JSON виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L295).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
      ........<truncated>  
    }
```

После развертывания hello свойства виртуальной машины можно увидеть в hello портал Azure.

![Виртуальная машина](./media/dotnet-core-2-architecture/vm.png)

## <a name="storage-account"></a>Учетная запись хранения
Учетные записи хранения имеют множество возможностей и параметров хранения. Для контекста hello виртуальных машин Azure учетная запись хранения содержит hello виртуальных жестких дисков виртуальной машины hello и любых дополнительных дисков данных. Образец Hello Music Store включает один хранилища учетной записи toohold hello виртуального жесткого диска для каждой виртуальной машины в развертывании hello. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [учетной записи хранилища](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L109).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

Учетная запись хранения —, связанных с виртуальной машины в объявлении шаблона диспетчера ресурсов hello hello виртуальной машины. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [виртуальной машины и учетной записи хранилища ассоциации](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L341).

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

После развертывания можно просмотреть hello учетной записи хранилища в hello портал Azure.

![Учетная запись хранения](./media/dotnet-core-2-architecture/storacct.png)

Щелкните кнопкой мыши в контейнер BLOB-объектов учетной записи хранилища hello, можно увидеть hello файлу виртуального жесткого диска для всех виртуальных машин, развернутых с помощью шаблона hello.

![Виртуальные жесткие диски](./media/dotnet-core-2-architecture/vhd.png)

Дополнительные сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Виртуальная сеть
Если виртуальная машина требует внутренней сети, например toocommunicate возможность hello с другими виртуальными машинами и ресурсами Azure, виртуальная сеть Azure не требуется.  Виртуальная сеть не делает hello виртуальной машины доступно по Интернету hello. Для открытого доступа нужен общедоступный IP-адрес, который описывается в следующих статьях этой серии.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [виртуальную сеть и подсети](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L136).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
    ]
  }
}
```

Из hello портал Azure виртуальная сеть hello выглядит как hello после изображения. Обратите внимание, что все виртуальные машины, развернутые с шаблоном hello вложенного toohello виртуальной сети.

![Виртуальная сеть](./media/dotnet-core-2-architecture/vnet.png)

## <a name="network-interface"></a>Сетевой интерфейс
 Сетевой интерфейс подключается виртуальной сети виртуальной машины tooa, точнее tooa подсети, который был определен в виртуальной сети hello. 

 Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [сетевой интерфейс](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L166).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceNamePrefix'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'SSH-VM', copyIndex())]"
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
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/SSH-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

Каждый ресурс виртуальной машины включает в себя профиль сети. сетевой интерфейс Hello не связанную с виртуальной машиной hello в этом профиле.  

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [профиль сети виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L350).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceNamePrefix'), copyindex()))]"
    }
  ]
}
```

Из hello портал Azure hello сетевой интерфейс выглядит как hello после изображения. внутренний IP-адрес Hello и наборов ассоциаций hello виртуальной машины можно просмотреть на ресурс hello сетевого интерфейса.

![Сетевой интерфейс](./media/dotnet-core-2-architecture/nic.png)

Дополнительные сведения см. в [документации по виртуальным сетям Azure](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>База данных SQL Azure
В дополнение к этому tooa виртуальная машина, содержащая Music Store hello веб-сайта, базы данных SQL Azure — развернутой toohost hello Music Store, база данных. Преимущество Hello здесь использования базы данных SQL Azure — что второй набор виртуальных машин не требуется и масштабируемость и доступность встроен в службы hello.

Базы данных Azure SQL можно добавить с помощью Visual Studio добавьте новый ресурс мастер, или путем вставки допустимых данных JSON в шаблоне hello. Hello ресурсов SQL Server включает в себя имя пользователя и пароль, которые предоставляются права администратора на экземпляре SQL Server hello. Также добавляется ресурс брандмауэра SQL. По умолчанию приложения, размещенные в Azure, может tooconnect с экземпляром SQL hello. tooallow внешних таких SQL Server Management studio tooconnect toohello экземпляр SQL Server, брандмауэр hello приложению toobe настроен. Конфигурация по умолчанию hello подойдет ради hello демонстрации Music Store hello. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [базу данных SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L401).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicStoreSqlName')]",
  "location": "[resourceGroup().location]",

  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('sqlAdminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicStoreSqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Представление hello SQL server и MusicStore базы данных, как показано в hello портал Azure.

![SQL Server](./media/dotnet-core-2-architecture/sql.png)

Дополнительные сведения о развертывании базы данных SQL см. в [документации по базе данных SQL Azure](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Дальнейшие действия
<hr>

[Шаг 2. Доступ и безопасность в шаблонах Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

