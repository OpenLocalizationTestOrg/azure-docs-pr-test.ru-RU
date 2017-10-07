---
title: "aaaUsing hello Azure 1.0 CLI со службой хранилища Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure командной строки (CLI Azure) 1.0 с toocreate хранилища Azure и управление учетными записями хранения и работы с файлами и больших двоичных объектов Azure. Hello Azure CLI — это средство кросс платформенных"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>С помощью Azure CLI 1.0 hello со службой хранилища Azure

## <a name="overview"></a>Обзор

Hello Azure CLI предоставляет набор с открытым исходным кодом кросс платформенных команды для работы с hello платформы Azure. Она предоставляет большую часть hello же функциональные возможности, найденные в hello [портал Azure](https://portal.azure.com) также как сложных данных, доступ к функциям.

В этом руководстве мы изучим как toouse [интерфейса командной строки Azure (Azure CLI)](../../cli-install-nodejs.md) tooperform различных задач разработки и администрирования хранилища Azure. Рекомендуется загрузить и установить или обновить toohello последнюю Azure CLI перед использованием в этом руководстве.

В этом руководстве предполагается, что вы понимаете основные понятия hello хранилища Azure. Hello руководство содержит ряд сценариев использования hello toodemonstrate hello Azure CLI со службой хранилища Azure. Быть убедиться, что tooupdate hello переменные сценария, на основе конфигурации перед выполнением каждого скрипта.

> [!NOTE]
> руководство по Hello примеры hello Azure CLI команд и скриптов для классические учетные записи хранения. В разделе [использование hello Azure CLI для Mac, Linux и Windows с помощью управления ресурсами Azure](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) для команды Azure CLI для учетных записей хранения Resource Manager.
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>Приступая к работе с хранилищем Azure и hello Azure CLI в 5 минут
В этом руководстве для демонстрации примеров используется ОС Ubuntu, но другие платформы должны работать аналогично.

**Новый tooAzure:** получить подписку Microsoft Azure и учетной записи Майкрософт, связанные с этой подпиской. Сведения о способах приобретения Azure см. на страницах [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/), [Как приобрести Azure](https://azure.microsoft.com/pricing/purchase-options/) и [Предложения для участников](https://azure.microsoft.com/pricing/member-offers/) (для подписчиков MSDN, участников Microsoft Partner Network, BizSpark и других наших программ).

Дополнительные сведения о подписках Azure см. на странице [Назначение ролей администратора в Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx).

**После создания подписки Microsoft Azure и учетной записи:**

1. Загрузите и установите Azure CLI, следуя инструкциям hello появлялся hello [Install hello Azure CLI](../../cli-install-nodejs.md).
2. После hello Azure CLI установлено, вы сможете может toouse hello azure команда из команды Azure CLI hello tooaccess интерфейс командной строки (Bash, терминалов, Командная строка). Тип hello _azure_ команда и вы увидите hello следующие выходные данные.

    ![Вывод команды Azure](./media/storage-azure-cli/azure_command.png)   
3. Hello интерфейса командной строки, введите `azure storage` toolist все hello команд хранилища azure и получить первое впечатление hello функции hello предоставляет Azure CLI. Можно ввести имя команды с **-h** параметра (например, `azure storage share create -h`) toosee подробные сведения о синтаксисе команды.
4. Теперь мы указываем, простой сценарий, который показывает основные tooaccess команды Azure CLI хранилища Azure. сценарий Hello сначала запросит tooset две переменные для учетной записи хранилища и ключа. Затем сценарий hello создать контейнер в этой новой учетной записи хранения и отправить существующий контейнер toothat образ файла (blob). После hello скрипт перечисляет все большие двоичные объекты в этом контейнере, он будет загружен hello образ файла toohello целевой каталог, существующего на локальном компьютере hello.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. Откройте любой текстовый редактор на локальном компьютере (например, Vim) Тип hello выше скрипт в текстовый редактор.
6. Теперь требуется переменных сценария hello tooupdate на основании параметров конфигурации.

   * **< Storage_account_name >** использовать hello с заданным именем в скрипте hello, или введите новое имя для вашей учетной записи. **Важно:** hello имя учетной записи хранения hello должно быть уникальным в Azure. и состоять из символов нижнего регистра.
   * **< storage_account_key >** hello ключ доступа учетной записи.
   * **< Container_name >** использовать hello с заданным именем в скрипте hello, или введите новое имя для контейнера.
   * **< Image_to_upload >** введите рисунок tooa путь на локальном компьютере, например: «~ / images/HelloWorld.png».
   * **< Destination_folder >** файлы toostore путь локального каталога tooa загружаются из хранилища Azure, такие как ввод: «~/downloadImages».
7. После обновления hello необходимые переменные в vim, нажмите клавишу сочетания клавиш `ESC`, `:`, `wq!` toosave hello скрипта.
8. toorun этот скрипт просто типа hello имя файла скрипта в консоли bash hello. После запуска этого сценария должно быть локальную целевую папку, которая содержит файл изображения загружаются hello. Следующий снимок экрана приветствия показан пример выходных данных:

После запуска сценария hello должно быть локальную целевую папку, которая содержит файл изображения загружаются hello.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Управление учетными записями хранения с hello Azure CLI
### <a name="connect-tooyour-azure-subscription"></a>Подключение tooyour подписки Azure
Большинство команд hello хранилища будет работать без подписки Azure, но рекомендуется tooconnect tooyour подписки из hello Azure CLI. tooconfigure hello Azure CLI toowork с подпиской, следуйте указаниям hello [подключение tooan подписки Azure из hello Azure CLI](../../xplat-cli-connect.md).

### <a name="create-a-new-storage-account"></a>Создание новой учетной записи хранения
toouse хранилища Azure, потребуется учетная запись хранения. После настройки подписки tooyour tooconnect компьютера, можно создать новую учетную запись хранилища Azure.

```azurecli
azure storage account create <account_name>
```

Hello имя учетной записи должно быть от 3 до 24 символов и содержать только строчные буквы и цифры.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>Установите учетную запись хранения Azure по умолчанию в переменных среды
В подписке может иметься несколько учетных записей хранения. Можно выбрать один из них и задать его в hello переменные среды для всех хранилищ hello команд hello же сеанса. Это позволяет toorun хранилища Azure CLI hello команды без указания hello хранилища учетной записи и ключа явным образом.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Другой способ tooset учетной записи хранения по умолчанию использует строку подключения. Во-первых, получите строку подключения hello командой:

```azurecli
azure storage account connectionstring show <account_name>
```

Затем скопируйте строку подключения для вывода hello и задать для него tooenvironment переменной:

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Создание больших двоичных объектов (BLOB-объектов) и управление ими
Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, например текстовых или двоичных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS. В этом разделе предполагается, что вы уже знакомы с основными понятиями хранилища больших двоичных объектов Azure hello. Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="create-a-container"></a>Создание контейнера
Каждый BLOB-объект в хранилище Azure должен находиться в контейнере. Можно создать закрытый контейнер с помощью hello `azure storage container create` команды:

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> Существует три уровня анонимного доступа для чтения: **Отключено**, **Большой двоичный объект** и **Контейнер**. tooprevent анонимный доступ к tooblobs параметр разрешения hello набора слишком**Off**. По умолчанию hello новый контейнер является закрытым и может осуществляться только владельцем учетной записи hello. анонимные открытый tooallow чтения tooblob доступ к ресурсам, но не toocontainer метаданные или toohello список больших двоичных объектов в контейнере hello, параметру hello разрешение слишком**большого двоичного объекта**. полный открытый tooallow чтения tooblob доступ к ресурсам, метаданные контейнера и hello список больших двоичных объектов в контейнере hello, задайте параметр разрешение hello слишком**контейнер**. Дополнительные сведения см. в разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](../blobs/storage-manage-access-to-resources.md).
>
>

### <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты. Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).

tooupload большие двоичные объекты в контейнере tooa, можно использовать hello `azure storage blob upload`. По умолчанию эта команда передает hello локальные файлы tooa блочного большого двоичного объекта. Тип hello toospecify для hello большого двоичного объекта, вы можете использовать hello `--blobtype` параметра.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>Загрузка BLOB-объектов из контейнера
Привет, в следующем примере показано, как toodownload большие двоичные объекты из контейнера.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>Копирование BLOB-объектов
Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями или внутри них.

Hello ниже приведен пример tooanother учетной записи toocopy больших двоичных объектов из одного места хранения. В этом примере мы создаем контейнер с общим анонимным доступом к BLOB-объектам.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

В этом примере выполняется асинхронное копирование. Можно отслеживать состояние hello каждой операции копирования, запустив hello `azure storage blob copy show` операции.

Обратите внимание, что hello исходный URL-адрес, указанный для операции копирования hello должен быть общедоступным или включать токен SAS (подпись общего доступа).

### <a name="delete-a-blob"></a>Удаление большого двоичного объекта
toodelete большого двоичного объекта используйте hello ниже команду:

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>Создание общих папок и управление ими
Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью стандартного протокола SMB hello. Виртуальные машины Microsoft Azure и облачные службы, а также локальные приложения, могут совместно использовать данные через монтированные ресурсы. Вы можете управлять файловыми ресурсами и файл данных с помощью hello Azure CLI. Дополнительные сведения о хранилище файлов Azure см. в разделе [приступить к работе с хранилищем Windows Azure файл](../storage-dotnet-how-to-use-files.md) или [как toouse хранилища Azure File с Linux](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Создайте общую папку
Общая папка Azure представляет собой общую папку с файлами SMB в Azure. Все каталоги и файлы должны быть созданы в общей папке. Учетная запись может содержать неограниченное количество общих ресурсов и общую папку можно сохранить неограниченное количество файлов копирование ограничения емкости toohello hello учетной записи хранилища. Hello следующий пример создает общую папку с именем **myshare**.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>Создайте каталог
Каталог обеспечивает дополнительную иерархическую структуру для общей папки Azure. Hello следующий пример создает каталог с именем **myDir** в общей папке hello.

```azurecli
azure storage directory create myshare myDir
```

Обратите внимание, что путь к каталогу может включать несколько уровней, *например***a/b**. Однако необходимо убедиться в наличии всех родительских каталогов. Например, для пути **a/b** вам потребуется сначала создать каталог **a**, а затем — каталог **b**.

### <a name="upload-a-local-file-toodirectory"></a>Отправка toodirectory локального файла
Hello следующий пример отправляет файл из **~/temp/samplefile.txt** toohello **myDir** каталога. Измените путь к файлу hello, которое указывает допустимый файл tooa на локальном компьютере.

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

Обратите внимание, что может быть файл в общей папке hello вверх too1 ТБ.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Список файлов hello в корневой папке hello или каталога
Можно перечислить hello файлов и подкаталогов в корневой общей папки или каталога, используя hello следующую команду:

```azurecli
azure storage file list myshare myDir
```

Обратите внимание, что имя каталога, hello является необязательным для операции перечисления hello. Если не указано, команда hello перечисляет содержимое hello hello корневой каталог общего ресурса hello.

### <a name="copy-files"></a>Копирование файлов
Начиная с версии 0.9.8 Azure CLI, можно скопировать файл tooanother, большой двоичный объект файла tooa или tooa файла большого двоичного объекта. Ниже показано как tooperform их копирования операции с помощью команды CLI. toocopy новый каталог toohello файла:

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

toocopy tooa файла большого двоичного объекта каталога:

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>Дальнейшие действия

Справочник по командам Azure CLI 1.0 для работы с ресурсами службы хранилища можно найти здесь:

* [Команды Azure CLI в режиме Resource Manager](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Установка Azure CLI](../../cli-install-nodejs.md)

Хотелось tootry hello [Azure CLI 2.0](../storage-azure-cli.md), нашей CLI следующего поколения, написанные на Python, для использования в модели развертывания диспетчера ресурсов hello.
