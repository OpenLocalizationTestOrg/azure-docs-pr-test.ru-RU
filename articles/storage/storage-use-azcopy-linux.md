---
title: "aaaCopy или переместите tooAzure данные хранилища с помощью AzCopy в Linux | Документы Microsoft"
description: "Используйте hello AzCopy Linux программа toomove или копирования данных tooor из больших двоичных объектов и содержимого файла. Копирование данных tooAzure хранилища из локальных файлов или копирования данных в пределах или между учетными записями хранения. Легко перенесите на tooAzure данных хранилища."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: dccb03c9e8cc3ea661494e7834f307b0e3e30cb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Перенос данных с помощью AzCopy для Linux
AzCopy в Linux является командной строки служебная программа, разработанная для копирования данных tooand из хранилища больших двоичных объектов Microsoft Azure и файл с помощью простой команды с оптимальной производительностью. Можно скопировать данные из одного объекта tooanother в вашей учетной записи хранения или между учетными записями хранения.

Существуют две версии AzCopy, которые можно скачать. Служебная программа AzCopy для Linux основана на платформе .NET Core, которая нацелена на платформы Linux, использующие параметры командной строки в формате POSIX. Служебная программа [AzCopy для Windows](storage-use-azcopy.md) основана на платформе .NET Framework и использует параметры командной строки в формате Windows. В этой статье рассматривается AzCopy для Linux.

## <a name="download-and-install-azcopy"></a>Скачивание и установка AzCopy
### <a name="installation-on-linux"></a>Установка в Linux

AzCopy в Linux требуется .NET Core framework на платформе hello. См. инструкции по установке hello hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) страницы.

Для примера давайте установим .NET Core в Ubuntu 16.10. Hello последние руководства, посетите [.NET Core для Linux](https://www.microsoft.com/net/core#linuxubuntu) страница установки.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

После установки .NET Core скачайте и установите AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

После установки AzCopy в Linux можно удалить файлы извлечены hello. Также если у вас права суперпользователя, также запускаются AzCopy с помощью сценария оболочки hello «azcopy» в извлеченной папке hello. 

### <a name="alternative-installation-on-ubuntu"></a>Альтернативная установка в Ubuntu

**Ubuntu 14.04**

Добавьте источник apt для .NET Core.

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Добавьте источник apt для .NET Core.

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

Добавьте источник apt для .NET Core.

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Написание первой команды AzCopy
Базовый синтаксис команды AzCopy Hello таков:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Привет, следующие примеры демонстрируют различные сценарии для копирования данных tooand из файлов и больших двоичных объектов Microsoft Azure. См. toohello `azcopy --help` меню подробное описание параметров hello, используемых в каждой выборке.

## <a name="blob-download"></a>Большой двоичный объект: скачивание
### <a name="download-single-blob"></a>Скачивание одного большого двоичного объекта

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Если папка hello `/mnt/myfiles` не существует, AzCopy создает его и загружает `abc.txt ` в новую папку hello.

### <a name="download-single-blob-from-secondary-region"></a>Скачивание большого двоичного объекта из дополнительного региона

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.

### <a name="download-all-blobs"></a>Скачивание всех больших двоичных объектов

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Предположим следующее hello большие двоичные объекты находятся в указанном контейнере hello:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

После завершения операции загрузки hello hello каталог `/mnt/myfiles` включает hello следующие файлы:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Если не задать параметр `--recursive`, большие двоичные объекты не будут скачаны.

### <a name="download-blobs-with-specified-prefix"></a>Скачивание больших двоичных объектов с указанным префиксом

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Предположим следующее hello большие двоичные объекты находятся в указанном контейнере hello. Все большие двоичные объекты, начинающиеся с префикса hello `a` загружаются.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

После завершения операции загрузки hello hello папку `/mnt/myfiles` включает hello следующие файлы:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

префикс Hello применяется toohello виртуальному каталогу, который формирует первую часть имени большого двоичного объекта hello hello. В приведенном выше примере hello hello виртуального каталога не соответствует hello указанного префикса, поэтому BLOB-объекты не загружается. Кроме того, если hello параметр `--recursive` не указан, AzCopy не загружать все большие двоичные объекты.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Задать время последнего изменения hello toobe экспортированные файлы так же, как hello исходный BLOB-объект

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

Большие двоичные объекты можно также исключить из операции загрузки hello, на основе их времени последнего изменения. Например, большие двоичные объекты tooexclude, время последнего изменения — hello же или более новая, чем конечный файл hello, добавить hello `--exclude-newer` параметр:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

Или если вы хотите tooexclude BLOB-объектов, время последнего изменения — hello же или более ранней, чем конечный файл hello, добавьте hello `--exclude-older` параметр:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>Большой двоичный объект: отправка
### <a name="upload-single-file"></a>Отправка одного файла

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Если hello указанный контейнер не существует, AzCopy создает эту службу и передачи файла hello в него.

### <a name="upload-single-file-toovirtual-directory"></a>Отправка одного файла каталога toovirtual

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Если hello указанный виртуальный каталог не существует, AzCopy передает hello tooinclude файл hello виртуальный каталог hello имя BLOB-объекта (*например*, `vd/abc.txt` в приведенном выше примере hello).

### <a name="upload-all-files"></a>Отправка всех файлов

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Задание параметра `--recursive` содержимое передачи hello hello указано рекурсивно хранилища tooBlob каталога, то есть также загрузить свои файлы и все вложенные папки. Например, предположим, hello следующие файлы размещаются в папке `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

После завершения операции отправки hello hello контейнер содержит hello следующие файлы:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Здравствуйте, когда параметр `--recursive` не определено, только hello следующие три отправки файлов:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Отправка файлов, соответствующих указанному шаблону

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Предполагается hello следующие файлы размещаются в папке `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

После завершения операции отправки hello hello контейнер содержит hello следующие файлы:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Здравствуйте, когда параметр `--recursive` не указан, AzCopy пропускает файлы, находящиеся в вложенные каталоги:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Укажите hello MIME-тип содержимого большого двоичного объекта назначения
По умолчанию AzCopy задает тип содержимого hello BLOB-объект назначения, слишком`application/octet-stream`. Тем не менее, можно явно указать тип содержимого hello через параметр hello `--set-content-type [content-type]`. Этот синтаксис задает hello-тип содержимого для всех больших двоичных объектов в операции передачи.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Если hello параметр `--set-content-type` указан без значения, то AzCopy задает каждого большого двоичного объекта или файла тип содержимого в соответствии с tooits расширение файла.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>Большой двоичный объект: копирование
### <a name="copy-single-blob-within-storage-account"></a>Копирование большого двоичного объекта в пределах учетной записи хранения

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

При копировании большого двоичного объекта без параметра --sync-copy выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-single-blob-across-storage-accounts"></a>Копирование большого двоичного объекта между различными учетными записями хранения

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

При копировании большого двоичного объекта без параметра --sync-copy выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Копирование одного большого двоичного объекта из области tooprimary дополнительный регион

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Копирование большого двоичного объекта и его моментальных снимков между различными учетными записями хранения

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

После завершения операции копирования hello hello целевой контейнер включает hello большого двоичного объекта и его моментальные снимки. Hello контейнер включает в себя следующие hello большого двоичного объекта и его моментальные снимки:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Синхронное копирование больших двоичных объектов между учетными записями хранения
По умолчанию AzCopy выполняет асинхронное копирование данных между двумя конечными точками хранилища. Таким образом копируется hello копирования операция выполняется в фоновом режиме hello, используя запасную пропускную способность емкости, которая имеет нет соглашения об уровне ОБСЛУЖИВАНИЯ с точки зрения быстродействия большого двоичного объекта. 

Hello `--sync-copy` параметр гарантирует, что операция копирования hello возвращает согласованные скорость. AzCopy выполняет копирование синхронной hello по загрузке больших двоичных объектов hello toocopy из hello указан источник toolocal памяти и передача их toohello местом назначения хранилища больших двоичных объектов.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`может создать копию tooasynchronous исходящих дополнительных затрат по сравнению. Привет, рекомендованный подход является toouse этот параметр на виртуальной Машине Azure, hello же регионе, что ваш источник учетной записи tooavoid исходящих затраты на хранение.

## <a name="file-download"></a>Файл: скачивание
### <a name="download-single-file"></a>Скачивание одного файла

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Если источником является Azure файловый ресурс, то необходимо указать hello точное имя файла, hello (*например* `abc.txt`) toodownload один файл, или задайте параметр `--recursive` toodownload все файлы в папке hello рекурсивно. Попытка toospecify и шаблону файла и параметр `--recursive` вместе приведет к ошибке.

### <a name="download-all-files"></a>Скачивание всех файлов

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Обратите внимание на то, что пустые папки не скачиваются.

## <a name="file-upload"></a>Файл: отправка
### <a name="upload-single-file"></a>Отправка одного файла

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Отправка всех файлов

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Обратите внимание на то, что пустые папки не передаются.

### <a name="upload-files-matching-specified-pattern"></a>Отправка файлов, соответствующих указанному шаблону

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>Файл: копирование
### <a name="copy-across-file-shares"></a>Копирование общих файловых ресурсов

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
При копировании файла между файловыми ресурсами выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-tooblob"></a>Копирование из файла tooblob общей папки

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
При копировании файла из файла tooblob общего ресурса, [копирование на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) выполняется операция.

### <a name="copy-from-blob-toofile-share"></a>Скопируйте из папки toofile больших двоичных объектов

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
При копировании файлов из папки toofile больших двоичных объектов, [копирование на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) выполняется операция.

### <a name="synchronously-copy-files"></a>Синхронное копирование файлов
Можно указать hello `--sync-copy` синхронно параметр toocopy данных из хранилища файлов tooFile хранилища, tooBlob хранения файлов хранилища или tooFile хранилища больших двоичных объектов хранилища. AzCopy по загрузке hello источника данных toolocal памяти и передачи их toodestination выполняет этой операции. В этом случае взимается стандартная плата за исходящий трафик.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

При копировании из хранилища файлов tooBlob хранения типа больших двоичных объектов по умолчанию hello блочного BLOB-объекта, пользователь может указать параметр `/BlobType:page` toochange hello конечного большого двоичного объекта типа.

Обратите внимание, что `--sync-copy` может создавать дополнительных исходящих стоимости сравнение tooasynchronous копии. Привет, рекомендованный подход является toouse этот параметр на виртуальной Машине Azure, hello же регионе, что ваш источник учетной записи tooavoid исходящих затраты на хранение.

## <a name="other-azcopy-features"></a>Другие функции AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Копирование данных, не существует в месте назначения hello
Hello `--exclude-older` и `--exclude-newer` параметры позволяют ресурсы старого или более нового источника tooexclude копируются, соответственно. Если требуется только ресурсы toocopy источника, которые не существуют в конечном hello, можно указать оба параметра в hello команды AzCopy:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Использование конфигурации параметров командной строки файл toospecify

```azcopy
azcopy --config-file "azcopy-config.ini"
```

В файл конфигурации можно добавить параметры командной строки AzCopy. AzCopy процессы hello параметры в файле hello, как если бы они были указаны в командной строке hello, выполнение прямых подстановки с hello содержимое файла hello.

Предположим, файл конфигурации с именем `copyoperation`, содержащий следующие строки hello. Каждый параметр AzCopy можно указать как в одной строке,

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

так и в разных:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy завершается неудачей, если параметр hello разбиты на две строки, как показано ниже для hello `--source-key` параметр:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Указание подписи общего доступа (SAS)

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

Можно также задать SAS для контейнера hello URI:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

Обратите внимание, что AzCopy в настоящее время поддерживает только hello [SAS для учетной записи](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Папка файлов журнала
Каждый раз, когда выдачи команды tooAzCopy, он проверяет, существует ли файл журнала в папке по умолчанию hello, или существует ли в папке, указанного с помощью этого параметра. Если файл журнала hello не существует в любом месте, AzCopy считает новые операции hello и создает новый файл журнала.

Если существует файл журнала hello, AzCopy проверяет, соответствует ли hello командной строки, что вы ввод hello командной строки в файле журнала hello. Если две командные строки hello совпадают, AzCopy возобновляет hello незавершенные операции. Если они не совпадают, AzCopy запрашивает пользователя tooeither перезаписать hello файла журнала toostart новую операцию или toocancel hello текущей операции.

Если необходимо использовать расположение по умолчанию hello toouse для файла журнала hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Если параметр опущен `--resume`, или задайте параметр `--resume` без hello путь к папке, как показано выше, AzCopy создает файл журнала hello в расположении по умолчанию hello, а именно `~\Microsoft\Azure\AzCopy`. Если уже существует файл журнала hello AzCopy возобновляет hello операции на основе файла журнала hello.

Если нужно toospecify пользовательское расположение для файла журнала hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

Этот пример создает файл журнала hello, если он еще не существует. Если он существует, AzCopy возобновляет hello операции на основе файла журнала hello.

Tooresume операции AzCopy повторите hello в одной команде. AzCopy для Linux запросит подтверждение.

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Вывод подробных журналов

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Укажите число hello toostart параллельных операций
Параметр `--parallel-level` указывает hello количество параллельных копирования операций. По умолчанию AzCopy запускается определенное число передачи пропускная способность hello tooincrease параллельных операций. Hello число параллельных операций будет равно числу процессоров, у вас есть hello восемь раз. При выполнении AzCopy в сети с низкой пропускной способностью, можно указать меньшее значение для--ошибка tooavoid параллельного уровень конкуренции ресурсов.

[!TIP]
>Полный список tooview hello параметров AzCopy извлечь «azcopy — справки» меню.

## <a name="known-issues-and-best-practices"></a>Известные проблемы и рекомендации
### <a name="error-net-core-is-not-found-in-hello-system"></a>Ошибка: .NET Core не найден в системе hello.
Если возникнет сообщение о том, что .NET Core не установлен в системе hello hello путь toohello .NET двоичного файла `dotnet` могут отсутствовать.

В заказ tooaddress эту проблему, найдите hello .NET двоичного файла в системе hello:
```bash
sudo find / -name dotnet
```

Hello путь toohello dotnet возвращает двоичные. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Теперь добавьте эту переменную пути toohello пути. Для вызова sudo изменение secure_path toocontain hello путь toohello dotnet двоичные:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

В этом примере переменная secure_path имеет следующий вид.

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Для текущего пользователя hello измените.bash_profile/.profile tooinclude hello путь toohello dotnet в переменную PATH двоичные файлы 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

Убедитесь, что теперь компонент .NET Core указан в переменной PATH.
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>Ошибка при установке AzCopy
При возникновении проблем с установкой AzCopy, попробуйте извлечь с помощью скрипта bash hello в hello AzCopy toorun `azcopy` папки.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Ограничение одновременных операций записи при копировании данных
При копировании больших двоичных объектов или файлов с помощью AzCopy, имейте в виду, возможно, изменение другое приложение hello данных при копировании его. Если это возможно убедитесь, hello данных при копировании не изменяется во время операции копирования hello. Например при копировании виртуальный жесткий ДИСК, связанный с виртуальной машины Azure, убедитесь, что нет других приложений в настоящее время пишете toohello виртуального жесткого диска. Toodo хорошим способом это по аренде toobe ресурсов hello копируются. Кроме того можно сначала создать моментальный снимок виртуального жесткого диска hello и скопируйте hello моментального снимка.

Если не может помешать записи tooblobs или файлы, пока они копируются, то следует помнить, заданием hello hello время завершения работы других приложений, hello скопированных ресурсов может больше нет полной четности с ресурсами источника hello.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Запускайте один экземпляр AzCopy на одном компьютере.
AzCopy является использование hello спроектированный toomaximize скорость передачи данных ресурсов tooaccelerate машины hello, мы рекомендуем запустить только один экземпляр AzCopy на одном компьютере и укажите параметр hello `--parallel-level` при необходимости несколько параллельных операций. Для получения дополнительных сведений введите `AzCopy --help parallel-level` hello командной строки.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о хранилище Azure и AzCopy см. в разделе hello следующие ресурсы:

### <a name="azure-storage-documentation"></a>Документация по хранилищу Azure:
* [Введение tooAzure хранилища](storage-introduction.md)
* [создать учетную запись хранения;](storage-create-storage-account.md)
* [Управление ресурсами хранилища BLOB-объектов Azure с помощью обозревателя хранилищ (предварительная версия)](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [С помощью hello Azure CLI 2.0 со службой хранилища Azure](storage-azure-cli.md)
* [Как toouse хранилища BLOB-объектов из C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Как toouse хранилища BLOB-объектов из Java](storage-java-how-to-use-blob-storage.md)
* [Как toouse хранилища BLOB-объектов из Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Как toouse хранилища BLOB-объектов из Python](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Записи блога по хранилищу Azure:
* [Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/) (Объявление о выпуске предварительной версии AzCopy для Linux)
* [Введение в предварительную версию библиотеки движения данных в хранилище Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: введение в синхронное копирование и настраиваемый тип содержимого](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: выпуск общедоступной версии AzCopy 3.0 и предварительной версии AzCopy 4.0 с поддержкой таблиц и файлов](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: оптимизированные сценарии для крупномасштабного копирования](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: поддержка геоизбыточного хранилища для доступа с правом чтения](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy – Transfer data with re-startable mode and SAS Token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) (AzCopy: передача данных с использованием перезапускаемого режима и маркера SAS)
* [AzCopy: использование копирования больших двоичных объектов между разными учетными записями](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: отправка и скачивание файлов для больших двоичных объектов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

