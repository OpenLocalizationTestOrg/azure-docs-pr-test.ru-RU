---
title: "aaaCreate и передачи Виртуальной машине OpenBSD изображений tooAzure | Документы Microsoft"
description: "Узнайте, как toocreate и передача виртуального жесткого диска (VHD), содержащий hello toocreate OpenBSD операционной системы виртуальной машины Azure через Azure CLI"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>Создание и отправка tooAzure образ диска OpenBSD
В этой статье показано, как toocreate и передача виртуального жесткого диска (VHD), содержащий hello OpenBSD операционной системы. После загрузки, она может служить toocreate собственный образ виртуальной машины (VM) в Azure через Azure CLI.


## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что hello следующих элементов:

* **Подписка Azure.** Если у вас нет учетной записи, то ее можно создать, что займет всего лишь несколько минут. Если у вас есть подписка MSDN, см. страницу [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). В противном случае — Узнайте, каким образом слишком[создать бесплатную пробную учетную запись](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure CLI 2.0** -убедитесь, что у вас есть hello последней [Azure CLI 2.0](/cli/azure/install-azure-cli) установлен и вход tooyour учетная запись Azure с [входа az](/cli/azure/#login).
* **OpenBSD операционной системы, установленной в VHD-файл** -поддерживаемой операционной системы OpenBSD (версии 6.1) должен быть tooa установленного виртуального жесткого диска. Существуют несколько средства toocreate VHD-файлы. Например можно использовать решение виртуализации, таких как Hyper-V toocreate hello VHD-файл и установить hello операционной системы. Инструкции о том, как tooinstall и использование Hyper-V, на экране [Установка Hyper-V и создание виртуальной машины](http://technet.microsoft.com/library/hh846766.aspx).


## <a name="prepare-openbsd-image-for-azure"></a>Подготовка образа OpenBSD для Azure
На hello виртуальной Машины, где установлен hello OpenBSD операционную систему 6.1, которая добавлена поддержка Hyper-V, выполните hello следующих процедур.

1. Если DHCP не включен во время установки, включите службу hello следующим образом:

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. Настройте последовательную консоль.

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. Настройте пакет установки следующим образом:

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. По умолчанию hello `root` пользователь отключен на виртуальных машинах в Azure. Пользователи могут запускать команды с повышенными привилегиями, используя hello `doas` на OpenBSD виртуальной Машины. Doas включен по умолчанию. Дополнительные сведения см. на веб-сайте [doas.conf](http://man.openbsd.org/doas.conf.5). 

5. Установка и настройка необходимых компонентов для hello агент Azure следующим образом:

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. всегда Hello последний выпуск hello Azure агента можно найти на [Github](https://github.com/Azure/WALinuxAgent/releases). Установка агента hello следующим образом:

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > После установки агента Azure очень хорошее представление tooverify, на котором выполняется следующим образом:
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. Отзыв hello системы tooclean его и внести он подходит для инициализацию. Hello следующая команда также удаляет hello последнего подготовленных учетную запись и hello связанных данных:

    ```sh
    waagent -deprovision+user -force
    ```

Теперь вы можете завершить работу виртуальной машины.


## <a name="prepare-hello-vhd"></a>Подготовка hello виртуального жесткого диска
Hello формат VHDX не поддерживается только в Azure, **фиксированный VHD**. Можно преобразовать с помощью диспетчера Hyper-V VHD формат hello диск toofixed или hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) командлета. Например.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>Создание и передача ресурсов хранилища
Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload виртуальный жесткий ДИСК, создайте учетную запись хранения с [создания учетной записи хранилища az](/cli/azure/storage/account#create). Имя учетной записи хранения должно быть уникальным, поэтому введите собственное имя. Hello следующий пример создает учетную запись хранения с именем *mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol доступ к учетной записи хранилища toohello, получите ключ хранилища hello с [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list) следующим образом:

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

отдельные hello toologically виртуальные жесткие диски, вы отправляете, создать контейнер в учетной записи хранилища hello с [создать контейнер хранилища az](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

Наконец, отправьте ваш VHD с помощью команды [az storage blob upload](/cli/azure/storage/blob#upload) следующим образом:

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>Создание виртуальной машины из VHD
Можно создать виртуальную машину с помощью [примера скрипта](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) или напрямую с помощью команды [az vm create](/cli/azure/vm#create). toospecify hello OpenBSD виртуального жесткого диска вы отправили hello используйте `--image` параметр следующим образом:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Получить hello IP-адрес для виртуальной Машины с OpenBSD [ВМ az список ip адреса](/cli/azure/vm#list-ip-addresses) следующим образом:

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

Теперь вы можете SSH tooyour OpenBSD ВМ в обычном режиме:
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о Hyper-V поддерживает на OpenBSD6.1 tooknow прочитать [OpenBSD 6.1](https://www.openbsd.org/61.html) и [hyperv.4](http://man.openbsd.org/hyperv.4).

Toocreate ВМ из управляемого диска следует прочитать [диска az](/cli/azure/disk). 
