---
title: "образ виртуальной Машины Linux aaaCapture | Документы Microsoft"
description: "Узнайте, как toocapture под управлением Linux Azure виртуальной машины (VM) создан образ с hello классической модели развертывания."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>Как toocapture классической виртуальной машины Linux как изображение
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

В этой статье показано, как toocapture классической виртуальной машине Azure (ВМ) других виртуальных машин под управлением Linux как toocreate изображения. Этот образ содержит hello диска ОС и дисков данных присоединяется toohello виртуальной Машины. Она не включает сетевую конфигурацию, поэтому требуется tooconfigure, при создании hello другой виртуальной Машины из образа hello.

Хранилища Azure hello образа в разделе **изображения**, вместе с отправленное изображений. Дополнительные сведения об образах см. в статье [Об образах виртуальных машин Linux][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Перед началом работы
Предполагается, что ВМ Azure с помощью hello классической модели развертывания и настроенный hello операционной системы, включая присоединение диски с данными, уже создана. Если вам требуется toocreate виртуальной Машины, чтение [как tooCreate виртуальной машины Linux][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Запись hello виртуальной машины
1. [Подключение виртуальной Машины toohello](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) с помощью такой клиент SSH, по своему усмотрению.
2. В окне приветствия SSH введите следующую команду hello. Вывод Hello `waagent` может несколько отличаться в зависимости от версии hello этой служебной программы:

    ```bash
    sudo waagent -deprovision+user
    ```

    Hello предыдущая команда пытается tooclean hello системы и соответствующих инициализацию. Эта операция не выполняет hello следующие задачи:

   * Удаляет ключи SSH узла (если Provisioning.RegenerateSshHostKeyPair «y» в файле конфигурации hello)
   * очищается конфигурация имени сервера в /etc/resolv.conf;
   * Удаляет hello `root` пароль пользователя с/etc/тени (если Provisioning.DeleteRootPassword «y» в файле конфигурации hello)
   * удаляются кэшированные аренды DHCP-клиентов.
   * Сброс размещения toolocalhost.localdomain имя
   * Удаляет hello последнего подготовленных учетную запись пользователя (полученные от /var/lib/waagent) **и связанные данные**.

     > [!NOTE]
     > Отзыв удаляет файлы и данные слишком «generalize» hello изображения. Только выполните команду на виртуальной Машине, следует присвоить toocapture как шаблон для нового образа. Он не гарантирует этот образ hello подходит для распространения toothird сторон или удаляется все конфиденциальные данные.

3. Тип **y** toocontinue. Можно добавить hello `-force` tooavoid параметр этого шага подтверждения.
4. Тип **выхода** tooclose hello SSH-клиента.

   > [!NOTE]
   > Hello оставшихся шагах предполагается уже имеется [установлен hello Azure CLI](../../../cli-install-nodejs.md) на клиентском компьютере. Все hello действий может быть также выполнена в hello [портал Azure](http://portal.azure.com).

5. С клиентского компьютера откройте Azure CLI и tooyour входа подписки Azure. Дополнительные сведения и статье [подключение tooan подписки Azure из hello Azure CLI](../../../xplat-cli-connect.md).

   > [!NOTE]
   > В hello портал Azure войдите в портал toohello.

6. Убедитесь, что вы находитесь в режиме управления службами:

    ```azurecli
    azure config mode asm
    ```

7. Завершите работу виртуальной Машины, которая уже удалена hello. Hello следующий пример завершает работу виртуальной Машины с именем hello `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   При необходимости можно просмотреть список всех hello виртуальные машины создаются в подписке с помощью`azure vm list`

   > [!NOTE]
   > Если вы используете hello портал Azure, выберите hello виртуальной Машины и нажмите кнопку **остановить** завершение работы виртуальной Машины hello.

8. При остановке hello ВМ образа hello. Следующий пример получает Hello hello виртуальной Машины с именем `myVM` и создает обобщенный образ с именем `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Hello `-t` подкоманда удалений hello исходной виртуальной машины.

    > [!NOTE]
    > В hello портал Azure, можно записать образ, выбрав **изображения** меню hello концентратора. Требуется toosupply hello следующую информацию для образа hello: имя группы ресурсов, расположение, тип операционной системы и путь к хранилищу больших двоичных объектов.

9. Hello новый образ будет теперь доступны в списке изображений, которые могут быть hello используются tooconfigure любой новой виртуальной Машины. Вы можете просмотреть с помощью команды hello:

   ```azurecli
   azure vm image list
   ```

   На hello [портал Azure](http://portal.azure.com), hello новое изображение отображается в hello **образов виртуальных Машин (классические)** , принадлежит toohello **вычислений** служб. Вы можете получить доступ к **образов виртуальных Машин (классические)** , щелкнув _дополнительные службы_ внизу hello hello Azure службы списка и затем проверив hello **вычислений** служб.   

   ![Успешная запись образа](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Дальнейшие действия
изображение Hello является toocreate готовности toobe использовать виртуальные машины. Можно использовать команду hello Azure CLI `azure vm create` и вы создали имя образа hello питания. Дополнительные сведения см. в разделе [использование hello Azure CLI классической модели развертывания](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

Можно также использовать hello [портал Azure](http://portal.azure.com) toocreate пользовательских виртуальных Машин с помощью hello **изображения** метод и выбрав hello образ был создан. Дополнительные сведения см. в разделе [как tooCreate специальной виртуальной Машины][How tooCreate a Custom Virtual Machine].

**См. также:** [Руководство пользователя агента Linux для Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
