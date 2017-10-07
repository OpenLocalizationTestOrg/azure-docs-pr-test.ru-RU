---
title: "Набор средств Azure для IntelliJ. Создание приложений Spark для кластера HDInsight | Документация Майкрософт"
description: "Использовать hello Azure Toolkit для IntelliJ toodevelop Spark приложений, написанных в Scala и их отправки tooan кластера HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Используйте набор средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight

Использовать hello набора средств Azure для приложений Spark toodevelop подключаемый модуль IntelliJ, написанных на Scala, а затем отправьте их tooan кластера HDInsight Spark непосредственно из hello IntelliJ интегрированной среды разработки (IDE). Можно использовать hello подключаемого модуля, несколькими способами:

* разрабатывать и отправлять приложения Scala Spark в кластер HDInsight Spark;
* получать доступ к ресурсам кластера Azure HDInsight Spark;
* разрабатывать и запускать приложения Scala Spark в локальной среде.

toocreate проекта, представление hello [создания приложений Spark с помощью средств Azure для IntelliJ hello](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) видео.

> [!IMPORTANT]
> Можно использовать этот подключаемый модуль toocreate и отправьте свои приложения только для кластера HDInsight Spark для Linux.
> 

## <a name="prerequisites"></a>Предварительные требования

- Кластер Apache Spark в HDInsight на платформе Linux. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).
- Комплект разработчика Oracle Java. Его можно установить из hello [веб-сайте Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. В этой статье используется версия 2017.1. Его можно установить из hello [JetBrains веб-сайт](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Установка набора средств Azure для IntelliJ
Инструкции по установке см. в статье [Установка набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-tooyour-azure-subscription"></a>Войдите в tooyour подписки Azure

1. Запустите hello IntelliJ интегрированной среды разработки и откройте обозреватель Azure. На hello **представление** выберите пункт **окна инструментов**, а затем выберите **обозреватель Azure**.
       
   ![ссылку Azure обозреватель Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Щелкните правой кнопкой мыши hello **Azure** узел, а затем выберите **входа**.

3. В hello **входа в Azure** установите флажок **входа**, а затем введите учетные данные Azure.

    ![Hello Azure входа в диалоговое окно](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. После подписи hello **подписки выберите** диалоговом появляется список всех hello подписок Azure, которые связаны с hello учетные данные. Выберите hello **выберите** кнопки.

    ![диалоговое окно Выбор подписки Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. На hello **обозреватель Azure** , раскройте **HDInsight** hello tooview кластеры HDInsight Spark, которые в вашей подписке.
   
    ![Кластеры HDInsight Spark в Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview hello ресурсов (например, учетные записи хранения), связанных с кластером hello, можно далее развернуть узел имя кластера.
   
    ![Развернутый узел имени кластера](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Запуск приложения Spark Scala в кластере HDInsight Spark

1. Запустите IntelliJ IDEA и создайте проект. В hello **новый проект** диалогового окна поле, hello следующие: 

   а. Выберите **HDInsight** > **Spark on HDInsight (Scala)** (Spark в HDInsight (Scala)).

   b. В hello **инструмент сборки** выберите либо hello следующие, tooyour потребность в соответствии с:

      * **Maven.** Для поддержки мастера создания проекта Scala.
      * **SBT**, для управления зависимостями hello и построения для проекта Scala hello

    ![диалоговое окно нового проекта Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Щелкните **Далее**.

3. Мастер создания проектов Scala Hello автоматически обнаруживает после установки hello Scala подключаемого модуля. Щелкните **Установить**.

   ![Проверка подключаемого модуля Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. hello toodownload Scala подключаемый модуль, выберите **ОК**. Следуйте инструкциям hello toorestart IntelliJ. 

   ![диалоговое окно приветствия подключаемого модуля Scala установки](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. В hello **новый проект** окне hello следующие:  

    ![При выборе hello Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   а. Введите имя и расположение проекта.

   b. В hello **проекта SDK** раскрывающемся списке выберите **Java 1.8** для кластера 2.x Spark hello, или выберите **Java 1.7** для hello Spark 1.x кластера.

   c. В hello **версии Spark** раскрывающегося списка, мастер создания проекта Scala интегрируется hello правильной версии пакета SDK Spark и Scala SDK. Если версия кластера Spark hello является более ранней, чем 2.0, выберите **усилить 1.x**. В противном случае выберите **Spark 2.x**. В этом примере используется **Spark 2.0.2 (Scala 2.11.8)**.

6. Выберите **Готово**.

7. Hello Spark проекта автоматически создается артефакта. артефакт tooview hello, hello следующие:

   а. На hello **файл** последовательно выберите пункты **структура проекта**.

   b. В hello **структура проекта** выберите **артефакты** tooview hello по умолчанию артефакт, который будет создан. Можно также создать свои собственные артефакта, выбрав hello "плюс" (**+**).

      ![Сведения о артефакта в диалоговое окно «hello»](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Добавьте исходный код приложения, выполнив hello ниже:

   а. Щелкните правой кнопкой мыши в обозревателе проектов **src**, слишком точки**New**и выберите **Scala класса**.
      
      ![Команды для создания класса Scala в обозревателе проектов](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. В hello **создать новый класс Scala** диалогового окна поле, укажите имя, выберите **объекта** в hello **вид** поле, а затем выберите **ОК**.
      
      ![Диалоговое окно создания класса Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. В hello **MyClusterApp.scala** файла, вставьте следующий код hello. Hello кода hello данные считываются из HVAC.csv (доступно на всех кластерах HDInsight Spark), извлекает hello строки, которые имеют только одну цифру в столбце седьмой hello в hello CSV-файл и записывает выходные данные hello слишком**/HVACOut** в группе по умолчанию hello Контейнер хранилища для кластера hello.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Запустите приложение hello в кластере HDInsight Spark, выполнив hello ниже:

   а. В обозревателе решений, щелкните правой кнопкой мыши имя проекта hello и выберите **tooHDInsight отправить приложение Spark**.
      
      ![Команда tooHDInsight отправить Spark приложения Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. Вы являются tooenter запрашиваемые учетные данные подписки Azure. В hello **отправки Spark** диалоговое окно, укажите следующие значения hello, а затем выберите **отправить**.
      
      * Для **усилить кластеров (Linux)**, выберите hello кластера HDInsight Spark, на котором будет toorun приложения.

      * Выберите артефакт проекта IntelliJ hello, или выберите его из hello жесткого диска.

      * В hello **имя класса Main** поле hello выберите кнопку с многоточием (**...** ), выберите основной класс hello в исходном коде приложения, а затем выберите **ОК**.

        ![диалоговое окно Выбор класса Main Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Так как в данном примере кода приложение hello не требуются аргументы командной строки или ссылаться на JAR-файлов или файлы, можно оставить hello оставшихся пустые поля. После ввода всех сведений hello, диалоговое окно «hello» должен быть похож hello после изображения.
        
        ![диалоговое окно отправки Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. Hello **отправки Spark** вкладку hello нижней части окна hello следует начинать отображение хода выполнения hello. Также можно остановить приложение hello, выбрав кнопку hello красным в hello **отправки Spark** окна.
      
      ![окна отправки Spark Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn tooaccess hello выходные данные задания, разделе hello «доступ и управление кластерами HDInsight Spark с помощью набора средств Azure для IntelliJ» далее в этой статье.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Запуск или отладка приложения Spark Scala в кластере HDInsight Spark
Также рекомендуется еще один способ отправки кластера toohello приложения hello Spark. Это можно сделать, задав параметры hello в hello **выполнения и отладки конфигураций** интегрированной среды разработки. Дополнительные сведения см. в статье [Удаленная отладка приложений Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Доступ к кластерам HDInsight Spark и управление ими с помощью набора средств Azure для IntelliJ
При помощи набора средств Azure для IntelliJ можно выполнять разные операции.

### <a name="access-hello-job-view"></a>Режим доступа к задания hello
1. В обозревателе Azure разверните **HDInsight**, разверните имя кластера Spark hello и выберите **задания**.  

    ![Узел представления задания](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. В правой области hello hello **представлении задания Spark** вкладка отображает все приложения hello, выполняющихся на кластере hello. Выберите имя hello приложения hello, для которого требуется toosee Дополнительные сведения см.

    ![Сведения о приложении](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay основные сведения, наведите на него схемы hello заданий. этапы graph tooview hello и информацию, которая создает каждого задания, выберите узел на диаграмме задания hello.

    ![Сведения об этапе задания](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview часто используемые журналы, такие как *Stderr драйвер*, *Stdout драйвер*, и *сведений о каталоге*выберите hello **журнала** вкладки.

    ![Подробные сведения журнала](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. Можно также просмотреть hello Spark журнала пользовательского интерфейса и hello YARN пользовательского интерфейса (на уровне приложения hello), выбрав ссылку hello верхней части окна hello.

### <a name="access-hello-spark-history-server"></a>Доступ к серверу журнал Spark hello
1. В Azure Explorer разверните **HDInsight**, щелкните имя кластера Spark правой кнопкой мыши и выберите **Open Spark History UI** (Открыть пользовательский интерфейс журнала Spark). 

2. Когда появится запрос, введите учетные данные администратора кластера hello, которых указан при настройке кластера hello.

3. На сервере мониторинга hello Spark журнала можно использовать для только что завершили выполнение приложения hello toolook имя приложения hello. В hello предшествующий код, можно задать имя приложения hello с помощью `val conf = new SparkConf().setAppName("MyClusterApp")`. Следовательно, приложение Spark называется **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Запустите портал Ambari hello
1. В Azure Explorer разверните **HDInsight**, щелкните имя кластера Spark правой кнопкой мыши и выберите **Open Cluster Management Portal (Ambari)** (Открыть портал управления кластерами (Ambari)). 

2. Когда появится запрос, введите учетные данные администратора hello hello кластера. Эти учетные данные указанным пользователем во время процесса установки кластера hello.

### <a name="manage-azure-subscriptions"></a>Управление подписками Azure
По умолчанию набор средств Azure для IntelliJ приведены кластеры Spark hello из всех подписок Azure. При необходимости можно указать hello подписок, которые должны tooaccess. 

1. В обозревателе Azure, щелкните правой кнопкой мыши hello **Azure** корневой узел, а затем выберите **управление подписками**. 

2. В диалоговом окне приветствия снимите подписок hello флажки Далее toohello, вы не хотите tooaccess, а затем выберите **закрыть**. Можно также выбрать **выйти** Если вам нужны toosign подписки Azure.

## <a name="run-a-spark-scala-application-locally"></a>Запуск приложения Spark Scala на локальном компьютере
Можно использовать набор средств Azure для приложений Spark Scala toorun IntelliJ локально на рабочей станции. Hello приложений обычно не требуется доступ к toocluster ресурсы, такие как контейнеры хранилища, и можно выполнить и проверить их локально.

### <a name="prerequisite"></a>Предварительные требования
Во время выполнения локального Spark Scala приложения hello на компьютере Windows может появиться исключение, как описано в статье [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Hello исключение возникает из-за отсутствия WinUtils.exe в Windows. 

tooresolve эту ошибку, [загрузить исполняемый hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa расположением, например **C:\WinUtils\bin**. Добавьте переменную среды hello **HADOOP_HOME**и задайте значение hello hello переменной слишком**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Запуск локального приложения Spark Scala
1. Запустите IntelliJ IDEA и создайте проект. 

2. В hello **новый проект** диалогового окна поле, hello следующие:
   
    а. Выберите **HDInsight** > **Spark on HDInsight Local Run Sample (Scala)** (Пример локального запуска Spark в HDInsight (Scala)).

    b. В hello **инструмент сборки** выберите либо hello следующие, tooyour потребность в соответствии с:

      * **Maven.** Для поддержки мастера создания проекта Scala.
      * **SBT**, для управления зависимостями hello и построения для проекта Scala hello

    ![диалоговое окно нового проекта Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Щелкните **Далее**.
 
4. В следующем окне приветствия hello следующие:
   
    а. Введите имя и расположение проекта.

    b. В hello **проекта SDK** раскрывающегося списка выберите версию Java, которая является более поздней, чем версия 1.7.

    c. В hello **версии Spark** раскрывающегося списка, выберите hello версию Scala нужных toouse: Scala 2.11.x Spark 2.0 или Scala 2.10.x для Spark 1.6.

    ![диалоговое окно нового проекта Hello](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. Выберите **Готово**.

6. пример кода добавляет шаблон Hello (**LogQuery**) в группе hello **src** папку, можно запустить локально на компьютере.
   
    ![Расположение LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Щелкните правой кнопкой мыши hello **LogQuery** приложение, а затем выберите **выполнения «LogQuery»**. На hello **запуска** вкладку внизу hello вывод hello следующим образом:
   
   ![Результат локального запуска приложения Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>Преобразование существующего toouse приложений IntelliJ ИДЕЯ набора средств Azure для IntelliJ
Можно преобразовать существующие Spark Scala приложения hello, созданных в toobe IntelliJ ИДЕЯ совместимые с Azure Toolkit для IntelliJ. Затем можно использовать hello подключаемый модуль toosubmit hello приложений tooan кластера HDInsight Spark.

1. Для существующих приложений Spark Scala, была создана с помощью IntelliJ ИДЕЯ откройте файл связанного .iml hello.

2. Hello корневой уровень является **модуль** элемент hello следующим образом:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Изменить элемент tooadd hello `UniqueKey="HDInsightTool"` таким образом, hello **модуль** элемент выглядит hello следующее:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Сохраните изменения hello. Ваше приложение станет совместимым с набором средств Azure для IntelliJ. Можно проверить его, щелкнув правой кнопкой мыши имя проекта hello в обозревателе проектов. во всплывающем меню Hello теперь имеет параметр hello **tooHDInsight отправить приложение Spark**.

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Ошибка *Please use a larger heap size* (Используйте больший размер кучи) в локальной среде
Если вы используете 32-разрядных Java SDK во время локального запуска в Spark 1.6, может возникнуть hello следующие ошибки:

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

Эти ошибки возникают потому, что размер кучи hello недостаточно велик для Spark toorun. Для Spark требуется не меньше 471 МБ. (Дополнительные сведения см. в статье о [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) Простое решение – toouse 64-разрядных Java SDK. Можно также изменить параметры виртуальной машины Java hello в IntelliJ путем добавления hello следующие параметры:

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Добавление параметров toohello поле «Параметры виртуальной Машины» в IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>Часто задаваемые вопросы
Выберите toosubmit хранилище Озера данных приложения tooAzure **Interactive** режим во время процесса hello Azure вход. Если выбрать **автоматический** режим, может произойти ошибка.

![Интерактивный вход](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

Теперь мы устранили ее. Вы можете toosubmit кластера Озера данных Azure приложения с помощью метода входа.

## <a name="feedback-and-known-issues"></a>Отзывы и известные проблемы
Сейчас просмотр выходных данных Spark напрямую не поддерживается.

С любыми отзывами и предложениями, а также в случае возникновения проблем при работе с этим подключаемым модулем вы можете отправить сообщение по электронному адресу hdivstool@microsoft.com.

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

### <a name="creating-and-running-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через виртуальную частную сеть](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

