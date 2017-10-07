---
title: "aaaUse a Linux, устранение неполадок виртуальной Машины с hello Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как tootroubleshoot ВМ Linux проблемы при подключении hello ОС диска tooa восстановления виртуальной Машины с помощью hello Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a>Устранение неполадок виртуальной Машины Linux путем присоединения диска hello ОС tooa восстановления виртуальной Машины с hello Azure CLI 2.0
Если Linux виртуальной машины (VM), возникает ошибка загрузки или диск, может потребоваться tooperform действия на виртуальном жестком диске hello сам по устранению неполадок. Распространенным примером будет недопустимую запись в `/etc/fstab` , предотвращает hello виртуальной Машины может tooboot успешно. Этой статьи описаны как toouse hello Azure CLI 2.0 tooconnect вашего виртуального жесткого диска tooanother toofix ВМ Linux все ошибки, а затем повторного создания исходной виртуальной Машины. Можно также выполнить следующие действия с hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="recovery-process-overview"></a>Обзор процесса восстановления
Поиск и устранение неполадок Hello выглядит следующим образом:

1. Удалите hello ВМ возникновения проблемы, поддержание hello виртуальных жестких дисков.
2. Присоедините и подключите tooanother hello виртуальный жесткий диск виртуальной Машины с Linux для устранения неполадок.
3. Подключите toohello Устранение неполадок виртуальной Машины. Изменение файлов или выполните любые средства toofix проблемы на hello исходный виртуальный жесткий диск.
4. Отключите образ и отсоединить виртуальный жесткий диск hello из hello, устранение неполадок виртуальной Машины.
5. Создайте виртуальную Машину с помощью hello исходный виртуальный жесткий диск.

tooperform следующие шаги, hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

В hello следующих примерах замените имена параметров собственные значения. Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.


## <a name="determine-boot-issues"></a>Выявление проблем при загрузке
Изучите toodetermine последовательного вывода hello, почему ВМ не могут tooboot правильно. Распространенным примером является недопустимой записью в `/etc/fstab`, или hello базового виртуального жесткого диска, удален или перемещен.

Получить журналы загрузки hello с [az ВМ Диагностика загрузки get загрузки журнал-](/cli/azure/vm/boot-diagnostics#get-boot-log). Hello следующий пример получает hello последовательного выходные данные из виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

Просмотрите почему hello виртуальной Машины происходит сбой tooboot toodetermine последовательного вывода hello. Если последовательного вывода hello не предоставляет сведения о том, может потребоваться tooreview файлы журналов в `/var/log` после hello виртуального жесткого диска, подключенного tooa Устранение неполадок виртуальной Машины.


## <a name="view-existing-virtual-hard-disk-details"></a>Просмотр сведений для существующего виртуального жесткого диска
Перед тем как присоединить tooanother вашего виртуального жесткого диска (VHD) виртуальной Машины, необходимо tooidentify hello URI hello диска операционной системы. 

Просмотрите сведения о виртуальной машине с помощью команды [az vm show](/cli/azure/vm#show). Используйте hello `--query` флаг tooextract hello URI toohello ОС диска. Hello следующий пример возвращает сведения о диске для виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

Hello URI аналогичен слишком**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.

## <a name="delete-existing-vm"></a>Удаление существующей виртуальной машины
Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure. Виртуальный жесткий диск является местом hello операционной системы, приложения и конфигурации. Hello самой ВМ — точно так же метаданные, которые определяет hello размер или расположение и ссылки на ресурсы, такие как виртуальный жесткий диск или виртуальный сетевой адаптер (NIC). Каждый виртуальный жесткий диск содержит аренды, назначенный при присоединении tooa виртуальной Машины. Несмотря на то, что диски с данными может быть присоединенные и отсоединенные даже в том случае, когда выполняется hello виртуальной Машины, диска ОС hello отключить невозможно, пока удаляется hello ресурса виртуальной Машины. Аренда Hello продолжается tooassociate hello ОС диска с виртуальной Машиной даже в том случае, если этой виртуальной Машины находится в состоянии остановки и освобождается.

Здравствуйте, первый шаг toorecover ВМ — toodelete hello ВМ сам ресурс. Удаление hello ВМ оставляет hello виртуальных жестких дисков в вашей учетной записи хранилища. После hello удаления виртуальной Машины присоединения hello виртуальный жесткий диск tooanother ВМ tootroubleshoot и устранение ошибок hello.

Удалить hello виртуальной Машины с [удаление виртуальной машины az](/cli/azure/vm#delete). Следующий пример удаляет Hello hello виртуальной Машины с именем `myVM` из группы ресурсов hello с именем `myResourceGroup`:

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

Подождите, пока hello ВМ закончит удаление перед присоединением tooanother hello виртуальный жесткий диск виртуальной Машины. Аренда Hello hello виртуальный жесткий диск, который связывает его с hello виртуальной Машины должен toobe выпуска перед тем как присоединить tooanother hello виртуальный жесткий диск виртуальной Машины.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Подключить существующий виртуальный жесткий диск tooanother виртуальной Машины
Для Здравствуйте рядом шагах, для устранения неполадок используется другой виртуальной Машиной. Подключить существующий виртуальный жесткий диск toothis hello Устранение неполадок виртуальной Машины toobrowse и изменить содержимое диска hello. Этот процесс позволяет toocorrect все ошибки конфигурации или Просмотр дополнительных приложений или файлы журналов, например системы. Выберите или создайте другой toouse виртуальной Машины для устранения неполадок.

Подключить hello существующий виртуальный жесткий диск с [присоединения az диск виртуальной машины неуправляемого-](/cli/azure/vm/unmanaged-disk#attach). При присоединении hello существующий виртуальный жесткий диск, укажите диск toohello hello URI, полученный на предыдущем hello `az vm show` команды. Hello примере присоединяет существующий виртуальный жесткий диск toohello Устранение неполадок виртуальной Машины с именем `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>Подключить hello подключенный диск данных

> [!NOTE]
> Hello следующих примерах приведены шаги на Виртуальной машине Ubuntu hello. Если вы используете другой дистрибутив Linux, например Red Hat Enterprise Linux или SUSE, hello расположения файлов журнала и `mount` команд может немного отличаться. См. в документации toohello для вашего конкретного дистрибутив для hello соответствующие изменения в командах.

1. Устранение неполадок виртуальной Машины, используя соответствующие учетные данные hello tooyour SSH. Если этот диск является tooyour данных диске, подключенном hello для первого Устранение неполадок виртуальной Машины, hello подключен жесткий диск, скорее всего слишком`/dev/sdc`. Используйте `dmseg` tooview присоединенных дисков:

    ```bash
    dmesg | grep SCSI
    ```

    Hello вывода будет примерно toohello следующий пример:

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    В предыдущих пример hello, диск hello ОС находится на `/dev/sda` и hello временного диска, указанное для каждой виртуальной Машины в `/dev/sdb`. Если у вас несколько дисков данных, они будут присоединены как `/dev/sdd`, `/dev/sde` и т. д.

2. Создайте directory toomount существующий виртуальный жесткий диск. Hello следующий пример создает каталог с именем `troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. При наличии нескольких секций на существующий виртуальный жесткий диск, подключите hello необходимые секции. Hello следующий пример подключает первому основному разделу hello в `/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > Лучший способ — что toomount диски с данными на виртуальных машинах в Azure с помощью hello универсальный уникальный идентификатор UUID hello виртуального жесткого диска. В этом сценарии короткий по устранению неполадок монтажного hello виртуального жесткого диска с помощью hello UUID не требуется. Тем не менее, при обычных условиях использования редактирования `/etc/fstab` toomount виртуальных жестких дисков с помощью имени, а не может вызвать UUID hello tooboot toofail виртуальной Машины.


## <a name="fix-issues-on-original-virtual-hard-disk"></a>Устранение неполадок на исходном виртуальном жестком диске
С hello существующий виртуальный жесткий диск подключен теперь можно выполнять обслуживание и действия по устранению неполадок при необходимости. После разрешения проблемы hello продолжите hello следующие шаги.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Отключение и отсоединение исходного виртуального жесткого диска
После разрешения ошибки, можно отключить и отсоединение hello существующий виртуальный жесткий диск от виртуальной Машины по устранению неполадок. Расположение виртуального жесткого диска нельзя использовать с любой другой ВМ до освобождения аренды hello присоединение toohello hello виртуального жесткого диска, устранение неполадок виртуальной Машины.

1. Из сеанса SSH hello tooyour Устранение неполадок виртуальной Машины отключите hello существующий виртуальный жесткий диск. Сначала измените вне hello родительский каталог для точки подключения:

    ```bash
    cd /
    ```

    Теперь отключите hello существующий виртуальный жесткий диск. Hello следующий пример отсоединяет диск hello устройство с `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. Теперь отсоедините hello виртуальный жесткий диск из виртуальной Машины hello. Выйти из сеанса tooyour hello SSH, устранение неполадок виртуальной Машины. Список hello присоединенного tooyour дисков данных, устранение неполадок виртуальной Машины с [списка неуправляемого дисков виртуальной машины az](/cli/azure/vm/unmanaged-disk#list). Hello списки hello диски с данными в примере присоединенного toohello виртуальной Машины с именем `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`:

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    Запишите имя hello для существующего виртуального жесткого диска. Например, диск с именем hello hello URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** — **myVHD**. 

    Отсоединить диск данных hello от ВМ [отсоединения az диск виртуальной машины неуправляемого-](/cli/azure/vm/unmanaged-disk#detach). Hello следующий пример отсоединяет hello диск с именем `myVHD` из виртуальной Машины с именем hello `myVMRecovery` в hello `myResourceGroup` группа ресурсов:

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a>Создание виртуальной машины из исходного жесткого диска
использовать ВМ с исходного виртуального жесткого диска, toocreate [этого шаблона Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd). шаблон фактического JSON Hello находится в hello по ссылке:

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

Hello шаблон развертывания ВМ с помощью hello URI VHD-файла из hello ранее команд. Развертывание шаблона hello с [создания развертывания группы az](/cli/azure/group/deployment#create). Укажите hello URI tooyour исходный виртуальный жесткий ДИСК и затем укажите тип hello ОС, размер виртуальной Машины и имя виртуальной Машины следующим образом:

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a>Восстановление диагностики загрузки
При создании ВМ из hello существующий виртуальный жесткий диск, диагностика загрузки может не быть доступной. Включите диагностику загрузки с помощью команды [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable). Hello следующий пример включает hello диагностического расширения для виртуальной Машины с именем hello `myDeployedVM` в группе ресурсов hello с именем `myResourceGroup`:

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>Дальнейшие действия
Если возникают проблемы с подключением tooyour виртуальной Машины, см. раздел [Устранение SSH подключений tooan виртуальной Машины Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Для решения проблем с доступом к приложениям, выполняющимся на виртуальной машине, см. статью [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
