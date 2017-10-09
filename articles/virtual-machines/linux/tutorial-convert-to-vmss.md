---
title: "набор масштабирования виртуальной Машины Azure tooa aaaConvert | Документы Microsoft"
description: "Создание и развертывание с hello Azure CLI масштабирования виртуальных машин Linux Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a>Преобразовать существующий набор масштабирования виртуальной машины Azure tooa

Этот учебник показывает, как tooconvert toouse Azure CLI 2.0 tooa виртуальной машины набора масштабирования виртуальных машин. Вы также узнаете, как задать конфигурации hello tooautomate hello виртуальных машин на шкале hello. Дополнительные сведения о том, как tooinstall Azure CLI версии 2.0, см. [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md). Дополнительные сведения о наборах масштабирования см. в разделе [Наборы масштабирования виртуальных машин](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).

## <a name="step-1---deprovision-hello-vm"></a>Шаг 1 hello отзыв виртуальной Машины.

С помощью SSH tooconnect toohello виртуальной Машины.

Hello отзыв виртуальной Машины с помощью файлов toodelete агента ВМ Azure hello и данных. Подробный обзор отзыва представлен в разделе [Запись образа виртуальной машины Linux](capture-image.md).

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a>Шаг 2 - запись образа виртуальной Машины hello

Подробный обзор записи представлен в разделе [Запись образа виртуальной машины Linux](capture-image.md).

DEALLOCATE hello виртуальной Машины с [ВМ az deallocate](/cli/azure/vm#deallocate):

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Обобщить hello виртуальной Машины с [ВМ az generalize](/cli/azure/vm#generalize):

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

Создать образ на hello ресурса виртуальной Машины с [создать образ az](/cli/azure/image#create):

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a>Шаг 3 — Создание набора масштабирования hello

Получить hello **идентификатор** hello изображения.

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

Создайте виртуальную машину из ресурса образа с помощью команды [az vmss create](/cli/azure/vmss#create).

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

Эта команда также подключает диск данных емкостью в 10 ГБ. Имейте в виду, что в зависимости от hello виртуальной Машины выбранного размера (мы использовали **Standard_DS1_v2**), количество дисков данных, допустимых в hello отличается. Дополнительные сведения см. в статье hello [размеры виртуальных машин](sizes.md).

После завершения набора масштабирования hello, connect tooit. Получить список IP-адресов для hello экземпляров для SSH с [списка vmss az-экземпляр соединения info](/cli/azure/vmss#list-instance-connection-info):

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

Теперь можно подключить диск данных hello tooinitialize экземпляр toohello виртуальной машины

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a>Шаг 4. инициализация диска данных hello

При подключенном toohello виртуальной машины, создать разделы на диске hello с `fdisk`:

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

Запись toohello разделе с файловой системой hello `mkfs` команды:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Подключите новый диск hello, чтобы она доступна в операционной системе hello:

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

Hello диск теперь может быть доступ через монтирования datadrive hello, который может быть проверена с помощью `ls /datadrive/`.

Завершение сеанса SSH hello.


## <a name="step-5---configure-firewall"></a>Шаг 5. Настройка брандмауэра

Дырокол бреши hello брандмауэра toohello webserver размещенных набором масштабирования hello. Когда был создан набор масштабирования hello, также было создано подсистемы балансировки нагрузки и он был использован **SSH** toohello отдельных виртуальных машин. tooopen порт требуется два блока данных, который можно получить с помощью Azure CLI.

* **Интерфейсный пул IP-адресов**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* **Внутренний пул IP-адресов**  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

С помощью этих двух имен можно открыть порт **80**.

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a>Шаг 6. Автоматизация настройки

диск данных Hello должен toobe, настроенный на каждый экземпляр виртуальной машины. Мы можете автоматизировать настройку hello hello виртуальную машину с hello **CustomScript** расширения.

Сначала создайте *.sh* скрипт, который содержит команды форматирования диска hello.

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

Затем отправка, hello toowhere файла сценария **CustomScript** доступ к нему расширение. Копия доступна [здесь](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).

Создание локального файла с именем **settings.json** и put hello после блока JSON в нем. Hello `flieUris` toowhere, отправленный в файле сценария необходимо задать для свойства.

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

Развертывание этой команды tooyour набор масштабирования с hello **CustomScript** расширения, ссылающиеся на hello **settings.json** только что созданный файл.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

Это расширение автоматически запускается на всех текущих экземплярах и экземплярах, который будут созданы позже при масштабировании.

## <a name="step-7---configure-autoscale-rules"></a>Шаг 7. Настройка правил автомасштабирования

В настоящее время с помощью Azure CLI нельзя задать правила автомасштабирования. Используйте hello [портал Azure](https://portal.azure.com) tooconfigure автомасштабирования.

## <a name="step-8---management-tasks"></a>Шаг 8. Задачи управления

На протяжении жизненного цикла hello набора масштабирования hello, может потребоваться toorun одну или несколько задач управления. Кроме того вы можете toocreate скрипты, автоматизирующие различные жизненного цикла задачи и hello Azure CLI предоставляет toodo быстро этих задач. Ниже приведено несколько распространенных задач.

### <a name="get-connection-info"></a>Получение сведений о подключении

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a>Задание числа экземпляров (ручное масштабирование)

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a>Удалить группу ресурсов

При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия
см. Дополнительные сведения о некоторых масштабирования виртуальных машин hello набор возможностей, представленных в этом учебнике toolearn hello следующую информацию:

- [Общие сведения о масштабируемых наборах виртуальных машин в Azure](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [Обзор Azure Load Balancer](../../load-balancer/load-balancer-overview.md)
- [Управление потоком сетевого трафика с помощью групп безопасности сети](../../virtual-network/virtual-networks-nsg.md)