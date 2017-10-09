---
title: "aaaManage Azure диски с hello Azure CLI | Документы Microsoft"
description: "Учебник - Управление дисками Azure с hello Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a>Управление дисками Azure с hello Azure CLI

Виртуальные машины Azure используют диски toostore hello виртуальные машины операционной системы, приложений и данных. При создании виртуальной Машины это важно toochoose размер диска и рабочей нагрузки соответствующие toohello ожидается конфигурации. В этом руководстве рассматривается развертывание дисков виртуальных машин и управление ими. Здесь содержатся сведения о:

> [!div class="checklist"]
> * дисках ОС и временных дисках;
> * Диски данных
> * дисками уровня "Стандартный" и "Премиум";
> * производительностью дисков;
> * присоединением и подготовкой дисков данных;
> * изменением размеров дисков;
> * моментальными снимками дисков.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="default-azure-disks"></a>Диски Azure по умолчанию

При создании виртуальной машины Azure двух дисков являются toohello автоматически подключенных виртуальных машин. 

**Диск операционной системы** - дисков операционной системы можно изменять, но копирование too1 терабайт и узлы hello операционной системы виртуальных машин. диск ОС Hello помечается */dev/sda* по умолчанию. кэширование конфигурацию диска ОС hello диска Hello оптимизирован для работы операционной системы. Из-за этой конфигурации hello диска ОС **не должны** размещения приложений или данных. Для приложений и данных используйте диски данных, которые описаны далее в этой статье. 

**Временный диск** -временные диски используют твердотельного накопителя, которая находится на hello же Azure узле hello виртуальной Машины. Временные диски обладают высокой производительностью и могут быть использованы для таких операций, как обработка временных данных. Данные, хранящиеся на временный диск удаляется, если hello виртуальной Машины, перемещенные tooa новый узел. размер Hello hello временного диска определяется hello размер виртуальной Машины. Временные диски помечаются как */dev/sdb* и используют точку подключения */mnt*.

### <a name="temporary-disk-sizes"></a>Размеры временных дисков

| Тип | Размер виртуальной машины | Максимальный размер временного диска (ГБ) |
|----|----|----|
| [Универсальные](sizes-general.md) | Серии A и D | 800 |
| [Оптимизированные для вычислений](sizes-compute.md) | Серия F | 800 |
| [Оптимизированные для памяти](../virtual-machines-windows-sizes-memory.md) | Серии D и G | 6144 |
| [Оптимизированные для хранилища](../virtual-machines-windows-sizes-storage.md) | Серия L | 5630 |
| [GPU](sizes-gpu.md) | Серия N | 1440 |
| [Высокопроизводительные](sizes-hpc.md) | Серии A и H | 2000 |

## <a name="azure-data-disks"></a>Диски данных Azure

Вы можете добавить дополнительные диски данных, чтобы установить приложения и хранить данные. Диски данных следует использовать в любой ситуации, где требуется надежное хранилище данных, обеспечивающее высокую скорость реагирования. Максимальная емкость каждого диска данных составляет 1 ТБ. Hello размера виртуальной машины hello определяет число дисков может быть tooa подключенных виртуальных Машин. Для каждого ядра виртуальной машины можно подключить два диска данных. 

### <a name="max-data-disks-per-vm"></a>Максимальное число дисков данных на виртуальную машину

| Тип | Размер виртуальной машины | Максимальное число дисков данных на виртуальную машину |
|----|----|----|
| [Универсальные](sizes-general.md) | Серии A и D | 32 |
| [Оптимизированные для вычислений](sizes-compute.md) | Серия F | 32 |
| [Оптимизированные для памяти](../virtual-machines-windows-sizes-memory.md) | Серии D и G | 64 |
| [Оптимизированные для хранилища](../virtual-machines-windows-sizes-storage.md) | Серия L | 64 |
| [GPU](sizes-gpu.md) | Серия N | 48 |
| [Высокопроизводительные](sizes-hpc.md) | Серии A и H | 32 |

## <a name="vm-disk-types"></a>Типы дисков виртуальной машины

В Azure предоставляются диски двух типов.

### <a name="standard-disk"></a>Диск уровня "Стандартный"

Хранилище класса Standard использует жесткие диски и обеспечивает экономичное хранилище с достаточной производительностью. Эти диски идеально подходят для экономных рабочих нагрузок разработки и тестирования.

### <a name="premium-disk"></a>Диск уровня "Премиум"

Диски уровня "Премиум" используют высокопроизводительные твердотельные накопители с низкой задержкой. Они идеально подходят для виртуальных машин, выполняющих производственную рабочую нагрузку. Хранилище уровня "Премиум" поддерживает виртуальные машины серий DS, DSv2, GS и FS. Диски Premium бывают трех типов (P10 P20, P30), размер диска hello hello определяет тип диска hello. При выборе, следующий тип toohello округляется hello значение размера диска. Например если размер диска hello не превышает 128 ГБ, hello используется диск P10. Если размер диска hello между 129 и 512 ГБ, размер hello — P20. Ничего более 512 ГБ, размер hello — P30.

### <a name="premium-disk-performance"></a>Производительность диска уровня "Премиум"

|Тип диска хранилища уровня "Премиум" | P10 | P20 | P30 |
| --- | --- | --- | --- |
| Размер диска (округленный в большую сторону) | 128 ГБ | 512 ГБ | 1024 ГБ (1 ТБ) |
| Макс. количество операций ввода-вывода в секунду на диск | 500 | 2300 | 5 000 |
Пропускная способность на диск | 100 МБ/с | 150 МБ/с | 200 МБ/с |

Хотя hello над таблицей идентифицирует max IOP для дисков, более высокий уровень производительности достигается путем чередования несколько дисков данных. Например, виртуальная машина Standard_GS5 может достичь 80 000 операций ввода-вывода в секунду. Дополнительные сведения о максимальных количествах операций ввода-вывода в секунду для виртуальных машин см. в разделе [Размеры виртуальных машин Linux](sizes.md).

## <a name="create-and-attach-disks"></a>Создание и подключение дисков

Диски данных можно создать и присоединенного во время создания виртуальной Машины или tooan существующей виртуальной Машины.

### <a name="attach-disk-at-vm-creation"></a>Подключение диска при создании виртуальной машины

Создание группы ресурсов с hello [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) команды. 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

Создайте виртуальную Машину с помощью hello [создания виртуальной машины az]( /cli/azure/vm#create) команды. Hello `--datadisk-sizes-gb` аргумент является используется toospecify, что дополнительный диск должен быть создан и присоединенного toohello виртуальной машины. toocreate и присоединить несколько дисков, используйте несколько значений размера диска. В следующем примере hello виртуальная машина создается с дисками данных, оба 128 ГБ. Поскольку размеры дисков hello 128 ГБ, эти диски настроены как P10s, содержащие максимальное 500 операций ввода-ВЫВОДА на диске.

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a>Присоединить диск tooexisting виртуальной Машины

toocreate и присоединить новый диск tooan существующей виртуальной машины, используйте hello [присоединить диск виртуальной машины az](/cli/azure/vm/disk#attach) команды. Hello следующий пример создает диск с premium 128 гигабайт и привязывает его toohello создания виртуальной Машины на последнем шаге hello.

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a>Подготовка дисков данных

После диск toohello подключенных виртуальных машин, hello операционной системы должен настроить toobe toouse hello диска. Hello в следующем примере показано, как toomanually Настройка диска. Этот процесс можно автоматизировать с помощью cloud-init, как описывается в [этом руководстве](./tutorial-automate-vm-deployment.md).

### <a name="manual-configuration"></a>Настройка вручную

Создайте SSH-подключения с hello виртуальной машины. Замените hello общедоступный IP-адрес виртуальной машины hello hello примере IP-адрес.

```azurecli-interactive 
ssh 52.174.34.95
```

Создать разделы на диске hello с `fdisk`.

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

Запись toohello системного раздела в файл с помощью hello `mkfs` команды.

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Подключите новый диск hello, чтобы она доступна в операционной системе hello.

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

диск Hello, теперь доступны через hello *datadrive* монтирования по умолчанию, который можно проверить, запустив hello `df -h` команды. 

```bash
df -h
```

Hello видно hello новый диск подключается к */datadrive*.

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

tooensure, hello диск будет подключена снова после перезагрузки, его необходимо добавить toohello */etc/fstab* файла. toodo таким образом, получить hello UUID диска hello с hello `blkid` программы.

```bash
sudo -i blkid
```

Вывод Hello отображает hello UUID диска hello `/dev/sdc1` в этом случае.

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

Добавление строки аналогично toohello, следуя toohello */etc/fstab* файла. Также обратите внимание на то, что ограничения записи можно отключить с помощью *barrier=0*. Это может повысить производительность диска. 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

Теперь, когда hello диск был настроен, закройте сеанс SSH hello.

```bash
exit
```

## <a name="resize-vm-disk"></a>Изменение размера диска виртуальной машины

После развертывания виртуальной Машины диск операционной системы hello или все подключенные диски данных можно увеличить размер. Увеличение размера hello диска полезно в том случае, при необходимости использовать больший объем памяти или более высокий уровень производительности (P10, P20, P30). Обратите внимание, что уменьшить размер дисков невозможно.

До увеличения места на диске, Здравствуйте, идентификатор или требуется указать имя диска hello. Используйте hello [список дисков az](/cli/azure/vm/disk#list) команда tooreturn все диски в группе ресурсов. Запишите имя диска hello, желательно tooresize.

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

Hello виртуальной Машины также должен быть освобождена. Используйте hello [ВМ az deallocate]( /cli/azure/vm#deallocate) команды toostop и освобождать hello виртуальной Машины.

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

Используйте hello [обновление диска az](/cli/azure/vm/disk#update) команда tooresize hello диска. Этот пример изменяет размер диска с именем *myDataDisk* too1 терабайт.

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

После завершения операции изменения размера hello, запустите hello виртуальной Машины.

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

Если вы изменили размер hello операционной системы диска, раздел hello автоматически расширяется. Если изменения размера диска данных, все текущие секции должны toobe развернуты в операционной системе hello виртуальных машин.

## <a name="snapshot-azure-disks"></a>Создание моментальных снимков дисков Azure по умолчанию

Создание снимка диск создает чтения только в момент копию hello диска. Моментальные снимки виртуальной Машины Azure можно использовать для быстрого сохранение состояния hello виртуальной машины перед изменением конфигурации. В событии hello hello изменения конфигурации доказать toobe нежелательным, состояние виртуальной Машины можно восстановить с помощью моментального снимка hello. Если виртуальная машина имеет более одного диска, моментальный снимок каждого диска, независимо от hello другим пользователям. Для подсчета согласованных копий приложения, рассмотрите возможность остановки hello виртуальной Машины перед созданием моментальных снимков диска. Можно также использовать hello [службы архивации Azure](/azure/backup/), который позволит вам tooperform автоматическое резервное копирование, при запущенной виртуальной Машине hello.

### <a name="create-snapshot"></a>Создание моментального снимка

Перед созданием моментального снимка виртуальной машины диск, hello идентификатор или имя диска hello необходим. Используйте hello [Показать ВМ az](https://docs.microsoft.com/en-us/cli/azure/vm#show) диска с идентификатором hello tooreturn команды. В этом примере диска с идентификатором hello хранится в переменной, чтобы он может использоваться в дальнейшем.

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

Теперь, когда идентификатор hello диска виртуальной машины hello hello следующая команда создает моментальный снимок hello диска.

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a>Создание диска на основе моментального снимка

Затем этот моментальный снимок может быть преобразован в диск, который можно использовать toorecreate hello виртуальной машины.

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a>Восстановление виртуальной машины на основе моментального снимка

восстановление виртуальных машин toodemonstrate delete hello существующей виртуальной машины. 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

Создайте новую виртуальную машину с диска hello моментального снимка.

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a>Повторное подключение диска данных

Все диски с данными необходимо повторно присоединить toobe toohello виртуальной машины.

Сначала найти имя диска данных hello, с помощью hello [список дисков az](https://docs.microsoft.com/cli/azure/disk#list) команды. В этом примере имя диска hello в переменной с именем hello местах *datadisk*, которое используется в следующем шаге hello.

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

Используйте hello [присоединить диск виртуальной машины az](https://docs.microsoft.com/cli/azure/vm/disk#attach) команда tooattach hello диска.

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы ознакомились с дисками виртуальных машин, а именно с:

> [!div class="checklist"]
> * дисками ОС и временными дисками;
> * Диски данных
> * дисками уровня "Стандартный" и "Премиум";
> * производительностью дисков;
> * присоединением и подготовкой дисков данных;
> * изменением размеров дисков;
> * моментальными снимками дисков.

Переместить следующий учебник toolearn toohello об автоматической конфигурации виртуальной Машины.

> [!div class="nextstepaction"]
> [Автоматизация настройки виртуальной машины](./tutorial-automate-vm-deployment.md)
