---
title: "Удаленная отладка приложений Spark через SSH с помощью набора средств Azure для IntelliJ | Документы Майкрософт"
description: "Пошаговые инструкции по как кластеры toouse средства HDInsight в набор средств Azure для приложений toodebug IntelliJ удаленно на HDInsight через SSH"
keywords: "удаленная отладка intellij, ssh, intellij, hdinsight, отладка intellij, отладка"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>Отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH

В этой статье содержатся пошаговые инструкции о том, как toouse средства HDInsight в набор средств Azure для приложений toodebug IntelliJ удаленно в кластере HDInsight. toodebug проекта, вы также можете просмотреть hello [HDInsight Spark отладка приложений с помощью набора средств Azure для IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) видео.

**Предварительные требования**

* **Средства HDInsight из набора средств Azure для IntelliJ**. Этот инструмент входит в состав набора средств Azure для IntelliJ. Дополнительные сведения см. в статье [Установка набора средств Azure для IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).
* **Набор средств Azure для IntelliJ**. Используйте этот набор средств toocreate Spark приложений для кластера HDInsight. Дополнительные сведения, следуйте инструкциям hello [использования набора средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).
* **Служба SSH HDInsight с функцией управления именем пользователя и паролем.** Дополнительные сведения см. в разделе [подключения tooHDInsight (Hadoop) с помощью SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) и [использование SSH туннелирования tooaccess Ambari веб-интерфейса пользователя, JobHistory, NameNode, Oozie и других сетевых интерфейсов](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>Создание приложения Spark Scala и его настройка для удаленной отладки

1. Запустите IntelliJ IDEA и создайте проект. В hello **новый проект** диалогового окна поле, hello следующие:

   а. Выберите **HDInsight**. 

   b. Выберите шаблон Java или Scala (на свой выбор). Выбор между hello следующие параметры:

      - **Spark on HDInsight (Scala)** (Spark в HDInsight [Scala])

      - **Spark on HDInsight (Java)** (Spark в HDInsight [Java])

      - **Spark on HDInsight Cluster Run Sample (Scala)** (Пример запуска Spark в кластере HDInsight [Scala])

      В этом примере используется шаблон **Пример запуска Spark в кластере HDInsight (Scala)**.

   c. В hello **инструмент сборки** выберите либо hello следующие, tooyour потребность в соответствии с:

      - **Maven.** Для поддержки мастера создания проекта Scala.

      -  **SBT**, для управления зависимостями hello и построения для проекта Scala hello 

      ![Создание проекта отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. Щелкните **Далее**.     
 
3. В hello Далее **новый проект** окне hello следующие:

   ![Выберите hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   а. Введите имя и расположение проекта.

   b. В hello **проекта SDK** раскрывающемся списке выберите **Java 1.8** для **усилить 2.x** кластера и выберите **Java 1.7** для **Spark 1. x** кластера.

   c. В hello **версии Spark** раскрывающегося списка, мастер создания проекта Scala hello интегрирует hello правильная версия пакета SDK Spark и Scala SDK. Если версия кластера spark hello является более ранней, чем 2.0, выберите **усилить 1.x**. В противном случае выберите **Spark 2.x.** В этом примере используется **Spark 2.0.2 (Scala 2.11.8)**.

   d. Выберите **Готово**.

4. Выберите **src** > **основной** > **scala** tooopen кода в проекте hello. В этом примере используется hello **SparkCore_wasbloTest** сценария.

5. tooaccess hello **изменение конфигураций** меню, выберите hello значок в правом верхнем углу hello. В этом меню можно создавать и редактировать hello конфигурации для удаленной отладки.

   ![Меню Edit Configurations (Изменение конфигураций)](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. В hello **выполнения и отладки конфигураций** диалоговое окно, выберите hello "плюс" (**+**). Затем выберите hello **отправки задания Spark** параметр.

   ![Добавление новой конфигурации](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. Введите сведения в полях **Name** (Имя), **Spark cluster** (Кластер Spark) и **Main class name** (Имя основного класса). Затем выберите **Advanced configuration** (Расширенная конфигурация). 

   ![Запуск конфигураций отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. В hello **Spark отправки Расширенная настройка** выберите **Spark Включение удаленной отладки**. Введите имя пользователя SSH hello, затем введите пароль или использовать файл закрытого ключа. toosave hello конфигурацию, нажмите кнопку **ОК**.

   ![Включение удаленной отладки Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. Конфигурация Hello теперь сохраняется с именем hello. tooview hello сведения о конфигурации, выберите hello имя конфигурации. Выберите изменения toomake **изменить конфигурации**. 

10. После завершения настройки конфигурации hello, можно запустить проект hello для удаленного кластера hello или выполнять удаленную отладку.

## <a name="learn-how-tooperform-remote-debugging"></a>Узнайте, как tooperform удаленной отладки
### <a name="scenario-1-perform-remote-run"></a>Сценарий 1. Удаленный запуск

В этом разделе вы узнаете toodebug драйверы и исполнителей.

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. Настройка слабые места, а затем выберите hello **отладки** значок.

   ![Выберите значок отладки hello](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. Когда выполнение программы hello достигает точки критические hello, см **драйвер** вкладку и два **исполнителя** вкладки в hello **отладчик** области. Выберите hello **программы Resume** toocontinue значок под управлением hello код, который затем достигает hello следующей точки останова и основное внимание уделяется соответствующий hello **исполнителя** вкладки. Изучите журналы выполнения hello на соответствующий hello **консоли** вкладки.

   ![Вкладка отладки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>Сценарий 2. Удаленная отладка и исправление ошибок
В этом разделе мы расскажем как toodynamically обновления hello значение переменной с помощью hello IntelliJ возможности для простого исправления отладки. В следующем примере кода hello исключение создается потому hello целевой файл уже существует.
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>tooperform удаленная отладка и исправление ошибок
1. Настройка двух слабые места, а затем выберите hello **отладки** значок toostart hello удаленной отладки процесса.

2. Hello кода останавливается на первой точки критические hello, а также параметр hello и сведения о переменных в hello **переменных** области. 

3. Выберите hello **программы Resume** toocontinue значок. Hello код останавливает hello второй точки. Hello исключение перехватывается, как ожидалось.

  ![Ошибка](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. Выберите hello **программы Resume** значок еще раз. Hello **HDInsight Spark отправки** окна отображается сообщение об ошибке «не удалось выполнить задание».

  ![Ошибка отправки](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. Выберите toodynamically обновления hello значение переменной с помощью функции отладки IntelliJ hello, **отладки** еще раз. Hello **переменных** появится область. 

6. Щелкните правой кнопкой мыши целевой hello на hello **отладки** , а затем выберите **задание значения**. Затем введите новое значение для переменной hello. Выберите **ввод** toosave значение hello. 

  ![Задание значения](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. Выберите hello **программы Resume** значок toocontinue toorun hello программы. На этот раз исключение не возникает. Вы увидите, что этот проект hello успешно выполняется без исключения.

  ![Отладка без исключений](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Дальнейшие действия
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Демонстрация
* Создание проекта Scala (видео): [создание приложений Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Удаленной отладки (видео): [используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно на кластер HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Сценарии
* [Использование средств визуализации данных с помощью Apache Spark BI в Azure HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark с машинного обучения: используйте Spark в HDInsight tooanalyze построение с использованием данных Кондиционирования температуры](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark потоковой передачи: Используйте Spark в HDInsight toobuild в режиме реального времени потоковую передачу приложений](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Используйте набор средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через виртуальную частную сеть](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядер, доступных для записной книжки Jupyter hello кластера Spark для HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)
