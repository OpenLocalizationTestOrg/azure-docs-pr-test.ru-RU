---
title: "хранилище файлов Azure на виртуальных машинах Linux по протоколу SMB с помощью Azure CLI 1.0 aaaMount | Документы Microsoft"
description: "Как toomount хранилище файлов Azure на виртуальных машинах Linux с помощью SMB"
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
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a>Подключение хранилища файлов Azure на виртуальных машинах Linux по протоколу SMB с помощью Azure CLI 1.0

В этой статье показано, как toomount хранилища Azure File на виртуальной Машине Linux с помощью hello протокола Server Message Block (SMB). Хранилище файлов предлагает общих файловых ресурсов в облаке hello через hello стандартного протокола SMB. Существуют следующие требования Hello.

* [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);
* [файлы открытого и закрытого ключей Secure Shell (SSH)](mac-create-ssh-keys.md).

## <a name="cli-versions-toouse"></a>Toouse версии CLI
Hello задачу можно выполнить с помощью одного из hello следующие версии интерфейса командной строки (CLI):

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="quick-commands"></a>Быстрые команды
Задача hello tooaccomplish быстро, выполните действия hello в этом разделе. Более подробные сведения и контекста, начинаются с Привет [«Подробное пошаговое руководство»](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) раздела.

### <a name="prerequisites"></a>Предварительные требования
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
Добавить слишком следующей строкой hello`/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

Хранилище файлов предлагает общих файловых ресурсов в облаке hello, использующих hello стандартного протокола SMB. С hello последний выпуск хранилища файлов можно также подключить общий файловый ресурс с любой ОС, которая поддерживает SMB 3.0. При использовании подключения SMB в Linux, вы получаете легко резервные копии tooa надежный, постоянный архивирования место хранения, поддерживаемый соглашения об уровне ОБСЛУЖИВАНИЯ.

Перенос файлов из монтирования SMB tooan виртуальная машина, размещенная в хранилище файлов — журналы toodebug хорошим способом. Это потому, что общий ресурс SMB же hello могут быть подключены локально tooyour рабочей станции Windows, Mac или Linux. SMB не hello наилучшим решением для потоковой передачи Linux или журналы приложений в режиме реального времени, так как протокол SMB hello не построен toohandle таких обязанностей интенсивной ведения журнала. Вместо SMB для сбора выходных данных журналов Linux и приложений лучше использовать специальный единый инструмент, работающий на уровне ведения журналов, например Fluentd.

Для Подробное пошаговое руководство мы создание необходимых компонентов hello необходимости toofirst создать hello общей папки хранилища, а затем подключать через SMB на виртуальной Машине Linux.

1. Создайте учетную запись хранилища Azure с помощью hello, следующий код:

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. Показать hello ключи учетной записи хранения.

    При создании учетной записи хранилища, hello ключи учетной записи создаются попарно, чтобы они могут быть повернуты без нарушения работы службы. При переключении toohello второго ключа в паре "hello", вы создаете новую пару ключей. Новых ключей учетной записи хранения всегда создаются попарно, убедитесь, что всегда существует по крайней мере один неиспользуемое пространство ключей готов tooswitch для. ключи учетной записи хранения hello tooshow использовать hello, следующий код:

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. Создание общей папки хранилища hello.

    Hello общей папки хранилища содержит общий ресурс SMB hello. Квота Hello всегда выражается в гигабайтах (ГБ). toocreate hello общей папки хранилища, выполните следующий код hello.

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. Создайте каталог hello точки подключения.

    Необходимо создать локальный каталог в hello Linux файл системы toomount hello в общей папке SMB. Запись или чтение из каталога hello локального подключения, направляются toohello общий ресурс SMB, размещенного в хранилище файлов. каталог toocreate hello, hello используйте следующий код:

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. Подключите hello в общей папке SMB, с помощью hello, следующий код:

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. Сохранение hello подключения SMB работу после перезагрузки.

    После перезагрузки виртуальной Машины с Linux hello hello подключенного общей папки SMB отключается во время завершения работы. tooremount hello общий ресурс SMB во время загрузки, необходимо добавить строку toohello/etc/fstab Linux. Linux использует hello fstab файл toolist hello файловых систем, он должен toomount во время процесса загрузки hello. Добавление общей папки SMB hello гарантирует, что в этой общей папки хранилища hello является постоянно подключенных файловой системы для виртуальной Машины с Linux hello. Добавление общей папки SMB tooa для hello файла хранения новой виртуальной Машины можно при использовании облачных init.

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>Дальнейшие действия

- [С помощью toocustomize init облака виртуальной Машины Linux во время создания](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Добавить диск tooa ВМ Linux](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
