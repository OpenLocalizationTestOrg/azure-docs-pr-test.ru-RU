---
title: "aaaSpark бизнес-Аналитики с помощью средств визуализации данных в Azure HDInsight | Документы Microsoft"
description: "Используйте средства визуализации данных для аналитики с помощью Apache Spark BI в кластерах HDInsight"
keywords: "apache spark bi, spark bi, визуализация данных spark, бизнес-аналитика spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight

Узнайте, как визуализации данных toouse средств, таких как Power BI и Tableau tooanalyze необработанные образец набора данных с помощью Apache Spark бизнес-Аналитики в кластерах HDInsight.

> [!NOTE]
> Возможности подключения к инструментам бизнес-аналитики, описываемые в этой статье, не поддерживаются в Spark 2.1 в Azure HDInsight 3.6 (предварительная версия). Поддерживается только Spark версий 1.6 и 2.0 (HDInsight 3.4 и HDInsight 3.5 соответственно).
>

Это руководство также доступно в виде записной книжки Jupyter в кластере HDInsight Spark. взаимодействие с ноутбука Hello позволяет выполнять фрагменты кода Python hello из записной книжки hello сам. Учебник hello tooperform в записной книжке создать кластер Spark, запустить записной книжке Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), и запустите записной книжки hello **средства используйте бизнес-Аналитики с Apache Spark в HDInsight.ipynb** под hello **Python**  папки.

## <a name="prerequisites"></a>Предварительные требования

* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="hivetable"></a>Подготовка данных для визуализации данных Spark

В этом разделе мы используем hello [Jupyter](https://jupyter.org) записной книжки из заданий toorun кластера HDInsight Spark, которые обрабатывают необработанные образцы данных и сохраните его в виде таблицы. Образец Hello данных является CSV-файла (hvac.csv) доступен во всех кластерах по умолчанию. После сохранения данных как таблицу в следующем разделе hello мы используйте таблицу toohello tooconnect средств бизнес-Аналитики и выполнять визуализации данных.

> [!NOTE]
> При выполнении hello шаги в этой статье после выполнения инструкций hello в [выполнения интерактивных запросов на кластере Spark в HDInsight](hdinsight-apache-spark-load-data-run-query.md), можно пропустить tooStep 8 ниже.
>

1. Из hello [портал Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели). Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.   

2. Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.

   > [!NOTE]
   > Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Создайте записную книжку. Щелкните **Создать**, а затем выберите **PySpark**.

    ![Создание записной книжки Jupyter для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "Создание записной книжки Jupyter для Apache Spark BI")

4. Создается и открывается с именем hello Untitled.pynb новый блокнот. Щелкните имя записной книжки hello вверху hello и введите понятное имя.

    ![Введите имя для ноутбука hello для бизнес-Аналитики Apache Spark](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "укажите имя для ноутбука hello для бизнес-Аналитики Apache Spark")

5. Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом. контексты Spark и Hive Hello автоматически создаются при выполнении первой ячейке кода hello. Можно запустить, импортировав hello типы, необходимые для этого сценария. toodo таким образом, поместите курсор hello в ячейке hello и нажмите клавишу **SHIFT + ВВОД**.

        from pyspark.sql import *

6. Загрузите демонстрационные данные во временную таблицу. При создании кластера Spark в HDInsight hello образец файла данных **hvac.csv**, является скопированный toohello связанные учетной записи хранилища в группе **\HdiSamples\HdiSamples\SensorSampleData\hvac**.

    В пустой ячейке, вставьте hello следующий фрагмент кода и нажмите клавишу **SHIFT + ВВОД**. В этом фрагменте регистрирует hello данных в таблицу с именем **кондиционирования**.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. Убедитесь, что таблица hello была успешно создана. Можно использовать hello `%%sql` магическая запросов Hive toorun напрямую. Дополнительные сведения о hello `%%sql` magic и другие доступные ядра PySpark hello, magics. в разделе [ядер, доступных на записные книжки Jupyter с кластерами Spark HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SHOW TABLES

    Вы увидите примерно следующие выходные данные:

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Здравствуйте, только таблицы, которые имеют значение false в группе hello **isTemporary** столбца — таблицы hive, которые хранятся в метахранилище hello и может осуществляться из средств бизнес-Аналитики hello. В этом учебнике мы соединение toohello **кондиционирования** созданную таблицу.

8. Убедитесь, что эта таблица hello содержит hello предназначен данных. В пустой ячейке в записной книжке hello, скопируйте следующие hello фрагмент и нажмите клавишу **SHIFT + ВВОД**.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Завершение работы toorelease hello hello записной книжки ресурсы. toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**.

## <a name="powerbi"></a>Использование Power BI для визуализации данных Spark

> [!NOTE]
> Этот раздел применим только к Spark 1.6 в HDInsight 3.4 и к Spark 2.0 в HDInsight 3.5.
>
>

После сохранения данных hello как таблицу, можно использовать Power BI tooconnect toohello данных и их визуализации toocreate отчеты, панели мониторинга и т. д.

1. Убедитесь, что у вас есть доступ tooPower бизнес-Аналитики. Вы можете оформить подписку на бесплатную предварительную версию Power BI на сайте [http://www.powerbi.com/](http://www.powerbi.com/).

2. Войдите в слишком[Power BI](http://www.powerbi.com/).

3. Hello нижней части левой панели hello, щелкните **получение данных**.

4. На hello **получить данные** в разделе **Импорт или подключение tooData**, для **баз данных**, нажмите кнопку **получить**.

    ![Получение данных в Power BI для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "Получение данных в Power BI для Apache Spark BI")

5. На следующем экране приветствия щелкните **Spark на Azure HDInsight** и нажмите кнопку **Connect**. При появлении запроса введите URL-адрес кластера hello (`mysparkcluster.azurehdinsight.net`) и tooconnect toohello hello учетные данные кластера.

    ![Подключение tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "подключения tooApache Spark бизнес-Аналитики")

    После установления соединения hello Power BI начинается Импорт данных из hello кластера Spark в HDInsight.

6. Power BI импортирует данные hello и добавляет **Spark** набора данных в группе hello **наборы данных** заголовок. Выберите набор данных hello tooopen новые данные hello toovisualize листа. Можно также сохранить hello листа в виде отчета. лист, из hello toosave **файл** меню, нажмите кнопку **Сохранить**.

    ![Плитка Apache Spark BI на информационной панели Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Плитка Apache Spark BI на информационной панели Power BI")
7. Обратите внимание, что hello **поля** списке справа hello перечислены hello **кондиционирования** таблицы, созданной ранее. Разверните hello toosee hello поля в таблице hello, как определено ранее в записной книжке.

      ![Список таблиц на панели мониторинга Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Список таблиц на панели мониторинга Apache Spark BI")

8. Построение визуализации tooshow hello расхождение целевой температуры и фактический температуры для каждой сборки. Выберите данные yoru toovisualize, **диаграмма с областями** (показано красным прямоугольником). toodefine hello оси, и перетащите hello **BuildingID** под **оси**, и **ActualTemp**/**TargetTemp** поля в группе **значение**.

    ![Создание визуализаций данных Spark с помощью Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "Создание визуализаций данных Spark с помощью Apache Spark BI")

9. По умолчанию hello визуализации показывает сумму hello **ActualTemp** и **TargetTemp**. Здравствуйте, оба поля, из раскрывающегося списка hello рекомендуется выбрать **среднее** tooget температуру целевой для обоих зданий и фактическое среднее.

    ![Создание визуализаций данных Spark с помощью Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "Создание визуализаций данных Spark с помощью Apache Spark BI")

10. Визуализация данных должно быть примерно toohello один на снимке экрана приветствия. Переместите указатель мыши hello визуализации tooget всплывающие подсказки с соответствующими данными.

    ![Создание визуализаций данных Spark с помощью Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "Создание визуализаций данных Spark с помощью Apache Spark BI")

11. Нажмите кнопку **Сохранить** из hello верхнего меню и введите имя отчета. Можно также закрепить hello visual. При закреплении визуализации хранится на панели мониторинга для отслеживания hello последние значения с одного взгляда.

   Можно добавить столько визуализации для hello того же набора данных и закреплять их toohello панель мониторинга для моментального снимка данных. Кроме того кластеры Spark на HDInsight будут подключенных tooPower бизнес-Аналитики с помощью прямого подключения. Это гарантирует, что Power BI всегда иметь hello большинство актуальные данные из кластера, поэтому нет необходимости tooschedule обновления для набора данных hello.

## <a name="tableau"></a>Использование Tableau Desktop для визуализации данных Spark

> [!NOTE]
> Этот раздел применим только для кластеров Spark 1.5.2, созданных в Azure HDInsight.
>
>

1. Установка [Tableau Desktop](http://www.tableau.com/products/desktop) на компьютере hello, где запускается этот учебник Apache Spark бизнес-Аналитики.

2. Убедитесь, что на этом компьютере также установлен драйвер ODBC Microsoft Spark. Можно установить драйвер hello из [здесь](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Запустите Tableau Desktop. Hello левой панели, из списка hello tooconnect сервера, щелкните **Spark SQL**. Если Spark SQL по умолчанию в левой области hello не указывается, его можно найти по щелчку **более серверов**.
2. В диалоговое окно «соединение» для hello Spark SQL, вводить значения hello, как показано на снимке экрана приветствия и нажмите кнопку **ОК**.

    ![Кластер tooa Connect для бизнес-Аналитики Apache Spark](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "кластера tooa Connect для бизнес-Аналитики Apache Spark")

    Здравствуйте, раскрывающиеся списки проверки подлинности **службы Microsoft Azure HDInsight** в качестве альтернативы только в том случае, если вы установили hello [драйвер Microsoft Spark ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) на компьютере hello.
3. На следующем экране hello из hello **схемы** раскрывающийся список, нажмите кнопку hello **найти** значок, а затем щелкните **по умолчанию**.

    ![Поиск схемы для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Поиск схемы для Apache Spark BI")
4. Для hello **таблицы** щелкните hello **найти** значок снова toolist все hello Hive таблиц, доступных в кластере hello. Вы увидите hello **кондиционирования** таблицы, созданной ранее с помощью записной книжки hello.

    ![Поиск схемы для Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Поиск схемы для Apache Spark BI")
5. Перетаскивание hello таблицы toohello верхнем поле на hello вправо. Tableau импортирует данные hello и отображает hello схемы как видно hello красным прямоугольником.

    ![Добавление таблицы tooTableau для бизнес-Аналитики Apache Spark](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "добавить tooTableau таблиц для бизнес-Аналитики Apache Spark")
6. Нажмите кнопку hello **Sheet1** вкладку внизу hello слева. Сделайте визуализации, показывающую средний целевой hello и фактический температуре все зданий для каждой даты. Перетащите **даты** и **код здания** слишком**столбцы** и **фактическое Temp**/**Temp целевой**слишком**строк**. В разделе **метки**выберите **область** toouse область карты для визуализации данных Spark.

     ![Добавление полей для визуализации данных Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Добавление полей для визуализации данных Spark")
7. По умолчанию показаны поля температуры hello как статистическое выражение. Если вместо этого требуется среднее температуры tooshow hello это можно сделать hello раскрывающемся списке, как показано ниже.

    ![Получение среднего значения температуры для визуализации данных Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "Получение среднего значения температуры для визуализации данных Spark")

8. Можно также super применить температуры сопоставления более hello других tooget лучше понять разницу между цель и фактический температуре. Переместите hello мыши toohello углу hello нижней области карты, пока не появиться фигуры дескриптор hello, выделяются в красном круге. Перетащите toohello карты hello другого сопоставления hello top и выпуска hello мыши при появлении hello фигуры, выделены красным прямоугольником.

    ![Слияние карт для визуализации данных Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "Слияние карт для визуализации данных Spark")

     Визуализация данных необходимо указать, как показано на снимке экрана приветствия:

    ![Выходные данные Tableau для визуализации данных Spark](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Выходные данные Tableau для визуализации данных Spark")
9. Нажмите кнопку **Сохранить** toosave hello листа. Можно создать панели мониторинга и добавьте один или несколько листов tooit.

## <a name="next-steps"></a>Дальнейшие действия

Пока вы узнали, как создать данных tooquery кадры данных Spark toocreate кластера и получить доступ к этим данным из средств бизнес-Аналитики. Теперь можно просмотреть инструкции по их как toomanage hello ресурсы кластера и отладка задания, запущенные в кластере HDInsight Spark.

* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

