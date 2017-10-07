---
title: "aaaRun интерактивной обработки запросов на кластере Azure HDInsight Spark | Документы Microsoft"
description: "Примеры использования HDInsight Spark на как кластер toocreate Apache Spark в HDInsight."
keywords: "краткое руководство Spark,интерактивный запрос Spark,интерактивный запрос,Hdinsight Spark,Azure Spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Выполнение интерактивных запросов в кластере HDInsight Spark

В этой статье используется Jupyter записной книжки toorun интерактивного Spark SQL-запросов к кластера Spark. Книжке Jupyter является приложением на основе браузера, расширяющий toohello интерактивное взаимодействие с помощью консоли hello Web. Дополнительные сведения см. в разделе [книжке Jupyter hello](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

В этом учебнике используется hello **PySpark** ядра в toorun записной книжки Jupyter hello интерактивный Spark SQL-запроса. Записные книжки Jupyter в кластерах HDInsight поддерживают еще две версии ядер — **PySpark3** и **Spark**. Дополнительные сведения о ядрах hello и преимущества использования hello **PySpark**, в разделе [кластеров ядер записной книжки Jupyter использования с Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Предварительные требования

* **Кластер Azure HDInsight Spark**. Инструкции см. в статье [Создание кластера Apache Spark в Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Создание записной книжке Jupyter toorun интерактивной обработки запросов

запросы toorun мы используем образец данных, по умолчанию, доступные в hello хранилище, связанное с кластером hello. Но эти данные нужно сначала загрузить в Spark в виде кадра данных. При наличии hello кадр данных можно выполнять запросы на его с помощью книжке Jupyter hello. Из этого раздела вы узнаете, как выполнять следующие действия:

* регистрация тестового набора данных в качестве кадра данных Spark;
* Выполнять запросы на кадр данных hello.

1. Откройте hello [портал Azure](https://portal.azure.com/). Если вы выбрали мониторинга toohello toopin hello кластера, щелкните плитку кластера hello из hello мониторинга toolaunch hello кластера колонки.

    Если не закрепить мониторинга toohello кластера hello hello левой панели, нажмите кнопку **кластеров HDInsight**и нажмите кнопку hello кластера, вы создали.

3. В разделе **Быстрые ссылки** щелкните **Панели мониторинга кластера**, а затем — **Записная книжка Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.

   ![Откройте Jupyter записной книжки toorun интерактивного Spark SQL-запроса](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "откройте Jupyter записной книжки toorun интерактивного Spark SQL-запроса")

   > [!NOTE]
   > Также может обращаться к записной книжки Jupyter hello для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Создайте записную книжку. Щелкните **Создать**, а затем выберите **PySpark**.

   ![Создать интерактивный запрос Spark SQL Jupyter записной книжки toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "создания Jupyter записной книжки toorun интерактивного Spark SQL-запроса")

   Создается и открывается с именем hello Untitled(Untitled.pynb) новый блокнот.

4. Щелкните имя записной книжки hello вверху hello и введите понятное имя, если требуется.

    ![Введите имя для hello Jupter записной книжки toorun интерактивных Spark запросов из](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "укажите имя для hello Jupter записной книжки toorun интерактивных Spark запросов из")

5. Ниже hello вставить код в пустой ячейке и нажмите клавишу **SHIFT + ВВОД** toorun кода hello. Код Hello импортирует hello типы, необходимые для этого сценария:

        from pyspark.sql.types import *

    Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом. контексты Spark и Hive Hello автоматически создаются при выполнении первой ячейке кода hello.

    ![Состояние интерактивного запроса Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Состояние интерактивного запроса Spark SQL")

    Показывает каждый раз при выполнении интерактивных запросов в Jupyter, заголовок окна обозревателя вашей веб **(Busy)** состояния вместе с hello записной книжки заголовка. Появится следующий toohello сплошной кружок **PySpark** текст в верхнем правом углу hello. По завершении задания hello изменяется tooa полый круг.

6. Перед загрузкой данных hello в кластере Spark, сообщите нам найти моментальный снимок. Hello образцы данных, используемые в этом учебнике доступен в виде CSV-файла на всех кластерах HDInsight Spark на **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. Hello данных захватывает hello температуры различные виды здания. Ниже приведены несколько первых строк данных hello hello.

    ![Моментальный снимок данных для интерактивных запросов Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Snapshot of data for interactive Spark SQL query")

6. Создайте кадр данных и временную таблицу (**кондиционирования**), выполнив следующий код hello. В этом учебнике мы не создавайте все столбцы hello в hello временную таблицу сравнения toohello в виде столбцов hello необработанных данных в формате CSV. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. После создания таблицы hello построения интерактивных запросов на основе данных hello, с помощью hello, следующий код.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Так как вы используете ядра PySpark, теперь можно напрямую запустить интерактивный SQL-запроса для временной таблицы hello **кондиционирования** , созданного с помощью hello `%%sql` магическое значение. Дополнительные сведения о hello `%%sql` magic и другие доступные ядра PySpark hello, magics. в разделе [ядер, доступных на записные книжки Jupyter с кластерами Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   по умолчанию отображаются следующие табличного вывода Hello.

     ![Таблица результатов интерактивного запроса Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Таблица результатов интерактивного запроса Spark")

    Можно также посмотреть результаты hello в другие представления, а также. Например график для приветствия такие же выходные данные выглядят hello следующее.

    ![Диаграмма с областями результата интерактивного запроса Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Диаграмма с областями результата интерактивного запроса Spark")

9. Завершение работы ресурсов кластера hello toorelease записной книжки hello, после завершения работы приложения hello. toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.

## <a name="next-step"></a>Дальнейшие действия

В этой статье вы узнали, каким образом toorun интерактивной обработки запросов в Spark с помощью книжке Jupyter. Далее в статье toosee toohello как извлечь данные hello, зарегистрированное в Spark приращения в средство анализа бизнес-Аналитики, таких как Power BI и Tableau. 

> [!div class="nextstepaction"]
>[Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight](hdinsight-apache-spark-use-bi-tools.md)




