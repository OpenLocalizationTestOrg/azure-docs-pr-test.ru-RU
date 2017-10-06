---
title: "aaaUse Apache Spark tooanalyze данные в хранилище Озера данных Azure | Документы Microsoft"
description: "Запуск заданий Spark tooanalyze данные, хранящиеся в хранилище Озера данных Azure"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>Использовать данные tooanalyze кластера HDInsight Spark в хранилище Озера данных

В этом учебнике используется книжке Jupyter доступны с кластерами HDInsight Spark toorun задание, которое считывает данные из учетной записи хранилища Озера данных.

## <a name="prerequisites"></a>Предварительные требования

* Учетная запись Azure Data Lake Store. Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).

* Кластер Azure HDInsight Spark с Data Lake Store в качестве хранилища. Следуйте инструкциям hello в [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    
## <a name="prepare-hello-data"></a>Подготовка данных hello

> [!NOTE]
> Необязательно tooperform этот шаг при создании кластера HDInsight hello с хранилища Озера данных в качестве хранилища по умолчанию. процессы создания кластера Hello добавляет некоторые демонстрационные данные в учетной записи хранилища Озера данных hello, указанным при создании кластера hello. Пропустите раздел toohello [HDInsight Spark использования кластера с хранилища Озера данных](#use-an-hdinsight-spark-cluster-with-data-lake-store).
>
>

При создании кластера HDInsight с хранилища Озера данных как дополнительное хранилище и больших двоичных объектов хранилища Azure хранения по умолчанию, следует скопировать эти некоторых toohello данных образец хранилища Озера данных. Можно использовать hello демонстрационных данных из больших двоичных объектов хранилища Azure, связанной с кластером HDInsight hello hello. Можно использовать hello [ADLCopy средство](http://aka.ms/downloadadlcopy) toodo так. Загрузите и установите программу hello ссылке hello.

1. Откройте командную строку и перейдите в каталог toohello AdlCopy установки, обычно `%HOMEPATH%\Documents\adlcopy`.

2. Запустите hello, следующая команда toocopy конкретного BLOB-объектов из hello исходный контейнер tooa хранилища Озера данных:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Копировать hello **HVAC.csv** файл образца данных **/HdiSamples/HdiSamples/SensorSampleData/кондиционирования/** toohello хранилища Озера данных Azure. фрагмент кода Hello должен выглядеть так:

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > Убедитесь, что hello файла и пути находятся в правильном регистре hello.
   >
   >
3. Появится запрос tooenter hello учетные данные для hello подписки Azure, в котором у вас есть учетная запись хранилища Озера данных. Вы увидите выходные данные примерно toohello следующие:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    файл данных Hello (**HVAC.csv**) будут скопированы в папке **/hvac** в hello хранилища Озера данных.

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>Использование кластера HDInsight Spark с Data Lake Store

1. Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели). Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.

2. Из колонки кластера Spark hello, нажмите кнопку **быстрые ссылки**, а затем из hello **мониторинга кластера** колонке нажмите кнопку **книжке Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.

   > [!NOTE]
   > Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Создайте новую записную книжку. Щелкните **Создать**, а затем выберите **PySpark**.

    ![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Создание записной книжки Jupyter")

4. Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом. контексты Spark и Hive Hello автоматически создается автоматически при выполнении первой ячейке кода hello. Можно запустить, импортировав hello типы, необходимые для этого сценария. toodo таким образом, вставьте следующий фрагмент кода в ячейку и нажать клавишу hello **SHIFT + ВВОД**.

        from pyspark.sql.types import *

    Отображается каждый раз при запуске задания в Jupyter, заголовок окна обозревателя вашей веб **(Busy)** состояния вместе с hello записной книжки заголовка. Вы также увидите Далее toohello сплошной кружок **PySpark** текст в верхнем правом углу hello. После завершения задания hello, это приведет к изменению tooa полый круг.

     ![Состояние задания записной книжки Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Состояние задания записной книжки Jupyter")

5. Загрузить образец данных во временную таблицу с помощью hello **HVAC.csv** файл, скопированный учетной записи хранилища Озера данных toohello. Можно получить доступ к hello данные в учетной записи хранилища Озера данных hello, используя следующий шаблон URL-адреса hello.

    * Если у вас есть хранилища Озера данных в качестве хранилища по умолчанию, HVAC.csv будет на аналогичные toohello hello путь URL-адреса:

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        Или можно также использовать сокращенный формат, например hello следующее:

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * Если у вас есть хранилища Озера данных в виде дополнительное хранилище, HVAC.csv будет в расположении hello, куда был скопирован, такие как:

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     В пустой ячейке, hello вставьте следующий пример кода замените **MYDATALAKESTORE** с помощью имени учетной записи хранилища Озера данных и нажмите клавишу **SHIFT + ВВОД**. В этом примере кода регистрируется hello данные во временную таблицу с именем **кондиционирования**.

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. Так как вы используете ядра PySpark, теперь можно напрямую запустить SQL-запрос для временной таблицы hello **кондиционирования** вы только что создали с помощью hello `%%sql` магическое значение. Дополнительные сведения о hello `%%sql` magic, а также другие доступные ядра PySpark hello, magics разделе [ядер, доступных на записные книжки Jupyter с кластерами Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. После успешного завершения задания hello hello, следуя табличного вывода отображается по умолчанию.

      ![Вывод результатов запроса в виде таблицы](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Вывод результатов запроса в виде таблицы")

     Можно также посмотреть результаты hello в другие представления, а также. Например график для приветствия такие же выходные данные выглядят hello следующее.

     ![Диаграмма с областями, показывающая результат запроса](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Диаграмма с областями, показывающая результат запроса")

8. После завершения работы приложения hello, необходимо hello toorelease ресурсы для завершения работы hello ноутбуков. toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**. В этом будет завершена и закрыть hello ноутбука.


## <a name="next-steps"></a>Дальнейшие действия

* [Создание автономного Scala приложения toorun кластере Apache Spark](hdinsight-apache-spark-create-standalone-application.md)
* [Используйте средства HDInsight в набор средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений для кластера HDInsight Spark Linux](hdinsight-apache-spark-eclipse-tool-plugin.md)
