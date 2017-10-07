---
title: "aaaCreate и управление виртуальными машинами Linux с hello Azure CLI | Документы Microsoft"
description: "Учебник — Создание и управление виртуальными машинами Linux с hello Azure CLI"
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
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a>Создание и управление виртуальными машинами Linux с hello Azure CLI

Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду. В этом руководстве рассматриваются основные элементы развертывания виртуальной машины Azure, например выбор ее размера, образа и ее развертывание. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создать и присоединить tooa виртуальной Машины
> * Выбор и использование образов виртуальных машин
> * Просмотр и использование определенных размеров виртуальных машин
> * Изменение размера виртуальной машины
> * Просмотр виртуальной машины и оценка ее состояния


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-resource-group"></a>Создать группу ресурсов

Создание группы ресурсов с hello [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) команды. 

Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. Группу ресурсов следует создавать до виртуальной машины. В этом примере имя группы ресурсов *myResourceGroupVM* создается в hello *eastus* области. 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

Группа ресурсов Hello указывается при создании или изменении виртуальных Машин, который можно увидеть на протяжении этого учебника.

## <a name="create-virtual-machine"></a>Создание виртуальной машины

Создание виртуальной машины с hello [создания виртуальной машины az](https://docs.microsoft.com/cli/azure/vm#create) команды. 

При создании виртуальной машины доступно несколько вариантов, таких как образ операционной системы, определение размера диска и учетные данные администратора. В этом примере создается виртуальная машина *myVM* под управлением Ubuntu Server. 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

Один раз hello создания виртуальной Машины, hello Azure CLI выводит сведения о hello виртуальной Машины. Запишите hello `publicIpAddress`, этот адрес может быть используется tooaccess hello виртуальной машины... 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a>Подключение tooVM

Теперь можно подключиться toohello виртуальной Машины с помощью SSH. Замените IP-адрес hello пример hello `publicIpAddress` отмечалось в предыдущем шаге hello.

```bash
ssh 52.174.34.95
```

После завершения работы с hello виртуальной Машины, закройте сеанс SSH hello. 

```bash
exit
```

## <a name="understand-vm-images"></a>Описание образов виртуальных машин

Hello Azure marketplace включает большое количество изображений, которые могут быть toocreate используемых виртуальных машин. В предыдущих шагах hello на виртуальной машине был создан с помощью Ubuntu изображения. На этом шаге hello Azure CLI — marketplace hello toosearch используется для создания образа CentOS, которое затем используется toodeploy второй виртуальной машины.  

toosee список hello чаще всего используются изображения, используйте hello [списка изображений ВМ az](/cli/azure/vm/image#list) команды.

```azurecli-interactive 
az vm image list --output table
```

выходные данные команды Hello возвращает hello наиболее популярных образов виртуальных Машин в Azure.

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

Полный список можно увидеть, добавив hello `--all` аргумент. список изображений Hello, также можно фильтровать по `--publisher` или `–-offer`. В этом примере hello список отфильтрован и все образы, соответствующий предложением *CentOS*. 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

Частичные выходные данные приведены ниже.

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

toodeploy ВМ с помощью специального образа, запишите значение hello hello *Urn* столбца. При указании изображения hello, номер версии образа hello можно заменить «последние», который выбирает последнюю версию hello hello распространения. В этом примере hello `--image` аргумент является последней версии используется toospecify hello образа CentOS версии 6.5.  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a>Описание размеров виртуальных машин

Размер виртуальной машины определяет hello объем вычислительных ресурсов, таких как ЦП, графического Процессора и памяти, сделанные доступными toohello виртуальной машины. Виртуальные машины должны toobe масштабы hello ожидается рабочей нагрузки. При увеличении рабочей нагрузки размер существующей виртуальной машины может быть изменен.

### <a name="vm-sizes"></a>Размеры виртуальных машин

в следующей таблице Hello относит размеры вариантов использования.  

| Тип                     | Размеры           |    Описание       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Универсальные](sizes-general.md)         |Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7| Сбалансированное соотношение ресурсов ЦП и памяти. Идеально подходит для разработки и тестирования и малого toomedium приложениям и данным решения.  |
| [Оптимизированные для вычислений](sizes-compute.md)   | Fs, F             | Высокое соотношение ресурсов ЦП и памяти. Подходят для приложений со средним объемом трафика, сетевых устройств и пакетных процессов.        |
| [Оптимизированные для памяти](../virtual-machines-windows-sizes-memory.md)    | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Высокое соотношение ресурсов памяти и числа ядер. Идеально подходит для реляционных баз данных, кэши средний toolarge и аналитики в памяти.                 |
| [Оптимизированные для хранилища](../virtual-machines-windows-sizes-storage.md)      | Ls                | Высокая пропускная способность дисков и количество операций ввода-вывода. Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.                                                         |
| [GPU](sizes-gpu.md)          | NV, NC            | Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.       |
| [Высокопроизводительные](sizes-hpc.md) | H, A8–A11          | Виртуальные машины с самыми мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA). 


### <a name="find-available-vm-sizes"></a>Поиск всех доступных размеров виртуальных машин

toosee список виртуальных Машин размеров, доступных в определенном регионе, используйте hello [списка размеров виртуальных машин az](/cli/azure/vm#list-sizes) команды. 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

Частичные выходные данные приведены ниже.

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a>Создание виртуальной машины с определенным размером

Hello предыдущего примера создания виртуальной Машины размер не указано, какие результаты размером по умолчанию. Размер виртуальной Машины можно выбрать во время создания с помощью [создания виртуальной машины az](/cli/azure/vm#create) и hello `--size` аргумент. 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a>Изменение размера виртуальной машины

После развертывания виртуальной Машины, ее можно изменять размер tooincrease или уменьшить выделения ресурсов.

Перед изменением размера виртуальной Машины, проверьте, если hello желаемый размер текущего кластера Azure hello. Hello [az виртуальной машины-vm-resize параметры списка](/cli/azure/vm#list-vm-resize-options) команда возвращает hello список размеров. 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
При желании hello, что он доступен hello виртуальной Машины могут быть изменены из состояния включении, однако он не будет перезагружен во время операции hello. Используйте hello [изменить размер виртуальной машины az]( /cli/azure/vm#resize) команда tooperform hello, изменения размера.

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

Если hello желаемый размер находится не на hello текущего кластера, hello ВМ потребностей, может произойти toobe освобождена до hello операцию изменения размера. Используйте hello [ВМ az deallocate]( /cli/azure/vm#deallocate) команды toostop и освобождать hello виртуальной Машины. Обратите внимание, что при hello виртуальная машина не будет включено обратно, могут быть удалены все данные на диске временный hello. Hello общедоступный IP-адрес также изменяется, если только не используется статический IP-адрес. 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

После освобождена, может произойти изменения размера hello. 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

После изменения размера hello, можно запустить hello виртуальной Машины.

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a>Состояния включенной виртуальной машины

Включенная виртуальная машина Azure может находиться в одном из многих состояний. Это состояние представляет текущее состояние hello hello виртуальной Машины с точки зрения hello hello низкоуровневой оболочки. 

### <a name="power-states"></a>Состояния включения

| Состояние включения | Описание
|----|----|
| Starting | Указывает, что hello виртуальная машина запускается. |
| Выполнение | Указывает, что выполняется hello виртуальной машины. |
| Остановка | Указывает, что выполняется остановка виртуальной машины hello. | 
| Остановлено | Указывает, что этот hello виртуальная машина остановлена. Виртуальные машины в состоянии остановки hello взиматься плата за вычислительные операции.  |
| Отмена выделения | Указывает, что выполняется освобождение hello виртуальной машины. |
| Освобождено | Указывает, что для этой виртуальной машине hello удален из hello низкоуровневой оболочки, но по-прежнему доступны в плоскости управления hello. Виртуальные машины в состоянии освобождена hello не взимается вычислений. |
| - | Указывает на неизвестное состояние электропитания hello hello виртуальной машины. |

### <a name="find-power-state"></a>Поиск состояние включения

состояние конкретной виртуальной Машины, используйте hello hello tooretrieve [ВМ az получить представление экземпляров](/cli/azure/vm#get-instance-view) команды. Быть toospecify убедиться, что допустимое имя для виртуальной машины и группе ресурсов. 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

Выходные данные:

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a>Задачи управления

Во время hello жизненного цикла виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины. Кроме того вы можете toocreate сценариев tooautomate повторяющихся или сложных задач. С помощью hello Azure CLI, стандартных задач управления можно запускать из командной строки hello или в скриптах. 

### <a name="get-ip-address"></a>Получение IP-адреса

Эта команда возвращает hello частных и общедоступных IP-адреса виртуальной машины.  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a>Прекращение работы виртуальной машины

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a>Запуск виртуальной машины

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a>Удалить группу ресурсов

При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a>Дальнейшие действия

В рамках этого руководства вы изучили основы создания виртуальной машины и управления ею. Вы узнали, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создать и присоединить tooa виртуальной Машины
> * Выбор и использование образов виртуальных машин
> * Просмотр и использование определенных размеров виртуальных машин
> * Изменение размера виртуальной машины
> * Просмотр виртуальной машины и оценка ее состояния

Переместить следующий учебник toolearn toohello о дисках виртуальных Машин.  

> [!div class="nextstepaction"]
> [Управление дисками Azure с помощью Azure CLI](./tutorial-manage-disks.md)
