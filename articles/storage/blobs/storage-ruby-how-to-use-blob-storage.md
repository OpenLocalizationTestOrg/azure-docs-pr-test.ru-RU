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
# <a name="how-toouse-blob-storage-from-ruby"></a>Как toouse хранилища BLOB-объектов из Ruby
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор
Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.

В этом руководстве будет показано, как tooperform распространенные сценарии использования хранилища больших двоичных объектов. образцы Hello записываются с помощью Ruby API hello. Hello сценарии включают **отправку, перечисление, загрузку** и **удаление** больших двоичных объектов.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Создание приложения Ruby
Создайте приложение Ruby. Инструкции см. в статье [Веб-приложение Ruby on Rails на виртуальной машине Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Настройка вашего приложения tooaccess хранилища
toouse хранилища Azure, понадобится toodownload и используйте hello Ruby azure пакет, который включает в себя набор библиотек удобства, взаимодействующих со службами REST hello хранилища.

### <a name="use-rubygems-tooobtain-hello-package"></a>Используйте RubyGems tooobtain hello пакет
1. Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).
2. Введите команду «gem Установка azure» в hello команда окна tooinstall hello gem и зависимости.

### <a name="import-hello-package"></a>Импорт пакета hello
С помощью предпочитаемого текстового редактора, добавьте следующие toohello вверху hello Ruby файл, куда будет toouse хранилища hello:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
модуль Hello azure будет считывать переменные среды hello **AZURE\_ХРАНЕНИЯ\_учетной записи** и **AZURE\_ХРАНЕНИЯ\_ключ_доступа** для сведения, необходимые учетной записи хранилища Azure tooyour tooconnect. Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello перед использованием **Azure::Blob::BlobService** с hello, следующий код:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain эти значения из классические или диспетчер ресурсов хранилища учетной записи в hello портала Azure:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Перейдите toohello необходимом toouse учетной записи хранилища.
3. В колонке параметров hello на hello вправо, щелкните **клавиши доступа**.
4. В колонке ключи hello доступа, отображается вы увидите ключ доступа hello 1 и ключ доступа 2. Можно использовать любой из них.
5. Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена.

## <a name="create-a-container"></a>Создание контейнера
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Hello **Azure::Blob::BlobService** объектов позволяет работать с контейнерами и BLOB-объектов. toocreate является контейнером, используйте hello **создания\_container()** метод.

Hello следующий пример кода создает контейнер или выводит hello ошибки, если оно назначено.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Если нужно toomake hello файлы в контейнере hello открытый, можно назначить разрешения контейнера hello.

Можно просто изменить hello <strong>создания\_container()</strong> hello вызовов toopass **: открытого\_доступа\_уровень** параметр:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Допустимые значения для hello **: открытого\_доступа\_уровень** , параметр:

* **blob** — это общий доступ на чтение для больших двоичных объектов. Данные BLOB-объектов в этом контейнере можно считать с помощью анонимного запроса, но данные контейнера недоступны. Клиенты не могут перечислять большие двоичные объекты в контейнере hello через анонимный запрос.
* **container** — это полный общий доступ на чтение данных контейнера и большого двоичного объекта. Клиенты могут перечислять большие двоичные объекты в контейнере hello через анонимный запрос, но не могут перечислять контейнеры в учетной записи хранилища hello.

Кроме того, можно изменить уровень общего доступа hello контейнера с помощью **задать\_контейнера\_acl()** уровень общего доступа метод toospecify hello.

Здравствуйте, следующий пример кода, изменения слишком hello уровень общего доступа**контейнера**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
tooupload tooa содержимого большого двоичного объекта, используйте hello **создания\_блок\_blob()** метод toocreate hello большого двоичного объекта, используйте файл или строка как hello содержимое большого двоичного объекта hello.

Hello следующий код отправляет hello файл **test.png** как новый большой двоичный объект с именем «-BLOB-объекта изображения» в контейнере hello.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
Используйте контейнеры hello toolist, **list_containers()** метод.
использовать toolist hello BLOB-объектов в контейнере, **списка\_blobs()** метод.

При этом происходит вывод hello URL-адреса всех больших двоичных объектов hello во всех контейнерах hello hello учетной записи.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Скачивание больших двоичных объектов
toodownload больших двоичных объектов, использовать hello **получить\_blob()** метод tooretrieve hello содержимое.

Hello следующем примере кода показано использование **получить\_blob()** toodownload содержимое «— BLOB-объект образа» Привет и записать их в локальный файл tooa.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Удаление BLOB-объекта
Наконец, toodelete большого двоичного объекта используйте hello **удаление\_blob()** метод. Hello следующем примере кода показано, как toodelete большого двоичного объекта.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Дальнейшие действия
toolearn о более сложных задач хранилища, приведены по следующим ссылкам:

* [Блог рабочей группы службы хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [пакетов SDK Azure для Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) на веб-сайте GitHub
* [Перенесите данные с помощью служебной программы командной строки AzCopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

