---
title: "Использование хранилища BLOB-объектов (хранилища объектов) из Ruby | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
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
ms.openlocfilehash: 7f7d0c52b2b50a360711477e8e0eafc07ddcf374
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="aebee-103">Использование хранилища BLOB-объектов из Ruby</span><span class="sxs-lookup"><span data-stu-id="aebee-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="aebee-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="aebee-104">Overview</span></span>
<span data-ttu-id="aebee-105">Хранилище BLOB-объектов Azure — это служба, которая хранит неструктурированные данные в облаке в качестве объектов или больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="aebee-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="aebee-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="aebee-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="aebee-107">Хранилище BLOB-объектов иногда также называют хранилищем объектов.</span><span class="sxs-lookup"><span data-stu-id="aebee-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="aebee-108">В этом руководстве показано, как реализовать типичные сценарии с использованием хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="aebee-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="aebee-109">Примеры написаны с помощью Ruby API.</span><span class="sxs-lookup"><span data-stu-id="aebee-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="aebee-110">Здесь описаны такие сценарии, как **отправка, перечисление, скачивание** и **удаление** BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="aebee-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="aebee-111">Создание приложения Ruby</span><span class="sxs-lookup"><span data-stu-id="aebee-111">Create a Ruby application</span></span>
<span data-ttu-id="aebee-112">Создайте приложение Ruby.</span><span class="sxs-lookup"><span data-stu-id="aebee-112">Create a Ruby application.</span></span> <span data-ttu-id="aebee-113">Инструкции см. в статье [Веб-приложение Ruby on Rails на виртуальной машине Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="aebee-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="aebee-114">Настройка приложения для доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="aebee-114">Configure your application to access Storage</span></span>
<span data-ttu-id="aebee-115">Для использования хранилища Azure необходимо загрузить и использовать пакет Ruby Azure, который содержит набор библиотек, взаимодействующих со службами REST хранилища.</span><span class="sxs-lookup"><span data-stu-id="aebee-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="aebee-116">Использование RubyGems для получения пакета</span><span class="sxs-lookup"><span data-stu-id="aebee-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="aebee-117">Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="aebee-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="aebee-118">Введите "gem install azure" в окне командной строки, чтобы установить пакеты и зависимости.</span><span class="sxs-lookup"><span data-stu-id="aebee-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="aebee-119">Импорт пакета</span><span class="sxs-lookup"><span data-stu-id="aebee-119">Import the package</span></span>
<span data-ttu-id="aebee-120">Используйте свой любимый текстовый редактор, чтобы добавить следующий код в начало файла Ruby, где планируется использовать хранилище.</span><span class="sxs-lookup"><span data-stu-id="aebee-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="aebee-121">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="aebee-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="aebee-122">Модуль Azure считывает переменные среды **AZURE\_STORAGE\_ACCOUNT** и **AZURE\_STORAGE\_ACCESS_KEY**, чтобы получить информацию, необходимую для подключения к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="aebee-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="aebee-123">Если эти переменные среды не заданы, необходимо указать сведения об учетной записи перед использованием **Azure::Blob::BlobService** с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="aebee-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="aebee-124">Вот как можно получить эти значения из классический учетной записи хранения или учетной записи хранения Resource Manager на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="aebee-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="aebee-125">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aebee-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aebee-126">Перейдите к учетной записи хранения, которая будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="aebee-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="aebee-127">В колонке "Параметры" справа щелкните **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="aebee-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="aebee-128">В колонке "Ключи доступа" вы увидите ключи доступа 1 и 2.</span><span class="sxs-lookup"><span data-stu-id="aebee-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="aebee-129">Можно использовать любой из них.</span><span class="sxs-lookup"><span data-stu-id="aebee-129">You can use either of these.</span></span>
5. <span data-ttu-id="aebee-130">Щелкните значок копирования, чтобы скопировать ключ в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="aebee-130">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="aebee-131">Вот как можно получить эти значения из классический учетной записи хранения на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="aebee-131">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="aebee-132">Войдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="aebee-132">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="aebee-133">Перейдите к учетной записи хранения, которая будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="aebee-133">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="aebee-134">Щелкните **УПРАВЛЕНИЕ КЛЮЧАМИ ДОСТУПА** в нижней части области навигации.</span><span class="sxs-lookup"><span data-stu-id="aebee-134">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="aebee-135">Во всплывающем диалоговом окне вы увидите имя учетной записи хранения, первичный ключ доступа и вторичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="aebee-135">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="aebee-136">В качестве ключа доступа можно использовать либо первичный, либо вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="aebee-136">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="aebee-137">Щелкните значок копирования, чтобы скопировать ключ в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="aebee-137">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="aebee-138">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="aebee-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="aebee-139">Объект **Azure::Blob::BlobService** позволяет работать с контейнерами и BLOB-объектами.</span><span class="sxs-lookup"><span data-stu-id="aebee-139">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="aebee-140">Чтобы создать контейнер, используйте метод **create\_container()**.</span><span class="sxs-lookup"><span data-stu-id="aebee-140">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="aebee-141">В следующем примере кода создается контейнер или выводится ошибка, если она возникла.</span><span class="sxs-lookup"><span data-stu-id="aebee-141">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="aebee-142">Если вы хотите сделать файлы в контейнере общедоступными, можно установить разрешения контейнера.</span><span class="sxs-lookup"><span data-stu-id="aebee-142">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="aebee-143">Вы можете просто изменить вызов <strong>create\_container()</strong> и передать параметр **:public\_access\_level**:</span><span class="sxs-lookup"><span data-stu-id="aebee-143">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="aebee-144">Параметр **:public\_access\_level** принимает такие значения:</span><span class="sxs-lookup"><span data-stu-id="aebee-144">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="aebee-145">**blob** — это общий доступ на чтение для больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="aebee-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="aebee-146">Данные BLOB-объектов в этом контейнере можно считать с помощью анонимного запроса, но данные контейнера недоступны.</span><span class="sxs-lookup"><span data-stu-id="aebee-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="aebee-147">Клиенты не могут перечислять BLOB-объекты внутри с помощью анонимного запроса.</span><span class="sxs-lookup"><span data-stu-id="aebee-147">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="aebee-148">**container** — это полный общий доступ на чтение данных контейнера и большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="aebee-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="aebee-149">Клиенты могут перечислять BLOB-объекты внутри контейнера с помощью анонимного запроса, но не могут перечислять контейнеры в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="aebee-149">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="aebee-150">Кроме того, можно изменить уровень общего доступа к контейнеру, определив уровень общего доступа в методе **set\_container\_acl()**.</span><span class="sxs-lookup"><span data-stu-id="aebee-150">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="aebee-151">В следующем примере кода уровень общего доступа изменяется на **container**:</span><span class="sxs-lookup"><span data-stu-id="aebee-151">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="aebee-152">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="aebee-152">Upload a blob into a container</span></span>
<span data-ttu-id="aebee-153">Чтобы передать содержимое в BLOB-объект, создайте этот объект с помощью метода **create\_block\_blob()**, а в качестве содержимого объекта используйте файл или строку.</span><span class="sxs-lookup"><span data-stu-id="aebee-153">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="aebee-154">Следующий код отправляет файл **test.png** как новый большой двоичный объект с именем "image-blob" в контейнер.</span><span class="sxs-lookup"><span data-stu-id="aebee-154">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="aebee-155">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="aebee-155">List the blobs in a container</span></span>
<span data-ttu-id="aebee-156">Для перечисления контейнеров используйте метод **list_containers()**.</span><span class="sxs-lookup"><span data-stu-id="aebee-156">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="aebee-157">Для перечисления BLOB-объектов в контейнере используйте метод **list\_blobs()**.</span><span class="sxs-lookup"><span data-stu-id="aebee-157">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="aebee-158">Этот пример выводит URL-адреса всех BLOB-объектов во всех контейнерах учетной записи.</span><span class="sxs-lookup"><span data-stu-id="aebee-158">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="aebee-159">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="aebee-159">Download blobs</span></span>
<span data-ttu-id="aebee-160">Для скачивания BLOB-объектов (получения их содержимого) используйте метод **get\_blob()**.</span><span class="sxs-lookup"><span data-stu-id="aebee-160">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="aebee-161">В следующем примере кода показано, как с помощью метода **get\_blob()** скачать содержимое объекта image-blob и записать его в локальный файл.</span><span class="sxs-lookup"><span data-stu-id="aebee-161">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="aebee-162">Удаление BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="aebee-162">Delete a Blob</span></span>
<span data-ttu-id="aebee-163">Для удаления BLOB-объекта используйте метод **delete\_blob()**.</span><span class="sxs-lookup"><span data-stu-id="aebee-163">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="aebee-164">В следующем примере кода показано, как удалить большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="aebee-164">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="aebee-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aebee-165">Next steps</span></span>
<span data-ttu-id="aebee-166">Дополнительную информацию о выполнении более сложных задач хранения см. по указанным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="aebee-166">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="aebee-167">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="aebee-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="aebee-168">[пакетов SDK Azure для Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) на веб-сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="aebee-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="aebee-169">Приступая к работе со служебной программой командной строки AzCopy</span><span class="sxs-lookup"><span data-stu-id="aebee-169">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

