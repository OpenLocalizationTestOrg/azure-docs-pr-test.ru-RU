---
title: "копия виртуальной Машины Linux с hello Azure CLI 1.0 aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate копию виртуальной машины с Azure Linux hello Azure CLI 1.0 в модели развертывания диспетчера ресурсов hello"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Создать копию виртуальной машины Linux, работающих в Azure с hello Azure CLI 1.0
В этой статье показано, как toocreate копию вашей виртуальной машины (VM) Azure запущенным Linux с помощью hello модели развертывания диспетчера ресурсов. Сначала копирования hello операционной системы и дисков tooa новый контейнер данных, а затем настроить ресурсы сети hello и создание новой виртуальной машины hello.

Кроме того, можно [передать пользовательский образ диска и создать виртуальную машину на его основе](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- Azure CLI 1.0 — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="before-you-begin"></a>Перед началом работы
Убедитесь, что выполнены следующие предварительные требования перед выполнением действий hello hello:

* У вас есть hello [Azure CLI](../../cli-install-nodejs.md) загружается и устанавливается на компьютере. 
* Необходимы также некоторые сведения о существующей виртуальной машине Linux в Azure.

| Сведения об исходной виртуальной машине | Где tooget его |
| --- | --- |
| имя виртуальной машины; |`azure vm list` |
| Имя группы ресурсов |`azure vm list` |
| Расположение |`azure vm list` |
| Имя учетной записи хранения |`azure storage account list -g <resourceGroup>` |
| Имя контейнера |`azure storage container list -a <sourcestorageaccountname>` |
| Имя исходного VHD-файла виртуальной машины |`azure storage blob list --container <containerName>` |

* О новой виртуальной Машины потребуется toomake некоторые варианты:   <br> - имя контейнера;    <br> - имя виртуальной машины;    <br> - размер виртуальной машины;    <br> - имя виртуальной сети;    <br> - имя подсети;    <br> - имя IP-адреса;    <br> - имя сетевой карты.

## <a name="login-and-set-your-subscription"></a>Вход и задание подписки
1. Toohello входа CLI.

    ```azurecli
    azure login
    ```
2. Убедитесь, что режим Resource Manager включен.

    ```azurecli
    azure config mode arm
    ```
3. Задать hello нужной подписки. Можно использовать «учетная запись azure список» toosee всех подписок.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Остановить hello виртуальной Машины
Остановка и освобождать hello исходной виртуальной Машины. «Список виртуальных машин azure» tooget список всех hello виртуальных машин можно использовать в вашей подписке и их имена групп ресурсов.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Скопируйте hello виртуального жесткого диска
Hello виртуального жесткого диска можно скопировать из хранилища toohello hello источник назначения с помощью hello `azure storage blob copy start`. В этом примере мы будем toocopy hello VHD toohello учетную запись хранения, но другой контейнер.

контейнер tooanother toocopy hello VHD в hello учетную запись хранения, введите:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>Настроить виртуальную сеть hello для новой виртуальной Машины
Настройте виртуальную сеть и сетевую карту для новой виртуальной машины. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>Создание новой виртуальной Машины hello
Теперь можно создать виртуальную Машину из виртуального диска [с помощью шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) или через hello CLI, указав hello URI tooyour копирования дисков, введя:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Дальнейшие действия
toolearn как toomanage Azure CLI toouse новой виртуальной машины в разделе [команды Azure CLI для диспетчера ресурсов Azure hello](../azure-cli-arm-commands.md).

