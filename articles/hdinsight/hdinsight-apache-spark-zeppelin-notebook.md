---
title: "кластер записных книжек Zeppelin aaaUse с Apache Spark на Azure HDInsight | Документы Microsoft"
description: "Пошаговые инструкции по как кластеры записных книжек Zeppelin toouse с Apache Spark на Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Использование записных книжек Zeppelin с кластером Apache Spark в Azure HDInsight

Кластеры HDInsight Spark включают Zeppelin портативные компьютеры, которые можно использовать toorun Spark заданий. В этой статье вы узнаете, как toouse hello записной книжки Zeppelin в кластере HDInsight.

> [!NOTE]
> Записные книжки Zeppelin доступны только для Spark 1.6.3 в HDInsight 3.5 и для Spark 2.1.0 в HDInsight 3.6.
>

**Предварительные требования:**

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="launch-a-zeppelin-notebook"></a>Запуск записной книжки Zeppelin
1. Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **Zeppelin ноутбук**. При появлении запроса введите учетные данные администратора hello hello кластера.
   
   > [!NOTE]
   > Также может достигать hello Zeppelin ноутбук для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. Создайте новую записную книжку. Hello заголовка области, щелкните ссылку **записной книжки**, а затем нажмите кнопку **создать новую заметку**.
   
    ![Создание записной книжки Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Создание записной книжки Zeppelin")
   
    Введите имя для hello портативного компьютера и нажмите кнопку **создать Примечание**.
3. Кроме того убедитесь, что заголовок записной книжки hello показывает подключенном состоянии. Он обозначается зеленая точка в верхнем правом углу hello.
   
    ![Состояния записной книжки Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Состояния записной книжки Zeppelin")
4. Загрузите демонстрационные данные во временную таблицу. При создании кластера Spark в HDInsight hello образец файла данных **hvac.csv**, является скопированный toohello связанные учетной записи хранилища в группе **\HdiSamples\SensorSampleData\hvac**.
   
    В пустой абзац hello, создаваемый по умолчанию в новой записной книжки hello вставьте следующий фрагмент кода hello.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    Нажмите клавишу **SHIFT + ВВОД** или нажмите кнопку hello **воспроизведение** кнопки для hello абзаца toorun hello фрагмента. состояние Hello в правом углу hello абзаца hello следует хода выполнения Готово, ОЖИДАЮЩИХ ВЫПОЛНЕНИЯ tooFINISHED. выходные данные Hello отображается внизу hello hello того же абзаца. Снимок экрана приветствия выглядит hello следующим образом:
   
    ![Создание временной таблицы из необработанных данных](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Создание временной таблицы из необработанных данных")
   
    Можно также ввести заголовок tooeach абзаца. В правом углу hello, выберите hello **параметры** значок, а затем щелкните **Показать заголовок**.
5. Теперь можно запустить инструкции Spark SQL для hello **кондиционирования** таблицы. Вставьте приветствия при следующем запросе в новый абзац. Hello запрос извлекает код здания hello и hello разницу между целевой hello и фактический температуру для каждой сборки в определенную дату. Нажмите **SHIFT + ВВОД**.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    Hello **% sql** оператор в начале hello указывает hello записной книжки toouse hello Livy Scala интерпретатора.
   
    Hello следующем снимке экрана показаны выходные данные hello.
   
    ![Выполнить Spark SQL с помощью записной книжки hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "выполнить Spark SQL с помощью записной книжки hello")
   
     Нажмите кнопку tooswitch (выделенный в прямоугольник) параметры отображения hello между различными представлениями для hello такие же выходные данные. Нажмите кнопку **параметры** toochoose какие consitutes hello ключа и значения в выходных данных hello. Здравствуйте, снимки экрана выше используется **buildingID** как ключ hello и среднее значение hello **temp_diff** как значение hello.
6. Можно также запустить инструкции Spark SQL, использование переменных в запросе hello. Далее показан фрагмент кода Hello как toodefine переменной, **Temp**, в запросе hello с возможными значениями hello требуется tooquery с. При первом запуске запроса hello, раскрывающийся список заполняется автоматически со значениями hello, указанное для переменной hello.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    Вставьте этот фрагмент кода в новый абзац и нажмите клавиши **SHIFT + ВВОД**. Hello следующем снимке экрана показаны выходные данные hello.
   
    ![Выполнить Spark SQL с помощью записной книжки hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "выполнить Spark SQL с помощью записной книжки hello")
   
    Для последующих запросов можно выбрать новое значение из раскрывающегося списка hello и снова запустите запрос hello. Нажмите кнопку **параметры** toochoose какие consitutes hello ключа и значения в выходных данных hello. Здравствуйте, снимки экрана выше используется **buildingID** в качестве ключа hello hello среднее **temp_diff** как значение hello и **targettemp** как группа hello.
7. Перезапустите приложения hello tooexit интерпретатор Livy hello. Откройте интерпретатор параметры, нажав кнопку входа имя пользователя в правом верхнем углу hello hello toodo и нажмите кнопку **интерпретатор**.
   
    ![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")
8. Прокрутите tooLivy интерпретатор параметры и нажмите кнопку **перезапустите**.
   
    ![Перезапустите hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "перезапустите hello Zeppelin intepreter")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>Как использовать внешние пакеты с ноутбука hello?
Можно настроить записной книжки Zeppelin hello в кластере Apache Spark на HDInsight (Linux) toouse внешних сообществом пакеты, которые не включены out-of box в кластере hello. Можно выполнить поиск hello [Maven репозитория](http://search.maven.org/) hello полный список доступных пакетов. Его также можно получить из других источников. Например, полный список предоставленных сообществом пакетов можно найти в разделе [Пакеты Spark](http://spark-packages.org/).

В этой статье вы увидите как toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) пакет записной книжки Jupyter hello.

1. Откройте параметры интерпретатора. Hello верхний правый угол, щелкните hello вход от имени пользователя и нажмите кнопку **интерпретатор**.
   
    ![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")
2. Прокрутите tooLivy интерпретатор параметры и нажмите кнопку **изменить**.
   
    ![Изменение параметров интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Изменение параметров интерпретатора")
3. Добавьте новый раздел, называется **livy.spark.jars.packages** и присвойте ему значение в формате hello `group:id:version`. Таким образом, если вы хотите toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) пакета, необходимо задать значение hello hello ключа слишком`com.databricks:spark-csv_2.10:1.4.0`.
   
    ![Изменение параметров интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Изменение параметров интерпретатора")
   
    Нажмите кнопку **Сохранить** , а затем перезапустите hello Livy интерпретатора.
4. **Совет**: Если необходимо, чтобы toounderstand как tooarrive hello значения ключа hello на введенный выше, Вот каким образом.
   
    а. Найдите пакет hello в hello Maven репозитория. В этом руководстве мы используем [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Из репозитория hello сбора значений hello **GroupId**, **ArtifactId**, и **версии**.
   
    ![Использование внешних пакетов с записными книжками Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Использование внешних пакетов с записными книжками Jupyter")
   
    c. Объединение hello трех значений, разделенных точкой с запятой (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>Где находятся hello записных книжек Zeppelin сохранить?
портативные компьютеры Zeppelin Hello сохраняются headnodes toohello кластера. Поэтому при удалении кластера hello записных книжек hello также будут удалены. Если требуется toopreserve записных книжек для последующего использования в других кластерах, необходимо экспортировать их после завершения выполнения заданий hello. tooexport записной книжке щелкните hello **Экспорт** значок, как показано в приведенном ниже рисунке hello.

![Загрузите записной книжки](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "записной книжки hello загрузки")

Это экономит записной книжки hello в формате JSON в место для загрузки.

## <a name="livy-session-management"></a>Управление сеансом Livy
При выполнении первого абзаца кода hello в блокноте Zeppelin Livy новый сеанс создается в кластере HDInsight Spark. Этот сеанс будет общим в записных книжках Zeppelin, которые вы затем создадите. Если для некоторых hello причина Livy сеанс завершен (Перезагрузка кластера, т. д.), не будет возможности toorun заданий из записной книжки Zeppelin hello.

В этом случае необходимо выполнить следующие действия перед началом выполнения заданий из записной книжке Zeppelin hello. 

1. Перезапустите hello интерпретатор Livy из записной книжки Zeppelin hello. Откройте интерпретатор параметры, нажав кнопку входа имя пользователя в правом верхнем углу hello hello toodo и нажмите кнопку **интерпретатор**.
   
    ![Запуск интерпретатора](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Выходные данные Hive")
2. Прокрутите tooLivy интерпретатор параметры и нажмите кнопку **перезапустите**.
   
    ![Перезапустите hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "перезапустите hello Zeppelin intepreter")
3. Запустите ячейку кода из имеющейся записной книжки Zeppelin. Будет создан новый сеанс Livy hello кластера HDInsight.

## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







