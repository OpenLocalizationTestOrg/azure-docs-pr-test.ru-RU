---
title: "набор средств для IntelliJ - отладки приложений удаленно на HDInsight Spark aaaAzure | Документы Microsoft"
description: "Узнайте, как использовать средства HDInsight в набор средств Azure для IntelliJ tooremotely отладки приложений, работающих в кластерах HDInsight Spark через виртуальную частную сеть."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Используйте набор средств Azure для приложений toodebug IntelliJ удаленно на HDInsight Spark через виртуальную частную сеть

Мы рекомендуем hello способ отладки spark applicaltion удаленно с помощью ssh. Инструкции см. в статье [Удаленная отладка приложений Spark в кластере HDInsight через SSH с помощью набора средств Azure для IntelliJ](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

В этой статье приводятся пошаговые инструкции о предоставлении toouse hello средства HDInsight в набор средств Azure для IntelliJ toosubmit задания Spark на HDInsight Spark кластера и затем выполните отладку удаленно с компьютера. toodo таким образом, необходимо выполнить следующие общие действия hello:

1. Создание виртуальной сети Azure типа "сеть — сеть" или "точка — сеть". Hello в этом документе предполагается использовать сетевой сайт сайт.
2. Создайте кластер Spark в HDInsight Azure, который является частью hello-сайтами Azure виртуальной сети.
3. Проверьте сетевое подключение hello между головному узлу кластера hello и рабочим столом.
4. Создание приложения Scala в IntelliJ IDEA и его настройка для удаленной отладки.
5. Запускать и отлаживать приложения hello.

## <a name="prerequisites"></a>Предварительные требования
* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).
* Комплект разработчика Oracle Java. Его можно установить [отсюда](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. В этой статье используется версия 2017.1. Его можно установить [отсюда](https://www.jetbrains.com/idea/download/).
* Средства HDInsight в наборе средств Azure для IntelliJ. Средства HDInsight для IntelliJ доступны как часть средств Azure для IntelliJ hello. Инструкции как tooinstall hello набора средств Azure см. в разделе [hello установка набора средств Azure для IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Войдите в подписку Azure из IntelliJ IDEA. Следуйте инструкциям hello [здесь](hdinsight-apache-spark-intellij-tool-plugin.md).
* При выполнении приложения Spark Scala для удаленной отладки на компьютере Windows, может возникнуть исключение, как описано в статье [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) это происходит из-за отсутствующих tooa WinUtils.exe в Windows. toowork возникновения этой ошибки необходимо [скачать hello исполняемый здесь](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) расположение tooa **C:\WinUtils\bin**. Затем необходимо добавить переменную среды **HADOOP_HOME** и задайте значение hello hello переменной слишком**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Шаг 1. Создание виртуальной сети Azure
Следуйте инструкциям hello hello ниже ссылки toocreate виртуальной сети Azure, а затем проверьте подключением hello hello desktop и виртуальной сети Azure.

* [Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью портала Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Настроить подключение точка сеть tooa виртуальной сети, с помощью PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Шаг 2. Создание кластера HDInsight Spark
Также следует создать кластер Apache Spark на Azure HDInsight, являющегося частью hello, созданную виртуальную сеть Azure. Используйте hello информация, доступная [под управлением Linux, создания кластеров в HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Как часть дополнительной конфигурации выберите виртуальную сеть Azure, созданную в предыдущем шаге hello hello.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Шаг 3: Проверьте подключение hello между головному узлу кластера hello и рабочего стола
1. Получите IP-адрес hello головному узлу hello. Откройте Ambari пользовательского интерфейса для hello кластера. Из колонки hello кластера, нажмите кнопку **мониторинга**.

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. Hello Ambari пользовательского интерфейса, в правом верхнем углу hello, щелкните **узлов**.

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Отобразится список головных узлов, рабочих узлов и узлов zookeeper. Hello headnodes имеют hello **hn*** префикс. Щелкните первый головному узлу hello.

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. Hello нижней части страницы hello, которое открывается из hello **Сводка** поле копирования hello IP-адрес головному узлу hello и имя узла hello.

    ![Поиск IP-адреса головного узла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Включить hello IP-адрес и имя узла hello hello головному узлу toohello **узлов** файл на компьютере hello, который нужно toorun и hello Spark заданий для удаленной отладки. Это позволит вам toocommunicate с hello головному узлу с помощью hello IP-адрес, а также имя узла hello.

   1. Откройте блокнот с повышенным уровнем разрешений. В меню "файл" hello, выберите **откройте** , а затем toohello расположение файла hosts hello. На компьютере под управлением Windows это папка `C:\Windows\System32\Drivers\etc\hosts`.
   2. Добавьте следующие toohello hello **узлов** файла.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. С hello компьютера, подключенного toohello виртуальной сети Azure, используемой кластером HDInsight hello проверьте связи обоих headnodes hello, с помощью hello IP-адрес, а также имя узла hello.
7. SSH в hello головному узлу кластера с помощью инструкций hello в [кластера HDInsight tooan соединение, с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md). С hello головному узлу кластера проверьте связь с IP-адрес hello hello настольного компьютера. Следует проверить подключение tooboth hello IP-адресов, назначенных toohello компьютера, один для hello сетевого подключения и hello других для hello виртуальной сети Azure, hello компьютер подключен к.
8. Повторите шаги hello для hello других головному узлу.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Шаг 4: Создание приложения Spark Scala со средствами HDInsight hello в набор средств Azure для IntelliJ и настройте его для удаленной отладки
1. Запустите IntelliJ IDEA и создайте проект. В hello нового диалогового окна, сделайте hello следующие варианты, а затем нажмите кнопку **Далее**.

    ![Создание приложения Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * Hello левой панели выберите **HDInsight**.
   * Hello правой области выберите **Spark в HDInsight (Scala)**.
   * Щелкните **Далее**.
2. В следующем окне приветствия укажите следующие сведения о проекте hello и нажмите кнопку **Готово**.  
   - Введите имя и расположение проекта.
   - Для параметра **Project SDK** (Пакет SDK проекта) выберите Java 1.8 для кластера Spark 2.x или Java 1.7 для кластера Spark 1.x.
   - Для параметра **Spark Version** (Версия Spark) мастер создания проекта Scala интегрирует правильную версию пакета SDK Spark и пакета SDK Scala. Если версия кластера spark hello ниже 2.0, выберите любые блестящие 1.x. В противном случае следует выбрать Spark 2.x. В этом примере используется Spark 2.0.2 (Scala 2.11.8).
       ![Создание приложения Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. Hello Spark проекта автоматически создаст артефакта. артефакт hello toosee, выполните следующие действия.

   1. Из hello **файл** меню, нажмите кнопку **структура проекта**.
   2. В hello **структура проекта** диалоговое окно, нажмите кнопку **артефакты** toosee hello по умолчанию артефакт, который будет создан.
   ![Создание JAR-файла](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      Можно также создать свои собственные артефакта bly, щелкнув hello  **+**  значок, выделяются в выше рисунке hello.

4. Добавьте проект библиотеки tooyour. Щелкните правой кнопкой мыши имя проекта hello в дереве проекта hello tooadd библиотеки и нажмите кнопку **открыть параметры модуля**. В hello **структура проекта** диалогового окна hello левой панели щелкните **библиотеки**, щелкните символ hello (+) и нажмите кнопку **из Maven**.

    ![Добавление библиотеки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    В hello **загрузка библиотеки из репозитория Maven** диалогового окна поле, поиск и добавить следующие библиотеки hello.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Копировать `yarn-site.xml` и `core-site.xml` из hello головному узлу кластера и добавить его в проект toohello. Используйте следующие команды toocopy hello файлы hello. Можно использовать [Cygwin](https://cygwin.com/install.html) toorun hello следующие `scp` команды toocopy hello файлы из кластера headnodes hello.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Так как мы уже добавлена hello кластера головному узлу IP адрес и имена узлов fo hello файл hosts на рабочем столе hello, мы используем hello **scp** команд в следующие способом hello.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Добавление проекта tooyour этих файлов, скопировав их в списке hello **/src** папки в дереве проекта, например `<your project directory>\src`.
6. Обновление hello `core-site.xml` toomake hello следующие отличия.

   1. `core-site.xml`включает шифрование hello учетной записи хранилища ключей toohello связанные с кластером hello. В hello `core-site.xml` добавления проекта toohello, замените hello зашифрованный ключ с ключом hello фактического хранения, связанный с учетной записью хранилища по умолчанию hello. Ознакомьтесь с разделом [Управление ключами доступа к хранилищу](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Удалите следующую записей из hello hello `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Сохраните файл hello.
7. Добавьте класс hello Main для вашего приложения. Из hello **обозревателя проектов**, щелкните правой кнопкой мыши **src**, слишком точки**New**и нажмите кнопку **Scala класса**.

    ![Добавить исходный код](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. В hello **создать новый класс Scala** диалогового окна введите имя, **вид** выберите **объекта**и нажмите кнопку **ОК**.

    ![Добавить исходный код](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. В hello `MyClusterAppMain.scala` файл, вставьте следующий код hello. Этот код создает контекст Spark hello и запускает `executeJob` метод hello `SparkSample` объекта.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Повторите шаги 8 и 9 над именем объекта Scala tooadd `SparkSample`. Класс toothis добавить hello, следующий код. Этот код считывает данные hello из hello HVAC.csv (доступно на всех кластерах HDInsight Spark), извлекает hello строки, которые имеют только одну цифру hello седьмой столбца в hello CSV и записывает выходные данные hello слишком**/HVACOut** в группе по умолчанию hello Контейнер хранилища для кластера hello.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Повторите шаги 8 и 9 выше tooadd новый класс с именем `RemoteClusterDebugging`. Этот класс реализует платформа тестирования hello Spark, которая используется для отладки приложений. Добавьте следующий код toohello hello `RemoteClusterDebugging` класса.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Несколько важных событий toonote здесь:

   * Для `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, убедитесь, что hello Spark сборки JAR-ФАЙЛ можно найти в хранилище кластера hello по указанному пути hello.
   * Для `setJars`, укажите расположение hello, где будут создаваться jar артефакта hello. Обычно это `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. В hello `RemoteClusterDebugging` класса, щелкните правой кнопкой мыши hello `test` ключевое слово и выберите **Создание конфигурации RemoteClusterDebugging**.

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. В диалоговом окне приветствия укажите имя для конфигурации hello и выберите hello **проверить тип** как **имя теста**. Оставьте остальные значения, установленные по умолчанию, нажмите кнопку **Применить**, а затем — кнопку **ОК**.

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Теперь вы увидите **удаленного запуска** конфигурации раскрывающееся меню в строке меню hello.

    ![Создание удаленной конфигурации](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>Шаг 5: Запуск приложения hello в режиме отладки
1. Откройте в проекте IntelliJ ИДЕЯ `SparkSample.scala` и создать точку останова следующей too'val rdd1 ". Во всплывающем меню hello для создания точки останова, выберите **строку в функции executeJob**.

    ![Добавление точки останова](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Щелкните hello **отладки запуска** кнопку Далее toohello **удаленного запуска** toostart раскрывающийся список конфигурации запущено приложение hello.

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Когда выполнение программы hello достигает точки останова hello, вы увидите **отладчик** вкладку в нижней области hello.

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Нажмите кнопку hello (**+**) tooadd значок контрольного значения, как показано в приведенном ниже рисунке hello.

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Здесь, так как приложение hello было передано до hello переменной `rdd1` был создан с помощью этого контрольного значения, мы видим, что являются hello первые 5 строк в переменную hello `rdd`. Нажмите клавишу **ВВОД**.

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    В приведенном выше изображении hello это представление, во время выполнения, может запросить terrabytes данных и отладки как работы вашего приложения. Например, в hello выводу, приведенному выше рисунке hello, вы увидите, hello первую строку hello выходных данных является заголовком. Исходя из этого, можно изменить в строку заголовка кода tooskip приложения hello при необходимости.
5. Теперь можно нажать hello **программы Resume** tooproceed значок с запустить приложение.

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Если приложение hello завершается успешно, вы увидите выход hello следующим образом.

    ![Запустите программу hello в режиме отладки](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Демонстрация
* Создание проекта Scala (видео): [создание приложений Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Удаленной отладки (видео): [используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно на кластер HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

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
* [Использование средства HDInsight в набор средств Azure для IntelliJ toocreate и отправка Spark Scala основных приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Используйте набор средств Azure для приложений Spark toodebug IntelliJ удаленно через SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Использование инструментов HDInsight для IntelliJ с песочницей Hortonworks](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Используйте средства HDInsight в набор средств Azure для Eclipse toocreate Spark приложений](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)
