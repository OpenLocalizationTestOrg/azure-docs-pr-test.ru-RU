---
title: "aaaCreate Hive таблиц и загрузки данных из хранилища больших двоичных объектов | Документы Microsoft"
description: "Создание таблиц Hive и загружают данные в таблицы toohive BLOB-объектов"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Создание таблиц Hive и загрузка данных из хранилища BLOB-объектов Azure
В этой статье рассматриваются общие запросы Hive, которые создают таблицы Hive и загружают данные из хранилищ BLOB-объектов Azure. Некоторые рекомендации также предоставляется для секционирования таблицы Hive и об использовании производительность запросов форматирования tooimprove hello оптимизированными строк по столбцам (ORC.).

Это **меню** связывает tootopics, описывающие, каким образом данные tooingest в целевых средах, где hello данные могут храниться и обрабатываться во время hello процесса обработки и анализа данных Team (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы:

* Создали учетную запись хранения Azure. Инструкции см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).
* Подготовить настроенные кластеру с hello службы HDInsight.  Инструкции см. в статье [Настройка кластеров Azure HDInsight Hadoop для процесса обработки и анализа данных группы](machine-learning-data-science-customize-hadoop-cluster.md).
* Кластер toohello включен удаленный доступ, зарегистрированы и открыть консоль командной строки Hadoop hello. При необходимости инструкции в разделе [доступа hello головного узла кластера Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Отправка больших двоичных объектов хранилища данных tooAzure
Если вы создали виртуальную машину Azure, следуя инструкциям hello в [Настройка виртуальной машины Azure для расширенной аналитики](machine-learning-data-science-setup-virtual-machine.md), этот файл сценария должно было загруженный toohello *C:\\ Пользователи\\\<имя пользователя\>\\документов\\сценарии обработки и анализа данных* каталог на виртуальной машине hello. Эти запросы Hive нужны только подключаемого модуля в собственных данных схемы и конфигурации хранилища больших двоичных объектов Azure в toobe соответствующие поля hello готова к отправке.

Мы предполагаем, что данные hello для куста таблиц находится в **несжатые** табличном формате, а также что hello данных была отправленного toohello по умолчанию (или дополнительных tooan) контейнера учетной записи хранения hello hello кластере Hadoop.

Если требуется, чтобы toopractice на hello **NYC такси обработки данных**, необходимо:

* **Загрузить** hello 24 [NYC такси обработки данных](http://www.andresmh.com/nyctaxitrips) файлов (12 Trip файлы и файлы 12 тариф авиакомпании),
* **распаковать** все CSV-файлы; а затем
* **Отправка** их toohello по умолчанию или соответствующего контейнера hello учетной записи хранилища Azure, созданные hello процедуры, описанной в hello [кластеры настройки Azure HDInsight Hadoop для Advanced Analytics процесса и технологии ](machine-learning-data-science-customize-hadoop-cluster.md) раздела. Hello процесса tooupload hello .csv файлы toohello контейнер по умолчанию hello учетной записи хранения можно найти в данном [страницы](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>Каким образом запросы Hive toosubmit
Инструменты для отправки запросов Hive:

1. [Отправка запросов Hive через командную строку Hadoop в головной узел кластера Hadoop](#headnode)
2. [Отправки запросов Hive с hello редактор Hive](#hive-editor)
3. [Отправка запросов Hive с помощью команд PowerShell Azure](#ps)

Запросы Hive похожи на SQL. Если вы знакомы с SQL, может оказаться hello [Hive для Памятка пользователей SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) полезно.

При отправке запроса Hive, можно также управлять назначением hello hello вывод запросов Hive будь hello экрана или tooa локальный файл на головном узле hello или tooan BLOB-объектов Azure.

### <a name="headnode"></a> 1. Отправка запросов Hive через командную строку Hadoop в головной узел кластера Hadoop
Если hello Hive запроса является сложным, передается непосредственно в hello головного узла кластера Hadoop hello обычно приводит toofaster, поворачивать, чем отправка его с помощью редактора, Hive или скриптов Azure PowerShell.

Войдите в toohello головного узла кластера Hadoop hello, откройте hello Hadoop командной строки на рабочем столе hello hello головного узла и введите команду `cd %hive_home%\bin`.

В командной строки Hadoop hello имеется запросов Hive toosubmit тремя способами:

* напрямую;
* с помощью HQL-файлов;
* с hello Hive командной консоли

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Отправка запросов Hive непосредственно из командной строки Hadoop
Можно выполнить команду, например `hive -e "<your hive query>;` toosubmit простых запросов Hive непосредственно в Hadoop командной строки. Ниже приведен пример, где поле контуров hello красный hello команду, которая отправляет запрос Hive hello и hello зеленой рамке контуров hello вывод запроса Hive hello.

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Отправка запросов Hive в HQL-файлах
Если запрос Hive hello более сложен и имеет несколько строк, редактирование запросов в командной строке или куст командной консоли не имеет смысла. Альтернативой является toouse текстового редактора в головном узле hello hello Hadoop кластера toosave hello запросов Hive в файле .hql в локальном каталоге hello головного узла. Затем запрос Hive hello в файле .hql hello могут передаваться с помощью hello `-f` аргумент, как показано ниже:

    hive -f "<path toohello .hql file>"

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Отменить вывод состояния хода выполнения запросов Hive на экран**

По умолчанию после отправки запроса Hive в Hadoop командной строки hello ход выполнения задания Map/Reduce hello будет выведен на экран. toosuppress Здравствуйте печати экран хода выполнения заданий Map/Reduce hello, можно использовать аргумент `-S` («S» в верхнем регистре) в hello командной строки следующим образом:

    hive -S -f "<path toohello .hql file>"
.    hive -S -e "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Отправка запросов Hive в командной консоли Hive
Можно также сначала ввести hello Hive командной консоли, выполнив команду `hive` в Hadoop командной строки и отправки запросов Hive в командной консоли Hive. Ниже приведен пример. В этом примере hello две Красные прямоугольники выделения hello команды, используемые tooenter hello командной консоли Hive и hello запроса Hive, отправленного в командной консоли Hive, соответственно. поле Hello зеленый выделяются hello выходные данные запроса Hive hello.

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

Hello предыдущих примерах непосредственно выходные результаты запроса Hive hello на экране. Можно также написать hello вывода tooa локальный файл на головном узле hello, или tooan BLOB-объектов Azure. Затем можно использовать другие средства toofurther анализ вывода hello запросов Hive.

**Выходного файла локального tooa результаты запроса Hive.**
toooutput Hive запроса результаты tooa локальный каталог на головном узле hello, имеется запрос Hive toosubmit hello в hello Hadoop командной строки следующим образом:

    hive -e "<hive query>" > <local path in hello head node>

В следующем примере hello, выходные данные запроса Hive hello записывается в файл `hivequeryoutput.txt` в каталоге `C:\apps\temp`.

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Результаты запроса tooan BLOB-объектов Azure для выходных данных Hive**

Кроме того, может выводить результаты запроса tooan BLOB-объектов Azure, в контейнере по умолчанию hello hello кластера Hadoop для hello Hive. Hello запрос Hive для это выглядит следующим образом:

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

В следующем примере hello, каталог больших двоичных объектов tooa записываются hello выходные данные запроса Hive `queryoutputdir` внутри контейнера по умолчанию hello hello кластера Hadoop. Здесь требуется только имя папки hello tooprovide без hello имя большого двоичного объекта. Если указать имя каталога и имя большого двоичного объекта, появится следующее сообщение об ошибке: `wasb:///queryoutputdir/queryoutput.txt`.

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

При открытии hello контейнер по умолчанию для кластера Hadoop hello, с помощью обозревателя хранилищ Azure, как показано в следующий рисунок hello видно hello выходных данных запроса Hive hello. Можно применить hello фильтра (выделенная красный прямоугольник) tooonly получить hello большой двоичный объект с указанным буквы в именах.

![Создание рабочей области](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Отправки запросов Hive с hello редактор Hive
Можно также использовать hello консоль запросов (редактор куста реестра), введя URL-адрес формы hello *https://&#60; Имя кластера Hadoop >.azurehdinsight.net/Home/HiveEditor* в веб-браузер. Вы должны быть зарегистрированы hello см. в разделе эту консоль, и поэтому необходимы полномочия кластера Hadoop.

### <a name="ps"></a> 3. Отправка запросов Hive с помощью команд PowerShell Azure
Можно также использовать запросы Hive toosubmit PowerShell. Инструкции см. в статье [Отправка заданий Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Создание базы данных и таблиц Hive
Hello запросов Hive общих в hello [репозитории GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) и могут быть загружены из него.

Ниже приведен запрос Hive hello, создающий таблицу Hive.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Ниже приведены описания hello необходимые tooplug в hello поля и другие элементы конфигурации.

* **&#60; имя базы данных >**: имя базы данных hello, что требуется toocreate hello. Если необходимо просто база данных по умолчанию hello toouse hello запроса *создать базу данных...*  может быть опущено.
* **&#60; имя таблицы >**: hello имя hello таблицы, которая будет toocreate в указанной базе данных hello. Если требуется база данных по умолчанию hello toouse hello таблицы можно непосредственно ссылаться по *&#60; имя таблицы >* без &#60; имя базы данных >.
* **&#60; разделитель >**: hello разделителя, разделяющий поля в файл toobe hello данные отправлены toohello таблицу Hive.
* **&#60; разделитель строк >**: hello разделителя, который разделяет строки в файле данных hello.
* **&#60; место хранения >**: hello расположение хранилища Azure toosave данные hello Hive таблиц. Если вы не укажете *РАСПОЛОЖЕНИЕ &#60; место хранения >*, hello базы данных и hello таблицы хранятся в *hive или хранилище или* каталог в контейнере по умолчанию hello hello Hive кластера по умолчанию. Если требуется, чтобы место хранения toospecify hello, место хранения hello имеет toobe внутри контейнера по умолчанию hello hello базы данных и таблиц. Это расположение имеет называется контейнер по умолчанию toohello относительное расположение кластера hello в формате hello toobe *"wasb: / / / &#60; каталог 1 > /"* или *"wasb: / / / &#60; каталог 1 > и &#60; каталог 2 > / "*и т. д. После выполнения запроса hello hello относительный каталоги создаются внутри контейнера по умолчанию hello.
* **TBLPROPERTIES("SKIP.Header.Line.Count"="1")**: Если hello файла данных строки заголовка, у вас есть tooadd это свойство **в конце hello** из hello *создать таблицу* запроса. В противном случае — как таблицу записей toohello загружаются hello заголовков строк. Если файл данных hello не имеет строку заголовка, эта конфигурация может быть опущено в запросе hello.

## <a name="load-data"></a>Загрузка данных tooHive таблиц
Ниже приведен запрос Hive hello, которая загружает данные в таблицу Hive.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; данные tooblob путь >**: hello в случае таблицу Hive toohello toobe загружен файл hello BLOB-объектов в контейнере по умолчанию hello hello кластера HDInsight Hadoop *&#60; данные tooblob путь >* должен иметь формат hello *"wasb: / / / &#60; каталог, в этом контейнере > и &#60; имя файла большого двоичного объекта >"*. файл Hello BLOB-объекта также могут быть в дополнительного контейнера hello кластера HDInsight Hadoop. В этом случае *&#60; данные tooblob путь >* должен иметь формат hello *"wasb: / / &#60; имя контейнера > @&#60; имя учетной записи хранения >.blob.core.windows.net/ &#60; имя файла большого двоичного объекта >"*.

  > [!NOTE]
  > Hello таблицы tooHive toobe отправки данных большого двоичного объекта имеет toobe по умолчанию hello или дополнительного контейнера hello учетной записи хранилища для кластера Hadoop hello. В противном случае hello *загрузки данных* запрос завершается ошибкой, обнаруживших, что нет доступа к данным hello.
  >
  >

## <a name="partition-orc"></a>Дополнительные разделы: секционированные таблицы и хранение данных Hive в формате ORC
Если hello данных имеет большой размер, секционирование таблицы hello предпочтительнее для запросов, которые не требуют tooscan несколько секций таблицы hello. Для экземпляра это данные журнала hello разумного toopartition веб-сайта по дате.

В дополнение toopartitioning Hive таблиц, а также данных Hive полезным toostore hello в hello оптимизированными строк по столбцам (формат ORC.). Дополнительную информацию об использовании формата ORC см. в <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">разделе о том, как использование ORC-файлов повышает производительность при чтении, записи и обработке данных Hive</a>.

### <a name="partitioned-table"></a>Секционированная таблица
Ниже приведен запрос Hive hello, Создание секционированной таблицы и загружает в нее данные.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

При запросах к секционированным таблицам, рекомендуется tooadd hello секции условие в hello **начало** из hello `where` предложения, как это повышает эффективность поиска значительно hello.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Хранение данных Hive в формате ORC
Нельзя загрузить напрямую данных из хранилища BLOB-данных в таблицы Hive, которые хранятся в формате ORC hello. Ниже приведены шаги, hello, hello требуются tootake tooload данные из Azure BLOB-объектов tooHive таблиц, сохраненных в формате ORC.

Создайте внешнюю таблицу **ХРАНЯТСЯ как текстовый ФАЙЛ** и загрузить данные из таблицы toohello хранилища больших двоичных объектов.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Создание внутренней таблицы с hello одной схеме с внешней таблицы hello в шаге 1, с hello же разделитель полей и сохранить hello данных Hive в формат ORC hello.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

Выбор данных из внешней таблицы hello в шаге 1 и вставки в таблицу ORC hello

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Если текстовый ФАЙЛ таблицы hello *&#60; имя базы данных >. &#60; имя таблицы внешних текстовый файл >* содержит разделы, в ШАГЕ 3 hello `SELECT * FROM <database name>.<external textfile table name>` команда выбирает hello секции переменной как поле в hello возвращаемого набора данных. Вставка в hello *&#60; имя базы данных >. &#60; имя таблицы ORC >* завершается сбоем с момента *&#60; имя базы данных >. &#60; имя таблицы ORC >* имеет переменную hello секционирования как поле в схеме таблицы hello. В этом случае необходимо toospecifically выберите hello поля toobe вставлены слишком*&#60; имя базы данных >. &#60; имя таблицы ORC >* следующим образом:
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

Это безопасно toodrop hello *&#60; имя таблицы внешних текстовый файл >* при приветствия при следующем запросе после всех данных с помощью была вставлена в *&#60; имя базы данных >. &#60; имя таблицы ORC >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

После выполнения этой процедуры, должна быть представлена таблица с данными в toouse готовности формат ORC hello.  
