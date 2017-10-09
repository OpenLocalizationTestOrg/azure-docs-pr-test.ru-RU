---
title: "aaaUse Apache Spark потоковой передачи с концентраторами событий в Azure HDInsight | Документы Microsoft"
description: "Постройте Apache Spark потоковой передачи потока tooAzure концентратора событий и затем получения этих событий в кластере HDInsight Spark с помощью приложения scala toosend данных."
keywords: "потоковая передача apache spark, потоковая передача spark, пример приложения spark, пример приложения потоковой передачи apache spark, пример концентратора событий azure, пример приложения spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a>Потоковая передача Apache Spark. Обработка данных из концентраторов событий Azure с помощью кластера Spark в HDInsight

В этой статье создайте Apache Spark, образец, который включает в себя следующие шаги hello потоковой передачи:

1. Использовать автономные приложения tooingest сообщений в концентратор событий Azure.

2. С два различных подхода получения сообщений hello из концентратора событий в режиме реального времени с помощью приложения, запущенного в кластере Spark на Azure HDInsight.

3. Построение потоковой передачи конвейеры аналитических систем хранения toodifferent toopersist данных или получения сведений из данных на лету hello.

## <a name="prerequisites"></a>Предварительные требования

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="spark-streaming-concepts"></a>Основные понятия потоковой передачи Spark

Подробное описание потоковой передачи Spark см. в [этом разделе](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview). HDInsight переводит hello кластера же потоковой передачи tooa функции Spark на Azure.  

## <a name="what-does-this-solution-do"></a>Каково предназначение этого решения?

В этой статье toocreate пример для потоковой передачи Spark выполните следующие шаги hello.

1. Создание концентратора событий Azure, который будет принимать поток событий.

2. Запуск локального автономное приложение, приводит к возникновению события и помещает его toohello концентратор событий Azure. Пример приложения Hello, делает это опубликованы по адресу [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).

3. Удаленно запустите в кластере Spark приложение потоковой передачи, которое считывает потоковые события из концентратора событий Azure и выполняет различные задачи обработки и анализа данных.

## <a name="create-an-azure-event-hub"></a>Создание концентратора событий Azure

1. Войдите на toohello [портала Azure](https://ms.portal.azure.com)и нажмите кнопку **New** на hello верхнего левого угла экрана приветствия.

2. Последовательно выберите **Интернет вещей** и **Концентраторы событий**.

    ![Создание концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Создание концентратора событий для примера приложения потоковой передачи Spark")

3. В hello **создать пространство имен** колонки, введите имя пространства имен. Выберите hello ценовой категории (Basic или Standard). Кроме того, в какой ресурс hello toocreate выберите подписки Azure, группа ресурсов и расположение. Нажмите кнопку **создать** toocreate приветствия имен.

      ![Указание имени концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Указание имени концентратора событий для примера приложения потоковой передачи Spark")

    > [!NOTE]
    > Вы должны выбрать hello же **расположение** как кластера Apache Spark в HDInsight tooreduce задержки и затраты.
    >
    >

4. В списке имен hello концентраторов событий выберите пространство имен созданного hello.      


5. В колонке hello пространства имен, щелкните **концентраторов событий**, а затем нажмите кнопку **+ концентратора событий** toocreate новый концентратор событий.
   
    ![Создание концентратора событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Создание концентратора событий для примера приложения потоковой передачи Spark")

6. Введите имя для концентратора событий, набор hello секции count too10 и too1 хранения сообщений. Мы не архивация выполняется сообщений hello в этом решении, оставьте hello rest по умолчанию и нажмите кнопку **создать**.
   
    ![Указание сведений о концентраторе событий для примера приложения потоковой передачи Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Указание сведений о концентраторе событий для примера приложения потоковой передачи Spark")

7. в колонке hello концентратора событий перечислены Hello вновь созданные концентратора событий.
    
     ![Просмотр концентратор событий для потоковой передачи пример hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "представление концентратор событий для hello Поместите здесь пример потоковой передачи")

8. В колонке hello пространства имен (не hello конкретного концентратора событий колонку), нажмите кнопку **политики общего доступа**, а затем нажмите кнопку **RootManageSharedAccessKey**.
    
     ![Установка политики концентратора событий для потоковой передачи пример hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "концентратора событий набор политик для hello Поместите здесь пример потоковой передачи")

9. Нажмите кнопку toocopy hello копирования hello **RootManageSharedAccessKey** первичный ключ и соединения строки toohello буфер обмена. Сохраните эти toouse далее в учебнике hello.
    
     ![Просмотр ключей политики концентратора событий для потоковой передачи пример hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "ключей политики концентратора событий представления для hello Поместите здесь пример потоковой передачи")

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a>Отправка сообщений tooAzure концентратора событий с помощью Scala примера приложения

В этом разделе используется изолированный локальное Scala приложение, приводит к возникновению ошибки потока событий и отправляет его tooAzure концентратора событий, которое было создано ранее. Это приложение доступно на сайте GitHub по адресу [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer). Hello здесь предполагается, что уже разделенными этот репозиторий GitHub.

1. Убедитесь, что у вас есть hello установлены следующие компоненты на компьютере hello, где выполняется это приложение.

    * Комплект разработчика Oracle Java. Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
    * Apache Maven. Скачать эту версию можно [здесь](https://maven.apache.org/download.cgi). Доступные инструкции tooinstall Maven [здесь](https://maven.apache.org/install.html).

2. Откройте командную строку и перейдите toohello расположение клонировать hello в репозитории GitHub для приложения Scala образец hello и запустите следующие команды toobuild hello приложения hello.

        mvn package

3. Hello jar выходных данных для приложения hello **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, будет создан в разделе **/target-** каталога. Далее в этой статье tootest hello полнофункциональную этот JAR-ФАЙЛ используется.

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a>Создания приложения tooreceive сообщений из концентратора событий в кластере Spark 

Имеется два подхода tooconnect, потоковая передача Spark и концентраторов событий Azure, подключение на основе приемника и Direct DStream-подключения на основе. Direct DStream на основе появился на января 2017 года, в выпуске hello 2.0.3. Он должен tooreplace hello исходного получателя подключения на основе как он обеспечивает более высокую производительность и эффективность ресурсов. Дополнительные сведения см. на странице [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs). Direct DStream поддерживает только Spark 2.0 и более поздние версии.

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a>Создание приложений с помощью соединителя toospark eventhubs hello зависимостей

Также мы опубликуем hello, промежуточные версии Spark EventHubs в GitHub. toouse hello промежуточной версии Spark EventHubs, hello первым шагом является tooindicate GitHub как hello источник репозитория, добавив следующие записи toopom.xml hello.

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

Затем можно добавить следующие предварительные выпуски версия зависимости tooyour проекта tootake hello hello.

Зависимость Maven

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

Зависимость SBT

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a>Подключение Direct DStream

Предварительно собранный JAR-файл, содержащий примеры использования Direct DStream, можно скачать по адресу [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).

Hello jar-файл содержит три примера, исходный код можно найти по адресу [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).

Рассмотрим [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) в качестве примера.

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

В hello в приведенном выше примере `eventhubParameters` один экземпляр EventHubs hello параметры конкретного tooa и у вас toopass его toohello `createDirectStreams` API, который создает имен прямой DStream объекта сопоставления tooa концентраторов событий. Над объектом прямой DStream hello можно вызвать любой DStream API, предоставляемые платформой Spark потоковый API-Интерфейс. В этом примере вычислять hello частоту каждого слова hello последнего пакета 3 micro интервалами.

### <a name="receiver-based-connection"></a>Подключение на основе получателя

Spark, пример приложения, написанного на Scala, который получает события и назначения toodifferent hello маршрутов, потоковая передача доступна на [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples). Выполните действия hello ниже приложения hello tooupdate конфигурации концентратора событий и создайте jar hello выходных данных.

1. Запустите IntelliJ ИДЕЯ и из hello Выбор экрана запуска **извлечь из системы управления версиями** и нажмите кнопку **Git**.
   
    ![Пример приложения потоковой передачи Apache Spark. Получение источников из Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Пример приложения потоковой передачи Apache Spark. Получение источников из Git")

2. В hello **клона репозитория** диалоговом предоставляют hello URL-адрес toohello Git из репозитория tooclone, укажите tooclone directory hello для и нажмите кнопку **клон**.
   
    ![Пример приложения потоковой передачи Apache Spark. Клонирование из Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Пример приложения потоковой передачи Apache Spark. Клонирование из Git")
3. Следуйте инструкциям hello, пока проект hello полностью клонируется. Нажмите клавишу **Alt + 1** tooopen hello **представления проекта**. Она должна иметь вид hello следующее.
   
    ![Пример приложения потоковой передачи Apache Spark. Представление проекта](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Пример приложения потоковой передачи Apache Spark. Представление проекта")
4. Убедитесь, что код приложения hello компилируется с помощью Java8. tooensure, нажмите кнопку **файл**, нажмите кнопку **структура проекта**и на hello **проекта** , убедитесь, что уровень языка проекта задано слишком**8 - лямбда-выражения, тип заметки, т. д.**.
   
    ![Пример приложения потоковой передачи Apache Spark. Настройка компилятора](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Пример приложения потоковой передачи Apache Spark. Настройка компилятора")
5. Откройте hello **pom.xml** и убедитесь, что выбрана правильная версия Spark hello. В разделе `<properties>` узел, найдите следующий фрагмент кода hello и проверить версию Spark hello.

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. приложение Hello требует зависимостей JAR-файл называется **JAR-файл драйвера JDBC**. Это обязательный toowrite сообщений hello, полученные от концентратора событий в базе данных Azure SQL. Этот JAR-файл (версии 4.1 или более поздней) можно скачать [здесь](https://msdn.microsoft.com/sqlserver/aa937724.aspx). Добавьте jar toothis ссылку в библиотеке проектов hello. Выполните следующие шаги hello.
     
     1. Щелкните в окне IntelliJ ИДЕЯ при наличии приложения hello откройте **файл**, нажмите кнопку **структура проекта**и нажмите кнопку **библиотеки**. 
     2. Щелкните hello значок добавления (![значок добавления](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), нажмите кнопку **Java**, а затем переходить toohello расположение, куда вы загрузили JAR-файл драйвера JDBC hello. Выполните запросы hello tooadd hello jar файла toohello проекта библиотеки.

         ![добавление отсутствующих зависимостей](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Добавление отсутствующих JAR-файлов зависимостей")
     3. Нажмите кнопку **Применить**.

7. Создайте выходной hello jar-файл. Выполните следующие шаги hello.

   1. В hello **структура проекта** диалоговое окно, нажмите кнопку **артефакты** и нажмите кнопку hello, а также символ. Hello всплывающее диалоговое окно, щелкните **JAR**, а затем нажмите кнопку **из модулей с зависимостями**.      
       
       ![Пример приложения потоковой передачи Apache Spark. Создание JAR-файла](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Пример приложения потоковой передачи Apache Spark. Создание JAR-файла")
   2. В hello **создать JAR из модулей** диалоговое окно, нажмите кнопку с многоточием hello (![многоточие](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) от hello **класс Main**.
   3. В hello **выберите класс Main** диалоговое окно, выберите любой из доступных классов hello и нажмите кнопку **ОК**.
      
       ![Пример приложения потоковой передачи Apache Spark. Выбор класса JAR-файла](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Пример приложения потоковой передачи Apache Spark. Выбор класса JAR-файла")
   4. В hello **создать JAR из модулей** диалогового окна поле, убедитесь, что этот параметр hello слишком**извлечения целевого toohello JAR** выбран и нажмите кнопку **ОК**. В результате будет создан один JAR-файл, содержащий все зависимости.
      
       ![Пример приложения потоковой передачи Apache Spark. Создание JAR-файла на основе модулей](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Пример приложения потоковой передачи Apache Spark. Создание JAR-файла на основе модулей")
   5. Hello **макета вывода** вкладке перечисляются все hello файлов, которые включены в состав проекта Maven hello. Можно выбрать и удалить hello, на которой другие hello Scala приложения имеет нет прямой зависимости. Для приложения hello, мы создаем здесь, можно удалить все, кроме hello последним (**spark-потоковой передачи--сохраняемости примеры данных компиляции выходной**). Выберите toodelete hello JAR-файлов и нажмите кнопку hello **удаление** значок (![значок удаления](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).
      
       ![Пример приложения потоковой передачи Apache Spark. Удаление извлеченных JAR-файлов](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Пример приложения потоковой передачи Apache Spark. Удаление извлеченных JAR-файлов")
      
       Убедитесь, что **сборки в проверьте** флажок, который гарантирует, что jar hello создаются каждый раз, hello проекта будут созданы или обновлены. Нажмите кнопку **Применить**.
   6. В hello **макета вывода** вкладки справа внизу hello hello **доступные элементы** поле, у вас есть jar SQL JDBC hello, добавленные ранее toohello проекта библиотеки. Необходимо добавить этот toohello **макета вывода** вкладки. Щелкните правой кнопкой мыши hello jar-файл и нажмите кнопку **извлечения в выходных данных корневой**.
      
       ![Пример приложения потоковой передачи Apache Spark. Извлечение JAR-файла зависимостей](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Пример приложения потоковой передачи Apache Spark. Извлечение JAR-файла зависимостей")  
      
       Hello **макета вывода** вкладка теперь должна выглядеть следующим образом.
      
       ![Пример приложения потоковой передачи Apache Spark. Вкладка окончательных выходных данных](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Пример приложения потоковой передачи Apache Spark. Вкладка окончательных выходных данных")        
      
       В hello **структура проекта** диалоговое окно, нажмите кнопку **применить** и нажмите кнопку **ОК**.    
   7. На панели меню hello, нажмите кнопку **построения**и нажмите кнопку **сделать проект**. Можно также щелкнуть **артефакты сборки** toocreate hello jar. Hello JAR-выходной файл будет создан в разделе **\classes\artifacts**.
      
       ![Пример приложения потоковой передачи Apache Spark. Выходной JAR-файл](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Пример приложения потоковой передачи Apache Spark. Выходной JAR-файл")

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a>Удаленно запускать приложения hello на кластере Spark, с помощью Livy

В этой статье используется потоковой передачи приложения hello toorun Apache Spark Livy удаленно на кластере Spark. Подробные сведения об как кластера toouse Livy с HDInsight Spark. в разделе [отправки заданий удаленно tooan Apache Spark кластера в Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md). Перед запуском приложение hello Spark потоковой передачи, существует несколько факторов, которые нужно выполнить.

1. Запуск событий toogenerate hello локального автономного приложения и отправляются tooEvent концентратора. Используйте hello следующая команда toodo так:

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. Потоковая передача jar hello копирования (**spark-потоковой передачи данные сохраняемости examples.jar,**) toohello хранилище больших двоичных объектов Azure, связанном с hello кластера. Это делает tooLivy доступен jar hello. Можно использовать [ **AzCopy**](../storage/common/storage-use-azcopy.md), Командная строка программы, toodo таким образом. Существует много других клиентов можно использовать tooupload данных. Дополнительные сведения о них см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).
3. Установите ПЕРЕЛИСТЫВАНИЕ на компьютере hello, где выполняются эти приложения с. Мы используем hello tooinvoke ПЕРЕЛИСТЫВАНИЕ hello toorun Livy конечных точек удаленного задания.

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a>Запуска hello события hello Spark потоковой передачи приложения tooreceive в BLOB-объект хранилища Azure в виде текста

Откройте командную строку, перейдите в каталог toohello, где установлены ПЕРЕЛИСТЫВАНИЕ и запустите следующую команду (замените имя пользователя и пароль и кластера имя) hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Здравствуйте, параметры в файле hello **inputBlob.txt** определяется следующим образом:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Сообщите нам понять, каковы параметры hello во входном файле hello:

* **файл** является hello путь toohello приложения jar-файл в учетной записи хранилища Azure hello, связанные с кластером hello.
* **className** — hello имя класса hello в банке hello.
* **args** — список hello аргументы, необходимые для класса hello
* **numExecutors** — hello количество ядер, используемых потоковой передачи приложения hello toorun Spark. Всегда должно быть по крайней мере дважды hello количество секций концентратора событий.
* **executorMemory**, **executorCores**, **driverMemory** — это ресурсы tooassign необходимые параметры, используемые toohello потоковой передачи приложения.

> [!NOTE]
> Не обязательно toocreate hello выходные папки (EventCheckpoint, EventCount или EventCount10), используемые в качестве параметров. Потоковая передача приложения Hello создает их.
>
>

При выполнении команды hello, вы увидите, что выход hello следующим образом:

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

Запишите идентификатор пакета hello в последней строке hello hello выходных данных (в этом примере это "1"). tooverify, hello приложения выполняется успешно, можно взглянуть на вашей учетной записи хранилища Azure, связанные с кластером hello и вы увидите hello **/EventCount/EventCount10** папки там создается. Эта папка должна содержать большие двоичные объекты, которые перехватывает hello количество событий, обработанных в hello периода времени, заданного для параметра hello **пакета интервал в секундах**.

Hello Spark потоковой передачи приложения будет продолжено toorun, пока не удалите его. Таким образом, toodo используйте hello следующую команду:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a>Приложения hello tooreceive hello события выполнения в BLOB-объект хранилища Azure как JSON
Откройте командную строку, перейдите в каталог toohello, где установлены ПЕРЕЛИСТЫВАНИЕ и запустите следующую команду (замените имя пользователя и пароль и кластера имя) hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Здравствуйте, параметры в файле hello **inputJSON.txt** определяется следующим образом:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Hello параметры, аналогичные toowhat, указанное для hello текстовый вывод в предыдущем шаге hello. Опять же необязательно toocreate hello выходные папки (EventCheckpoint, EventCount или EventCount10), используемые в качестве параметров. Потоковая передача приложения Hello создает их.

 После выполнения команды hello, вы можете воспользоваться вашей учетной записи хранилища Azure, связанные с кластером hello и вы увидите hello **/EventStore10** папки там создается. Откройте любой файл с префиксом **часть -** и вы увидите hello событий, обработанных в формате JSON.

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a>Запускать приложения hello tooreceive hello события в таблицу Hive
Некоторые дополнительные компоненты, необходимые toorun hello Spark потоковой передачи приложений, который потоки событий в куст таблицу вы. а именно:

* datanucleus-api-jdo-3.2.6.jar;
* datanucleus-rdbms-3.2.9.jar;
* datanucleus-core-3.2.10.jar;
* hive-site.xml

Hello **.jar** файлы доступны в кластере HDInsight Spark на `/usr/hdp/current/spark-client/lib`. Hello **hive-site.xml** доступен на `/usr/hdp/current/spark-client/conf`.

Можно использовать [WinScp](http://winscp.net/eng/download.php) toocopy эти файлы с локального компьютера hello кластера tooyour. Затем можно использовать средства toocopy эти файлы по tooyour учетной записи хранения, связанные с кластером hello. Дополнительные сведения о как tooupload файлы toohello учетной записи хранения см. в разделе [передать данные для заданий Hadoop в HDInsight](hdinsight-upload-data.md).

После копирования через tooyour файлы hello учетной записи хранилища Azure, откройте командную строку, перейдите toohello каталог, где установлены ПЕРЕЛИСТЫВАНИЕ и выполните следующую команду (замените имя пользователя и пароль и кластера имя) hello:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Здравствуйте, параметры в файле hello **inputHive.txt** определяется следующим образом:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

Hello параметры, аналогичные toowhat, указанное для hello текстовый вывод в предыдущих шагах hello. Еще раз, нет необходимости toocreate hello выходной папки (EventCheckpoint, EventCount или EventCount10) или hello вывод таблицу Hive (EventHiveTable10), которые используются в качестве параметров. Потоковая передача приложения Hello создает их. Обратите внимание, что hello **JAR-файлов** и **файлы** параметр включает в себя файлы .jar toohello пути и hello hive-site.xml, скопированными с перекрытием toohello учетной записи хранилища.

tooverify, таблица hive hello успешно создан, можно SSH в кластере hello и выполнения запросов Hive. Инструкции см. в статье [Использование Hive с Hadoop в HDInsight с применением протокола SSH](hdinsight-hadoop-use-hive-ssh.md). После установления соединения с помощью SSH можно запустить следующие команды tooverify hello таблицу Hive hello и **EventHiveTable10**, создается.

    show tables;

Вы должны увидеть следующие выходные данные как toohello.

    OK
    eventhivetable10
    hivesampletable

Можно также запустите запрос SELECT tooview hello содержимое таблицы hello.

    SELECT * FROM eventhivetable10 LIMIT 10;

Вы должны увидеть результаты hello следующим образом:

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a>Запускать приложения hello tooreceive hello события в таблицу базы данных Azure SQL
Прежде чем выполнять этот шаг, убедитесь, что у вас есть созданная база данных SQL Azure. Инструкции см. в статье [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../sql-database/sql-database-get-started.md). toocomplete в этом разделе, требуются значения для имени базы данных, имя сервера базы данных и учетные данные администратора hello базы данных в качестве параметров. Не требуется таблица базы данных hello toocreate хотя. Hello приложения потоковой Spark, будет создан.

Откройте командную строку, перейдите в каталог toohello, где установлены ПЕРЕЛИСТЫВАНИЕ и выполните hello следующую команду:

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

Здравствуйте, параметры в файле hello **inputSQL.txt** определяется следующим образом:

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

tooverify, приложение hello выполняется успешно, можно подключить toohello базы данных Azure SQL с помощью SQL Server Management Studio. Дополнительные сведения о toodo, в разделе [подключения tooSQL базы данных с SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md). После toohello подключенной базы данных, можно переходить toohello **EventContent** таблицы, созданные потоковой передачи приложения hello. Можно запустить tooget hello быстрого запроса данных из таблицы hello. Выполните приветствия при следующем запросе:

    SELECT * FROM EventCount

Вы увидите примерно toohello следующие выходные данные:

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)
* [Проектирование подключения на основе приемника и Direct DStream](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
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
[azure-create-storageaccount]: ../storage-create-storage-account/
