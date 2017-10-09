---
title: "aaaMove данные из локального SQL Server tooSQL Azure с фабрикой данных Azure | Документы Microsoft"
description: "Настройка конвейер ADF, которая состоит из двух действий миграции данных, которые совместно перемещают данные ежедневно между базами данных в локальной среде и в облаке hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>Перемещение данных из локальной tooSQL сервера SQL Azure с фабрикой данных Azure
В этом разделе показано, как toomove данные из локальной базы данных SQL Server tooa база данных SQL Azure через хранилище больших двоичных объектов Azure с помощью hello фабрики данных Azure (ADF).

Для таблицы, перечислены различные параметры для перемещения данных tooan базы данных SQL Azure, в разделе [перемещение данных tooan базы данных SQL Azure для машинного обучения Azure](machine-learning-data-science-move-sql-azure.md).

## <a name="intro"></a>Общие сведения: Что такое ADF и когда он должен быть используется toomigrate данных?
Фабрика данных Azure — это служба интеграции полностью управляемая данных на основе облака, координирует и автоматизирует процессы hello перемещения и преобразования данных. Ключевым принципом Hello hello ADF модели является конвейера. Конвейер — это логическое группирование действий, каждое из которых определяет действия tooperform hello на hello данные, содержащиеся в наборах данных. Связанные службы, используемые toodefine hello сведения, необходимые для фабрики данных tooconnect toohello данных ресурсов.

С ADF существующие службы обработки данных могут быть включены в конвейерах данных, которые высокодоступной и управляемой в облаке hello. Конвейеры этих данных может быть запланированных tooingest, подготовка, преобразование, анализ и публиковать данные и управляет hello сложных данных и обработки зависимости и управляет им ADF. Решения могут быть hello быстро встроенного и развернутого в облаке, подключение все большее число локальных и облачных источников данных.

ADF стоит использовать в следующих случаях:

* Когда данные toobe потребности постоянно перенесены в гибридном сценарии, который обращается к оба локальные и облачные ресурсы
* добавить при переносе tooit при транзакции данных hello или toobe потребностей изменен или иметь бизнес-логики.

ADF позволяет hello планирования и отслеживания заданий, используя простые сценарии JSON, управлять hello перемещение данных на периодической основе. ADF также обладает другими возможностями, такими как поддержка сложных операций. Дополнительные сведения о ADF документации hello в [фабрики данных Azure (ADF)](https://azure.microsoft.com/services/data-factory/).

## <a name="scenario"></a>Hello сценария
Мы настраиваем конвейер ADF, который объединяет два действия переноса данных. Вместе они перемещаются данные ежедневно между локальной базы данных SQL и базы данных SQL Azure в облаке hello. Hello два действия являются:

* копирование данных из tooan базы данных SQL Server в локальной учетной записи хранилища больших двоичных объектов
* Копирует данные из tooan учетной записи хранилища больших двоичных объектов hello базы данных SQL Azure.

> [!NOTE]
> Здравствуйте, описанного здесь было адаптировать из более подробные учебник, обеспечиваемый hello ADF hello: [перемещения данных между локальным источникам и облако с помощью шлюза управления данными](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) ссылается на toohello соответствующие разделы этой статьи предоставляются, когда это необходимо.
>
>

## <a name="prereqs"></a>Предварительные требования
Для выполнения действий, описанных в этом учебнике, вам необходимо следующее.

* <seg>
  **Подписка Azure**.</seg> Если у вас нет подписки, вы можете зарегистрироваться для получения [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).
* **Azure storage account**. Использовать учетную запись хранилища Azure для хранения данных hello в этом учебнике. При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи. После создания учетной записи хранилища hello необходимо tooobtain hello от имени учетной записи хранилища hello tooaccess использования ключа. Ознакомьтесь с разделом [Управление ключами доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Доступ tooan **базы данных SQL Azure**. Если необходимо настроить базы данных SQL Azure, hello tpoic [Приступая к работе с базой данных SQL Microsoft Azure ](../sql-database/sql-database-get-started.md) предоставляет сведения о том, как tooprovision новый экземпляр базы данных SQL Azure.
* Установленная и настроенная локальная среда **Azure PowerShell**. Инструкции см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

> [!NOTE]
> В этой процедуре используется hello [портал Azure](https://portal.azure.com/).
>
>

## <a name="upload-data"></a>Отправка hello данных tooyour локального SQL Server
Мы используем hello [NYC такси dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) процесс миграции toodemonstrate hello. Hello такси NYC набор данных доступен, описанных в этой записи в хранилище больших двоичных объектов [NYC такси данных](http://www.andresmh.com/nyctaxitrips/). Hello данные содержат два файла, файл trip_data.csv hello, который содержит сведения о пути, и hello trip_far.csv файл, содержащий сведения о тариф авиакомпании hello платная для каждого маршрута. Пример и описание этих файлов приведены в [описании набора данных «Поездки такси Нью-Йорка»](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Можно адаптировать hello процедуры, описанные здесь tooa набор данных или действуйте hello, как описано с помощью hello такси NYC набора данных. hello tooupload такси NYC набора данных в базу данных SQL Server в локальной среде, выполните процедуру hello, описанные в [массового импорта данных в базу данных SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Эти инструкции относятся к SQL Server на виртуальной машине Azure, но hello процедур для передачи toohello находится на локальном сервере SQL Server hello таким же.

## <a name="create-adf"></a> Создание фабрики данных Azure
Здравствуйте, инструкции по созданию новой фабрики данных Azure и группы ресурсов в hello [портал Azure](https://portal.azure.com/) предоставляются [создания фабрики данных Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory). Новый экземпляр ADF имя hello *adfdsp* и создание группы ресурсов имя hello *adfdsprg*.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>Установить и настроить шлюз управления данными hello
tooenable конвейеры toowork фабрики данных Azure с SQL Server в локальной среде, необходимо tooadd его как фабрика данных toohello связанной службы. toocreate связанной службы локального сервера SQL Server, необходимо выполнить следующее:

* Загрузите и установите шлюз управления данными Майкрософт на hello на локальном компьютере.
* Настройте службу hello связаны для hello локального источника данных toouse hello шлюза.

Шлюз управления данными Hello сериализует и десериализует данные источника и приемника hello, на компьютере hello, в котором она размещена.

Инструкции по установке и сведения о шлюзе управления данными см. в статье [Перемещение данных между локальными источниками и облаком при помощи шлюза управления данными](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

## <a name="adflinkedservices"></a>Создание связанных служб tooconnect toohello ресурсы данных
Связанная служба определяет hello сведения, необходимые для ресурса данных tooa tooconnect фабрики данных Azure. Hello пошаговые инструкции для создания связанных служб предоставляется в [создания связанных служб](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).

В данном сценарии есть три ресурса, для которых требуются связанные службы.

1. [Связанная служба для локального SQL Server](#adf-linked-service-onprem-sql)
2. [Связанная служба для хранилища больших двоичных объектов Azure](#adf-linked-service-blob-store)
3. [Связанная служба для базы данных SQL Azure](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>Связанная служба для базы данных локального SQL Server
Служба hello связаны toocreate для hello локального SQL Server:

* Нажмите кнопку hello **хранилище данных** в hello ADF целевая страница на классический портал Azure
* Выберите **SQL** и введите hello *username* и *пароль* учетные данные для hello локального SQL Server. Требуется servername hello tooenter как **имени экземпляра обратную косую черту полное доменное имя сервера (имя_сервера\имя_экземпляра)**. Hello имя связанной службы *adfonpremsql*.

### <a name="adf-linked-service-blob-store"></a>Связанная служба для больших двоичных объектов
toocreate hello связанной службы для учетной записи хранилища больших двоичных объектов hello:

* Нажмите кнопку hello **хранилище данных** в hello ADF целевая страница на классический портал Azure
* выберите **Учетная запись хранения Azure**
* Введите hello хранилища больших двоичных объектов Azure имя учетной записи ключа и контейнера. Hello имя связанной службы *adfds*.

### <a name="adf-linked-service-azure-sql"></a>Связанная служба для базы данных SQL Azure
toocreate hello связанной службы для hello базы данных SQL Azure:

* Нажмите кнопку hello **хранилище данных** в hello ADF целевая страница на классический портал Azure
* Выберите **Azure SQL** и введите hello *username* и *пароль* учетные данные для hello базы данных SQL Azure. Hello *username* должен быть указан как  *user@servername* .   

## <a name="adf-tables"></a>Определение и создание таблиц toospecify как tooaccess hello наборов данных
Создание таблиц, задающих структуры hello, расположение и доступность hello наборов данных с помощью следующих процедур на основе сценария hello. Файлы JSON — это таблицы используется toodefine hello. Дополнительные сведения о структуре hello этих файлов см. в разделе [наборы данных](../data-factory/data-factory-create-datasets.md).

> [!NOTE]
> Необходимо выполнить hello `Add-AzureAccount` командлет перед выполнением hello [New AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm командлета, hello подписки справа Azure установлен для выполнения команды hello. Документацию по этим командлетам см. в статье [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).
>
>

определения на основе JSON Hello в таблицах hello использовать hello следующие имена:

* Hello **имя таблицы** в hello в локальной среде SQL server — *nyctaxi_data*
* Hello **имя контейнера** в hello хранилища больших двоичных объектов учетная запись является *имя_контейнера*  

Для этого конвейера ADF необходимо определить три таблицы:

1. [Локальная таблица SQL](#adf-table-onprem-sql).
2. [таблица больших двоичных объектов; ](#adf-table-blob-store)
3. [таблица SQL Azure.](#adf-table-azure-sql)

> [!NOTE]
> Эти процедуры используйте toodefine Azure PowerShell и создайте hello ADF действий. Однако эти задачи можно также выполнить при помощи hello портал Azure. Дополнительные сведения см. в разделе [Создание наборов данных](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).
>
>

### <a name="adf-table-onprem-sql"></a>Локальная таблица SQL
Определение таблицы Hello для hello локального SQL Server, указанного в hello следующий JSON-файла:

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

имена столбцов Hello не были включены здесь. Можно подзапроса select на приветствия имен столбцов, включая их здесь (сведений проверьте hello [документации ADF](../data-factory/data-factory-data-movement-activities.md) раздела.

Копирование определения JSON hello hello таблицы в файл с именем *onpremtabledef.json* файл и сохраните его tooa известно расположение (здесь предполагается, что toobe *C:\temp\onpremtabledef.json*). Создайте таблицу hello в ADF с hello, выполнив командлет Azure PowerShell:

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>таблица больших двоичных объектов;
Определение таблицы hello для hello выходные данные больших двоичных объектов находятся в следующих hello (сопоставляет полученный hello данных из большого двоичного объекта в локальной tooAzure):

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Копирование определения JSON hello hello таблицы в файл с именем *bloboutputtabledef.json* файл и сохраните его tooa известно расположение (здесь предполагается, что toobe *C:\temp\bloboutputtabledef.json*). Создайте таблицу hello в ADF с hello, выполнив командлет Azure PowerShell:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>таблица SQL Azure.
Определение таблицы hello для приветствия выходных данных SQL Azure имеет следующие hello (Эта схема сопоставляет hello данные поступают из hello больших двоичных объектов):

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Копирование определения JSON hello hello таблицы в файл с именем *AzureSqlTable.json* файл и сохраните его tooa известно расположение (здесь предполагается, что toobe *C:\temp\AzureSqlTable.json*). Создайте таблицу hello в ADF с hello, выполнив командлет Azure PowerShell:

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>Определение и создание конвейера hello
Укажите hello действиями, которые входят toohello конвейера и создать конвейер hello с помощью следующих процедур на основе сценария hello. Файл JSON, используется toodefine hello конвейера свойства.

* Hello сценарий предполагает, что hello **имя конвейера** — *AMLDSProcessPipeline*.
* Также Обратите внимание, что мы устанавливаем hello периодичности toobe конвейера hello выполнена на ежедневно основы и использование hello по умолчанию время выполнения для задания hello (12: 00 UTC).

> [!NOTE]
> Hello следующие процедуры используйте toodefine Azure PowerShell и создать конвейер ADF hello. Однако эту задачу также можно выполнить на портале Azure. Дополнительные сведения см. в разделе [Создание конвейера](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).
>
>

С помощью определения таблиц hello ранее приведено определение конвейера hello для hello ADF задается следующим образом:

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

Скопировать это определение JSON конвейера hello в файл с именем *pipelinedef.json* файл и сохраните его tooa известно расположение (здесь предполагается, что toobe *C:\temp\pipelinedef.json*). Создайте конвейер hello в ADF с hello, выполнив командлет Azure PowerShell:

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

Убедитесь, что вы может конвейера hello на hello ADF в hello классическом портале Azure отображаются следующим образом (при нажатии кнопки hello схемы)

![Конвейер ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Запуск конвейера hello
конвейер Hello можно запустить с помощью hello следующую команду:

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

Hello *startdate* и *enddate* значения параметров необходимо заменить фактические даты hello, между которыми требуется hello конвейера toorun toobe.

После выполняется конвейера hello, можно будет toosee hello данные отображались в контейнере hello, выбранных для большого двоичного объекта hello, один файл в день.

Обратите внимание, что мы не использовались hello функциональные возможности, предоставляемые данные toopipe ADF, постепенно. Дополнительные сведения о toodo это и другие возможности, предоставляемые ADF, в статье hello [документации ADF](https://azure.microsoft.com/services/data-factory/).
