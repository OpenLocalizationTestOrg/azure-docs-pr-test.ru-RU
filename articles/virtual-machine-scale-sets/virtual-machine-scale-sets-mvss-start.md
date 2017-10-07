---
title: "aaaLearn о масштабирования виртуальных машин выбирать шаблоны | Документы Microsoft"
description: "Дополнительные сведения toocreate Минимальный масштаб допустимого набора шаблона для набора масштабирования виртуальной машины"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>Подробнее о шаблонах масштабируемых наборов виртуальных машин
[Шаблоны Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) — toodeploy хорошим способом группы связанных ресурсов. Этот учебник, показывающие, как toocreate Минимальный масштаб допустимого шаблона набора и как toomodify этот шаблон toosuit различных сценариев. Все примеры взяты из этого [репозитория GitHub](https://github.com/gatneil/mvss). 

Этот шаблон является предполагаемым toobe простой. Более полные примеры шкалы набор шаблонов см. в разделе hello [репозитории GitHub шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates) и выполните поиск папок, содержащих строку hello `vmss`.

Если вы уже знакомы с созданием шаблоны, можно пропустить toohello toosee раздел «Дальнейшие действия» как toomodify этот шаблон.

## <a name="review-hello-template"></a>Шаблон проверке hello

Использовать GitHub tooreview шаблона, набора наши Минимальный масштаб реальную [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).

В этом учебнике мы изучаем hello diff (`git diff master minimum-viable-scale-set`) toocreate hello минимальное работало в наборе шаблона по частям.

## <a name="define-schema-and-contentversion"></a>Определение элементов $schema и contentVersion
Во-первых, определим `$schema` и `contentVersion` в шаблоне hello. Hello `$schema` элемент определяет версию hello языка шаблона hello и используется для выделения синтаксиса в Visual Studio и другие аналогичные возможности проверки. Hello `contentVersion` элемент не используется в Azure. Вместо этого он позволяет хранить список версия шаблона hello.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>Определение параметров
Далее мы определим два параметра: `adminUsername` и `adminPassword`. Параметры являются значениями, задаваемыми во время развертывания hello. Hello `adminUsername` параметр является просто `string` типа, но поскольку `adminPassword` такое секрет, мы отправляем тип `securestring`. Более поздней версии эти параметры передаются в конфигурацию набора масштабирования hello.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>Определение переменных
Шаблоны диспетчера ресурсов также позволяют определить toobe переменных, используемых в дальнейшем в шаблон hello. Поэтому мы оставили hello объекта JSON пустым в нашем примере не используется любые переменные.

```json
  "variables": {},
```

## <a name="define-resources"></a>Определение ресурсов
Далее следует hello раздел ресурсов шаблона hello. Здесь, определить, действительно требуется toodeploy. В отличие от разделов `parameters` и `variables`, которые сами являются объектами JSON, раздел `resources` представляет собой JSON-список объектов JSON.

```json
   "resources": [
```

Каждый ресурс должен иметь свойства `type`, `name`, `apiVersion` и `location`. В этом примере для первого ресурса указан тип `Microsft.Network/virtualNetwork`, имя `myVnet` и версия API `2016-03-30`. (toofind hello последнюю версию API для типа ресурса в разделе hello [документация по Azure REST API](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>Определение расположения
расположение hello toospecify hello виртуальной сети, мы используем [функции шаблона диспетчера ресурсов](../azure-resource-manager/resource-group-template-functions.md). Каждая функция заключается в кавычки и квадратные скобки, примерно так: `"[<template-function>]"`. В этом случае мы используем hello `resourceGroup` функции. Он принимает аргументы и возвращает объект JSON, содержащий метаданные о группе ресурсов hello, развертывания для этого развертывания. Группа ресурсов Hello задается пользователем hello во время hello развертывания. Мы затем индекс в этот объект JSON с `.location` tooget hello, откуда hello объекта JSON.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>Определение свойств виртуальной сети
Каждый диспетчер ресурсов ресурс имеет свой собственный `properties` раздела для ресурса toohello определенных конфигураций. В этом случае мы указываем hello виртуальной сети должен иметь одну подсеть hello диапазон частных IP-адресов с помощью `10.0.0.0/16`. Масштабируемый набор всегда содержится в одной подсети. Он не может охватывать подсети.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>Добавление списка зависимостей (dependsOn)
В дополнение к этому требуется toohello `type`, `name`, `apiVersion`, и `location` свойства каждого ресурса может иметь дополнительный `dependsOn` список строк. Этот список определяет, какие еще ресурсы из текущего развертывания необходимо создать перед развертыванием этого ресурса.

В этом случае есть только один элемент в списке hello hello виртуальной сети из предыдущего примера hello. Мы указать эту зависимость, поскольку hello в наборе потребностей сети tooexist hello перед созданием все виртуальные машины. Таким образом, набор масштабирования hello можно предоставить эти виртуальные машины частных IP-адресов из диапазона IP-адресов hello, указанные в свойствах сети hello. Каждая строка в списке dependsOn hello Hello формат `<type>/<name>`. Используйте hello же `type` и `name` ранее используется в определении ресурса hello виртуальной сети.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>Определение свойств масштабируемого набора
Наборы масштабирования имеют множество свойств для настройки виртуальных машин hello в наборе масштабирования hello. Полный список этих свойств см. в разделе hello [в наборе документации по REST API](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set). В этом руководстве мы определим лишь несколько наиболее распространенных свойств.
### <a name="supply-vm-size-and-capacity"></a>Определение размера и емкости виртуальных машин
tooknow потребности набора масштабирования Hello, выберите размер виртуальной Машины toocreate («имя sku») и сколько таких виртуальных машин toocreate («объем sku»). toosee какие размеры виртуальных Машин доступны в разделе hello [размеры виртуальных Машин документации](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>Выбор типа обновления
набор масштабирования Hello также должен tooknow способ toohandle обновления в наборе масштабирования hello. Сейчас поддерживаются два варианта: `Manual` и `Automatic`. Дополнительные сведения о hello различия между двумя hello документации hello на [tooupgrade шкалу настроек](./virtual-machine-scale-sets-upgrade-scale-set.md).

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>Выбор операционной системы для виртуальных машин
Hello набора масштабирования tooknow потребностей какие tooput операционной системы на виртуальных машинах hello. Здесь мы создать виртуальные машины hello с полностью обновленного образа 16.04 LTS Ubuntu.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>Определение префикса имени компьютера (computerNamePrefix)
набор масштабирования Hello развертывает несколько виртуальных машин. Мы не будем указывать имя отдельно для каждой из них, а просто укажем префикс `computerNamePrefix`. Hello набор масштабирования добавляет префикс toohello индекс для каждой виртуальной Машины, имена виртуальных Машин имеют форму hello `<computerNamePrefix>_<auto-generated-index>`.

В следующий фрагмент кода hello мы используем hello параметров из перед tooset hello администратора, имя пользователя и пароль для всех виртуальных машин в наборе масштабирования hello. Это делается с hello `parameters` функции шаблона. Эта функция принимает строку, указывающую, какой параметр toorefer tooand выводит hello значение для этого параметра.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>Определение конфигурации сети для виртуальных машин
Наконец мы должны toospecify hello сетевая конфигурация для виртуальных машин hello в наборе масштабирования hello. В этом случае нам требуется только идентификатор hello toospecify подсети hello, созданного ранее. Это значение определяет масштаб hello набора tooput hello сетевых интерфейсов в этой подсети.

Можно получить идентификатор hello hello виртуальной сети, содержащего hello подсети с помощью hello `resourceId` функции шаблона. Эта функция принимает hello тип и имя ресурса и возвращает hello полный идентификатор этого ресурса. Этот идентификатор имеет форму hello.`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

Однако идентификатор hello hello виртуальной сети недостаточно. Необходимо указать, hello масштабный набор виртуальных машин должны находиться в определенной подсети hello. toodo этого объединения `/subnets/mySubnet` toohello идентификатор hello виртуальной сети. результат Hello — идентификатор hello полное hello подсети. Сделать это объединение с hello `concat` функции, которая принимает набор строк и возвращает их объединения.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
