---
title: "aaaAnalyze и процесс JSON документы с Hive в HDInsight | Документы Microsoft"
description: "Узнайте, как toouse JSON документы и анализировать их с помощью Hive в HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>Обрабатывайте и анализируйте документы JSON с использованием Hive в HDInsight

Узнайте, как tooprocess и анализировать файлы JSON с помощью Hive в HDInsight. Следующий документ JSON Hello используется в учебнике hello:

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

Hello файл можно найти в wasb://processjson@hditutorialdata.blob.core.windows.net/. Дополнительные сведения об использовании хранилища Azure Blob с HDInsight приведены в разделе [Использование HDFS-совместимой службы хранилища с Hadoop в HDInsight](hdinsight-hadoop-use-blob-storage.md). Можно скопировать контейнер по умолчанию hello файл toohello кластера.

В этом учебнике используйте консоль Hive hello.  Инструкции по открытию консоли Hive hello см. в разделе [используйте Hive в с Hadoop в HDInsight с помощью удаленного рабочего стола](hdinsight-hadoop-use-hive-remote-desktop.md).

## <a name="flatten-json-documents"></a>Документы JSON, преобразованные в плоскую структуру
Hello методов, перечисленных в следующем разделе hello требуют hello документа JSON в одной строке. Поэтому необходимо свести строки tooa документа JSON hello. Если документ JSON уже является плоским, можно пропустить этот шаг и перейти прямой toohello следующий раздел по данным анализа JSON.

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

Hello необработанный JSON-файл расположен в  **wasb://processjson@hditutorialdata.blob.core.windows.net/** . Hello *StudentsRaw* таблицу Hive указывает toohello необработанные несведенные документа JSON.

Hello *StudentsOneLine* таблицу Hive hello данные хранятся в hello HDInsight по умолчанию файловая система под hello */json/учащихся/* пути.

Инструкция INSERT Hello заполняет таблицу StudentOneLine hello hello в плоский формат данных JSON.

Hello инструкции SELECT должны возвращать только одну строку.

Вот hello выходных данных инструкции SELECT hello.

![Выравнивание hello документа JSON.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>Анализ документов JSON в Hive
Куст предоставляет три различных механизмов toorun запросов в документах JSON:

* использовать hello GET\_JSON\_ОБЪЕКТА определяемой пользователем функции (определяемой пользователем функции)
* использовать hello JSON_TUPLE определяемой пользователем функции
* пользовательские SerDe
* написание собственной определяемой пользователем функции с использованием Python или других языков. Сведения о выполнении кода Python в Hive приведена [в этой статье][hdinsight-python].

### <a name="use-hello-getjsonobject-udf"></a>Используйте hello GET\_JSON_OBJECT определяемой пользователем функции
В Hive есть встроенная определяемая пользователем функция под названием [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), которая может выполнять запросы JSON во время выполнения. Этот метод принимает два аргумента — имя таблицы hello и имя метода, который имеет hello плоский JSON документа и hello JSON поле, которое должен toobe синтаксического анализа. Давайте рассмотрим пример toosee, как работает эта пользовательская Функция.

Получить hello имя и фамилия каждого студента

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

Вот hello выходных данных, при выполнении этого запроса в окне консоли.

![Пользовательская функция get_json_object][image-hdi-hivejson-getjsonobject]

Существует несколько ограничений hello get-json_object определяемой пользователем функции.

* Так как для каждого поля в запросе hello требуется повторный синтаксический анализ запроса hello, влияет на производительность hello.
* ПОЛУЧИТЬ\_JSON_OBJECT() возвращает hello строковое представление массива. tooconvert этого массива куст tooa массива, у вас есть tooreplace регулярных выражений toouse hello квадратных скобок "[" и "]" и затем, вызов разбиение tooget hello массива.

Именно поэтому вики-сайте Hive hello Корпорация Майкрософт рекомендует использовать json_tuple.  

### <a name="use-hello-jsontuple-udf"></a>Использовать hello JSON_TUPLE определяемой пользователем функции
Еще одна определяемая пользователем функция в Hive называется [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), и она дает лучшие результаты по сравнению с [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object). Этот метод принимает набор ключей и строку JSON, а затем возвращает кортеж из значений, используя одну функцию. Hello следующий запрос возвращает идентификатор студента hello и уровнем hello из документа JSON hello.

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

Hello выходные данные этого сценария в консоли Hive hello:

![Пользовательская функция json_tuple][image-hdi-hivejson-jsontuple]

JSON\_КОРТЕЖА использует hello [боковое представление](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) синтаксиса в кусте, что позволяет json\_toocreate кортежа виртуальную таблицу, применяя hello определяемого пользователем ТИПА функции tooeach строку hello исходной таблицы.  Сложные JSONs становятся слишком громоздким из-за hello повторяется используйте БОКОВОЕ представления. Кроме того, JSON_TUPLE не может обрабатывать вложенные JSON.

### <a name="use-custom-serde"></a>Использование пользовательских SerDe
SerDe hello лучший выбор для синтаксического анализа вложенных документов JSON, оно позволяет toodefine hello JSON схемы и используйте hello tooparse hello документов схемы. В этом учебнике используется один из hello популярные SerDe, которая была разработана с [Roberto Congiu](https://github.com/rcongiu).

**toouse hello пользовательских SerDe:**

1. Установите [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR). Выберите версию Windows X64 hello hello JDK, если вы собираетесь toobe использования развертывания Windows hello HDInsight
   
   > [!WARNING]
   > JDK 1.8 не будет работать с этим SerDe.
   > 
   > 
   
    После завершения установки hello, добавьте новую переменную среды пользователя.
   
   1. Откройте **Просмотр расширенных параметров системы** с экрана приветствия Windows.
   2. Выберите **Переменные среды**.  
   3. Добавьте новый **JAVA_HOME** слишком указывает переменную среды**C:\Program Files\Java\jdk1.7.0_55** или везде, где установлен JDK.
      
      ![Настройка правильных значений конфигурации для JDK][image-hdi-hivejson-jdk]
2. Установите [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Добавьте путь к tooyour папке bin hello, перейдя tooControl панель--> изменить hello системные переменные для переменных среды вашей учетной записи. Hello следующем снимке экрана показано, как toodo это.
   
    ![Настройка Maven][image-hdi-hivejson-maven]
3. Клон hello проект из [Hive, JSON, SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) сайте github. Это можно сделать, нажав на кнопку «Загрузить Zip» hello, как показано на следующий снимок экрана приветствия.
   
    ![Клонирование hello проекта][image-hdi-hivejson-serde]

4: go toohello папку, где загрузки пакета и затем тип «пакет mvn». Это следует создать hello необходимые jar-файла, который затем можно скопировать на toohello кластера.

5: go toohello целевую папку в корневой папке hello, где был загружен пакет hello. Отправьте hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar файл toohead узлами кластера. Я обычно поместить его в папку hive hello: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin или что-нибудь подобное.

6: в строке hive hello, введите «добавить jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar». Так как в моем случае hello JAR-файл находится в папке C:\apps\dist\hive-0.13.x\bin hello, можно добавить непосредственно hello JAR-файл с именем hello, как показано:

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Добавление проекта tooyour JAR][image-hdi-hivejson-addjar]

Теперь все готово toouse hello SerDe toorun запросами hello документа JSON.

Hello, следующая инструкция создает таблицу с определенной схемой:

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

toolist hello имя и фамилию студента hello

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Ниже приведен результат hello из консоли Hive hello.

![Запрос SerDe 1][image-hdi-hivejson-serde_query1]

Сумма hello toocalculate оценок документа JSON hello

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

предшествующий запрос использует Hello [разрезать боковое представление](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) tooexpand определяемой пользователем функции hello массива оценок, чтобы для сложения.

Вот hello выходные данные консоли Hive hello.

![Запрос SerDe 2][image-hdi-hivejson-serde_query2]

toofind которого субъектам студент заданного оцененных более 80 точек:

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

Hello предыдущий запрос возвращает Hive массив, в отличие от get\_json\_объекта, который возвращает строку.

![Запрос SerDe 3][image-hdi-hivejson-serde_query3]

Если требуется tooskil имеет неправильный формат JSON, а затем, как описано в hello [вики-странице](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) из этого SerDe можно добиться, введя hello, следующий код:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>Сводка
В заключение hello тип оператора JSON в кусте, зависит от вашего сценария. Если у вас есть простой документ JSON и имеется только одно поле toolook — вы можете get Hive определяемой пользователем функции hello toouse\_json\_объекта. Если у вас есть более одного ключа toolook, то можно использовать json_tuple. При наличии вложенных документа следует использовать hello JSON SerDe.

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи по этой теме приведены в

* [Используйте Hive и HiveQL с Hadoop в HDInsight tooanalyze Apache log4j образец файла](hdinsight-use-hive.md)
* [Анализ данных о задержке рейсов с помощью Hadoop в HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Анализ данных Twitter с помощью Hive в HDInsight](hdinsight-analyze-twitter-data.md)
* [Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md) (Выполнение задания Apache Hive, Pig или Hadoop с помощью Azure Cosmos DB и HDInsight)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
