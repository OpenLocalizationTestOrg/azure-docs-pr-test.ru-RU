---
title: "aaaUse toowork Ambari представления с Hive в HDInsight (Hadoop) - Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Hive представления из вашего веб-браузера toosubmit Hive запросы. Hello Hive представление является частью hello, предоставленные Ambari веб-интерфейса пользователя с кластером HDInsight под управлением Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>Использовать hello Hive представление на Hadoop в HDInsight

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Узнайте, как toorun Hive запросов с помощью Ambari Hive представления. Ambari — это служебная программа для управления и мониторинга, предоставляемая с кластерами HDInsight под управлением Linux. Одна из функций hello, предоставленные с помощью Ambari — веб-интерфейса, можно использовать toorun запросов Hive.

> [!NOTE]
> У Ambari много разных функций, которые не рассматриваются в этом документе. Дополнительные сведения см. в разделе [кластеры HDInsight управление с помощью веб-интерфейса Ambari hello](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Предварительные требования

* Кластер HDInsight под управлением Linux. Сведения о создании кластера см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="open-hello-hive-view"></a>Откройте представление Hive hello

Вы можете Ambari представления из hello портал Azure; Выберите кластер HDInsight, а затем выберите **представления Ambari** из hello **быстрые ссылки** раздела.

![Быстрые ссылки раздел hello портала](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

Выберите из списка hello представлений hello __Hive представление__.

![Hello Hive представления, выбранного](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> При доступе к Ambari, все запрашиваемые tooauthenticate toohello сайта. Введите Здравствуйте, администратор (по умолчанию `admin`) учетной записи, имя и пароль, используемый при создании hello кластера.

Вы увидите примерно toohello страницы, следующие изображения:

![Изображение листа hello запрос для представления Hive hello](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Выполнение запроса

toorun запрос hive с помощью hello, выполнив действия из представления Hive hello.

1. Из hello __запроса__ , вставьте следующие инструкции HiveQL лист hello hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Эти операторы выполняют hello, следующие действия:

   * `DROP TABLE`— Удаляет hello таблицы и файла данных hello, в случае, если таблица hello уже существует.

   * `CREATE EXTERNAL TABLE` — создание "внешней" таблицы в Hive.
   Внешние таблицы хранить только определение таблицы hello в кусте. Hello данные остаются в исходном расположении hello.

   * `ROW FORMAT`-Способа форматирования данных hello. В этом случае hello полей в каждом журнале разделенные пробелом.

   * `STORED AS TEXTFILE LOCATION`-Hello хранения данных и хранится как текст.

   * `SELECT`-Выбор количества всех строк, где t4 столбец содержит значение hello [ошибка].

     > [!NOTE]
     > Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника. Например, с использованием процесса автоматической передачи данных или другой операции MapReduce. Удаление внешней таблицы *не* удаление данных hello, только определение таблицы hello.

    > [!IMPORTANT]
    > Оставьте hello __базы данных__ Выбор __по умолчанию__. Hello примерах в этом документе используется базой данных по умолчанию hello в HDInsight.

2. запрос toostart hello, используйте hello **Execute** кнопки ниже hello листа. Включает оранжевый и hello изменения текста слишком**остановить**.

3. После завершения запроса hello, hello **результатов** вкладка отображает hello результаты операции hello. После текста Hello представляет hello результат запроса hello.

        sev       cnt
        [ERROR]   3

    Hello **журналы** вкладке может быть используется tooview hello ведения журнала данных, созданных заданием hello.

   > [!TIP]
   > Hello **сохранить результаты** диалоговое окно раскрывающегося списка в hello верхнего левого угла hello **результаты процесса запроса** раздел позволяет вам toodownload или сохранить результаты.

4. Выберите hello первые четыре строки этого запроса, затем выберите **Execute**. Обратите внимание, что нет результатов при завершении задания hello. С помощью hello **Execute** как часть запроса hello выбран только запусков hello выбранных инструкций. В этом случае Выбор hello не были включены hello последнюю инструкцию, которая извлекает строки из таблицы hello. Если выбрать только этой строки и использовать **Execute**, вы увидите результаты ожидается hello.

5. tooadd лист, используйте hello **новый лист** кнопку внизу hello hello **редактора запросов**. В новом листе hello введите следующие инструкции HiveQL hello:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Эти операторы выполняют hello, следующие действия:

   * **CREATE TABLE IF NOT EXISTS** : создание таблицы, если она до этого не существовала. С момента hello **ВНЕШНИХ** ключевое слово не используется, создается внутренней таблицы. Внутренняя таблица хранится в хранилище данных Hive hello и полностью управляются Hive. В отличие от внешних таблиц при удалении внутренней таблицы удаляются hello базовые данные.

   * **ORC ХРАНИМОЙ AS** -хранит данные hello в оптимизированные строк по столбцам (формат ORC.). Это высокооптимизированный и эффективный формат для хранения данных Hive.

   * **INSERT OVERWRITE ... ВЫБЕРИТЕ** -выбирает строки из hello **log4jLogs** таблицы, которые содержат `[ERROR]`, и затем вставляет hello данных в hello **журналы ошибок** таблицы.

     Используйте hello **Execute** кнопку toorun этот запрос. Hello **результатов** вкладка не содержит все сведения, когда hello запрос возвращает 0 строк. состояние Hello должно отображаться как **успешно** после завершения выполнения запроса hello.

### <a name="visual-explain"></a>Визуальное объяснение

toodisplay визуализации плана запроса hello, выберите hello **Visual объяснить** под hello листа.

Hello **Visual объяснить** представление hello запроса могут быть полезны для понимания hello потока сложных запросов. Текстовый эквивалент этого представления можно просмотреть с помощью hello **объяснение** кнопку в hello редактора запросов.

### <a name="tez-ui"></a>Пользовательский интерфейс Tez

toodisplay hello Tez пользовательского интерфейса для запроса hello, выберите hello **Tez** под hello листа.

> [!IMPORTANT]
> Tez является tooresolve не используется все запросы. Многие запросы можно разрешить и без применения Tez. 

Если Tez запроса используется tooresolve hello, отображается hello расширенный ациклического графа (DAG). Tooview hello DAG для запросов уже выполнялись в прошлом hello, или отладке hello Tez процесса, используйте hello [Tez представление](hdinsight-debug-ambari-tez-view.md) вместо него.

## <a name="view-job-history"></a>Просмотр журнала заданий

Hello __заданий__ вкладка отображается История запросов Hive.

![Изображение hello журнал заданий](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Таблицы базы данных

Можно использовать hello __таблиц__ вкладке toowork с таблицами в базе данных Hive.

![Изображение вкладку таблицы hello](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Сохраненные запросы

На вкладке запросов hello при необходимости можно сохранить запросы. После сохранения можно повторно использовать запрос hello из hello __сохраненные запросы__ вкладки.

![Изображение вкладки "Сохраненные запросы"](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Определяемые пользователем функции

Инфраструктуру Hive также можно расширить с помощью определяемых пользователем функций (UDF). Определяемая пользователем Функция позволяет tooimplement функциональность или логику, которая не легко моделируется в HiveQL.

Hello UDF вкладку вверху hello hello Hive представление позволяет toodeclare и сохраните набор определяемых пользователем функций. Эти пользовательские функции могут использоваться с hello **редактора запросов**.

![Изображение вкладки "Определяемая пользователем функция"](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

После добавления определяемой пользователем функции toohello представление Hive, **Вставка определяемых пользователем функций** появляется кнопка внизу hello hello **редактора запросов**. При выборе этой записи отображаются раскрывающиеся hello определяемые пользователем функции, определенные в hello Hive представления. При выборе определяемой пользователем функции добавляется hello HiveQL инструкций tooyour запроса tooenable определяемой пользователем функции.

Например, если вы определили определяемой пользователем функции с hello следующие свойства:

* имя ресурса — myudfs;

* путь к ресурсу — /myudfs.jar;

* имя определяемой пользователем функции — myawesomeudf;

* имя класса определяемой пользователем функции — com.myudfs.Awesome.

С помощью hello **Вставка определяемых пользователем функций** кнопки отображаются записи с именем **myudfs**, с другим раскрывающегося списка для каждой определяемой пользователем функции определен для этого ресурса. В нашем примере это функция **myawesomeudf**. При выборе этой записи добавляет hello после начала toohello hello запроса:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

Затем можно использовать hello определяемой пользователем функции в запросе. Например, `SELECT myawesomeudf(name) FROM people;`.

Дополнительные сведения об использовании определяемых пользователем функций с Hive в HDInsight см. в разделе hello следующие документы:

* [Использование Python с Hive и Pig в HDInsight](hdinsight-python.md)
* [Как tooadd пользовательские tooHDInsight Hive определяемой пользователем функции](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Параметры Hive

Параметры могут быть различные параметры Hive используется toochange. Например изменение hello подсистема выполнения для куста tooMapReduce Tez (по умолчанию hello).

## <a id="nextsteps"></a>Дальнейшие действия

Общая информация о Hive в HDInsight.

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight.

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)
