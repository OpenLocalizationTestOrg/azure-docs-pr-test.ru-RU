---
title: "Разработка для хранилища файлов Azure с помощью Python | Документация Майкрософт"
description: "Узнайте, как разрабатывать приложения и службы Python, использующие хранилище файлов Azure для хранения данных файлов."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: a1a37266908277b54e7b42d85b9b4873af77e622
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Разработка для хранилища файлов Azure с помощью Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>О данном учебнике
В этом руководстве мы рассмотрим основы использования Python для разработки приложений и служб, использующих хранилище файлов Azure для хранения данных файлов. В рамках этого руководства мы создадим простое консольное приложение, а также покажем, как выполнять базовые действия с Python и хранилищем файлов Azure:

* создание файловых ресурсов Azure;
* создание каталогов;
* перечисление файлов и каталогов в файловом ресурсе Azure;
* передача, загрузка и удаление файла.

> [!Note]  
> Так как доступ к хранилищу файлов Azure можно получить с помощью SMB, можно написать простые приложения, которые получают доступ к файловому ресурсу Azure, используя стандартные классы и функции Python для ввода-вывода. Из этой статьи вы узнаете, как создавать приложения, использующие пакет SDK Python для службы хранилища Azure, который использует [REST API хранилища файлов Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) для взаимодействия с этим хранилищем.

### <a name="set-up-your-application-to-use-azure-file-storage"></a>Настройка приложения для работы с хранилищем файлов Azure
Добавьте следующий код в начало любого исходного файла Python, из которого планируется получать доступ к хранилищу Azure программным способом:

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a>Настройка подключения к хранилищу файлов Azure 
Объект `FileService` позволяет работать с общими ресурсами, каталогами и файлами. Следующий код создает объект `FileService`, используя имя и ключ учетной записи хранения. Замените `<myaccount>` и `<mykey>` именем учетной записи и ключом.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Создание файлового ресурса Azure
В следующем примере кода для создания общего ресурса (если он не существует) можно использовать объект `FileService`.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Создайте каталог
Вы также можете организовать хранилище, помещая файлы в подкаталоги вместо их размещения в корневом каталоге. Хранилище файлов Azure позволяет создать столько каталогов, сколько может позволить ваша учетная запись. В следующем примере кода в корневом каталоге создается вложенный каталог с именем **sampledir** .

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Перечисление файлов и каталогов в файловом ресурсе Azure
Чтобы получить список файлов и каталогов в общем ресурсе, используйте метод **list\_directories\_and\_files**. Этот метод возвращает генератор. Приведенный далее код выводит в консоль **имя** каждого файла и каталога в общем ресурсе.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Отправить файл. 
Файловый ресурс Azure содержит по крайней мере корневой каталог, где могут размещаться файлы. В этом разделе вы узнаете, как отправить файл из локального хранилища в корневой каталог общего ресурса.

Для создания файла и передачи данных используйте методы `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` или `create_file_from_text`. Это высокоуровневые методы, которые выполняют необходимое фрагментирование данных, если их размер превышает 64 МБ.

Метод `create_file_from_path` передает содержимое файла из указанного пути, а метод `create_file_from_stream` передает содержимое уже открытого файла или потока. Метод `create_file_from_bytes` передает массив байтов, а `create_file_from_text` — указанное текстовое значение с использованием указанной кодировки (по умолчанию UTF-8).

В примере далее содержимое файла **sunset.png** передается в файл **myfile**.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Скачивание файла
Чтобы загрузить данные из файла, используйте методы `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes` или `get_file_to_text`. Это высокоуровневые методы, которые выполняют необходимое фрагментирование данных, если их размер превышает 64 МБ.

В следующем примере показано использование метода `get_file_to_path` для загрузки содержимого файла **myfile** и его сохранения в файл **out-sunset.png**.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Удаление файла
Наконец, чтобы удалить файл, вызовите метод `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали о работе с хранилищем файлов Azure с помощью Python, воспользуйтесь следующими ссылками для изучения дополнительных сведений.

* [Центр по разработке для Python](/develop/python/)
* [API-интерфейс REST служб хранилища Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [пакет SDK для службы хранилища Microsoft Azure для Python](https://github.com/Azure/azure-storage-python)