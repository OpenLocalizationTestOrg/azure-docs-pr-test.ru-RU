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
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="f1c28-103">Обрабатывайте и анализируйте документы JSON с использованием Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1c28-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="f1c28-104">Узнайте, как tooprocess и анализировать файлы JSON с помощью Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f1c28-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="f1c28-105">Следующий документ JSON Hello используется в учебнике hello:</span><span class="sxs-lookup"><span data-stu-id="f1c28-105">hello following JSON document is used in hello tutorial:</span></span>

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

<span data-ttu-id="f1c28-106">Hello файл можно найти в wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="f1c28-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="f1c28-107">Дополнительные сведения об использовании хранилища Azure Blob с HDInsight приведены в разделе [Использование HDFS-совместимой службы хранилища с Hadoop в HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f1c28-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="f1c28-108">Можно скопировать контейнер по умолчанию hello файл toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="f1c28-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="f1c28-109">В этом учебнике используйте консоль Hive hello.</span><span class="sxs-lookup"><span data-stu-id="f1c28-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="f1c28-110">Инструкции по открытию консоли Hive hello см. в разделе [используйте Hive в с Hadoop в HDInsight с помощью удаленного рабочего стола](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="f1c28-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="f1c28-111">Документы JSON, преобразованные в плоскую структуру</span><span class="sxs-lookup"><span data-stu-id="f1c28-111">Flatten JSON documents</span></span>
<span data-ttu-id="f1c28-112">Hello методов, перечисленных в следующем разделе hello требуют hello документа JSON в одной строке.</span><span class="sxs-lookup"><span data-stu-id="f1c28-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="f1c28-113">Поэтому необходимо свести строки tooa документа JSON hello.</span><span class="sxs-lookup"><span data-stu-id="f1c28-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="f1c28-114">Если документ JSON уже является плоским, можно пропустить этот шаг и перейти прямой toohello следующий раздел по данным анализа JSON.</span><span class="sxs-lookup"><span data-stu-id="f1c28-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="f1c28-115">Hello необработанный JSON-файл расположен в  **wasb://processjson@hditutorialdata.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="f1c28-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="f1c28-116">Hello *StudentsRaw* таблицу Hive указывает toohello необработанные несведенные документа JSON.</span><span class="sxs-lookup"><span data-stu-id="f1c28-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="f1c28-117">Hello *StudentsOneLine* таблицу Hive hello данные хранятся в hello HDInsight по умолчанию файловая система под hello */json/учащихся/* пути.</span><span class="sxs-lookup"><span data-stu-id="f1c28-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="f1c28-118">Инструкция INSERT Hello заполняет таблицу StudentOneLine hello hello в плоский формат данных JSON.</span><span class="sxs-lookup"><span data-stu-id="f1c28-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="f1c28-119">Hello инструкции SELECT должны возвращать только одну строку.</span><span class="sxs-lookup"><span data-stu-id="f1c28-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="f1c28-120">Вот hello выходных данных инструкции SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="f1c28-120">Here is hello output of hello SELECT statement:</span></span>

![Выравнивание hello документа JSON.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="f1c28-122">Анализ документов JSON в Hive</span><span class="sxs-lookup"><span data-stu-id="f1c28-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="f1c28-123">Куст предоставляет три различных механизмов toorun запросов в документах JSON:</span><span class="sxs-lookup"><span data-stu-id="f1c28-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="f1c28-124">использовать hello GET\_JSON\_ОБЪЕКТА определяемой пользователем функции (определяемой пользователем функции)</span><span class="sxs-lookup"><span data-stu-id="f1c28-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="f1c28-125">использовать hello JSON_TUPLE определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="f1c28-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="f1c28-126">пользовательские SerDe</span><span class="sxs-lookup"><span data-stu-id="f1c28-126">use custom SerDe</span></span>
* <span data-ttu-id="f1c28-127">написание собственной определяемой пользователем функции с использованием Python или других языков.</span><span class="sxs-lookup"><span data-stu-id="f1c28-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="f1c28-128">Сведения о выполнении кода Python в Hive приведена [в этой статье][hdinsight-python].</span><span class="sxs-lookup"><span data-stu-id="f1c28-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="f1c28-129">Используйте hello GET\_JSON_OBJECT определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="f1c28-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="f1c28-130">В Hive есть встроенная определяемая пользователем функция под названием [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), которая может выполнять запросы JSON во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="f1c28-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="f1c28-131">Этот метод принимает два аргумента — имя таблицы hello и имя метода, который имеет hello плоский JSON документа и hello JSON поле, которое должен toobe синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="f1c28-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="f1c28-132">Давайте рассмотрим пример toosee, как работает эта пользовательская Функция.</span><span class="sxs-lookup"><span data-stu-id="f1c28-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="f1c28-133">Получить hello имя и фамилия каждого студента</span><span class="sxs-lookup"><span data-stu-id="f1c28-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="f1c28-134">Вот hello выходных данных, при выполнении этого запроса в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="f1c28-134">Here is hello output when running this query in console window.</span></span>

![Пользовательская функция get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="f1c28-136">Существует несколько ограничений hello get-json_object определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="f1c28-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="f1c28-137">Так как для каждого поля в запросе hello требуется повторный синтаксический анализ запроса hello, влияет на производительность hello.</span><span class="sxs-lookup"><span data-stu-id="f1c28-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="f1c28-138">ПОЛУЧИТЬ\_JSON_OBJECT() возвращает hello строковое представление массива.</span><span class="sxs-lookup"><span data-stu-id="f1c28-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="f1c28-139">tooconvert этого массива куст tooa массива, у вас есть tooreplace регулярных выражений toouse hello квадратных скобок "[" и "]" и затем, вызов разбиение tooget hello массива.</span><span class="sxs-lookup"><span data-stu-id="f1c28-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="f1c28-140">Именно поэтому вики-сайте Hive hello Корпорация Майкрософт рекомендует использовать json_tuple.</span><span class="sxs-lookup"><span data-stu-id="f1c28-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="f1c28-141">Использовать hello JSON_TUPLE определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="f1c28-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="f1c28-142">Еще одна определяемая пользователем функция в Hive называется [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), и она дает лучшие результаты по сравнению с [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="f1c28-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="f1c28-143">Этот метод принимает набор ключей и строку JSON, а затем возвращает кортеж из значений, используя одну функцию.</span><span class="sxs-lookup"><span data-stu-id="f1c28-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="f1c28-144">Hello следующий запрос возвращает идентификатор студента hello и уровнем hello из документа JSON hello.</span><span class="sxs-lookup"><span data-stu-id="f1c28-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="f1c28-145">Hello выходные данные этого сценария в консоли Hive hello:</span><span class="sxs-lookup"><span data-stu-id="f1c28-145">hello output of this script in hello Hive console:</span></span>

![Пользовательская функция json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="f1c28-147">JSON\_КОРТЕЖА использует hello [боковое представление](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) синтаксиса в кусте, что позволяет json\_toocreate кортежа виртуальную таблицу, применяя hello определяемого пользователем ТИПА функции tooeach строку hello исходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="f1c28-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="f1c28-148">Сложные JSONs становятся слишком громоздким из-за hello повторяется используйте БОКОВОЕ представления.</span><span class="sxs-lookup"><span data-stu-id="f1c28-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="f1c28-149">Кроме того, JSON_TUPLE не может обрабатывать вложенные JSON.</span><span class="sxs-lookup"><span data-stu-id="f1c28-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="f1c28-150">Использование пользовательских SerDe</span><span class="sxs-lookup"><span data-stu-id="f1c28-150">Use custom SerDe</span></span>
<span data-ttu-id="f1c28-151">SerDe hello лучший выбор для синтаксического анализа вложенных документов JSON, оно позволяет toodefine hello JSON схемы и используйте hello tooparse hello документов схемы.</span><span class="sxs-lookup"><span data-stu-id="f1c28-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="f1c28-152">В этом учебнике используется один из hello популярные SerDe, которая была разработана с [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="f1c28-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="f1c28-153">**toouse hello пользовательских SerDe:**</span><span class="sxs-lookup"><span data-stu-id="f1c28-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="f1c28-154">Установите [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="f1c28-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="f1c28-155">Выберите версию Windows X64 hello hello JDK, если вы собираетесь toobe использования развертывания Windows hello HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1c28-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="f1c28-156">JDK 1.8 не будет работать с этим SerDe.</span><span class="sxs-lookup"><span data-stu-id="f1c28-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="f1c28-157">После завершения установки hello, добавьте новую переменную среды пользователя.</span><span class="sxs-lookup"><span data-stu-id="f1c28-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="f1c28-158">Откройте **Просмотр расширенных параметров системы** с экрана приветствия Windows.</span><span class="sxs-lookup"><span data-stu-id="f1c28-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="f1c28-159">Выберите **Переменные среды**.</span><span class="sxs-lookup"><span data-stu-id="f1c28-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="f1c28-160">Добавьте новый **JAVA_HOME** слишком указывает переменную среды**C:\Program Files\Java\jdk1.7.0_55** или везде, где установлен JDK.</span><span class="sxs-lookup"><span data-stu-id="f1c28-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Настройка правильных значений конфигурации для JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="f1c28-162">Установите [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="f1c28-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="f1c28-163">Добавьте путь к tooyour папке bin hello, перейдя tooControl панель--> изменить hello системные переменные для переменных среды вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f1c28-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="f1c28-164">Hello следующем снимке экрана показано, как toodo это.</span><span class="sxs-lookup"><span data-stu-id="f1c28-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![Настройка Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="f1c28-166">Клон hello проект из [Hive, JSON, SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) сайте github.</span><span class="sxs-lookup"><span data-stu-id="f1c28-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="f1c28-167">Это можно сделать, нажав на кнопку «Загрузить Zip» hello, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="f1c28-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![Клонирование hello проекта][image-hdi-hivejson-serde]

<span data-ttu-id="f1c28-169">4: go toohello папку, где загрузки пакета и затем тип «пакет mvn».</span><span class="sxs-lookup"><span data-stu-id="f1c28-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="f1c28-170">Это следует создать hello необходимые jar-файла, который затем можно скопировать на toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="f1c28-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="f1c28-171">5: go toohello целевую папку в корневой папке hello, где был загружен пакет hello.</span><span class="sxs-lookup"><span data-stu-id="f1c28-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="f1c28-172">Отправьте hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar файл toohead узлами кластера.</span><span class="sxs-lookup"><span data-stu-id="f1c28-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="f1c28-173">Я обычно поместить его в папку hive hello: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin или что-нибудь подобное.</span><span class="sxs-lookup"><span data-stu-id="f1c28-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="f1c28-174">6: в строке hive hello, введите «добавить jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar».</span><span class="sxs-lookup"><span data-stu-id="f1c28-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="f1c28-175">Так как в моем случае hello JAR-файл находится в папке C:\apps\dist\hive-0.13.x\bin hello, можно добавить непосредственно hello JAR-файл с именем hello, как показано:</span><span class="sxs-lookup"><span data-stu-id="f1c28-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Добавление проекта tooyour JAR][image-hdi-hivejson-addjar]

<span data-ttu-id="f1c28-177">Теперь все готово toouse hello SerDe toorun запросами hello документа JSON.</span><span class="sxs-lookup"><span data-stu-id="f1c28-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="f1c28-178">Hello, следующая инструкция создает таблицу с определенной схемой:</span><span class="sxs-lookup"><span data-stu-id="f1c28-178">hello following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="f1c28-179">toolist hello имя и фамилию студента hello</span><span class="sxs-lookup"><span data-stu-id="f1c28-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="f1c28-180">Ниже приведен результат hello из консоли Hive hello.</span><span class="sxs-lookup"><span data-stu-id="f1c28-180">Here is hello result from hello Hive console.</span></span>

![Запрос SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="f1c28-182">Сумма hello toocalculate оценок документа JSON hello</span><span class="sxs-lookup"><span data-stu-id="f1c28-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="f1c28-183">предшествующий запрос использует Hello [разрезать боковое представление](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) tooexpand определяемой пользователем функции hello массива оценок, чтобы для сложения.</span><span class="sxs-lookup"><span data-stu-id="f1c28-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="f1c28-184">Вот hello выходные данные консоли Hive hello.</span><span class="sxs-lookup"><span data-stu-id="f1c28-184">Here is hello output from hello Hive console.</span></span>

![Запрос SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="f1c28-186">toofind которого субъектам студент заданного оцененных более 80 точек:</span><span class="sxs-lookup"><span data-stu-id="f1c28-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="f1c28-187">Hello предыдущий запрос возвращает Hive массив, в отличие от get\_json\_объекта, который возвращает строку.</span><span class="sxs-lookup"><span data-stu-id="f1c28-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Запрос SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="f1c28-189">Если требуется tooskil имеет неправильный формат JSON, а затем, как описано в hello [вики-странице](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) из этого SerDe можно добиться, введя hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="f1c28-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="f1c28-190">Сводка</span><span class="sxs-lookup"><span data-stu-id="f1c28-190">Summary</span></span>
<span data-ttu-id="f1c28-191">В заключение hello тип оператора JSON в кусте, зависит от вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="f1c28-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="f1c28-192">Если у вас есть простой документ JSON и имеется только одно поле toolook — вы можете get Hive определяемой пользователем функции hello toouse\_json\_объекта.</span><span class="sxs-lookup"><span data-stu-id="f1c28-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="f1c28-193">Если у вас есть более одного ключа toolook, то можно использовать json_tuple.</span><span class="sxs-lookup"><span data-stu-id="f1c28-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="f1c28-194">При наличии вложенных документа следует использовать hello JSON SerDe.</span><span class="sxs-lookup"><span data-stu-id="f1c28-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1c28-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f1c28-195">Next steps</span></span>

<span data-ttu-id="f1c28-196">Другие статьи по этой теме приведены в</span><span class="sxs-lookup"><span data-stu-id="f1c28-196">For other related articles, see</span></span>

* [<span data-ttu-id="f1c28-197">Используйте Hive и HiveQL с Hadoop в HDInsight tooanalyze Apache log4j образец файла</span><span class="sxs-lookup"><span data-stu-id="f1c28-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f1c28-198">Анализ данных о задержке рейсов с помощью Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1c28-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="f1c28-199">Анализ данных Twitter с помощью Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f1c28-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* <span data-ttu-id="f1c28-200">[Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md) (Выполнение задания Apache Hive, Pig или Hadoop с помощью Azure Cosmos DB и HDInsight)</span><span class="sxs-lookup"><span data-stu-id="f1c28-200">[Run a Hadoop job using Azure Cosmos DB and HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md)</span></span>

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
