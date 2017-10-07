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
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="b5544-105">Перенесите данные с помощью hello AzCopy в Windows</span><span class="sxs-lookup"><span data-stu-id="b5544-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="b5544-106">AzCopy является командной строки служебная программа, разработанная для копирования данных tooand из хранилища больших двоичных объектов Microsoft Azure, таблицы и файла с помощью простой команды с оптимальной производительностью.</span><span class="sxs-lookup"><span data-stu-id="b5544-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="b5544-107">Можно скопировать данные из одного объекта tooanother в вашей учетной записи хранения или между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="b5544-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="b5544-108">Существуют две версии AzCopy, которые можно скачать.</span><span class="sxs-lookup"><span data-stu-id="b5544-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="b5544-109">Служебная программа AzCopy для Windows основана на платформе .NET Framework и использует параметры командной строки в формате Windows.</span><span class="sxs-lookup"><span data-stu-id="b5544-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="b5544-110">Служебная программа [AzCopy для Linux](storage-use-azcopy-linux.md) основана на платформе .NET Core, которая нацелена на платформы Linux, использующие параметры командной строки в формате POSIX.</span><span class="sxs-lookup"><span data-stu-id="b5544-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="b5544-111">В этой статье рассматривается AzCopy для Windows.</span><span class="sxs-lookup"><span data-stu-id="b5544-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="b5544-112">Скачивание и установка AzCopy</span><span class="sxs-lookup"><span data-stu-id="b5544-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="b5544-113">AzCopy для Windows</span><span class="sxs-lookup"><span data-stu-id="b5544-113">AzCopy on Windows</span></span>
<span data-ttu-id="b5544-114">Загрузите hello [последнюю версию AzCopy в Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="b5544-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="b5544-115">Установка в Windows</span><span class="sxs-lookup"><span data-stu-id="b5544-115">Installation on Windows</span></span>
<span data-ttu-id="b5544-116">После установки AzCopy в Windows, с помощью установщика hello, откройте окно командной строки и перейдите toohello AzCopy установочный каталог на компьютере -, где hello `AzCopy.exe` исполняемый файл находится.</span><span class="sxs-lookup"><span data-stu-id="b5544-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="b5544-117">При желании можно добавить hello AzCopy tooyour системы путь установки.</span><span class="sxs-lookup"><span data-stu-id="b5544-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="b5544-118">По умолчанию AzCopy установлен слишком`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` или `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="b5544-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="b5544-119">Написание первой команды AzCopy</span><span class="sxs-lookup"><span data-stu-id="b5544-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="b5544-120">Базовый синтаксис команды AzCopy Hello таков:</span><span class="sxs-lookup"><span data-stu-id="b5544-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="b5544-121">Hello следующие примеры демонстрируют различные сценарии для копирования данных tooand из BLOB-объектов Microsoft Azure, файлы и таблицы.</span><span class="sxs-lookup"><span data-stu-id="b5544-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="b5544-122">См. toohello [AzCopy параметры](#azcopy-parameters) раздел подробное описание параметров hello, используемых в каждой выборке.</span><span class="sxs-lookup"><span data-stu-id="b5544-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="b5544-123">Большой двоичный объект: скачивание</span><span class="sxs-lookup"><span data-stu-id="b5544-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="b5544-124">Скачивание одного большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="b5544-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="b5544-125">Обратите внимание, что если папка hello `C:\myfolder` не существует, AzCopy создаст его и загрузить `abc.txt ` в новую папку hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="b5544-126">Скачивание большого двоичного объекта из дополнительного региона</span><span class="sxs-lookup"><span data-stu-id="b5544-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="b5544-127">Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.</span><span class="sxs-lookup"><span data-stu-id="b5544-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="b5544-128">Скачивание всех больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="b5544-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="b5544-129">Предположим следующее hello большие двоичные объекты находятся в указанном контейнере hello:</span><span class="sxs-lookup"><span data-stu-id="b5544-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="b5544-130">После завершения операции загрузки hello hello каталог `C:\myfolder` будет включать hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="b5544-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="b5544-131">Если не задать параметр `/S`, большие двоичные объекты не будут скачаны.</span><span class="sxs-lookup"><span data-stu-id="b5544-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="b5544-132">Скачивание больших двоичных объектов с указанным префиксом</span><span class="sxs-lookup"><span data-stu-id="b5544-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="b5544-133">Предположим следующее hello большие двоичные объекты находятся в указанном контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="b5544-134">Все большие двоичные объекты, начинающиеся с префикса hello `a` будут загружены:</span><span class="sxs-lookup"><span data-stu-id="b5544-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="b5544-135">После завершения операции загрузки hello hello папку `C:\myfolder` будет включать hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="b5544-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="b5544-136">префикс Hello применяется toohello виртуальному каталогу, который формирует первую часть имени большого двоичного объекта hello hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="b5544-137">В приведенном выше примере hello hello виртуального каталога не соответствует hello указанного префикса, поэтому оно не загружается.</span><span class="sxs-lookup"><span data-stu-id="b5544-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="b5544-138">Кроме того, если hello параметр `\S` не указан, AzCopy не будет загружать все большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="b5544-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="b5544-139">Задать время последнего изменения hello toobe экспортированные файлы так же, как hello исходный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="b5544-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="b5544-140">Большие двоичные объекты можно также исключить из операции загрузки hello, на основе их времени последнего изменения.</span><span class="sxs-lookup"><span data-stu-id="b5544-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="b5544-141">Например, большие двоичные объекты tooexclude, время последнего изменения — hello же или более новая, чем конечный файл hello, добавить hello `/XN` параметр:</span><span class="sxs-lookup"><span data-stu-id="b5544-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="b5544-142">Или если вы хотите tooexclude BLOB-объектов, время последнего изменения — hello же или более ранней, чем конечный файл hello, добавьте hello `/XO` параметр:</span><span class="sxs-lookup"><span data-stu-id="b5544-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="b5544-143">Большой двоичный объект: отправка</span><span class="sxs-lookup"><span data-stu-id="b5544-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="b5544-144">Отправка одного файла</span><span class="sxs-lookup"><span data-stu-id="b5544-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="b5544-145">Если hello указанный контейнер не существует, AzCopy создайте его и отправить файл hello в него.</span><span class="sxs-lookup"><span data-stu-id="b5544-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="b5544-146">Отправка одного файла каталога toovirtual</span><span class="sxs-lookup"><span data-stu-id="b5544-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="b5544-147">Если hello указан виртуальный каталог не существует, AzCopy, передают hello файл tooinclude hello виртуального каталога в имени (*например*, `vd/abc.txt` в приведенном выше примере hello).</span><span class="sxs-lookup"><span data-stu-id="b5544-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="b5544-148">Отправка всех файлов</span><span class="sxs-lookup"><span data-stu-id="b5544-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="b5544-149">Задание параметра `/S` содержимое передачи hello hello указано tooBlob хранилище каталога рекурсивно, это означает, что все вложенные папки и файлы будут отправлены также.</span><span class="sxs-lookup"><span data-stu-id="b5544-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="b5544-150">Например, предположим, hello следующие файлы размещаются в папке `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="b5544-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="b5544-151">После завершения операции отправки hello hello контейнер будет содержать hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="b5544-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="b5544-152">Если параметр `/S` не указан, программа AzCopy не будет выполнять отправку рекурсивно.</span><span class="sxs-lookup"><span data-stu-id="b5544-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="b5544-153">После завершения операции отправки hello hello контейнер будет содержать hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="b5544-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="b5544-154">Отправка файлов, соответствующих указанному шаблону</span><span class="sxs-lookup"><span data-stu-id="b5544-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="b5544-155">Предполагается hello следующие файлы размещаются в папке `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="b5544-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="b5544-156">После завершения операции отправки hello hello контейнер будет содержать hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="b5544-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="b5544-157">Если вы не укажете параметр `/S`, программа AzCopy будет отправлять только большие двоичные объекты, которых нет в виртуальном каталоге:</span><span class="sxs-lookup"><span data-stu-id="b5544-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="b5544-158">Укажите hello MIME-тип содержимого большого двоичного объекта назначения</span><span class="sxs-lookup"><span data-stu-id="b5544-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="b5544-159">По умолчанию AzCopy задает тип содержимого hello BLOB-объект назначения, слишком`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="b5544-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="b5544-160">Начиная с версии 3.1.0, можно явно указать тип содержимого hello через параметр hello `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="b5544-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="b5544-161">Этот синтаксис задает hello-тип содержимого для всех больших двоичных объектов в операции передачи.</span><span class="sxs-lookup"><span data-stu-id="b5544-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="b5544-162">При указании `/SetContentType` без значения, затем AzCopy установит каждый BLOB-объект или тип содержимого файла, в соответствии с tooits расширение файла.</span><span class="sxs-lookup"><span data-stu-id="b5544-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="b5544-163">Большой двоичный объект: копирование</span><span class="sxs-lookup"><span data-stu-id="b5544-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="b5544-164">Копирование большого двоичного объекта в пределах учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="b5544-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="b5544-165">При копировании большого двоичного объекта в пределах учетной записи хранения выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b5544-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="b5544-166">Копирование большого двоичного объекта между различными учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="b5544-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="b5544-167">При копировании большого двоичного объекта между различными учетными записями хранения выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b5544-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="b5544-168">Копирование одного большого двоичного объекта из области tooprimary дополнительный регион</span><span class="sxs-lookup"><span data-stu-id="b5544-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="b5544-169">Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.</span><span class="sxs-lookup"><span data-stu-id="b5544-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="b5544-170">Копирование большого двоичного объекта и его моментальных снимков между различными учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="b5544-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="b5544-171">После завершения операции копирования hello hello целевой контейнер будет содержать hello больших двоичных объектов и ее моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="b5544-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="b5544-172">При условии, что большой двоичный объект hello в приведенном выше примере hello имеются два моментальные снимки, hello контейнер будет содержать следующие hello больших двоичных объектов и моментальных снимков:</span><span class="sxs-lookup"><span data-stu-id="b5544-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="b5544-173">Синхронное копирование больших двоичных объектов между учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="b5544-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="b5544-174">По умолчанию AzCopy выполняет асинхронное копирование данных между двумя конечными точками хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5544-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="b5544-175">Таким образом, операция копирования hello будет выполняться в фоновом режиме hello, используя запасную пропускную способность емкости, которая имеет нет соглашения об уровне ОБСЛУЖИВАНИЯ с точки зрения быстродействия большой двоичный объект будет скопирован и AzCopy периодически проверять состояние копирования hello до завершения или не удалось выполнить копирование hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="b5544-176">Hello `/SyncCopy` параметр обеспечивает то, что операция копирования hello получит согласованное скорость.</span><span class="sxs-lookup"><span data-stu-id="b5544-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="b5544-177">AzCopy выполняет копирование синхронной hello по загрузке больших двоичных объектов hello toocopy из hello указан источник toolocal памяти и передача их toohello местом назначения хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b5544-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="b5544-178">`/SyncCopy`может создавать дополнительные исходящих стоимости копирования сравниваемых tooasynchronous hello рекомендованный подход является toouse этот параметр на виртуальной Машине Azure, hello же регионе, что ваш источник учетной записи tooavoid исходящих затраты на хранение.</span><span class="sxs-lookup"><span data-stu-id="b5544-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="b5544-179">Файл: скачивание</span><span class="sxs-lookup"><span data-stu-id="b5544-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="b5544-180">Скачивание одного файла</span><span class="sxs-lookup"><span data-stu-id="b5544-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="b5544-181">Если источником является Azure файловый ресурс, то необходимо указать hello точное имя файла, hello (*например* `abc.txt`) toodownload один файл, или задайте параметр `/S` toodownload все файлы в папке hello рекурсивно.</span><span class="sxs-lookup"><span data-stu-id="b5544-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="b5544-182">Попытка toospecify и шаблону файла и параметр `/S` вместе приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="b5544-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="b5544-183">Скачивание всех файлов</span><span class="sxs-lookup"><span data-stu-id="b5544-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="b5544-184">Обратите внимание, что пустые папки не скачиваются.</span><span class="sxs-lookup"><span data-stu-id="b5544-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="b5544-185">Файл: отправка</span><span class="sxs-lookup"><span data-stu-id="b5544-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="b5544-186">Отправка одного файла</span><span class="sxs-lookup"><span data-stu-id="b5544-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="b5544-187">Отправка всех файлов</span><span class="sxs-lookup"><span data-stu-id="b5544-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="b5544-188">Обратите внимание, что пустые папки не передаются.</span><span class="sxs-lookup"><span data-stu-id="b5544-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="b5544-189">Отправка файлов, соответствующих указанному шаблону</span><span class="sxs-lookup"><span data-stu-id="b5544-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="b5544-190">Файл: копирование</span><span class="sxs-lookup"><span data-stu-id="b5544-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="b5544-191">Копирование общих файловых ресурсов</span><span class="sxs-lookup"><span data-stu-id="b5544-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="b5544-192">При копировании файла между файловыми ресурсами выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5544-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="b5544-193">Копирование из файла tooblob общей папки</span><span class="sxs-lookup"><span data-stu-id="b5544-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="b5544-194">При копировании файла из файла tooblob общего ресурса, [копирование на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) выполняется операция.</span><span class="sxs-lookup"><span data-stu-id="b5544-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="b5544-195">Скопируйте из папки toofile больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="b5544-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="b5544-196">При копировании файлов из папки toofile больших двоичных объектов, [копирование на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) выполняется операция.</span><span class="sxs-lookup"><span data-stu-id="b5544-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="b5544-197">Синхронное копирование файлов</span><span class="sxs-lookup"><span data-stu-id="b5544-197">Synchronously copy files</span></span>
<span data-ttu-id="b5544-198">Можно указать hello `/SyncCopy` toocopy данные из хранилища файлов tooFile хранилище, из хранилища файлов tooBlob хранилища, а из хранилища больших двоичных объектов tooFile хранилища синхронно, AzCopy происходит загрузка hello источника данных toolocal памяти и отправьте его снова toodestination.</span><span class="sxs-lookup"><span data-stu-id="b5544-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="b5544-199">При этом применяется стандартный тариф для исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="b5544-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="b5544-200">При копировании из хранилища файлов tooBlob хранения типа больших двоичных объектов по умолчанию hello блочного BLOB-объекта, пользователь может указать параметр `/BlobType:page` toochange hello конечного большого двоичного объекта типа.</span><span class="sxs-lookup"><span data-stu-id="b5544-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="b5544-201">Обратите внимание, что `/SyncCopy` может создавать дополнительных исходящих стоимости сравнение копирования tooasynchronous, hello рекомендуется toouse виртуальную Машину Azure, которая находится в hello hello этот параметр в одном регионе вашей исходной учетной записи tooavoid исходящих затраты на хранение.</span><span class="sxs-lookup"><span data-stu-id="b5544-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="b5544-202">Таблица: экспорт</span><span class="sxs-lookup"><span data-stu-id="b5544-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="b5544-203">Экспорт таблицы</span><span class="sxs-lookup"><span data-stu-id="b5544-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="b5544-204">AzCopy записывает файл манифеста toohello указанную папку.</span><span class="sxs-lookup"><span data-stu-id="b5544-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="b5544-205">файл манифеста Hello используется в файлах hello импорта процесса toolocate hello необходимые данные и выполнить проверку данных.</span><span class="sxs-lookup"><span data-stu-id="b5544-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="b5544-206">файл манифеста Hello используется следующее соглашение об именовании по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="b5544-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="b5544-207">Пользователь также может указать параметр hello `/Manifest:<manifest file name>` имя файла манифеста tooset hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="b5544-208">Разбивка экспорта на несколько файлов</span><span class="sxs-lookup"><span data-stu-id="b5544-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="b5544-209">Использует AzCopy *индекса объема* в hello разбиение данных имена файлов toodistinguish несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="b5544-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="b5544-210">индекс объема Hello состоит из двух частей, *индекс диапазона ключа секции* и *индекс разбиение файлов*.</span><span class="sxs-lookup"><span data-stu-id="b5544-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="b5544-211">Оба индекса отсчитываются, начиная с нуля.</span><span class="sxs-lookup"><span data-stu-id="b5544-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="b5544-212">индекс диапазона ключа секции Hello будет равно 0, если пользователь не указал параметр `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="b5544-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="b5544-213">Например, предположим, что после hello пользователь указывает параметр AzCopy создает два файла данных `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="b5544-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="b5544-214">Привет, возникающие в имена файлов данных, может быть:</span><span class="sxs-lookup"><span data-stu-id="b5544-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="b5544-215">Обратите внимание, что hello минимально возможное значение для параметра `/SplitSize` — 32 МБ.</span><span class="sxs-lookup"><span data-stu-id="b5544-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="b5544-216">Если hello указан назначения хранилища больших двоичных объектов, AzCopy будет разделить файл данных hello после его ограничение размера большого двоичного объекта hello достигает размера (200 ГБ), независимо от того, параметр `/SplitSize` был указан пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="b5544-217">Экспорт таблицы tooJSON или CSV-файл данных</span><span class="sxs-lookup"><span data-stu-id="b5544-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="b5544-218">AzCopy по умолчанию экспортирует файлы данных tooJSON таблиц.</span><span class="sxs-lookup"><span data-stu-id="b5544-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="b5544-219">Можно указать параметр hello `/PayloadFormat:JSON|CSV` tooexport hello таблиц в формате JSON или CSV.</span><span class="sxs-lookup"><span data-stu-id="b5544-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="b5544-220">При указании формат полезных данных CSV hello, AzCopy также будет создан файл схемы с расширением файла `.schema.csv` для каждого файла данных.</span><span class="sxs-lookup"><span data-stu-id="b5544-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="b5544-221">Экспорт объектов таблицы в несколько потоков</span><span class="sxs-lookup"><span data-stu-id="b5544-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="b5544-222">AzCopy запускает сущностей tooexport параллельных операций, когда пользователь hello указывает параметр `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="b5544-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="b5544-223">Каждая операция экспортирует объем данных равный значению объема, указанного в индексе диапазонов ключей секций.</span><span class="sxs-lookup"><span data-stu-id="b5544-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="b5544-224">Обратите внимание, hello числом одновременных операций также определяется параметром `/NC`.</span><span class="sxs-lookup"><span data-stu-id="b5544-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="b5544-225">AzCopy использует hello число процессоров core как значение по умолчанию hello `/NC` при копировании сущностей таблицы, даже если `/NC` не указан.</span><span class="sxs-lookup"><span data-stu-id="b5544-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="b5544-226">Когда пользователь hello указывает параметр `/PKRS`, AzCopy использует hello меньшего количества hello двух значений — раздел диапазонов ключей и явно или неявно заданного параллельных операций - toodetermine hello toostart параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="b5544-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="b5544-227">Для получения дополнительных сведений введите `AzCopy /?:NC` hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="b5544-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="b5544-228">Экспорт таблицы tooblob</span><span class="sxs-lookup"><span data-stu-id="b5544-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="b5544-229">AzCopy создаст файл данных JSON в контейнер больших двоичных объектов hello следующее соглашение об именовании:</span><span class="sxs-lookup"><span data-stu-id="b5544-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="b5544-230">файл данных создан Hello JSON hello формат полезных данных для минимальные метаданные:</span><span class="sxs-lookup"><span data-stu-id="b5544-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="b5544-231">За более подробной информацией о формате полезных данных обратитесь к разделу [Формат полезных данных для служб работы с таблицами](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5544-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="b5544-232">Обратите внимание, что при экспорте таблицы tooblobs, AzCopy будет загрузить hello таблицы сущности toolocal временных файлов данных затем передать blob toohello этих сущностей.</span><span class="sxs-lookup"><span data-stu-id="b5544-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="b5544-233">Эти временные файлы данных помещаются в папку файла журнала hello hello пути по умолчанию «<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>», можно указать параметр / [папка журнала файла] toochange Z: hello расположение папки для файла журнала и таким образом изменить расположение файлов hello временных данных.</span><span class="sxs-lookup"><span data-stu-id="b5544-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="b5544-234">Hello временных данных, размер файлов определяется по сущностей таблицы и размеров hello, указанным в /SplitSize параметр hello, несмотря на то, что файл временные данные hello в локальном диске будут удалены немедленно после ее отправлены toohello больших двоичных объектов, убедитесь, что вы иметь достаточно дискового пространства toostore эти временные файлы данных, прежде чем они будут удалены.</span><span class="sxs-lookup"><span data-stu-id="b5544-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="b5544-235">Таблица: импорт</span><span class="sxs-lookup"><span data-stu-id="b5544-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="b5544-236">Импорт таблиц</span><span class="sxs-lookup"><span data-stu-id="b5544-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="b5544-237">Здравствуйте, параметр `/EntityOperation` показывает, как tooinsert сущностей в hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="b5544-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="b5544-238">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="b5544-238">Possible values are:</span></span>

* <span data-ttu-id="b5544-239">`InsertOrSkip`: Пропускает существующую сущность или вставляет новую сущность, если она не существует в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="b5544-240">`InsertOrMerge`: Объединяет существующую сущность или вставляет новую сущность, если она не существует в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="b5544-241">`InsertOrReplace`: Заменяет существующую сущность или вставляет новую сущность, если она не существует в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="b5544-242">Обратите внимание, что нельзя задать параметр `/PKRS` в случае импорта hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="b5544-243">В отличие от сценария экспорта hello, в котором необходимо указать параметр `/PKRS` toostart параллельных операций, AzCopy по умолчанию запустится параллельных операций при импорте таблицы.</span><span class="sxs-lookup"><span data-stu-id="b5544-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="b5544-244">количество параллельных операций запуска по умолчанию Hello равно toohello равно числу процессоров core; Тем не менее, можно указать другое количество одновременных с параметром `/NC`.</span><span class="sxs-lookup"><span data-stu-id="b5544-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="b5544-245">Для получения дополнительных сведений введите `AzCopy /?:NC` hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="b5544-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="b5544-246">Обратите внимание, что программа AzCopy поддерживает импорт только для формата JSON, но не для формата CSV.</span><span class="sxs-lookup"><span data-stu-id="b5544-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="b5544-247">AzCopy не поддерживает импорт таблиц из созданных пользователями JSON-файла и файла манифеста.</span><span class="sxs-lookup"><span data-stu-id="b5544-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="b5544-248">Оба файла должны поступить в результате экспорта таблицы AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b5544-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="b5544-249">ошибки tooavoid, не изменяйте hello экспортируются JSON или файл манифеста.</span><span class="sxs-lookup"><span data-stu-id="b5544-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="b5544-250">Импорт сущностей tootable использование больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="b5544-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="b5544-251">Предположим, контейнер больших двоичных объектов содержит следующие hello: JSON-файл, представляющий таблиц Azure и сопутствующий файл манифеста.</span><span class="sxs-lookup"><span data-stu-id="b5544-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="b5544-252">Можно запустить hello, следующая команда tooimport сущностей в таблицу с использованием файла манифеста hello в этом контейнере BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="b5544-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="b5544-253">Другие функции AzCopy</span><span class="sxs-lookup"><span data-stu-id="b5544-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="b5544-254">Копирование данных, не существует в месте назначения hello</span><span class="sxs-lookup"><span data-stu-id="b5544-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="b5544-255">Hello `/XO` и `/XN` параметры позволяют ресурсы старого или более нового источника tooexclude копируются, соответственно.</span><span class="sxs-lookup"><span data-stu-id="b5544-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="b5544-256">Если требуется только ресурсы toocopy источника, которые не существуют в конечном hello, можно указать оба параметра в hello команды AzCopy:</span><span class="sxs-lookup"><span data-stu-id="b5544-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="b5544-257">Обратите внимание, что это не поддерживается при hello исходной или целевой таблицы.</span><span class="sxs-lookup"><span data-stu-id="b5544-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="b5544-258">Использование параметра командной строки toospecify файл ответа</span><span class="sxs-lookup"><span data-stu-id="b5544-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="b5544-259">В файл ответа можно включить параметры командной строки AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b5544-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="b5544-260">AzCopy процессы hello параметры в файле hello, как если бы они были указаны в командной строке hello, выполнение прямых подстановки с hello содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="b5544-261">Предположим, файл ответов с именем `copyoperation.txt`, содержащий следующие строки hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="b5544-262">Каждый параметр AzCopy можно указать как в одной строке,</span><span class="sxs-lookup"><span data-stu-id="b5544-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="b5544-263">так и в разных:</span><span class="sxs-lookup"><span data-stu-id="b5544-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="b5544-264">AzCopy завершится ошибкой, если параметр hello разбиты на две строки, как показано ниже для hello `/sourcekey` параметр:</span><span class="sxs-lookup"><span data-stu-id="b5544-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="b5544-265">Использовать несколько ответа файлы toospecify параметры командной строки</span><span class="sxs-lookup"><span data-stu-id="b5544-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="b5544-266">Предположим, что у нас имеется файл ответа с именем `source.txt`, который указывает исходный контейнер:</span><span class="sxs-lookup"><span data-stu-id="b5544-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="b5544-267">И файл ответов с именем `dest.txt` задает целевую папку в файловой системе hello:</span><span class="sxs-lookup"><span data-stu-id="b5544-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="b5544-268">А также файл ответа с именем `options.txt`, определяющий параметры для AzCopy:</span><span class="sxs-lookup"><span data-stu-id="b5544-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="b5544-269">toocall AzCopy с этими файлами ответа, все они находятся в каталоге `C:\responsefiles`, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5544-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="b5544-270">AzCopy обрабатывает эта команда также, как если бы вы все hello отдельных параметров в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="b5544-271">Указание подписи общего доступа (SAS)</span><span class="sxs-lookup"><span data-stu-id="b5544-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="b5544-272">Можно также задать SAS для контейнера hello URI:</span><span class="sxs-lookup"><span data-stu-id="b5544-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="b5544-273">Папка файлов журнала</span><span class="sxs-lookup"><span data-stu-id="b5544-273">Journal file folder</span></span>
<span data-ttu-id="b5544-274">Каждый раз, когда выдачи команды tooAzCopy, он проверяет, существует ли файл журнала в папке по умолчанию hello, или существует ли в папке, указанного с помощью этого параметра.</span><span class="sxs-lookup"><span data-stu-id="b5544-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="b5544-275">Если файл журнала hello не существует в любом месте, AzCopy считает новые операции hello и создает новый файл журнала.</span><span class="sxs-lookup"><span data-stu-id="b5544-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="b5544-276">Если существует файл журнала hello, AzCopy проверяет, соответствует ли hello командной строки, что вы ввод hello командной строки в файле журнала hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="b5544-277">Если две командные строки hello совпадают, AzCopy возобновляет hello незавершенные операции.</span><span class="sxs-lookup"><span data-stu-id="b5544-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="b5544-278">Если они не совпадают, появится запрос tooeither перезаписать hello журнала файла toostart новую операцию или toocancel hello текущей операции.</span><span class="sxs-lookup"><span data-stu-id="b5544-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="b5544-279">Если необходимо использовать расположение по умолчанию hello toouse для файла журнала hello:</span><span class="sxs-lookup"><span data-stu-id="b5544-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="b5544-280">Если параметр опущен `/Z`, или задайте параметр `/Z` без hello путь к папке, как показано выше, AzCopy создает файл журнала hello в расположении по умолчанию hello, а именно `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="b5544-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="b5544-281">Если уже существует файл журнала hello AzCopy возобновляет hello операции на основе файла журнала hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="b5544-282">Если нужно toospecify пользовательское расположение для файла журнала hello:</span><span class="sxs-lookup"><span data-stu-id="b5544-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="b5544-283">Этот пример создает файл журнала hello, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="b5544-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="b5544-284">Если он существует, AzCopy возобновляет hello операции на основе файла журнала hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="b5544-285">Если нужно tooresume операции AzCopy:</span><span class="sxs-lookup"><span data-stu-id="b5544-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="b5544-286">В этом примере возобновляется hello последней операции, которая может не toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b5544-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="b5544-287">Создание файла журнала</span><span class="sxs-lookup"><span data-stu-id="b5544-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="b5544-288">При указании параметра `/V` без указания пути файла toohello подробный журнал, AzCopy создает файл журнала hello в расположении по умолчанию hello, т. е `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="b5544-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="b5544-289">В противном случае можно создать файл журнала в настраиваемом расположении:</span><span class="sxs-lookup"><span data-stu-id="b5544-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="b5544-290">Обратите внимание, что при указании относительного пути, после параметра `/V`, такие как `/V:test/azcopy1.log`, то hello подробного журнала создается в текущем рабочем каталоге hello в вложенную папку с именем `test`.</span><span class="sxs-lookup"><span data-stu-id="b5544-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="b5544-291">Укажите число hello toostart параллельных операций</span><span class="sxs-lookup"><span data-stu-id="b5544-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="b5544-292">Параметр `/NC` указывает hello количество параллельных копирования операций.</span><span class="sxs-lookup"><span data-stu-id="b5544-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="b5544-293">По умолчанию AzCopy запускается определенное число передачи пропускная способность hello tooincrease параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="b5544-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="b5544-294">Для операций с таблицами hello числом одновременных операций — равно toohello количество процессоров, к которым у вас есть.</span><span class="sxs-lookup"><span data-stu-id="b5544-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="b5544-295">Для больших двоичных объектов и файла операций hello числом одновременных операций — равно 8 раз hello число процессоров, к которым у вас есть.</span><span class="sxs-lookup"><span data-stu-id="b5544-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="b5544-296">При выполнении AzCopy в сети с низкой пропускной способностью, можно указать меньшее число /NC tooavoid сбоя, причиной конкуренции ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b5544-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="b5544-297">Запуск AzCopy с использованием эмулятора службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="b5544-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="b5544-298">Вы можете выполнить AzCopy для hello [эмулятор хранилища Azure](storage-use-emulator.md) для больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="b5544-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="b5544-299">и таблиц:</span><span class="sxs-lookup"><span data-stu-id="b5544-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="b5544-300">Параметры AzCopy</span><span class="sxs-lookup"><span data-stu-id="b5544-300">AzCopy Parameters</span></span>
<span data-ttu-id="b5544-301">Параметры для AzCopy описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="b5544-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="b5544-302">Можно также ввести один из следующих команд из командной строки hello для получения справки по использованию AzCopy hello:</span><span class="sxs-lookup"><span data-stu-id="b5544-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="b5544-303">Подробная справка по командной строке AzCopy: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="b5544-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="b5544-304">Подробная справка по параметрам AzCopy: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="b5544-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="b5544-305">Примеры командной строки: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="b5544-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="b5544-306">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="b5544-306">/Source:"source"</span></span>
<span data-ttu-id="b5544-307">Задает hello источник данных, из которого toocopy.</span><span class="sxs-lookup"><span data-stu-id="b5544-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="b5544-308">Hello источник может быть каталог файловой системы, контейнер больших двоичных объектов, виртуальный каталог больших двоичных объектов, общей папки хранилища, каталог файлов хранения или таблицы Azure.</span><span class="sxs-lookup"><span data-stu-id="b5544-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="b5544-309">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="b5544-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="b5544-310">/Dest:"destination"</span></span>
<span data-ttu-id="b5544-311">Указывает toocopy hello назначения для.</span><span class="sxs-lookup"><span data-stu-id="b5544-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="b5544-312">Hello назначения может быть каталог файловой системы, контейнер больших двоичных объектов, виртуальный каталог больших двоичных объектов, общей папки хранилища, каталог файлов хранения или таблицы Azure.</span><span class="sxs-lookup"><span data-stu-id="b5544-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="b5544-313">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="b5544-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="b5544-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="b5544-315">Указывает шаблон файла, указывающее, какие файлы toocopy.</span><span class="sxs-lookup"><span data-stu-id="b5544-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="b5544-316">поведение Hello hello /Pattern параметра определяется расположение hello hello исходных данных, а также наличие hello hello рекурсивный режим.</span><span class="sxs-lookup"><span data-stu-id="b5544-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="b5544-317">Рекурсивный режим задается с помощью параметра "/S.".</span><span class="sxs-lookup"><span data-stu-id="b5544-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="b5544-318">Если hello указанный исходный каталог в файловой системе hello, то действуют стандартные подстановочные знаки, и предоставлен шаблон файла hello противопоставляется файлов в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="b5544-319">Если параметр задан, затем AzCopy также соответствует указанному шаблону hello все файлы в подкаталогах, каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="b5544-320">Если указанный источник hello контейнер больших двоичных объектов или виртуального каталога, подстановочные знаки не применяются.</span><span class="sxs-lookup"><span data-stu-id="b5544-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="b5544-321">Если параметр задан, затем AzCopy интерпретирует шаблон hello указанный файл как префикс большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="b5544-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="b5544-322">Если параметр /S не указан, затем AzCopy соответствует шаблону файла hello с именами требуемый BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="b5544-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="b5544-323">Если источником является Azure файловый ресурс, то необходимо указать hello точное имя файла, (например abc.txt) hello toocopy один файл, или укажите параметр /S toocopy все файлы в общей папки рекурсивно hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="b5544-324">Попытка toospecify и шаблону файла и параметр /S вместе приведет к ошибку.</span><span class="sxs-lookup"><span data-stu-id="b5544-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="b5544-325">AzCopy использует сопоставление с учетом регистра, когда hello/source — это контейнер больших двоичных объектов или виртуальный каталог больших двоичных объектов и Здравствуйте, используются без учета регистра, сопоставления во всех других случаях.</span><span class="sxs-lookup"><span data-stu-id="b5544-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="b5544-326">Hello файл шаблон по умолчанию, используемый, когда указан шаблон нет файла является *.*</span><span class="sxs-lookup"><span data-stu-id="b5544-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="b5544-327">для расположения файловой системы или пустой префикс для расположения службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5544-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="b5544-328">Задание нескольких шаблонов не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b5544-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="b5544-329">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="b5544-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="b5544-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="b5544-331">Указывает ключ учетной записи хранения hello для hello конечного ресурса.</span><span class="sxs-lookup"><span data-stu-id="b5544-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="b5544-332">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="b5544-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="b5544-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="b5544-334">Задает подпись общего доступа (SAS) с разрешениями на чтение и запись для назначения hello (если применимо).</span><span class="sxs-lookup"><span data-stu-id="b5544-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="b5544-335">Заключение hello SAS в двойные кавычки, он может содержит специальные знаки командной строки.</span><span class="sxs-lookup"><span data-stu-id="b5544-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="b5544-336">Если ресурсы назначения hello контейнер больших двоичных объектов, общей папки или таблицу, можно либо указать этот параметр, следуют маркер SAS hello или hello SAS можно указать как часть hello конечный контейнер больших двоичных объектов, общая папка или URI таблицы без этого параметра.</span><span class="sxs-lookup"><span data-stu-id="b5544-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="b5544-337">Если hello источником и назначением является обоих больших двоичных объектов, то hello целевой большой двоичный объект должен находиться на hello же учетной записи хранилища BLOB-объект источника hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="b5544-338">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="b5544-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="b5544-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="b5544-340">Указывает ключ учетной записи хранения hello для hello исходного ресурса.</span><span class="sxs-lookup"><span data-stu-id="b5544-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="b5544-341">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="b5544-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="b5544-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="b5544-343">Задает подпись общего доступа с разрешениями чтения и список для источника hello (если применимо).</span><span class="sxs-lookup"><span data-stu-id="b5544-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="b5544-344">Заключение hello SAS в двойные кавычки, он может содержит специальные знаки командной строки.</span><span class="sxs-lookup"><span data-stu-id="b5544-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="b5544-345">Если hello источника ресурсов — это контейнер больших двоичных объектов и подписанный URL-адрес, ни ключ предоставляется, контейнер больших двоичных объектов hello будут считываться через анонимный доступ.</span><span class="sxs-lookup"><span data-stu-id="b5544-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="b5544-346">Если источник hello в общей папке или таблицу, необходимо указать ключ или SAS.</span><span class="sxs-lookup"><span data-stu-id="b5544-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="b5544-347">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="b5544-348">/S</span><span class="sxs-lookup"><span data-stu-id="b5544-348">/S</span></span>
<span data-ttu-id="b5544-349">Задает рекурсивный режим для операций копирования.</span><span class="sxs-lookup"><span data-stu-id="b5544-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="b5544-350">В режиме рекурсивные AzCopy скопирует все BLOB-объектов или файлов, соответствующих шаблону hello указанного файла, включая файлы во вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="b5544-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="b5544-351">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="b5544-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="b5544-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="b5544-353">Указывает, является ли BLOB-объект назначения hello блочный BLOB-объект, большой двоичный объект страницы или добавочный большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="b5544-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="b5544-354">Этот параметр применяется только при передаче большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="b5544-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="b5544-355">В противном случае возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="b5544-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="b5544-356">Если целевой hello является большой двоичный объект, и этот параметр не указан, по умолчанию AzCopy создает большой двоичный объект блока.</span><span class="sxs-lookup"><span data-stu-id="b5544-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="b5544-357">**Применимо к** большим двоичным объектам.</span><span class="sxs-lookup"><span data-stu-id="b5544-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="b5544-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="b5544-358">/CheckMD5</span></span>
<span data-ttu-id="b5544-359">Вычисляет хэш MD5 для загруженных данных и проверяет, что хэш MD5 hello хранимых в большом двоичном объекте hello или свойства Content-MD5 файла соответствует hello вычислить хэш.</span><span class="sxs-lookup"><span data-stu-id="b5544-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="b5544-360">Проверка Hello MD5 отключена по умолчанию, поэтому эта проверка MD5 hello tooperform параметра необходимо указать при загрузке данных.</span><span class="sxs-lookup"><span data-stu-id="b5544-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="b5544-361">Обратите внимание, что хранилище Azure не гарантирует, что hello хэш MD5, сохраненное для большого двоичного объекта hello, или файл актуален.</span><span class="sxs-lookup"><span data-stu-id="b5544-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="b5544-362">Это клиента ответственности tooupdate hello MD5 при каждом изменении hello большого двоичного объекта или файла.</span><span class="sxs-lookup"><span data-stu-id="b5544-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="b5544-363">AzCopy всегда задает hello свойства Content-MD5 для BLOB-объектов Azure или файл после его отправки toohello службы.</span><span class="sxs-lookup"><span data-stu-id="b5544-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="b5544-364">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="b5544-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="b5544-365">/Snapshot</span></span>
<span data-ttu-id="b5544-366">Указывает, является ли tootransfer моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="b5544-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="b5544-367">Этот параметр допустим, только когда источник hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="b5544-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="b5544-368">Hello моментальные снимки переносятся большого двоичного объекта переименовываются в следующем формате: .extension blob-name (время создания моментального снимка)</span><span class="sxs-lookup"><span data-stu-id="b5544-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="b5544-369">По умолчанию моментальные снимки не копируются.</span><span class="sxs-lookup"><span data-stu-id="b5544-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="b5544-370">**Применимо к** большим двоичным объектам.</span><span class="sxs-lookup"><span data-stu-id="b5544-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="b5544-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="b5544-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="b5544-372">Выводит сообщения с подробным состоянием в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="b5544-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="b5544-373">По умолчанию hello подробный файл журнала называется AzCopyVerbose.log в `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="b5544-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="b5544-374">Если указать расположение существующих файлов, для этого параметра hello подробный журнал будет присоединенных toothat файл.</span><span class="sxs-lookup"><span data-stu-id="b5544-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="b5544-375">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="b5544-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="b5544-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="b5544-377">Задает папку файла журнала для возобновления операции.</span><span class="sxs-lookup"><span data-stu-id="b5544-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="b5544-378">AzCopy всегда поддерживает возобновление, если операция была прервана.</span><span class="sxs-lookup"><span data-stu-id="b5544-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="b5544-379">Если этот параметр не указан или указан без путь к папке, AzCopy создаст файл журнала hello в расположении по умолчанию hello, а именно % LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b5544-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="b5544-380">Каждый раз, когда выдачи команды tooAzCopy, он проверяет, существует ли файл журнала в папке по умолчанию hello, или существует ли в папке, указанного с помощью этого параметра.</span><span class="sxs-lookup"><span data-stu-id="b5544-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="b5544-381">Если файл журнала hello не существует в любом месте, AzCopy считает новые операции hello и создает новый файл журнала.</span><span class="sxs-lookup"><span data-stu-id="b5544-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="b5544-382">Если существует файл журнала hello, AzCopy проверяет, соответствует ли hello командной строки, что вы ввод hello командной строки в файле журнала hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="b5544-383">Если две командные строки hello совпадают, AzCopy возобновляет hello незавершенные операции.</span><span class="sxs-lookup"><span data-stu-id="b5544-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="b5544-384">Если они не совпадают, появится запрос tooeither перезаписать hello журнала файла toostart новую операцию или toocancel hello текущей операции.</span><span class="sxs-lookup"><span data-stu-id="b5544-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="b5544-385">файл журнала Hello удаляется после успешного завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="b5544-386">Обратите внимание, что возобновление операции из файла журнала, созданного предыдущей версией AzCopy, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b5544-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="b5544-387">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="b5544-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="b5544-388">/@:"parameter-file"</span></span>
<span data-ttu-id="b5544-389">Задает файл, который содержит параметры.</span><span class="sxs-lookup"><span data-stu-id="b5544-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="b5544-390">AzCopy процессы hello параметры в файле hello, как если бы они были указаны в командной строке hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="b5544-391">В файле ответа можно либо задать несколько параметров в одной строке, либо задать каждый параметр в отдельной строке.</span><span class="sxs-lookup"><span data-stu-id="b5544-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="b5544-392">Обратите внимание, что отдельный параметр не может занимать несколько строк.</span><span class="sxs-lookup"><span data-stu-id="b5544-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="b5544-393">Файлы ответа могут содержать комментарии строки, начинающиеся с символа # hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="b5544-394">Можно задать несколько файлов ответов.</span><span class="sxs-lookup"><span data-stu-id="b5544-394">You can specify multiple response files.</span></span> <span data-ttu-id="b5544-395">Однако, следует иметь в виду, что AzCopy не поддерживает вложенных фалов ответов.</span><span class="sxs-lookup"><span data-stu-id="b5544-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="b5544-396">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="b5544-397">/Y</span><span class="sxs-lookup"><span data-stu-id="b5544-397">/Y</span></span>
<span data-ttu-id="b5544-398">Скрывает все запросы на подтверждение AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b5544-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="b5544-399">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="b5544-400">/L</span><span class="sxs-lookup"><span data-stu-id="b5544-400">/L</span></span>
<span data-ttu-id="b5544-401">Задает только операцию перечисления, данные не копируются.</span><span class="sxs-lookup"><span data-stu-id="b5544-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="b5544-402">AzCopy будет интерпретировать hello с помощью этого параметра, как моделирования для выполнения командной строки hello без этого параметра/l и подсчитать, сколько объектов будут скопированы, можно указать параметр /V на hello одновременную toocheck объектов, которые будут скопированы в hello подробного журнала.</span><span class="sxs-lookup"><span data-stu-id="b5544-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="b5544-403">Hello поведение этого параметра также определяется наличие hello hello рекурсивные параметр /S и файл шаблона режим /Pattern и расположение hello hello исходных данных.</span><span class="sxs-lookup"><span data-stu-id="b5544-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="b5544-404">При использовании этого параметра AzCopy необходимы права на ЧТЕНИЕ и СОЗДАНИЕ СПИСКА для местоположения исходных данных.</span><span class="sxs-lookup"><span data-stu-id="b5544-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="b5544-405">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="b5544-406">/MT</span><span class="sxs-lookup"><span data-stu-id="b5544-406">/MT</span></span>
<span data-ttu-id="b5544-407">Задает время последнего изменения hello загруженный файл toobe Здравствуйте таким же, как hello исходного большого двоичного объекта или файла.</span><span class="sxs-lookup"><span data-stu-id="b5544-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="b5544-408">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="b5544-409">/XN</span><span class="sxs-lookup"><span data-stu-id="b5544-409">/XN</span></span>
<span data-ttu-id="b5544-410">Исключает более новый исходный ресурс.</span><span class="sxs-lookup"><span data-stu-id="b5544-410">Excludes a newer source resource.</span></span> <span data-ttu-id="b5544-411">Если hello время последнего изменения источника hello hello же или более новая, чем целевой ресурс Hello не копируются.</span><span class="sxs-lookup"><span data-stu-id="b5544-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="b5544-412">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="b5544-413">/XO</span><span class="sxs-lookup"><span data-stu-id="b5544-413">/XO</span></span>
<span data-ttu-id="b5544-414">Исключает более старый исходный ресурс.</span><span class="sxs-lookup"><span data-stu-id="b5544-414">Excludes an older source resource.</span></span> <span data-ttu-id="b5544-415">Если hello время последнего изменения источника hello hello же или более ранней, чем целевой ресурс Hello не копируются.</span><span class="sxs-lookup"><span data-stu-id="b5544-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="b5544-416">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="b5544-417">/A</span><span class="sxs-lookup"><span data-stu-id="b5544-417">/A</span></span>
<span data-ttu-id="b5544-418">Отправляет только файлы, имеющие атрибут "архивный" hello набор.</span><span class="sxs-lookup"><span data-stu-id="b5544-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="b5544-419">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="b5544-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="b5544-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="b5544-421">Передачи только файлы, содержащие любое hello указанный набор атрибутов.</span><span class="sxs-lookup"><span data-stu-id="b5544-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="b5544-422">Доступные атрибуты:</span><span class="sxs-lookup"><span data-stu-id="b5544-422">Available attributes include:</span></span>

* <span data-ttu-id="b5544-423">R — файлы только для чтения</span><span class="sxs-lookup"><span data-stu-id="b5544-423">R = Read-only files</span></span>
* <span data-ttu-id="b5544-424">A — файлы, готовые к архивированию</span><span class="sxs-lookup"><span data-stu-id="b5544-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="b5544-425">S — системные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-425">S = System files</span></span>
* <span data-ttu-id="b5544-426">H — скрытые файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-426">H = Hidden files</span></span>
* <span data-ttu-id="b5544-427">C — сжатые файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-427">C = Compressed files</span></span>
* <span data-ttu-id="b5544-428">N — обычные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-428">N = Normal files</span></span>
* <span data-ttu-id="b5544-429">E — зашифрованные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-429">E = Encrypted files</span></span>
* <span data-ttu-id="b5544-430">T — временные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-430">T = Temporary files</span></span>
* <span data-ttu-id="b5544-431">O — автономные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-431">O = Offline files</span></span>
* <span data-ttu-id="b5544-432">I — неиндексированные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-432">I = Non-indexed files</span></span>

<span data-ttu-id="b5544-433">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="b5544-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="b5544-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="b5544-435">Исключает файлы, содержащие любое hello указанный набор атрибутов.</span><span class="sxs-lookup"><span data-stu-id="b5544-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="b5544-436">Доступные атрибуты:</span><span class="sxs-lookup"><span data-stu-id="b5544-436">Available attributes include:</span></span>

* <span data-ttu-id="b5544-437">R — файлы только для чтения</span><span class="sxs-lookup"><span data-stu-id="b5544-437">R = Read-only files</span></span>
* <span data-ttu-id="b5544-438">A — файлы, готовые к архивированию</span><span class="sxs-lookup"><span data-stu-id="b5544-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="b5544-439">S — системные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-439">S = System files</span></span>
* <span data-ttu-id="b5544-440">H — скрытые файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-440">H = Hidden files</span></span>
* <span data-ttu-id="b5544-441">C — сжатые файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-441">C = Compressed files</span></span>
* <span data-ttu-id="b5544-442">N — обычные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-442">N = Normal files</span></span>
* <span data-ttu-id="b5544-443">E — зашифрованные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-443">E = Encrypted files</span></span>
* <span data-ttu-id="b5544-444">T — временные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-444">T = Temporary files</span></span>
* <span data-ttu-id="b5544-445">O — автономные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-445">O = Offline files</span></span>
* <span data-ttu-id="b5544-446">I — неиндексированные файлы</span><span class="sxs-lookup"><span data-stu-id="b5544-446">I = Non-indexed files</span></span>

<span data-ttu-id="b5544-447">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="b5544-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="b5544-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="b5544-449">Указывает, что символ-разделитель hello использовать toodelimit виртуальные каталоги в имени большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="b5544-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="b5544-450">По умолчанию использует AzCopy / как символ-разделитель hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="b5544-451">Однако, AzCopy поддерживает любой общий символ (например, @, # или %) в качестве разделителя.</span><span class="sxs-lookup"><span data-stu-id="b5544-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="b5544-452">Если вам требуется один из этих специальных символов в командной строке hello tooinclude, заключите имя файла hello в двойные кавычки.</span><span class="sxs-lookup"><span data-stu-id="b5544-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="b5544-453">Этот параметр применяется только для загрузки BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="b5544-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="b5544-454">**Применимо к** большим двоичным объектам.</span><span class="sxs-lookup"><span data-stu-id="b5544-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="b5544-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="b5544-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="b5544-456">Указывает номер hello одновременных операций.</span><span class="sxs-lookup"><span data-stu-id="b5544-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="b5544-457">AzCopy по умолчанию запускается определенное число передачи пропускная способность hello tooincrease параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="b5544-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="b5544-458">Обратите внимание, что большое количество параллельных операций в среде с низкой пропускной способностью может произойти переполнение hello сетевое подключение предотвращают hello операции полностью завершить.</span><span class="sxs-lookup"><span data-stu-id="b5544-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="b5544-459">Регулируйте количество одновременных операций в зависимости от фактической доступной пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="b5544-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="b5544-460">Hello верхний предел для одновременных операций — 512.</span><span class="sxs-lookup"><span data-stu-id="b5544-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="b5544-461">**Применимо к** большим двоичным объектам, файлам, таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="b5544-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="b5544-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="b5544-463">Указывает, что hello `source` ресурсом является большой двоичный объект в hello локальной среде разработки, работающее в эмуляторе хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="b5544-464">**Применимо к** большим двоичным объектам и таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="b5544-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="b5544-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="b5544-466">Указывает, что hello `destination` ресурсом является большой двоичный объект в hello локальной среде разработки, работающее в эмуляторе хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="b5544-467">**Применимо к** большим двоичным объектам и таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="b5544-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="b5544-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="b5544-469">Разбиений hello секции диапазона ключей tooenable Экспорт таблицы данных в параллельном режиме, что повышает скорость hello hello операции экспорта.</span><span class="sxs-lookup"><span data-stu-id="b5544-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="b5544-470">Если этот параметр не указан, AzCopy использует один поток tooexport таблицы сущности.</span><span class="sxs-lookup"><span data-stu-id="b5544-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="b5544-471">Например, если hello пользователь указывает /PKRS: «aa #bb», а затем AzCopy запускает три параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="b5544-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="b5544-472">Каждая операция экспортирует один из диапазонов ключей секций, как это показано на примере ниже:</span><span class="sxs-lookup"><span data-stu-id="b5544-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="b5544-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="b5544-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="b5544-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="b5544-474">[aa, bb)</span></span>

  <span data-ttu-id="b5544-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="b5544-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="b5544-476">**Применимо к** таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="b5544-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="b5544-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="b5544-478">Указывает Здравствуйте экспортированный файл разделить размер в МБ, hello допустимое минимальное значение — 32.</span><span class="sxs-lookup"><span data-stu-id="b5544-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="b5544-479">Если этот параметр не указан, AzCopy экспортирует файл toosingle таблицы данных.</span><span class="sxs-lookup"><span data-stu-id="b5544-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="b5544-480">Если hello таблица содержит данные BLOB-объект экспортированного tooa и hello экспортированный файл достигает размера 200 hello ГБ для размера большого двоичного объекта, AzCopy будет разделить hello экспортированного файла, даже если этот параметр не указан.</span><span class="sxs-lookup"><span data-stu-id="b5544-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="b5544-481">**Применимо к** таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="b5544-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="b5544-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="b5544-483">Задает поведение при импорте данных таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="b5544-484">InsertOrSkip - пропускает существующую сущность или вставляет новую сущность, если она не существует в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="b5544-485">InsertOrMerge - объединяет существующую сущность или вставляет новую сущность, если она не существует в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="b5544-486">InsertOrReplace - заменяет существующую сущность или вставляет новую сущность, если она не существует в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="b5544-487">**Применимо к** таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="b5544-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="b5544-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="b5544-489">Указывает файл манифеста hello hello таблицы экспорта и импорта операции.</span><span class="sxs-lookup"><span data-stu-id="b5544-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="b5544-490">Этот параметр является необязательным, во время операции экспорта hello, AzCopy создает файл манифеста с предварительно определенное имя, если этот параметр не указан.</span><span class="sxs-lookup"><span data-stu-id="b5544-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="b5544-491">Этот параметр является обязательным, во время операции импорта hello поиска файлов данных hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="b5544-492">**Применимо к** таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="b5544-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="b5544-493">/SyncCopy</span></span>
<span data-ttu-id="b5544-494">Указывает ли toosynchronously копирование больших двоичных объектов или файлов между двумя конечными точками службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b5544-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="b5544-495">По умолчанию AzCopy использует серверное асинхронное копирование.</span><span class="sxs-lookup"><span data-stu-id="b5544-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="b5544-496">Укажите этот параметр tooperform синхронного копирования, который загружает большие двоичные объекты или файлы памяти toolocal и отправляет их tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="b5544-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="b5544-497">Этот параметр можно использовать при копировании файлов в хранилище больших двоичных объектов в хранилище файлов или из большого двоичного объекта хранилища tooFile хранилища, и наоборот.</span><span class="sxs-lookup"><span data-stu-id="b5544-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="b5544-498">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="b5544-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="b5544-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="b5544-500">Задает тип содержимого MIME hello для целевых больших двоичных объектов или файлов.</span><span class="sxs-lookup"><span data-stu-id="b5544-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="b5544-501">Наборы AzCopy hello тип содержимого большого двоичного объекта или файла tooapplication/octet-stream по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b5544-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="b5544-502">Можно задать тип содержимого hello для всех больших двоичных объектов или файлы, явно указав значение для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="b5544-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="b5544-503">При указании этого параметра без указания значения AzCopy установит каждый BLOB-объект или тип содержимого файла, в соответствии с tooits расширение файла.</span><span class="sxs-lookup"><span data-stu-id="b5544-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="b5544-504">**Применимо к** большим двоичным объектам и файлам.</span><span class="sxs-lookup"><span data-stu-id="b5544-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="b5544-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="b5544-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="b5544-506">Задает формат hello hello таблицы экспортированного файла данных.</span><span class="sxs-lookup"><span data-stu-id="b5544-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="b5544-507">Если этот параметр не указан, по умолчанию AzCopy экспортирует файл данных таблицы в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b5544-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="b5544-508">**Применимо к** таблицам.</span><span class="sxs-lookup"><span data-stu-id="b5544-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="b5544-509">Известные проблемы и рекомендации</span><span class="sxs-lookup"><span data-stu-id="b5544-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="b5544-510">Ограничение одновременных операций записи при копировании данных</span><span class="sxs-lookup"><span data-stu-id="b5544-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="b5544-511">При копировании больших двоичных объектов или файлов с помощью AzCopy, имейте в виду, возможно, изменение другое приложение hello данных при копировании его.</span><span class="sxs-lookup"><span data-stu-id="b5544-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="b5544-512">Если это возможно убедитесь, hello данных при копировании не изменяется во время операции копирования hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="b5544-513">Например при копировании виртуальный жесткий ДИСК, связанный с виртуальной машины Azure, убедитесь, что нет других приложений в настоящее время пишете toohello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="b5544-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="b5544-514">Toodo хорошим способом это по аренде toobe ресурсов hello копируются.</span><span class="sxs-lookup"><span data-stu-id="b5544-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="b5544-515">Кроме того можно сначала создать моментальный снимок виртуального жесткого диска hello и скопируйте hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="b5544-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="b5544-516">Если не может помешать записи tooblobs или файлы, пока они копируются, то следует помнить, заданием hello hello время завершения работы других приложений, hello скопированных ресурсов может больше нет полной четности с ресурсами источника hello.</span><span class="sxs-lookup"><span data-stu-id="b5544-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="b5544-517">Запускайте один экземпляр AzCopy на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b5544-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="b5544-518">AzCopy является использование hello спроектированный toomaximize скорость передачи данных ресурсов tooaccelerate машины hello, мы рекомендуем запустить только один экземпляр AzCopy на одном компьютере и укажите параметр hello `/NC` при необходимости несколько параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="b5544-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="b5544-519">Для получения дополнительных сведений введите `AzCopy /?:NC` hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="b5544-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="b5544-520">Включайте FIPS-совместимые алгоритмы MD5 для AzCopy при использовании FIPS-совместимых алгоритмов для шифрования, хэширования и подписывания.</span><span class="sxs-lookup"><span data-stu-id="b5544-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="b5544-521">AzCopy по умолчанию использует .NET MD5 реализацию toocalculate hello MD5 при копировании объектов, но существуют некоторые требования безопасности, которым требуется параметром совместимости MD5 AzCopy tooenable FIPS.</span><span class="sxs-lookup"><span data-stu-id="b5544-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="b5544-522">Для этого можно создать файл app.config `AzCopy.exe.config` со свойством `AzureStorageUseV1MD5` и поместить его в папку с файлом AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="b5544-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="b5544-523">Для свойства «AzureStorageUseV1MD5» • True: значение по умолчанию hello, AzCopy будет использоваться реализация .NET MD5.</span><span class="sxs-lookup"><span data-stu-id="b5544-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="b5544-524">• False - будет использоваться FIPS-совместимый алгоритм MD5.</span><span class="sxs-lookup"><span data-stu-id="b5544-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="b5544-525">Обратите внимание, что по умолчанию на компьютере Windows FIPS-совместимые алгоритмы отключены. Эту настройку можно изменить, набрав в окне запуска команд "secpol.msc" и выбрав "Настройки безопасности -> Локальные политики -> Параметры безопасности -> Системная криптография: Использовать FIPS-совместимые алгоритмы для шифрования, хеширования и подписывания".</span><span class="sxs-lookup"><span data-stu-id="b5544-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5544-526">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5544-526">Next steps</span></span>
<span data-ttu-id="b5544-527">Дополнительные сведения о хранилище Azure и AzCopy см. следующие ресурсы toohello.</span><span class="sxs-lookup"><span data-stu-id="b5544-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="b5544-528">Документация по хранилищу Azure:</span><span class="sxs-lookup"><span data-stu-id="b5544-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="b5544-529">Введение tooAzure хранилища</span><span class="sxs-lookup"><span data-stu-id="b5544-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="b5544-530">Как toouse хранилища BLOB-объектов из .NET</span><span class="sxs-lookup"><span data-stu-id="b5544-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="b5544-531">Как toouse хранения файлов из .NET</span><span class="sxs-lookup"><span data-stu-id="b5544-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="b5544-532">Как toouse хранилище таблиц из .NET</span><span class="sxs-lookup"><span data-stu-id="b5544-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="b5544-533">Как управлять toocreate, или удалить учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="b5544-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="b5544-534">Перенос данных с помощью AzCopy для Linux</span><span class="sxs-lookup"><span data-stu-id="b5544-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="b5544-535">Записи блога по хранилищу Azure:</span><span class="sxs-lookup"><span data-stu-id="b5544-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="b5544-536">Введение в предварительную версию библиотеки движения данных в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="b5544-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="b5544-537">AzCopy: введение в синхронное копирование и настраиваемый тип содержимого</span><span class="sxs-lookup"><span data-stu-id="b5544-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="b5544-538">AzCopy: выпуск общедоступной версии AzCopy 3.0 и предварительной версии AzCopy 4.0 с поддержкой таблиц и файлов</span><span class="sxs-lookup"><span data-stu-id="b5544-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="b5544-539">AzCopy: оптимизированные сценарии для крупномасштабного копирования</span><span class="sxs-lookup"><span data-stu-id="b5544-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="b5544-540">AzCopy: поддержка геоизбыточного хранилища для доступа с правом чтения</span><span class="sxs-lookup"><span data-stu-id="b5544-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="b5544-541">AzCopy: передача данных с использованием перезапускаемого режима и маркера SAS</span><span class="sxs-lookup"><span data-stu-id="b5544-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="b5544-542">AzCopy: использование копирования больших двоичных объектов между разными учетными записями</span><span class="sxs-lookup"><span data-stu-id="b5544-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="b5544-543">AzCopy: отправка и скачивание файлов для больших двоичных объектов Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b5544-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

