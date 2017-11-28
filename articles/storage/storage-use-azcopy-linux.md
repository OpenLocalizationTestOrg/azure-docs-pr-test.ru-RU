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
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="d2d15-105">Перенос данных с помощью AzCopy для Linux</span><span class="sxs-lookup"><span data-stu-id="d2d15-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="d2d15-106">AzCopy в Linux является командной строки служебная программа, разработанная для копирования данных tooand из хранилища больших двоичных объектов Microsoft Azure и файл с помощью простой команды с оптимальной производительностью.</span><span class="sxs-lookup"><span data-stu-id="d2d15-106">AzCopy on Linux is a command-line utility designed for copying data tooand from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="d2d15-107">Можно скопировать данные из одного объекта tooanother в вашей учетной записи хранения или между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="d2d15-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="d2d15-108">Существуют две версии AzCopy, которые можно скачать.</span><span class="sxs-lookup"><span data-stu-id="d2d15-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="d2d15-109">Служебная программа AzCopy для Linux основана на платформе .NET Core, которая нацелена на платформы Linux, использующие параметры командной строки в формате POSIX.</span><span class="sxs-lookup"><span data-stu-id="d2d15-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="d2d15-110">Служебная программа [AzCopy для Windows](storage-use-azcopy.md) основана на платформе .NET Framework и использует параметры командной строки в формате Windows.</span><span class="sxs-lookup"><span data-stu-id="d2d15-110">[AzCopy on Windows](storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="d2d15-111">В этой статье рассматривается AzCopy для Linux.</span><span class="sxs-lookup"><span data-stu-id="d2d15-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="d2d15-112">Скачивание и установка AzCopy</span><span class="sxs-lookup"><span data-stu-id="d2d15-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="d2d15-113">Установка в Linux</span><span class="sxs-lookup"><span data-stu-id="d2d15-113">Installation on Linux</span></span>

<span data-ttu-id="d2d15-114">AzCopy в Linux требуется .NET Core framework на платформе hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-114">AzCopy on Linux requires .NET Core framework on hello platform.</span></span> <span data-ttu-id="d2d15-115">См. инструкции по установке hello hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) страницы.</span><span class="sxs-lookup"><span data-stu-id="d2d15-115">See hello installation instructions on hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="d2d15-116">Для примера давайте установим .NET Core в Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="d2d15-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="d2d15-117">Hello последние руководства, посетите [.NET Core для Linux](https://www.microsoft.com/net/core#linuxubuntu) страница установки.</span><span class="sxs-lookup"><span data-stu-id="d2d15-117">For hello latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="d2d15-118">После установки .NET Core скачайте и установите AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d2d15-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="d2d15-119">После установки AzCopy в Linux можно удалить файлы извлечены hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-119">You can remove hello extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="d2d15-120">Также если у вас права суперпользователя, также запускаются AzCopy с помощью сценария оболочки hello «azcopy» в извлеченной папке hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using hello shell script 'azcopy' in hello extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="d2d15-121">Альтернативная установка в Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d2d15-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="d2d15-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="d2d15-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="d2d15-123">Добавьте источник apt для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d2d15-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="d2d15-124">Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d2d15-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="d2d15-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="d2d15-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="d2d15-126">Добавьте источник apt для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d2d15-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="d2d15-127">Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d2d15-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="d2d15-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="d2d15-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="d2d15-129">Добавьте источник apt для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d2d15-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="d2d15-130">Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d2d15-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="d2d15-131">Написание первой команды AzCopy</span><span class="sxs-lookup"><span data-stu-id="d2d15-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="d2d15-132">Базовый синтаксис команды AzCopy Hello таков:</span><span class="sxs-lookup"><span data-stu-id="d2d15-132">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="d2d15-133">Привет, следующие примеры демонстрируют различные сценарии для копирования данных tooand из файлов и больших двоичных объектов Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d2d15-133">hello following examples demonstrate various scenarios for copying data tooand from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="d2d15-134">См. toohello `azcopy --help` меню подробное описание параметров hello, используемых в каждой выборке.</span><span class="sxs-lookup"><span data-stu-id="d2d15-134">Refer toohello `azcopy --help` menu for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="d2d15-135">Большой двоичный объект: скачивание</span><span class="sxs-lookup"><span data-stu-id="d2d15-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="d2d15-136">Скачивание одного большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="d2d15-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="d2d15-137">Если папка hello `/mnt/myfiles` не существует, AzCopy создает его и загружает `abc.txt ` в новую папку hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-137">If hello folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="d2d15-138">Скачивание большого двоичного объекта из дополнительного региона</span><span class="sxs-lookup"><span data-stu-id="d2d15-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="d2d15-139">Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.</span><span class="sxs-lookup"><span data-stu-id="d2d15-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="d2d15-140">Скачивание всех больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="d2d15-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="d2d15-141">Предположим следующее hello большие двоичные объекты находятся в указанном контейнере hello:</span><span class="sxs-lookup"><span data-stu-id="d2d15-141">Assume hello following blobs reside in hello specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="d2d15-142">После завершения операции загрузки hello hello каталог `/mnt/myfiles` включает hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="d2d15-142">After hello download operation, hello directory `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="d2d15-143">Если не задать параметр `--recursive`, большие двоичные объекты не будут скачаны.</span><span class="sxs-lookup"><span data-stu-id="d2d15-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="d2d15-144">Скачивание больших двоичных объектов с указанным префиксом</span><span class="sxs-lookup"><span data-stu-id="d2d15-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="d2d15-145">Предположим следующее hello большие двоичные объекты находятся в указанном контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-145">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="d2d15-146">Все большие двоичные объекты, начинающиеся с префикса hello `a` загружаются.</span><span class="sxs-lookup"><span data-stu-id="d2d15-146">All blobs beginning with hello prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="d2d15-147">После завершения операции загрузки hello hello папку `/mnt/myfiles` включает hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="d2d15-147">After hello download operation, hello folder `/mnt/myfiles` includes hello following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="d2d15-148">префикс Hello применяется toohello виртуальному каталогу, который формирует первую часть имени большого двоичного объекта hello hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-148">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="d2d15-149">В приведенном выше примере hello hello виртуального каталога не соответствует hello указанного префикса, поэтому BLOB-объекты не загружается.</span><span class="sxs-lookup"><span data-stu-id="d2d15-149">In hello example shown above, hello virtual directory does not match hello specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="d2d15-150">Кроме того, если hello параметр `--recursive` не указан, AzCopy не загружать все большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="d2d15-150">In addition, if hello option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="d2d15-151">Задать время последнего изменения hello toobe экспортированные файлы так же, как hello исходный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="d2d15-151">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="d2d15-152">Большие двоичные объекты можно также исключить из операции загрузки hello, на основе их времени последнего изменения.</span><span class="sxs-lookup"><span data-stu-id="d2d15-152">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="d2d15-153">Например, большие двоичные объекты tooexclude, время последнего изменения — hello же или более новая, чем конечный файл hello, добавить hello `--exclude-newer` параметр:</span><span class="sxs-lookup"><span data-stu-id="d2d15-153">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="d2d15-154">Или если вы хотите tooexclude BLOB-объектов, время последнего изменения — hello же или более ранней, чем конечный файл hello, добавьте hello `--exclude-older` параметр:</span><span class="sxs-lookup"><span data-stu-id="d2d15-154">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="d2d15-155">Большой двоичный объект: отправка</span><span class="sxs-lookup"><span data-stu-id="d2d15-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="d2d15-156">Отправка одного файла</span><span class="sxs-lookup"><span data-stu-id="d2d15-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="d2d15-157">Если hello указанный контейнер не существует, AzCopy создает эту службу и передачи файла hello в него.</span><span class="sxs-lookup"><span data-stu-id="d2d15-157">If hello specified destination container does not exist, AzCopy creates it and uploads hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="d2d15-158">Отправка одного файла каталога toovirtual</span><span class="sxs-lookup"><span data-stu-id="d2d15-158">Upload single file toovirtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="d2d15-159">Если hello указанный виртуальный каталог не существует, AzCopy передает hello tooinclude файл hello виртуальный каталог hello имя BLOB-объекта (*например*, `vd/abc.txt` в приведенном выше примере hello).</span><span class="sxs-lookup"><span data-stu-id="d2d15-159">If hello specified virtual directory does not exist, AzCopy uploads hello file tooinclude hello virtual directory in hello blob name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="d2d15-160">Отправка всех файлов</span><span class="sxs-lookup"><span data-stu-id="d2d15-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="d2d15-161">Задание параметра `--recursive` содержимое передачи hello hello указано рекурсивно хранилища tooBlob каталога, то есть также загрузить свои файлы и все вложенные папки.</span><span class="sxs-lookup"><span data-stu-id="d2d15-161">Specifying option `--recursive` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="d2d15-162">Например, предположим, hello следующие файлы размещаются в папке `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="d2d15-162">For instance, assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="d2d15-163">После завершения операции отправки hello hello контейнер содержит hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="d2d15-163">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="d2d15-164">Здравствуйте, когда параметр `--recursive` не определено, только hello следующие три отправки файлов:</span><span class="sxs-lookup"><span data-stu-id="d2d15-164">When hello option `--recursive` is not specified, only hello following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="d2d15-165">Отправка файлов, соответствующих указанному шаблону</span><span class="sxs-lookup"><span data-stu-id="d2d15-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="d2d15-166">Предполагается hello следующие файлы размещаются в папке `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="d2d15-166">Assume hello following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="d2d15-167">После завершения операции отправки hello hello контейнер содержит hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="d2d15-167">After hello upload operation, hello container includes hello following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="d2d15-168">Здравствуйте, когда параметр `--recursive` не указан, AzCopy пропускает файлы, находящиеся в вложенные каталоги:</span><span class="sxs-lookup"><span data-stu-id="d2d15-168">When hello option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="d2d15-169">Укажите hello MIME-тип содержимого большого двоичного объекта назначения</span><span class="sxs-lookup"><span data-stu-id="d2d15-169">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="d2d15-170">По умолчанию AzCopy задает тип содержимого hello BLOB-объект назначения, слишком`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="d2d15-170">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="d2d15-171">Тем не менее, можно явно указать тип содержимого hello через параметр hello `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="d2d15-171">However, you can explicitly specify hello content type via hello option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="d2d15-172">Этот синтаксис задает hello-тип содержимого для всех больших двоичных объектов в операции передачи.</span><span class="sxs-lookup"><span data-stu-id="d2d15-172">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="d2d15-173">Если hello параметр `--set-content-type` указан без значения, то AzCopy задает каждого большого двоичного объекта или файла тип содержимого в соответствии с tooits расширение файла.</span><span class="sxs-lookup"><span data-stu-id="d2d15-173">If hello option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according tooits file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="d2d15-174">Большой двоичный объект: копирование</span><span class="sxs-lookup"><span data-stu-id="d2d15-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="d2d15-175">Копирование большого двоичного объекта в пределах учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="d2d15-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="d2d15-176">При копировании большого двоичного объекта без параметра --sync-copy выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2d15-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="d2d15-177">Копирование большого двоичного объекта между различными учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="d2d15-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="d2d15-178">При копировании большого двоичного объекта без параметра --sync-copy выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2d15-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="d2d15-179">Копирование одного большого двоичного объекта из области tooprimary дополнительный регион</span><span class="sxs-lookup"><span data-stu-id="d2d15-179">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="d2d15-180">Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.</span><span class="sxs-lookup"><span data-stu-id="d2d15-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="d2d15-181">Копирование большого двоичного объекта и его моментальных снимков между различными учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="d2d15-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="d2d15-182">После завершения операции копирования hello hello целевой контейнер включает hello большого двоичного объекта и его моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="d2d15-182">After hello copy operation, hello target container includes hello blob and its snapshots.</span></span> <span data-ttu-id="d2d15-183">Hello контейнер включает в себя следующие hello большого двоичного объекта и его моментальные снимки:</span><span class="sxs-lookup"><span data-stu-id="d2d15-183">hello container includes hello following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="d2d15-184">Синхронное копирование больших двоичных объектов между учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="d2d15-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="d2d15-185">По умолчанию AzCopy выполняет асинхронное копирование данных между двумя конечными точками хранилища.</span><span class="sxs-lookup"><span data-stu-id="d2d15-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="d2d15-186">Таким образом копируется hello копирования операция выполняется в фоновом режиме hello, используя запасную пропускную способность емкости, которая имеет нет соглашения об уровне ОБСЛУЖИВАНИЯ с точки зрения быстродействия большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="d2d15-186">Therefore, hello copy operation runs in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="d2d15-187">Hello `--sync-copy` параметр гарантирует, что операция копирования hello возвращает согласованные скорость.</span><span class="sxs-lookup"><span data-stu-id="d2d15-187">hello `--sync-copy` option ensures that hello copy operation gets consistent speed.</span></span> <span data-ttu-id="d2d15-188">AzCopy выполняет копирование синхронной hello по загрузке больших двоичных объектов hello toocopy из hello указан источник toolocal памяти и передача их toohello местом назначения хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="d2d15-188">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="d2d15-189">`--sync-copy`может создать копию tooasynchronous исходящих дополнительных затрат по сравнению.</span><span class="sxs-lookup"><span data-stu-id="d2d15-189">`--sync-copy` might generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="d2d15-190">Привет, рекомендованный подход является toouse этот параметр на виртуальной Машине Azure, hello же регионе, что ваш источник учетной записи tooavoid исходящих затраты на хранение.</span><span class="sxs-lookup"><span data-stu-id="d2d15-190">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="d2d15-191">Файл: скачивание</span><span class="sxs-lookup"><span data-stu-id="d2d15-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="d2d15-192">Скачивание одного файла</span><span class="sxs-lookup"><span data-stu-id="d2d15-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="d2d15-193">Если источником является Azure файловый ресурс, то необходимо указать hello точное имя файла, hello (*например* `abc.txt`) toodownload один файл, или задайте параметр `--recursive` toodownload все файлы в папке hello рекурсивно.</span><span class="sxs-lookup"><span data-stu-id="d2d15-193">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `--recursive` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="d2d15-194">Попытка toospecify и шаблону файла и параметр `--recursive` вместе приведет к ошибке.</span><span class="sxs-lookup"><span data-stu-id="d2d15-194">Attempting toospecify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="d2d15-195">Скачивание всех файлов</span><span class="sxs-lookup"><span data-stu-id="d2d15-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="d2d15-196">Обратите внимание на то, что пустые папки не скачиваются.</span><span class="sxs-lookup"><span data-stu-id="d2d15-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="d2d15-197">Файл: отправка</span><span class="sxs-lookup"><span data-stu-id="d2d15-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="d2d15-198">Отправка одного файла</span><span class="sxs-lookup"><span data-stu-id="d2d15-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="d2d15-199">Отправка всех файлов</span><span class="sxs-lookup"><span data-stu-id="d2d15-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="d2d15-200">Обратите внимание на то, что пустые папки не передаются.</span><span class="sxs-lookup"><span data-stu-id="d2d15-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="d2d15-201">Отправка файлов, соответствующих указанному шаблону</span><span class="sxs-lookup"><span data-stu-id="d2d15-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="d2d15-202">Файл: копирование</span><span class="sxs-lookup"><span data-stu-id="d2d15-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="d2d15-203">Копирование общих файловых ресурсов</span><span class="sxs-lookup"><span data-stu-id="d2d15-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="d2d15-204">При копировании файла между файловыми ресурсами выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2d15-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="d2d15-205">Копирование из файла tooblob общей папки</span><span class="sxs-lookup"><span data-stu-id="d2d15-205">Copy from file share tooblob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="d2d15-206">При копировании файла из файла tooblob общего ресурса, [копирование на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) выполняется операция.</span><span class="sxs-lookup"><span data-stu-id="d2d15-206">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="d2d15-207">Скопируйте из папки toofile больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="d2d15-207">Copy from blob toofile share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="d2d15-208">При копировании файлов из папки toofile больших двоичных объектов, [копирование на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) выполняется операция.</span><span class="sxs-lookup"><span data-stu-id="d2d15-208">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="d2d15-209">Синхронное копирование файлов</span><span class="sxs-lookup"><span data-stu-id="d2d15-209">Synchronously copy files</span></span>
<span data-ttu-id="d2d15-210">Можно указать hello `--sync-copy` синхронно параметр toocopy данных из хранилища файлов tooFile хранилища, tooBlob хранения файлов хранилища или tooFile хранилища больших двоичных объектов хранилища.</span><span class="sxs-lookup"><span data-stu-id="d2d15-210">You can specify hello `--sync-copy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously.</span></span> <span data-ttu-id="d2d15-211">AzCopy по загрузке hello источника данных toolocal памяти и передачи их toodestination выполняет этой операции.</span><span class="sxs-lookup"><span data-stu-id="d2d15-211">AzCopy runs this operation by downloading hello source data toolocal memory, and then uploading it toodestination.</span></span> <span data-ttu-id="d2d15-212">В этом случае взимается стандартная плата за исходящий трафик.</span><span class="sxs-lookup"><span data-stu-id="d2d15-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="d2d15-213">При копировании из хранилища файлов tooBlob хранения типа больших двоичных объектов по умолчанию hello блочного BLOB-объекта, пользователь может указать параметр `/BlobType:page` toochange hello конечного большого двоичного объекта типа.</span><span class="sxs-lookup"><span data-stu-id="d2d15-213">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="d2d15-214">Обратите внимание, что `--sync-copy` может создавать дополнительных исходящих стоимости сравнение tooasynchronous копии.</span><span class="sxs-lookup"><span data-stu-id="d2d15-214">Note that `--sync-copy` might generate additional egress cost comparing tooasynchronous copy.</span></span> <span data-ttu-id="d2d15-215">Привет, рекомендованный подход является toouse этот параметр на виртуальной Машине Azure, hello же регионе, что ваш источник учетной записи tooavoid исходящих затраты на хранение.</span><span class="sxs-lookup"><span data-stu-id="d2d15-215">hello recommended approach is toouse this option in an Azure VM, that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="d2d15-216">Другие функции AzCopy</span><span class="sxs-lookup"><span data-stu-id="d2d15-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="d2d15-217">Копирование данных, не существует в месте назначения hello</span><span class="sxs-lookup"><span data-stu-id="d2d15-217">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="d2d15-218">Hello `--exclude-older` и `--exclude-newer` параметры позволяют ресурсы старого или более нового источника tooexclude копируются, соответственно.</span><span class="sxs-lookup"><span data-stu-id="d2d15-218">hello `--exclude-older` and `--exclude-newer` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="d2d15-219">Если требуется только ресурсы toocopy источника, которые не существуют в конечном hello, можно указать оба параметра в hello команды AzCopy:</span><span class="sxs-lookup"><span data-stu-id="d2d15-219">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a><span data-ttu-id="d2d15-220">Использование конфигурации параметров командной строки файл toospecify</span><span class="sxs-lookup"><span data-stu-id="d2d15-220">Use a configuration file toospecify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="d2d15-221">В файл конфигурации можно добавить параметры командной строки AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d2d15-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="d2d15-222">AzCopy процессы hello параметры в файле hello, как если бы они были указаны в командной строке hello, выполнение прямых подстановки с hello содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-222">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="d2d15-223">Предположим, файл конфигурации с именем `copyoperation`, содержащий следующие строки hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-223">Assume a configuration file named `copyoperation`, that contains hello following lines.</span></span> <span data-ttu-id="d2d15-224">Каждый параметр AzCopy можно указать как в одной строке,</span><span class="sxs-lookup"><span data-stu-id="d2d15-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="d2d15-225">так и в разных:</span><span class="sxs-lookup"><span data-stu-id="d2d15-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="d2d15-226">AzCopy завершается неудачей, если параметр hello разбиты на две строки, как показано ниже для hello `--source-key` параметр:</span><span class="sxs-lookup"><span data-stu-id="d2d15-226">AzCopy fails if you split hello parameter across two lines, as shown here for hello `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="d2d15-227">Указание подписи общего доступа (SAS)</span><span class="sxs-lookup"><span data-stu-id="d2d15-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="d2d15-228">Можно также задать SAS для контейнера hello URI:</span><span class="sxs-lookup"><span data-stu-id="d2d15-228">You can also specify a SAS on hello container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="d2d15-229">Обратите внимание, что AzCopy в настоящее время поддерживает только hello [SAS для учетной записи](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="d2d15-229">Note that AzCopy currently only supports hello [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="d2d15-230">Папка файлов журнала</span><span class="sxs-lookup"><span data-stu-id="d2d15-230">Journal file folder</span></span>
<span data-ttu-id="d2d15-231">Каждый раз, когда выдачи команды tooAzCopy, он проверяет, существует ли файл журнала в папке по умолчанию hello, или существует ли в папке, указанного с помощью этого параметра.</span><span class="sxs-lookup"><span data-stu-id="d2d15-231">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="d2d15-232">Если файл журнала hello не существует в любом месте, AzCopy считает новые операции hello и создает новый файл журнала.</span><span class="sxs-lookup"><span data-stu-id="d2d15-232">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="d2d15-233">Если существует файл журнала hello, AzCopy проверяет, соответствует ли hello командной строки, что вы ввод hello командной строки в файле журнала hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-233">If hello journal file does exist, AzCopy checks whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="d2d15-234">Если две командные строки hello совпадают, AzCopy возобновляет hello незавершенные операции.</span><span class="sxs-lookup"><span data-stu-id="d2d15-234">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="d2d15-235">Если они не совпадают, AzCopy запрашивает пользователя tooeither перезаписать hello файла журнала toostart новую операцию или toocancel hello текущей операции.</span><span class="sxs-lookup"><span data-stu-id="d2d15-235">If they do not match, AzCopy prompts user tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="d2d15-236">Если необходимо использовать расположение по умолчанию hello toouse для файла журнала hello:</span><span class="sxs-lookup"><span data-stu-id="d2d15-236">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="d2d15-237">Если параметр опущен `--resume`, или задайте параметр `--resume` без hello путь к папке, как показано выше, AzCopy создает файл журнала hello в расположении по умолчанию hello, а именно `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="d2d15-237">If you omit option `--resume`, or specify option `--resume` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="d2d15-238">Если уже существует файл журнала hello AzCopy возобновляет hello операции на основе файла журнала hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-238">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="d2d15-239">Если нужно toospecify пользовательское расположение для файла журнала hello:</span><span class="sxs-lookup"><span data-stu-id="d2d15-239">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="d2d15-240">Этот пример создает файл журнала hello, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="d2d15-240">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="d2d15-241">Если он существует, AzCopy возобновляет hello операции на основе файла журнала hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-241">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="d2d15-242">Tooresume операции AzCopy повторите hello в одной команде.</span><span class="sxs-lookup"><span data-stu-id="d2d15-242">If you want tooresume an AzCopy operation, repeat hello same command.</span></span> <span data-ttu-id="d2d15-243">AzCopy для Linux запросит подтверждение.</span><span class="sxs-lookup"><span data-stu-id="d2d15-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="d2d15-244">Вывод подробных журналов</span><span class="sxs-lookup"><span data-stu-id="d2d15-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="d2d15-245">Укажите число hello toostart параллельных операций</span><span class="sxs-lookup"><span data-stu-id="d2d15-245">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="d2d15-246">Параметр `--parallel-level` указывает hello количество параллельных копирования операций.</span><span class="sxs-lookup"><span data-stu-id="d2d15-246">Option `--parallel-level` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="d2d15-247">По умолчанию AzCopy запускается определенное число передачи пропускная способность hello tooincrease параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="d2d15-247">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="d2d15-248">Hello число параллельных операций будет равно числу процессоров, у вас есть hello восемь раз.</span><span class="sxs-lookup"><span data-stu-id="d2d15-248">hello number of concurrent operations is equal eight times hello number of processors you have.</span></span> <span data-ttu-id="d2d15-249">При выполнении AzCopy в сети с низкой пропускной способностью, можно указать меньшее значение для--ошибка tooavoid параллельного уровень конкуренции ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d2d15-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level tooavoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="d2d15-250">Полный список tooview hello параметров AzCopy извлечь «azcopy — справки» меню.</span><span class="sxs-lookup"><span data-stu-id="d2d15-250">tooview hello complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="d2d15-251">Известные проблемы и рекомендации</span><span class="sxs-lookup"><span data-stu-id="d2d15-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-hello-system"></a><span data-ttu-id="d2d15-252">Ошибка: .NET Core не найден в системе hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-252">Error: .NET Core is not found in hello system.</span></span>
<span data-ttu-id="d2d15-253">Если возникнет сообщение о том, что .NET Core не установлен в системе hello hello путь toohello .NET двоичного файла `dotnet` могут отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="d2d15-253">If you encounter an error stating that .NET Core is not installed in hello system, hello PATH toohello .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="d2d15-254">В заказ tooaddress эту проблему, найдите hello .NET двоичного файла в системе hello:</span><span class="sxs-lookup"><span data-stu-id="d2d15-254">In order tooaddress this issue, find hello .NET Core binary in hello system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="d2d15-255">Hello путь toohello dotnet возвращает двоичные.</span><span class="sxs-lookup"><span data-stu-id="d2d15-255">This returns hello path toohello dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="d2d15-256">Теперь добавьте эту переменную пути toohello пути.</span><span class="sxs-lookup"><span data-stu-id="d2d15-256">Now add this path toohello PATH variable.</span></span> <span data-ttu-id="d2d15-257">Для вызова sudo изменение secure_path toocontain hello путь toohello dotnet двоичные:</span><span class="sxs-lookup"><span data-stu-id="d2d15-257">For sudo, edit secure_path toocontain hello path toohello dotnet binary:</span></span>
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

<span data-ttu-id="d2d15-258">В этом примере переменная secure_path имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="d2d15-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="d2d15-259">Для текущего пользователя hello измените.bash_profile/.profile tooinclude hello путь toohello dotnet в переменную PATH двоичные файлы</span><span class="sxs-lookup"><span data-stu-id="d2d15-259">For hello current user, edit .bash_profile/.profile tooinclude hello path toohello dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

<span data-ttu-id="d2d15-260">Убедитесь, что теперь компонент .NET Core указан в переменной PATH.</span><span class="sxs-lookup"><span data-stu-id="d2d15-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="d2d15-261">Ошибка при установке AzCopy</span><span class="sxs-lookup"><span data-stu-id="d2d15-261">Error Installing AzCopy</span></span>
<span data-ttu-id="d2d15-262">При возникновении проблем с установкой AzCopy, попробуйте извлечь с помощью скрипта bash hello в hello AzCopy toorun `azcopy` папки.</span><span class="sxs-lookup"><span data-stu-id="d2d15-262">If you encounter issues with AzCopy installation, you may try toorun AzCopy using hello bash script in hello extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="d2d15-263">Ограничение одновременных операций записи при копировании данных</span><span class="sxs-lookup"><span data-stu-id="d2d15-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="d2d15-264">При копировании больших двоичных объектов или файлов с помощью AzCopy, имейте в виду, возможно, изменение другое приложение hello данных при копировании его.</span><span class="sxs-lookup"><span data-stu-id="d2d15-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="d2d15-265">Если это возможно убедитесь, hello данных при копировании не изменяется во время операции копирования hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-265">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="d2d15-266">Например при копировании виртуальный жесткий ДИСК, связанный с виртуальной машины Azure, убедитесь, что нет других приложений в настоящее время пишете toohello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="d2d15-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="d2d15-267">Toodo хорошим способом это по аренде toobe ресурсов hello копируются.</span><span class="sxs-lookup"><span data-stu-id="d2d15-267">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="d2d15-268">Кроме того можно сначала создать моментальный снимок виртуального жесткого диска hello и скопируйте hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="d2d15-268">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="d2d15-269">Если не может помешать записи tooblobs или файлы, пока они копируются, то следует помнить, заданием hello hello время завершения работы других приложений, hello скопированных ресурсов может больше нет полной четности с ресурсами источника hello.</span><span class="sxs-lookup"><span data-stu-id="d2d15-269">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="d2d15-270">Запускайте один экземпляр AzCopy на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="d2d15-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="d2d15-271">AzCopy является использование hello спроектированный toomaximize скорость передачи данных ресурсов tooaccelerate машины hello, мы рекомендуем запустить только один экземпляр AzCopy на одном компьютере и укажите параметр hello `--parallel-level` при необходимости несколько параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="d2d15-271">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="d2d15-272">Для получения дополнительных сведений введите `AzCopy --help parallel-level` hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="d2d15-272">For more details, type `AzCopy --help parallel-level` at hello command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2d15-273">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2d15-273">Next steps</span></span>
<span data-ttu-id="d2d15-274">Дополнительные сведения о хранилище Azure и AzCopy см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="d2d15-274">For more information about Azure Storage and AzCopy, see hello following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="d2d15-275">Документация по хранилищу Azure:</span><span class="sxs-lookup"><span data-stu-id="d2d15-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="d2d15-276">Введение tooAzure хранилища</span><span class="sxs-lookup"><span data-stu-id="d2d15-276">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="d2d15-277">создать учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="d2d15-277">Create a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="d2d15-278">Управление ресурсами хранилища BLOB-объектов Azure с помощью обозревателя хранилищ (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d2d15-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="d2d15-279">С помощью hello Azure CLI 2.0 со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="d2d15-279">Using hello Azure CLI 2.0 with Azure Storage</span></span>](storage-azure-cli.md)
* [<span data-ttu-id="d2d15-280">Как toouse хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="d2d15-280">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="d2d15-281">Как toouse хранилища BLOB-объектов из Java</span><span class="sxs-lookup"><span data-stu-id="d2d15-281">How toouse Blob storage from Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="d2d15-282">Как toouse хранилища BLOB-объектов из Node.js</span><span class="sxs-lookup"><span data-stu-id="d2d15-282">How toouse Blob storage from Node.js</span></span>](storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="d2d15-283">Как toouse хранилища BLOB-объектов из Python</span><span class="sxs-lookup"><span data-stu-id="d2d15-283">How toouse Blob storage from Python</span></span>](storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="d2d15-284">Записи блога по хранилищу Azure:</span><span class="sxs-lookup"><span data-stu-id="d2d15-284">Azure Storage blog posts:</span></span>
* <span data-ttu-id="d2d15-285">[Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/) (Объявление о выпуске предварительной версии AzCopy для Linux)</span><span class="sxs-lookup"><span data-stu-id="d2d15-285">[Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)</span></span>
* [<span data-ttu-id="d2d15-286">Введение в предварительную версию библиотеки движения данных в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="d2d15-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="d2d15-287">AzCopy: введение в синхронное копирование и настраиваемый тип содержимого</span><span class="sxs-lookup"><span data-stu-id="d2d15-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="d2d15-288">AzCopy: выпуск общедоступной версии AzCopy 3.0 и предварительной версии AzCopy 4.0 с поддержкой таблиц и файлов</span><span class="sxs-lookup"><span data-stu-id="d2d15-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="d2d15-289">AzCopy: оптимизированные сценарии для крупномасштабного копирования</span><span class="sxs-lookup"><span data-stu-id="d2d15-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="d2d15-290">AzCopy: поддержка геоизбыточного хранилища для доступа с правом чтения</span><span class="sxs-lookup"><span data-stu-id="d2d15-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* <span data-ttu-id="d2d15-291">[AzCopy – Transfer data with re-startable mode and SAS Token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) (AzCopy: передача данных с использованием перезапускаемого режима и маркера SAS)</span><span class="sxs-lookup"><span data-stu-id="d2d15-291">[AzCopy: Transfer data with restartable mode and SAS token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)</span></span>
* [<span data-ttu-id="d2d15-292">AzCopy: использование копирования больших двоичных объектов между разными учетными записями</span><span class="sxs-lookup"><span data-stu-id="d2d15-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="d2d15-293">AzCopy: отправка и скачивание файлов для больших двоичных объектов Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d2d15-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

