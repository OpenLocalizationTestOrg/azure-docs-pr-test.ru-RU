---
title: "aaaCapture toouse виртуальной Машине Linux Azure как шаблон | Документы Microsoft"
description: "Узнайте, как toocapture и обобщить образ на основе Linux Azure созданная виртуальная машина (ВМ) с моделью развертывания диспетчера ресурсов Azure hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Запись виртуальной машины Linux, работающей в Azure
Выполните действия hello в этой статье toogeneralize и сохранения виртуальной машине Azure Linux (ВМ) в модели развертывания диспетчера ресурсов hello. При создании hello виртуальной Машины вы удалите личных учетных записей и подготовка toobe hello виртуальной Машины, используемое в качестве изображения. Вы затем обобщенный виртуальный жесткий диск (VHD) из образа для hello ОС, виртуальные жесткие диски для подключенные диски данных, отслеживания и [шаблона диспетчера ресурсов](../../azure-resource-manager/resource-group-overview.md) для нового развертывания виртуальной Машины. В этой статье указаны как образ toocapture виртуальной Машины с hello Azure CLI 1.0 для виртуальной Машины с помощью неуправляемых дисков. Вы также можете [захватить ВМ с помощью управляемых дисков Azure с hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Управляемый диски обрабатываются hello платформы Azure и не требуют toostore любые предварительные и расположение их. Дополнительные сведения об Управляемых дисках Azure см. в [этой статье](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

toocreate виртуальные машины с помощью образа hello настроить сетевые ресурсы для каждой новой виртуальной Машины и использовать toodeploy hello шаблон (файл JavaScript, или JSON,), его из hello записанных образов виртуальных жестких ДИСКОВ. Таким образом можно реплицировать виртуальную Машину с текущей конфигурации программного обеспечения, так же как toohello использование изображений в hello Azure Marketplace.

> [!TIP]
> Если toocreate копию существующей ВМ Linux с ее состоянием специализированные для резервного копирования или отладки, см. [создать копию виртуальной машины Linux в Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). И если tooupload VHD из локальной виртуальной Машины Linux, см. [передача и создание виртуальной Машины Linux из пользовательского образа](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#before-you-begin) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="before-you-begin"></a>Перед началом работы
Убедитесь, что выполнены следующие предварительные требования hello:

* **Виртуальная машина Azure создаются в модели развертывания диспетчера ресурсов hello** -Если вы еще не создали ВМ Linux, можно использовать hello [портала](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [Azure CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), или [диспетчера ресурсов шаблоны](create-ssh-secured-vm-from-template.md). 
  
    Настройка виртуальной Машины, при необходимости hello. Например, [добавьте диски данных](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), примените обновления и установите приложения. 
* **Azure CLI** -Install hello [Azure CLI](../../cli-install-nodejs.md) на локальном компьютере.

## <a name="step-1-remove-hello-azure-linux-agent"></a>Шаг 1: Удаление агента Azure Linux hello
Сначала запустите hello **waagent** с hello **отзыва** параметров на виртуальной Машине Linux hello. Эта команда удаляет файлы и данные toomake hello виртуальная машина готова для обобщения. Дополнительные сведения см. в разделе hello [руководство пользователя Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

1. Подключите tooyour виртуальных Машин Linux с помощью SSH-клиента.
2. В окне приветствия SSH введите hello следующую команду:
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > Только выполните команду на виртуальной Машине, следует присвоить toocapture как изображение. Он не гарантирует этот образ hello подходит для распространения или удаляется все конфиденциальные данные.
 
3. Тип **y** toocontinue. Можно добавить hello **-принудительно** tooavoid параметр этого шага подтверждения.
4. После выполнения команды hello введите **выхода**. Этот шаг закрывает клиент SSH hello.

## <a name="step-2-capture-hello-vm"></a>Шаг 2: Запись hello виртуальной Машины
Используйте toogeneralize hello Azure CLI и записать hello виртуальной Машины. В hello следующих примерах замените примеры имен параметров собственные значения. Примеры имен параметров: **myResourceGroup**, **myVnet** и **myVM**.

1. С локального компьютера, откройте hello Azure CLI и [tooyour входа подписки Azure](../../xplat-cli-connect.md). 
2. Убедитесь, что режим Resource Manager включен.
   
    ```azurecli
    azure config mode arm
    ```
3. Завершение работы hello виртуальной Машине, которая уже удалена с помощью hello следующую команду:
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. Обобщить hello виртуальной Машины с hello следующую команду:
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. Теперь запустите hello **записи виртуальной машины azure** команды, который получает hello виртуальной Машины. В следующем примере hello, hello образ VHD записанный с помощью имен, начиная с **MyVHDNamePrefix**и hello **-t** указывает путь шаблона toohello **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > Hello образ VHD-файлов создаются по умолчанию в приветствия использовать одну учетную запись хранилища, hello исходной виртуальной Машины. Используйте hello *учетную запись хранения* toostore hello виртуальных жестких дисков для создания из образа hello новые виртуальные машины. 

6. расположение hello toofind записанный образ шаблона JSON Привет открыть в текстовом редакторе. В hello **storageProfile**, найти hello **uri** из hello **изображения** в hello **системы** контейнера. Например hello URI образа диска ОС hello аналогичен слишком`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Шаг 3: Создание виртуальной Машины из образа захвачен hello
Теперь можно используйте образ hello с toocreate шаблона виртуальной Машины Linux. Эти шаги показано, как toouse hello Azure CLI и hello шаблона файла JSON, вы записали hello toocreate виртуальной Машины в новой виртуальной сети.

### <a name="create-network-resources"></a>Создание сетевых ресурсов
шаблон toouse hello, необходимо сначала tooset виртуальной сети и сетевой Адаптер для новой виртуальной Машины. Рекомендуется создать группу ресурсов для этих ресурсов hello там, где хранится образ виртуальной Машины. Выполните команды toohello примерно следующие, указав имена ресурсов и расположение соответствующих Azure («centralus» в этих командах):

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Получить идентификатор hello Сетевых hello
toodeploy виртуальной Машины из образа hello с помощью hello JSON, сохраненный во время записи, необходимо hello идентификатор hello сетевого адаптера. Получите его, запустив hello следующую команду:

```azurecli
azure network nic show myResourceGroup1 myNIC
```

Hello **идентификатор** в hello вывод команды будет примерно слишком`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>Создание виртуальной машины
После выполнения hello следующая команда toocreate ВМ из hello запись образа виртуальной Машины. Используйте hello **-f** toohello путь шаблон JSON для параметра toospecify hello файл был сохранен.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

В выходных данных команды hello вы запрашиваемые toosupply новое имя виртуальной Машины, имя пользователя администратора hello и пароль и hello идентификатор hello сетевого Адаптера, созданной ранее.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

Следующий образец Hello показывает, отображаемые для успешного развертывания:

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Проверка развертывания hello
Теперь SSH toohello виртуальной машины вы создали tooverify hello развертывания и запуска с помощью hello новой виртуальной Машины. tooconnect через SSH, поиска IP-адреса hello hello виртуальной Машины, созданные с помощью hello следующую команду:

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

Hello общедоступный IP-адрес отображается в выходных данных команды hello. По умолчанию соединение toohello виртуальных Машин Linux по протоколу SSH на порт 22.

## <a name="create-additional-vms"></a>Создание дополнительных виртуальных машин
Используйте hello захвата образа и шаблон toodeploy дополнительных ВМ с помощью действия hello в предшествующих раздел hello. Другие параметры toocreate виртуальные машины, из образа hello включать с помощью шаблона примеры использования или запуска hello **создания виртуальной машины azure** команды.

### <a name="use-hello-captured-template"></a>Используйте шаблон записанного hello
toouse hello захвата образа и шаблона, выполните следующие действия, (подробные hello предшествующий раздел):

* Убедитесь, что образ виртуальной Машины в hello учетную запись хранения, на котором размещается виртуальный жесткий ДИСК Виртуальной машины.
* Скопируйте файл JSON hello шаблон и укажите уникальное имя для диска ОС hello hello новой Виртуальной машины виртуальный жесткий ДИСК (или виртуальные жесткие диски). Например, в hello **storageProfile**в разделе **виртуального жесткого диска**в **uri**, укажите уникальное имя для hello **osDisk** виртуального жесткого диска, аналогичные слишком`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* Создайте сетевую КАРТУ в любом hello того же или другой виртуальной сети.
* С помощью JSON-файл шаблона изменен hello, создайте развертывание в группе ресурсов hello, в котором можно настроить виртуальную сеть hello.

### <a name="use-a-quickstart-template"></a>Использование шаблона быстрого запуска
Если вы хотите настроить автоматически при создании виртуальной Машины из образа hello сети hello, можно указать эти ресурсы в шаблоне. Например, в разделе hello [101 виртуальных машин из пользовательского образа шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) из GitHub. Этот шаблон создает виртуальную Машину из пользовательского образа и hello необходимости виртуальной сети, общедоступный IP-адрес и Сетевых ресурсов. Пошаговое руководство по с помощью шаблона hello в hello портал Azure, в разделе [как toocreate виртуальной машины из образа с помощью шаблона диспетчера ресурсов](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).

### <a name="use-hello-azure-vm-create-command"></a>Создание виртуальной машины hello azure используйте команды
Обычно это самый простой toouse toocreate шаблона диспетчера ресурсов виртуальной Машины из образа hello. Тем не менее, можно создать hello ВМ *принудительно* с помощью hello **создания виртуальной машины azure** с hello **-Q** (**--urn изображения**) параметра . При использовании этого метода можно также передать hello **-d** (**--ОС диска vhd-**) параметра toospecify hello расположение VHD-файл hello ОС для hello новой виртуальной Машины. Этот файл должен быть в контейнере VHD-файлов hello учетной записи хранения hello, где хранится hello образ VHD-файл. Здравствуйте, команда копирует hello виртуального жесткого диска для hello новой виртуальной Машины автоматически toohello **виртуальные жесткие диски** контейнера.

Перед запуском **создания виртуальной машины azure** с образа hello, выполните следующие шаги hello:

1. Создайте группу ресурсов или укажите существующую группу ресурсов для развертывания hello.
2. Создайте открытый IP-адреса и ресурса сетевого Адаптера для hello новой виртуальной Машины. Действия toocreate виртуальной сети открытый IP-адреса и сетевого Адаптера с помощью hello CLI, см. выше в этой статье. (**создания виртуальной машины azure** можно также создать сетевой Адаптер, но требуется toopass Дополнительные параметры для виртуальной сети и подсети.)

Выполните команду, которая передает идентификаторы URI tooboth hello новый файл виртуального жесткого диска операционной системы и hello существующий образ. В этом примере размер виртуальной Машины Standard_A1 создается в регионе Восток США hello.

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

Чтобы получить информацию о дополнительных параметрах команды, выполните команду `azure help vm create`.

## <a name="next-steps"></a>Дальнейшие действия
toomanage виртуальные машины с hello CLI, просмотреть задачи hello в [развертывание и управление виртуальными машинами с помощью шаблонов диспетчера ресурсов Azure и Azure CLI hello](create-ssh-secured-vm-from-template.md).

