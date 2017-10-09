---
title: "файлы aaaPersist в оболочке облако Azure (Предварительная версия) | Документы Microsoft"
description: "Пошаговое руководство по сохранению файлов в Azure Cloud Shell."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a>Сохранение файлов в Azure Cloud Shell
Оболочки облака использует файлы toopersist хранилища Azure файл во всех сеансах.

## <a name="set-up-a-clouddrive-file-share"></a>Настройка файлового ресурса `clouddrive`
Для первоначального запуска оболочки облака предлагает tooassociate нового или существующего файла совместно использовать файлы toopersist между сеансами.

### <a name="create-new-storage"></a>Создание хранилища

При использовании основные параметры и выберите только подписки, облака оболочки создаются три ресурсы от вашего имени в регионе hello поддерживается ближайшем tooyou:
* группу ресурсов `cloud-shell-storage-<region>`;
* учетную запись хранения `cs<uniqueGuid>`;
* файловый ресурс `cs-<user>-<domain>-com-<uniqueGuid>`.

![Подписка приветствия](media/basic-storage.png)

Подключает Hello общей папки как `clouddrive` в ваш `$Home` каталога. Hello общая папка является также используется toostore образ размером 5 ГБ, который создается для вас и который автоматически обновляет и сохраняет вашей `$Home` каталога. Это однократное действие, и автоматически подключает hello общей папки в последующих сеансах.

### <a name="use-existing-resources"></a>Использование существующих ресурсов

С помощью hello дополнительный параметр, можно связать существующие ресурсы. При появлении подсказки при установке хранилища hello выберите **Показывать дополнительные параметры** tooview Дополнительные параметры. Существующие общие папки приема toopersist изображения размером 5 ГБ пользователя вашего `$Home` каталога. отфильтрованные Hello раскрывающиеся меню для своего региона оболочки облачной и локальной избыточности & географически избыточное хранилище учетных записей.

![параметр группы ресурсов Hello](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a>Ограничение создания ресурсов с помощью политик ресурсов Azure
Учетные записи хранения, создаваемые в Cloud Shell, помечаются тегом `ms-resource-usage:azure-cloud-shell`. Toodisallow пользователям возможность создавать учетные записи хранения в облаке оболочки создать [политики ресурсов Azure для тегов](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) , активируемых этого конкретного тега.

## <a name="how-cloud-shell-works"></a>Как работает Cloud Shell
Облако оболочки сохранится файлов с помощью обоих hello следующие методы:
* Создание образа диска вашей `$Home` toopersist каталога все содержимое в каталоге hello. образ диска Hello сохраняется в папке указанный файл как `acc_<User>.img` в `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, и он автоматически синхронизирует изменения.

* Подключение выбранного файлового ресурса как `clouddrive` в каталоге `$Home`. Это позволяет взаимодействовать с ним напрямую. `/Home/<User>/clouddrive`сопоставляется слишком`fileshare.storage.windows.net/fileshare`.
 
> [!NOTE]
> Все файлы в каталоге `$Home`, такие как ключи SSH, сохраняются в образе диска пользователя, который хранится в подключенном файловом ресурсе. Соблюдайте рекомендации при сохранении информации в каталоге `$Home` и подключенном файловом ресурсе.

## <a name="use-hello-clouddrive-command"></a>Используйте hello `clouddrive` команды
С оболочкой облака, можно выполнить команду, вызывается `clouddrive`, который позволяет вам toomanually обновления hello общей папки с подключенного tooCloud оболочки.
![Выполнив команду «clouddrive» hello](media/clouddrive-h.png)

## <a name="mount-a-new-clouddrive"></a>Подключение нового `clouddrive`

### <a name="prerequisites-for-manual-mounting"></a>Предварительные требования для подключения вручную
Вы можете обновить hello общий файловый ресурс, связанный с облачной оболочки с помощью hello `clouddrive mount` команды.

Если подключить существующий файловый ресурс, необходимо hello учетные записи хранения.
* Локально избыточное хранилище или геоизбыточное хранилище toosupport общих папок.
* Находиться в назначенном вам регионе. При адаптации hello регион назначения toois, перечисленные в имя группы ресурсов hello `cloud-shell-storage-<region>`.

### <a name="supported-storage-regions"></a>Поддерживаемые регионы хранилища
Hello Azure файлы должны находиться в hello же регионе, что машина оболочки облака hello, подключение их. Кластеры оболочки облака в настоящее время существует в hello следующие области:
|Область|Регион|
|---|---|
|Северная и Южная Америка|Восточная часть США, юго-центральный регион США, западная часть США|
|Европа|Северная Европа, Западная Европа|
|Азиатско-Тихоокеанский регион|Центральная Индия, Юго-Восточная Азия|

### <a name="hello-clouddrive-mount-command"></a>Hello `clouddrive mount` команды

> [!NOTE]
> Если подключение новую общую папку, создается новый пользовательский образ вашей `$Home` каталог, из-за предыдущих `$Home` изображение сохраняется в hello предыдущих общей папки.

Запустите hello `clouddrive mount` с hello следующие параметры:

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

tooview сведения, запустите `clouddrive mount -h`, как показано ниже:

![Выполнение hello "clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a>Отключение `clouddrive`
Можно отключить общий файловый ресурс с подключенного tooCloud оболочки в любое время. После файлового ресурса отключены, вы сможете запрашиваемые toomount новый tooyour предыдущего общую папку файл следующего сеанса.

tooremove файл для общей папки из облака оболочки:
1. Запустите `clouddrive unmount`.
2. Подтверждаю и подтвердите hello приглашения.

Файлового ресурса по-прежнему tooexist пока не будут удалены вручную. Cloud Shell больше не будет искать эту общую папку для последующих сеансов.

tooview сведения, запустите `clouddrive unmount -h`, как показано ниже:

![Выполнение hello "clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> При выполнении этой команды ресурсы не удаляются. Вручную удалить группу ресурсов, учетной записи хранилища или общую папку, сопоставленный tooCloud оболочки приведет к окончательному удалению вашей `$Home` directory изображения и другие файлы в папке файла. Это действие невозможно отменить.

## <a name="list-clouddrive-file-shares"></a>Вывод списка файловых ресурсов `clouddrive`
какие общей папки подключается как toodiscover `clouddrive`, hello следующей `df` команды. 

tooclouddrive путь файла Hello показывает, что имя учетной записи хранилища и файл общей папки в URL-адрес hello. Например, `//storageaccountname.file.core.windows.net/filesharename`

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a>Перенос локальных файлов tooCloud оболочки
Hello `clouddrive` синхронизации каталогов с колонке hello портала хранилища Azure. Используйте локальные файлы tooor с tootransfer этой колонке из файлового ресурса. Обновление файлов из облака оболочки отражается в хранилище файлов hello графического пользовательского интерфейса при обновлении колонки hello.

### <a name="download-files"></a>Скачивание файлов

![Вывод списка локальных файлов](media/download.png)
1. В hello портал Azure перейдите toohello подключенного общей папки.
2. Выберите целевой файл hello.
3. Выберите hello **загрузки** кнопки.

### <a name="upload-files"></a>Отправка файлов

![Отправить toobe локальные файлы](media/upload.png)
1. Последовательно выберите tooyour подключить общую папку.
2. Выберите hello **отправить** кнопки.
3. Выберите файл hello или файлы, которые должны tooupload.
4. Подтверждение отправки hello.

Теперь вы увидите hello файлы, доступные в вашей `clouddrive` каталог в облаке оболочки.

## <a name="next-steps"></a>Дальнейшие действия
[Краткое руководство по Cloud Shell](quickstart.md) <br>
[Хранилище файлов](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[Использование тегов для организации ресурсов в Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
