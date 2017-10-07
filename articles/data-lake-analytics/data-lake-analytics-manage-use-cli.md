---
title: "Аналитика Озера данных Azure, с помощью интерфейса командной строки Azure aaaManage | Документы Microsoft"
description: "Узнайте об использовании заданий учетные записи аналитики Озера данных toomanage, источники данных и пользователей с помощью Azure CLI"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Управление аналитикой озера данных Azure с помощью интерфейса командной строки (CLI) Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Узнайте, как учетные записи toomanage аналитики Озера данных Azure, источники данных, пользователей и заданий с помощью hello Azure CLI. toosee статьи, посвященные управлению с помощью других средств, щелкните выше выберите вкладку hello.


**Предварительные требования**

Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Подписка Azure**. См. страницу [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Интерфейс командной строки Azure**. См. статью [Установка и настройка интерфейса командной строки Azure](../cli-install-nodejs.md).
  * Загрузите и установите hello **предварительного выпуска** [средства Azure CLI](https://github.com/MicrosoftBigData/AzureDataLake/releases) чтобы toocomplete этой демонстрации.
* **Проверка подлинности**, с использованием hello следующую команду:
  
        azure login
    Дополнительные сведения о проверке подлинности с помощью рабочей или учебной учетной записи см. в разделе [подключение tooan подписки Azure из hello Azure CLI](../xplat-cli-connect.md).
* **Переключите режим диспетчера ресурсов Azure toohello**, с использованием hello следующую команду:
  
        azure config mode arm

**toolist hello хранилища Озера данных и аналитики Озера данных команды:**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Управление учетными записями
Перед выполнением любого задания аналитики озера данных необходимо иметь учетную запись аналитики озера данных. В отличие от Azure HDInsight учетная запись аналитики не оплачивается, если ни одно задание не выполняется.  Вы платите только за время hello, при выполнении задания.  Дополнительные сведения см. в разделе [Обзор аналитики озера данных Azure](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Создание учетных записей
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>Обновление учетных записей
Hello следующая команда обновляет свойства hello существующей учетной записи аналитики Озера данных

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>Список учетных записей
Список учетных записей аналитики озера данных 

    azure datalake analytics account list

Список учетных записей аналитики озера данных в конкретной группе ресурсов

    azure datalake analytics account list -g "<Azure Resource Group Name>"

Получение сведений о конкретной учетной записи аналитики озера данных

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>Удаление учетных записей аналитики озера данных
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Управление источниками данных учетной записи
Аналитика Озера данных в настоящее время поддерживает следующие источники данных hello:

* [Хранилище озера данных Azure](../data-lake-store/data-lake-store-overview.md)
* [Хранилище Azure](../storage/common/storage-introduction.md)

При создании учетной записи аналитики, необходимо назначить хранилища Озера данных Azure учетная запись toobe hello по умолчанию учетной записи хранения. Hello учетной записи хранения по умолчанию ADL используется toostore метаданные задания и задания журналы аудита. После создания учетной записи аналитики можно добавить дополнительные учетные записи хранения озера данных и учетные записи хранения Azure. 

### <a name="find-hello-default-adl-storage-account"></a>Найти учетную запись хранения ADL по умолчанию hello
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

значение Hello указана в списке свойств: datalakeStoreAccount:name.

### <a name="add-additional-azure-blob-storage-accounts"></a>Добавление дополнительных учетных записей хранения больших двоичных объектов Azure
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Поддерживаются только короткие имена хранилищ BLOB-объектов.  Не следует использовать полное доменное имя, например "myblob.blob.core.windows.net".
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>Добавление дополнительных учетных записей хранения озера данных
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d] — tooindicate необязательный ключ, является ли hello Озера данных добавляется учетная запись Озера данных по умолчанию hello. 

### <a name="update-existing-data-source"></a>Обновление существующего источника данных
tooset существующего хранилища Озера данных учетной записи toobe hello значения по умолчанию:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate существующего ключа учетной записи хранилища больших двоичных объектов:

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>Список источников данных
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Источник данных списка аналитики озера данных](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Удаление источников данных
toodelete учетной записи хранилища Озера данных:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete учетной записи хранилища больших двоичных объектов:

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>Управление заданиями
Для создания любого задания требуется учетная запись аналитики озера данных.  Дополнительные сведения см. в разделе [Управление учетными записями Data Lake Analytics](#manage-accounts).

### <a name="list-jobs"></a>Список заданий
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Источник данных списка аналитики озера данных](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Получение сведений о задании
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>Отправка заданий
> [!NOTE]
> приоритет по умолчанию Hello задания равно 1000, а степень параллелизма для задания hello по умолчанию — 1.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>Отмена задания
Использовать идентификатор задания hello toofind команда hello списка, а затем использовать задание hello toocancel "Отмена".

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>Управление каталогом
каталог Hello U-SQL является toostructure используемых данных и кода, поэтому они могут совместно использоваться сценарии U-SQL. Hello каталога включает hello максимально возможную производительность с данными в Озера данных Azure. Дополнительные сведения см. в разделе [Использование каталога U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-catalog-items"></a>Список элементов каталога
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

типы Hello включают базы данных, схемы, сборки, внешний источник данных, таблицы, возвращающей табличное значение функции или статистики таблицы.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>Использование групп ARM
Обычно приложения состоят из множества компонентов, например веб-приложения, базы данных, сервера базы данных, хранилища и служб сторонних поставщиков. Диспетчер ресурсов Azure (ARM) позволяет toowork с ресурсами hello в приложении как группы, который ссылается tooas группу ресурсов Azure. Можно развернуть, обновления, отслеживания или удалить все ресурсы hello для вашего приложения, в один, согласованной операции. Вы можете уточнить счета для своей организации, просмотрев сведенные затраты для всей группы. Можно уточнить выставления счетов для вашей организации, просмотрев hello сведенные затраты для всей группы hello. в статье [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md). 

Служба аналитики Озера данных могут включать hello следующие компоненты:

* Учетная запись аналитики озера данных Azure
* Требуемая учетная запись хранения озера данных Azure по умолчанию
* Дополнительные учетные записи хранения озера данных Azure
* Дополнительные учетные записи хранения Azure

Можно создать все эти компоненты в группе один toomake группы ARM их проще toomanage.

![Аналитика озера данных Azure: учетная запись и хранилище](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Учетную запись аналитики Озера данных и учетных записей хранилища зависимых hello должны быть помещены в hello же центре обработки данных Azure.
Однако Hello ARM группы могут быть расположены в другом центре обработки данных.  

## <a name="see-also"></a>См. также
* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
* [Начало работы с аналитикой озера данных с помощью портала Azure](data-lake-analytics-get-started-portal.md)
* [Управление аналитикой озера данных Azure с помощью портала Azure](data-lake-analytics-manage-use-portal.md)
* [Мониторинг заданий аналитики озера данных Azure и устранение связанных с ними неполадок с помощью портала Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

