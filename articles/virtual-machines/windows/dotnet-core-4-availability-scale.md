---
title: "aaaAvailability и масштабирования в шаблоны диспетчера ресурсов Azure | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a122d8e9536ea5fc2dc9c3f84042ed5c5179d783
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a>Параметры доступности и масштабирования в шаблонах Azure Resource Manager для виртуальных машин Windows

См. toouptime и hello запросу toomeet возможности высокой доступности и масштабируемости. Если приложение должно быть 99,9% времени hello, он должен toohave архитектуру, которая позволяет нескольким ресурсам параллельных вычислений. Например вместо одного веб-сайта, конфигурации с более высоким уровнем доступности содержится несколько экземпляров hello же сайт, с технологией перед их балансировки. В этой конфигурации один экземпляр приложения hello можно отключить для обслуживания, прерывая toofunction оставшихся hello. Масштаб на hello другой стороны относится возможность tooserve tooan приложений запросу. С загрузкой балансировкой приложения, добавление или удаление экземпляров из пула hello позволяет запросу toomeet tooscale приложения.

В этом документе описаны как hello развертывания образца Music Store настраивается для высокой доступности и масштабируемости. Здесь будут описаны все зависимости и уникальные настройки. Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure. Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания в Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="availability-set"></a>Группа доступности
Группа доступности логически охватывает виртуальные машины Azure на физических узлах и другие инфраструктурные компоненты, например источники питания и физическое сетевое оборудование. Она гарантирует, что в случае обслуживания, сбоя устройства или простоя по другой причине не все виртуальные машины будут затронуты. Группы доступности могут быть добавлены tooan шаблона Azure Resource Manager с помощью Visual Studio новый мастер добавления ресурсов hello или вставка допустимых данных JSON в шаблон.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [набор доступности](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

Группа доступности определяется как свойство ресурса виртуальной машины. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [набор доступности связи с виртуальной машиной](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
Hello доступности, как видно из hello портал Azure. Каждой виртуальной машине и сведения о конфигурации hello подробно описаны ниже.

![Группа доступности](./media/dotnet-core-4-availability-scale/ase-win.png)

Дополнительные сведения о группах доступности см. в статье [Управление доступностью виртуальных машин](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="network-load-balancer"></a>Балансировщик сетевой нагрузки
В то время как группа доступности обеспечивает устойчивость к сбоям приложения, подсистемы балансировки нагрузки создает много экземпляров приложения hello на одного сетевого адреса. Несколько экземпляров приложения могут размещаться на нескольких виртуальных машин, каждый из них подключен tooa подсистемы балансировки нагрузки. Как осуществляется приложения hello, маршруты подсистемы балансировки нагрузки hello hello входящего запроса участниках присоединенного hello. Подсистема балансировки нагрузки могут добавляться с помощью Visual Studio новый мастер добавления ресурсов hello или путем вставки должным образом в формате JSON ресурсов в шаблон диспетчера ресурсов Azure hello.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [балансировки сетевой нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

Так как пример приложения hello предоставляется toohello Интернет, общий IP-адрес, этот адрес связан с подсистемой балансировки нагрузки hello. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [связь балансировки сетевой нагрузки с общедоступным IP-адресом](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

От hello портал Azure hello Обзор балансировки сетевой нагрузки показывает hello связь с hello общедоступный IP-адрес.

![Балансировщик сетевой нагрузки](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a>Правило балансировщика нагрузки
При использовании подсистемы балансировки нагрузки, настроены правила, определяющие, как трафик распределяется по всем ресурсам hello предназначен. Приложение Music Store образец hello трафик порта 80 hello общедоступного IP-адреса и распределяется по порту 80 всех виртуальных машин. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [правило подсистемы балансировки нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

Представление в виде сети hello правило подсистемы балансировки нагрузки с портала hello.

![Правило балансировщика сетевой нагрузки](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a>Проба балансировщика нагрузки
Hello балансировки нагрузки также требуется toomonitor каждой виртуальной машины, чтобы запросы обслуживаются только toorunning системы. Для этого он постоянно проверяет предопределенный порт. Развертывание Music Store Hello — tooprobe настроенный порт 80 на всех включенных виртуальных машин. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [пробы подсистемы балансировки нагрузки](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

с портала Azure hello Hello зонд подсистемы балансировки нагрузки.

![Проба балансировщика сетевой нагрузки](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a>Правила преобразования сетевых адресов для входящих подключений
При использовании подсистемы балансировки нагрузки, правила должны toobe помещен на место, которые предоставляют Сбалансированный доступа без загрузки tooeach виртуальной машины. Например, при создании RDP-подключения к каждой виртуальной машине для этого трафика не следует применять балансировку нагрузки. Вместо этого необходимо настроить предопределенный путь с использованием ресурса правила NAT для входящего трафика. Использовать этот ресурс, входящих сообщений может быть сопоставленных tooindividual виртуальных машин. 

С hello приложение Music Store начиная с 5000 порта — сопоставленных tooport 3389 на каждой виртуальной машине для RDP-доступ. Hello `copyindex()` функция является используется tooincrement Здравствуйте входящий порт, таким образом, что hello второй виртуальной машины получит входящий порт 5001, hello 5002 третьей и т. д.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [правила для входящих подключений NAT](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

Один пример правила для входящего трафика NAT как hello возникающим в портале Azure. Правило NAT протокола удаленного рабочего СТОЛА создается для каждой виртуальной машины в развертывании hello.

![Правило NAT для входящего трафика](./media/dotnet-core-4-availability-scale/natrule-win.png)

Подробные сведения о hello Azure балансировки сетевой нагрузки см. в разделе [балансировки нагрузки для служб инфраструктуры Azure](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Развертывание нескольких виртуальных машин
Наконец функция tooeffectively группе доступности или балансировки нагрузки необходимы несколько виртуальных машин. Несколько виртуальных машин можно развернуть с помощью функции копирования шаблона диспетчера ресурсов Azure hello. С помощью функции копирования hello, это не требуется toodefine ограниченное число виртуальных машин, вместо этого значения могут быть предоставлены динамически во время развертывания hello. функция копирования Hello потребляет hello число экземпляров toobe создан и обрабатывает развертывание hello нужное число виртуальных машин и связанных ресурсов.

В шаблоне музыка хранилища образец hello параметр определен, принимающий в число экземпляров. Этот номер используется во всех hello шаблона при создании виртуальных машин и связанные ресурсы.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
},
```

На hello ресурса виртуальной машины цикл hello копии присваивается имя и hello число экземпляров параметра toocontrol hello число полученный копий.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [функции копирования виртуальной машины](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

Текущая итерация Hello функции копирования hello можно осуществить с помощью hello `copyIndex()` функции. Hello значение индекса функции hello копирования может быть используется tooname виртуальные машины и другие ресурсы. Например, если развернуты два экземпляра виртуальной машины, им необходимо присвоить разные имена. Hello `copyIndex()` функция может использоваться как часть виртуальной машины hello имя toocreate уникальное имя. Пример hello `copyindex()` функция, используемая для именования можно увидеть в hello ресурса виртуальной машины. Здесь hello имя компьютера представляет собой объединение hello `vmName` параметр и hello `copyIndex()` функции. 

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [функции копирования в индекс](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309). 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

Hello `copyIndex` функция используется несколько раз в шаблоне образец hello Music Store. Ресурсы и использование функции `copyIndex` включают один экземпляр hello виртуальной машины такой что-либо конкретных tooa и сетевого интерфейса, правила подсистемы балансировки нагрузки, и любые зависит от функции. 

Дополнительные сведения о функции копирования hello см. в разделе [создание нескольких экземпляров ресурсов в диспетчере ресурсов Azure](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Дальнейшие действия
<hr>

[Шаг 4. Развертывание приложений с использованием шаблонов Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

