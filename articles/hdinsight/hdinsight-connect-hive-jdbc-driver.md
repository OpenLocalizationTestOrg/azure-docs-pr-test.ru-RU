---
title: "aaaQuery Hive через драйвер JDBC hello - Azure HDInsight | Документы Microsoft"
description: "Используйте драйвер JDBC hello от tooHadoop запросов приложения toosubmit Java Hive в HDInsight. Подключите программными средствами, а от клиента SQL белка hello."
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
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Запрос Hive через драйвер JDBC hello в HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Узнайте, как драйвер JDBC hello toouse из toosubmit приложения Java Hive запрашивает tooHadoop в Azure HDInsight. Hello сведения в этом документе показано, как tooconnect программно и с hello белка клиента SQL.

Дополнительные сведения о hello Hive интерфейса JDBC см. в разделе [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Предварительные требования

* Hadoop в кластере HDInsight. Работают кластеры либо под управлением Linux, либо под управлением Windows.

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе о [прекращении поддержки HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL представляет собой клиентское приложение JDBC.

* Hello [Java Developer Kit (JDK) версии 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) или более поздней версии.

* [Apache Maven](https://maven.apache.org). Maven — проект создания системы проектов Java, используемый hello проект, связанный с этой статьей.

## <a name="jdbc-connection-string"></a>Строка подключения JDBC

Кластер HDInsight tooan соединения JDBC на платформе Azure становятся более 443 и hello трафик защищается с помощью протокола SSL. Hello открытый шлюза, который hello кластеров находятся за перенаправляет hello трафика toohello порт, который HiveServer2 факта прослушивания. Hello ниже приведен пример строки подключения:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Замените `CLUSTERNAME` с hello имя кластера HDInsight.

## <a name="authentication"></a>Аутентификация

При установке соединения hello, необходимо использовать hello HDInsight кластер admin имя и пароль tooauthenticate toohello кластера шлюза. При соединении с JDBC клиентов, таких как белка SQL, необходимо ввести имя администратора hello и пароль в параметрах клиента.

Из приложения Java необходимо использовать hello имя и пароль при установлении соединения. Например hello ниже код Java открывает новое соединение с помощью строки подключения hello, имя администратора и пароль:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Подключение с использованием клиента SQuirreL SQL

Белка SQL является клиентом JDBC, может быть используется tooremotely выполнения запросов Hive с кластером HDInsight. Hello следующие шаги предполагают, что вы уже установили белка SQL.

1. Скопируйте драйверы Hive JDBC hello из кластера HDInsight.

    * Для **HDInsight под управлением Linux**, используйте hello следующие шаги, необходимые hello toodownload jar-файла.

        1. Создайте каталог, содержащий файлы hello. Например, `mkdir hivedriver`.

        2. Из командной строки используйте hello следующими командами toocopy hello файлы из кластера HDInsight hello:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Замените `USERNAME` с именем учетной записи пользователя hello SSH для hello кластера. Замените `CLUSTERNAME` с именем кластера HDInsight hello.

    * Для **HDInsight под управлением Windows**, используйте hello следующие шаги toodownload hello jar-файла.

        1. Из hello портал Azure, выберите ваш HDInsight кластер, а затем выберите hello **удаленного рабочего стола** значок.

            ![Значок удаленного рабочего стола](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. В колонке hello удаленного рабочего стола, используйте hello **Connect** кнопку tooconnect toohello кластера. Если hello удаленный рабочий стол не включен, используйте форму hello tooprovide имя пользователя и пароль, а затем выберите **включить** tooenable удаленного рабочего стола для кластера hello.

            ![Колонка удаленного рабочего стола](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            После нажатия кнопки **Подключить** будет скачан RDP-файл. Используйте этот клиент удаленного рабочего стола hello toolaunch файлов. При появлении запроса используйте hello имя пользователя и пароль для доступа к удаленному рабочему столу.

        3. После подключения, скопируйте следующие файлы с локального компьютера сеанса удаленного рабочего стола tooyour hello hello. Поместите их в локальный каталог с именем `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > версии Hello чисел, включенных в hello пути и имена файлов может быть разным для кластера.

        4. Отключение сеанса удаленного рабочего стола hello после завершения копирования файлов hello.

2. Запустите приложение hello белка SQL. Hello левого края окна hello, выберите **драйверы**.

    ![Hello левой части окна hello: вкладка драйверов](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Из значков hello вверху hello hello **драйверы** диалоговое окно, выберите hello  **+**  toocreate значок драйвера.

    ![Значки драйверов](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. В диалоговом окне Добавление драйвера hello добавьте hello следующую информацию:

    * **Имя:** Hive.
    * **Пример URL-адреса:** `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Дополнительный путь к классу**: используйте hello добавить кнопку tooadd hello jar-файла загружены ранее
    * **Имя класса:** org.apache.hive.jdbc.HiveDriver.

   ![диалоговое окно "Добавить драйвер"](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Нажмите кнопку **ОК** toosave эти параметры.

5. Hello левой части окна hello белка SQL, выберите **псевдонимы**. Нажмите кнопку hello  **+**  toocreate значок псевдоним соединения.

    ![добавление нового псевдонима](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. Используйте hello следующие значения для hello **добавить псевдоним** диалогового окна.

    * **Имя:** Hive в HDInsight.

    * **Драйвер**: раскрывающийся список tooselect используйте hello hello **Hive** драйвера

    * **URL-адрес**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Замените **CLUSTERNAME** с hello имя кластера HDInsight.

    * **Имя пользователя**: имя учетной записи входа hello кластера для кластера HDInsight. по умолчанию Hello — `admin`.

    * **Пароль**: hello пароль для учетной записи входа hello кластера.

 ![диалоговое окно "Добавить псевдоним"](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Используйте hello **тест** tooverify кнопки, hello подключение работает. При **соединиться: Hive в HDInsight** откроется диалоговое окно, выберите **Connect** tooperform hello теста. Если hello выполнен успешно, появится **подключение выполнено успешно** диалогового окна.

    подключение hello toosave псевдоним, использовать hello **ОК** кнопку внизу hello hello **добавить псевдоним** диалогового окна.

7. Из hello **подключиться к** выберите в раскрывающемся списке вверху hello SQL белка **Hive в HDInsight**. При появлении запроса выберите **Подключиться**.

    ![диалоговое окно подключения](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. После подключения введите hello ниже запроса в диалоговом окне запроса SQL hello, а затем выберите hello **запуска** значок. область результатов Hello должны показывать hello результаты запроса hello.

        select * from hivesampletable limit 10;

    ![диалоговое окно запроса SQL с результатами запроса](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Подключение из примера приложения Java

Пример использования tooquery клиента Java Hive в HDInsight доступна на [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Следуйте инструкциям hello toobuild репозитория hello и запуск образца hello.

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Произошла неожиданная ошибка при попытке tooopen SQL-соединение

**Симптомы**: при подключении кластера HDInsight tooan версии 3.3 или 3.4, может появиться сообщение об ошибке с произошла непредвиденная ошибка. Hello трассировку стека для этой ошибки начинается со слова hello, следующие строки:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Причина**: Эта ошибка возникает при несоответствии hello версию файла commons codec.jar hello, используемые белка и hello один необходимые компоненты Hive JDBC hello.

**Разрешение**: toofix эту ошибку, используйте hello следующие шаги:

1. Загрузите файл jar кодек commons hello с кластером HDInsight.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. Выйти из белка, а затем перейдите toohello directory установленным белка в вашей системе. В каталоге белка hello, hello `lib` directory замены hello существующих commons-codec.jar с hello загрузить один из кластера HDInsight hello.

3. Перезапустите SQuirreL. При подключении tooHive на HDInsight больше не возникает ошибка Hello.

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда вы узнали, как toouse toowork JDBC с Hive hello используйте следующие ссылки tooexplore toowork другими способами с Azure HDInsight.

* [Отправка данных tooHDInsight](hdinsight-upload-data.md)
* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование заданий MapReduce с HDInsight](hdinsight-use-mapreduce.md)
