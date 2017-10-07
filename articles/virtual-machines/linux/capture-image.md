---
title: "образ виртуальной Машины Linux в Azure с помощью CLI 2.0 aaaCapture | Документы Microsoft"
description: "Запись образа виртуальной Машины Azure toouse массы развертываний с помощью Azure CLI 2.0 hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>Как toocreate образ виртуальной машины или виртуального жесткого диска

<!-- generalize, image - extended version of hello tutorial-->

toocreate несколько копий виртуальной машины (VM) toouse в Azure, запись образа виртуальной Машины hello или hello виртуального жесткого диска операционной системы. toocreate изображения, необходимо удалить сведения личную учетную запись, что делает более безопасным toodeploy несколько раз. В следующие шаги hello отзыв существующей виртуальной Машины, deallocate и создания образа. Можно использовать этот образ toocreate виртуальных машин, в любую группу ресурсов в подписке.

Если требуется toocreate копию существующей ВМ Linux для резервного копирования или отладки, или отправить специализированные Linux VHD из локальной виртуальной Машины, см. раздел [отправить и создавать из пользовательского образа виртуальной Машины Linux](upload-vhd.md).  

Можно также использовать **Packer** toocreate вашей пользовательской конфигурации. Дополнительные сведения об использовании Packer см. в разделе [как виртуальная машина Linux toocreate toouse Packer образы в Azure](build-image-with-packer.md).


## <a name="before-you-begin"></a>Перед началом работы
Убедитесь, что выполнены следующие предварительные требования hello:

* Необходимо создать в модели развертывания диспетчера ресурсов hello, с помощью управляемых дисков виртуальной Машины Azure. Если вы еще не создали ВМ Linux, можно использовать hello [портала](quick-create-portal.md), hello [Azure CLI](quick-create-cli.md), или [шаблоны диспетчера ресурсов](create-ssh-secured-vm-from-template.md). Настройка виртуальной Машины, при необходимости hello. Например, [добавьте диски данных](add-disk.md), примените обновления и установите приложения. 

* Необходимо также toohave hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установки и входят в систему по учетной записи Azure tooan [входа az](/cli/azure/#login).

## <a name="quick-commands"></a>Быстрые команды

Упрощенную версию этого раздела, для тестирования, оценки или сведения о виртуальных машинах в Azure, см. [создать образ виртуальной машины Azure с помощью hello CLI](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>Шаг 1: Отзыв виртуальной Машины hello
В случае отмены провизионирования hello виртуальной Машины, используя агент ВМ Azure hello, toodelete машины определенные файлы и данные. Используйте hello `waagent` с hello *-deprovision + пользователь* параметра в вашей исходной виртуальной Машины Linux. Дополнительные сведения см. в разделе hello [руководство пользователя Azure Linux Agent](../windows/agent-user-guide.md).

1. Подключите tooyour виртуальных Машин Linux с помощью SSH-клиента.
2. В окне приветствия SSH введите hello следующую команду:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Только выполните команду на виртуальной Машине, следует присвоить toocapture как изображение. Он не гарантирует этот образ hello подходит для распространения или удаляется все конфиденциальные данные. Hello *+ пользователь* параметра также приведет к удалению hello последняя подготовленного пользователя учетной записи. Учетные данные учетной записи tookeep в hello виртуальных Машин, просто используйте *-deprovision* tooleave hello учетной записи пользователя на месте.
 
3. Тип **y** toocontinue. Можно добавить hello **-принудительно** tooavoid параметр этого шага подтверждения.
4. После выполнения команды hello введите **выхода**. Этот шаг закрывает клиент SSH hello.

## <a name="step-2-create-vm-image"></a>Шаг 2. Создайте образ виртуальной машины
Служит обобщенный hello toomark hello Azure CLI 2.0 ВМ и образа hello. В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.

1. DEALLOCATE hello виртуальной Машине, которая удалена с [ВМ az deallocate](/cli//azure/vm#deallocate). Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. Пометить hello виртуальной Машины как универсализации с [ВМ az generalize](/cli//azure/vm#generalize). Следующий пример метки hello hello виртуальной Машины с именем Hello *myVM* в группе ресурсов hello с именем *myResourceGroup* как обобщенный:
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Теперь создайте образ hello ресурса виртуальной Машины с [создать образ az](/cli//azure/image#create). Hello следующий пример создает образ с именем *myImage* в группе ресурсов hello с именем *myResourceGroup* с помощью hello ВМ ресурс с именем *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Hello образу в hello же группе ресурсов, что к исходной виртуальной Машины. Виртуальную машину из этого образа можно создать в любой группе ресурсов в рамках вашей подписки. С точки зрения управления вы можете toocreate определенной группы ресурсов для виртуальной Машины ресурсов и изображений.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Шаг 3: Создание виртуальной Машины из образа захвачен hello
Создайте виртуальную Машину с помощью образа hello, созданные с помощью [создания виртуальной машины az](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем *myVMDeployed* из образа hello с именем *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Создание виртуальной Машины hello в другой группе ресурсов 

Вы можете создавать виртуальные машины из образа в любой группе ресурсов в рамках своей подписки. toocreate виртуальной Машины в другой группе ресурсов чем изображение hello укажите hello полный идентификатор tooyour изображение ресурса. Используйте [списка изображений az](/cli/azure/image#list) tooview список образов. Hello вывода будет примерно toohello следующий пример:

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Hello следующий пример использует [создания виртуальной машины az](/cli/azure/vm#create) toocreate виртуальной Машины в группе ресурсов, отличной от исходного образа hello, указав идентификатор ресурса изображения hello:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Шаг 4: Проверка развертывания hello

Теперь SSH toohello виртуальной машины вы создали tooverify hello развертывания и запуска с помощью hello новой виртуальной Машины. tooconnect через SSH, найти hello IP-адрес или полное доменное имя вашей виртуальной машины с [Показать ВМ az](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Дальнейшие действия
Вы можете создать несколько виртуальных машин из исходного образа виртуальной машины. Если требуется, чтобы изображение tooyour toomake изменения: 

- Создайте виртуальную машину из образа.
- Выполните желаемые обновления или изменения конфигурации.
- Выполните hello снова toodeprovision, deallocate, обобщения, а также создания образа.
- Используйте этот новый образ для будущих развертываний. При необходимости удалите hello исходного изображения.

Дополнительные сведения об управлении виртуальных машин с hello CLI см. в разделе [Azure CLI 2.0](/cli/azure/overview).
