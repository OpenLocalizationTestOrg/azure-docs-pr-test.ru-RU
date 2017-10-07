---
title: "aaaCopy данные из BLOB-объектов хранилища Azure в хранилище Озера данных | Документы Microsoft"
description: "Использовать AdlCopy средство toocopy данные из хранилища Озера tooData больших двоичных объектов хранилища Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure
> [!div class="op_single_selector"]
> * [С помощью DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [С помощью AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Хранилище Озера данных Azure предоставляет средство командной строки, [AdlCopy](http://aka.ms/downloadadlcopy), toocopy данные из hello следующие источники:

* Из больших двоичных объектов службы хранилища Azure в Data Lake Store. Нельзя использовать AdlCopy toocopy данные из хранилища Озера данных tooAzure хранилища больших двоичных объектов.
* Между двумя учетными записями хранения Azure Data Lake Store.

Кроме того можно использовать средство AdlCopy hello в двух разных режимах:

* **Автономный**, где hello средство использует задачу hello tooperform ресурсы хранилища Озера данных.
* **С помощью учетной записи аналитики Озера данных**, в которых hello единиц, учетной записи аналитики Озера данных tooyour являются операции копирования используется tooperform hello. Может потребоваться toouse этот параметр при исследовании задачах копирования hello tooperform предсказуемым образом.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **больших двоичных объектов хранилища Azure** с некоторыми данными.
* **Учетная запись Azure Data Lake Store.** Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md)
* **Azure аналитики Озера данных учетной записи (необязательно)** -разделе [Приступая к работе с аналитики Озера данных Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md) инструкции как toocreate Озера данных хранения учетной записи.
* **Средство AdlCopy**. Установка средства AdlCopy hello из [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).

## <a name="syntax-of-hello-adlcopy-tool"></a>Синтаксис программы AdlCopy hello
Используйте следующий синтаксис toowork инструментом AdlCopy hello hello

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

Ниже описаны параметры Hello в синтаксисе hello:

| Параметр | Описание |
| --- | --- |
| Источник |Указывает расположение hello hello исходных данных в большом двоичном объекте hello хранилища Azure. Hello источник может быть контейнер больших двоичных объектов, большой двоичный объект или другой учетной записи хранилища Озера данных. |
| Dest |Задает toocopy назначения hello хранилища Озера данных для. |
| SourceKey |Указывает ключ доступа к хранилищу hello для hello источник больших двоичных объектов хранилища Azure. Это необходимо только в том случае, если источник hello — контейнер больших двоичных объектов или большого двоичного объекта. |
| Учетная запись. |**Необязательно**. Используйте это задание копирования hello toorun учетной записи toouse аналитики Озера данных Azure. Если использовать параметр/Account hello в синтаксисе hello, но не указывать учетную запись аналитики Озера данных, AdlCopy использует задание hello toorun учетной записи по умолчанию. Кроме того при использовании этого параметра необходимо добавить источник hello (больших двоичных объектов хранилища Azure) и назначение (хранилища Озера данных Azure) в качестве источников данных для учетной записи аналитики Озера данных. |
| Units |Указывает hello число единиц аналитики Озера данных, которые будут использоваться для задания копирования hello. Этот параметр является обязательным, если вы используете hello **/учетной записи** параметр учетной записи аналитики Озера данных toospecify hello. |
| Модель |Указывает шаблон регулярного выражения, которое указывает, какие toocopy больших двоичных объектов или файлов. В AdlCopy используется сопоставление с учетом регистра. использовать шаблон по умолчанию Hello, когда ни одному из шаблонов является toocopy все элементы. Задание нескольких шаблонов не поддерживается. |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>Использовать данные toocopy AdlCopy (как автономный) из BLOB-объект хранилища Azure
1. Откройте командную строку и перейдите в каталог toohello AdlCopy установки, обычно `%HOMEPATH%\Documents\adlcopy`.
2. Запустите hello, следующая команда toocopy конкретного BLOB-объектов из hello исходный контейнер tooa хранилища Озера данных:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Например:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] выше синтаксис Hello указывает hello файл toobe скопированный tooa папку в учетной записи хранилища Озера данных hello. Средство AdlCopy создает папку, если имя hello указанная папка не существует.

    Появится запрос tooenter hello учетные данные для hello подписки Azure, в котором у вас есть учетная запись хранилища Озера данных. Вы увидите выходные данные примерно toohello следующие:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. Можно также скопировать все большие двоичные объекты hello из одного контейнера toohello хранилища Озера данных учетной записи с помощью hello следующую команду:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    Например:

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>Рекомендации по производительности

При копировании из учетной записи хранилища больших двоичных объектов может регулироваться во время копирования на стороне хранилища больших двоичных объектов hello. Это может повлиять на производительность hello задания копирования. toolearn более об ограничениях hello хранилища больших двоичных объектов Azure, см. ограничения хранилища Azure при [подписка Azure и ограничения служб](../azure-subscription-service-limits.md).

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>Использовать данные toocopy AdlCopy (как автономный) с другой учетной записи хранилища Озера данных
Можно также использовать AdlCopy toocopy данных между двумя учетными записями хранилища Озера данных.

1. Откройте командную строку и перейдите в каталог toohello AdlCopy установки, обычно `%HOMEPATH%\Documents\adlcopy`.
2. Запустите следующие команды toocopy hello определенного файла из один tooanother учетной записи хранилища Озера данных.

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    Например:

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > выше синтаксис Hello указывает hello файл toobe скопированный tooa папку в учетной записи хранилища Озера данных назначения hello. Средство AdlCopy создает папку, если имя hello указанная папка не существует.
   >
   >

    Появится запрос tooenter hello учетные данные для hello подписки Azure, в котором у вас есть учетная запись хранилища Озера данных. Вы увидите выходные данные примерно toohello следующие:

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. Hello следующая команда копирует все файлы из папки в папки tooa учетной записи хранилища Озера данных источника hello в конечном hello хранилища Озера данных.

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>Рекомендации по производительности

При использовании AdlCopy как отдельный инструмент, hello копирование выполняется на общих, Azure управляемые ресурсы. производительность Hello, которое может быть получено в этой среде зависит от загрузки системы и доступных ресурсов. Этот режим лучше всего применять для небольших передач, выполняемых при необходимости. Без параметров необходимо toobe настройки при использовании AdlCopy как отдельный инструмент.

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>Использовать данные toocopy AdlCopy (с помощью учетной записи аналитики Озера данных)
Можно также использовать аналитики Озера данных hello toorun AdlCopy данные toocopy заданий из хранилища Azure BLOB-объектов хранилища Озера tooData учетной записи. Этот параметр применяется обычно при toobe данных hello перемещен находится в диапазоне hello ГБ и ТБ, и требуется пропускная способность более и прогнозируемую производительность.

toouse, которую необходимо добавить свою учетную запись аналитики Озера данных с toocopy AdlCopy из хранилища BLOB-объект Azure, hello источника (больших двоичных объектов хранилища Azure) в качестве источника данных для учетной записи аналитики Озера данных. Инструкции по добавлению учетной записи аналитики Озера данных tooyour источников дополнительных данных см. в разделе [управление аналитики Озера данных учетной записи источников данных](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).

> [!NOTE]
> При копировании из учетной записи хранилища Озера данных Azure как источник hello, используя учетную запись аналитики Озера данных, не обязательно tooassociate hello хранилища Озера данных с hello учетной записи аналитики Озера данных. Hello требование tooassociate hello исходное хранилище с hello учетной записи аналитики Озера данных является только в том случае, когда источник hello является учетная запись хранилища Azure.
>
>

Выполните следующую команду toocopy из хранилища Azure blob tooa хранилища Озера данных учетной записи с помощью учетной записи аналитики Озера данных hello.

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

Например:

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

Аналогичным образом выполните следующую команду toocopy из хранилища Azure blob tooa хранилища Озера данных учетной записи с помощью учетной записи аналитики Озера данных hello:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>Рекомендации по производительности

При копировании данных в диапазоне hello терабайт, использование AdlCopy собственную учетную запись аналитики Озера данных Azure обеспечивает лучшую и более предсказуемую производительность. параметр Hello, который должен быть настроен так: hello число toouse единицы аналитика Озера данных Azure для задания копирования hello. Увеличение hello число единиц увеличит производительность hello задания копирования. Каждый toobe файл скопирован можно использовать максимальное одной единицы. Указание превышающее hello число копируемых файлов не позволяют повысить производительность.

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>Использовать AdlCopy toocopy данные с помощью сравнения с шаблоном
В этом разделе вы узнаете, как toouse AdlCopy toocopy данные из источника (в нашем примере ниже используется BLOB-объекта хранилища Azure) tooa учетной записи хранилища Озера данных назначения с помощью сравнения с шаблоном. Например вы можно использовать hello описанные ниже toocopy все файлы с расширением CSV-файл из назначение toohello hello источник больших двоичных объектов.

1. Откройте командную строку и перейдите в каталог toohello AdlCopy установки, обычно `%HOMEPATH%\Documents\adlcopy`.
2. Выполните следующие команды toocopy hello все файлы с расширением *.csv из определенного большого двоичного объекта из hello исходный контейнер tooa хранилища Озера данных:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    Например:

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>Выставление счетов
* При использовании средства AdlCopy hello как вам будет выставлен счет автономным расходы на исходящие данные для перемещения данных, если источник hello учетной записи хранилища Azure не находится в hello же регионе, как hello хранилища Озера данных.
* При использовании средства AdlCopy hello с аналитики Озера данных учетной записи, стандартная [аналитики Озера данных выставления счетов ставки](https://azure.microsoft.com/pricing/details/data-lake-analytics/) будет применяться.

## <a name="considerations-for-using-adlcopy"></a>Рекомендации по использованию AdlCopy
* AdlCopy (для версии 1.0.5) поддерживает копирование данных из источников, которые совокупно содержат тысячи файлов и папок. Тем не менее при возникновении проблем, копирование большого набора данных, можно разделить hello файлов и папок на разных вложенных папках и вместо этого использовать hello путь toothose вложенные папки в качестве источника hello.

## <a name="performance-considerations-for-using-adlcopy"></a>Рекомендации по производительности при использовании AdlCopy

AdlCopy поддерживает копирование данных, содержащих тысячи файлов и папок. Тем не менее если возникли проблемы, копирование большого набора данных, можно распространять hello файлов и папок в небольших вложенных папок. Инструмент AdlCopy был создан для выполнения задач копирования при необходимости. Если вы пытаетесь toocopy данные на регулярной основе, можно использовать [фабрики данных Azure](../data-factory/data-factory-azure-datalake-connector.md) , обеспечивающий полное управление вокруг hello операций копирования.

## <a name="release-notes"></a>Заметки о выпуске
* 1.0.13 - при копировании данных toohello учетную запись хранилища Озера данных Azure по нескольким adlcopy команды tooreenter учетные данные для каждого выполнения больше не требуется. Теперь Adlcopy будет кэшировать эти данные в нескольких запусках.

## <a name="next-steps"></a>Дальнейшие действия
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
