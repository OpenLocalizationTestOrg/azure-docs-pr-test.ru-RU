---
title: "aaaDevelop для хранилища Azure File с Python | Документы Microsoft"
description: "Узнайте, как данные файлов toodevelop Python приложений и служб, использующих toostore хранилище файлов Azure."
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
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Разработка для хранилища файлов Azure с помощью Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>О данном учебнике
Этот учебник продемонстрируют hello основы работы с Python toodevelop приложений или служб, которые используют данные файла toostore хранилище файлов Azure. В этом учебнике мы создайте простое консольное приложение и Показать как tooperform базовые действия с хранилищем, Python и файлов Azure:

* создание файловых ресурсов Azure;
* создание каталогов;
* перечисление файлов и каталогов в файловом ресурсе Azure;
* Передача, загрузка и удаление файлов.

> [!Note]  
> Поскольку хранилище файлов Azure может осуществляться по протоколу SMB, вполне возможно toowrite простых приложений, получающих доступ к папке файлов Azure hello, с помощью стандартных классов ввода-вывода Python hello и функции. В этой статье описывается, как toowrite приложения, использующие hello SDK Python хранилища Azure, которая использует hello [хранилища Azure File API-интерфейса REST](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure хранилища файлов.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Настройка вашего приложения toouse хранилища Azure File
Добавьте следующее hello вверху hello любой Python исходный файл, в котором вы хотите tooprogrammatically доступа хранилища Azure.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Настройка подключения tooAzure хранения файлов 
Hello `FileService` объекта позволяет работать с общие папки, каталоги и файлы. Hello следующий код создает `FileService` объекта с помощью hello ключ учетной записи хранения имени и учетной записи. Замените `<myaccount>` и `<mykey>` именем учетной записи и ключом.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Создание файлового ресурса Azure
В следующем примере кода hello, можно использовать `FileService` объекта toocreate hello папки, если он не существует.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Создайте каталог
Кроме того, можно организовать хранилища путем помещения файлов в подкаталоги вместо их все в корневом каталоге hello. Хранилище файлов Azure позволяет toocreate как количество каталогов в вашей учетной записи будет разрешено. Приведенный ниже код Hello будет создавать вложенный каталог с именем **sampledir** в корневом каталоге hello.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Перечисление файлов и каталогов в файловом ресурсе Azure
toolist hello файлы и каталоги в общей папке, используйте hello **списка\_каталогов\_и\_файлы** метод. Этот метод возвращает генератор. Hello следующий код выводит hello **имя** всех файлов и каталогов в консоли toohello общей папки.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Отправить файл. 
Общая папка содержит очень бы в hello Azure файл, корневой каталог, где находятся файлы, можно. В этом разделе вы узнаете, как tooupload файла из локального хранилища на hello корневой каталог общего ресурса.

файл toocreate и передачи данных, используйте hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` или `create_file_from_text` методы. Они являются высокого уровня методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.

`create_file_from_path`передачи hello содержимое файла из указанного пути hello, и `create_file_from_stream` передачи hello содержимое из уже открытого файла или потока. `create_file_from_bytes`передает массив байтов, и `create_file_from_text` передачи hello указан с помощью hello текстовое значение кодировки (по умолчанию tooUTF-8).

Hello следующий пример отправляет содержимое hello hello **sunset.png** файла в hello **myfile** файла.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Скачивание файла
toodownload данных из файла, используйте `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, или `get_file_to_text`. Они являются высокого уровня методы, выполняющие hello необходимые фрагментации hello размер данных hello превышает 64 МБ.

Hello следующий пример демонстрирует использование `get_file_to_path` toodownload содержимое hello hello **myfile** файл и сохранить его toohello **out sunset.png** файла.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Удаление файла
Наконец, вызовите toodelete файл `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали, как toomanipulate хранилища Azure File с Python, выполните следующие дополнительные toolearn ссылки.

* [Центр по разработке для Python](/develop/python/)
* [API-интерфейс REST служб хранилища Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [пакет SDK для службы хранилища Microsoft Azure для Python](https://github.com/Azure/azure-storage-python)