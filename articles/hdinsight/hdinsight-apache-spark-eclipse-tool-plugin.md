---
title: "набор средств для Eclipse — Scala создание приложений для HDInsight Spark aaaAzure | Документы Microsoft"
description: "Использование средства HDInsight в набор средств Azure для Eclipse toodevelop Spark приложений, написанных в Scala и их отправки tooan кластера HDInsight Spark, непосредственно из их hello интегрированной среды разработки Eclipse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Используйте набор средств Azure для Eclipse toocreate Spark приложений для кластера HDInsight

Используйте средства HDInsight в набор средств Azure для Eclipse toodevelop Spark приложений, написанных в Scala и их отправки кластера Azure HDInsight Spark tooan, непосредственно из hello интегрированной среды разработки Eclipse. Можно использовать средства HDInsight hello подключаемого модуля, несколькими способами:

* toodevelop и отправка в приложении Scala Spark на кластере Spark в HDInsight
* tooaccess ресурсы кластера Azure HDInsight Spark
* toodevelop и запуск приложения Scala Spark в локально

> [!IMPORTANT]
> Это средство можно использовать toocreate и отправьте свои приложения только для кластера HDInsight Spark для Linux.
> 
> 

## <a name="prerequisites"></a>Предварительные требования

* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit версии 8, который используется для выполнения hello интегрированной среды разработки Eclipse. Его можно загрузить из hello [веб-сайте Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Интегрированная среда разработки Eclipse. В этой статье используется Eclipse Neon. Его можно установить из hello [Eclipse веб-сайт](https://www.eclipse.org/downloads/).   
* Пакет SDK для Spark. Скачать эту версию можно с [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Установка средства HDInsight в набор средств Azure для Eclipse и Scala подключаемого модуля
### <a name="install-hdinsight-tools"></a>Установка средств HDInsight
Средства HDInsight для Eclipse доступны в составе набора средств Azure для Eclipse. Инструкции по установке см. в статье [Установка набора средств Azure для Eclipse](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Установите подключаемый модуль Scala
При открытии hello Intellij hello средства HDInsight автоматически определяет, установлен ли подключаемый модуль Scala или не. Нажмите кнопку **ОК** toocontinue и следовать tooinstall hello инструкции по hello Eclipse Marketplace.

 ![Подключаемый модуль Scala установки автоматически](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Войдите в tooyour подписки Azure
1. Запуск интегрированной среды разработки Eclipse hello и откройте обозреватель Azure. На hello **окна** меню, нажмите кнопку **Показать представление**, а затем нажмите кнопку **других**. В hello открывшемся диалоговом окне, разверните **Azure**, нажмите кнопку **обозреватель Azure**, а затем нажмите кнопку **ОК**.

    ![Диалоговое окно Show View (Показать представление)](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Щелкните правой кнопкой мыши hello **Azure** узел, а затем нажмите кнопку **входа в**.
3. В hello **входа в Azure** диалоговое окно, выберите метод проверки подлинности hello щелкните **входа**и введите учетные данные Azure.
   
    ![Диалоговое окно входа в Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. После подписи hello **подписки выберите** диалоговом появляется список всех hello подписок Azure, связанных с учетными данными hello. Нажмите кнопку **выберите** hello tooclose-диалоговое окно.

    ![Диалоговое окно выбора подписок](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. На hello **обозреватель Azure** , раскройте **HDInsight** toosee hello кластеров HDInsight Spark под вашей подпиской.
   
    ![Кластеры HDInsight Spark в Azure Explorer](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. Далее можно развернуть имя узла toosee hello ресурсы кластера (например, учетные записи хранения) связанные с кластером hello.
   
    ![Расширение ресурсов toosee имени кластера](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Настройка проекта Spark Scala для кластера HDInsight Spark

1. В рабочей области интегрированной среды разработки Eclipse hello, нажмите кнопку **файл**, нажмите кнопку **New**, а затем нажмите кнопку **проекта**. 
2. В приветствия мастера создания проекта, разверните **HDInsight**выберите **Spark в HDInsight (Scala)**, а затем нажмите кнопку **Далее**.

    ![При выборе hello Spark на HDInsight (Scala) проекта](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. Hello Scala проект создания мастер автоматически обнаруживает ли установлен подключаемый модуль Scala или нет. Нажмите кнопку **ОК** toocontinue Загрузка подключаемого модуля Scala hello, а затем выполните hello инструкции toorestart Eclipse.

    ![Проверка Scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. В hello **новый проект Scala HDInsight** диалоговое окно, укажите следующие значения hello и нажмите кнопку **Далее**:
   * Введите имя для проекта hello.
   * В hello **JRE** область, убедитесь, что **использование среды выполнения JRE** задано слишком**JavaSE 1.7** или более поздней версии.
   * Убедитесь, что Spark SDK toohello месте, куда вы загрузили hello SDK. Hello загрузки toohello URL-адрес включается в hello [необходимые компоненты](#prerequisites) ранее в этой статье. Можно также загрузить hello SDK hello связи, включенные в диалоговое окно «hello».

    ![Диалоговое окно нового проекта Scala HDInsight](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  Hello Далее диалогового окна щелкните hello **библиотеки** и оставьте значения по умолчанию hello и нажмите кнопку **Готово**. 
   
    ![Вкладка Libraries (Библиотеки)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Создание приложения Scala для кластера HDInsight Spark

1. В hello интегрированной среды разработки Eclipse, из обозревателя пакета hello проекта, созданного ранее, щелкните правой кнопкой **src**, точки слишком**New**, а затем нажмите кнопку **других**.
2. В hello **выберите мастер** диалогового окна разверните **мастеров Scala**, нажмите кнопку **объекта Scala**и нажмите кнопку **Далее**.
   
    ![Диалоговое окно выбора мастера](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. В hello **создать новый файл** диалоговое окно, введите имя для hello объекта и нажмите кнопку **Готово**.
   
    ![Диалоговое окно создания нового файла](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Вставьте следующий код в текстовом редакторе hello hello:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Запустите приложение hello в кластере HDInsight Spark:
   
   1. Из обозревателя пакета, щелкните правой кнопкой мыши имя проекта hello и выберите **tooHDInsight отправить приложение Spark**.        
   2. В hello **отправки Spark** диалоговое окно, укажите следующие значения hello и нажмите кнопку **отправить**:
      
      * Для **имя кластера**, выберите hello кластера HDInsight Spark, на котором будет toorun приложения.
      * Выберите артефакта из проектов Eclipse hello, или выберите его с жесткого диска. значение по умолчанию Hello зависит от элемента hello, щелкнуть правой кнопкой мыши в обозревателе пакетов.
      * В hello **имя класса Main** dropdownlist отправки мастер отображает все имена объектов из выбранного проекта. Выбрать или ввести один нужных toorun. При выборе артефакта с жесткого диска необходимо указать имя класса main самостоятельно. 
      * Так как в данном примере кода приложение hello не требуют аргументов командной строки или ссылаться на JAR-файлов или файлы, можно оставить hello оставшихся пустые текстовые поля.
        
       ![Диалоговое окно Spark Submission (Отправка в Spark)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. Hello **отправки Spark** вкладку следует начать отображение хода выполнения hello. Можно остановить приложение hello, нажав кнопку hello красным в hello **отправки Spark** окна. Можно также просмотреть журналы hello для данного конкретного приложения, выполнить, щелкнув значок глобуса hello (обозначается синей рамки hello hello изображения).
      
       ![Окно Spark Submission (Отправка в Spark)](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Доступ к кластерам HDInsight Spark и управление ими с помощью средств HDInsight в наборе средств Azure для Eclipse
Можно выполнять различные операции с помощью средства HDInsight, включая доступ к hello выходные данные задания.

### <a name="access-hello-job-view"></a>Режим доступа к задания hello
1. В обозревателе Azure разверните **HDInsight**, разверните имя кластера Spark hello и нажмите кнопку **задания**. 

    ![Узел представления задания](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Щелкните hello **заданий** узла. Средства HDInsight Hello автоматически обнаруживает ли установлен подключаемый модуль clipse E (fx) hello или нет. Нажмите кнопку **ОК** toocontinue и следуйте инструкциям hello tooinstall hello Eclipse Marketplace и перезапустите Eclipse.

    ![Установка E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Откройте представление задания hello из hello **заданий** узла. В правой области hello hello **представлении задания Spark** вкладка отображает все приложения hello, выполняющихся на кластере hello. Щелкните имя hello приложения hello, для которого требуется toosee Дополнительные сведения см.

    ![Сведения о приложении](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. При наведении указателя мыши на диаграмме hello задания отображается базовые сведения выполняющегося задания. Щелкните задание graph hello отобразить граф этапы hello и информация, что приводит к возникновению ошибки каждого задания.

    ![Сведения об этапе задания](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Часто используемые журналов, включая Stderr драйвера, драйвер Stdout и сведений о каталоге, перечислены в hello **журнала** вкладки.

    ![Подробные сведения журнала](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. Hello Spark журнала пользовательского интерфейса и hello YARN пользовательского интерфейса (на уровне приложения hello) также можно открыть, щелкнув гиперссылку соответствующих hello hello верхней части окна hello.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Контейнер хранилища hello доступа для кластера hello
1. В обозревателе Azure разверните hello **HDInsight** toosee корневой узел список кластеров HDInsight Spark, доступны.
2. Разверните узел учетной записи хранилища hello toosee в имени кластера hello и hello контейнер хранилища по умолчанию для кластера hello.
   
    ![Учетная запись хранения и контейнер по умолчанию](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Щелкните имя контейнера хранилища hello, связанные с кластером hello. Hello правой панели дважды щелкните hello **HVACOut** папки. Откройте один из hello **часть -** файлы toosee hello выходные данные приложения hello.

### <a name="access-hello-spark-history-server"></a>Доступ к серверу журнал Spark hello
1. В Azure Explorer щелкните имя кластера Spark правой кнопкой мыши и выберите пункт **Open Spark History UI** (Открыть пользовательский интерфейс журнала Spark). Когда появится запрос, введите учетные данные администратора hello hello кластера. Необходимо указать эти при подготовке кластера hello.
2. В панели мониторинга сервера журнал Spark hello используется toolook имя приложения hello для только что завершили выполнение приложения hello. В hello предшествующий код, можно задать имя приложения hello с помощью `val conf = new SparkConf().setAppName("MyClusterApp")`. Следовательно, приложение Spark называлось **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Запустите портал Ambari hello
1. В Azure Explorer щелкните имя кластера Spark правой кнопкой мыши и выберите пункт **Open Cluster Management Portal (Ambari)** (Открыть портал управления кластерами (Ambari)). 
2. Когда появится запрос, введите учетные данные администратора hello hello кластера. Необходимо указать эти при подготовке кластера hello.

### <a name="manage-azure-subscriptions"></a>Управление подписками Azure
По умолчанию средства HDInsight в набор средств Azure для Eclipse приведены кластеры Spark hello из всех подписок Azure. При необходимости можно указать hello подписки, для которых требуется tooaccess hello кластера. 

1. В обозревателе Azure, щелкните правой кнопкой мыши hello **Azure** корневой узел, а затем нажмите кнопку **управление подписками**. 
2. В диалоговом окне приветствия снять флажки hello hello подписки, не требуется tooaccess, а затем выберите **закрыть**. Можно также щелкнуть **выйти** Если вам нужны toosign подписки Azure.

## <a name="run-a-spark-scala-application-locally"></a>Запуск приложения Spark Scala на локальном компьютере
Можно использовать средства HDInsight в набор средств Azure для Eclipse toorun Spark Scala приложений локально на рабочей станции. Как правило эти приложения не требуется доступ к ресурсам toocluster, таких как контейнер хранилища, и можно выполнить и проверить их локально.

### <a name="prerequisite"></a>Предварительные требования
Во время выполнения локального Spark Scala приложения hello на компьютере Windows, может возникнуть исключение, как описано в статье [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Это исключение возникает, так как в Windows отсутствует файл **WinUtils.exe**. 

tooresolve эту ошибку, необходимо [загрузить исполняемый hello](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) расположение tooa **C:\WinUtils\bin**. Затем необходимо добавить переменную среды hello **HADOOP_HOME** и задайте значение hello hello переменной слишком**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Запуск локального приложения Spark Scala
1. Запустите Eclipse и создайте новый проект. В hello **новый проект** диалоговое окно, внесите следующие варианты hello и нажмите кнопку **Далее**.
   
   * Выберите в левой области hello **HDInsight**.
   * Выберите в правой области hello **Spark в HDInsight локального запуска образца (Scala)**.

    ![Диалоговое окно "Новый проект"](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. Здравствуйте, сведениями о проекте hello tooprovide, повторите шаги 3 – 6 из ранее [настройки проекта Spark Scala для HDInsight Spark кластера](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. пример кода добавляет шаблон Hello (**LogQuery**) в группе hello **src** папку, можно запустить локально на компьютере.
   
    ![Расположение LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Щелкните правой кнопкой мыши hello **LogQuery** приложения, точки слишком**Запуск от имени**и нажмите кнопку **1 приложение Scala**. Вы увидите выходные данные следующим образом в hello **консоли** вкладку внизу hello:
   
   ![Результат локального запуска приложения Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>Часто задаваемые вопросы
Выберите toosubmit хранилище Озера данных приложения tooAzure **Interactive** режим во время процесса hello Azure вход. Если выбрать **автоматический** режим, может произойти ошибка.

![Интерактивный вход](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

Теперь мы устранили ее. Вы можете toosubmit кластера Озера данных Azure приложения с помощью метода входа.

## <a name="feedback-and-known-issues"></a>Отзывы и известные проблемы
Сейчас просмотр выходных данных Spark напрямую не поддерживается.

Если любые отзывы и предложения, или если возникли проблемы при использовании этого инструмента, вы бесплатно toosend нам по адресу hdivstool@microsoft.com.

## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Используйте набор средств Azure для IntelliJ toocreate и отправка Spark Scala приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через виртуальную частную сеть](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

