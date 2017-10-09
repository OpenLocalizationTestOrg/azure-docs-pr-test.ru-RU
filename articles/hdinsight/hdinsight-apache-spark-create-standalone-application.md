---
title: "toorun приложения Scala aaaCreate в кластерах Spark - Azure HDInsight | Документы Microsoft"
description: "Создайте приложение Spark языке Scala с помощью Apache Maven как hello построения системы и существующие архетипа Maven для Scala, предоставляемые IntelliJ ИДЕЯ."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>Создание приложения Scala Maven toorun на кластере Apache Spark в HDInsight

Узнайте, как toocreate Spark приложения, написанного на Scala использование Maven с IntelliJ ИДЕЯ. статья Hello использует Apache Maven как hello системы сборки и начинается с существующие архетипа Maven для Scala, предоставляемые IntelliJ ИДЕЯ.  Создание приложения Scala в IntelliJ ИДЕЯ состоит hello следующие шаги:

* Используйте Maven как система сборки hello.
* Обновление зависимостей модуля Spark tooresolve файла модели объекта проекта (POM).
* написание приложения на языке Scala;
* Создания файла JAR-файл, который может быть отправленной tooHDInsight Spark кластеров.
* Запустите приложение hello на кластере Spark с помощью Livy.

> [!NOTE]
> HDInsight также предоставляет IntelliJ ИДЕЯ подключаемого модуля средства tooease hello процесс создания и отправки приложения tooan кластера Spark на HDInsight в Linux. Дополнительные сведения см. в разделе [использование подключаемого модуля средства HDInsight для toocreate IntelliJ ИДЕЯ и отправки приложения Spark](hdinsight-apache-spark-intellij-tool-plugin.md).
> 
> 

## <a name="prerequisites"></a>Предварительные требования

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).
* Комплект разработчика Oracle Java. Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Java IDE. В этой статье используется среда IntelliJ IDEA 15.0.1. Его можно установить [отсюда](https://www.jetbrains.com/idea/download/).

## <a name="install-scala-plugin-for-intellij-idea"></a>Установка подключаемого модуля Scala для IntelliJ IDEA
Если ПРЕДСТАВЛЕНИЕ IntelliJ установки была не запрашивает Включение Scala подключаемого модуля, запустите IntelliJ ИДЕЯ и выполните следующие шаги tooinstall hello, подключаемый модуль hello:

1. Запустите IntelliJ IDEA и на экране приветствия щелкните **Configure** (Настройка), а затем — **Plugins** (Подключаемые модули).
   
    ![Включение подключаемого модуля Scala](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. В следующем экране приветствия щелкните **JetBrains установить подключаемый модуль** в левом нижнем углу hello. В hello **Обзор подключаемых модулей JetBrains** диалоговым окном, которое открывается, поиск Scala и нажмите кнопку **установить**.
   
    ![Установка подключаемого модуля Scala](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. После успешной установки подключаемого модуля hello щелкните hello **кнопкой перезапустить ИДЕЯ IntelliJ** toorestart hello интегрированной среды разработки.

## <a name="create-a-standalone-scala-project"></a>Создание автономного проекта Scala
1. Запустите IntelliJ IDEA и создайте проект. В hello нового диалогового окна, сделайте hello следующие варианты, а затем нажмите кнопку **Далее**.
   
    ![Создание проекта Maven](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * Выберите **Maven** hello тип проекта.
   * Выберите пакет в поле **Project SDK** (Пакет SDK проекта). Нажмите кнопку Создать и перейдите в каталог установки Java toohello, обычно `C:\Program Files\Java\jdk1.8.0_66`.
   * Выберите hello **из архетипа** параметр.
   * Список archetypes hello, выберите **org.scala tools.archetypes:scala архетипа простой**. Будет создан структура каталога hello и загрузите программу Scala toowrite зависимостей по умолчанию hello требуется.
2. Введите соответствующие значения для параметров **GroupId**, **ArtifactId** и **Version**. Щелкните **Далее**.
3. В hello Далее диалоговое окно, где указываются домашний каталог Maven и другие пользовательские настройки, примите значения по умолчанию hello и нажмите кнопку **Далее**.
4. В последней диалоговое окно «hello», укажите имя и расположение проекта и нажмите кнопку **Готово**.
5. Удалить hello **MySpec.Scala** файл **src\test\scala\com\microsoft\spark\example**. Это не требуется для приложения hello.
6. При необходимости переименуйте файлов исходного кода и тестирования по умолчанию hello. Hello левой панели hello IntelliJ ПРЕДСТАВЛЕНИЕ, перейти слишком**src\main\scala\com.microsoft.spark.example**. Щелкните правой кнопкой мыши **App.scala**, нажмите кнопку **рефакторинг**, щелкните переименовать файл и в диалоговом окне приветствия предоставляют hello новое имя для приложения hello и нажмите кнопку **рефакторинг**.
   
    ![Переименование файлов](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. В последующих шагах hello обновит hello pom.xml toodefine hello зависимости для hello Spark Scala приложения. Для этих зависимостей toobe загружаются и разрешить автоматически, необходимо соответствующим образом настроить Maven.
   
    ![Настройка автоматической загрузки Maven](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. Из hello **файл** меню, нажмите кнопку **параметры**.
   2. В hello **параметры** диалоговом окне перейдите слишком**, выполнение построения, развертывания** > **средства построения** > **Maven**  >  **Импорта**.
   3. Выберите параметр hello слишком**Maven импорта проектов автоматически**.
   4. Нажмите кнопку **Применить**, а затем — **ОК**.
8. Обновите исходный файл hello Scala tooinclude код вашего приложения. Откройте и замените существующий образец кода с hello после кода hello и сохранить изменения hello. Этот код считывает данные hello из hello HVAC.csv (доступно на всех кластерах HDInsight Spark), извлекает hello строки, которые имеют только одну цифру шестому столбцу hello и записывает выходные данные hello слишком**/HVACOut** в группе хранения по умолчанию hello контейнер для hello кластера.
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. Обновите hello pom.xml.
   
   1. В пределах `<project>\<properties>` добавьте hello следующее:
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. В пределах `<project>\<dependencies>` добавьте hello следующее:
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      Сохраните изменения toopom.xml.
10. Создайте hello JAR-файлу. IntelliJ IDEA позволяет создавать JAR-файлы в качестве артефактов проекта. Выполните следующие шаги hello.
    
    1. Из hello **файл** меню, нажмите кнопку **структура проекта**.
    2. В hello **структура проекта** диалоговое окно, нажмите кнопку **артефакты** и нажмите кнопку hello, а также символ. Hello всплывающее диалоговое окно, щелкните **JAR**, а затем нажмите кнопку **из модулей с зависимостями**.
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. В hello **создать JAR из модулей** диалоговое окно, нажмите кнопку с многоточием hello (![многоточие](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) от hello **класс Main**.
    4. В hello **выберите класс Main** диалоговое окно, выберите hello класс, который отображается по умолчанию и нажмите кнопку **ОК**.
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. В hello **создать JAR из модулей** диалогового окна поле, убедитесь, что этот параметр hello слишком**извлечения целевого toohello JAR** выбран и нажмите кнопку **ОК**. В результате будет создан один JAR-файл, содержащий все зависимости.
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. Hello вывода макета вкладке перечисляются все hello файлов, которые включены в состав проекта Maven hello. Можно выбрать и удалить hello, на которой другие hello Scala приложения имеет нет прямой зависимости. Для приложения hello, мы создаем здесь, можно удалить все, кроме hello последним (**SparkSimpleApp компиляции выходной**). Выберите toodelete hello JAR-файлов и нажмите кнопку hello **удалить** значок.
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        Убедитесь, что **сборки в проверьте** флажок, который гарантирует, что jar hello создаются каждый раз, hello проекта будут созданы или обновлены. Нажмите кнопку **Применить**, а затем — **ОК**.
    7. На панели меню hello, нажмите кнопку **построения**и нажмите кнопку **сделать проект**. Можно также щелкнуть **артефакты сборки** toocreate hello jar. Hello JAR-выходной файл будет создан в разделе **\out\artifacts**.
       
        ![Создание JAR-файла](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Запустите приложение hello на кластере Spark hello
приложение hello toorun hello кластере, необходимо выполнить следующие hello:

* **Копирования hello приложения jar toohello хранилища Azure BLOB-объекта** связанные с кластером hello. Можно использовать [ **AzCopy**](../storage/common/storage-use-azcopy.md), Командная строка программы, toodo таким образом. Существует много других клиентов также можно использовать tooupload данных. Дополнительные сведения о них см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).
* **Удаленно использовать Livy toosubmit задание приложения** toohello кластера Spark. Кластеры Spark на HDInsight включает Livy, предоставляющую отправить tooremotely конечные точки REST Spark заданий. Дополнительные сведения см. в статье [Удаленная отправка заданий Spark в кластер Apache Spark в HDInsight на платформе Linux с помощью Livy](hdinsight-apache-spark-livy-rest-interface.md).

## <a name="next-step"></a>Дальнейшие действия

В этой статье вы узнали, каким образом toocreate приложении scala Spark. Предварительное toohello далее в статье toolearn как toorun кластера с помощью Livy этого приложения на HDInsight Spark.

> [!div class="nextstepaction"]
>[Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

