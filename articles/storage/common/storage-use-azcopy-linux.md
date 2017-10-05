---
title: "Копирование или перемещение данных в службу хранилища Azure с помощью AzCopy для Linux | Документация Майкрософт"
description: "Служебная программа AzCopy для Linux позволяет копировать и перемещать данные в BLOB-объект или файл и из него. Копируйте данные в хранилище Azure из локальных файлов, а также внутри учетной записи хранения и из одной такой учетной записи в другую. Легко переносите данные в хранилище Azure."
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
ms.openlocfilehash: 441227d84b9c1ec721ae36fdc423ba797654f128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a><span data-ttu-id="8256e-105">Перенос данных с помощью AzCopy для Linux</span><span class="sxs-lookup"><span data-stu-id="8256e-105">Transfer data with AzCopy on Linux</span></span>
<span data-ttu-id="8256e-106">AzCopy для Linux — это служебная программа командной строки. Она предназначена для копирования данных из хранилища BLOB-объектов и хранилища файлов Microsoft Azure (и обратно) с помощью простых команд, обеспечивающих оптимальную производительность.</span><span class="sxs-lookup"><span data-stu-id="8256e-106">AzCopy on Linux is a command-line utility designed for copying data to and from Microsoft Azure Blob and File storage using simple commands with optimal performance.</span></span> <span data-ttu-id="8256e-107">Кроме того, она позволяет копировать данные из одного объекта в другой в пределах одной учетной записи хранения или из одной такой записи в другую.</span><span class="sxs-lookup"><span data-stu-id="8256e-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="8256e-108">Существуют две версии AzCopy, которые можно скачать.</span><span class="sxs-lookup"><span data-stu-id="8256e-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="8256e-109">Служебная программа AzCopy для Linux основана на платформе .NET Core, которая нацелена на платформы Linux, использующие параметры командной строки в формате POSIX.</span><span class="sxs-lookup"><span data-stu-id="8256e-109">AzCopy on Linux is built with .NET Core Framework, which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="8256e-110">Служебная программа [AzCopy для Windows](../storage-use-azcopy.md) основана на платформе .NET Framework и использует параметры командной строки в формате Windows.</span><span class="sxs-lookup"><span data-stu-id="8256e-110">[AzCopy on Windows](../storage-use-azcopy.md) is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="8256e-111">В этой статье рассматривается AzCopy для Linux.</span><span class="sxs-lookup"><span data-stu-id="8256e-111">This article covers AzCopy on Linux.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="8256e-112">Скачивание и установка AzCopy</span><span class="sxs-lookup"><span data-stu-id="8256e-112">Download and install AzCopy</span></span>
### <a name="installation-on-linux"></a><span data-ttu-id="8256e-113">Установка в Linux</span><span class="sxs-lookup"><span data-stu-id="8256e-113">Installation on Linux</span></span>

<span data-ttu-id="8256e-114">Для работы AzCopy для Linux на платформе должен быть установлен компонент .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8256e-114">AzCopy on Linux requires .NET Core framework on the platform.</span></span> <span data-ttu-id="8256e-115">Ознакомьтесь с инструкциями по установке на странице [.NET Core](https://www.microsoft.com/net/core#linuxubuntu).</span><span class="sxs-lookup"><span data-stu-id="8256e-115">See the installation instructions on the [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) page.</span></span>

<span data-ttu-id="8256e-116">Для примера давайте установим .NET Core в Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="8256e-116">As an example, let's install .NET Core on Ubuntu 16.10.</span></span> <span data-ttu-id="8256e-117">Последняя версия руководства доступна на странице установки [.NET Core для Linux](https://www.microsoft.com/net/core#linuxubuntu).</span><span class="sxs-lookup"><span data-stu-id="8256e-117">For the latest installation guide, visit [.NET Core on Linux](https://www.microsoft.com/net/core#linuxubuntu) installation page.</span></span>


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

<span data-ttu-id="8256e-118">После установки .NET Core скачайте и установите AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8256e-118">Once you have installed .NET Core, download and install AzCopy.</span></span>

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

<span data-ttu-id="8256e-119">После установки AzCopy для Linux извлеченные файлы можно будет удалить.</span><span class="sxs-lookup"><span data-stu-id="8256e-119">You can remove the extracted files once AzCopy on Linux is installed.</span></span> <span data-ttu-id="8256e-120">Если у вас нет привилегий суперпользователя, AzCopy можно также выполнить с помощью сценария оболочки azcopy в извлеченной папке.</span><span class="sxs-lookup"><span data-stu-id="8256e-120">Alternatively if you do not have superuser privileges, you can also run AzCopy using the shell script 'azcopy' in the extracted folder.</span></span> 

### <a name="alternative-installation-on-ubuntu"></a><span data-ttu-id="8256e-121">Альтернативная установка в Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8256e-121">Alternative Installation on Ubuntu</span></span>

<span data-ttu-id="8256e-122">**Ubuntu 14.04**</span><span class="sxs-lookup"><span data-stu-id="8256e-122">**Ubuntu 14.04**</span></span>

<span data-ttu-id="8256e-123">Добавьте источник apt для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8256e-123">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="8256e-124">Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8256e-124">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="8256e-125">**Ubuntu 16.04**</span><span class="sxs-lookup"><span data-stu-id="8256e-125">**Ubuntu 16.04**</span></span>

<span data-ttu-id="8256e-126">Добавьте источник apt для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8256e-126">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="8256e-127">Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8256e-127">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

<span data-ttu-id="8256e-128">**Ubuntu 16.10**</span><span class="sxs-lookup"><span data-stu-id="8256e-128">**Ubuntu 16.10**</span></span>

<span data-ttu-id="8256e-129">Добавьте источник apt для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8256e-129">Add apt source for .Net Core:</span></span>

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

<span data-ttu-id="8256e-130">Добавьте источник apt для репозитория продуктов Linux от корпорации Майкрософт и установите AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8256e-130">Add apt source for Microsoft Linux product repository and install AzCopy:</span></span>

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

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="8256e-131">Написание первой команды AzCopy</span><span class="sxs-lookup"><span data-stu-id="8256e-131">Writing your first AzCopy command</span></span>
<span data-ttu-id="8256e-132">В командах AzCopy используется следующий базовый синтаксис:</span><span class="sxs-lookup"><span data-stu-id="8256e-132">The basic syntax for AzCopy commands is:</span></span>

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

<span data-ttu-id="8256e-133">В приведенных ниже примерах описаны разные сценарии копирования данных в большие двоичные объекты и файлы Microsoft Azure (и обратно).</span><span class="sxs-lookup"><span data-stu-id="8256e-133">The following examples demonstrate various scenarios for copying data to and from Microsoft Azure Blobs and Files.</span></span> <span data-ttu-id="8256e-134">Чтобы получить подробное объяснение параметров, используемых в каждом примере, воспользуйтесь меню `azcopy --help`.</span><span class="sxs-lookup"><span data-stu-id="8256e-134">Refer to the `azcopy --help` menu for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="8256e-135">Большой двоичный объект: скачивание</span><span class="sxs-lookup"><span data-stu-id="8256e-135">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="8256e-136">Скачивание одного большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="8256e-136">Download single blob</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8256e-137">Если папка `/mnt/myfiles` не существует, AzCopy создаст ее и скачает `abc.txt ` в эту новую папку.</span><span class="sxs-lookup"><span data-stu-id="8256e-137">If the folder `/mnt/myfiles` does not exist, AzCopy creates it and downloads `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="8256e-138">Скачивание большого двоичного объекта из дополнительного региона</span><span class="sxs-lookup"><span data-stu-id="8256e-138">Download single blob from secondary region</span></span>

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8256e-139">Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.</span><span class="sxs-lookup"><span data-stu-id="8256e-139">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="8256e-140">Скачивание всех больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="8256e-140">Download all blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="8256e-141">Предположим, что в указанном контейнере находятся следующие BLOB-объекты:</span><span class="sxs-lookup"><span data-stu-id="8256e-141">Assume the following blobs reside in the specified container:</span></span>  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

<span data-ttu-id="8256e-142">После скачивания в каталог `/mnt/myfiles` будут помещены следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="8256e-142">After the download operation, the directory `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

<span data-ttu-id="8256e-143">Если не задать параметр `--recursive`, большие двоичные объекты не будут скачаны.</span><span class="sxs-lookup"><span data-stu-id="8256e-143">If you do not specify option `--recursive`, no blob will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="8256e-144">Скачивание больших двоичных объектов с указанным префиксом</span><span class="sxs-lookup"><span data-stu-id="8256e-144">Download blobs with specified prefix</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

<span data-ttu-id="8256e-145">Предположим, что в указанном контейнере находятся следующие BLOB-объекты:</span><span class="sxs-lookup"><span data-stu-id="8256e-145">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="8256e-146">Будут скачаны все большие двоичные объекты, имя которых начинается с префикса `a`.</span><span class="sxs-lookup"><span data-stu-id="8256e-146">All blobs beginning with the prefix `a` are downloaded.</span></span>

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

<span data-ttu-id="8256e-147">После скачивания в папку `/mnt/myfiles` будут помещены следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="8256e-147">After the download operation, the folder `/mnt/myfiles` includes the following files:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

<span data-ttu-id="8256e-148">Префикс применяется к виртуальному каталогу, который формирует первую часть имени большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="8256e-148">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="8256e-149">В указанном выше примере виртуальный каталог не соответствует заданному префиксу, поэтому ни один большой двоичный объект не скачивается.</span><span class="sxs-lookup"><span data-stu-id="8256e-149">In the example shown above, the virtual directory does not match the specified prefix, so no blob is downloaded.</span></span> <span data-ttu-id="8256e-150">Кроме того, если не задан параметр `--recursive`, то AzCopy не скачивает большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="8256e-150">In addition, if the option `--recursive` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="8256e-151">Установка одинакового времени последнего изменения для экспортированных файлов и исходных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="8256e-151">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

<span data-ttu-id="8256e-152">Исключить большие двоичные объекты из операции скачивания вы можете также на основе времени их последнего изменения.</span><span class="sxs-lookup"><span data-stu-id="8256e-152">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="8256e-153">Например, если нужно исключить большие двоичные объекты, измененные в то же время, что и конечный файл, или позднее, добавьте параметр `--exclude-newer`:</span><span class="sxs-lookup"><span data-stu-id="8256e-153">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `--exclude-newer` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

<span data-ttu-id="8256e-154">А если нужно исключить большие двоичные объекты, измененные в то же время, что и конечный файл, или раньше, добавьте параметр `--exclude-older`:</span><span class="sxs-lookup"><span data-stu-id="8256e-154">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `--exclude-older` option:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a><span data-ttu-id="8256e-155">Большой двоичный объект: отправка</span><span class="sxs-lookup"><span data-stu-id="8256e-155">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="8256e-156">Отправка одного файла</span><span class="sxs-lookup"><span data-stu-id="8256e-156">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8256e-157">Если указанный контейнер назначения не существует, AzCopy создаст его и передаст в него файл.</span><span class="sxs-lookup"><span data-stu-id="8256e-157">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="8256e-158">Отправка одного файла в виртуальный каталог</span><span class="sxs-lookup"><span data-stu-id="8256e-158">Upload single file to virtual directory</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8256e-159">Если указанный виртуальный каталог не существует, AzCopy передаст файл и включит имя виртуального каталога в имя большого двоичного объекта (*например*, `vd/abc.txt` в указанном выше примере).</span><span class="sxs-lookup"><span data-stu-id="8256e-159">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in the blob name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="8256e-160">Отправка всех файлов</span><span class="sxs-lookup"><span data-stu-id="8256e-160">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="8256e-161">Выбор параметра `--recursive` обеспечивает рекурсивную передачу указанного каталога в хранилище BLOB-объектов. Это означает, что передаются также все вложенные папки и файлы.</span><span class="sxs-lookup"><span data-stu-id="8256e-161">Specifying option `--recursive` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="8256e-162">Например, предположим, что следующие файлы находятся в папке `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="8256e-162">For instance, assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="8256e-163">Когда передача завершится, в контейнер будут помещены следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="8256e-163">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="8256e-164">Если параметр `--recursive` не указать, будут переданы только следующие три файла:</span><span class="sxs-lookup"><span data-stu-id="8256e-164">When the option `--recursive` is not specified, only the following three files are uploaded:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="8256e-165">Отправка файлов, соответствующих указанному шаблону</span><span class="sxs-lookup"><span data-stu-id="8256e-165">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

<span data-ttu-id="8256e-166">Предположим, что следующие файлы размещены в папке `/mnt/myfiles`:</span><span class="sxs-lookup"><span data-stu-id="8256e-166">Assume the following files reside in folder `/mnt/myfiles`:</span></span>

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

<span data-ttu-id="8256e-167">Когда передача завершится, в контейнер будут помещены следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="8256e-167">After the upload operation, the container includes the following files:</span></span>

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

<span data-ttu-id="8256e-168">Если параметр `--recursive` не указан, AzCopy пропускает файлы, находящиеся во вложенных каталогах.</span><span class="sxs-lookup"><span data-stu-id="8256e-168">When the option `--recursive` is not specified, AzCopy skips files that are in sub-directories:</span></span>

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="8256e-169">Задание типа содержимого MIME целевого большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="8256e-169">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="8256e-170">По умолчанию AzCopy задает для типа содержимого целевого большого двоичного объекта значение `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="8256e-170">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="8256e-171">Однако вы можете явно задать тип содержимого с помощью параметра `--set-content-type [content-type]`.</span><span class="sxs-lookup"><span data-stu-id="8256e-171">However, you can explicitly specify the content type via the option `--set-content-type [content-type]`.</span></span> <span data-ttu-id="8256e-172">Этот синтаксис задает тип содержимого для всех больших двоичных объектов в операции отправки.</span><span class="sxs-lookup"><span data-stu-id="8256e-172">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

<span data-ttu-id="8256e-173">Если вы задали параметр `--set-content-type`, не указав значение, AzCopy задаст тип содержимого для каждого большого двоичного объекта или файла в соответствии с расширением файла.</span><span class="sxs-lookup"><span data-stu-id="8256e-173">If the option `--set-content-type` is specified without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a><span data-ttu-id="8256e-174">Большой двоичный объект: копирование</span><span class="sxs-lookup"><span data-stu-id="8256e-174">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="8256e-175">Копирование большого двоичного объекта в пределах учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="8256e-175">Copy single blob within Storage account</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8256e-176">При копировании большого двоичного объекта без параметра --sync-copy выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8256e-176">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="8256e-177">Копирование большого двоичного объекта между различными учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="8256e-177">Copy single blob across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="8256e-178">При копировании большого двоичного объекта без параметра --sync-copy выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8256e-178">When you copy a blob without --sync-copy option, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="8256e-179">Копирование одного большого двоичного объекта из дополнительного региона в основной регион</span><span class="sxs-lookup"><span data-stu-id="8256e-179">Copy single blob from secondary region to primary region</span></span>

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

<span data-ttu-id="8256e-180">Обратите внимание: должно быть включено геоизбыточное хранилище с доступом только для чтения.</span><span class="sxs-lookup"><span data-stu-id="8256e-180">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="8256e-181">Копирование большого двоичного объекта и его моментальных снимков между различными учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="8256e-181">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

<span data-ttu-id="8256e-182">После выполнения копирования целевой контейнер будет содержать большой двоичный объект и его моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="8256e-182">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="8256e-183">Контейнер будет содержать следующий большой двоичный объект и его моментальные снимки:</span><span class="sxs-lookup"><span data-stu-id="8256e-183">The container includes the following blob and its snapshots:</span></span>

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="8256e-184">Синхронное копирование больших двоичных объектов между учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="8256e-184">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="8256e-185">По умолчанию AzCopy выполняет асинхронное копирование данных между двумя конечными точками хранилища.</span><span class="sxs-lookup"><span data-stu-id="8256e-185">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="8256e-186">Следовательно, операция копирования выполняется в фоновом режиме, используя запасную пропускную способность, для которой не установлено соглашение об уровне обслуживания, регулирующее скорость, с которой копируется большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="8256e-186">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied.</span></span> 

<span data-ttu-id="8256e-187">Параметр `--sync-copy` обеспечивает постоянную скорость операции копирования.</span><span class="sxs-lookup"><span data-stu-id="8256e-187">The `--sync-copy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="8256e-188">AzCopy выполняет синхронное копирование, при котором большие двоичные объекты копируются из указанного источника в локальную память путем скачивания, а затем загружаются в целевое хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="8256e-188">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

<span data-ttu-id="8256e-189">Параметр `--sync-copy` может повлечь дополнительные затраты на исходящий трафик по сравнению с асинхронным копированием.</span><span class="sxs-lookup"><span data-stu-id="8256e-189">`--sync-copy` might generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="8256e-190">Во избежание таких затрат мы советуем использовать данный режим в виртуальных машинах Azure, которые находятся в одном регионе с вашей исходной учетной записью хранения.</span><span class="sxs-lookup"><span data-stu-id="8256e-190">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="8256e-191">Файл: скачивание</span><span class="sxs-lookup"><span data-stu-id="8256e-191">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="8256e-192">Скачивание одного файла</span><span class="sxs-lookup"><span data-stu-id="8256e-192">Download single file</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

<span data-ttu-id="8256e-193">Если исходный файл для копирования находится в общей папке Azure, необходимо указать либо точное имя файла (*например*, `abc.txt`) для копирования одного файла, либо параметр `--recursive` для рекурсивного копирования всех файлов в общей папке.</span><span class="sxs-lookup"><span data-stu-id="8256e-193">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `--recursive` to download all files in the share recursively.</span></span> <span data-ttu-id="8256e-194">Попытка одновременно задать шаблон файла и параметр `--recursive` приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="8256e-194">Attempting to specify both a file pattern and option `--recursive` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="8256e-195">Скачивание всех файлов</span><span class="sxs-lookup"><span data-stu-id="8256e-195">Download all files</span></span>

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

<span data-ttu-id="8256e-196">Обратите внимание на то, что пустые папки не скачиваются.</span><span class="sxs-lookup"><span data-stu-id="8256e-196">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="8256e-197">Файл: отправка</span><span class="sxs-lookup"><span data-stu-id="8256e-197">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="8256e-198">Отправка одного файла</span><span class="sxs-lookup"><span data-stu-id="8256e-198">Upload single file</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="8256e-199">Отправка всех файлов</span><span class="sxs-lookup"><span data-stu-id="8256e-199">Upload all files</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

<span data-ttu-id="8256e-200">Обратите внимание на то, что пустые папки не передаются.</span><span class="sxs-lookup"><span data-stu-id="8256e-200">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="8256e-201">Отправка файлов, соответствующих указанному шаблону</span><span class="sxs-lookup"><span data-stu-id="8256e-201">Upload files matching specified pattern</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a><span data-ttu-id="8256e-202">Файл: копирование</span><span class="sxs-lookup"><span data-stu-id="8256e-202">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="8256e-203">Копирование общих файловых ресурсов</span><span class="sxs-lookup"><span data-stu-id="8256e-203">Copy across file shares</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="8256e-204">При копировании файла между файловыми ресурсами выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8256e-204">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="8256e-205">Копирование из общего файлового ресурса в BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="8256e-205">Copy from file share to blob</span></span>

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="8256e-206">При копировании файла из файлового ресурса в большой двоичный объект выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8256e-206">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="8256e-207">Копирование из большого двоичного объекта в общий файловый ресурс</span><span class="sxs-lookup"><span data-stu-id="8256e-207">Copy from blob to file share</span></span>

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
<span data-ttu-id="8256e-208">При копировании файла из большого двоичного объекта в файловый ресурс выполняется [операция копирования на стороне сервера](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="8256e-208">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="8256e-209">Синхронное копирование файлов</span><span class="sxs-lookup"><span data-stu-id="8256e-209">Synchronously copy files</span></span>
<span data-ttu-id="8256e-210">Вы можете указать параметр `--sync-copy` для синхронного копирования данных из хранилища файлов в хранилище файлов, из хранилища файлов в хранилище BLOB-объектов, а также из хранилища BLOB-объектов в хранилище файлов.</span><span class="sxs-lookup"><span data-stu-id="8256e-210">You can specify the `--sync-copy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously.</span></span> <span data-ttu-id="8256e-211">AzCopy выполняет эту операцию, скачивая исходные данные в локальную память и передавая их в место назначения.</span><span class="sxs-lookup"><span data-stu-id="8256e-211">AzCopy runs this operation by downloading the source data to local memory, and then uploading it to destination.</span></span> <span data-ttu-id="8256e-212">В этом случае взимается стандартная плата за исходящий трафик.</span><span class="sxs-lookup"><span data-stu-id="8256e-212">In this case, standard egress cost applies.</span></span>

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

<span data-ttu-id="8256e-213">При копировании из хранилища файлов в хранилище BLOB-объектов пользователь может указать параметр `/BlobType:page` для изменения типа большого двоичного объекта назначения.</span><span class="sxs-lookup"><span data-stu-id="8256e-213">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="8256e-214">Обратите внимание на то, что параметр `--sync-copy` может повлечь дополнительные затраты на исходящий трафик по сравнению с асинхронным копированием.</span><span class="sxs-lookup"><span data-stu-id="8256e-214">Note that `--sync-copy` might generate additional egress cost comparing to asynchronous copy.</span></span> <span data-ttu-id="8256e-215">Во избежание таких затрат мы советуем использовать данный режим в виртуальных машинах Azure, которые находятся в одном регионе с вашей исходной учетной записью хранения.</span><span class="sxs-lookup"><span data-stu-id="8256e-215">The recommended approach is to use this option in an Azure VM, that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="other-azcopy-features"></a><span data-ttu-id="8256e-216">Другие функции AzCopy</span><span class="sxs-lookup"><span data-stu-id="8256e-216">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="8256e-217">Копирование только тех данных, которых нет в целевой папке</span><span class="sxs-lookup"><span data-stu-id="8256e-217">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="8256e-218">Предотвратить копирование старого или нового ресурса позволяют параметры `--exclude-older` и `--exclude-newer` соответственно.</span><span class="sxs-lookup"><span data-stu-id="8256e-218">The `--exclude-older` and `--exclude-newer` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="8256e-219">Если нужно скопировать только те исходные ресурсы, которых нет в целевой папке, в команде AzCopy вы можете указать оба параметра:</span><span class="sxs-lookup"><span data-stu-id="8256e-219">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-to-specify-command-line-parameters"></a><span data-ttu-id="8256e-220">Использование файла конфигурации для задания параметров командной строки</span><span class="sxs-lookup"><span data-stu-id="8256e-220">Use a configuration file to specify command-line parameters</span></span>

```azcopy
azcopy --config-file "azcopy-config.ini"
```

<span data-ttu-id="8256e-221">В файл конфигурации можно добавить параметры командной строки AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8256e-221">You can include any AzCopy command-line parameters in a configuration file.</span></span> <span data-ttu-id="8256e-222">AzCopy обрабатывает параметры в файле, как если бы он были заданы в командной строке, выполняя прямую замену содержимого файла.</span><span class="sxs-lookup"><span data-stu-id="8256e-222">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="8256e-223">Предположим, у нас имеется файл конфигурации `copyoperation`, содержащий приведенные ниже строки.</span><span class="sxs-lookup"><span data-stu-id="8256e-223">Assume a configuration file named `copyoperation`, that contains the following lines.</span></span> <span data-ttu-id="8256e-224">Каждый параметр AzCopy можно указать как в одной строке,</span><span class="sxs-lookup"><span data-stu-id="8256e-224">Each AzCopy parameter can be specified on a single line.</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

<span data-ttu-id="8256e-225">так и в разных:</span><span class="sxs-lookup"><span data-stu-id="8256e-225">or on separate lines:</span></span>

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

<span data-ttu-id="8256e-226">При выполнении AzCopy возникнет ошибка, если разделить параметр на две строки, как показано ниже на примере параметра `--source-key`.</span><span class="sxs-lookup"><span data-stu-id="8256e-226">AzCopy fails if you split the parameter across two lines, as shown here for the `--source-key` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="8256e-227">Указание подписи общего доступа (SAS)</span><span class="sxs-lookup"><span data-stu-id="8256e-227">Specify a shared access signature (SAS)</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

<span data-ttu-id="8256e-228">Кроме того, вы можете указать SAS в коде URI контейнера:</span><span class="sxs-lookup"><span data-stu-id="8256e-228">You can also specify a SAS on the container URI:</span></span>

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

<span data-ttu-id="8256e-229">Обратите внимание на то, что в настоящее время AzCopy поддерживает только [подписанный URL-адрес учетной записи](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="8256e-229">Note that AzCopy currently only supports the [Account SAS](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

### <a name="journal-file-folder"></a><span data-ttu-id="8256e-230">Папка файлов журнала</span><span class="sxs-lookup"><span data-stu-id="8256e-230">Journal file folder</span></span>
<span data-ttu-id="8256e-231">При каждом вводе команды для AzCopy выполняется проверка на наличие файла журнала в папке по умолчанию или в папке, которая была задана с помощью данного параметра.</span><span class="sxs-lookup"><span data-stu-id="8256e-231">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="8256e-232">Если в обоих местах файл журнала отсутствует, AzCopy воспринимает операцию как новую и создает новый файл журнала.</span><span class="sxs-lookup"><span data-stu-id="8256e-232">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="8256e-233">Если файл журнала существует, AzCopy проверяет, соответствует ли введенная командная строка командной строке в файле журнала.</span><span class="sxs-lookup"><span data-stu-id="8256e-233">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="8256e-234">Если две командные строки совпадают, AzCopy возобновляет незавершенную операцию.</span><span class="sxs-lookup"><span data-stu-id="8256e-234">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="8256e-235">Если они не совпадают, AzCopy предложит пользователю либо перезаписать файл журнала, чтобы начать новую операцию, либо отменить текущую операцию.</span><span class="sxs-lookup"><span data-stu-id="8256e-235">If they do not match, AzCopy prompts user to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="8256e-236">Использование расположения по умолчанию для файла журнала.</span><span class="sxs-lookup"><span data-stu-id="8256e-236">If you want to use the default location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

<span data-ttu-id="8256e-237">Если опустить параметр`--resume` или задать параметр `--resume` без пути папки, как указано выше, AzCopy создает файл журнала в расположении по умолчанию: `~\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="8256e-237">If you omit option `--resume`, or specify option `--resume` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `~\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="8256e-238">Если файл журнала уже существует, то AzCopy возобновляет операцию на основе файла журнала.</span><span class="sxs-lookup"><span data-stu-id="8256e-238">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="8256e-239">Использование настраиваемого расположения для файла журнала.</span><span class="sxs-lookup"><span data-stu-id="8256e-239">If you want to specify a custom location for the journal file:</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

<span data-ttu-id="8256e-240">В этом примере создается файл журнала, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="8256e-240">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="8256e-241">Если такой файл существует, то AzCopy возобновляет операцию на основе файла журнала.</span><span class="sxs-lookup"><span data-stu-id="8256e-241">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="8256e-242">Если вы хотите возобновить операцию AzCopy, повторите ту же самую команду.</span><span class="sxs-lookup"><span data-stu-id="8256e-242">If you want to resume an AzCopy operation, repeat the same command.</span></span> <span data-ttu-id="8256e-243">AzCopy для Linux запросит подтверждение.</span><span class="sxs-lookup"><span data-stu-id="8256e-243">AzCopy on Linux then will prompt for confirmation:</span></span>

```azcopy
Incomplete operation with same command line detected at the journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want to resume the operation? Choose Yes to resume, choose No to overwrite the journal to start a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a><span data-ttu-id="8256e-244">Вывод подробных журналов</span><span class="sxs-lookup"><span data-stu-id="8256e-244">Output verbose logs</span></span>

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="8256e-245">Задание количества одновременных операций для запуска</span><span class="sxs-lookup"><span data-stu-id="8256e-245">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="8256e-246">Параметр `--parallel-level` задает количество одновременных операций копирования.</span><span class="sxs-lookup"><span data-stu-id="8256e-246">Option `--parallel-level` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="8256e-247">По умолчанию AzCopy запускает несколько одновременных операций для увеличения скорости передачи данных.</span><span class="sxs-lookup"><span data-stu-id="8256e-247">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="8256e-248">Количество одновременных операций равно восьмикратному количеству процессоров в вашем распоряжении.</span><span class="sxs-lookup"><span data-stu-id="8256e-248">The number of concurrent operations is equal eight times the number of processors you have.</span></span> <span data-ttu-id="8256e-249">При выполнении AzCopy в сети с низкой пропускной способностью можно задать меньшее значение для параметра --parallel-level, чтобы избежать сбоев, вызванных соревнованием за ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8256e-249">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for --parallel-level to avoid failure caused by resource competition.</span></span>

[!TIP]
><span data-ttu-id="8256e-250">Чтобы просмотреть полный список параметров AzCopy, ознакомьтесь с меню azcopy --help.</span><span class="sxs-lookup"><span data-stu-id="8256e-250">To view the complete list of AzCopy parameters, check out 'azcopy --help' menu.</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="8256e-251">Известные проблемы и рекомендации</span><span class="sxs-lookup"><span data-stu-id="8256e-251">Known issues and best practices</span></span>
### <a name="error-net-core-is-not-found-in-the-system"></a><span data-ttu-id="8256e-252">Ошибка: компонент .NET Core не найден в системе.</span><span class="sxs-lookup"><span data-stu-id="8256e-252">Error: .NET Core is not found in the system.</span></span>
<span data-ttu-id="8256e-253">Если отображается сообщение об ошибке, в котором говорится, что в системе не установлен компонент .NET Core, возможно, отсутствует переменная PATH, указывающая путь к двоичному файлу `dotnet` .NET Core.</span><span class="sxs-lookup"><span data-stu-id="8256e-253">If you encounter an error stating that .NET Core is not installed in the system, the PATH to the .NET Core binary `dotnet` may be missing.</span></span>

<span data-ttu-id="8256e-254">Чтобы устранить эту проблему, найдите данный двоичный файл .NET Core в системе.</span><span class="sxs-lookup"><span data-stu-id="8256e-254">In order to address this issue, find the .NET Core binary in the system:</span></span>
```bash
sudo find / -name dotnet
```

<span data-ttu-id="8256e-255">Эта команда возвращает путь к двоичному файлу dotnet.</span><span class="sxs-lookup"><span data-stu-id="8256e-255">This returns the path to the dotnet binary.</span></span> 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

<span data-ttu-id="8256e-256">Теперь добавьте этот путь в переменную PATH.</span><span class="sxs-lookup"><span data-stu-id="8256e-256">Now add this path to the PATH variable.</span></span> <span data-ttu-id="8256e-257">В случае использования sudo измените secure_path, добавив путь к двоичному файлу dotnet.</span><span class="sxs-lookup"><span data-stu-id="8256e-257">For sudo, edit secure_path to contain the path to the dotnet binary:</span></span>
```bash 
sudo visudo
### Append the path found in the preceding example to 'secure_path' variable
```

<span data-ttu-id="8256e-258">В этом примере переменная secure_path имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="8256e-258">In this example, secure_path variable reads as:</span></span>

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

<span data-ttu-id="8256e-259">Измените .bash_profile/.profile для текущего пользователя, добавив путь к двоичному файлу dotnet в переменную PATH.</span><span class="sxs-lookup"><span data-stu-id="8256e-259">For the current user, edit .bash_profile/.profile to include the path to the dotnet binary in PATH variable</span></span> 
```bash
vi ~/.bash_profile
### Append the path found in the preceding example to 'PATH' variable
```

<span data-ttu-id="8256e-260">Убедитесь, что теперь компонент .NET Core указан в переменной PATH.</span><span class="sxs-lookup"><span data-stu-id="8256e-260">Verify that .NET Core is now in PATH:</span></span>
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a><span data-ttu-id="8256e-261">Ошибка при установке AzCopy</span><span class="sxs-lookup"><span data-stu-id="8256e-261">Error Installing AzCopy</span></span>
<span data-ttu-id="8256e-262">В случае возникновения проблем при установке AzCopy можно попытаться запустить AzCopy с помощью сценария bash в извлеченной папке `azcopy`.</span><span class="sxs-lookup"><span data-stu-id="8256e-262">If you encounter issues with AzCopy installation, you may try to run AzCopy using the bash script in the extracted `azcopy` folder.</span></span>

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="8256e-263">Ограничение одновременных операций записи при копировании данных</span><span class="sxs-lookup"><span data-stu-id="8256e-263">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="8256e-264">При копировании BLOB-объектов или файлов с помощью AzCopy следует иметь в виду, что другое приложение может изменять данные в то время, когда они копируются.</span><span class="sxs-lookup"><span data-stu-id="8256e-264">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="8256e-265">Если это возможно, обеспечьте, чтобы во время операции копирования не происходило изменение копируемых данных.</span><span class="sxs-lookup"><span data-stu-id="8256e-265">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="8256e-266">Например, при копировании VHD, связанного с виртуальной машиной Azure, убедитесь в том, что никакое другое приложение в это время не записывает данные на VHD.</span><span class="sxs-lookup"><span data-stu-id="8256e-266">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="8256e-267">Для этого рекомендуется сдать ресурс, который нужно скопировать, в аренду.</span><span class="sxs-lookup"><span data-stu-id="8256e-267">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="8256e-268">В качестве альтернативы можно сначала создать моментальный снимок VHD, а затем скопировать его.</span><span class="sxs-lookup"><span data-stu-id="8256e-268">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="8256e-269">Если не удается предотвратить запись в BLOB-объекты или файлы во время их копирования со стороны других приложений, следует иметь в виду, что к моменту завершения задания скопированные ресурсы могут больше не иметь полного соответствия с исходными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="8256e-269">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="8256e-270">Запускайте один экземпляр AzCopy на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="8256e-270">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="8256e-271">AzCopy предназначен для максимального использования ресурсов компьютера для ускорения передачи данных. Рекомендуется запускать только один экземпляр AzCopy на одном компьютере и указать параметр `--parallel-level`, если требуется несколько параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="8256e-271">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `--parallel-level` if you need more concurrent operations.</span></span> <span data-ttu-id="8256e-272">Для получения более подробной информации введите в командной строке `AzCopy --help parallel-level` .</span><span class="sxs-lookup"><span data-stu-id="8256e-272">For more details, type `AzCopy --help parallel-level` at the command line.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8256e-273">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8256e-273">Next steps</span></span>
<span data-ttu-id="8256e-274">Для получения дополнительной информации о службе хранилища Azure и AzCopy ознакомьтесь со следующими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="8256e-274">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="8256e-275">Документация по хранилищу Azure:</span><span class="sxs-lookup"><span data-stu-id="8256e-275">Azure Storage documentation:</span></span>
* [<span data-ttu-id="8256e-276">Введение в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="8256e-276">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="8256e-277">создать учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="8256e-277">Create a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="8256e-278">Управление ресурсами хранилища BLOB-объектов Azure с помощью обозревателя хранилищ (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="8256e-278">Manage blobs with Storage Explorer</span></span>](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [<span data-ttu-id="8256e-279">Использование Azure CLI 2.0 со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="8256e-279">Using the Azure CLI 2.0 with Azure Storage</span></span>](../storage-azure-cli.md)
* [<span data-ttu-id="8256e-280">Использование хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="8256e-280">How to use Blob storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="8256e-281">Использование хранилища BLOB-объектов из Java</span><span class="sxs-lookup"><span data-stu-id="8256e-281">How to use Blob storage from Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="8256e-282">Использование хранилища больших двоичных объектов из Node.js</span><span class="sxs-lookup"><span data-stu-id="8256e-282">How to use Blob storage from Node.js</span></span>](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="8256e-283">Использование хранилища больших двоичных объектов из Python</span><span class="sxs-lookup"><span data-stu-id="8256e-283">How to use Blob storage from Python</span></span>](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="8256e-284">Записи блога по хранилищу Azure:</span><span class="sxs-lookup"><span data-stu-id="8256e-284">Azure Storage blog posts:</span></span>
* <span data-ttu-id="8256e-285">[Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/) (Объявление о выпуске предварительной версии AzCopy для Linux)</span><span class="sxs-lookup"><span data-stu-id="8256e-285">[Announcing AzCopy on Linux Preview](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)</span></span>
* [<span data-ttu-id="8256e-286">Введение в предварительную версию библиотеки движения данных в хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="8256e-286">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="8256e-287">AzCopy: введение в синхронное копирование и настраиваемый тип содержимого</span><span class="sxs-lookup"><span data-stu-id="8256e-287">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="8256e-288">AzCopy: выпуск общедоступной версии AzCopy 3.0 и предварительной версии AzCopy 4.0 с поддержкой таблиц и файлов</span><span class="sxs-lookup"><span data-stu-id="8256e-288">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="8256e-289">AzCopy: оптимизированные сценарии для крупномасштабного копирования</span><span class="sxs-lookup"><span data-stu-id="8256e-289">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="8256e-290">AzCopy: поддержка геоизбыточного хранилища для доступа с правом чтения</span><span class="sxs-lookup"><span data-stu-id="8256e-290">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* <span data-ttu-id="8256e-291">[AzCopy – Transfer data with re-startable mode and SAS Token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx) (AzCopy: передача данных с использованием перезапускаемого режима и маркера SAS)</span><span class="sxs-lookup"><span data-stu-id="8256e-291">[AzCopy: Transfer data with restartable mode and SAS token](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)</span></span>
* [<span data-ttu-id="8256e-292">AzCopy: использование копирования больших двоичных объектов между разными учетными записями</span><span class="sxs-lookup"><span data-stu-id="8256e-292">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="8256e-293">AzCopy: отправка и скачивание файлов для больших двоичных объектов Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8256e-293">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

