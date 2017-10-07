---
title: "набор средств Azure для IntelliJ с песочницей Hortonworks aaaUse | Документы Microsoft"
description: "Дополнительные сведения о том, как toouse HDInsight средства в набор средств Azure для IntelliJ с Hortonworks \"песочницы\"."
keywords: "инструменты hadoop,запрос hive,intellij,песочница hortonworks,набор средств azure для intellij"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: b587cc9b-a41a-49ac-998f-b54d6c0bdfe0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 2bf97068a9cec99fcc7b4ff9469b91d8cbe2a8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-tools-for-intellij-with-hortonworks-sandbox"></a>Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks

Узнайте, как toouse средства HDInsight для приложений Apache Scala toodevelop IntelliJ и проверки hello приложений на [Hortonworks "песочницы"](http://hortonworks.com/products/sandbox/) на рабочей станции. 

[IntelliJ IDEA](https://www.jetbrains.com/idea/) — это интегрированная среда разработки (IDE) Java для разработки программного обеспечения для компьютеров. После разработки и тестирования приложения в "песочнице" Hortonworks, вы можете переместить их слишком[Azure HDInsight](hdinsight-hadoop-introduction.md).

## <a name="prerequisites"></a>Предварительные требования

Для работы с этим руководством вам потребуется:

- Платформа данных Hortonworks Data Platform 2.4 (HDP) в песочнице Hortonworks, выполняемая в локальной среде. в разделе tooconfigure HDP, [приступить к работе в экосистеме hello Hadoop с изолированной среде Hadoop на виртуальной машине](hdinsight-hadoop-emulator-get-started.md). 
    >[!NOTE]
    >Средства HDInsight для IntelliJ были протестированы только с HDP 2.4. Разверните tooget HDP 2.4 **Hortonworks "песочницы" архив** на hello [сайта загрузки для "песочницы" Hortonworks](http://hortonworks.com/downloads/#sandbox).

- [Java Developer Kit (JDK) версии 1.8 или более поздней версии](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). JDK требуется hello Azure Toolkit для IntelliJ.

- [ИДЕЯ IntelliJ community edition](https://www.jetbrains.com/idea/download) с hello [Scala](https://plugins.jetbrains.com/idea/plugin/1347-scala) подключаемого модуля и hello [средств Azure для IntelliJ](../azure-toolkit-for-intellij.md) подключаемого модуля. Средства HDInsight для IntelliJ доступен как часть средств Azure для IntelliJ hello. 

  tooinstall hello подключаемые модули, hello следующие:

  1. Откройте IntelliJ IDEA.
  2. На hello **приветствия** выберите **Настройка**, а затем выберите **подключаемых модулей**.
  3. Выберите **JetBrains установить подключаемый модуль** в левом нижнем углу hello.
  4. Использовать hello toosearch функции поиска для **Scala**, а затем выберите **установить**.
  5. Выберите **перезапустите ИДЕЯ IntelliJ** toocomplete hello установки.
  6. Повторите шаг 4 и 5 hello tooinstall **средств Azure для IntelliJ**. Дополнительные сведения см. в разделе [hello установки набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="create-a-spark-scala-application"></a>Создание приложения Spark Scala

В этом разделе с помощью IntelliJ IDEA создается пример проекта Scala. В следующем разделе hello свяжите ИДЕЯ IntelliJ toohello Hortonworks "песочницы" (эмулятора) перед отправкой hello проекта.

1. Откройте IntelliJ IDEA со своей рабочей станции. В hello **новый проект** диалогового окна поле, hello следующие:

   а. Выберите **HDInsight** > **Spark on HDInsight (Scala)** (Spark в HDInsight (Scala)).

   b. В hello **инструмент сборки** выберите либо hello следующие, tooyour потребность в соответствии с:

    * **Maven.** Для поддержки мастера создания проекта Scala.
    * **SBT**, для управления зависимостями hello и построения для проекта Scala hello

   ![диалоговое окно нового проекта Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project.png)

2. Щелкните **Далее**.

3. В hello Далее **новый проект** диалогового окна поле, hello следующие:

    ![Создание свойств проекта IntelliJ Scala](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-scala-project-properties.png)

    а. В hello **имя проекта** введите имя проекта.

    b. В hello **расположение проекта** введите расположение проекта.

    c. Далее toohello **проекта SDK** раскрывающемся списке выберите **New**выберите **JDK**, и укажите папку hello Java JDK версии 1.7 или более поздней версии. Выберите **Java 1.8** для кластера 2.x Spark hello, или выберите **Java 1.7** для hello Spark 1.x кластера. расположение по умолчанию Hello — C:\Program Files\Java\jdk1.8.x_xxx.

    d. В hello **версии Spark** раскрывающегося списка, мастер создания проекта Scala интегрируется hello правильной версии пакета SDK Spark и Scala SDK. Если версия кластера Spark hello является более ранней, чем 2.0, выберите **усилить 1.x**. В противном случае выберите **Spark 2.x**. В этом примере используется Spark 1.6.2 (Scala 2.10.5). Убедитесь, что вы используете помечен Scala репозитория hello 2.10.x. Не используйте репозиторий hello помечен Scala 2.11.x.

4. Выберите **Готово**.

5. Если hello **проекта** представление еще не открыта, нажмите клавишу **Alt + 1** tooopen его.

6. В **обозревателя проектов**, разверните проект hello и выберите **src**.

7. Щелкните правой кнопкой мыши **src**, слишком точки**New**и выберите **Scala класса**.

8. В hello **имя** введите имя в hello **тип** выберите **объекта**, а затем выберите **ОК**.

    ![Создайте новый класс Scala окна Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-create-new-scala-class.png)

9. В файле .scala hello вставьте hello, следующий код:

        import java.util.Random
        import org.apache.spark.{SparkConf, SparkContext}
        import org.apache.spark.SparkContext._

        /**
        * Usage: GroupByTest [numMappers] [numKVPairs] [valSize] [numReducers]
        */
        object GroupByTest {
            def main(args: Array[String]) {
                val sparkConf = new SparkConf().setAppName("GroupBy Test")
                var numMappers = 3
                var numKVPairs = 10
                var valSize = 10
                var numReducers = 2

                val sc = new SparkContext(sparkConf)

                val pairs1 = sc.parallelize(0 until numMappers, numMappers).flatMap { p =>
                val ranGen = new Random
                var arr1 = new Array[(Int, Array[Byte])](numKVPairs)
                for (i <- 0 until numKVPairs) {
                    val byteArr = new Array[Byte](valSize)
                    ranGen.nextBytes(byteArr)
                    arr1(i) = (ranGen.nextInt(Int.MaxValue), byteArr)
                }
                arr1
                }.cache
                // Enforce that everything has been calculated and in cache
                pairs1.count

                println(pairs1.groupByKey(numReducers).count)
            }
        }

10. На hello **построения** последовательно выберите пункты **построения проекта**. Убедитесь, что успешно завершена hello компиляции.


## <a name="link-toohello-hortonworks-sandbox"></a>Связать "песочницы" Hortonworks toohello

Прежде чем связывать tooa Hortonworks "песочницы" (эмулятора), необходимо иметь приложение IntelliJ.

Эмулятор tooan toolink, hello следующие:

1. Привет открыть проект в IntelliJ.

2. На hello **представление** выберите пункт **средства Windows**, а затем выберите **обозреватель Azure**.

3. Разверните **Azure**, щелкните правой кнопкой мыши **HDInsight**, а затем выберите **Link an Emulator** (Установить связь с эмулятором).

4. В hello **новый эмулятор ссылку** окно, введите пароль hello, настроенных для учетной записи корневой hello hello Hortonworks "песочницы", введите примерно toothose значения в следующий снимок экрана приветствия и выберите **ОК** . 

   ![окна «Связи новый эмулятор» Hello](./media/hdinsight-tools-for-intellij-with-hortonworks-sandbox/intellij-link-an-emulator.png)

5. Эмулятор hello tooconfigure, выберите **Да**.

Если подключения эмулятора hello hello эмулятор (Hortonworks "песочницы") отображается в узел HDInsight hello.

## <a name="submit-hello-spark-scala-application-toohello-hortonworks-sandbox"></a>Отправить toohello приложения hello Spark Scala Hortonworks "песочницы"

После связывания IntelliJ ИДЕЯ toohello эмулятора, вы можете отправить проекта.

toosubmit симулятор tooan проекта hello следующие:

1. В **обозревателя проектов**, щелкните правой кнопкой мыши проект hello и выберите **tooHDInsight приложения отправить Spark**.

2. Здравствуйте, следующие:

    а. В hello **кластера Spark (Linux)** раскрывающегося списка выберите локальный "песочницы" Hortonworks.

    b. В hello **имя класса Main** выберите или введите имя основного класса hello. В этом учебнике — имя hello **GroupByTest**.

3. Нажмите кнопку **Submit** (Отправить). журналы отправки заданий Hello отображаются в окне инструментов отправки Spark hello.

## <a name="next-steps"></a>Дальнейшие действия

- как toocreate приложений Spark для HDInsight с помощью средства HDInsight для IntelliJ, перейдите в слишком toolearn[используйте средства HDInsight в набор средств Azure для приложений Spark toocreate IntelliJ для кластера HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md).

- слишком go toowatch видео средства HDInsight для IntelliJ,[вводит средства HDInsight для IntelliJ для разработки Spark](https://www.youtube.com/watch?v=YTZzYVgut6c).

- toolearn как toodebug Spark приложений с помощью hello toolkit удаленно на HDInsight через SSH, перейдите слишком[удаленно отлаживать приложения Spark в кластере HDInsight с помощью набора средств Azure для IntelliJ через SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md).

- toolearn как toodebug Spark приложений с помощью hello toolkit удаленно на HDInsight через виртуальную частную сеть, перейдите слишком[используйте средства HDInsight в набор средств Azure для приложений Spark toodebug IntelliJ удаленно в кластере HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md).

- как toouse средства HDInsight для Eclipse toocreate приложении Spark go слишком toolearn[используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений](hdinsight-apache-spark-eclipse-tool-plugin.md).

- toowatch видео средства HDInsight для Eclipse, go слишком[использовать инструмент HDInsight Spark приложений Eclipse toocreate](https://mix.office.com/watch/1rau2mopb6fha).
