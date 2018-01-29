---
title: "Выполнение запроса Hive с помощью драйвера JDBC в Azure HDInsight | Документы Майкрософт"
description: "Используйте драйвер JDBC из приложения Java для отправки запросов Hive в Hadoop на основе HDInsight. Подключение можно осуществлять программными средствами и из клиента SQL SQuirrel."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/28/2017
ms.author: larryfr
ms.openlocfilehash: 7da4a7e0a60fd1e5c78f53b0a8e7ab333c5d2465
ms.sourcegitcommit: 4bd369fc472dced985239aef736fece42fecfb3b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2018
---
# <a name="query-hive-through-the-jdbc-driver-in-hdinsight"></a>Выполнение запроса Hive с помощью драйвера JDBC в HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../../includes/hdinsight-selector-odbc-jdbc.md)]

Узнайте, как использовать драйвер JDBC из приложения Java для отправки запросов Hive в Hadoop на основе Azure HDInsight. Из этой статьи вы узнаете, как подключиться программным способом или из клиента SQuirreL SQL.

Дополнительные сведения об интерфейсе JDBC Hive см. в статье [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Технические условия

* Hadoop в кластере HDInsight. Работают кластеры либо под управлением Linux, либо под управлением Windows.

  > [!IMPORTANT]
  > Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий. Дополнительные сведения см. в разделе о [прекращении поддержки HDInsight 3.3](../hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL представляет собой клиентское приложение JDBC.

* [Java Developer Kit (JDK) версии 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) или более поздней версии.

* [Apache Maven](https://maven.apache.org). Maven — система сборки для проектов Java, используемая в проекте, связанном с данной статьей.

## <a name="jdbc-connection-string"></a>Строка подключения JDBC

Подключения JDBC к кластеру HDInsight в Azure осуществляются через порт 443, а защита трафика обеспечивается с помощью протокола SSL. Открытый шлюз, за которым находятся кластеры, перенаправляет трафик к порту, который фактически прослушивается HiveServer2. В следующей строке подключения показан формат для HDInsight:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Замените `CLUSTERNAME` на имя вашего кластера HDInsight.

## <a name="authentication"></a>Authentication

При установке подключения необходимо указать имя администратора кластера HDInsight и пароль для проверки подлинности в шлюзе кластера. При подключении клиентов JDBC, например SQuirreL SQL, необходимо ввести имя и пароль администратора в параметрах клиента.

При подключении из приложения Java необходимо использовать имя пользователя и пароль. Например, приведенный ниже код Java открывает новое подключение с помощью строки подключения, имени администратора и пароля:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Подключение с использованием клиента SQuirreL SQL

SQuirreL SQL — клиент JDBC, который можно использовать для удаленного выполнения запросов Hive с кластером HDInsight. В следующих шагах предполагается, что SQuirreL SQL уже установлен.

1. Скопируйте драйверы JDBC Hive из кластера HDInsight.

    * Чтобы скачать необходимые JAR-файлы, для кластера **HDInsight 3.5 или 3.6 под управлением Linux** сделайте следующее.

        1. Создайте каталог, содержащий файлы. Например, `mkdir hivedriver`.

        2. В командной строке выполните следующие команды, чтобы копировать файлы из кластера HDInsight.

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/lib/log4j-*.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/lib/slf4j-*.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-*-1.2*.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/httpclient-*.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/httpcore-*.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/libthrift-*.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/libfb*.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-logging-*.jar .
            ```

            Замените `USERNAME` именем учетной записи пользователя SSH для кластера. Замените `CLUSTERNAME` именем кластера HDInsight.

    * Чтобы скачать JAR-файлы, для **HDInsight под управлением Windows** сделайте следующее.

        1. На портале Azure выберите свой кластер HDInsight, а затем — значок **Удаленный рабочий стол**.

            ![Значок удаленного рабочего стола](./media/apache-hadoop-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. В разделе "Удаленный рабочий стол" нажмите кнопку **Подключить** для подключения к кластеру. Если значок "Удаленный рабочий стол" не включен, укажите имя пользователя и пароль в форме, а затем выберите **Включить**, чтобы включить значок "Удаленный рабочий стол" для кластера.

            ![Раздел "Удаленный рабочий стол"](./media/apache-hadoop-connect-hive-jdbc-driver/remotedesktopblade.png)

            После нажатия кнопки **Подключить** будет скачан RDP-файл. Используйте этот файл для запуска клиента удаленного рабочего стола. При появлении запроса укажите имя пользователя и пароль для доступа к удаленному рабочему столу.

        3. После подключения скопируйте следующие файлы из сеанса удаленного рабочего стола на локальный компьютер. Поместите их в локальный каталог с именем `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > Номера версий в путях и имена файлов для вашего кластера могут отличаться от указанных.

        4. После завершения копирования файлов отключите сеанс удаленного рабочего стола.

2. Запустите приложение SQuirreL SQL. В левой части окна выберите **Драйверы**.

    ![Вкладка "Драйверы" в левой части окна](./media/apache-hadoop-connect-hive-jdbc-driver/squirreldrivers.png)

3. Среди значков в верхней части диалогового окна **Drivers** (Драйверы) щелкните значок **+** для создания драйвера.

    ![Значки драйверов](./media/apache-hadoop-connect-hive-jdbc-driver/driversicons.png)

4. В диалоговом окне Add Driver (Добавление драйвера) укажите следующие сведения.

    * **Имя:** Hive.
    * **Пример URL-адреса:** `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Путь к дополнительным классам.** Нажмите кнопку "Добавить", чтобы добавить скачанные ранее JAR-файлы.
    * **Имя класса:** org.apache.hive.jdbc.HiveDriver.

   ![диалоговое окно "Добавить драйвер"](./media/apache-hadoop-connect-hive-jdbc-driver/adddriver.png)

   Нажмите кнопку **ОК**, чтобы сохранить эти параметры.

5. В левой части окна SQuirreL SQL выберите **Псевдонимы**. Затем щелкните значок **+**, чтобы создать псевдоним для подключения.

    ![добавление нового псевдонима](./media/apache-hadoop-connect-hive-jdbc-driver/aliases.png)

6. В диалоговом окне **Добавить псевдоним** укажите следующие значения.

    * **Имя:** Hive в HDInsight.

    * **Драйвер.** Выберите драйвер **Hive** в раскрывающемся списке.

    * **URL-адрес:** `jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2`

        Замените **CLUSTERNAME** именем кластера HDInsight.

    * **Имя пользователя.** Имя пользователя для учетной записи входа кластера HDInsight. Значение по умолчанию — `admin`.

    * **Пароль.** Пароль для учетной записи входа кластера.

 ![диалоговое окно "Добавить псевдоним"](./media/apache-hadoop-connect-hive-jdbc-driver/addalias.png)

    Нажмите кнопку **Проверить**, чтобы убедиться, что подключение работает. При появлении диалогового окна **Connect to: Hive on HDInsight** (Подключение: Hive в HDInsight) выберите **Подключиться**, чтобы выполнить проверку. Если проверка пройдет успешно, вы увидите диалоговое окно **Connection successful** (Подключение выполнено успешно). При возникновении ошибки см. раздел [Устранение неполадок](#troubleshooting).

    Чтобы сохранить псевдоним подключения, в нижней части диалогового окна **Add Alias** (Добавить псевдоним) нажмите кнопку **ОК**.

7. В раскрывающемся списке **Подключиться к** в верхней части окна SQuirreL SQL выберите **Hive on HDInsight** (Hive в HDInsight). При появлении запроса выберите **Подключиться**.

    ![диалоговое окно подключения](./media/apache-hadoop-connect-hive-jdbc-driver/connect.png)

8. После подключения введите следующий запрос в диалоговое окно запроса SQL, а затем нажмите кнопку **Запустить**. В области результатов должны появиться результаты запроса.

        select * from hivesampletable limit 10;

    ![диалоговое окно запроса SQL с результатами запроса](./media/apache-hadoop-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Подключение из примера приложения Java

Пример использования клиента Java для запроса Hive в HDInsight доступен на странице [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Следуйте инструкциям в репозитории, чтобы построить и запустить образец.

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a>Непредвиденная ошибка при попытке открыть подключение к SQL

**Признаки.** При подключении к кластеру HDInsight версии 3.3 или более поздней может появиться сообщение о возникновении непредвиденной ошибки. Трассировка стека для этой ошибки начинается со следующих строк:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Причина.** Эту ошибку вызывают прежние версии файла commons-codec.jar в составе SQuirreL.

**Решение.** Чтобы устранить эту ошибку, выполните приведенные далее действия.

1. Скачайте файл commons-codec.jar из кластера HDInsight.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. Закройте SQuirreL, а затем перейдите в каталог, где установлен SQuirreL. В каталоге SquirreL в каталоге `lib` замените существующий файл commons-codec.ja файлом, скачанным из кластера HDInsight.

3. Перезапустите SQuirreL. При последующих подключениях к Hive в HDInsight ошибка больше не должна возникать.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как использовать JDBC для работы с Hive, воспользуйтесь следующими ссылками, чтобы изучить другие способы работы с Azure HDInsight.

* [Визуализация данных Hive с помощью Microsoft Power BI в Azure HDInsight](apache-hadoop-connect-hive-power-bi.md).
* [Визуализация данных Hive интерактивного запроса с помощью Power BI в Azure HDInsight](../interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md).
* [Выполнение запросов Hive в Azure HDInsight с помощью Zeppelin](./../hdinsight-connect-hive-zeppelin.md)
* [Подключение Excel к Hadoop в Azure HDInsight с помощью Microsoft Hive ODBC Driver](apache-hadoop-connect-excel-hive-odbc-driver.md)
* [Подключение Excel к Hadoop с помощью Power Query](apache-hadoop-connect-excel-power-query.md)
* [Подключение к Azure HDInsight и выполнение запросов Hive с помощью средств Data Lake для Visual Studio](apache-hadoop-visual-studio-tools-get-started.md)
* [Использование средств Azure HDInsight для Visual Studio Code](../hdinsight-for-vscode.md).
* [Отправка данных в HDInsight](../hdinsight-upload-data.md)
* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование заданий MapReduce с HDInsight](hdinsight-use-mapreduce.md)
