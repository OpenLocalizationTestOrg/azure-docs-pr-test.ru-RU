---
title: "способы aaaDifferent toocreate виртуальной Машины Linux в Azure | Microsoft Azure"
description: "Дополнительные сведения различными способами hello toocreate виртуальной машины Linux в Azure, включая tootools ссылки и учебники для каждого метода."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>Различные способы toocreate ВМ Linux
У вас hello гибкость в Azure toocreate Linux виртуальной машины (VM) с помощью средства и рабочие процессы научились tooyou. В этой статье приведены эти различия и примеры для создания виртуальных машин Linux, включая hello Azure CLI 2.0. Вы также можете просмотреть варианты создания, включая hello [Azure CLI 1.0](creation-choices-nodejs.md).

Hello [Azure CLI 2.0](/cli/azure/install-az-cli2) доступна на платформах через пакета npm, предоставляемых системой дистрибутив пакеты или контейнер Docker. Установите сборку наиболее подходящий hello для вашей среды и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login)

* [Создайте виртуальную Машину Linux с hello Azure CLI 2.0](quick-create-cli.md)
  
  * С помощью команды [az group create](/cli/azure/group#create) создайте группу ресурсов с именем *myResourceGroup*. 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * Создайте виртуальную Машину с [создания виртуальной машины az](/cli/azure/vm#create) с именем *myVM* с помощью последней hello *UbuntuLTS* образ и создать ключи SSH, если они еще не существуют в *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Создание виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md).
  
  * Hello следующий пример использует [создания развертывания группы az](/cli/azure/group/deployment#create) toocreate виртуальной Машины из шаблона, сохраненного на GitHub:
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Создание виртуальной машины Linux и ее настройка с помощью файла cloud-init](tutorial-automate-vm-deployment.md).

* [Создание приложения с балансировкой нагрузки и высоким уровнем доступности на нескольких виртуальных машинах Linux](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Портал Azure
Hello [портал Azure](https://portal.azure.com) позволяет tooquickly создания виртуальной Машины, так как нет ничего tooinstall в системе. Используйте hello Azure портала toocreate hello виртуальной Машины:

* [Создайте виртуальную Машину Linux с помощью портала Azure hello](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>Операционная система и варианты образов
При создании виртуальной Машины, вы выбираете изображение, зависящее от операционной системы требуется toorun hello. Azure и партнеры предлагают множество образов, некоторые из которых содержат предустановленные приложения и средства. Или передать один из собственных образов (см. [hello следующий раздел](#use-your-own-image)).

### <a name="azure-images"></a>Образы Azure
Используйте hello [образа виртуальной машины az](/cli/azure/vm/image) команды toosee, доступные по издателям, дистрибутив версии и сборки.

Отображение списка доступных издателей:

```azurecli
az vm image list-publishers --location eastus
```

Отображение списка доступных продуктов (предложений) нужного издателя:

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

Отображение списка доступных номеров SKU (для дистрибутивов) требуемого предложения:

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

Отображение списка всех доступных образов для определенного выпуска:

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

Дополнительные примеры на просмотр и использование доступных образов см. в разделе [перехода, а затем выберите образы виртуальных машин Azure с hello Azure CLI](cli-ps-findimage.md).

Hello [создания виртуальной машины az](/cli/azure/vm#create) команда имеет tooquickly доступа можно использовать псевдонимы hello чаще дистрибутивы и их последние версии. С помощью псевдонимов часто быстрее, чем указание hello издателя, предложение, SKU и версии каждый раз при создании виртуальной Машины:

| Alias | Издатель | ПРЕДЛОЖЕНИЕ | SKU | Версия |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |CentOS |7,2 |последних |
| CoreOS |CoreOS |CoreOS |Stable |последняя |
| Debian |credativ |Debian |8 |последняя |
| openSUSE |SUSE |openSUSE |13.2 |последних |
| RHEL |Redhat |RHEL |7,2 |последних |
| SLES |SLES |SLES |12-SP1 |последних |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |последних |

### <a name="use-your-own-image"></a>Использование своего образа
Если вам требуются особые настройки, используйте образ на основе имеющейся виртуальной машины Azure. Для этого запишите образ такой виртуальной машины. Вы также можете отправить собственный образ, созданный на локальном диске. Дополнительные сведения о поддерживаемых дистрибутивах и toouse собственные образы. в статье hello следующие статьи:

* [Linux on Azure-Endorsed Distributions (Linux на дистрибутивах, рекомендованных для Azure)](endorsed-distros.md)
* [Information for Non-Endorsed Distributions (Информация о нерекомендованных дистрибутивах)](create-upload-generic.md)
* [Как toocreate изображение из существующей виртуальной Машине Azure](tutorial-custom-images.md).
  
  * Пример: быстрый запуск команды toocreate образ с существующей виртуальной Машине Azure:
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>Дальнейшие действия
* Создайте виртуальную Машину Linux с hello [CLI](quick-create-cli.md), из hello [портала](quick-create-portal.md), или с помощью [шаблона Azure Resource Manager](../windows/cli-deploy-templates.md).
* После создания виртуальной машины Linux [прочтите статью о дисках и хранилище Azure](tutorial-manage-disks.md).
* Быстрое шаги слишком[сбросить пароль или SSH-ключи пользователей и управление ими](using-vmaccess-extension.md).
