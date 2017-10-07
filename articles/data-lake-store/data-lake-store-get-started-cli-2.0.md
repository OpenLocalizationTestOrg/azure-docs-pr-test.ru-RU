---
title: "интерфейс tooget aaaUse Azure 2.0 командной строки к выполнению хранилища Озера данных Azure | Документы Microsoft"
description: "Использование командной строки Azure кросс платформенных 2.0 toocreate учетной записи хранилища Озера данных и выполнения основных операций"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Начало работы с Azure Data Lake Store с помощью Azure CLI 2.0
> [!div class="op_single_selector"]
> * [Портал](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Пакет SDK для .NET](data-lake-store-get-started-net-sdk.md)
> * [Пакет SDK для Java](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Узнайте, как toocreate toouse Azure CLI 2.0 Azure Озера данных хранения учетной записи и выполнения основных операций, таких как создание папками, отправка и загрузка файлов данных, удалите учетную запись, и т. д. Дополнительные сведения о хранилище озера данных см. в [обзоре Data Lake Store](data-lake-store-overview.md).

Hello Azure CLI 2.0 — это новый интерфейс командной строки Azure для управления ресурсами Azure. Его можно использовать в Windows, Linux и macOS. Дополнительные сведения см. в [обзоре Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview). Вы также можете изучить hello [хранилища Озера данных Azure, CLI 2.0 ссылка](https://docs.microsoft.com/cli/azure/dls) полный список команд и синтаксис.


## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Azure CLI 2.0** — см. инструкции в статье об [установке Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="authentication"></a>Аутентификация

В этой статье используется более простой подход к проверке подлинности в службе Data Lake Store, в которую выполняется вход от имени пользователя. Hello доступ уровня хранилища Озера tooData учетной записи и файловая система распространяется уровень доступа hello приветствия вошедшего пользователя. Однако существуют другие методы как хорошо tooauthenticate с хранилища Озера данных, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**. Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).


## <a name="log-in-tooyour-azure-subscription"></a>Войдите в tooyour подписки Azure

1. Войдите в подписку Azure.

    ```azurecli
    az login
    ```

    В следующем шаге hello получить toouse кода. Используйте страницу https://aka.ms/devicelogin hello tooopen веб браузера и введите tooauthenticate кода hello. Все запрашиваемые toolog, используя свои учетные данные.

2. После входа список окна hello всех hello подписки Azure, которые связаны с вашей учетной записи. Используйте hello, следующая команда toouse конкретной подписки.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Создание учетной записи хранения озера данных Azure

1. Создайте новую группу ресурсов. В hello следующую команду предоставляют значения параметров, которые вы хотите toouse hello. Если имя расположения hello содержит пробелы, необходимо поместите его в кавычки. Например, "East US 2". 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Создайте учетную запись хранилища Озера данных hello.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Создание папок в учетной записи хранения озера данных

Можно создать папки под вашей toomanage учетной записи хранилища Озера данных Azure и хранения данных. Следующая команда toocreate папка hello используйте **mynewfolder** hello корню hello хранилища Озера данных.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> Hello `--folder` параметр гарантирует, что команда hello создает папку. Если этот параметр не указан, команда hello создает пустой файл с именем mynewfolder в корне hello hello хранилища Озера данных.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>Отправка учетной записи хранилища Озера данных tooa данных

Можно передать хранилища Озера данных tooData непосредственно на hello корневого уровня или tooa папку, созданную в пределах учетной записи hello. фрагменты кода Hello ниже показано, как tooupload некоторые папку с образцами данных toohello (**mynewfolder**) был создан в предыдущем разделе hello.

Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Загрузите файл hello и сохранить его в локальный каталог на компьютере, например C:\sampledata\.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Для назначения hello необходимо указать hello полный путь, включая имя файла hello.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Вывод списка файлов в учетной записи Data Lake Store

Используйте следующие команды toolist hello файлы в учетную запись хранилища Озера данных hello.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

выходные данные Hello объекта должны быть примерно следующее toohello:

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Переименование, скачивание и удаление данных из Data Lake Store 

* **файл toorename**, использовать hello следующую команду:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **файл toodownload**, используйте следующую команду hello. Убедитесь, что путь hello назначения уже существует.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > Hello команда создает папку назначения hello, если он не существует.
    > 
    >

* **файл toodelete**, использовать hello следующую команду:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Папка hello toodelete **mynewfolder** и файл hello **vehicle1_09142014_copy.csv** вместе в одной команде, используйте hello--recurse параметра

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Работа с разрешениями и списками управления доступом для учетной записи Data Lake Store

В этом разделе вы узнаете о том, как toomanage списки управления доступом и разрешения с помощью Azure CLI 2.0. Подробные сведения о реализации списков ACL в Azure Data Lake Store см. в статье [Контроль доступа в Azure Data Lake Store](data-lake-store-access-control.md).

* **tooupdate hello владельца файла или папки**, использовать hello следующую команду:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **tooupdate hello разрешения для файла или папки**, использовать hello следующую команду:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **hello tooget ACL для определенного пути**, использовать hello следующую команду:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    Hello выходные данные должны быть примерно toohello следующее:

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **tooset запись ACL**, использовать hello следующую команду:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **tooremove запись ACL**, использовать hello следующую команду:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **весь список управления Доступом по умолчанию tooremove**, использовать hello следующую команду:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **tooremove всей нестандартных ACL**, использовать hello следующую команду:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Удаление учетной записи хранения озера данных
Используйте следующие команды toodelete учетной записи хранилища Озера данных hello.

```azurecli
az dls account delete --account mydatalakestore
```

При появлении запроса введите **Y** учетной записи toodelete hello.

## <a name="next-steps"></a>Дальнейшие действия

* [Справочник по CLI 2.0 Azure Data Lake](https://docs.microsoft.com/cli/azure/dls)
* [Защита данных в Data Lake Store](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
