---
title: "хранилище файлов Azure на виртуальных машинах Linux с помощью SMB aaaMount | Документы Microsoft"
description: "Как toomount хранилище файлов Azure на виртуальных машинах Linux с помощью SMB с hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>Подключение хранилища файлов Azure на виртуальных машинах Linux с помощью протокола SMB

В этой статье показано, как подключить hello tooutilize службы хранилища Azure файла на виртуальной Машине Linux с помощью SMB с hello Azure CLI 2.0. Хранилище файлов Azure предлагает общих файловых ресурсов в облаке hello, с помощью стандартного протокола SMB hello. Можно также выполнить следующие действия с hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Существуют следующие требования Hello.

- [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);
- [файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).

## <a name="quick-commands"></a>Быстрые команды

* Группа ресурсов.
* Виртуальная сеть Azure.
* Группа безопасности сети с входящим трафиком SSH.
* Подсеть.
* Учетная запись хранения Azure.
* Ключи учетной записи хранения Azure.
* Общая папка хранилища файлов Azure.
* Виртуальная машина Linux.

Замените все примеры параметров своими параметрами.

### <a name="create-a-directory-for-hello-local-mount"></a>Создайте каталог для локального подключения hello

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>Подключить файл hello хранилища общей папки SMB toohello точки подключения

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>Сохранение подключения hello после перезагрузки
toodo таким образом, добавьте следующие строки toohello hello `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

Хранилище файлов предлагает общих файловых ресурсов в облаке hello, использующих hello стандартного протокола SMB. С hello последний выпуск хранилища файлов можно также подключить общий файловый ресурс с любой ОС, которая поддерживает SMB 3.0. При использовании подключения SMB в Linux, вы получаете легко резервные копии tooa надежный, постоянный архивирования место хранения, поддерживаемый соглашения об уровне ОБСЛУЖИВАНИЯ.

Перенос файлов из монтирования SMB tooan виртуальная машина, размещенная в хранилище файлов — журналы toodebug хорошим способом. Это потому, что общий ресурс SMB же hello могут быть подключены локально tooyour рабочей станции Windows, Mac или Linux. SMB не hello наилучшим решением для потоковой передачи Linux или журналы приложений в режиме реального времени, так как протокол SMB hello не построен toohandle таких обязанностей интенсивной ведения журнала. Вместо SMB для сбора выходных данных журналов Linux и приложений лучше использовать специальный единый инструмент, работающий на уровне ведения журналов, например Fluentd.

Для Подробное пошаговое руководство мы создание необходимых компонентов hello необходимости toofirst создать hello общей папки хранилища, а затем подключать через SMB на виртуальной Машине Linux.

1. Создание группы ресурсов с [Создание группы az](/cli/azure/group#create) toohold hello общей папки.

    Группа ресурсов с именем toocreate `myResourceGroup` в hello расположение «West US», используйте следующий пример hello:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. Создать учетную запись хранилища Azure с [создания учетной записи хранилища az](/cli/azure/storage/account#create) toostore hello сами файлы.

    toocreate учетной записи хранилища с именем mystorageaccount с помощью хранилища Standard_LRS hello SKU, hello используйте следующий пример:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. Показать hello ключи учетной записи хранения.

    При создании учетной записи хранилища, hello ключи учетной записи создаются попарно, чтобы они могут быть повернуты без нарушения работы службы. При переключении toohello второго ключа в паре "hello", вы создаете новую пару ключей. Новых ключей учетной записи хранения всегда создаются попарно, убедитесь, что всегда существует по крайней мере один неиспользуемое пространство учетной записи ключа готов tooswitch для.

    Просмотреть ключи учетной записи хранения hello с hello [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list). Здравствуйте, ключи учетной записи с именем hello `mystorageaccount` , перечислены в hello в следующем примере:

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract один ключ, используйте hello `--query` флаг. Hello следующий пример извлекает первый ключ hello (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. Создание общей папки хранилища hello.

    Hello общей папки хранилища содержит общий ресурс SMB с hello [создать общую папку хранилища az](/cli/azure/storage/share#create). Квота Hello всегда выражается в гигабайтах (ГБ). Передачи в одном из разделов hello из предыдущего hello `az storage account keys list` команды. Создайте папку с именем mystorageshare с квотой 10 ГБ, используя следующий пример hello:

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. Создайте каталог точек подключения.

    Создает локальный каталог в hello Linux файл системы toomount hello в общей папке SMB. Запись или чтение из каталога hello локального подключения, направляются toohello общий ресурс SMB, размещенного в хранилище файлов. toocreate локального каталога в/mnt/mymountdirectory, hello используйте следующий пример:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. Подключите локального каталога общей папки SMB toohello hello.

    Укажите имя пользователя учетной записи хранилища и ключ учетной записи хранения для учетных данных подключения hello следующим образом:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. Сохранение hello подключения SMB работу после перезагрузки.

    После перезагрузки виртуальной Машины с Linux hello hello подключенного общей папки SMB отключается во время завершения работы. hello tooremount общей папке SMB, во время загрузки, добавьте строку toohello/etc/fstab Linux. Linux использует hello fstab файл toolist hello файловых систем, он должен toomount во время процесса загрузки hello. Добавление общей папки SMB hello гарантирует, что в этой общей папки хранилища hello является постоянно подключенных файловой системы для виртуальной Машины с Linux hello. Добавление общей папки SMB tooa для hello файла хранения новой виртуальной Машины можно при использовании облачных init.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Дальнейшие действия

- [С помощью toocustomize init облака виртуальной Машины Linux во время создания](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Добавить диск tooa ВМ Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
