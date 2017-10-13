---
title: "Копирование или перемещение данных в службу хранилища Azure с помощью AzCopy для Windows | Документация Майкрософт"
description: "Утилита AzCopy для Windows позволяет копировать и перемещать данные в содержимое BLOB-объектов, таблиц и файлов и из него. Копируйте данные в хранилище Azure из локальных файлов, а также внутри учетной записи хранения и из одной такой учетной записи в другую. Легко переносите данные в хранилище Azure."
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
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: 1a4c52babe76e59eacb30e8be91ed934cdbe305b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a>Перенос данных с помощью AzCopy для Windows
AzCopy — это служебная программа командной строки. Она предназначена для копирования данных из хранилища BLOB-объектов, хранилища файлов и хранилища таблиц Microsoft Azure (и обратно) с помощью простых команд, обеспечивающих оптимальную производительность. Кроме того, она позволяет копировать данные из одного объекта в другой в пределах одной учетной записи хранения или из одной такой записи в другую.

Существуют две версии AzCopy, которые можно скачать. Служебная программа AzCopy для Windows основана на платформе .NET Framework и использует параметры командной строки в формате Windows. Служебная программа [AzCopy для Linux](storage-use-azcopy-linux.md) основана на платформе .NET Core, которая нацелена на платформы Linux, использующие параметры командной строки в формате POSIX. В этой статье рассматривается AzCopy для Windows.

## <a name="download-and-install-azcopy-on-windows"></a>Скачивание и установка AzCopy для Windows

Скачайте [последнюю версию AzCopy для Windows](http://aka.ms/downloadazcopy).

После установки AzCopy для Windows с помощью установщика откройте командное окно и перейдите к каталогу установки AzCopy на компьютере, где располагается исполняемый файл `AzCopy.exe`. При необходимости можно добавить место установки AzCopy к системному пути. По умолчанию инструмент AzCopy установлен в `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` или `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Написание первой команды AzCopy

В командах AzCopy используется следующий базовый синтаксис:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

В приведенных ниже примерах описаны разные сценарии копирования данных из хранилища больших двоичных объектов, файлов и таблиц Microsoft Azure (и обратно). Подробное объяснение параметров, используемых в каждом примере, см. в разделе [Общие сведения о параметрах](#azcopy-parameters).

## <a name="download-blobs-from-blob-storage"></a>Скачивание больших двоичных объектов из хранилища BLOB-объектов

Рассмотрим несколько способов скачивания больших двоичных объектов с помощью AzCopy.

### <a name="download-a-single-blob"></a>Скачивание одного большого двоичного объекта

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Обратите внимание: если папка `C:\myfolder` не существует, AzCopy создаст ее и скачает `abc.txt ` в эту новую папку.

### <a name="download-a-single-blob-from-the-secondary-region"></a>Скачивание одного большого двоичного объекта из дополнительного региона

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Обратите внимание, что для доступа к дополнительному региону необходимо включить геоизбыточное хранилище с доступом только для чтения.

### <a name="download-all-blobs-in-a-container"></a>Скачивание всех больших двоичных объектов в контейнере

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Предположим, что в указанном контейнере находятся следующие BLOB-объекты:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

После скачивания в каталог `C:\myfolder` будут помещены следующие файлы:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Если не задать параметр `/S`, большие двоичные объекты не будут скачаны.

### <a name="download-blobs-with-a-specific-prefix"></a>Скачивание больших двоичных объектов с определенным префиксом

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Предположим, что в указанном контейнере находятся следующие BLOB-объекты: Будут скачаны все большие двоичные объекты, имя которых начинается с префикса `a`:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

После скачивания в папку `C:\myfolder` будут помещены следующие файлы:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

Префикс применяется к виртуальному каталогу, который формирует первую часть имени большого двоичного объекта. В указанном выше примере виртуальный каталог не соответствует заданному префиксу и поэтому не скачивается. Кроме того, если не задан параметр `\S`, то AzCopy не скачивает большие двоичные объекты.

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a>Установка одинакового времени последнего изменения для экспортированных файлов и исходных больших двоичных объектов

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

Исключить большие двоичные объекты из операции скачивания вы можете также на основе времени их последнего изменения. Например, если нужно исключить большие двоичные объекты, измененные в то же время, что и конечный файл, или позднее, добавьте параметр `/XN`:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

Если нужно исключить большие двоичные объекты, измененные в то же время, что и конечный файл, или раньше, добавьте параметр `/XO`:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="upload-blobs-to-blob-storage"></a>Отправка больших двоичных объектов в хранилище BLOB-объектов

Рассмотрим несколько способов отправки больших двоичных объектов с помощью AzCopy.

### <a name="upload-a-single-blob"></a>Отправка одного большого двоичного объекта

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Если указанный контейнер назначения не существует, AzCopy создаст его и передаст в него файл.

### <a name="upload-a-single-blob-to-a-virtual-directory"></a>Отправка одного большого двоичного объекта в виртуальный каталог

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Если указанный виртуальный каталог не существует, AzCopy скачает файл и включит имя виртуального каталога в его имя (*например*, `vd/abc.txt` в указанном выше примере).

### <a name="upload-all-blobs-in-a-folder"></a>Отправка всех больших двоичных объектов в папке

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Выбор параметра `/S` обеспечивает рекурсивную передачу указанного каталога в хранилище BLOB-объектов. Это означает, что передаются также все вложенные папки и файлы. Например, предположим, что следующие файлы находятся в папке `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Когда передача завершится, в контейнер будут помещены следующие файлы:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Если вы не укажете параметр `/S`, программа AzCopy не выполнит отправку рекурсивно. Когда передача завершится, в контейнер будут помещены следующие файлы:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-blobs-matching-a-specific-pattern"></a>Отправка больших двоичных объектов, соответствующих определенному шаблону

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Предположим, что следующие файлы размещены в папке `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Когда передача завершится, в контейнер будут помещены следующие файлы:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Если вы не укажете параметр `/S`, программа AzCopy отправит только большие двоичные объекты, находящиеся вне виртуального каталога:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a>Задание типа содержимого MIME целевого большого двоичного объекта

По умолчанию AzCopy задает для типа содержимого целевого большого двоичного объекта значение `application/octet-stream`. Начиная с версии 3.1.0 вы можете задать тип содержимого с помощью параметра `/SetContentType:[content-type]`. Этот синтаксис задает тип содержимого для всех больших двоичных объектов в операции отправки.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Если вы задали параметр `/SetContentType`, не указав значения, AzCopy задаст тип содержимого для каждого большого двоичного объекта или файла в соответствии с расширением файла.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="copy-blobs-in-blob-storage"></a>Копирование больших двоичных объектов в хранилище BLOB-объектов

Рассмотрим несколько способов копирования больших двоичных объектов из одного расположения в другое с помощью AzCopy.

### <a name="copy-a-single-blob-from-one-container-to-another-within-the-same-storage-account"></a>Копирование одного большого двоичного объекта из одного контейнера в другой в одной учетной записи хранения 

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

При копировании большого двоичного объекта в пределах учетной записи хранения выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .

### <a name="copy-a-single-blob-from-one-storage-account-to-another"></a>Копирование одного большого двоичного объекта из одной учетной записи хранения в другую

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

При копировании большого двоичного объекта между различными учетными записями хранения выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .

### <a name="copy-a-single-blob-from-the-secondary-region-to-the-primary-region"></a>Копирование одного большого двоичного объекта из дополнительного региона в основной

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Обратите внимание, что для доступа к дополнительному хранилищу необходимо включить геоизбыточное хранилище с доступом только для чтения.

### <a name="copy-a-single-blob-and-its-snapshots-from-one-storage-account-to-another"></a>Копирование одного большого двоичного объекта и его моментальных снимков из одной учетной записи хранения в другую

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

После выполнения копирования целевой контейнер будет содержать большой двоичный объект и его моментальные снимки. Предположим, что большой двоичный объект в приведенном выше примере имеет два моментальных снимка, тогда контейнер будет содержать следующий большой двоичный объект и моментальные снимки:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="copy-all-blobs-in-a-container-to-another-storage-account"></a>Копирование всех больших двоичных объектов в контейнере в другую учетную запись хранения 

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 
/Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /S
```

Если задать параметр /S, содержимое указанного контейнера отправится рекурсивно. Дополнительные сведения и пример см. в разделе [Отправка всех больших двоичных объектов в папке](#upload-all-blobs-in-a-folder).

### <a name="synchronously-copy-blobs-from-one-storage-account-to-another"></a>Синхронное копирование больших двоичных объектов из одной учетной записи хранения в другую

По умолчанию AzCopy выполняет асинхронное копирование данных между двумя конечными точками хранилища. Таким образом, операция копирования выполняется в фоновом режиме, используя свободную пропускную способность, для которой не предусмотрено соглашение об уровне обслуживания касательно скорости копирования большого двоичного объекта, и AzCopy будет периодически проверять состояние операции копирования до ее завершения или сбоя.

Параметр `/SyncCopy` обеспечивает постоянную скорость операции копирования. AzCopy выполняет синхронное копирование, при котором большие двоичные объекты копируются из указанного источника в локальную память путем скачивания, а затем загружаются в целевое хранилище больших двоичных объектов.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

Использование параметра `/SyncCopy` может повлечь дополнительные затраты на исходящие данные по сравнению с асинхронным копированием. Во избежание таких затрат мы советуем использовать этот параметр в виртуальных машинах Azure, которые находятся в одном регионе с вашей учетной записью хранения.

## <a name="download-files-from-file-storage"></a>Скачивание файлов из хранилища файлов

Рассмотрим несколько способов скачивания файлов с помощью AzCopy.

### <a name="download-a-single-file"></a>Скачивание одного файла

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Если исходный файл для копирования находится в общей папке Azure, необходимо указать либо точное имя файла (*например*, `abc.txt`) для скачивания одного файла, либо параметр `/S` для рекурсивного скачивания всех файлов в общей папке. Попытка одновременно задать шаблон файла и параметр `/S` приводит к ошибке.

### <a name="download-all-files-in-a-directory"></a>Скачивание всех файлов в каталоге

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Обратите внимание на то, что пустые папки не скачиваются.

## <a name="upload-files-to-an-azure-file-share"></a>Отправка файлов в общую папку файлов Azure

Рассмотрим несколько способов отправки файлов с помощью AzCopy.

### <a name="upload-a-single-file"></a>Отправка одного файла

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files-in-a-folder"></a>Отправка всех файлов в папке

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Обратите внимание на то, что пустые папки не отправляются.

### <a name="upload-files-matching-a-specific-pattern"></a>Отправка файлов, соответствующих определенному шаблону

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="copy-files-in-file-storage"></a>Копирование файлов в хранилище файлов

Рассмотрим несколько способов копирования файлов в общую папку Azure с помощью AzCopy.

### <a name="copy-from-one-file-share-to-another"></a>Копирование из одной общей папки в другую

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
При копировании файла между файловыми ресурсами выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-an-azure-file-share-to-blob-storage"></a>Копирование из общей папки Azure в хранилище BLOB-объектов

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
При копировании файла из файлового ресурса в большой двоичный объект выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-a-blob-from-blob-storage-to-an-azure-file-share"></a>Копирование большого двоичного объекта из хранилища BLOB-объектов в общую папку Azure

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
При копировании файла из большого двоичного объекта в общую папку выполняется операция [копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="synchronously-copy-files"></a>Синхронное копирование файлов

Пользователь также может указать параметр `/SyncCopy` для синхронного копирования данных из хранилища файлов в хранилище файлов, из хранилища файлов в хранилище BLOB-объектов, а также из хранилища BLOB-объектов в хранилище файлов. AzCopy сделает это, скачивая данные источника в локальную память и отправляя их в место назначения. Взимается стандартная плата за исходящий трафик.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

При копировании из хранилища файлов в хранилище BLOB-объектов пользователь может указать параметр `/BlobType:page` для изменения типа большого двоичного объекта назначения. По умолчанию используется блочный BLOB-объект.

Обратите внимание на то, что параметр `/SyncCopy` может повлечь дополнительные затраты на исходящий трафик по сравнению с асинхронным копированием. Во избежание таких затрат мы советуем использовать этот режим на виртуальных машинах Azure, которые находятся в одном регионе с исходной учетной записью хранения.

## <a name="export-data-from-table-storage"></a>Экспорт данных из хранилища таблиц

Рассмотрим пример экспорта данных из хранилища таблиц Azure с помощью AzCopy.

### <a name="export-a-table"></a>Экспорт таблицы

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy создает файл манифеста в заданной целевой папке. Файл манифеста используется в ходе операции для обнаружения нужных файлов и проверки данных. В файле описания по умолчанию используется следующее соглашение о наименовании:

    <account name>_<table name>_<timestamp>.manifest

Пользователь может также указать имя файла описания в параметре `/Manifest:<manifest file name>`.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-an-export-from-table-storage-into-multiple-files"></a>Разделение на несколько файлов для экспорта из хранилища таблиц

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy использует *индекс тома* в именах разделенных файлов для того, чтобы отличить один файл от другого. Индекс тома состоит из двух частей: *индекс диапазонов ключей секций* и *индекс разделенного файла*. Оба индекса отсчитываются, начиная с нуля.

Индекс диапазонов ключей разделов равен 0, если пользователь не укажет параметр `/PKRS`.

Предположим, например, что AzCopy создает два файла данных после того, как пользователь задал значение параметра `/SplitSize`. В таком случае конечные имена файлов могут выглядеть следующим образом:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Обратите внимание, что минимальное возможное значение для `/SplitSize` составляет 32 МБ. Если в качестве назначения задано хранилище BLOB-объектов, AzCopy разделит файл данных, как только размер файла достигнет предельного значения (200 ГБ), вне зависимости от того, задал ли пользователь параметр `/SplitSize`.

### <a name="export-a-table-to-json-or-csv-data-file-format"></a>Экспорт таблицы в файл данных формата JSON или CSV

По умолчанию AzCopy экспортирует таблицы в файлы данных в формате JSON. Чтобы экспортировать таблицы в формате JSON или CSV, вы можете задать параметр `/PayloadFormat:JSON|CSV`.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

При указании формата полезных данных CSV программа AzCopy создает файл схемы с расширением `.schema.csv` для каждого файла данных.

### <a name="export-table-entities-concurrently"></a>Экспорт объектов таблицы в несколько потоков

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

Если пользователь задал параметр `/PKRS`, AzCopy начнет выполнение параллельных операций для экспорта сущностей. Каждая операция экспортирует объем данных равный значению объема, указанного в индексе диапазонов ключей секций.

Обратите внимание на то, что количество одновременных операций можно контролировать с помощью параметра `/NC`. При копировании сущностей таблиц AzCopy использует информацию о количестве основных процессоров в качестве значения `/NC` по умолчанию для параметра `/NC`, даже если параметр не задан. Если пользователь задал параметр `/PKRS`, AzCopy использует меньшее из двух значений (индекса диапазонов ключей разделов и явно или неявно заданный параметр количества одновременных операций), чтобы определить количество одновременных операций, которые можно запустить. Для получения более подробной информации введите в командной строке `AzCopy /?:NC` .

### <a name="export-a-table-to-blob-storage"></a>Экспорт таблицы в хранилище BLOB-объектов

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy создает файл данных в формате JSON в контейнере больших двоичных объектов в соответствии с соглашением об именовании:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

Созданный JSON-файл следует формату полезных метаданных. За более подробной информацией о формате полезных данных обратитесь к разделу [Формат полезных данных для служб работы с таблицами](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Обратите внимание: при экспорте таблиц в большие двоичные объекты программа AzCopy скачивает объекты таблицы в локальные временные файлы данных и отправляет эти объекты в большой двоичный объект. Эти временные файлы данных помещаются в папку с файлами журнала с путем по умолчанию "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>". Вы можете указать параметр /Z:[journal-file-folder], чтобы изменить расположение папки файлов журнала и таким образом изменить расположение временных файлов данных. Размер временных файлов данных определяется по размеру сущностей таблицы и размеру, указанному в параметре /SplitSize. Хотя временный файл данных на локальном диске будет немедленно удален после передачи в большой двоичный объект, убедитесь, что на диске достаточно места для хранения этих временных файлов данных до удаления.

## <a name="import-data-into-table-storage"></a>Импорт данных в хранилище таблиц

Рассмотрим пример импорта данных в хранилище таблиц Azure с помощью AzCopy.

### <a name="import-a-table"></a>Импорт таблицы

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Параметр `/EntityOperation` определяет способ размещения данных в таблице. Возможные значения:

* `InsertOrSkip`: пропускает существующую сущность или вставляет новую, если сущности нет в таблице.
* `InsertOrMerge`: объединяет существующую сущность или вставляет новую, если сущности нет в таблице.
* `InsertOrReplace`: заменяет существующую сущность или вставляет новую, если сущности нет в таблице.

Обратите внимание на то, что вы не можете задать значение параметра `/PKRS` в сценарии импорта данных. В отличие от сценария экспорта данных, в котором необходимо задавать параметр `/PKRS` для начала параллельных операций, при импорте таблиц программа AzCopy задает параметр параллельных операций по умолчанию. Количество потоков по умолчанию соответствует количеству основных процессоров. Однако вы можете задать свое значение с помощью параметра `/NC`. Для получения более подробной информации введите в командной строке `AzCopy /?:NC` .

Обратите внимание, что программа AzCopy поддерживает импорт только для формата JSON, но не для формата CSV. AzCopy не поддерживает импорт таблиц из созданных пользователями JSON-файла и файла манифеста. Оба файла должны поступить в результате экспорта таблицы AzCopy. Чтобы избежать ошибок, не изменяйте экспортированный JSON-файл и файл манифеста.

### <a name="import-entities-into-a-table-from-blob-storage"></a>Импорт сущностей в таблицу из хранилища BLOB-объектов

Предположим, контейнер больших двоичных объектов содержит следующее: JSON-файл, представляющий таблицу Azure, и сопутствующий файл манифеста.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Чтобы импортировать объекты в таблицу с помощью файла манифеста в контейнере больших двоичных объектов, вы можете выполнить такие команды:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Другие функции AzCopy

Давайте рассмотрим некоторые другие функции AzCopy.

### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a>Копирование только тех данных, которых нет в целевой папке

Предотвратить копирование старого или нового ресурса позволяют параметры `/XO` и `/XN` соответственно. Если нужно скопировать только те исходные ресурсы, которых нет в целевой папке, в команде AzCopy вы можете указать оба параметра:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Обратите внимание, что эта функция не поддерживается, если источником или местом назначения является таблица.

### <a name="use-a-response-file-to-specify-command-line-parameters"></a>Использование файла ответа для задания параметров командной строки

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

В файл ответа можно включить параметры командной строки AzCopy. AzCopy обрабатывает параметры в файле, как если бы он были заданы в командной строке, выполняя прямую замену содержимого файла.

Предположим, у нас имеется файл ответа с именем `copyoperation.txt`, содержащий следующие строки: Каждый параметр AzCopy можно указать как в одной строке,

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

так и в разных:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

При выполнении AzCopy возникнет ошибка, если разделить параметр на две строки, как показано ниже на примере параметра `/sourcekey`.

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a>Использование нескольких файлов ответа для выбора параметров командной строки

Предположим, что у нас имеется файл ответа с именем `source.txt`, который указывает исходный контейнер:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

И файл ответа с именем `dest.txt`, который указывает папку назначения в файловой системе:

    /Dest:C:\myfolder

А также файл ответа с именем `options.txt`, определяющий параметры для AzCopy:

    /S /Y

Чтобы вызвать AzCopy с этими файлами ответов, размещенными в каталоге `C:\responsefiles`, используйте команду:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy обрабатывает эту команду, как если бы все индивидуальные параметры были включены в командную строку:

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Указание подписи общего доступа (SAS)

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

Кроме того, вы можете указать SAS в коде URI контейнера:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Папка файлов журнала

При каждом вводе команды для AzCopy выполняется проверка на наличие файла журнала в папке по умолчанию или в папке, которая была задана с помощью данного параметра. Если в обоих местах файл журнала отсутствует, AzCopy воспринимает операцию как новую и создает новый файл журнала.

Если файл журнала существует, AzCopy проверяет, соответствует ли введенная командная строка командной строке в файле журнала. Если две командные строки совпадают, AzCopy возобновляет незавершенную операцию. Если они не совпадают, вам будет предложено либо перезаписать файл журнала, чтобы начать новую операцию, либо отменить текущую операцию.

Использование расположения по умолчанию для файла журнала.

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Если опустить параметр`/Z` или задать параметр `/Z` без пути папки, как указано выше, AzCopy создает файл журнала в расположении по умолчанию: `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Если файл журнала уже существует, то AzCopy возобновляет операцию на основе файла журнала.

Использование настраиваемого расположения для файла журнала.

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

В этом примере создается файл журнала, если он еще не существует. Если такой файл существует, то AzCopy возобновляет операцию на основе файла журнала.

Возобновление операции AzCopy.

```azcopy
AzCopy /Z:C:\journalfolder\
```

В этом примере возобновляется последняя операция, при завершении которой произошел сбой.

### <a name="generate-a-log-file"></a>Создание файла журнала

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Если задать параметр `/V` без указания пути файла к журналу с подробными данными, AzCopy создает файл журнала в расположении по умолчанию: `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

В противном случае можно создать файл журнала в настраиваемом расположении:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Обратите внимание, что если задать относительный путь после параметра `/V`, например `/V:test/azcopy1.log`, то журнал с подробными данными создается в текущем рабочем каталоге в подпапке с именем `test`.

### <a name="specify-the-number-of-concurrent-operations-to-start"></a>Задание количества одновременных операций для запуска

Параметр `/NC` задает количество одновременных операций копирования. По умолчанию AzCopy запускает несколько одновременных операций для увеличения скорости передачи данных. При работе с таблицами количество одновременных операций равно количеству процессоров. При работе с большими двоичными объектами и файлами количество одновременных операций в восемь раз превышает количество процессоров. При выполнении AzCopy в сети с низкой пропускной способностью можно задать меньшее количество для этого параметра (/NC), чтобы избежать сбоев, вызванных конкуренцией за ресурсы.

### <a name="run-azcopy-against-the-azure-storage-emulator"></a>Запуск AzCopy с использованием эмулятора хранения Azure

Вы можете запустить программу AzCopy с использованием [эмулятора хранения Azure](storage-use-emulator.md) для больших двоичных объектов.

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

Вы также можете запустить ее для таблиц.

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>Параметры AzCopy

Параметры для AzCopy описаны ниже. Вы можете использовать одну из следующих команд для получения справки во время работы с AzCopy:

* Подробная справка по командной строке AzCopy: `AzCopy /?`
* Подробная справка по параметрам AzCopy: `AzCopy /?:SourceKey`
* Примеры командной строки: `AzCopy /?:Samples`

### <a name="sourcesource"></a>/Source:"source"

Параметр определяет исходные данные для копирования. Источником может быть каталог файловой системы, контейнер BLOB-объектов, виртуальный каталог BLOB-объектов, общая папка файлового хранилища, каталог файлового хранилища или таблица Azure.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="destdestination"></a>/Dest:"destination"

Параметр определяет целевую директорию копирования. Целевой директорией может быть каталог файловой системы, контейнер BLOB-объектов, виртуальный каталог BLOB-объектов, общая папка файлового хранилища, каталог файлового хранилища и таблица Azure.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="patternfile-pattern"></a>/Pattern:"file-pattern"

Параметр определяет шаблон файла, который указывает, какие именно файлы нужно копировать. Поведение дополнительного параметра "/Pattern" определяется местоположением исходных данных, а также наличием параметра "рекурсивный режим". Рекурсивный режим задается с помощью параметра "/S.".

Если определенный источник представляет собой каталог в файловой системе, то используются стандартные подстановочные знаки, и предоставленный шаблон файла сравнивается с файлами в каталоге. При задании параметра "/S." AzCopy также выполняет сравнение определенного шаблона со всеми файлами в любых подпапках каталога.

Если определенный источник представляет собой контейнер BLOB-объектов или виртуальный каталог, то подстановочные знаки не используются. Если задан параметр "/S", то AzCopy интерпретирует заданный шаблон файла как префикс большого двоичного объекта. Если параметр "/S" не задан, то AzCopy выполняет сопоставление шаблона файла с точными именами больших двоичных объектов.

Если исходный файл для копирования находится в общей папке Azure, вам необходимо либо уточнить имя файла (например, abc.txt), либо указать в "/S" параметр рекурсивного копирования всего содержания общей папки. Попытка одновременно задать шаблон файла и параметр /S приводит к ошибке.

В AzCopy используется сопоставление с учетом регистра, в котором /Source представляет собой контейнер больших двоичных объектов или виртуальный каталог больших двоичных объектов, а также сопоставление без учета регистра во всех остальных случаях.

Если шаблон файла не указан, по умолчанию используется шаблон файла *.* для расположения файловой системы или пустой префикс для расположения службы хранилища Azure. Задание нескольких шаблонов не поддерживается.

**Применимо к** большим двоичным объектам и файлам.

### <a name="destkeystorage-key"></a>/DestKey:"storage-key"

Задает ключ учетной записи хранения для ресурса в месте назначения.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="destsassas-token"></a>/DestSAS:"sas-token"

Задает подпись общего доступа (SAS) с правами ЧТЕНИЯ и ЗАПИСИ для контейнера назначения (если применяется). Поместите SAS в двойные кавычки, так как подпись может содержать специальные символы командной строки.

Если ресурс места назначения представляет собой контейнер BLOB-объекта, общую папку или таблицу, можно либо указать эту опцию перед маркером SAS, либо указать SAS как часть пути контейнера BLOB-объекта места назначения, общей папки или URI таблицы, не указывая этой опции.

Если исходное место копирования и место назначения копирования являются BLOB-объектами, то BLOB-объект места назначения должен находиться в той же учетной записи хранилища, что и BLOB-объект исходного места копирования.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="sourcekeystorage-key"></a>/SourceKey:"storage-key"

Задает ключ учетной записи хранения для исходного ресурса.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="sourcesassas-token"></a>/SourceSAS:"sas-token"

Задает подпись общего доступа (SAS) с правами ЧТЕНИЯ и СОЗДАНИЯ СПИСКА для исходного ресурса (если применяется). Поместите SAS в двойные кавычки, так как подпись может содержать специальные символы командной строки.

Если исходный ресурс для копирования является большим двоичным объектом и не предоставляется ни ключ, ни SAS, то контейнер считывается через анонимный доступ.

Если исходный ресурс для копирования является общей папкой или таблицей, необходимо указать ключ или SAS.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="s"></a>/S

Задает рекурсивный режим для операций копирования. В рекурсивном режиме AzCopy копирует все большие двоичные объекты или файлы, соответствующие определенному шаблону файла, в том числе файлы из подпапок.

**Применимо к** большим двоичным объектам и файлам.

### <a name="blobtypeblock--page--append"></a>/BlobType:"block" | "page" | "append"

Определяет, является ли большой двоичный объект места назначения блочным, страничным или расширенным. Этот параметр применяется только при передаче большого двоичного объекта. В противном случае возникает ошибка. Если в качестве места назначения выступает большой двоичный объект и этот параметр не указан, то по умолчанию AzCopy создает блочный BLOB-объект.

**Применимо к** большим двоичным объектам.

### <a name="checkmd5"></a>/CheckMD5

Вычисляет хэш MD5 для загруженных данных и проверяет соответствие хэша MD5, сохраненного в BLOB-объекте, или свойства Content-MD5 файла вычисленному хэшу. Проверка MD5 выключена по умолчанию. Чтобы выполнить проверку MD5 при загрузке данных, необходимо задать этот параметр.

Обратите внимание, что хранилище Azure не гарантирует актуальность хэша MD5, сохраненного для BLOB-объекта или файла. Клиент несет ответственность за обновление MD5 при каждом изменении BLOB-объекта или файла.

AzCopy всегда задает свойство Content-MD5 для BLOB-объекта или файла Azure после отправки его в службу.  

**Применимо к** большим двоичным объектам и файлам.

### <a name="snapshot"></a>/Snapshot

Указывает, передаются ли моментальные снимки. Это параметр действителен только, если в качестве источника используется BLOB-объект.

Передаваемые моментальные снимки BLOB-объекта переименовываются в следующем формате: имя BLOB-объекта (время моментального снимка).расширение.

По умолчанию моментальные снимки не копируются.

**Применимо к** большим двоичным объектам.

### <a name="vverbose-log-file"></a>/V:[verbose-log-file]

Выводит сообщения с подробным состоянием в файл журнала.

По умолчанию файлу журнала с подробными данными в каталоге `%LocalAppData%\Microsoft\Azure\AzCopy` присваивается имя AzCopyVerbose.log. При указании имеющегося местоположения файла для этого параметра подробный журнал добавляется к этому файлу.  

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="zjournal-file-folder"></a>/Z:[journal-file-folder]

Задает папку файла журнала для возобновления операции.

AzCopy всегда поддерживает возобновление, если операция была прервана.

Если этот параметр не указан или указан без пути к папке, AzCopy создает файл журнала в папке по умолчанию, которой является папка %LocalAppData%\Microsoft\Azure\AzCopy.

При каждом вводе команды для AzCopy выполняется проверка на наличие файла журнала в папке по умолчанию или в папке, которая была задана с помощью данного параметра. Если в обоих местах файл журнала отсутствует, AzCopy воспринимает операцию как новую и создает новый файл журнала.

Если файл журнала существует, AzCopy проверяет, соответствует ли введенная командная строка командной строке в файле журнала. Если две командные строки совпадают, AzCopy возобновляет незавершенную операцию. Если они не совпадают, вам будет предложено либо перезаписать файл журнала, чтобы начать новую операцию, либо отменить текущую операцию.

После успешного завершения операции файл журнала удаляется.

Обратите внимание, что возобновление операции из файла журнала, созданного предыдущей версией AzCopy, не поддерживается.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="parameter-file"></a>/@:"parameter-file"

Задает файл, который содержит параметры. AzCopy обрабатывает параметры в файле, как если бы они были заданы в командной строке.

В файле ответа можно либо задать несколько параметров в одной строке, либо задать каждый параметр в отдельной строке. Обратите внимание, что отдельный параметр не может занимать несколько строк.

Файлы ответа могут включать строки комментариев, начинающиеся с символа #.

Можно задать несколько файлов ответов. Однако, следует иметь в виду, что AzCopy не поддерживает вложенных фалов ответов.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="y"></a>/Y

Скрывает все запросы на подтверждение AzCopy.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="l"></a>/L

Задает только операцию перечисления, данные не копируются.

AzCopy интерпретирует использование этого параметра как моделирование запуска команды без параметра /L и подсчитает количество копируемых объектов. Одновременно можно указать параметр /V для вывода подробной информации о копируемых объектах.

Поведение этого параметра также определяется местоположением исходных данных и наличием параметра рекурсивного режима /S и параметра шаблона файла /Pattern.

При использовании этого параметра AzCopy необходимы права на ЧТЕНИЕ и СОЗДАНИЕ СПИСКА для местоположения исходных данных.

**Применимо к** большим двоичным объектам и файлам.

### <a name="mt"></a>/MT

Задает такое же время последнего изменения загруженного файла, как в исходном BLOB-объекте или файле.

**Применимо к** большим двоичным объектам и файлам.

### <a name="xn"></a>/XN

Исключает более новый исходный ресурс. Ресурс не будет копироваться, если исходный файл был изменен в то же время, что и конечный файл, или позднее.

**Применимо к** большим двоичным объектам и файлам.

### <a name="xo"></a>/XO
Исключает более старый исходный ресурс. Ресурс не будет копироваться, если исходный файл был изменен в то же время, что и конечный файл, или раньше.

**Применимо к** большим двоичным объектам и файлам.

### <a name="a"></a>/A

Отправляет только файлы с установленным атрибутом "Архивный".

**Применимо к** большим двоичным объектам и файлам.

### <a name="iarashcnetoi"></a>/IA:[RASHCNETOI]

Передает файлы, содержащие любой из следующих заданных атрибутов.

Доступные атрибуты:

* R — файлы только для чтения
* A — файлы, готовые к архивированию
* S — системные файлы
* H — скрытые файлы
* C — сжатые файлы
* N — обычные файлы
* E — зашифрованные файлы
* T — временные файлы
* O — автономные файлы
* I — неиндексированные файлы

**Применимо к** большим двоичным объектам и файлам.

### <a name="xarashcnetoi"></a>/XA:[RASHCNETOI]

Исключает файлы с любым из следующих установленных атрибутов.

Доступные атрибуты:

* R — файлы только для чтения
* A — файлы, готовые к архивированию
* S — системные файлы
* H — скрытые файлы
* C — сжатые файлы
* N — обычные файлы
* E — зашифрованные файлы
* T — временные файлы
* O — автономные файлы
* I — неиндексированные файлы

**Применимо к** большим двоичным объектам и файлам.

### <a name="delimiterdelimiter"></a>/Delimiter:"delimiter"

Указывает разделитель, используемый для разделения виртуальных каталогов в имени большого двоичного объекта.

По умолчанию AzCopy использует / как разделитель. Однако, AzCopy поддерживает любой общий символ (например, @, # или %) в качестве разделителя. Если необходимо ввести любой из этих специальных символов в командную строку следует заключить имя файла в двойные кавычки.

Этот параметр применяется только для загрузки BLOB-объектов.

**Применимо к** большим двоичным объектам.

### <a name="ncnumber-of-concurrent-operations"></a>/NC:"number-of-concurrent-operations"

Задает количество одновременных операций.

По умолчанию AzCopy запускает несколько одновременных операций для увеличения скорости передачи данных. Обратите внимание, что большое количество одновременных операций в среде с низкой пропускной способностью может переполнить сетевое подключение и помешать полному завершению операций. Регулируйте количество одновременных операций в зависимости от фактической доступной пропускной способности сети.

Верхний лимит количества одновременно выполняемых операций составляет 512.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="sourcetypeblob--table"></a>/SourceType:"Blob" | "Table"

Указывает, что ресурс `source` — это большой двоичный объект, доступный в локальной среде разработки, которая запущена в эмуляторе хранения.

**Применимо к** большим двоичным объектам и таблицам.

### <a name="desttypeblob--table"></a>/DestType:"Blob" | "Table"

Указывает, что ресурс `destination` — это большой двоичный объект, доступный в локальной среде разработки, которая запущена в эмуляторе хранения.

**Применимо к** большим двоичным объектам и таблицам.

### <a name="pkrskey1key2key3"></a>/PKRS:"key1#key2#key3#..."

Разбивает диапазоны ключей секций для обеспечения параллельной передачи данных с целью увеличения скорости экспорта данных.

Если параметр не задан, то AzCopy будет использовать одиночный поток для экспорта данных таблицы. Например, если пользователем задан параметр /PKRS:"aa#bb", то AzCopy начинает три одновременных операции передачи.

Каждая операция экспортирует один из диапазонов ключей секций, как это показано на примере ниже:

  [first-partition-key, aa)

  [aa, bb)

  [bb, last-partition-key]

**Применимо к** таблицам.

### <a name="splitsizefile-size"></a>/SplitSize:"file-size"

Указывает размер разбитого экспортированного файла в МБ, минимальное допустимое значение — 32.

Если этот параметр не задан, то AzCopy поместит экспортированные данные таблицы в один файл.

Если данные таблицы экспортируются в большой двоичный объект и размер экспортированного файла достигает 200 ГБ для большого двоичного объекта, то AzCopy разделяет экспортированный файл, даже если такой параметр не задан.

**Применимо к** таблицам.

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"

Задает поведение импортированных данных таблиц.

* InsertOrSkip — Пропускает существующий объект или вставляет новый, если объект не существует в таблице.
* InsertOrMerg — Объединяет существующий объект или вставляет новый, если объект не существует в таблице.
* InsertOrReplace — Заменяет существующий объект или вставляет новый, если объект не существует в таблице.

**Применимо к** таблицам.

### <a name="manifestmanifest-file"></a>/Manifest:"manifest-file"

Задает файл описания для операций экспорта и импорта таблицы.

Во время операции экспорта этот параметр является необязательным. Если он не указан, AzCopy создаст файл манифеста с предварительно определенным именем.

Этот параметр является обязательным во время операции импорта для обнаружения файлов данных.

**Применимо к** таблицам.

### <a name="synccopy"></a>/SyncCopy

Указывает, копируются ли большие двоичные объекты или файлы синхронно между двумя конечными точками службы хранилища Azure.

По умолчанию AzCopy использует серверное асинхронное копирование. Задайте этот параметр, чтобы выполнить синхронное копирование, при котором большие двоичные объекты или файлы скачиваются в локальную память, а затем передаются в службу хранилища Azure.

Вы можете использовать этот параметр для копирования файлов в хранилище больших двоичных объектов и хранилище файлов или из хранилища больших двоичных объектов в хранилище файлов и наоборот.

**Применимо к** большим двоичным объектам и файлам.

### <a name="setcontenttypecontent-type"></a>/SetContentType:"content-type"

Задает тип содержимого MIME для целевых больших двоичных объектов или файлов.

AzCopy по умолчанию задает тип содержимого для большого двоичного объекта или файла application/octet-stream. Вы можете задать тип содержимого для всех больших двоичных объектов или файлов, указав значение для этого параметра.

Если вы задали этот параметр, не указав значения, AzCopy установит тип содержимого для каждого большого двоичного объекта или содержимого файла в соответствии с расширением файла.

**Применимо к** большим двоичным объектам и файлам.

### <a name="payloadformatjson--csv"></a>/PayloadFormat:"JSON" | "CSV"

Указывает формат файла экспортируемых данных таблицы.

Если этот параметр не указан, по умолчанию AzCopy экспортирует файл данных таблицы в формате JSON.

**Применимо к** таблицам.

## <a name="known-issues-and-best-practices"></a>Известные проблемы и рекомендации

Давайте рассмотрим некоторые известные проблемы и рекомендации.

### <a name="limit-concurrent-writes-while-copying-data"></a>Ограничение одновременных операций записи при копировании данных

При копировании BLOB-объектов или файлов с помощью AzCopy следует иметь в виду, что другое приложение может изменять данные в то время, когда они копируются. Если это возможно, обеспечьте, чтобы во время операции копирования не происходило изменение копируемых данных. Например, при копировании VHD, связанного с виртуальной машиной Azure, убедитесь в том, что никакое другое приложение в это время не записывает данные на VHD. Для этого рекомендуется сдать ресурс, который нужно скопировать, в аренду. В качестве альтернативы можно сначала создать моментальный снимок VHD, а затем скопировать его.

Если не удается предотвратить запись в BLOB-объекты или файлы во время их копирования со стороны других приложений, следует иметь в виду, что к моменту завершения задания скопированные ресурсы могут больше не иметь полного соответствия с исходными ресурсами.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Запускайте один экземпляр AzCopy на одном компьютере.

AzCopy предназначен для максимального использования ресурсов компьютера для ускорения передачи данных. Рекомендуется запускать только один экземпляр AzCopy на одном компьютере и указать параметр `/NC`, если требуется несколько параллельных операций. Для получения более подробной информации введите в командной строке `AzCopy /?:NC` .

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>Включайте FIPS-совместимые алгоритмы MD5 для AzCopy при использовании FIPS-совместимых алгоритмов для шифрования, хэширования и подписывания.

По умолчанию в AzCopy используется реализация .NET MD5 для вычисления MD5 при копировании объектов, но существует ряд требований безопасности, при которых в AzCopy необходимо включать FIPS-совместимую реализацию MD5.

Для этого можно создать файл app.config `AzCopy.exe.config` со свойством `AzureStorageUseV1MD5` и поместить его в папку с файлом AzCopy.exe.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Для свойства AzureStorageUseV1MD5 задайте одно из следующих значений:

* True — значение по умолчанию, AzCopy использует реализацию .NET MD5.
* False — AzCopy использует FIPS-совместимый алгоритм MD5.

По умолчанию FIPS-совместимые алгоритмы отключены для Windows. Вы можете изменить этот параметр политики на своем компьютере. В окне запуска команд (Windows+R) введите secpol.msc, чтобы открыть окно **Локальная политика безопасности**. В окне **настроек безопасности** выберите **Параметры безопасности** > **Локальные политики** > **Параметры безопасности**. Найдите политику **Системная криптография: использовать FIPS-совместимые алгоритмы для шифрования, хэширования и подписывания**. Дважды щелкните ее, чтобы в столбце **Параметр безопасности** отобразилось значение.

## <a name="next-steps"></a>Дальнейшие действия

Для получения дополнительной информации о службе хранилища Azure и AzCopy ознакомьтесь со следующими ресурсами.

### <a name="azure-storage-documentation"></a>Документация по хранилищу Azure:
* [Введение в хранилище Azure](../storage-introduction.md)
* [Использование хранилища BLOB-объектов из .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Использование хранилища файлов из .NET](../storage-dotnet-how-to-use-files.md)
* [Использование табличного хранилища из .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Создание и удаление учетной записи хранения, а также управление ею](../storage-create-storage-account.md)
* [Перенос данных с помощью AzCopy для Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Записи блога по хранилищу Azure:
* [Введение в предварительную версию библиотеки движения данных в хранилище Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: введение в синхронное копирование и настраиваемый тип содержимого](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: выпуск общедоступной версии AzCopy 3.0 и предварительной версии AzCopy 4.0 с поддержкой таблиц и файлов](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: оптимизированные сценарии для крупномасштабного копирования](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: поддержка геоизбыточного хранилища для доступа с правом чтения](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy – Transfer data with re-startable mode and SAS Token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) (AzCopy: передача данных с использованием перезапускаемого режима и маркера SAS)
* [AzCopy: использование копирования больших двоичных объектов между разными учетными записями](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: отправка и скачивание файлов для больших двоичных объектов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)