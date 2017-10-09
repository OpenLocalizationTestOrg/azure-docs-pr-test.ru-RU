---
title: "aaaCopy или переместите tooAzure данные хранилища с помощью AzCopy в Windows | Документы Microsoft"
description: "Используйте hello AzCopy Windows программа toomove или копирования данных tooor из больших двоичных объектов, таблиц и содержимое файла. Копирование данных tooAzure хранилища из локальных файлов или копирования данных в пределах или между учетными записями хранения. Легко перенесите на tooAzure данных хранилища."
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
ms.openlocfilehash: a063a0380b7b8e6b212d0cec276f7d0f421936ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Перенесите данные с помощью hello AzCopy в Windows
AzCopy является командной строки служебная программа, разработанная для копирования данных tooand из хранилища больших двоичных объектов Microsoft Azure, таблицы и файла с помощью простой команды с оптимальной производительностью. Можно скопировать данные из одного объекта tooanother в вашей учетной записи хранения или между учетными записями хранения.

Существуют две версии AzCopy, которые можно скачать. Служебная программа AzCopy для Windows основана на платформе .NET Framework и использует параметры командной строки в формате Windows. Служебная программа [AzCopy для Linux](storage-use-azcopy-linux.md) основана на платформе .NET Core, которая нацелена на платформы Linux, использующие параметры командной строки в формате POSIX. В этой статье рассматривается AzCopy для Windows.

## <a name="download-and-install-azcopy"></a>Скачивание и установка AzCopy
### <a name="azcopy-on-windows"></a>AzCopy для Windows
Загрузите hello [последнюю версию AzCopy в Windows](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Установка в Windows
После установки AzCopy в Windows, с помощью установщика hello, откройте окно командной строки и перейдите toohello AzCopy установочный каталог на компьютере -, где hello `AzCopy.exe` исполняемый файл находится. При желании можно добавить hello AzCopy tooyour системы путь установки. По умолчанию AzCopy установлен слишком`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` или `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Написание первой команды AzCopy
Базовый синтаксис команды AzCopy Hello таков:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Hello следующие примеры демонстрируют различные сценарии для копирования данных tooand из BLOB-объектов Microsoft Azure, файлы и таблицы. См. toohello [AzCopy параметры](#azcopy-parameters) раздел подробное описание параметров hello, используемых в каждой выборке.

## <a name="blob-download"></a>Большой двоичный объект: скачивание
### <a name="download-single-blob"></a>Скачивание одного большого двоичного объекта

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Обратите внимание, что если папка hello `C:\myfolder` не существует, AzCopy создает его и загрузки `abc.txt ` в новую папку hello.

### <a name="download-single-blob-from-secondary-region"></a>Скачивание большого двоичного объекта из дополнительного региона

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.

### <a name="download-all-blobs"></a>Скачивание всех больших двоичных объектов

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Предположим следующее hello большие двоичные объекты находятся в указанном контейнере hello:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

После завершения операции загрузки hello hello каталог `C:\myfolder` включает hello следующие файлы:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Если не задать параметр `/S`, большие двоичные объекты не будут скачаны.

### <a name="download-blobs-with-specified-prefix"></a>Скачивание больших двоичных объектов с указанным префиксом

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Предположим следующее hello большие двоичные объекты находятся в указанном контейнере hello. Все большие двоичные объекты, начинающиеся с префикса hello `a` загружаются:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

После завершения операции загрузки hello hello папку `C:\myfolder` включает hello следующие файлы:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

префикс Hello применяется toohello виртуальному каталогу, который формирует первую часть имени большого двоичного объекта hello hello. В приведенном выше примере hello hello виртуального каталога не соответствует hello указанного префикса, поэтому оно не загружается. Кроме того, если hello параметр `\S` не указан, AzCopy не загружать все большие двоичные объекты.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Задать время последнего изменения hello toobe экспортированные файлы так же, как hello исходный BLOB-объект

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

Большие двоичные объекты можно также исключить из операции загрузки hello, на основе их времени последнего изменения. Например, большие двоичные объекты tooexclude, время последнего изменения — hello же или более новая, чем конечный файл hello, добавить hello `/XN` параметр:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

Или если вы хотите tooexclude BLOB-объектов, время последнего изменения — hello же или более ранней, чем конечный файл hello, добавьте hello `/XO` параметр:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>Большой двоичный объект: отправка
### <a name="upload-single-file"></a>Отправка одного файла

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Если hello указанный контейнер не существует, AzCopy создает эту службу и передачи файла hello в него.

### <a name="upload-single-file-toovirtual-directory"></a>Отправка одного файла каталога toovirtual

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Если hello указанный виртуальный каталог не существует, AzCopy передает hello файл tooinclude hello виртуального каталога в имени (*например*, `vd/abc.txt` в приведенном выше примере hello).

### <a name="upload-all-files"></a>Отправка всех файлов

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Задание параметра `/S` содержимое передачи hello hello указано рекурсивно хранилища tooBlob каталога, то есть также загрузить свои файлы и все вложенные папки. Например, предположим, hello следующие файлы размещаются в папке `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

После завершения операции отправки hello hello контейнер содержит hello следующие файлы:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Если вы не укажете параметр `/S`, программа AzCopy не выполнит отправку рекурсивно. После завершения операции отправки hello hello контейнер содержит hello следующие файлы:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Отправка файлов, соответствующих указанному шаблону

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Предполагается hello следующие файлы размещаются в папке `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

После завершения операции отправки hello hello контейнер содержит hello следующие файлы:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Если вы не укажете параметр `/S`, программа AzCopy отправит только большие двоичные объекты, находящиеся вне виртуального каталога:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Укажите hello MIME-тип содержимого большого двоичного объекта назначения
По умолчанию AzCopy задает тип содержимого hello BLOB-объект назначения, слишком`application/octet-stream`. Начиная с версии 3.1.0, можно явно указать тип содержимого hello через параметр hello `/SetContentType:[content-type]`. Этот синтаксис задает hello-тип содержимого для всех больших двоичных объектов в операции передачи.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

При указании `/SetContentType` без указания значения AzCopy задает каждый BLOB-объект или тип содержимого файла, в соответствии с tooits расширение файла.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>Большой двоичный объект: копирование
### <a name="copy-single-blob-within-storage-account"></a>Копирование большого двоичного объекта в пределах учетной записи хранения

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

При копировании большого двоичного объекта в пределах учетной записи хранения выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .

### <a name="copy-single-blob-across-storage-accounts"></a>Копирование большого двоичного объекта между различными учетными записями хранения

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

При копировании большого двоичного объекта между различными учетными записями хранения выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Копирование одного большого двоичного объекта из области tooprimary дополнительный регион

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Копирование большого двоичного объекта и его моментальных снимков между различными учетными записями хранения

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

После завершения операции копирования hello hello целевой контейнер включает hello большого двоичного объекта и его моментальные снимки. При условии, что большой двоичный объект hello в приведенном выше примере hello имеются два моментальные снимки, hello контейнер включает в себя следующие hello больших двоичных объектов и моментальных снимков:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Синхронное копирование больших двоичных объектов между учетными записями хранения
По умолчанию AzCopy выполняет асинхронное копирование данных между двумя конечными точками хранилища. Таким образом выполняется операция копирования hello в фоновом режиме hello, используя запасную пропускную способность емкости, которая имеет нет соглашения об уровне ОБСЛУЖИВАНИЯ с точки зрения быстродействия большой двоичный объект копируется и AzCopy периодически проверяет состояние копирования hello до завершения или не удалось выполнить копирование hello.

Hello `/SyncCopy` параметр гарантирует, что операция копирования hello возвращает согласованные скорость. AzCopy выполняет копирование синхронной hello по загрузке больших двоичных объектов hello toocopy из hello указан источник toolocal памяти и передача их toohello местом назначения хранилища больших двоичных объектов.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`может создавать дополнительные исходящих стоимости копирования сравниваемых tooasynchronous hello рекомендованный подход является toouse этот параметр на виртуальной Машине Azure, hello же регионе, что ваш источник учетной записи tooavoid исходящих затраты на хранение.

## <a name="file-download"></a>Файл: скачивание
### <a name="download-single-file"></a>Скачивание одного файла

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Если источником является Azure файловый ресурс, то необходимо указать hello точное имя файла, hello (*например* `abc.txt`) toodownload один файл, или задайте параметр `/S` toodownload все файлы в папке hello рекурсивно. Попытка toospecify и шаблону файла и параметр `/S` вместе приведет к ошибке.

### <a name="download-all-files"></a>Скачивание всех файлов

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Обратите внимание на то, что пустые папки не скачиваются.

## <a name="file-upload"></a>Файл: отправка
### <a name="upload-single-file"></a>Отправка одного файла

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Отправка всех файлов

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Обратите внимание на то, что пустые папки не передаются.

### <a name="upload-files-matching-specified-pattern"></a>Отправка файлов, соответствующих указанному шаблону

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>Файл: копирование
### <a name="copy-across-file-shares"></a>Копирование общих файловых ресурсов

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
При копировании файла между файловыми ресурсами выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-tooblob"></a>Копирование из файла tooblob общей папки

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
При копировании файла из файла tooblob общего ресурса, [копирование на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) выполняется операция.


### <a name="copy-from-blob-toofile-share"></a>Скопируйте из папки toofile больших двоичных объектов

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
При копировании файлов из папки toofile больших двоичных объектов, [копирование на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) выполняется операция.

### <a name="synchronously-copy-files"></a>Синхронное копирование файлов
Можно указать hello `/SyncCopy` toocopy данные из хранилища файлов tooFile хранилище, из хранилища файлов tooBlob хранилища, а из хранилища больших двоичных объектов tooFile хранилища синхронно, AzCopy происходит загрузка hello источника данных toolocal памяти и отправьте его снова toodestination. Взимается стандартная плата за исходящий трафик.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

При копировании из хранилища файлов tooBlob хранения типа больших двоичных объектов по умолчанию hello блочного BLOB-объекта, пользователь может указать параметр `/BlobType:page` toochange hello конечного большого двоичного объекта типа.

Обратите внимание, что `/SyncCopy` может создавать дополнительных исходящих стоимости сравнение копирования tooasynchronous, hello рекомендуется toouse виртуальную Машину Azure, которая находится в hello hello этот параметр в одном регионе вашей исходной учетной записи tooavoid исходящих затраты на хранение.

## <a name="table-export"></a>Таблица: экспорт
### <a name="export-table"></a>Экспорт таблицы

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy записывает файл манифеста toohello указанную папку. файл манифеста Hello используется в файлах hello импорта процесса toolocate hello необходимые данные и выполнить проверку данных. файл манифеста Hello используется следующее соглашение об именовании по умолчанию hello:

    <account name>_<table name>_<timestamp>.manifest

Пользователь также может указать параметр hello `/Manifest:<manifest file name>` имя файла манифеста tooset hello.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>Разбивка экспорта на несколько файлов

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

Использует AzCopy *индекса объема* в hello разбиение данных имена файлов toodistinguish несколько файлов. индекс объема Hello состоит из двух частей, *индекс диапазона ключа секции* и *индекс разбиение файлов*. Оба индекса отсчитываются, начиная с нуля.

индекс диапазона ключа секции Hello равно 0, если параметр не указан пользователь hello `/PKRS`.

Например, предположим, что после hello пользователь указывает параметр AzCopy создает два файла данных `/SplitSize`. Привет, возникающие в имена файлов данных, может быть:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Обратите внимание, что hello минимально возможное значение для параметра `/SplitSize` — 32 МБ. Если hello указан назначения хранилища больших двоичных объектов, AzCopy разделяет hello файла данных, его размеры при достижении ограничений размера большого двоичного объекта hello (200 ГБ), независимо от того, параметр `/SplitSize` был указан пользователем hello.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Экспорт таблицы tooJSON или CSV-файл данных
AzCopy по умолчанию экспортирует файлы данных tooJSON таблиц. Можно указать параметр hello `/PayloadFormat:JSON|CSV` tooexport hello таблиц в формате JSON или CSV.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

При указании формат полезных данных CSV hello, AzCopy также создает файл схемы с расширением файла `.schema.csv` для каждого файла данных.

### <a name="export-table-entities-concurrently"></a>Экспорт объектов таблицы в несколько потоков

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy начинается сущностей tooexport параллельных операций, когда пользователь hello указывает параметр `/PKRS`. Каждая операция экспортирует объем данных равный значению объема, указанного в индексе диапазонов ключей секций.

Обратите внимание, hello числом одновременных операций также определяется параметром `/NC`. AzCopy использует hello число процессоров core как значение по умолчанию hello `/NC` при копировании сущностей таблицы, даже если `/NC` не указан. Когда пользователь hello указывает параметр `/PKRS`, AzCopy использует hello меньшего количества hello двух значений — раздел диапазонов ключей и явно или неявно заданного параллельных операций - toodetermine hello toostart параллельных операций. Для получения дополнительных сведений введите `AzCopy /?:NC` hello командной строки.

### <a name="export-table-tooblob"></a>Экспорт таблицы tooblob

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy создает файл данных JSON в контейнер больших двоичных объектов hello следующее соглашение об именовании:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

файл данных создан Hello JSON hello формат полезных данных для минимальные метаданные: За более подробной информацией о формате полезных данных обратитесь к разделу [Формат полезных данных для служб работы с таблицами](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Обратите внимание, что при экспорте таблицы tooblobs, AzCopy загружает hello таблицы сущности toolocal временных файлов данных затем загружает blob toohello этих сущностей. Эти временные файлы данных помещаются в папку файла журнала hello hello пути по умолчанию «<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>», можно указать параметр / [папка журнала файла] toochange Z: hello расположение папки для файла журнала и таким образом изменить расположение файлов hello временных данных. Hello временных данных, размер файлов определяется по сущностей таблицы и размеров hello, указанным в /SplitSize параметр hello, несмотря на то, что файл временные данные hello в локальном диске удаляется сразу после ее отправлены toohello больших двоичных объектов, убедитесь в том, что у вас есть Недостаточно локальной на диске места toostore эти временные файлы данных до их удаления.

## <a name="table-import"></a>Таблица: импорт
### <a name="import-table"></a>Импорт таблиц

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

Здравствуйте, параметр `/EntityOperation` показывает, как tooinsert сущностей в hello таблицы. Возможные значения:

* `InsertOrSkip`: Пропускает существующую сущность или вставляет новую сущность, если она не существует в таблице hello.
* `InsertOrMerge`: Объединяет существующую сущность или вставляет новую сущность, если она не существует в таблице hello.
* `InsertOrReplace`: Заменяет существующую сущность или вставляет новую сущность, если она не существует в таблице hello.

Обратите внимание, что нельзя задать параметр `/PKRS` в случае импорта hello. В отличие от сценария экспорта hello, в котором необходимо указать параметр `/PKRS` toostart параллельных операций, AzCopy параллельных операций по умолчанию включается при импорте таблицы. количество параллельных операций запуска по умолчанию Hello равно toohello равно числу процессоров core; Тем не менее, можно указать другое количество одновременных с параметром `/NC`. Для получения дополнительных сведений введите `AzCopy /?:NC` hello командной строки.

Обратите внимание, что программа AzCopy поддерживает импорт только для формата JSON, но не для формата CSV. AzCopy не поддерживает импорт таблиц из созданных пользователями JSON-файла и файла манифеста. Оба файла должны поступить в результате экспорта таблицы AzCopy. ошибки tooavoid, не изменяйте hello экспортируются JSON или файл манифеста.

### <a name="import-entities-tootable-using-blobs"></a>Импорт сущностей tootable использование больших двоичных объектов
Предположим, контейнер больших двоичных объектов содержит следующие hello: JSON-файл, представляющий таблиц Azure и сопутствующий файл манифеста.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

Можно запустить hello, следующая команда tooimport сущностей в таблицу с использованием файла манифеста hello в этом контейнере BLOB-объектов:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Другие функции AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Копирование данных, не существует в месте назначения hello
Hello `/XO` и `/XN` параметры позволяют ресурсы старого или более нового источника tooexclude копируются, соответственно. Если требуется только ресурсы toocopy источника, которые не существуют в конечном hello, можно указать оба параметра в hello команды AzCopy:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Обратите внимание, что это не поддерживается при hello исходной или целевой таблицы.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Использование параметра командной строки toospecify файл ответа

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

В файл ответа можно включить параметры командной строки AzCopy. AzCopy процессы hello параметры в файле hello, как если бы они были указаны в командной строке hello, выполнение прямых подстановки с hello содержимое файла hello.

Предположим, файл ответов с именем `copyoperation.txt`, содержащий следующие строки hello. Каждый параметр AzCopy можно указать как в одной строке,

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

так и в разных:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy завершается неудачей, если параметр hello разбиты на две строки, как показано ниже для hello `/sourcekey` параметр:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Использовать несколько ответа файлы toospecify параметры командной строки
Предположим, что у нас имеется файл ответа с именем `source.txt`, который указывает исходный контейнер:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

И файл ответов с именем `dest.txt` задает целевую папку в файловой системе hello:

    /Dest:C:\myfolder

А также файл ответа с именем `options.txt`, определяющий параметры для AzCopy:

    /S /Y

toocall AzCopy с этими файлами ответа, все они находятся в каталоге `C:\responsefiles`, используйте следующую команду:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy обрабатывает эта команда также, как если бы вы все hello отдельных параметров в командной строке hello.

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Указание подписи общего доступа (SAS)

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

Можно также задать SAS для контейнера hello URI:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Папка файлов журнала
Каждый раз, когда выдачи команды tooAzCopy, он проверяет, существует ли файл журнала в папке по умолчанию hello, или существует ли в папке, указанного с помощью этого параметра. Если файл журнала hello не существует в любом месте, AzCopy считает новые операции hello и создает новый файл журнала.

Если существует файл журнала hello, AzCopy проверяет, соответствует ли hello командной строки, что вы ввод hello командной строки в файле журнала hello. Если две командные строки hello совпадают, AzCopy возобновляет hello незавершенные операции. Если они не совпадают, не запрошенные tooeither перезаписать hello журнала файла toostart новую операцию или toocancel hello текущей операции.

Если необходимо использовать расположение по умолчанию hello toouse для файла журнала hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Если параметр опущен `/Z`, или задайте параметр `/Z` без hello путь к папке, как показано выше, AzCopy создает файл журнала hello в расположении по умолчанию hello, а именно `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Если уже существует файл журнала hello AzCopy возобновляет hello операции на основе файла журнала hello.

Если нужно toospecify пользовательское расположение для файла журнала hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

Этот пример создает файл журнала hello, если он еще не существует. Если он существует, AzCopy возобновляет hello операции на основе файла журнала hello.

Если нужно tooresume операции AzCopy:

```azcopy
AzCopy /Z:C:\journalfolder\
```

В этом примере возобновляется hello последней операции, которая может не toocomplete.

### <a name="generate-a-log-file"></a>Создание файла журнала

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

При указании параметра `/V` без указания пути файла toohello подробный журнал, AzCopy создает файл журнала hello в расположении по умолчанию hello, т. е `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

В противном случае можно создать файл журнала в настраиваемом расположении:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Обратите внимание, что при указании относительного пути, после параметра `/V`, такие как `/V:test/azcopy1.log`, то hello подробного журнала создается в текущем рабочем каталоге hello в вложенную папку с именем `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Укажите число hello toostart параллельных операций
Параметр `/NC` указывает hello количество параллельных копирования операций. По умолчанию AzCopy запускается определенное число передачи пропускная способность hello tooincrease параллельных операций. Для операций с таблицами hello числом одновременных операций — равно toohello количество процессоров, к которым у вас есть. Для больших двоичных объектов и файла операций hello числом одновременных операций — равно 8 раз hello число процессоров, к которым у вас есть. При выполнении AzCopy в сети с низкой пропускной способностью, можно указать меньшее число /NC tooavoid сбоя, причиной конкуренции ресурсов.

### <a name="run-azcopy-against-azure-storage-emulator"></a>Запуск AzCopy с использованием эмулятора службы хранилища Azure
Вы можете выполнить AzCopy для hello [эмулятор хранилища Azure](storage-use-emulator.md) для больших двоичных объектов:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

и таблиц:

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>Параметры AzCopy
Параметры для AzCopy описаны ниже. Можно также ввести один из следующих команд из командной строки hello для получения справки по использованию AzCopy hello:

* Подробная справка по командной строке AzCopy: `AzCopy /?`
* Подробная справка по параметрам AzCopy: `AzCopy /?:SourceKey`
* Примеры командной строки: `AzCopy /?:Samples`

### <a name="sourcesource"></a>/Source:"source"
Задает hello источник данных, из которого toocopy. Hello источник может быть каталог файловой системы, контейнер больших двоичных объектов, виртуальный каталог больших двоичных объектов, общей папки хранилища, каталог файлов хранения или таблицы Azure.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="destdestination"></a>/Dest:"destination"
Указывает toocopy hello назначения для. Hello назначения может быть каталог файловой системы, контейнер больших двоичных объектов, виртуальный каталог больших двоичных объектов, общей папки хранилища, каталог файлов хранения или таблицы Azure.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="patternfile-pattern"></a>/Pattern:"file-pattern"
Указывает шаблон файла, указывающее, какие файлы toocopy. поведение Hello hello /Pattern параметра определяется расположение hello hello исходных данных, а также наличие hello hello рекурсивный режим. Рекурсивный режим задается с помощью параметра "/S.".

Если hello указанный исходный каталог в файловой системе hello, то действуют стандартные подстановочные знаки, и предоставлен шаблон файла hello противопоставляется файлов в каталоге hello. Если параметр задан, затем AzCopy также соответствует указанному шаблону hello все файлы в подкаталогах, каталоге hello.

Если указанный источник hello контейнер больших двоичных объектов или виртуального каталога, подстановочные знаки не применяются. Если параметр задан, затем AzCopy интерпретирует шаблон hello указанный файл как префикс большого двоичного объекта. Если параметр /S не указан, затем AzCopy соответствует шаблону файла hello с именами требуемый BLOB-объект.

Если источником является Azure файловый ресурс, то необходимо указать hello точное имя файла, (например abc.txt) hello toocopy один файл, или укажите параметр /S toocopy все файлы в общей папки рекурсивно hello. Предпринята попытка toospecify оба файла шаблону и параметру /S вместе приведет к ошибке.

AzCopy использует сопоставление с учетом регистра, когда hello/source — это контейнер больших двоичных объектов или виртуальный каталог больших двоичных объектов и Здравствуйте, используются без учета регистра, сопоставления во всех других случаях.

Hello файл шаблон по умолчанию, используемый, когда указан шаблон нет файла является *.* для расположения файловой системы или пустой префикс для расположения службы хранилища Azure. Задание нескольких шаблонов не поддерживается.

**Применимо к** большим двоичным объектам и файлам.

### <a name="destkeystorage-key"></a>/DestKey:"storage-key"
Указывает ключ учетной записи хранения hello для hello конечного ресурса.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="destsassas-token"></a>/DestSAS:"sas-token"
Задает подпись общего доступа (SAS) с разрешениями на чтение и запись для назначения hello (если применимо). Заключение hello SAS в двойные кавычки, он может содержит специальные знаки командной строки.

Если ресурсы назначения hello контейнер больших двоичных объектов, общей папки или таблицу, можно либо указать этот параметр, следуют маркер SAS hello или hello SAS можно указать как часть hello конечный контейнер больших двоичных объектов, общая папка или URI таблицы без этого параметра.

Если hello источником и назначением является обоих больших двоичных объектов, то hello целевой большой двоичный объект должен находиться на hello же учетной записи хранилища BLOB-объект источника hello.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="sourcekeystorage-key"></a>/SourceKey:"storage-key"
Указывает ключ учетной записи хранения hello для hello исходного ресурса.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="sourcesassas-token"></a>/SourceSAS:"sas-token"
Задает подпись общего доступа с разрешениями чтения и список для источника hello (если применимо). Заключение hello SAS в двойные кавычки, он может содержит специальные знаки командной строки.

Если hello источника ресурсов — это контейнер больших двоичных объектов и подписанный URL-адрес, ни ключ предоставляется, контейнер больших двоичных объектов hello считывается через анонимный доступ.

Если источник hello в общей папке или таблицу, необходимо указать ключ или SAS.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="s"></a>/S
Задает рекурсивный режим для операций копирования. В режиме рекурсивные AzCopy копирует все BLOB-объектов или файлов, соответствующих шаблону hello указанного файла, включая файлы во вложенных папках.

**Применимо к** большим двоичным объектам и файлам.

### <a name="blobtypeblock--page--append"></a>/BlobType:"block" | "page" | "append"
Указывает, является ли BLOB-объект назначения hello блочный BLOB-объект, большой двоичный объект страницы или добавочный большой двоичный объект. Этот параметр применяется только при передаче большого двоичного объекта. В противном случае возникает ошибка. Если целевой hello является большой двоичный объект, и этот параметр не указан, по умолчанию AzCopy создает большой двоичный объект блока.

**Применимо к** большим двоичным объектам.

### <a name="checkmd5"></a>/CheckMD5
Вычисляет хэш MD5 для загруженных данных и проверяет, что хэш MD5 hello хранимых в большом двоичном объекте hello или свойства Content-MD5 файла соответствует hello вычислить хэш. Проверка Hello MD5 отключена по умолчанию, поэтому эта проверка MD5 hello tooperform параметра необходимо указать при загрузке данных.

Обратите внимание, что хранилище Azure не гарантирует, что hello хэш MD5, сохраненное для большого двоичного объекта hello, или файл актуален. Это клиента ответственности tooupdate hello MD5 при каждом изменении hello большого двоичного объекта или файла.

AzCopy всегда задает hello свойства Content-MD5 для BLOB-объектов Azure или файл после его отправки toohello службы.  

**Применимо к** большим двоичным объектам и файлам.

### <a name="snapshot"></a>/Snapshot
Указывает, является ли tootransfer моментальные снимки. Этот параметр допустим, только когда источник hello большого двоичного объекта.

Hello моментальные снимки переносятся большого двоичного объекта переименовываются в следующем формате: .extension blob-name (время создания моментального снимка)

По умолчанию моментальные снимки не копируются.

**Применимо к** большим двоичным объектам.

### <a name="vverbose-log-file"></a>/V:[verbose-log-file]
Выводит сообщения с подробным состоянием в файл журнала.

По умолчанию hello подробный файл журнала называется AzCopyVerbose.log в `%LocalAppData%\Microsoft\Azure\AzCopy`. Если указать расположение существующих файлов, для этого параметра hello подробный журнал — toothat добавленный файл.  

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="zjournal-file-folder"></a>/Z:[journal-file-folder]
Задает папку файла журнала для возобновления операции.

AzCopy всегда поддерживает возобновление, если операция была прервана.

Если этот параметр не указан или указан без путь к папке, AzCopy создает файл журнала hello в расположении по умолчанию hello, а именно % LocalAppData%\Microsoft\Azure\AzCopy.

Каждый раз, когда выдачи команды tooAzCopy, он проверяет, существует ли файл журнала в папке по умолчанию hello, или существует ли в папке, указанного с помощью этого параметра. Если файл журнала hello не существует в любом месте, AzCopy считает новые операции hello и создает новый файл журнала.

Если существует файл журнала hello, AzCopy проверяет, соответствует ли hello командной строки, что вы ввод hello командной строки в файле журнала hello. Если две командные строки hello совпадают, AzCopy возобновляет hello незавершенные операции. Если они не совпадают, не запрошенные tooeither перезаписать hello журнала файла toostart новую операцию или toocancel hello текущей операции.

файл журнала Hello удаляется после успешного завершения операции hello.

Обратите внимание, что возобновление операции из файла журнала, созданного предыдущей версией AzCopy, не поддерживается.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="parameter-file"></a>/@:"parameter-file"
Задает файл, который содержит параметры. AzCopy процессы hello параметры в файле hello, как если бы они были указаны в командной строке hello.

В файле ответа можно либо задать несколько параметров в одной строке, либо задать каждый параметр в отдельной строке. Обратите внимание, что отдельный параметр не может занимать несколько строк.

Файлы ответа могут содержать комментарии строки, начинающиеся с символа # hello.

Можно задать несколько файлов ответов. Однако, следует иметь в виду, что AzCopy не поддерживает вложенных фалов ответов.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="y"></a>/Y
Скрывает все запросы на подтверждение AzCopy.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="l"></a>/L
Задает только операцию перечисления, данные не копируются.

AzCopy интерпретирует hello, используя для этого параметра моделирования для выполнения командной строки hello без этого параметра/l, а также счетчики, сколько объектов будут скопированы, можно указать параметр /V во же время toocheck объектов, которые копируются в подробный журнал hello hello.

Hello поведение этого параметра также определяется наличие hello hello рекурсивные параметр /S и файл шаблона режим /Pattern и расположение hello hello исходных данных.

При использовании этого параметра AzCopy необходимы права на ЧТЕНИЕ и СОЗДАНИЕ СПИСКА для местоположения исходных данных.

**Применимо к** большим двоичным объектам и файлам.

### <a name="mt"></a>/MT
Задает время последнего изменения hello загруженный файл toobe Здравствуйте таким же, как hello исходного большого двоичного объекта или файла.

**Применимо к** большим двоичным объектам и файлам.

### <a name="xn"></a>/XN
Исключает более новый исходный ресурс. Hello ресурсов не копируются в случае hello время последнего изменения источника hello hello же или более новая, чем назначения.

**Применимо к** большим двоичным объектам и файлам.

### <a name="xo"></a>/XO
Исключает более старый исходный ресурс. Hello ресурсов не копируется в случае hello время последнего изменения источника hello hello же или более ранней, чем назначения.

**Применимо к** большим двоичным объектам и файлам.

### <a name="a"></a>/A
Отправляет только файлы, имеющие атрибут "архивный" hello набор.

**Применимо к** большим двоичным объектам и файлам.

### <a name="iarashcnetoi"></a>/IA:[RASHCNETOI]
Передачи только файлы, содержащие любое hello указанный набор атрибутов.

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
Исключает файлы, содержащие любое hello указанный набор атрибутов.

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
Указывает, что символ-разделитель hello использовать toodelimit виртуальные каталоги в имени большого двоичного объекта.

По умолчанию использует AzCopy / как символ-разделитель hello. Однако, AzCopy поддерживает любой общий символ (например, @, # или %) в качестве разделителя. Если вам требуется один из этих специальных символов в командной строке hello tooinclude, заключите имя файла hello в двойные кавычки.

Этот параметр применяется только для загрузки BLOB-объектов.

**Применимо к** большим двоичным объектам.

### <a name="ncnumber-of-concurrent-operations"></a>/NC:"number-of-concurrent-operations"
Указывает номер hello одновременных операций.

AzCopy по умолчанию запускается определенное число передачи пропускная способность hello tooincrease параллельных операций. Обратите внимание, что большое количество параллельных операций в среде с низкой пропускной способностью может произойти переполнение hello сетевое подключение предотвращают hello операции полностью завершить. Регулируйте количество одновременных операций в зависимости от фактической доступной пропускной способности сети.

Hello верхний предел для одновременных операций — 512.

**Применимо к** большим двоичным объектам, файлам, таблицам.

### <a name="sourcetypeblob--table"></a>/SourceType:"Blob" | "Table"
Указывает, что hello `source` ресурсом является большой двоичный объект в hello локальной среде разработки, работающее в эмуляторе хранилища hello.

**Применимо к** большим двоичным объектам и таблицам.

### <a name="desttypeblob--table"></a>/DestType:"Blob" | "Table"
Указывает, что hello `destination` ресурсом является большой двоичный объект в hello локальной среде разработки, работающее в эмуляторе хранилища hello.

**Применимо к** большим двоичным объектам и таблицам.

### <a name="pkrskey1key2key3"></a>/PKRS:"key1#key2#key3#..."
Разбиений hello секции диапазона ключей tooenable Экспорт таблицы данных в параллельном режиме, что повышает скорость hello hello операции экспорта.

Если этот параметр не указан, AzCopy использует один поток tooexport таблицы сущности. Например, если hello пользователь указывает /PKRS: «aa #bb», а затем AzCopy запускает три параллельных операций.

Каждая операция экспортирует один из диапазонов ключей секций, как это показано на примере ниже:

  [first-partition-key, aa)

  [aa, bb)

  [bb, last-partition-key]

**Применимо к** таблицам.

### <a name="splitsizefile-size"></a>/SplitSize:"file-size"
Указывает Здравствуйте экспортированный файл разделить размер в МБ, hello допустимое минимальное значение — 32.

Если этот параметр не указан, AzCopy экспортирует tooa таблицы данных одного файла.

Если hello таблица содержит данные BLOB-объект экспортированного tooa hello экспортированный файл достигает размера 200 hello ГБ для размера большого двоичного объекта, AzCopy разделяет hello экспортированного файла, даже если этот параметр не указан.

**Применимо к** таблицам.

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
Задает поведение при импорте данных таблицы hello.

* InsertOrSkip - пропускает существующую сущность или вставляет новую сущность, если она не существует в таблице hello.
* InsertOrMerge - объединяет существующую сущность или вставляет новую сущность, если она не существует в таблице hello.
* InsertOrReplace - заменяет существующую сущность или вставляет новую сущность, если она не существует в таблице hello.

**Применимо к** таблицам.

### <a name="manifestmanifest-file"></a>/Manifest:"manifest-file"
Указывает файл манифеста hello hello таблицы экспорта и импорта операции.

Этот параметр является необязательным, во время операции экспорта hello, AzCopy создает файл манифеста с предопределенным именем, если этот параметр не указан.

Этот параметр является обязательным, во время операции импорта hello поиска файлов данных hello.

**Применимо к** таблицам.

### <a name="synccopy"></a>/SyncCopy
Указывает ли toosynchronously копирование больших двоичных объектов или файлов между двумя конечными точками службы хранилища Azure.

По умолчанию AzCopy использует серверное асинхронное копирование. Укажите этот параметр tooperform синхронного копирования, который загружает большие двоичные объекты или файлы памяти toolocal и отправляет их tooAzure хранилища.

Этот параметр можно использовать при копировании файлов в хранилище больших двоичных объектов в хранилище файлов или из большого двоичного объекта хранилища tooFile хранилища, и наоборот.

**Применимо к** большим двоичным объектам и файлам.

### <a name="setcontenttypecontent-type"></a>/SetContentType:"content-type"
Задает тип содержимого MIME hello для целевых больших двоичных объектов или файлов.

Наборы AzCopy hello тип содержимого большого двоичного объекта или файла tooapplication/octet-stream по умолчанию. Можно задать тип содержимого hello для всех больших двоичных объектов или файлы, явно указав значение для этого параметра.

При указании этого параметра без указания значения AzCopy задает каждый BLOB-объект или тип содержимого файла, в соответствии с tooits расширение файла.

**Применимо к** большим двоичным объектам и файлам.

### <a name="payloadformatjson--csv"></a>/PayloadFormat:"JSON" | "CSV"
Задает формат hello hello таблицы экспортированного файла данных.

Если этот параметр не указан, по умолчанию AzCopy экспортирует файл данных таблицы в формате JSON.

**Применимо к** таблицам.

## <a name="known-issues-and-best-practices"></a>Известные проблемы и рекомендации
### <a name="limit-concurrent-writes-while-copying-data"></a>Ограничение одновременных операций записи при копировании данных
При копировании больших двоичных объектов или файлов с помощью AzCopy, имейте в виду, возможно, изменение другое приложение hello данных при копировании его. Если это возможно убедитесь, hello данных при копировании не изменяется во время операции копирования hello. Например при копировании виртуальный жесткий ДИСК, связанный с виртуальной машины Azure, убедитесь, что нет других приложений в настоящее время пишете toohello виртуального жесткого диска. Toodo хорошим способом это по аренде toobe ресурсов hello копируются. Кроме того можно сначала создать моментальный снимок виртуального жесткого диска hello и скопируйте hello моментального снимка.

Если не может помешать записи tooblobs или файлы, пока они копируются, то следует помнить, заданием hello hello время завершения работы других приложений, hello скопированных ресурсов может больше нет полной четности с ресурсами источника hello.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Запускайте один экземпляр AzCopy на одном компьютере.
AzCopy является использование hello спроектированный toomaximize скорость передачи данных ресурсов tooaccelerate машины hello, мы рекомендуем запустить только один экземпляр AzCopy на одном компьютере и укажите параметр hello `/NC` при необходимости несколько параллельных операций. Для получения дополнительных сведений введите `AzCopy /?:NC` hello командной строки.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>Включайте FIPS-совместимые алгоритмы MD5 для AzCopy при использовании FIPS-совместимых алгоритмов для шифрования, хэширования и подписывания.
AzCopy по умолчанию использует .NET MD5 реализацию toocalculate hello MD5 при копировании объектов, но существуют некоторые требования безопасности, которым требуется параметром совместимости MD5 AzCopy tooenable FIPS.

Для этого можно создать файл app.config `AzCopy.exe.config` со свойством `AzureStorageUseV1MD5` и поместить его в папку с файлом AzCopy.exe.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Для свойства «AzureStorageUseV1MD5» • True: значение по умолчанию hello, AzCopy использует реализацию .NET MD5.
• False — AzCopy использует FIPS-совместимый алгоритм MD5.

Обратите внимание, что по умолчанию на компьютере Windows FIPS-совместимые алгоритмы отключены. Эту настройку можно изменить, набрав в окне запуска команд "secpol.msc" и выбрав "Настройки безопасности -> Локальные политики -> Параметры безопасности -> Системная криптография: Использовать FIPS-совместимые алгоритмы для шифрования, хеширования и подписывания".

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о хранилище Azure и AzCopy см. в разделе hello следующие ресурсы:

### <a name="azure-storage-documentation"></a>Документация по хранилищу Azure:
* [Введение tooAzure хранилища](../storage-introduction.md)
* [Как toouse хранилища BLOB-объектов из .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Как toouse хранения файлов из .NET](../storage-dotnet-how-to-use-files.md)
* [Как toouse хранилище таблиц из .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Как управлять toocreate, или удалить учетную запись хранения](../storage-create-storage-account.md)
* [Перенос данных с помощью AzCopy для Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Записи блога по хранилищу Azure:
* [Введение в предварительную версию библиотеки движения данных в хранилище Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: введение в синхронное копирование и настраиваемый тип содержимого](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: выпуск общедоступной версии AzCopy 3.0 и предварительной версии AzCopy 4.0 с поддержкой таблиц и файлов](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: оптимизированные сценарии для крупномасштабного копирования](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy: поддержка геоизбыточного хранилища для доступа с правом чтения](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy: передача данных с использованием перезапускаемого режима и маркера SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: использование копирования больших двоичных объектов между разными учетными записями](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: отправка и скачивание файлов для больших двоичных объектов Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

