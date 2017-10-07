---
title: "aaaCreate пользовательских образов виртуальной Машины с hello Azure CLI | Документы Microsoft"
description: "Учебник - создать образ виртуальной Машины с помощью hello Azure CLI."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Создать образ виртуальной машины Azure с помощью hello CLI

Пользовательские образы похожи на образы магазина, однако их можно создавать самостоятельно. Пользовательские изображения может быть конфигурации используется toobootstrap, такие как предварительной загрузки приложений, конфигурации приложений и других настроек операционной системы. В рамках этого руководства вы создадите собственный пользовательский образ виртуальной машины Azure. Вы узнаете, как выполнять такие задачи.

> [!div class="checklist"]
> * отменить подготовку виртуальных машин и подготовить их к использованию;
> * создавать пользовательский образ;
> * Создание виртуальной машины из пользовательского образа
> * Отображение списка всех образов hello в подписке
> * удалять образ.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Перед началом работы

в следующих шагах Hello подробно, как tootake существующей виртуальной Машины и включите его в доступных для использования пользовательского образа, который можно использовать toocreate новые экземпляры виртуальной Машины.

Пример hello toocomplete в этом учебнике, необходимо иметь существующую виртуальную машину. Этот [пример сценария](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) позволяет создать ее при необходимости. Если заменить прохождение учебника hello группы ресурсов hello и ВМ имен при необходимости.

## <a name="create-a-custom-image"></a>создавать пользовательский образ;

toocreate образ виртуальной машины, необходимо tooprepare hello виртуальной Машины путем отмены подготовки, освобождение и пометки hello исходной виртуальной Машины, как обобщенный. Один раз при hello, который был подготовлен виртуальной Машины, можно создать образ.

### <a name="deprovision-hello-vm"></a>Hello отзыв виртуальной Машины 

Отзыв обобщает hello виртуальных Машин, удалив сведения о компьютере. Из этого общего правила делает возможных toodeploy много виртуальных машин из одного образа. Во время отмены подготовки, имя узла hello сбрасывается слишком*localhost.localdomain*. Ключи узла SSH, конфигурации сервера доменных имен, пароль учетной записи root и кэшированные аренды DHCP также удаляются.

hello toodeprovision виртуальной Машины, с помощью агента ВМ Azure hello (waagent). агент ВМ Azure Hello устанавливается на hello виртуальной Машины и управляет подготовки и работать с ними hello Azure Fabric Controller. Дополнительные сведения см. в разделе hello [руководство пользователя Azure Linux Agent](agent-user-guide.md).

Подключение tooyour виртуальной Машины с помощью SSH и выполнения hello команда toodeprovision hello виртуальной Машины. С hello `+user` аргумента, hello последнюю подготовленный пользователь учетную запись и все связанные с ними данные удаляются. Замените IP-адрес hello пример hello общедоступный IP-адрес виртуальной Машины.

Toohello SSH виртуальной Машины.
```bash
ssh azureuser@52.174.34.95
```
Здравствуйте, отзыв виртуальной Машины.

```bash
sudo waagent -deprovision+user -force
```
Закрыть сеанс SSH hello.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Выделение и пометить hello виртуальной Машины как обобщенный

toocreate изображения hello виртуальной Машины должен toobe освобождена. DEALLOCATE hello виртуальной Машины с помощью [ВМ az deallocate](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Задайте состояние hello hello виртуальной Машины как универсализации с [ВМ az generalize](/cli//azure/vm#generalize) чтобы hello ВМ обобщенный знал hello платформы Azure. Создать образ можно только из подготовленной виртуальной машины.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Создание образа hello

Теперь можно создавать с помощью образа виртуальной Машины hello [создать образ az](/cli//azure/image#create). Hello следующий пример создает образ с именем *myImage* из виртуальной Машины с именем *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Создать виртуальные машины из образа hello

Теперь, когда у вас есть образ, можно создать один или несколько новых виртуальных машин из hello изображения с помощью [создания виртуальной машины az](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем *myVMfromImage* из образа hello с именем *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Управление образами 

Ниже приведены некоторые примеры типичных задач управления изображения и как toocomplete их с помощью hello Azure CLI.

Получение списка всех образов по имени в формате таблицы.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Удаление образа. Этот пример удаляет hello изображение с именем *myOldImage* из hello *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

В рамках этого руководства вы создали пользовательский образ виртуальной машины. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * отменять подготовку виртуальных машин и подготавливать их к использованию;
> * создавать пользовательский образ;
> * Создание виртуальной машины из пользовательского образа
> * Отображение списка всех образов hello в подписке
> * удалять образ.

Переместить следующий учебник toolearn toohello о виртуальных машин высокой надежности.

> [!div class="nextstepaction"]
> [Создание высокодоступных виртуальных машин](tutorial-availability-sets.md)

