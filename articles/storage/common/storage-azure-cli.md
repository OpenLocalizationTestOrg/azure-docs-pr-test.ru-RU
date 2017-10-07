---
title: "aaaUsing hello Azure CLI 2.0 со службой хранилища Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure командной строки (CLI Azure) 2.0 с toocreate хранилища Azure и управление учетными записями хранения и работы с файлами и больших двоичных объектов Azure. Hello Azure CLI 2.0 — это средство кросс платформенных, написанных на Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>С помощью hello Azure CLI 2.0 со службой хранилища Azure

Hello открытый исходный код, кросс платформенных Azure CLI 2.0 предоставляет набор команд для работы с hello платформы Azure. Она предоставляет большую часть hello же функциональные возможности, найденные в hello [портал Azure](https://portal.azure.com), включая доступ сложных данных.

В этом руководстве вы узнаете toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform несколько задач, работы с ресурсами в вашей учетной записи хранилища Azure. Рекомендуется загрузить и установить или обновление toohello последнюю версию CLI 2.0 hello ранее с помощью этого руководства.

Примеры Hello в руководстве hello предполагается использование hello hello оболочке Bash на Ubuntu, но другие платформы должен выполнять аналогичным образом. 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Предварительные требования
В этом руководстве предполагается, что вы понимаете основные понятия hello хранилища Azure. Также предполагается, что вы будете требования к создания может toosatisfy hello учетной записи, указанные ниже для Azure и hello службы хранилища.

### <a name="accounts"></a>Учетные записи
* **Учетная запись Azure.** Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/).
* **Учетная запись хранения**. См. раздел [Создание учетной записи хранения](storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](storage-create-storage-account.md).

### <a name="install-hello-azure-cli-20"></a>Установка hello Azure CLI 2.0

Загрузите и установите hello Azure CLI 2.0, следуя указаниям hello в [установить CLI Azure 2.0](/cli/azure/install-az-cli2).

> [!TIP]
> Если возникли проблемы с установкой hello, извлечь hello [Устранение неполадок установки](/cli/azure/install-az-cli2#installation-troubleshooting) раздел статьи hello и hello [Устранение неполадок установки](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) руководство по на сайте GitHub.
>

## <a name="working-with-hello-cli"></a>Работа с hello CLI

После установки hello CLI можно использовать hello `az` в командах Azure CLI hello tooaccess интерфейс командной строки (Bash, терминалов, командной строки). Тип hello `az` toosee команда полный список базовых команд hello (был усечен hello следующий пример выходных данных):

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

В интерфейсе командной строки, выполните команду hello `az storage --help` toolist hello `storage` команды подгруппы. описания Hello подгрупп hello содержит краткую приветствия функции hello Azure CLI предоставляет для работы с ресурсами хранилища.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Подключение tooyour CLI hello подписки Azure

toowork с ресурсами hello в вашей подписке Azure необходимо сначала войти в tooyour учетная запись Azure с `az login`. Для этого существует несколько способов.

* **Интерактивный вход**: `az login`.
* **Вход с использованием имени пользователя SSH и пароля**: `az login -u johndoe@contoso.com -p VerySecret`.
  * Этот способ не работает с учетными записями Майкрософт или с учетными записями, которые используют многофакторную идентификацию.
* **Вход с использованием субъекта-службы**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`.

## <a name="azure-cli-20-sample-script"></a>Пример скрипта Azure CLI 2.0

Далее мы будем работать с небольшой сценарий, который выдает несколько основных toointeract команды Azure CLI 2.0 с ресурсов хранилища Azure. Hello скрипт сначала создает новый контейнер в учетной записи, а затем передает существующий контейнер toothat файла (в виде больших двоичных объектов). Затем перечисляет все большие двоичные объекты в контейнере hello и наконец, загружает hello назначения tooa файл на локальном компьютере, который можно указать.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Настройка и выполнение скрипта hello**

1. Откройте текстовый редактор, затем скопируйте и вставьте hello предшествующий скрипт в редактор hello.

2. Затем обновите tooreflect переменные сценария hello параметры конфигурации. Замените следующие значения, заданные hello:

   * **\<storage_account_name\>**  hello имя вашей учетной записи хранилища.
   * **\<storage_account_key\>**  hello первичный или вторичный ключ доступа для учетной записи хранилища.
   * **\<container_name\>**  имя hello новый контейнер toocreate, такие как «azure-cli пример container».
   * **\<blob_name\>**  имя BLOB-объект назначения hello в контейнере hello.
   * **\<file_to_upload\>**  hello путь к файлу toosmall на локальном компьютере, такие как «~ / images/HelloWorld.png».
   * **\<destination_file\>**  hello путь к файлу назначения, такие как «~ / downloadedImage.png».

3. После обновления hello необходимые переменные, сохранить сценарий hello и выйти из редактора. Hello Далее предполагается, что с названием сценарий **my_storage_sample.sh**.

4. Пометка hello скрипта как исполняемый файл и при необходимости:`chmod +x my_storage_sample.sh`

5. Выполнение скрипта hello. например в Bash: `./my_storage_sample.sh`

Вы должны видеть аналогичные toohello следующие выходные данные и hello  **\<destination_file\>**  указан в hello скрипт должен отобразиться на локальном компьютере.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Hello выше выходные данные выглядят в **таблицы** формат. Можно указать, какой выход toouse формат, указав hello `--output` аргумент командах CLI или задать глобально с помощью `az configure`.
>

## <a name="manage-storage-accounts"></a>Управление учетными записями хранения

### <a name="create-a-new-storage-account"></a>Создать новую учетную запись хранения
toouse хранилища Azure, необходима учетная запись хранения. Можно создать новую учетную запись хранилища Azure, после настройки компьютера слишком[подключения подписки tooyour](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location` — расположение (обязательный параметр). Например, "западная часть США".
* `--name`[Обязательно]: имя учетной записи хранения hello. Hello имя должно состоять из 3 символов too24 и использовать только строчные буквы или цифры.
* `--resource-group` — имя группы ресурсов (обязательный параметр).
* `--sku`[Обязательно]: hello учетной записи хранилища Конфигураций. Допустимые значения:
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Установка учетной записи хранения Azure по умолчанию в переменные среды
В подписке может быть несколько учетных записей хранения Azure. один из них tooselect toouse для хранения всех последующих команд, можно задать эти переменные среды:

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Другой способ tooset учетной записи хранения по умолчанию — с помощью строки подключения. Сначала необходимо получить строку подключения hello с hello `show-connection-string` команды:

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

Затем hello копирования выходных данных строки подключения и установите hello `AZURE_STORAGE_CONNECTION_STRING` переменной среды (возможно, придется строка подключения tooenclose hello в кавычки):

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Все примеры в следующих разделах этой статьи hello предполагается, что вы задали hello `AZURE_STORAGE_ACCOUNT` и `AZURE_STORAGE_ACCESS_KEY` переменные среды.
>

## <a name="create-and-manage-blobs"></a>Создание больших двоичных объектов (BLOB-объектов) и управление ими
Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, например текстовых или двоичных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS. В этом разделе предполагается, что вы уже знакомы с понятиями службы хранилища BLOB-объектов Azure. Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](/rest/api/storageservices/blob-service-concepts).

### <a name="create-a-container"></a>Создание контейнера
Каждый BLOB-объект в хранилище Azure должен находиться в контейнере. Контейнер можно создать с помощью hello `az storage container create` команды:

```azurecli
az storage container create --name <container_name>
```

Можно задать один из трех уровней доступа на чтение для нового контейнера с помощью hello необязательно `--public-access` аргумент:

* `off`(по умолчанию): контейнер данных является закрытым toohello владелец учетной записи.
* `blob`: общий доступ на чтение для больших двоичных объектов.
* `container`: Открытого списка доступа toohello весь контейнер.

Дополнительные сведения см. в разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](../blobs/storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Отправка tooa контейнер больших двоичных объектов
Хранилище BLOB-объектов Azure поддерживает блочные, добавочные и страничные BLOB-объекты. Отправка больших двоичных объектов tooa контейнера с помощью hello `blob upload` команды:

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 По умолчанию hello `blob upload` команда отправляет большие двоичные объекты toopage *.vhd файлы, или блочных BLOB-объектов в противном случае. toospecify другой тип при отправить большой двоичный объект, можно использовать hello `--type` аргумент--допустимыми значениями являются `append`, `block`, и `page`.

 Дополнительные сведения о типах другой большой двоичный объект hello. в разделе [основные сведения о блочных, добавлять большие двоичные объекты и страничные большие двоичные объекты](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Скачивание большого двоичного объекта из контейнера
В этом примере показано, как toodownload большого двоичного объекта из контейнера:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере

Перечисление hello больших двоичных объектов в контейнере с hello [списка больших двоичных объектов хранилища az](/cli/azure/storage/blob#list) команды.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>Копирование BLOB-объектов
Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями или внутри них.

Hello ниже приведен пример tooanother учетной записи toocopy больших двоичных объектов из одного места хранения. Сначала создается контейнер в учетной записи хранения источника hello, указав доступ для чтения к его большим двоичным объектам. Далее мы отправьте файл toohello контейнера и, наконец, копирования hello BLOB-объекта контейнера, в котором в контейнер в учетной записи хранения назначения hello.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

В приведенном выше примере hello hello конечный контейнер должен уже существовать в hello целевой учетной записью хранения для toosucceed операцию копирования hello. Кроме того, hello исходного большого двоичного объекта указан в hello `--source-uri` аргумент должен включать токен общего доступа адреса (SAS) или быть общедоступным, как показано в примере.

### <a name="delete-a-blob"></a>Удаление большого двоичного объекта
toodelete большого двоичного объекта используйте hello `blob delete` команды:

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Создание общих папок и управление ими
Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью протокола Server Message Block (SMB) hello. Виртуальные машины Microsoft Azure и облачные службы, а также локальные приложения, могут совместно использовать данные через монтированные ресурсы. Вы можете управлять файловыми ресурсами и файл данных с помощью hello Azure CLI. Дополнительные сведения о хранилище файлов Azure см. в разделе [приступить к работе с хранилищем Windows Azure файл](../storage-dotnet-how-to-use-files.md) или [как toouse хранилища Azure File с Linux](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Создайте общую папку
Общая папка Azure представляет собой общую папку с файлами SMB в Azure. Все каталоги и файлы должны быть созданы в общей папке. Учетная запись может содержать неограниченное количество общих ресурсов и общую папку можно сохранить неограниченное количество файлов копирование ограничения емкости toohello hello учетной записи хранилища. Hello следующий пример создает общую папку с именем **myshare**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Создайте каталог
Каталог обеспечивает иерархическую структуру в общей папке Azure. Hello следующий пример создает каталог с именем **myDir** в общей папке hello.

```azurecli
az storage directory create --name myDir --share-name myshare
```

Путь к каталогу может включать несколько уровней, например **dir1/dir2**. Однако прежде чем создавать подкаталог, необходимо убедиться в наличии всех родительских каталогов. Например, для пути **dir1/dir2** вам потребуется сначала создать каталог **dir1**, а затем — каталог **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Отправка в локальной папке tooa
Hello следующий пример отправляет файл из **~/temp/samplefile.txt** tooroot из hello **myshare** общей папки. Hello `--source` аргумент задает существующего локального файла tooupload hello.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Как и в случае создания каталога можно указать путь к каталогу в hello общего ресурса tooupload hello tooan существующий каталог файлов в общей папке hello:

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Копирование ТБ too1 может быть файл в общей папке hello.

### <a name="list-hello-files-in-a-share"></a>Список файлов hello в общей папке
Список файлов и каталогов в общей папке, можно с помощью hello `az storage file list` команды:

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Копирование файлов      
Можно скопировать файл tooanother, большой двоичный объект файла tooa или tooa файла большого двоичного объекта. Например, toocopy tooa каталога файла в другую общую папку:        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Дальнейшие действия
Ниже приведены некоторые дополнительные ресурсы для изучения работы с hello Azure CLI 2.0.

* [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) (Приступая к работе с Azure CLI 2.0)
* [Azure CLI 2.0 command reference](/cli/azure) (Справочник по командам Azure CLI 2.0)
* [Статья об Azure CLI 2.0 на сайте GitHub](https://github.com/Azure/azure-cli)
