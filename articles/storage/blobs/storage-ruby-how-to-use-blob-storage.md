---
title: "aaaHow toouse хранилища больших двоичных объектов (объект хранилища) из Ruby | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="34925-103">Как toouse хранилища BLOB-объектов из Ruby</span><span class="sxs-lookup"><span data-stu-id="34925-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="34925-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="34925-104">Overview</span></span>
<span data-ttu-id="34925-105">Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты.</span><span class="sxs-lookup"><span data-stu-id="34925-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="34925-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="34925-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="34925-107">Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="34925-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="34925-108">В этом руководстве будет показано, как tooperform распространенные сценарии использования хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="34925-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="34925-109">образцы Hello записываются с помощью Ruby API hello.</span><span class="sxs-lookup"><span data-stu-id="34925-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="34925-110">Hello сценарии включают **отправку, перечисление, загрузку** и **удаление** больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="34925-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="34925-111">Создание приложения Ruby</span><span class="sxs-lookup"><span data-stu-id="34925-111">Create a Ruby application</span></span>
<span data-ttu-id="34925-112">Создайте приложение Ruby.</span><span class="sxs-lookup"><span data-stu-id="34925-112">Create a Ruby application.</span></span> <span data-ttu-id="34925-113">Инструкции см. в статье [Веб-приложение Ruby on Rails на виртуальной машине Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="34925-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="34925-114">Настройка вашего приложения tooaccess хранилища</span><span class="sxs-lookup"><span data-stu-id="34925-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="34925-115">toouse хранилища Azure, понадобится toodownload и используйте hello Ruby azure пакет, который включает в себя набор библиотек удобства, взаимодействующих со службами REST hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="34925-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="34925-116">Используйте RubyGems tooobtain hello пакет</span><span class="sxs-lookup"><span data-stu-id="34925-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="34925-117">Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="34925-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="34925-118">Введите команду «gem Установка azure» в hello команда окна tooinstall hello gem и зависимости.</span><span class="sxs-lookup"><span data-stu-id="34925-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="34925-119">Импорт пакета hello</span><span class="sxs-lookup"><span data-stu-id="34925-119">Import hello package</span></span>
<span data-ttu-id="34925-120">С помощью предпочитаемого текстового редактора, добавьте следующие toohello вверху hello Ruby файл, куда будет toouse хранилища hello:</span><span class="sxs-lookup"><span data-stu-id="34925-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="34925-121">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="34925-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="34925-122">модуль Hello azure будет считывать переменные среды hello **AZURE\_ХРАНЕНИЯ\_учетной записи** и **AZURE\_ХРАНЕНИЯ\_ключ_доступа** для сведения, необходимые учетной записи хранилища Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="34925-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="34925-123">Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello перед использованием **Azure::Blob::BlobService** с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="34925-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="34925-124">tooobtain эти значения из классические или диспетчер ресурсов хранилища учетной записи в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="34925-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="34925-125">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="34925-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="34925-126">Перейдите toohello необходимом toouse учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="34925-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="34925-127">В колонке параметров hello на hello вправо, щелкните **клавиши доступа**.</span><span class="sxs-lookup"><span data-stu-id="34925-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="34925-128">В колонке ключи hello доступа, отображается вы увидите ключ доступа hello 1 и ключ доступа 2.</span><span class="sxs-lookup"><span data-stu-id="34925-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="34925-129">Можно использовать любой из них.</span><span class="sxs-lookup"><span data-stu-id="34925-129">You can use either of these.</span></span>
5. <span data-ttu-id="34925-130">Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="34925-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="34925-131">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="34925-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="34925-132">Hello **Azure::Blob::BlobService** объектов позволяет работать с контейнерами и BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="34925-132">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="34925-133">toocreate является контейнером, используйте hello **создания\_container()** метод.</span><span class="sxs-lookup"><span data-stu-id="34925-133">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="34925-134">Hello следующий пример кода создает контейнер или выводит hello ошибки, если оно назначено.</span><span class="sxs-lookup"><span data-stu-id="34925-134">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="34925-135">Если нужно toomake hello файлы в контейнере hello открытый, можно назначить разрешения контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="34925-135">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="34925-136">Можно просто изменить hello <strong>создания\_container()</strong> hello вызовов toopass **: открытого\_доступа\_уровень** параметр:</span><span class="sxs-lookup"><span data-stu-id="34925-136">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="34925-137">Допустимые значения для hello **: открытого\_доступа\_уровень** , параметр:</span><span class="sxs-lookup"><span data-stu-id="34925-137">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="34925-138">**blob** — это общий доступ на чтение для больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="34925-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="34925-139">Данные BLOB-объектов в этом контейнере можно считать с помощью анонимного запроса, но данные контейнера недоступны.</span><span class="sxs-lookup"><span data-stu-id="34925-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="34925-140">Клиенты не могут перечислять большие двоичные объекты в контейнере hello через анонимный запрос.</span><span class="sxs-lookup"><span data-stu-id="34925-140">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="34925-141">**container** — это полный общий доступ на чтение данных контейнера и большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="34925-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="34925-142">Клиенты могут перечислять большие двоичные объекты в контейнере hello через анонимный запрос, но не могут перечислять контейнеры в учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="34925-142">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="34925-143">Кроме того, можно изменить уровень общего доступа hello контейнера с помощью **задать\_контейнера\_acl()** уровень общего доступа метод toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="34925-143">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="34925-144">Здравствуйте, следующий пример кода, изменения слишком hello уровень общего доступа**контейнера**:</span><span class="sxs-lookup"><span data-stu-id="34925-144">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="34925-145">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="34925-145">Upload a blob into a container</span></span>
<span data-ttu-id="34925-146">tooupload tooa содержимого большого двоичного объекта, используйте hello **создания\_блок\_blob()** метод toocreate hello большого двоичного объекта, используйте файл или строка как hello содержимое большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="34925-146">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="34925-147">Hello следующий код отправляет hello файл **test.png** как новый большой двоичный объект с именем «-BLOB-объекта изображения» в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="34925-147">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="34925-148">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="34925-148">List hello blobs in a container</span></span>
<span data-ttu-id="34925-149">Используйте контейнеры hello toolist, **list_containers()** метод.</span><span class="sxs-lookup"><span data-stu-id="34925-149">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="34925-150">использовать toolist hello BLOB-объектов в контейнере, **списка\_blobs()** метод.</span><span class="sxs-lookup"><span data-stu-id="34925-150">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="34925-151">При этом происходит вывод hello URL-адреса всех больших двоичных объектов hello во всех контейнерах hello hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="34925-151">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="34925-152">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="34925-152">Download blobs</span></span>
<span data-ttu-id="34925-153">toodownload больших двоичных объектов, использовать hello **получить\_blob()** метод tooretrieve hello содержимое.</span><span class="sxs-lookup"><span data-stu-id="34925-153">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="34925-154">Hello следующем примере кода показано использование **получить\_blob()** toodownload содержимое «— BLOB-объект образа» Привет и записать их в локальный файл tooa.</span><span class="sxs-lookup"><span data-stu-id="34925-154">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="34925-155">Удаление BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="34925-155">Delete a Blob</span></span>
<span data-ttu-id="34925-156">Наконец, toodelete большого двоичного объекта используйте hello **удаление\_blob()** метод.</span><span class="sxs-lookup"><span data-stu-id="34925-156">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="34925-157">Hello следующем примере кода показано, как toodelete большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="34925-157">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="34925-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="34925-158">Next steps</span></span>
<span data-ttu-id="34925-159">toolearn о более сложных задач хранилища, приведены по следующим ссылкам:</span><span class="sxs-lookup"><span data-stu-id="34925-159">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="34925-160">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="34925-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="34925-161">[пакетов SDK Azure для Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) на веб-сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="34925-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="34925-162">Перенесите данные с помощью служебной программы командной строки AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="34925-162">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

