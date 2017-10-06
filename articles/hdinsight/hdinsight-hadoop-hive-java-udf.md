---
title: "aaaJava определяемой пользователем функции (UDF) с Hive в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toocreate на основе Java определяемой пользователем функции (UDF), который работает с Hive. В этом примере определяемая пользователем Функция преобразует таблицу toolowercase строки текста."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Работа с определяемыми пользователем функциями Java с использованием Hive в HDInsight

Узнайте, как toocreate на основе Java определяемой пользователем функции (UDF), который работает с Hive. Hello Java определяемой пользователем функции в этом примере преобразует таблицу символов нижнего регистра tooall строки текста.

## <a name="requirements"></a>Требования

* Кластер HDInsight. 

    > [!IMPORTANT]
    > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

    Большинство действий, описываемых в этой статье, можно выполнять в кластерах как на основе Windows, так и на основе Linux. Однако hello этапы tooupload hello скомпилирован кластера toohello определяемой пользователем функции и запустить его, определенных кластеров на основе tooLinux. Tooinformation, который может использоваться с кластерами под управлением Windows, приводятся соответствующие ссылки.

* Пакет [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 или более поздней версии (или эквивалентный пакет, например OpenJDK).

* [Apache Maven](http://maven.apache.org/)

* Текстовый редактор или Java IDE.

    > [!IMPORTANT]
    > При создании hello Python файлы на клиенте Windows, необходимо использовать редактор, который использует LF в качестве конца строки. Если вы не уверены, использует ли редактора LF или CRLF, в разделе hello [Устранение неполадок](#troubleshooting) раздел для действия по удалению hello символов CR.

## <a name="create-an-example-java-udf"></a>Создание примера определяемой пользователем функции Java 

1. Из командной строки используйте следующие toocreate новый проект Maven hello.

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > При использовании PowerShell необходимо поместить в кавычки hello параметров. Например, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    Эта команда создает каталог с именем **exampleudf**, которая содержит проект Maven hello.

2. После создания проекта hello удалить hello **exampleudf/src/test** каталогом, созданным в рамках проекта hello.

3. Откройте hello **exampleudf/pom.xml**и заменить существующий hello `<dependencies>` запись с hello следующий XML-код:

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    Эти записи указывают версию hello Hadoop и Hive, входящий в состав HDInsight 3.5. Можно найти сведения о версиях hello Hadoop и Hive, предоставляемую с HDInsight hello [управление версиями компонента HDInsight](hdinsight-component-versioning.md) документа.

    Добавить `<build>` раздел перед hello `</project>` строку hello конец файла hello. В этом разделе, должны иметь hello следующий XML-код:

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                        </transformer>
                    </transformers>
                    <!-- Keep us from getting a bad signature error -->
                    <filters>
                        <filter>
                            <artifact>*:*</artifact>
                            <excludes>
                                <exclude>META-INF/*.SF</exclude>
                                <exclude>META-INF/*.DSA</exclude>
                                <exclude>META-INF/*.RSA</exclude>
                            </excludes>
                        </filter>
                    </filters>
                </configuration>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ```

    Эти записи определяют, как toobuild hello проекта. В частности, hello версию Java, hello проекте используется и как toobuild uberjar для развертывания кластера toohello.

    Сохраните файл hello, когда были внесены изменения hello.

4. Переименуйте **exampleudf/src/main/java/com/microsoft/examples/App.java** слишком**ExampleUDF.java**, а затем откройте файл hello в редакторе.

5. Замените содержимое hello hello **ExampleUDF.java** следующие hello-файл, а затем сохраните файл hello.

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    Этот код реализует определяемой пользователем функции, которая принимает строковое значение и возвращает версия hello строки в нижний регистр.

## <a name="build-and-install-hello-udf"></a>Создание и установка hello определяемой пользователем функции.

1. Используйте следующие команды toocompile hello и пакета hello определяемой пользователем функции:

    ```bash
    mvn compile package
    ```

    Эта команда выполняет сборку и пакеты hello определяемой пользователем функции в hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` файла.

2. Используйте hello `scp` команда toocopy hello файл toohello кластера HDInsight.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Замените `myuser` с hello SSH учетной записи пользователя для кластера. Замените `mycluster` с именем кластера hello. Если вы использовали hello toosecure пароль учетной записи SSH, не требуется запрашиваемые tooenter hello пароль. Если используется сертификат, то может потребоваться toouse hello `-i` параметр toospecify hello файл закрытого ключа.

3. Подключите кластер toohello с помощью SSH.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

4. Из сеанса SSH hello скопируйте файл tooHDInsight hello jar хранилища.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>Использовать hello определяемой пользователем функции из куста

1. Используйте следующие toostart hello Beeline клиента из сеанса SSH hello hello.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Эта команда предполагает, что используется по умолчанию hello **администратора** для учетной записи входа hello для кластера.

2. Как только будет выполнен переход на hello `jdbc:hive2://localhost:10001/>` запрос, введите следующие tooHive определяемой пользователем функции hello tooadd hello и вывести ее в качестве функции.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > Предполагается, что хранилище Azure хранилища по умолчанию для кластера hello. Если кластер использует хранилище Озера данных вместо этого, измените hello `wasb:///` значение слишком`adl:///`.

3. Используйте значения tooconvert определяемой пользователем функции hello, полученные из строк регистром toolower таблицы.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    Этот запрос, выбирает hello платформы устройств (Android, Windows, iOS, т. д.) из таблицы hello преобразовании случая toolower строку hello и их отображения. Hello выходные данные отображаются как toohello следующий текст:

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a>Дальнейшие действия

Другие способы toowork с Hive, в разделе [используйте Hive с HDInsight](hdinsight-use-hive.md).

Дополнительные сведения о функциях Hive User-Defined см. в разделе [Hive операторы и определяемые пользователем функции](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) разделе вики-сайте Hive hello в программами.
