---
title: "aaaHow toouse хранилища больших двоичных объектов Azure (объект хранилища) из Python | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>Как toouse хранилища больших двоичных объектов Azure с Python
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор
Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.

В этой статье будет показано, как tooperform распространенные сценарии использования хранилища больших двоичных объектов. Hello примеры написаны на Python и использовать hello [пакет SDK хранилища Microsoft Azure для Python]. Hello сценарии включают отправки, список, загрузка и удаление больших двоичных объектов.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>Создание контейнера
Исходя из большого двоичного объекта типа hello хотелось бы toouse, создайте **BlockBlobService**, **AppendBlobService**, или **PageBlobService** объекта. Hello следующий код использует **BlockBlobService** объекта. Добавьте следующее hello верхней hello любого файла Python, в котором вы хотите tooprogrammatically доступа Azure блочное хранилище больших двоичных объектов.

```python
from azure.storage.blob import BlockBlobService
```

Hello следующий код создает **BlockBlobService** объекта с помощью hello ключ учетной записи хранения имени и учетной записи.  Замените myaccount и mykey фактическими значениями имени и ключа учетной записи.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

В следующем примере кода hello, можно использовать **BlockBlobService** hello контейнера объекта toocreate, если он не существует.

```python
block_blob_service.create_container('mycontainer')
```

По умолчанию hello новый контейнер является закрытым, поэтому необходимо указать ключи доступа к хранилищу (как это было сделано ранее) toodownload большие двоичные объекты из этого контейнера. Следует toomake hello BLOB-объектов в доступных tooeveryone hello контейнера можно создать контейнер hello и передать hello уровень общего доступа, с помощью hello, следующий код.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

Кроме того можно изменить контейнер после создания его с помощью hello, следующий код.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

После этого изменения всем пользователям в Интернете hello можно увидеть в открытый контейнер BLOB-объектов, но только можно изменить или удалить их.

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
toocreate большого двоичного объекта и передачи данных, используйте hello **создания\_большого двоичного объекта\_из\_путь**, **создать\_большого двоичного объекта\_из\_поток**, **создания\_большого двоичного объекта\_из\_байт** или **создания\_большого двоичного объекта\_из\_текста** методы. Они являются высокого уровня методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.

**Создание\_большого двоичного объекта\_из\_путь** передач hello содержимое файла из указанного пути hello, и **создать\_больших двоичных объектов\_из\_поток** передачи hello содержимое из уже открытого файла или потока. **Создание\_большого двоичного объекта\_из\_байт** передает массив байтов, и **создания\_большого двоичного объекта\_из\_текст** передает указанный hello текстовое значение, с помощью hello указан кодирования (по умолчанию tooUTF-8).

Hello следующий пример отправляет содержимое hello hello **sunset.png** файла в hello **«myblob»** больших двоичных объектов.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
toolist hello BLOB-объектов в контейнере, используйте hello **списка\_большие двоичные объекты** метод. Этот метод возвращает генератор. Hello следующий код выводит hello **имя** каждого BLOB-объекта в контейнер toohello консоли.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Скачивание больших двоичных объектов
toodownload данные из большого двоичного объекта используйте **получить\_большого двоичного объекта\_для\_путь**, **получить\_большого двоичного объекта\_для\_поток**, **получить\_большого двоичного объекта\_для\_байт**, или **получить\_большого двоичного объекта\_для\_текст**. Они являются высокого уровня методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.

Hello следующий пример демонстрирует использование **получить\_большого двоичного объекта\_для\_путь** toodownload содержимое hello hello **«myblob»** больших двоичных объектов и их сохранения toohello **out sunset.png** файла.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Удаление большого двоичного объекта
Наконец, вызовите toodelete большой двоичный объект **delete_blob**.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>Написание tooan append больших двоичных объектов
Добавочный большой двоичный объект оптимизирован для операций добавления, например ведения журналов. Как большой двоичный объект блока добавочный BLOB-объект состоит из блоков, но при добавлении нового большого двоичного объекта tooan append блок, это всегда присоединенных toohello конец hello большого двоичного объекта. Вы не можете обновить или удалить существующий блок в добавочном большом двоичном объекте. Идентификаторы блокировок Hello для добавочный большой двоичный объект не отображаются, как и для большого двоичного объекта.

Каждый блок в добавочный большой двоичный объект может быть разный размер копии tooa более 4 Мбайт и добавочный большой двоичный объект может содержать не более 50 000 блоков. Максимальный размер Hello добавочный большой двоичный объект таким образом — немного более 195 ГБ (4 МБ X 50 000 блоков).

Hello приведенном ниже примере создается новый добавочный большой двоичный объект и добавляет tooit некоторых данных, имитируя операция простого ведения журнала.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища больших двоичных объектов, выполните следующие дополнительные toolearn ссылки.

* [Центр по разработке для Python](https://azure.microsoft.com/develop/python/)
* [API-интерфейс REST служб хранилища Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Блог рабочей группы службы хранилища Azure]
* [пакет SDK хранилища Microsoft Azure для Python]

[Блог рабочей группы службы хранилища Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[пакет SDK хранилища Microsoft Azure для Python]: https://github.com/Azure/azure-storage-python
