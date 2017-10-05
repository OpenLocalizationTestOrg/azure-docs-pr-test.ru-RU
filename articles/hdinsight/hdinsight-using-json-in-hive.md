---
title: "Анализ и обработка документов JSON с помощью Hive в HDInsight | Документация Майкрософт"
description: "Узнайте, как использовать документы JSON и анализировать их с помощью Hive в HDInsight."
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
ms.openlocfilehash: bd136afebeceb0cd9c24cfc5f15601caa80a755e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="641ec-103">Обрабатывайте и анализируйте документы JSON с использованием Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="641ec-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="641ec-104">Узнайте, как обрабатывать и анализировать файлы JSON с помощью Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="641ec-104">Learn how to process and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="641ec-105">В этом руководстве используется следующий документ JSON:</span><span class="sxs-lookup"><span data-stu-id="641ec-105">The following JSON document is used in the tutorial:</span></span>

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

<span data-ttu-id="641ec-106">Файл можно найти в wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="641ec-106">The file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="641ec-107">Дополнительные сведения об использовании хранилища Azure Blob с HDInsight приведены в разделе [Использование HDFS-совместимой службы хранилища с Hadoop в HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="641ec-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="641ec-108">Вы можете скопировать файл в контейнер по умолчанию кластера.</span><span class="sxs-lookup"><span data-stu-id="641ec-108">You can copy the file to the default container of your cluster.</span></span>

<span data-ttu-id="641ec-109">В этом руководстве используется консоль Hive.</span><span class="sxs-lookup"><span data-stu-id="641ec-109">In this tutorial, you use the Hive console.</span></span>  <span data-ttu-id="641ec-110">Инструкции по открытию консоли Hive приведены в разделе [Использование Hive с Hadoop в HDInsight с помощью удаленного рабочего стола](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="641ec-110">For instructions of opening the Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="641ec-111">Документы JSON, преобразованные в плоскую структуру</span><span class="sxs-lookup"><span data-stu-id="641ec-111">Flatten JSON documents</span></span>
<span data-ttu-id="641ec-112">Методы, перечисленные в следующем разделе требуют, чтобы документ JSON содержал одну строку.</span><span class="sxs-lookup"><span data-stu-id="641ec-112">The methods listed in the next section require the JSON document in a single row.</span></span> <span data-ttu-id="641ec-113">Поэтому необходимо преобразовать документ JSON в строку.</span><span class="sxs-lookup"><span data-stu-id="641ec-113">So you must flatten the JSON document to a string.</span></span> <span data-ttu-id="641ec-114">Если документ JSON уже преобразован, можно пропустить этот шаг и сразу перейти к следующему разделу, посвященному анализу данных JSON.</span><span class="sxs-lookup"><span data-stu-id="641ec-114">If your JSON document is already flattened, you can skip this step and go straight to the next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="641ec-115">Необработанный файл JSON находится в **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="641ec-115">The raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="641ec-116">Таблица Hive *StudentsRaw* указывает на необработанный документ JSON.</span><span class="sxs-lookup"><span data-stu-id="641ec-116">The *StudentsRaw* Hive table points to the raw unflattened JSON document.</span></span>

<span data-ttu-id="641ec-117">Таблица Hive *StudentsOneLine* сохраняет данные в файловой системе по умолчанию HDInsight в каталоге */json/students/*.</span><span class="sxs-lookup"><span data-stu-id="641ec-117">The *StudentsOneLine* Hive table stores the data in the HDInsight default file system under the */json/students/* path.</span></span>

<span data-ttu-id="641ec-118">Запрос INSERT заполняет таблицу StudentOneLine плоскими данными JSON.</span><span class="sxs-lookup"><span data-stu-id="641ec-118">The INSERT statement populates the StudentOneLine table with the flattened JSON data.</span></span>

<span data-ttu-id="641ec-119">Запрос SELECT должен возвращать всего одну строку.</span><span class="sxs-lookup"><span data-stu-id="641ec-119">The SELECT statement shall only return one row.</span></span>

<span data-ttu-id="641ec-120">Вот результат выполнения запроса SELECT:</span><span class="sxs-lookup"><span data-stu-id="641ec-120">Here is the output of the SELECT statement:</span></span>

![Преобразование документа JSON в плоскую структуру][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="641ec-122">Анализ документов JSON в Hive</span><span class="sxs-lookup"><span data-stu-id="641ec-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="641ec-123">Hive предоставляет три различных механизма для выполнения запросов к документам JSON:</span><span class="sxs-lookup"><span data-stu-id="641ec-123">Hive provides three different mechanisms to run queries on JSON documents:</span></span>

* <span data-ttu-id="641ec-124">определяемая пользователем функция GET\_JSON\_OBJECT;</span><span class="sxs-lookup"><span data-stu-id="641ec-124">use the GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="641ec-125">определяемая пользователем функция JSON_TUPLE</span><span class="sxs-lookup"><span data-stu-id="641ec-125">use the JSON_TUPLE UDF</span></span>
* <span data-ttu-id="641ec-126">пользовательские SerDe</span><span class="sxs-lookup"><span data-stu-id="641ec-126">use custom SerDe</span></span>
* <span data-ttu-id="641ec-127">написание собственной определяемой пользователем функции с использованием Python или других языков.</span><span class="sxs-lookup"><span data-stu-id="641ec-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="641ec-128">Сведения о выполнении кода Python в Hive приведена [в этой статье][hdinsight-python].</span><span class="sxs-lookup"><span data-stu-id="641ec-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-the-getjsonobject-udf"></a><span data-ttu-id="641ec-129">Использование определяемой пользователем функции GET\_JSON_OBJECT</span><span class="sxs-lookup"><span data-stu-id="641ec-129">Use the GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="641ec-130">В Hive есть встроенная определяемая пользователем функция под названием [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), которая может выполнять запросы JSON во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="641ec-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="641ec-131">Этот метод принимает два аргумента — имя таблицы, которая содержит плоский документ JSON, и поле JSON, которое требуется проанализировать.</span><span class="sxs-lookup"><span data-stu-id="641ec-131">This method takes two arguments – the table name and method name, which has the flattened JSON document and the JSON field that needs to be parsed.</span></span> <span data-ttu-id="641ec-132">Рассмотрим на примере, как работает эта пользовательская функция.</span><span class="sxs-lookup"><span data-stu-id="641ec-132">Let’s look at an example to see how this UDF works.</span></span>

<span data-ttu-id="641ec-133">Получение имени и фамилии каждого студента</span><span class="sxs-lookup"><span data-stu-id="641ec-133">Get the first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="641ec-134">Вот какие результаты дает выполнение этого запроса в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="641ec-134">Here is the output when running this query in console window.</span></span>

![Пользовательская функция get_json_object][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="641ec-136">У определяемой пользователем функции get-json_object есть несколько ограничений.</span><span class="sxs-lookup"><span data-stu-id="641ec-136">There are a few limitations of the get-json_object UDF.</span></span>

* <span data-ttu-id="641ec-137">Так как каждое поле в запросе требует повторного синтаксического анализа запроса, это влияет на производительность.</span><span class="sxs-lookup"><span data-stu-id="641ec-137">Because each field in the query requires reparsing the query, it affects the performance.</span></span>
* <span data-ttu-id="641ec-138">GET\_JSON_OBJECT() возвращает строковое представление массива.</span><span class="sxs-lookup"><span data-stu-id="641ec-138">GET\_JSON_OBJECT() returns the string representation of an array.</span></span> <span data-ttu-id="641ec-139">Для преобразования этого массива в массив Hive необходимо использовать регулярные выражения для замены квадратных скобок "[" и "]", а затем также выполнить разбиение для получения массива.</span><span class="sxs-lookup"><span data-stu-id="641ec-139">To convert this array to a Hive array, you have to use regular expressions to replace the square brackets ‘[‘ and ‘]’ and then also call split to get the array.</span></span>

<span data-ttu-id="641ec-140">Именно поэтому в вики Hive рекомендуется использовать json_tuple.</span><span class="sxs-lookup"><span data-stu-id="641ec-140">This is why the Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-the-jsontuple-udf"></a><span data-ttu-id="641ec-141">Использование определяемой пользователем функции JSON_TUPLE</span><span class="sxs-lookup"><span data-stu-id="641ec-141">Use the JSON_TUPLE UDF</span></span>
<span data-ttu-id="641ec-142">Еще одна определяемая пользователем функция в Hive называется [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), и она дает лучшие результаты по сравнению с [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="641ec-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="641ec-143">Этот метод принимает набор ключей и строку JSON, а затем возвращает кортеж из значений, используя одну функцию.</span><span class="sxs-lookup"><span data-stu-id="641ec-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="641ec-144">Следующий запрос возвращает идентификатор студента и его оценку из документа JSON.</span><span class="sxs-lookup"><span data-stu-id="641ec-144">The following query returns the student id and the grade from the JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="641ec-145">Выходные данные этого сценария в консоли Hive:</span><span class="sxs-lookup"><span data-stu-id="641ec-145">The output of this script in the Hive console:</span></span>

![Пользовательская функция json_tuple][image-hdi-hivejson-jsontuple]

<span data-ttu-id="641ec-147">JSON\_TUPLE использует синтаксис [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) Hive, который позволяет json\_tuple создать виртуальную таблицу, применяя определяемую пользователем функцию к каждой строке исходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="641ec-147">JSON\_TUPLE uses the [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple to create a virtual table by applying the UDT function to each row of the original table.</span></span>  <span data-ttu-id="641ec-148">Из-за многократного использования LATERAL VIEW синтаксис сложных документов JSON становится слишком громоздким.</span><span class="sxs-lookup"><span data-stu-id="641ec-148">Complex JSONs become too unwieldy because of the repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="641ec-149">Кроме того, JSON_TUPLE не может обрабатывать вложенные JSON.</span><span class="sxs-lookup"><span data-stu-id="641ec-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="641ec-150">Использование пользовательских SerDe</span><span class="sxs-lookup"><span data-stu-id="641ec-150">Use custom SerDe</span></span>
<span data-ttu-id="641ec-151">SerDe — лучший выбор для синтаксического анализа вложенных документов JSON, так как с ними можно определить схему JSON и использовать ее для синтаксического анализа документов.</span><span class="sxs-lookup"><span data-stu-id="641ec-151">SerDe is the best choice for parsing nested JSON documents, it allows you to define the JSON schema, and use the schema to parse the documents.</span></span> <span data-ttu-id="641ec-152">В этом руководстве мы воспользуемся более распространенными SerDe, которые были разработаны [Роберто Конгиу](https://github.com/rcongiu) (Roberto Congiu).</span><span class="sxs-lookup"><span data-stu-id="641ec-152">In this tutorial, you use one of the more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="641ec-153">**Для использования пользовательских SerDe выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="641ec-153">**To use the custom SerDe:**</span></span>

1. <span data-ttu-id="641ec-154">Установите [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="641ec-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="641ec-155">Если вы собираетесь использовать развертывание HDInsight в Windows, выберите версию JDK для 64-разрядной Windows</span><span class="sxs-lookup"><span data-stu-id="641ec-155">Choose the Windows X64 version of the JDK if you are going to be using the Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="641ec-156">JDK 1.8 не будет работать с этим SerDe.</span><span class="sxs-lookup"><span data-stu-id="641ec-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="641ec-157">После завершения установки добавьте новую переменную среды пользователя:</span><span class="sxs-lookup"><span data-stu-id="641ec-157">After the installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="641ec-158">Откройте окно **Дополнительные параметры системы** в Windows.</span><span class="sxs-lookup"><span data-stu-id="641ec-158">Open **View advanced system settings** from the Windows screen.</span></span>
   2. <span data-ttu-id="641ec-159">Выберите **Переменные среды**.</span><span class="sxs-lookup"><span data-stu-id="641ec-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="641ec-160">Добавьте новую переменную среды **JAVA_HOME**, которая указывает на **C:\Program Files\Java\jdk1.7.0_55** или на другую папку, в которую установлен JDK.</span><span class="sxs-lookup"><span data-stu-id="641ec-160">Add a new **JAVA_HOME** environment variable is pointing to **C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Настройка правильных значений конфигурации для JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="641ec-162">Установите [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="641ec-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="641ec-163">Добавьте в путь папку bin, выбрав на панели управления команду "Изменение системных переменных среды" для переменных среды вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="641ec-163">Add the bin folder to your path by going to Control Panel-->Edit the System Variables for your account Environment variables.</span></span> <span data-ttu-id="641ec-164">На следующем снимке экрана показано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="641ec-164">The following screenshot shows you how to do this.</span></span>
   
    ![Настройка Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="641ec-166">Создайте клон проекта с сайта [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) .</span><span class="sxs-lookup"><span data-stu-id="641ec-166">Clone the project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="641ec-167">Это можно сделать, нажав кнопку Download Zip ("Скачать ZIP-файл"), как показано на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="641ec-167">You can do this by clicking on the “Download Zip” button as shown in the following screenshot.</span></span>
   
    ![Клонирование проекта][image-hdi-hivejson-serde]

<span data-ttu-id="641ec-169">4: Перейдите в папку, куда скачан этот пакет, и введите mvn package.</span><span class="sxs-lookup"><span data-stu-id="641ec-169">4: Go to the folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="641ec-170">При этом должны создаться нужные JAR-файлы, который затем можно скопировать в кластер.</span><span class="sxs-lookup"><span data-stu-id="641ec-170">This should create the necessary jar files that you can then copy over to the cluster.</span></span>

<span data-ttu-id="641ec-171">5: Перейдите в целевую папку в корневой папке, в которую загрузили пакет.</span><span class="sxs-lookup"><span data-stu-id="641ec-171">5: Go to the target folder under the root folder where you downloaded the package.</span></span> <span data-ttu-id="641ec-172">Добавьте файл json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar в головной узел кластера.</span><span class="sxs-lookup"><span data-stu-id="641ec-172">Upload the json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file to head-node of your cluster.</span></span> <span data-ttu-id="641ec-173">Я обычно помещаю его в папку двоичных файлов Hive: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin или что-то подобное.</span><span class="sxs-lookup"><span data-stu-id="641ec-173">I usually put it under the hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="641ec-174">6: В командной строке Hive введите “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span><span class="sxs-lookup"><span data-stu-id="641ec-174">6: In the hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="641ec-175">Так как в моем случае JAR-файл находится в папке C:\apps\dist\hive-0.13.x\bin, можно напрямую добавить JAR с этим именем, как показано:</span><span class="sxs-lookup"><span data-stu-id="641ec-175">Since in my case, the jar is in the C:\apps\dist\hive-0.13.x\bin folder, I can directly add the jar with the name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Добавление JAR в проект][image-hdi-hivejson-addjar]

<span data-ttu-id="641ec-177">Теперь мы можем использовать SerDe для выполнения запросов к документу JSON.</span><span class="sxs-lookup"><span data-stu-id="641ec-177">Now, you are ready to use the SerDe to run queries against the JSON document.</span></span>

<span data-ttu-id="641ec-178">Следующий запрос создает таблицу с заданной схемой:</span><span class="sxs-lookup"><span data-stu-id="641ec-178">The following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="641ec-179">Для вывода имени и фамилии студента</span><span class="sxs-lookup"><span data-stu-id="641ec-179">To list the first name and last name of the student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="641ec-180">Вот результат из консоли Hive:</span><span class="sxs-lookup"><span data-stu-id="641ec-180">Here is the result from the Hive console.</span></span>

![Запрос SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="641ec-182">Для вычисления суммы оценок из документа JSON</span><span class="sxs-lookup"><span data-stu-id="641ec-182">To calculate the sum of scores of the JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="641ec-183">В предыдущем запросе используется пользовательская функция [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView), позволяющая развернуть массив оценок, чтобы просуммировать их.</span><span class="sxs-lookup"><span data-stu-id="641ec-183">The preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF to expand the array of scores so that they can be summed.</span></span>

<span data-ttu-id="641ec-184">Вот результат из консоли Hive:</span><span class="sxs-lookup"><span data-stu-id="641ec-184">Here is the output from the Hive console.</span></span>

![Запрос SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="641ec-186">Для поиска предметов, по которым данный студент получил более 80 баллов:</span><span class="sxs-lookup"><span data-stu-id="641ec-186">To find which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="641ec-187">Предыдущий запрос возвращает массив Hive (в отличие от функции get\_json\_object, возвращающей строку).</span><span class="sxs-lookup"><span data-stu-id="641ec-187">The preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Запрос SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="641ec-189">Если вы хотите пропустить документы JSON неправильного формата, просмотрите инструкции на [вики-странице](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) этого SerDe. Для этого можно ввести следующий код:</span><span class="sxs-lookup"><span data-stu-id="641ec-189">If you want to skil malformed JSON, then as explained in the [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing the following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="641ec-190">Сводка</span><span class="sxs-lookup"><span data-stu-id="641ec-190">Summary</span></span>
<span data-ttu-id="641ec-191">Напоследок следует заметить, что тип оператора JSON в Hive, который нужно выбрать, зависит от ситуации.</span><span class="sxs-lookup"><span data-stu-id="641ec-191">In conclusion, the type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="641ec-192">Если вам требуется найти всего одно поле в простом документе JSON, можно применять пользовательскую функцию Hive get\_json\_object.</span><span class="sxs-lookup"><span data-stu-id="641ec-192">If you have a simple JSON document and you only have one field to look up on – you can choose to use the Hive UDF get\_json\_object.</span></span> <span data-ttu-id="641ec-193">Если нужно выполнить поиск по нескольким ключам, можно использовать json_tuple.</span><span class="sxs-lookup"><span data-stu-id="641ec-193">If you have more than one key to look up on, then you can use json_tuple.</span></span> <span data-ttu-id="641ec-194">При наличии вложенного документа следует использовать SerDe JSON.</span><span class="sxs-lookup"><span data-stu-id="641ec-194">If you have a nested document, then you should use the JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="641ec-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="641ec-195">Next steps</span></span>

<span data-ttu-id="641ec-196">Другие статьи по этой теме приведены в</span><span class="sxs-lookup"><span data-stu-id="641ec-196">For other related articles, see</span></span>

* [<span data-ttu-id="641ec-197">Использование Hive и HiveQL с Hadoop в HDInsight для анализа примера файла log4j Apache</span><span class="sxs-lookup"><span data-stu-id="641ec-197">Use Hive and HiveQL with Hadoop in HDInsight to analyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="641ec-198">Анализ данных о задержке рейсов с помощью Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="641ec-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="641ec-199">Анализ данных Twitter с помощью Hive в HDInsight</span><span class="sxs-lookup"><span data-stu-id="641ec-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* <span data-ttu-id="641ec-200">[Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md) (Выполнение задания Apache Hive, Pig или Hadoop с помощью Azure Cosmos DB и HDInsight)</span><span class="sxs-lookup"><span data-stu-id="641ec-200">[Run a Hadoop job using Azure Cosmos DB and HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md)</span></span>

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
